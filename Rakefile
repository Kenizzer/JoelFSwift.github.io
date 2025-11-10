# From: https://github.com/ainc/awesomeinc2013/blob/master/Rakefile

require "rubygems"
require "tmpdir"

require "bundler/setup"
require "jekyll"

ENV["JEKYLL_ENV"] = "production"

desc "Generate site files"
task :generate do
  Jekyll::Site.new(Jekyll.configuration({
    "source"      => ".",
    "destination" => "_site"
  })).process
end

desc "Build and publish site to GitHub Pages"
task :publish => [:generate] do
  Dir.mktmpdir do |tmp|
    cp_r "_site/.", tmp

    pwd = Dir.pwd
    Dir.chdir tmp

    system "git init"
    system "git add ."
    message = "Site updated at #{Time.now.utc}"
    system "git commit -m #{message.inspect}"

    # ✅ Use your real repo and correct branch
    system "git branch -M main"
    system "git remote add origin git@github.com:joelfswift/joelfswift.github.io.git"
    system "git push -f origin main"

    Dir.chdir pwd
  end
end
