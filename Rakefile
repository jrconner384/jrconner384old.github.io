require 'date'

# Public: Creates a new post file in the _posts directory using the standardized
# form YYYY-MM-DD-<title>.md.
#
# This task will abort if a title is not provided or if the title is not unique.
#
# title       - The title of the new post. This is required or the Rake task
#               will abort.
#
# description - An optional description for the post.
#
# categories  - An optional set of categories. I'm not sure if this behavior is
#               just part of Jekyll or something specific to the setup, but
#               categories are used to create subdirectories in the URL such
#               that the categories 'first second' will nest the post under
#               'first/second/'.
#
# tags        - An optional set of tags to add metadata to the post.
#
# Examples:
#
#   rake post title="Awesomest Post!"
#
#   rake post title="Newer Post!" description="It's newer!" categories="new, ya"
desc 'Creates a new file in _posts of the form YYYY-MM-DD-<title>.md'
task :post do
  abort 'Please provide a title for the new post.' unless ENV['title']

  date = DateTime.now.strftime '%Y-%m-%d'
  slug = ENV['title'].downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  extension = ENV['extension'] ? ENV['extension'] : 'md'
  extension[0] = '' if extension[0] == '.'
  filename = File.join "./_posts/#{date}-#{slug}.#{extension}"

  abort 'Please choose a unique filename.' if File.exist? filename

  File.write filename, post_front_matter
end

# Public: Starts the Jekyll server using the ENV variables included in the call
# to the Rake task as the CLI options. All options available on the command line
# are available through this Rake task.
#
# The options can't be passed on their own, since Rake requires the variables to
# be set to something. They can often be set to something like "true" or "yes"
# if that makes more sense to you but, often, any sort of string will be useful.
#
# There are a few options which use the specific value assigned: limit, port,
# host, and url.
#
# Examples:
#
#   rake serve
#   rake serve verbose="true" force_polling="true" detached="true"
#   rake serve verbose="bananas" force_polling="" detached="sure"
desc 'Starts the Jekyll server using the provided options.'
task :serve do
  options = ''
  options.concat '--future ' if ENV['future']
  options.concat "--limit_posts #{limit} " if ENV['limit']
  options.concat '-w ' if ENV['watch'] || ENV['w']
  options.concat '--no-watch ' if ENV['no_watch']
  options.concat '--force_polling ' if ENV['force_polling'] || ENV['force']
  options.concat '--lsi ' if ENV['lsi']
  options.concat '-D ' if ENV['drafts'] || ENV['D']
  options.concat '--unpublished ' if ENV['unpublished']
  options.concat '-q ' if ENV['quiet'] || ENV['q']
  options.concat '-V ' if ENV['verbose'] || ENV['V']
  options.concat '-B ' if ENV['detached'] || ENV['detach'] || ENV['B']
  options.concat "--port #{ENV['port']} " if ENV['port'] || ENV['P']
  options.concat "--host #{ENV['host']} " if ENV['host'] || ENV['H']
  options.concat "--baseurl #{ENV['url']} " if ENV['url']
  options.concat '--skip-initial-build' if ENV['skip_initial_build']
  %x( `jekyll serve "#{options}"` )
end

# Internal: Provides the standard YAML front-matter block for posts.
# This is basically a string pretending to be a method.
#
# Returns the YAML front-matter block for posts.
def post_front_matter
  fm =      "---\n"
  fm.concat "layout:      post\n"
  fm.concat "title:       \"#{ENV['title']}\"\n" if ENV['title']
  fm.concat "date:        #{DateTime.now.strftime '%Y-%m-%d %H:%M'}\n"
  fm.concat "description: #{ENV['description']}\n" if ENV['description']
  fm.concat "categories:  #{ENV['categories']}\n" if ENV['categories']
  fm.concat "tags:        #{ENV['tags']}\n" if ENV['tags']
  fm.concat "---\n\n"
end
