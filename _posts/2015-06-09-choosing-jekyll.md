---
layout: post
title:  "Choosing Jekyll"
date:   2015-06-09 17:00
categories: jekyll writing
---
Hi, I'm Jason and I write code. And I write _about_ code. It's more challenging than it should be and that's a real shame.

The first and biggest problem is working for companies who tightly guard every single line of code. If I'm going to write about something I found at work, I have to be willing to spend a lot of time redacting anything that might be sensitive or proprietary. It's much easier to write about an ecosystem that the readers can actually move through.

The second problem is in choosing a platform. I've used [Wordpress](https://wordpress.com), which was fine and could be tweaked to show off stuff the way I wanted but it's not really tailored for code. Writing content is also only okay. You can use a word processor-type interface or a subset of HTML which, again, is fine. It's not great, though. I hate formatting my text using word processors and HTML feels more and more chunky to me each year.

##Enter Jekyll##
[Jekyll](jekyllrb.com) has a lot going for it but here's how it won me over:

- It uses [Markdown](https://help.github.com/articles/github-flavored-markdown/) right out of the box.
- It's written in [Ruby](http://www.ruby-lang.org)
- It's [open source](https://github.com/jekyll/jekyll)
- It's the platform used by [GitHub Pages](https://pages.github.com/)

#Markdown#
First off, this is the cleanest markup language I've used. I am in no way an expert on markup languages but I definitely know what I like. Markdown has very little syntactic noise which makes it easy to read _and_ write. For example, the links I've included are written like so:

`[Jekyll](jekyllrb.com)`

The same content in HTML would look more like this:

{% highlight html %}
<a href="jekyllrb.com">Jekyll</a>
{% endhighlight %}

It might not seem like a huge deal but imagine seeing that little extra bit of overhead duplicated dozens of times per page across hundreds of pages.

Next, it's really easy to write code in Markdown. Jekyll adds a little flavor using [Liquid](https://github.com/Shopify/liquid/wiki) and [Pygments](http://pygments.org/) for syntax highlighting. That makes it easy for me to write code samples like this one from my [OpenInteger](https://github.com/jrconner384/open_integer) gem:

{% highlight ruby %}
# Public: Finds the lowest prime factor of the receiver.
#
# Returns the lowest prime factor of the receiver or nil if the receiver has
# no prime factors.
def lowest_prime_factor
  top = (Math.sqrt self).to_i

  Prime.each top do |prime|
    return prime if prime.factor_of? self
  end
end
{% endhighlight %}

#Ruby#
While I'm talking about low overhead, I need to plug Ruby. Like Markdown, it's not overburdened with repetitious grammar. It has an amazing community which is always churning out brilliant tools.

#Open Source#
My instinct was to write that I didn't _need_ an open source tool but that's not exactly true. I've used proprietary and open source software and I've always had an easier time working with open source. It means that I can let the framework do what it does out of the box or hack it inside out to bend to my will. It also means that others will hack it and come up with all kinds of fun tools and extensions.

#GitHub Pages#
As a programmer, I love the idea of GitHub Pages. All of the work I've hosted online is at GitHub already so making a site in that same ecosystem is super appealing to me. I can write about my work where my work is.

##Conclusion##
This is just about my incipient love affair with this platform. I hope this can  help you if you're choosing a platform or are curious about someone else's thought process.

I'll do a write up about my experience setting up Jekyll and my GitHub Page pretty soon so, if you're interested in the platform, I'll take you through it.
