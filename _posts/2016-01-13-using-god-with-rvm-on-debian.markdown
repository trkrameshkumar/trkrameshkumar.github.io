---
layout: post
title:  "Using GOD with RVM on Debian!"
date:   2016-01-13 12:57:00
comments: true
categories: rails god rvm debian
---
God is very powerful and useful tool to monitor process server , to setup god on Debian with RVM we have to follow the following steps. I am assuming you alrady have rvm on your server


* STEP 1 : Install 'god' gem 
* STEP 2 : Insert this line of code "require 'bootstrap-sass'""  in top of config.ru file
* STEP 3 : Create “bootstrap-config.scss” file in /app/assets/stylesheets folder
* STEP 4 : Insert this line of code ' @import “bootstrap”; ' in bootstrap-config.scss file
* STEP 5 : Restart application

Thats it, you are done!
