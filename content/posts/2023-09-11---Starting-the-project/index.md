---
title: "Installing Laravel and Tailwind"
date: "2023-11-09T13:00:00.284Z"
template: "post"
draft: false
slug: "/posts/installing-laravel-and-tailwind"
category: "Install"
tags:
  - "Set Up"
  - "Laravel"
  - "Tailwind"
description: "I created a new Laravel project locally on my machine and created a GitHub repo to back up my work. With the idea of deploying the application once it has been completed."
socialImage: "./media/root-dir.png"
---

## Starting the application

As I was having performance issues with my Raspberry Pi, I created a new Laravel project locally on my machine and created a GitHub repo to back up my work. With the idea of deploying the application once it has been completed.

Following the same steps as before I had a basic Laravel application.  This time I wanted to include a design framework; I went with Tailwind: [Install-Tailwind-CSS-with-Larvel](https://tailwindcss.com/docs/guides/laravel).

The installation was straightforward, using the terminal in the project’s directory execute the following commands:
```npm install -D tailwindcss postcss autoprefixer```
```npx tailwindcss init -p```

A tailwind.config.js file should have been created, copying the following code into this file:
```
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./resources/**/*.blade.php",
    "./resources/**/*.js",
    "./resources/**/*.vue",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```
Code Block 1: Tailwind config


In the app.css file:
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```
Code Block 2: Applications main stylesheet


Making sure that the following line of code is added to the head of every page in your application:
``` @vite('resources/css/app.css')```

To run this in the development mode use the command `npm run dev` in the terminal, and also open a new terminal to run the Laravel project too `php artisan serve`
