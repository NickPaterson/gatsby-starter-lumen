---
title: "Creating a Motorbike Controller"
date: "2023-11-19T20:03:00Z"
template: "post"
draft: false
slug: "/posts/creating-motorbike-controller"
category: "Dev"
tags:
  - "Laravel"
  - "Artisan"
  - "Controller"
description: "Following the Laravel docs, I created a controller for the Motorbike listings"
socialImage: " "
---
Following the Laravel docs, [Laravel Contollers]( https://laravel.com/docs/10.x/controllers) I executed the following artisan command to automatically create a boilerplate controller for me
`php artisan make:controller MotorbikeController`
This created a `MotorbikeController.php` file in the `Http/Controllers` directory.
Withing this class I created the following methods, to return all motorbikes and a single motorbike:
```
// show all motorbikes
    public function index(): View
    {
        return view('pages/listings', [
            'motorbikes' => Motorbike::all()
        ]);
    }

    // show a single motorbike
    public function show(Motorbike $motorbike): View
    {
        return view('pages/motorbike', [
            'motorbike' => $motorbike
        ]);
    }
```
And updated the `web.php` routes file:
```
Route::get('/listings', [MotorbikeController::class, 'index']);
Route::get('/motorbikes/{motorbike}', [MotorbikeController::class, 'show']);
```
At this point I wanted to create the functionality to upload a motorbike
I created a blade file for the form, and updated the `MotorbikeController`
```
    // create a motorbike
    public function create(Request $request): View
    {
        $categoryController = new CategoryController();
        $categories = $categoryController->findAll();

        return view('motorbikes/create', [
            'categories' => $categories,
            'request' => $request,
        ]);
    }
```
I created a separate file for the motorbike routes:

```
<?php

use App\Http\Controllers\MotorbikeController;
use Illuminate\Support\Facades\Route;

/*
|--------------------------------------------------------------------------
| Motorbike Routes
|--------------------------------------------------------------------------
|
*/

Route::get('/listings', [MotorbikeController::class, 'index']);
Route::get('/motorbikes/{motorbike}', [MotorbikeController::class, 'show']);

Route::get('/motorbikes/create', [MotorbikeController::class, 'create']);

Route::post('/motorbike', [MotorbikeController::class, 'store'])->middleware(['auth', 'verified'])->name('motorbike.store');
Route::patch('/motorbikes', [MotorbikeController::class, 'store'])->middleware(['auth', 'verified'])->name('motorbikes.store');

require __DIR__.'/auth.php';

```
With this I was getting a 404 error. After a lot of debugging, I eventually figured out that the order of the routes are important:
```
Route::get('/listings', [MotorbikeController::class, 'index']);
Route::get('/motorbikes/create', [MotorbikeController::class, 'create']);

Route::get('/motorbikes/{motorbike}', [MotorbikeController::class, 'show']);

Route::post('/motorbike', [MotorbikeController::class, 'store'])->middleware(['auth', 'verified'])->name('motorbike.store');
Route::patch('/motorbikes', [MotorbikeController::class, 'store'])->middleware(['auth', 'verified'])->name('motorbikes.store');

```

I added a store method in the `MotorbikesController`:
```
// store a motorbike
    public function store(Request $request): View
    {
        $motorbike = new Motorbike();
        $motorbike->user_id = Auth::id();
        $motorbike->category_id = $request->category;
        $motorbike->title = $request->title;
        $motorbike->slug = 'slug';
        $motorbike->thumbnail_url = 'https://loremflickr.com/320/240';
        $motorbike->summary = $request->summary;
        $motorbike->description = $request->description;
        $motorbike->make = $request->make;
        $motorbike->model = $request->model;
        $motorbike->engine = $request->engine;
        $motorbike->year = $request->year;
        $motorbike->price = $request->price;
        $motorbike->save();
        return view('pages/motorbike', [
            'motorbike' => $motorbike
        ]);
    }
  ```

For now some of the values are hard coded … I plan to create the slug from the title and to solve the issue with it being unique, my plan is to use the user id in the url for example `/motorbikes/userid/slug` and for the images I will create a new table, model and controller for this …
I tested the form upload with inputting test into most of the fields. It worked! 😊

![Test-upload]('./media/testupload.png')
