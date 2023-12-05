---
title: "Setting up Laravel Web Application"
date: "2023-11-02T22:12:03.284Z"
template: "post"
draft: false
slug: "/posts/setting-up-laravel"
category: "Install"
tags:
  - "Open source"
  - "Laravel"
  - "Set Up"
description: "Once my raspberry pi was up and running, with PHP and MySql already installed it was time to get started with Laravel."
socialImage: "./media/application-ready.png"
---
## Setting up Laravel

Having successfully set up my Raspberry Pi and detailed the process in a previous post titled [Setting up a Rasberry Pi](https://blog.nickpaterson.dev/posts/setting-up-a-rasberry-pi),here PHP and MySQL were already configured, my focus shifted to initiating Laravel, a prominent PHP web application framework crafted by [Taylor Otwell](https://twitter.com/taylorotwell). Recognized for its elegant syntax facilitating streamlined web development, Laravel presented an efficient solution for building web applications.

To get started with Laravel, the first essential software was Composer, a PHP package manager simplifying dependency management for Laravel projects. The installation involved a single command in the project's terminal:

`php composer-setup.php --install-dir=bin --filename=composer`

To access Composer globally, the following command moves the composer file to the /usr/local/bin directory:

`mv composer.phar /usr/local/bin/composer`

With Composer installed, the next step was to install the Laravel installer globally, a command line tool that simplifies the process of creating new Laravel projects, by using the following command:

`laravel new project-name`


At this point I was encounted an error: mkdir(): Permissions denied

![mkdir(): Permission denied](./media/mkdir-permissions.png)
Figure 1: Permission denied

Using linux `ll` command to list the names of the files, with permissions  and groups information.  I saw that the www folder was owned by the root user, which was denying Laravel access to create a new directory in the www directory.

![Directory Information](./media/root-dir.png)
Figure 2: /var directory information

I created a www-data group and changed the owner using linux `chown` command.

![Directory Information](./media/chown-permissions.png)
Figure 3: /var/www direcorty information

Typing in the `laravel new project` again! This time it worked! I have successfully created a Laravel project, hosted on my Raspberry Pi.

![Application Ready](./media/application-ready.png)
Figure 4: Application read message info

## Conclusion

Installing Laravel should be easy.  However, an error, "mkdir(): Permissions denied," popped up, pointing to an issue with the ownership of the www folder. A quick check using the Linux `ll` command revealed that the www folder belonged to the root user, causing hiccups in creating directories.

To fix this, I set up a www-data group and tweaked ownership using the chown command. With these adjustments, the Laravel project creation went off without a hitch. The conclusion of this process meant a Laravel project successfully hosted on my Raspberry Pi
