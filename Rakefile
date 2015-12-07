    require 'rubygems'
    require 'rake'
    require 'rdoc'
    require 'date'
    require 'yaml'
    require 'tmpdir'
    require 'jekyll'

    desc "Push to github"
    task :push do
        commit = ENV['m']
        system "git add -A"
        system "git commit -m '#{commit}'"
        system "git push"
    end

    desc "Generate blog files"
    task :generate => [:push] do
      #Jekyll::Site.new(Jekyll.configuration({
      #  "source"      => ".",
      #  "destination" => "_site"
      #})).process
      system "bundle exec jekyll build"
    end


    desc "Generate and publish blog to gh-pages"
    task :publish => [:generate] do
      system "mv _site ~/tmp"
      system "mv _assets/vendors ~/tmp"
      system "mv node_modules ~/tmp"
      system "mv db.json ~/tmp"
      system "mv themes ~/tmp"
      system "git checkout -B gh-pages"
      system "rm -rf *"
      system "mv ~/tmp/_site/* ."
      message = "Site updated at #{Time.now.utc}"
      system "git add ."
      system "git commit -am #{message.shellescape}"
      system "git push origin gh-pages --force"
      system "git checkout master"
      system "mv ~/tmp/vendors ./_assets/"
      system "mv ~/tmp/node_modules ./"
      system "mv ~/tmp/themes ./"
      system "mv ~/tmp/db.json ./"
      system "echo yolo"
      system "cat todo.log"
    end

task :default => :publish
