---
title: "Static Awesomeness"
layout: post
published: true
date: 2013-05-27
---

<p class="lead">Remember the days of no databases and just pure HTML files? They had many advantages, however managing content and templates isn't ideal. Enter static site generators.</p>

Recently, I was all set for a re-design in WordPress when I came across static site generator, Jekyll, which GitHub uses to generate its static pages for repositories. Because it uses no databases, *everything* can be stored in version control. Awesome.

Jekyll is primarily for blogging, however I wanted the ability to expand in the future should I feel the need to&mdash;perhaps by adding on a portfolio section or any other dynamic content types. I then stumbled across [Middleman](http//middlemanapp.com), which is like a suped up Jekyll.

## Who's the Middleman?
Middleman is a static site site generator which includes built-in features such as Sass, Haml, CoffeeScript, Markdown, LiveReload and many more that work straight out of the box with little or no configuration needed. With the ability to create multiple blogs, this is perfect to use for a portfolio section. It's also extensible with many [useful extensions](http://directory.middlemanapp.com/#/extensions/all).

Middleman is a little more involved to get set up, requiring use of Terminal and some basic Ruby knowledge. Knowing this, and armed without any Ruby knowledge, I managed to get set up pretty quick and found it relatively painless&mdash;so don't let it put you off. There is a great [walkthrough](http://middlemanapp.com/getting-started/) on the Middleman site, which explains how to install and set-up a new project.

### How does it work?
It's simple. My site has two folders: `source` and `build`. All my templates/Sass files are in the `source` folder, which are then compiled into flat HTML and CSS files in the `build` folder when I'm ready to deploy. I then deploy the `build` folder to my server and that's it. No database synching to worry about.

## Why Static?
Static sites have many benefits, such as being super fast due to no querying databases or generating dynamic pages. As mentioned, being able to store the whole site&mdash;including content&mdash;in version control is awesome.

Being static HTML files means you can host pretty much anywhere. For instance you can use [GitHub](http://github.com) to host static HTML sites for free, which works great when using Git.

There's also less security issues with static files too—I'm sure anyone who's dealt with WordPress (and perhaps other database driven CMS's) will be thankful of.

## Other options
There are many other static site generators, some made in PHP if you don't fancy Ruby. Another tool to watch out for is [mixture.io](http://mixture.io). It has many similarities to Middleman, but without requiring the command line. It also runs on Windows too! I'd recommend checking it out.

If you don't want to go fully static but like the idea of no databases, there's also flat file CMS's, which store all content in text files rather than a database. One option is [Kirby](http://getkirby.com), and another one that's becoming increasingly popular is [Statamic](http://statamic.com/). I've not used either of these yet, but both look worth checking out.
