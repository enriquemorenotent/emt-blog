---
layout: post
title: Creating custom post types in Wordpress
categories: wordpress php
---
It is not seldom that a website needs different kinds of data. Wordpress comes out of the box with "post" and "page", but we might need more.

Many times this is achieved with **categories** since they provide a way of differentiate between the content of the post, in relation with their content.

But what happens if we start adding different data structures to our post? Let's say that we want to define "city profiles" into out Wordpress system. A city might come with very different custom fields. For instance, `location`, `amount of population`, `continent`.

The topic of how to add custom fields is in itself worth of another post, but let's say that we have that as a given. We could separate the posts that represent a city within a "City" category, but that makes the management of data quite hard. One would have to look through all the posts for the needed data  every time, and set the filters properly to reach the post one is looking for.

There is a better way.

First let's register a new kind of post type:

```
// functions.php
<?php

add_action('init', 'register_custom_posts_init');

function register_custom_posts_init() {

    $cities_labels = array(
        'name'               => 'Cities',
        'singular_name'      => 'City',
        'menu_name'          => 'Cities'
    );

    $cities_args = array(
        'labels'             => $cities_labels,
        'public'             => true,
        'capability_type'    => 'post',
        'has_archive'        => true,
        'supports'           => ['title', 'editor']
    );

    register_post_type('city', $cities_args);
}
```

This way we create an structure "City" that will contain all the information. If we look now in the Wordpress backend, we will see that a new menu item has been added, called "Cities". There, we can add all the entries that belong within that data structure, without being disturbed by other kinds of post, and without worrying to set any other kind of flag to set our new data entry.

Now, to query the information, we can do it this way:

```
<?php

$query = new WP_Query([
    'post_type' => 'city',
    'order' => 'ASC',
    'posts_per_page' => 100
]);

$cities = $query->posts;
?>

```

We can query directly by post type, which is a very easy query to write.

How about declaring a "Detail view" of our new post type? Usually for normal posts, we would be using a file `single.php` but since we are using custom post types, we have to declare a file called `single-city.php`. It is inside this file where we will be displaying the information in detail of one entry.

**NOTICE!** One important thing to remember. After creating your new post types, it would be a good idea to go to `Settings > Permalinks` and update the settings there. The configuration might need a flush to recognize the new post type. An error that happened to me too often.

This is a new way of representing data that I will not be forgetting anytime soon, when it comes to Wordpress development.

Cheers
