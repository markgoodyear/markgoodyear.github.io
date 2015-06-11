---
title: "Introducing the vr unit to create simple vertical rhythm—using PostCSS"
excerpt: "Using PostCSS to extend CSS and create a custom vertical rhythm unit"
layout: post
published: true
date: 2015-06-12
---


<p class="lead">With Sass, I use a function to create simple vertical ryhtm—generated from the base line-height—without the complexity of maintaining a baseline grid. With Post CSS, we can take this further and create a new unit.</p>

## Function-able Sass
The Sass (SCSS) function I use is very simple. It essentially returns a multiple of the base line-height to help create vertical rhythm. The function looks a little like this:

{% highlight css %}
$line-height: 32px;

@function vr($amount) {
  @return $line-height * $amount;
}
{% endhighlight %}

And we can use it in our stylesheet like this:

{% highlight css %}
.selector { margin-bottom: vr(2); }
{% endhighlight %}

This will multiply the line-height by the number passed in, so the result here would be `64px`.

## Extending with PostCSS
After digging into PostCSS, I decided to re-create the Sass function with a PostCSS plugin. Because PostCSS is a post-processer, we are able to extend CSS. The result was [postcss-vertical-ryhtym](https://github.com/markgoodyear/postcss-vertical-rhythm/), which replicates the Sass function, but using a custom CSS unit—`vr`—instead of a function. For example:

{% highlight css %}
.selector { margin-bottom: 2vr; }
{% endhighlight %}

This method works more like using plain CSS.

## How do I use the vr unit?

Firstly, install [postcss-vertical-ryhtym](https://github.com/markgoodyear/postcss-vertical-rhythm/) via npm:

{% highlight bash %}
npm install postcss-vertical-rhythm --save-dev
{% endhighlight %}

If you're using gulp, you can then add it to your project like this:

{% highlight js %}
gulp.task('styles', function () {
  return gulp.src('source.css')
    .pipe(postcss(
      require('postcss-vertical-rhythm')()
    ))
    .pipe(gulp.dest('output.css'));
});
{% endhighlight %}

Next, we need to define the base font-size and line-height using the shorthand `font` property:

{% highlight css %}
body {
  font: 1rem/2 sans-serif;
}
{% endhighlight %}

The font-size can be either `em`, `rem`, `px` or `%` based. [postcss-vertical-ryhtym](https://github.com/markgoodyear/postcss-vertical-rhythm/) will parse the property and calculate the `px` line-height value automatically—no variable set up required. In the case above, the line-height would be `32px`.

Once this is set up, we can now use the `vr` unit:

{% highlight css %}
p {
  padding-top: 1vr
  margin-bottom: 2vr;
}
{% endhighlight %}

And with the line-height at `32px` from the above font property, the output is:

{% highlight css %}
p {
  padding-top: 32px;
  margin-bottom: 64px;
}
{% endhighlight %}

[postcss-vertical-ryhtym](https://github.com/markgoodyear/postcss-vertical-rhythm/) also supports decimal values so we can easily use half or quarter values, for example: `.5vr`, `.25vr`.

## Thoughts
If you have any feedback, please leave a comment below or you can find me on [Twitter](https://twitter.com/markgdyr). If you'd like to know more more about PostCSS, I wrote about it <a class="external-link" href="http://bigbitecreative.com/a-look-into-writing-future-css-with-postcss-cssnext/">here</a>. _Happy vertical rhythm-ing!_
