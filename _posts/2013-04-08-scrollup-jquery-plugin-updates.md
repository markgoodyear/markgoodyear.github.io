---
title: "scrollUp jQuery plugin updates"
excerpt: "A new option has been introduced to allow easily setting an image, rather than resorting to CSS image replacement techniques. Some under the hood optimisations and tweaks have been made, too."
published: true
layout: post
date: 2013-04-08
demo: http://markgoodyear.com/labs/scrollup
download: https://github.com/markgoodyear/scrollup/archive/master.zip
fork: https://github.com/markgoodyear/scrollup
---

<p>A new option has been introduced to allow easily setting an image, rather than resorting to CSS image replacement techniques. Some under the hood optimisations and tweaks have been made, too. <span class="milli">(Thanks to NickRameau for suggestions).</span></p>

{% include post-actions.html %}

## Using images
To use the new image feature simply add the following line to your settings (<a href="http://markgoodyear.com/2013/01/scrollup-jquery-plugin/">see this post for how to install</a>): <code><span class="opt">scrollImg</span>: <span class="val">true</span>
</code> This will prevent any text set in <code>scollText</code> from being visible, allowing you to set a background image in your CSS file — no image replacement techniques needed to hide the the text. Any text set in <code>scrollText</code> will still be used as the link title.

### Example usage

<strong>JavaScript</strong>

{% highlight js %}
$.scrollUp({
  scrollImg: true
});
{% endhighlight %}

<strong>CSS</strong>

{% highlight css %}
#scrollUp {
  bottom: 20px;
  right: 20px;
  width: 38px; /* Width of image */
  height: 38px; /* Height of image */
  background: url(../../img/top.png) no-repeat;
}
{% endhighlight %}

{% include post-actions.html %}
