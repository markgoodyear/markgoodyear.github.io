---
title: "scrollUp jQuery plugin"
layout: post
published: true
date: 2013-01-22
demo: http://markgoodyear.com/labs/scrollup
download: https://github.com/markgoodyear/scrollup/archive/master.zip
fork: https://github.com/markgoodyear/scrollup
---

<p class="lead">ScrollUp is a lightweight jQuery plugin to create a customisable "Scroll to top" feature that will work with any website, with ease.</p>

Recently whilst working on a client project I was required to implement a "Scroll to top" feature to make it easy for the user to get back to the top of the page. I decided to take this further and turn it into a fully customisable jQuery plugin to work with any site.

<div>
<p><em><strong>Update 08/04/2013</strong>: ScrollUp updated to v1.1. <a href="http://markgoodyear.com/2013/04/scrollup-jquery-plugin-updates/">Read more here.</a></em></p>
</div>

{% include post-actions.html %}

## How to use

Simply include the `jquery.scrollUp.min.js` file and place the following in the head of your document (make sure jQuery is included):

### Minimum setup

{% highlight js %}
$(function(){
  $.scrollUp();
});
{% endhighlight %}

### Example with default options

{% highlight js %}
$(function () {
  $.scrollUp({
    scrollName: 'scrollUp', // Element ID
    topDistance: '300', // Distance from top before showing element (px)
    topSpeed: 300, // Speed back to top (ms)
    animation: 'fade', // Fade, slide, none
    animationInSpeed: 200, // Animation in speed (ms)
    animationOutSpeed: 200, // Animation out speed (ms)
    scrollText: 'Scroll to top', // Text for element
    activeOverlay: false, // Set CSS color to display scrollUp active point, e.g '#00FFFF'
  });
});
{% endhighlight %}

### activeOverlay

To create a visible line to help determin an ideal scroll distance from the top, assign a valid CSS colour to the `activeOverlay` setting. This could be HEX, HSLA or RGB(A). Example: `activeOverlay: '#00FFFF'`. [See the demo for an example](<%= current_page.data.demo %>).


## Fully Customisable

ScrollUp is fully customisable through CSS which makes it simple to fit right into your project. Simply target the scrollUp's generated ID in your CSS file and set your styles. Below is a basic style example:

{% highlight css %}
#scrollUp {
  bottom: 20px;
  right: 20px;
  padding: 10px 20px;
  background: #555;
  color: #fff;
}
{% endhighlight %}

[Check out the demo](<%= current_page.data.demo %>) for more style and feature examples.

{% include post-actions.html %}
