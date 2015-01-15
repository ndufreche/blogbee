Day 3: the Content model
======================

In the last episods:

 - [Day1: Setup and install BackBee](https://github.com/backbee/blogbee/blob/day1-doc/doc/day1.md)
 - [Day2: Bootstrap of BlogBee project](https://github.com/backbee/blogbee/blob/day2-doc/doc/day2.md)

Introduction
---------------

BackBee is a complete and flexible content management system. If architecture is a bit complex to understand, you will see that it is subsequently very easy to quickly build any type of website.


What for today?
-------------------

Today we will learn how BackBee manages content. This will be a somewhat difficult day and we recommend you to reread this tutorial to understand the system. By late afternoon, you will understand how to integrate the templates that we built in the second day and have created our layouts for our pages.

The "big picture"
--------------------

Let's start with a schema which represent the BackBee architecture of our *Article page*:

![the BackBee big picture](http://i.imgur.com/sLLJ19x.png "the BackBee big picture")

Each element have his object representation inside **BackBee core library**:

 - **Site** (``BackBuilder\Site\Site``) is your application.
 - **Page** (``BackBuilder\NestedNode\Page``) represent each page of your application, for example for blogbee have three pages: home page, article page and author page.
 - **Layout** (``BackBuilder\Site\Layout``) represent the layout of a page.
 - **ContentSet** (``BackBuilder\ClassContent\ContentSet``) represent the blocs/columns of your layouts, there are blocs can be editables by user.
A *ContentSet* inside a *Layout* have some properties:
  - ``inherited``
  - ``height`` and ``width``
  - ``accept``: the contents you can put inside it
  - main
 - **Content** (``BackBuilder\ClassContent\AContent``) represent a simple data: this can be a text, a date, a link... *BackBee core library* provide some of them (``ClassContent/Element`` directory inside ``BackBuilder``) and you can do your owns.

Let's go a little further in the architecture of our website: we want to display an article. We can represent an article like a container of simple content elements:

 - A title: a text element decorated by ``<h1>`` or ``<h2>`` tags.
 - An abstract: a short text element decorated by ``<p>`` or ``<div>`` tags.
 - A picture header which is at least a path with a description, a title and an "alt" argument if we consider it as an ``<img>`` tag.
 - Of course, a *body* which will probably contains some rich content. This can be a ``<div>`` or an HTML5 ``<article>`` tag, but you may probably want more like add social network sharing features or add an "ad". Let's try to be flexible for this part. 
 
  ![BackBee architecture of an article](http://i.imgur.com/IZYN945.png "BackBee architecture of an article")

As you can see, we have created a ``ContentSet`` called "article" which contains what we need at this point on the left big column which is also a ``ContentSet``.

Inside article ``ContentSet``, we will set some ``Content Elements`` like formatted texts and picture.
Also, we need to let the body flexible so we create a new ``ContentSet`` for the body, which for now only contain a *paragraph* text element.

We will create the complete structure of our pages on **Day 4**, for now let's create our layouts.

Layout creation
-------------------

It's time to work!

Connect to BackBee "Edition mode" and select **Templates** tab on top of the editor.
We will have two layouts in *BlogBee*:
* A "two-columns" layout, for home and article pages
* A "main-column" layout for author related pages

Luckely, BackBee embed a lot of common layouts  and the layouts we need are already provided by the CMS.
Click on "Others templates", and select "Default template" which is only composed of one single column.

![Author layout](http://i.imgur.com/LUQTsiv.png "Author layout")

Edit the Template name and set it to *Author*.

Look at your ``repository/Layouts`` folder:

    repository/
        Layouts/
            Article.twig
            Home.twig
            Author.twig


A new ``Author.twig`` (empty file) has been generated, where we will insert our previous Bootstrap 3 templates from **Day 2**.





Final thoughts
============



