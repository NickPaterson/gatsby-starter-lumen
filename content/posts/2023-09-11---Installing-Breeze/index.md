---
title: "Installing Laravel Breeze"
date: "2023-11-18T20:56:00Z"
template: "post"
draft: false
slug: "/posts/laravel-breeze"
category: "Install"
tags:
  - "Laravel"
  - "Breeze"
description: "Laravel Breeze is a framework for authentication, this framework automatically creates the routes, controllers and views required for user authentication."
socialImage: ""
---

Laravel Breeze is a framework for authentication, this framework automatically creates the routes, controllers and views required for user authentication.
Before installing Laravel Breeze, I committed my code to my GitHub repository, to backup my work as install Laravel Breeze rewrites a lot of your base files.

First you need to install breeze:

`composer require laravel/breeze –dev`

`php artisan breeze:install`

And that’s it! 😊

I had installed [Flowbite](https://flowbite.com/) which helps to create websites faster by using premade components on top of Tailwind CSS.

I didn’t anticipate, how much work it was going to be fixing all the bugs within these components, that installing Breeze had introduced.

As I had already spent most of the day setting up the application, I decided that I would leave the styling issues another day. And because I had left it for over a week, prioritising other projects, I forgot that I had added, styles and scripts into the head of the file to make some of the components for Flowbite to work, like my sidebar opening and closing, so debugging this issue took way longer than it should have done.  Once I had added these back in, it solved a lot of my issues.

Critical reflection: My plan for today was to create controllers for my Motorbike model, but I got caught up fixing styling issues, and fixing the small details that don't really matter ... but its now nearly 9pm, and I have been working on other university projects since 9am!  In hindsight I should have created Breeze during the initial step up of the application, and if I am going to be using Breeze in future applications, I will be sure to do this!
