---
layout:      post
title:       "Bootstrapping Jekyll"
date:        2015-06-11 19:33
tags:        Ruby Jekyll
---
As promised in [Choosing Jekyll]({% post_url 2015-06-09-choosing-jekyll %}), I'm going to go through the dirty details of setting this up.

##Hacking it Together##
In my last post, I wrote that one of the reasons I chose Jekyll is that it's written in Ruby. You don't need to know Ruby to use Jekyll and you can even do a lot of this work using any of a number of languages or just do it by hand but we're not cavemen.

#Making Posts#
Out of the box, Jekyll makes you manually add your post files which is a little annoying since it requires the file to be named a certain way. To streamline the process, I use [Rake](https://github.com/ruby/rake) to define a task which generates the file for me using the expected format.

You can always check out my [Rakefile](https://github.com/jrconner384/jrconner384.github.io/blob/master/Rakefile) to see the full extent of the tasks I'm automating but I'll cover the important parts of generating a posts file in detail here.

#Rake is Ruby#
The first thing to know is that Rake is a Ruby tool so you write tasks in Ruby. Since I'm making a Rake task to generate post files, I'll obviously want to be able to call it like this:

`rake post title="My brand new post!" categories="automation, Ruby"`

So I go under the hood to define the task. I started with a vanilla Jekyll install so I didn't have a Rakefile. I remedied this the obvious way, by adding a file named "Rakefile" at the root of the Jekyll directory.

__Protip__: Rakefile is spelled exactly like that and conventially has a capital R, though I accidentally found out that isn't required. Even though the tasks are written in Ruby, there isn't a file extension, not even .rb.

#The First Task#
Here's the boilerplate for a Rake task. The `desc` call is optional, in the stricted syntactical sense, but you should feel bad if you leave it out.

{% highlight ruby %}
desc 'Creates a new file in _posts of the form YYYY-MM-DD-<title>.md'
task :post do
  # ...do stuff like build up your file name, perform validations, etc.
end
{% endhighlight %}

At this stage, you can do a couple of things from the CLI with this task. If you open a terminal, navigate to the root of your blog, and write `rake -T`, it'll print a nice list of the tasks in your Rakefile using the `desc` test to define the _what_ of the thing.

`rake post   # Creates a new file in _posts of the form YYYY-MM-DD-<title>.md`

You can even call `rake post` at the CLI and it won't blow up. That at least proves that the Rake program recognized `post` as a task it can perform. So now that I've got something Rake knows about, I have to actually make it do something.

#Validating#
So I can't create a file without a filename and it's not the sort of thing I wanted to let the program choose for me. To keep the interface moving smoothly, I added a validation which guarantees that the task was fed a title for the post. It's easy to do in one line:

{% highlight ruby %}
abort 'Please provide a title for the new post.' unless ENV['title']
{% endhighlight %}

This confirms that the title environment variable is defined like so: `rake post title="Validations are Useful!"`.

#Naming the File#
So, to strike a balance between customizability and ease-of-use, I made the task choose the rest of the file name. To get the datestamp for the front of the file, I used the excellent `strftime` function to format the date the way Jekyll expects.

{% highlight ruby %}
date = DateTime.now.strftime '%Y-%m-%d'
{% endhighlight %}

Next, create a slug out of the post's title so the filename plays nicely with more filesystems and so we don't have to worry about escaping characters in the URL. Basically, downcase it all for readability, replace spaces with hyphens, and remove non-word characters.

{% highlight ruby %}
slug = ENV['title'].downcase.strip.gsub(' ', '-').gsub(/[^w-]/, '')
{% endhighlight %}

Finally, Voltron it together into the full filename. Notice that the task automatically gives the file the .md extension since that's what I write these posts in. I could easily change the task to let me define a different extension if I wanted but, I don't want that functionality for now.

{% highlight ruby %}
filename = File.join "./_posts/#{date}-#{slug}.md"
{% endhighlight %}

#More Validations?#
Yes, it's true. I'd prefer to do all of the validations up front but I needed to get through that section above to determine the file name. The syntax for this validation closely follows the first one.

{% highlight ruby %}
abort 'Please choose a unique filename.' if File.exist? filename
{% endhighlight %}

A more robust variation on this would prompt the user to enter a different name, confirm overwriting the post with that name, or cancel and do something else. That's why developers exist, though, and I'll improve this code down the line somewhere.

#So...Where's My File?#
The last step here is to actually create the file. This is yet another really simple thing to do.

{% highlight ruby %}
File.write filename, post_front_matter
{% endhighlight %}

Remember that `filename` was defined above, so the only thing left is `post_front_matter`.

#Set Us Up The Defaults#
The very last thing I had my task do is spit out some YAML front-matter. Front-matter is a topic all its own, so I'll just cover what front-matter I want my task to generate.

Except for `layout`, I used guard clauses to add a line if the appropriate variable was added. That way, if I decide to not add a description, there won't be a junk line in the block (i.e. `description: ""`).

{% highlight ruby %}
def post_front_matter
  fm =      "---\n"
  fm.concat "layout:      post\n"
  fm.concat "title:       \"#{ENV['title']}\"\n" if ENV['title']
  fm.concat "date:        \"#{DateTime.now.strftime '%Y-%m-%d %H:%M'}\"\n"
  fm.concat "description: \"#{ENV['description']}\"\n" if ENV['description']
  fm.concat "categories:  \"#{ENV['categories']}\"\n" if ENV['categories']
  fm.concat "---\n"
end
{% endhighlight %}

#Putting It All Together#
Here it is all in one place. This may be more verbose than it needs to be, in the strictest sense, but that just means I have an opportunity to out-clever myself.

{% highlight ruby %}
desc 'Creates a new file in _posts of the form YYYY-MM-DD-<title>.md'
task :post do
  abort 'Please provide a title for the new post.' unless ENV['title']

  date = DateTime.now.strftime '%Y-%m-%d'
  slug = ENV['title'].downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  filename = File.join "./_posts/#{date}-#{slug}.md"

  abort 'Please choose a unique filename.' if File.exist? filename

  File.write filename, post_front_matter
end

def post_front_matter
  fm =      "---\n"
  fm.concat "layout:      post\n"
  fm.concat "title:       \"#{ENV['title']}\"\n" if ENV['title']
  fm.concat "date:        \"#{DateTime.now.strftime '%Y-%m-%d %H:%M'}\"\n"
  fm.concat "description: \"#{ENV['description']}\"\n" if ENV['description']
  fm.concat "categories:  \"#{ENV['categories']}\"\n" if ENV['categories']
  fm.concat "---\n"
end
{% endhighlight %}
