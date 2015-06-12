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
# categories  - An optional comma-separated list of categories. These can be
#               considered analogous to tags.
#               The categories section of the YAML front-matter block will look
#               exactly the same as the variable passed through the CLI. If it
#               is given the string "blog article", the YAML front-matter will
#               show `categories: "blog article"` even if the intent is for each
#               word to appear as its own tag.
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
  filename = File.join "./_posts/#{date}-#{slug}.md"

  abort 'Please choose a unique filename.' if File.exist? filename

  File.write filename, post_front_matter
end

# Public: Starts the Jekyll server using the ENV variables included in the call
# to the Rake task as the CLI options. All options available on the command line
# are available through this Rake task.
#
# Examples:
#
#   rake serve
#   rake serve verbose force_polling detached
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
  fm.concat "description: \"#{ENV['description']}\"\n" if ENV['description']
  fm.concat "categories:  \"#{ENV['categories']}\"\n" if ENV['categories']
  fm.concat "---\n"
end