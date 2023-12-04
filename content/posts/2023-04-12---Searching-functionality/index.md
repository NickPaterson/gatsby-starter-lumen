---
title: "Search Motorbikes Functionality"
date: "2023-12-04T22:34:00Z"
template: "post"
draft: false
slug: "/posts/searching-functionality"
category: "Controllers"
tags:
  - "Controllers"
  - "Models"
  - "Search"
description: "For the search functionality, I decided to watch the Laracast videos on search rather than trying figure it out from the documentation.  And I was surprised how easy this was to do! "
socialImage: "./media/create-200.png"
---

Searching functionality
For the search functionality, I decided to watch the Laracast videos on search rather than trying figure it out from the documentation.  And I was surprised how easy this was to do!
I already had a search bar in the top of the navigation, I updated the action for the search and in the `MotorbikeController.php` file I wrote an if statement to see if there was a search request, and to return a list of bikes that had that in the title.
```
if (request('search')) {
            $motorbikes = Motorbike::where('title', 'like', '%' . request('search') . '%')->get();
            //dd($motorbikes);
            return view('pages/listings', [
                'motorbikes' => $motorbikes,
            ]);
        }
```
I had to create some more listings to test the search, which ended up taking a lot longer than expected, as I had not tested this enough and I had to solve a lot of logic within my code, mainly with the images.  And when updating the motorbike, it was updating a different bike.  In my edit method I had `edit(Request $request, $motorbike) {}` I didn’t specify that the $motorbike was a Motorbike class instance.  So its now `edit(Request $request, Motorbike $motorbike) {}`.
I also suddenly realised, this was the error I was getting earlier with my `MotorbikePolicy`, with the motorbike id getting passed rather than the motorbike object`.  Two birds one stone 😊
Anyway, back to the search!
I added a scope function to the Motorbike Model
```
    public function scopeFilter($query, array $filters)
    {
        $query
            ->where('title', 'like', '%' . request('search') . '%')
            ->orWhere('summary', 'like', '%' . request('search') . '%')
            ->orWhere('description', 'like', '%' . request('search') . '%')
            ->orWhere('make', 'like', '%' . request('search') . '%')
            ->orWhere('model', 'like', '%' . request('search') . '%');
    }
```
And in the `MotorbikeController.php` file I change the `index()` method to: to filter all the posts if there was a search query
```
    public function index() : View
    {
        return view('pages/listings', [
            'motorbikes' => Motorbike::latest()->filter(request(['search']))->get(),
        ]);
    }
```

