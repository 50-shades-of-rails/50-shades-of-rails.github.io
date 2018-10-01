---
layout: post
title:  "Chapter 1 - New Application"
date:   2018-09-30 21:14:46 +0100
categories: chapter-1
---

In this chapter we will generate the basic Rails application config and
some Frontend setup so we can start explaining some more advanced
concepts.

> I'll not explain everything in details as this
> basic concepts are already covered in first few chapters of book [Agile web development with Rails](https://books.google.sk/books/about/Agile_Web_Development_with_Rails.html?id=Qq9nQgAACAAJ&source=kp_book_description&redir_esc=y)
> But please don't feel discouraged I'll make sure further chapters
> about Backend development are explained better

I assume you have Ruby version `2.5.1`
[installed](https://www.ruby-lang.org/en/documentation/installation/)
on your machine.

Let's install [Rails](https://rubyonrails.org/) framework

{% highlight bash %}
gem install rails
{% endhighlight %}

Now lets generate new project. As explained in previous article the project name will be **Century a day**
We will generate project without standard
rails tests. This is due to fact that later in the project we will
install [RSpec](http://rspec.info/)

{% highlight bash %}
rails new  centuryaday --skip-test
{% endhighlight %}

> `rails new` is providing lot of more option I'll not
> explain here. You can check the out with `rails new --help`.
> For example there is `--api` option to generate API only application.

`rails new` will generate project files.
After the command is finished let's get into the folder install
necessary gems and lunch the server:

{% highlight bash %}
cd centuryaday
bundle install
rails server
{% endhighlight %}

Now if we visit in our browser `http://localhost:3000`  you should see
default welcome page of a new Rails project saying `Yay! You’re on Rails!`

> Commit progress: `de80abd63c9420e87738027495f5ea00ee5f20ed`
> [Chapter 1](https://github.com/50-shades-of-rails/century-a-day/tree/chapter1)

### Intalling gems for testing

Now let's add some esential gems for writing tests. We will use
[rspec-rails gem](https://github.com/rspec/rspec-rails) and while we at
it we will install [Factory bot gem](https://github.com/thoughtbot/factory_bot)

Add this lines to `Gemfile`

{% highlight bash %}
# Gemfile
# ...
group :development, :test do
  # ...

  gem 'rspec-rails'
  gem 'factory_bot_rails'
end
{% endhighlight %}


... and run `bundle install`

After the gems were installed run:

{% highlight bash %}
rails generate rspec:install
{% endhighlight %}

...this will create `spec` folder and setup RSpec in our Rails app


Now if you run `rspec spec` we should see message `0 examples, 0 failures`
marking our RSpec successfully installed

> Commit progress:  `38dc554676932e54d57a4751ed93f372b3420c22` in
> [Chapter 1](https://github.com/50-shades-of-rails/century-a-day/tree/chapter1)

### Create welcome page

Now lets replace the `Yay! You’re on Rails!` landing website with something
meaningful. We will generate controller for handling marketing pages
named `PagesController`

{% highlight bash %}
rails g controller pages landing
{% endhighlight %}

...which generate:

{% highlight bash %}
      create  app/controllers/pages_controller.rb
       route  get 'pages/landing'
      invoke  erb
      create    app/views/pages
      create    app/views/pages/landing.html.erb
      invoke  rspec
      create    spec/controllers/pages_controller_spec.rb
      create    spec/views/pages
      create    spec/views/pages/landing.html.erb_spec.rb
      invoke  helper
      create    app/helpers/pages_helper.rb
      invoke    rspec
      create      spec/helpers/pages_helper_spec.rb
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/pages.coffee
      invoke    scss
      create      app/assets/stylesheets/pages.scss
{% endhighlight %}


Now lets tell Rails routing the `PagesController` action `landing` is
the new root page in `config/routes.rb`:

{% highlight ruby %}
# config/routes.rb
Rails.application.routes.draw do
  root 'pages#landing'
end
{% endhighlight %}

Now if we load `localhost:3000` in our browser we should see:

![Pages#landing - Find me in app/views/pages/landing.html.erb]({{ site.url }}/assets/chapter01-pages-landing-state1.png)

> Commit progress:  `c12c5f9f537d664a283709f26ed2477a63982c3f` in
> [Chapter 1](https://github.com/50-shades-of-rails/century-a-day/tree/chapter1)


### Adding CSS and JS libraries

We need to make our web app project pretty. In order to do that we will
use [Materialize](https://materializecss.com) HTML+CSS framework and
some good old [jQuery](https://jquery.com/)

> Note to advanced Frontend Developers: To understand why I'm not implementing any
> fancy SPA solution please read my [Prologue article]({% post_url 2018-09-29-prologue-welcome-to-50-shades-of-rails %})

In our `Gemfile` add:

```ruby
# Gemfile

# ...
gem 'materialize-sass'
gem 'jquery-rails'
gem 'jquery-ui-rails'
# ...
```

...and run `bundle install`


#### JavaScript config

Once that is set up go to `app/assets/javascript/application.js`
and change:

```
// ...
//
//= require rails-ujs
//= require activestorage
//= require turbolinks
//= require_tree .
```

...to:

```
// ...
//
//= require jquery
//= require jquery-ui
//= require rails-ujs
//= require activestorage
//= require turbolinks
//= require materialize
//= require_tree .
```

> the order of some libraries names may be important

#### CSS config

CSS is bit more tricky as we need to tell rails we want to use SCSS to
load our files. To do that rename `app/assets/css/application.css` to `app/assets/css/application.scss`

> if you didn't spot the change we changed `.css` to `.scss`

And change the content of `app/assets/css/application.scss` to:

```scss
@import "jquery-ui";
@import "materialize";
@import "https://fonts.googleapis.com/icon?family=Material+Icons";
```

I'm not going to explain in details why this is needed as it's Frontend
stuff and this tutorial will be mainly about Backend.

> Make sure you restart the rails server after this changes.


> Commit progress:  `71d0c31ac05a98d731ea009cd7edfcfaeaf653d4` in
> [Chapter 1](https://github.com/50-shades-of-rails/century-a-day/tree/chapter1)

### Changing the layout

### Wrap up this chapter
