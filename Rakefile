require "rubygems"
require "tmpdir"

require "bundler/setup"
require "jekyll"


# Change your GitHub reponame
GITHUB_USERNAME = "ningsuhen"
GITHUB_REPONAME = "ningsuhen.github.io"

GITHUB_REPOPATH = "#{GITHUB_USERNAME}/#{GITHUB_REPONAME}"
TMP_PATH = "/Users/ningsuhen/.tmp/"


desc "Generate blog files"
task :generate do
  Jekyll::Site.new(Jekyll.configuration({
    "source"      => ".",
    "destination" => "_site"
  })).process
end


desc "Generate and publish blog to gh-pages"
task :publish => [:generate] do
    mkpath TMP_PATH
    pwd = Dir.pwd
    Dir.chdir TMP_PATH
    system "git clone git@github.com:#{GITHUB_REPOPATH}.git"
    Dir.chdir pwd
    cp_r "_site/.", "#{TMP_PATH}/#{GITHUB_REPONAME}/", :remove_destination => true

    Dir.chdir "#{TMP_PATH}/#{GITHUB_REPONAME}/"

    system "git add ."
    message = "Site updated at #{Time.now.utc}"
    system "git commit -m #{message.inspect}"
    system "git push origin master"

    Dir.chdir pwd
  #end
end