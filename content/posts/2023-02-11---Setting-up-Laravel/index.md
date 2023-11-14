---
title: "Setting up Laravel Web Application"
date: "2023-11-02T22:12:03.284Z"
template: "post"
draft: false
slug: "/posts/setting-up-laravel"
category: "Set Up"
tags:
  - "Open source"
  - "Laravel"
  - "Set Up"
description: "Once my raspberry pi was up and running, see my post: ![Setting up a Rasberry Pi](../2023-20-10---Setting-Up-A-Raspberry-Pi/index.md), with PHP and MySql already installed it was time to get started with Laravel."
socialImage: ""
---


Once my Raspberry Pi was up and running, see my post on [Setting up a Raspberry Pi](https://blog.nickpaterson.dev/posts/setting-up-a-raspberry-pi) with PHP and MySQL already installed, it was time to get started with Laravel.

Laravel is a popular PHP web application framework, created by ![Taylor Otwell](https://twitter.com/taylorotwell). Laravel is known for its elegant and exprssive syntax, which simplifies common web development tasks, making it easier and more efficient to build web applications.

To get started, I needed Composer, a PHP package manager.  Composer is a crucial tool for laravel development as it simplifies the process of managing the projects dependencies.

With Composer installed, the next step was to install the Laravel installer globally, a command line tool that simplifies the process of creating new Laravel projects, by using the command laravel new project-name.

At this point I was encounted an error: mkdir(): Permissions denied

![mkdir(): Permission denied](./media/mkdir-permissions.png)

Using linux ll command to list the names of the files, with permissons and groups information.  I saw that the www folder was owned by the root user, which was denying access for laravel to create a new directory in the www directory.

![Directory Information](./media/root-dir.png)

I created a www-data group and changed the owner using linux chown command.

![Directory Information](./media/chown-permissions.png)

Typing in the laravel new project again! This time it worked! I have successfully created a Laravel project, hosted on my Raspberry Pi.

![Application Ready](./media/application-ready.png)
