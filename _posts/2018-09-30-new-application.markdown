---
layout: post
title:  "New Rails Application"
date:   2018-09-30 21:14:46 +0100
categories: chapter-1
---

I assume you have Ruby version `2.5.1`
[installed](https://www.ruby-lang.org/en/documentation/installation/)
on your machine.

Let's install Rails framework

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
default welcome page of a new Rails project.

> Work was committed in  `de80abd63c9420e87738027495f5ea00ee5f20ed`


