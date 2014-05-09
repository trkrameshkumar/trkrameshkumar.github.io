---
layout: post
title:  "How to integrate bootstrap with Ruby on Rails!"
date:   2014-05-09 06:37:00
categories: blog update
---
Twitter Bootstrap is one of the defacto tool for web developers to build responsive and modern web applications , to integrate bootstrap with ruby on rails we have to follow the following steps.


* STEP 1 : Install 'bootstrap-sass' gem
* STEP 2 : Insert this line of code "require 'bootstrap-sass'""  in top of config.ru file
* STEP 3 : Create “bootstrap-config.scss” file in /app/assets/stylesheets folder
* STEP 4 : Insert this line of code ' @import “bootstrap”; ' in bootstrap-config.scss file
* STEP 5 : Restart application

Thats it, you are done!
