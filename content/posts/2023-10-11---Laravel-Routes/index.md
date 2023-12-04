---
title: "Laravel Routes"
date: "2023-10-12T09:30:00Z"
template: "post"
draft: false
slug: "/posts/laravel-routes"
category: "Routes"
tags:
  - "Laravel"
  - "Routes"
description: ""
socialImage: "./media/listings.png"
---

In Laravel, routes serve as a crucial component for defining the entry points of your web application. They determine how HTTP requests should be handled and which controllers or closures should respond to them. Laravel's routing system is powerful, allowing developers to create clean and expressive URLs, organize code effectively, and implement various middleware for additional functionalities.

Laravel provides you with a `web.php` routes file, I wanted to try and keep the code as clean as possible, so I created a custom `motorbike.php` routes file and at the bottom of the `web.php` I included `require __DIR__.'/motorbike.php';` code.
In the `motorbike.php` file in included the following code

```
Route::get('/listings', [MotorbikeController::class, 'index']);
Route::get('/motorbikes/{slug}', [MotorbikeController::class, 'show']);

Route::middleware('auth')->group(function () {
    Route::get('/motorbike/create', [MotorbikeController::class, 'create']);
    Route::post('/motorbike/create', [MotorbikeController::class, 'store'])->name('motorbike.store');
    Route::get('/motorbike/edit/{slug}', [MotorbikeController::class, 'edit'])->name('motorbike.edit');
    Route::put('/motorbike/edit/{slug}', [MotorbikeController::class, 'update'])->name('motorbike.update');
    Route::delete('/motorbike/{motorbike}', [MotorbikeController::class, 'destroy'])->name('motorbike.destroy');
});
```
The `/listings` and `/motorbike/{slug}` will be accessible by everyone visiting the website.
However the routes handling the CRUD operations for the motorbike are inside the `Route::middleware`  to ensure the user is authenticated before performing any actions.
