---
title: "Create an on-demand sticky header with Headhesive.js"
excerpt: "Headhesive.js is a lightweight, fully customisable JavaScript plugin for creating an on-demand sticky header."
layout: post
published: true
date: 2014-04-07
demo: "http://markgoodyear.com/labs/headhesive"
download: "https://github.com/markgoodyear/headhesive/archive/master.zip"
fork: "https://github.com/markgoodyear/headhesive"
---

<p class="lead">Headhesive.js is a lightweight, fully customisable JavaScript plugin for creating an on-demand sticky header.</p>

{% include post-actions.html %}

For a recent project I needed to create a sticky header that was only visible after a certain point on the page. I found a few plugins available, some relied on jQuery, some had many extra features that weren’t necessary. Whilst jQuery isn't always a bad thing, I was looking for a lightweight, dependency-free solution. Headhesive.js was created.

## What does it do?
Headhesive.js creates an *on-demand* sticky header that will appear after a specific scroll distance, or at a certain element. No dependancies and no fancy extra frills to get in your way. It works exactly how you tell it.

## How to use
First of all you'll need to include the `headhesive.min.js` file in your footer, then create an instance using any element:

{% highlight js %}
var header = new Headhesive('.header');
{% endhighlight %}

This instantiates Headhesive.js on the `.header` element, using the default options—*see the [readme](https://github.com/markgoodyear/headhesive.js/blob/master/README.md#options) for more info on options*. Upon instantiating, the `.header` element will be cloned with the class `.headhesive--clone`. In this example, the cloned element will look like this:

{% highlight html %}
<div class="header headhesive--clone">
  <!-- header elements will be cloned inside -->
</div>
{% endhighlight %}

No styles are injected via the plugin, keeping the plugin lightweight and as user customisable as possible. To create a basic hide/show effect we need to add some CSS magic to the cloned element:

{% highlight css %}
.headhesive--clone {
  position: fixed;                   /* fix the element */
  top: 0;                            /* make sure it's at the top */
  transform: translateY(-100%);      /* move it off screen */
  transition: all 300ms ease-in-out; /* add animation */
}
{% endhighlight %}

We shift the element off-screen by setting the `transform: translateY` property to `-100%`. Alternatively, we could use a negative margin to move the element off-screen. I prefer `transform` as there is no need to define any heights, and it works perfectly in IE9.

When reaching the target scroll distance, the class `.headhesive--stick` is added. We can use this and create some styles to show the element:

{% highlight css %}
.headhesive--stick {
  transform: translateY(0%); /* move it back on screen */
}
{% endhighlight %}

We now have an on-demand sticky header!

## Further customisation
Please check out the [Headhesive.js project on GitHub](https://github.com/markgoodyear/headhesive.js/) for an always up-to-date guide on the options, methods, along with a downloadable demo.

If you have any questions or find an issue, please leave a comment below, or you can find me on [Twitter](https://markgoodyear.com/markgdyr).

{% include post-actions.html %}
