require "rubygems"
require "tmpdir"

require "bundler/setup"
require "jekyll"


# Change your GitHub reponame
GITHUB_REPONAME = "ningsuhen/ningsuhen.github.io"


desc "Generate blog files"
task :generate do
  Jekyll::Site.new(Jekyll.configuration({
    "source"      => ".",
    "destination" => "_site"
  })).process
end

 #   FileUtils.mkpath "/Users/ningsuhen/.tmp/ningsuhen.github.io/"
 # Dir.mktmpdir do |tmp|



desc "Generate and publish blog to gh-pages"
task :publish => [:generate] do
    pwd = Dir.pwd
    Dir.chdir "/Users/ningsuhen/.tmp/"
    system "git clone git@github.com:#{GITHUB_REPONAME}.git"
    Dir.chdir pwd
    cp_r "_site/.", "/Users/ningsuhen/.tmp/ningsuhen.github.io/", :remove_destination => true


    Dir.chdir "/Users/ningsuhen/.tmp/ningsuhen.github.io/"

    #system "git init"
    system "git add ."
    message = "Site updated at #{Time.now.utc}"
    system "git commit -m #{message.inspect}"
    #system "git remote add origin git@github.com:#{GITHUB_REPONAME}.git"
    system "git push origin master"
    #--force

    Dir.chdir pwd
  #end
end