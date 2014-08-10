---
title: "BrowserBlast 2: Relaunch"
layout: post
excerpt: "BrowserBlast 2 relaunched, departing ways from jQuery&mdash;faster and more reliable. Rebuilt in vanilla JS and using Microsofts recommended methods, it ensures rock solid, fast, IE detection."
published: true
date: 2013-02-13

demo: http://markgoodyear.com/labs/browserblast
download: https://github.com/markgoodyear/BrowserBlast/archive/master.zip
fork: https://github.com/markgoodyear/browserblast
---

<p class="lead">BrowserBlast 2 relaunched, departing ways from jQuery&mdash;faster and more reliable.</p>

To make the previous browserBlast even faster and more reliable, it’s been rebuilt entirely in JS, without needing to rely on jQuery. Using Microsofts recommended methods it ensures rock solid IE detection.

{% include post-actions.html %}

Also changed is separating CSS from the JS so it’s even easier to customise. This means by default, all styling is placed in your CSS file for ultimate control.

## How to use

Simply include the `browserBlast.min.js` and add the following to the **footer:**


{% highlight js %}
browserBlast();
{% endhighlight %}

## Settings

A list of all the settings with the defaults

{% highlight js %}
browserBlast({
  devMode: false, // Show warning on all browsers for testing
  supportedIE: '8', // Supported IE version, warning will display on older browsers
  message: "Hey! Your browser is unsupported. Please upgrade for the best experience." // Set custom message
});
{% endhighlight %}
{% include post-actions.html %}
