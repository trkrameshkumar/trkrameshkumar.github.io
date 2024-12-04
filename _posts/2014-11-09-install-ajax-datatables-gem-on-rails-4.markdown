---
layout: post
title:  "Install ajax datatables gem on rails 4"
date:   2014-05-09 06:30:00
comments: true
categories: rails datatables
---

This is part 1 of a 2-part tutorial series.

In part one of this tutorial, we will introduce you to these four tools

1. DataTable (Jquery Library)
1. jquery-datatables-rails (Ruby Gem)
1. ajax-datatables-rails (Ruby Gem)
1. kaminari (Ruby Gem)

And We will also teach you how to create a Rails app and integrate it with jquery-datatables-rails and ajax-datatables-rails.


**What is DataTable?**

[DataTable](http://www.datatables.net/) is a plug-in for the jQuery Javascript library. It is a highly flexible tool, based upon the foundations of progressive enhancement, and will add advanced interaction controls to any HTML table.

**What is jquery-datatables-rails?**

[jquery-datatables-rails](https://github.com/rweng/jquery-datatables-rails) is a ruby gem and this packages the jQuery DataTables plugin for easy use with the Rails 3.1+ asset pipleine. It provides all the basic DataTables files, and a few of the extras.

**What is ajax-datatables-rails?**

[ajax-datatables-rails](https://github.com/antillas21/ajax-datatables-rails) is a ruby gem,it helps to enable ajax functionality for datatable, and this gem  makes our life lot easier , without this gem the way to enable ajax on your datatable is very cumbersome , for that i am thanking ajax-datatables-rails.

**What is kaminari?**

[kaminari](https://github.com/amatsuda/kaminari) is a Scope & Engine based, clean, powerful, customizable and sophisticated paginator for modern web app frameworks and ORMs

**Create a new Rails application**

This section will help you create a new Rails application. If you already have an application that you want to integrate with jquery-datatables-rails and ajax-datatables-rails, please skip to [Part 2 The Datatables with ajax functionality](https://github.com/antillas21/ajax-datatables-rails/wiki/Part-2-The-Datatables-with-ajax-functionality).

> First you will need to make sure that you install the Rails gem.

```
gem install rails
```

> Now let’s create our sample Rails app called simple_app.

```
rails new simple_app
```

> and generate a User model:

```
rails generate scaffold User name:string phone:string address:string
```

> Migrate the changes to your database:

```
rake db:migrate
```

> We need some data to show for our simple app, so let’s seed the database with some sample user data. Put the following lines in your db/seeds.rb file.

```
#db/seeds.rb
User.create!(name: 'User1', phone: '111111111', address: "xyz xyz xyz")
User.create!(name: 'User2', phone: '121212121', address: "zyx zyx zyx")
User.create!(name: 'User3', phone: '131313131', address: "zyx zyx zyx")
User.create!(name: 'User4', phone: '141414141', address: "zyx zyx zyx")
User.create!(name: 'User5', phone: '151515151', address: "zyx zyx zyx")
User.create!(name: 'User6', phone: '161616161', address: "zyx zyx zyx")
```

> then run the following in your terminal/command prompt:

```
rake db:seed
```

> Now let’s set up a simple route:

```
# config/routes.rb
Rails.application.routes.draw do
  resources :users
  root 'users#index'

  ...
```

> Now run the server:
```
rails s
```

Now when you visit the app in your browser, at http://localhost:3000, you should see this:

![image from img](https://i.imgur.com/bllQYoO.png)


***

### Integrating ajax-datatables-rails with Rails

Now that we have a Rails app with some data in it, we can start working on integrating ajax-datatables-rails.

> ### Install these three Ruby Gems jquery-datatables-rails, ajax-datatables-rails , and kaminari

Let’s add the necessary gems to our Gemfile:

```
# Gemfile
...

gem 'jquery-datatables-rails', git: 'git://github.com/rweng/jquery-datatables-rails.git', branch: 'master'
gem 'ajax-datatables-rails'
gem "kaminari"
```
> Now run

```
bundle install
```
to install the gems.

> ### Import Datatable Javascript assets

You need to add:
```
//= require dataTables/jquery.dataTables
```
to your` app/assets/javascripts/application.js` file.

> ###  Import Datatable CSS assets

```
*= require dataTables/jquery.dataTables
```

to your` app/assets/stylesheets/application.css` file.

> It is important that it comes after:

```
//= require jquery
```

> Your application.js file should look like this:

```
// app/assets/javascripts/application.js

//= require jquery
//= require jquery_ujs
//= require turbolinks
//= require dataTables/jquery.dataTables
//= require_tree .
```

> It is also important that:

```
//= require_tree .
```

is the last thing to be required.


The reason is, `//= require_tree` . compiles each of the other Javascript files in the javascripts directory and any subdirectories. If you require `dataTables/jquery.dataTables` after everything else, your other scripts may not have access to the `DataTables` functions.


***

**Congratulations**
You now have a working Rails app with Datatable installed. In Next post in this series will tech you how to enable datatables with ajax functionality for your html table. 

Read Part 2 of this turorial series for to enable datatables with ajax functionality
