---
title: "Simplify form testing with Populatr"
date: 2013-09-09
layout: post
excerpt: "Populatr is a JavaScript plugin that will populate any form with pre-defined data to help reduce testing time."
published: true
demo: "http://markgoodyear.com/labs/populatr"
download: "https://github.com/markgoodyear/populatr/archive/master.zip"
fork: "https://github.com/markgoodyear/populatr"

---

<p class="lead">Populatr is a JavaScript plugin that will populate any form with pre-defined data to help reduce testing time.</p>

{% include post-actions.html %}

## What is Populatr?
On a recent project I needed to handle multiple large forms and monitor how the data handled each step of the way. Going through the forms manually is not only tedious, but very time consuming. To overcome this I decided to write a small, lightweight JavaScript plugin which will auto-fill form inputs based on given data.

## Getting started
Populatr is very simple to use. We can use CSS selectors to target a form (ID, class, etc) and for inputs&mdash;including selects&mdash;it targets the `name` attribute. Take the following form for example:

{% highlight html %}
<form id="demo-form">
  <input name="first-name" type="text">
  <input name="last-name" type="text">
  <input name="email" type="email">
</form>
{% endhighlight %}

To populate this form we need to initiate Populatr and then feed in some data:

{% highlight js %}
Populatr.init(true, {
  '#demo-form': {             // CSS selector to select the form
    'first-name': 'Mark',     // 'Input name': 'Input value'
    'last-name': 'Goodyear',
    'email': 'hello@markgoodyear.com'
  }
});
{% endhighlight %}

We initialise Populatr with `Populatr.init()` then pass in if it's active using either `true` or `false`. Following this, we set the data to be used. The data can be passed in as a standard JavaScript object&mdash;as above&mdash;or we can specify an external JSON file, keeping the form data separate and to prevent bloating template files. Using the example above, initiate Populatr with a file to use:

{% highlight js %}
Populatr.init(true, 'populatr.json');
{% endhighlight %}

Then `populatr.json` would look like:

{% highlight js %}
{
  "#demo-form": {
    "first-name": "Mark",
    "last-name": "Goodyear",
    "email": "hello@markgoodyear.com",
  }
}
{% endhighlight %}

_Note: double quotes are required for JSON._

### Multiple forms
Defining multiple forms is possible by passing in multiple objects:

{% highlight js %}
Populatr.init(true, {
  '#form-one': {
    // Form one data...
  },
  '#form-two': {
    // Form two data...
  },
  '#form-three': {
    // Form three data...
  }
});
{% endhighlight %}

### Input types
Most input types are supported, including newer HTML5 inputs. See the [demo](<%= current_page.data.demo %>) for the full range along with an example on populating them.

## Thoughts?
If you have any thoughts, suggestions or issues, please leave a comment below.

{% include post-actions.html %}
