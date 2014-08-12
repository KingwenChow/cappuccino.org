---
title: First Post, Thanks to Middleman
tags: programming
published: true
---



## Hello world!

I had been meaning to create a personal website for some time now and it's finally here!

I've had this domain up and running a Ruby on Rails app hosted on Heroku, but it was more than what I needed for a personal site.
I never got much further than making an alternate [homepage](/drew.html) for myself about my best friend.
Finally, I had some convincing to really get the site going, thanks to [Middleman](http://middlemanapp.com).

%READMORE%

I was introduced to Middleman by a friend who had hung out with him before.
I found out that Middleman helps you generate static sites via Ruby and the [Sinatra](http://www.sinatrarb.com) web framework.
After realizing that I could create a **free** custom static blog site with the help of Middleman and Github, I became close friends with Middleman.
We are besties now.


<img src="http://ww2.sinaimg.cn/large/dce48faejw1ej12ywt50mj20p00ge756.jpg" alt="middleman" class="blockimg"/>
## Why Middleman?
- **Flexible** - you can add whatever code/gems you want
- **Fast** - well, he spits out HTML, CSS, and Javascript; is there anything faster?
- **Simple** - it's fast because it's simple, no database or backend
- **Cheap** - Middleman and his components are open source and you can host a static site somewhere like [Github](https://github.com) for free
- **Safe** - since it's a static site there are fewer ways for someone to destroy it
- **Light** - it doesn't give you that bloated feeling, it's just the right proportion
- **Familiar** - that is if you've used Ruby on Rails or the like before
- **Ruby** - seriously an awesome language, for scripting and building websites
- **Markdown** - the blog add-in allows you to write all your articles in [Markdown](http://daringfireball.net/projects/markdown)
- **Live Reload** - save a file and the browser will automatically refresh with your changes, really useful when writing Markdown
- **Flexible Again** - because you can use stuff like [Haml](http://haml.info), [Sass](http://sass-lang.com), [CoffeeScript](http://coffeescript.org) etc. in any editor you want \**cough [Vim](http://www.vim.org) cough*\*

## How He Conducts Business
Middleman is professional, clean cut and the coolest guy in the office. 
He runs on the light Sinatra and serves flat HTML rather than dynamic pages.
You can write Ruby code to fill out your HTML files allowing less code to be written and more flexibility.
Things like partials, templates, and helpers allow you to keep your site better organized.
Then you just tell Middleman to build out your site to folders containing HTML, CSS, Javascript and images.
The blogging feature is done via writing plain Markdown files with parameters.
Middleman will turn them in HTML and put them where they need to go.
If you have experience with Ruby on Rails then this will be a breeze.

## How Do We Become Friends?
First you need to understand [Ruby and RubyGems](http://code.tutsplus.com/articles/ruby-for-newbies-working-with-gems--net-18977). 
Then you can start your relationship with Middleman by opening up Terminal. 
You will need you install the Middleman gem first.
Then run a Middleman init to get a blog ready version of Middleman in the current directory.
That's all the setup required, so you can start Middleman and navigate to [http://localhost:4567](http://localhost:4567).

```
$ gem install middleman
$ middleman init BLOGNAME --template=blog
$ cd BLOGNAME
$ middleman
```

From here you can see that Middleman provides you with an example article and a way to browse your articles by date and tag.
This is your start page that will uses paginate to list all your blog articles.
You can easily move the code in ``source/index.html.erb`` to something like ``source/blog.html.erb`` if you'd like a home page other than the blog.
I found that moving the blog articles into a subdirectory will also keep the project a little better organized.

## Gemfile
The gemfile is where you can specify which gems for Middleman to use.
I prefer to use Haml, Sass and CoffeeScript. 
Not only do each of these use indentation to specify blocks and lack semicolons, but the each have their own additional features that make building a website that much more enjoyable.
To use these I simply add the gems to my Gemfile, run ``bundle install``, and use ``.haml`` instead of ``.html``, ``.sass`` instead of ``.css`` and ``.coffee`` instead of ``.js``.
Below is my gemfile for this site.

``` ruby
source "http://rubygems.org"

gem "middleman", "~> 3.3.3"
gem "middleman-blog", "~> 3.5.3"
gem "middleman-favicon-maker", "~> 3.7"
gem "middleman-livereload", "~> 3.3.4"
gem "middleman-gh-pages", "~> 0.0.3"
gem "middleman-syntax", "~> 2.0.0"
gem "builder", "~> 3.2.2"
gem "tzinfo-data", "~> 1.2014.5"
gem "sass", "~> 3.2.17"
gem "haml", "~> 4.0.5"
gem "coffee-script", "~> 2.2.0"
gem "redcarpet", "~> 3.1.2"
gem "wdm", :platform => [:mswin, :mingw]
```

## Config File
Here is where you introduce yourself to ``source/config.rb``.
It's Middleman's instructions on how to create your site.
I know you just met but he's used to being told what to do.
You can change different settings and store helper methods for your site.

### Blog Settings
All of the blog settings are in the config file.
If you initialized the site with the blog template then the ``middleman-blog`` gem should already be in the ``Gemfile``.
To change something like the directory of your blog you will need to change ``blog.prefix`` to your desired subfolder name.
*Note* I have mine configured to ``source/blog``.
You can also change other blog settings like ``summary_separator``, which indicates to Middleman where an article should stop when calling ``article.summary``.
For this article I placed "README" before my "Why Middleman?" header.
Middleman strips out the seperator when rendering the full ``article.body`` and preview ``article.summary``.

``` ruby
# Blog settings
activate :blog do |blog|
  blog.prefix = "blog"
  blog.default_extension = ".md"
  blog.calendar_template = "calendar.html"
  blog.tag_template = "tag.html"
  blog.taglink = "{tag}.html"
  blog.year_link = "{year}.html"
  blog.month_link = "{year}/{month}.html"
  blog.day_link = "{year}/{month}/{day}.html"
  blog.permalink = "{year}/{month}/{day}/{title}.html"
  blog.sources = "{year}-{month}-{day}-{title}.html"
  blog.layout = "article_layout"
  blog.summary_separator = /(%READMORE%)/
  blog.summary_length = -1
  blog.paginate = true
  blog.per_page = 10
  blog.page_link = "page/{num}"
end
```

### Live Reload
I highly recommend using Middleman's live reload feature for a better development experience.
When enabled, he sits there watching attentively for any saved changes you make and tells your browser to refresh.
It evens works when connected to the development site from a mobile device so you can live test your site on a different platform.
For example, if your computer is at 10.0.1.1 then you could access your development at 10.0.1.1:4567 on a mobile device.
Just make sure the ``middleman-livereload`` gem is in your ``Gemfile`` and add the following to ``config.rb``.

``` ruby
# Reload the browser automatically whenever files change
activate :livereload
```

### Relative Links 
Relative assets, links, and paths tell Middleman to convert the path given to a relative path.
For example, lets say I want to grab the image at ``source/images/sloth.png``.
I would link to the image with ``/images/sloth.png``.
Middleman would then convert the link to a relative path like ``../../images/sloth.png`` depending on the path currently being visited.
This feature is **required** if you are going to host your site with Github pages.
Add the following to ``config.rb``.

``` ruby
# Use relative links
activate :relative_assets
set :relative_links, true
set :relative_paths, true
```

### Pretty URLs
Middleman supplies all his friends with free URL makeovers.
He can turn an ugly URL like ``/contact.html`` into something beautiful like ``/contact``.
Middleman does this by creating subfolders for each page, renaming the page to ``index.html`` and placing it in the subfolder.
Take advantage of this greatness with the following in ``config/rb``.

``` ruby
# Pretty URLs
activate :directory_indexes
```

## Layouts and Partials
Middleman is an excellent listener and you'll never have to tell him the same thing twice.
Layouts and partials allow you to specify HTML once and use it on multiple pages. 

### Layouts
Middleman will start you out with a default site layout at ``source/layout.erb`` that is wrapped around each page.
Just put some HTML around a ``yield`` and Middleman will take care of the rest.
The following is my layout at ``source/layouts/layout.haml``, which Middleman knows to use as the default layout.

``` haml
!!! 5
%html
  = partial "partials/head"
  %body{ class: "#{page_classes}" }
    = partial "partials/nav"
    #main= yield
    = partial "partials/footer"
```

### Partials
Partials allow you to render a snippet of HTML on any page.
You can see in my layout above I am rendering partials for the head, nav and footer of my site.
I simply create a file at ``source/partials/_nav.haml`` and tell Haml to render the file at the top of my site.

### Nested Layouts
Middleman grants you the power to create a stack of layouts.
I used this feature for rendering individual articles, both summary and full views.
To do this, you will first need to create the new layout at ``source/layouts/article_layout.haml``. 

``` haml
= wrap_layout :layout do
  %article
    = partial "partials/article", locals: { article: current_article }
```

Then apply this layout to all articles by adding the following to your ``config.rb``.

``` ruby
# Custom layout for articles
page "blog/../*", layout: :article_layout
```

Notice that I'm using a partial to render an individual article, so the articles look the same on an article page and when viewing a list of articles.
When I call this partial I pass the article in and I can also pass an optional variable to indicate if I want the article summary rendered.
The following is my article partial. 

``` haml
- summary ||= false

.article{ class: ("summary" if summary) }
  .title= link_to article.title, article
  .date= article.date.strftime('%b %e, %Y')
  - if summary
    = article.summary
    - if article.summary != article.body
      %p= link_to "Read more", article
  - else
    = article.body
    = partial "partials/disqus"
```

## Comments With Disqus
Disqus is an easy way to add commenting to your articles.
Don't worry, Disqus and Middleman go way back.
Simply [signup](https://disqus.com/admin/signup/?utm_source=New-Site) and follow the instructions.
When you are ready to paste the Disqus Javascript you can create a Disqus partial as I did and render it as above.
Notice I only include the Disqus partial when rendering the full article.

## Build That Site
Well this is the super easiest thing ever. Just run the following command and watch as Middleman generates your static site and places it in ``build/``.

```
$ bundle exec middleman build
```

## Hosting With Github Pages
Now you can bascially host that static site on any webserver, but I found [Github Pages](https://pages.github.com) convenient, free and easy to use.
This is especially nice if you are already using Github to track your site.
Remember that relative links, paths, and assests are **required** when hosting on Github.

First you'll need to create a Github account and add you site to source control.
Make sure you add ``/build`` to your ``.gitignore`` before commiting.

Next you will need to add the ``middleman-gh-pages`` gem to the ``Gemfile``.
Then the following to the ``Rakefile``.

``` ruby
require "middleman-gh-pages"
```

To deploy, make sure that all your changes are committed and run the following commands to build and publish the site.
This will push the static pages created from the build to the ``gh-pages`` branch of your Github project.

```
$ bundle exec rake build
$ bundle exec rake publish
```

Then you can check out your site at http://USERNAME.github.io/BLOGNAME.
You now have a free, fast, flexible blog site!
Just create some new blog articles and start publishing.
You can also configure a custom domain with the project by following these [instructions](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages).

## All Done
To be completely honest, writting this article took just as long as creating my Middleman website.
I do believe Middleman and I will stay friends for quite a while.

You can view the [source](https://github.com/flipxfx/flipxfx/tree/e712a293671617556e2da3e26e51f2a39a5929f3) of my website at the time of writting this article.

And if you need more info on Middleman you can check out the superb [documentation](http://middlemanapp.com/basics/getting-started).
