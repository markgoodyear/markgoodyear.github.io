---
title: "Retinfy your Craft site with Retinafy plugin."
excerpt: "Retinafy is a small plugin for Craft. Its aim is to provide a simple way to generate the required images and markup for a retina screen."
layout: post
published: true
date: 2015-03-14
download: "https://github.com/markgoodyear/craft-retinafy/archive/master.zip"
fork: "https://github.com/markgoodyear/craft-retinafy"
---

<p class="lead">Retinafy is a small plugin for Craft CMS. Its aim is to provide a simple way to generate the required images and markup for a retina screen.</p>

## How it works
Retinafy uses the `srcset` attribute, which lets us define different sized images to display depending what screen the user is browsing with. It uses the common `2x` definition which lets us display a higher resolution image for retina screens.

To let Retinafy know which images are intended to be used for retina purposes, they will need to have an `@2x` suffix, e.g. `image-name@2x.png`. This signifies the intent of the image, and allows us to still upload non-retina images if a higher resolution isn't available.

## Usage
Once installed, there are two ways to call Retinafy. The first is via a Craft variable, and the second being a Twig filter. Firstly, the Craft Variable:

{% highlight html %}
{% raw %}
<img src="{{ craft.retinafy.image(assetFieldName) }}" alt="">
{% endraw %}
{% endhighlight %}

And the Twig filter:
{% highlight html %}
{% raw %}
<img src="{{ assetFieldName | reftinafy }}" alt="">
{% endraw %}
{% endhighlight %}

Both ways perform exactly the same function, so it's a matter of preference for which method to use.

By default, Refinafy will create the 1x non-retina version of the uploaded `@2x` image. This  will be used as the `src` attribute and the original `@2x` image will be used as the `srcset`. For example if we upload a 500 x 500 `@2x` image, Retinfafy will create a 250 x 250 version, and the markup generated would be:

{% highlight html %}
{% raw %}
<img src="[generated-image-250x250]" srcset="[original-image-500x500] 2x">
{% endraw %}
{% endhighlight %}

Any browser supporting `scrset` will then display the correct image based upon the display. A handy place to find out what browser support for this is at [caniuse](http://caniuse.com/#search=srcset). Retinafy doesn't provide any polyfills, however it gracefully degrades as any browser that doesn't support `srcset` will get the non-retina version. Polyfills can be added manually if desired.

### Using transforms
Transforms are a powerful feature of Craft. Retinafy can utilise existing transforms, and if the image is big enough to display a 2x version of the transform, it will be added to the `srcset` attribute. To use a transform, we can pass it into the Craft variable, or Twig filter:

{% highlight html %}
{% raw %}
<!-- Craft variable -->
<img src="{{ craft.retinafy.image(assetFieldName, 'transformHandle') }}">

<!-- Twig filter -->
<img src="{{ assetFieldName | reftinafy('transformHandle') }}" alt="">
{% endraw %}
{% endhighlight %}

Providing the uploaded image is equal too—or larger than—2x the transform size, it will create the `@2x` version. As an example, if we have a transform set at 250 x 250, it will create a 500 x 500 image, and the generated markup would be:

{% highlight html %}
{% raw %}
<img src="[transform-250x250]" srcset="[transform-2x-500x500] 2x">
{% endraw %}
{% endhighlight %}

## Download
You can find the plugin on [GitHub](https://github.com/markgoodyear/craft-retinafy), and is also available to install through the [Directory](https://dukt.net/craft/directory) plugin. If you have any questions, let me know in the comments below or give me a [Tweet](http://twitter.com/markgdyr).

Enjoy Retinafying!
