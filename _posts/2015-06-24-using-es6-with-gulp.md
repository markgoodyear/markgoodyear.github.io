---
title: "Using ES6 with gulp"
excerpt: "Learn how to use ES6 in your gulpfile"
layout: post
published: true
date: 2015-06-24
updated: 2015-11-02
---

<div class="callout  callout--info  callout--small">
  <em><strong>Nov 2nd, 2015</strong></em><br>
  <ul class="callout__list">
    <li>
      As of node 4, we're now able to use ES2015 without the need for Babel. However modules are not currently supported so you'll need to use `require()` still. Checkout the <a href="https://nodejs.org/en/docs/es6/">node docs</a> for more info on what's supported. If you'd like module support and to utilise Babel, read on.
    </li>

    <li>
      Post updated to use Babel 6.
    </li>
  </ul>
</div>

<p class="lead">With gulp 3.9, we are now able to use ES6 (or ES2015 as it's now named) in our gulpfile—thanks to the awesome Babel transpiler.</p>

Firstly make sure you have at least version 3.9 of both the CLI and local version of gulp. To check which version you have, open up terminal and type:

{% highlight bash %}
gulp -v
{% endhighlight %}

This should return:

{% highlight bash %}
CLI version 3.9.0
Local version 3.9.0
{% endhighlight %}

If you get any versions lower than 3.9, update gulp in your `package.json` file, and run the following to update both versions:

{% highlight bash %}
npm install gulp && npm install gulp -g
{% endhighlight %}

### Creating an ES6 gulpfile
To leverage ES6 you will need to install Babel (make sure you have Babel 6) as a dependency to your project, along with the es2015 plugin preset:

{% highlight bash %}
npm install babel-core babel-preset-es2015 --save-dev
{% endhighlight %}

Once this has finished, we need to create a `.babelrc` config file to enable the es2015 preset:

{% highlight javascript %}
touch .babelrc
{% endhighlight %}

And add the following to the file:

{% highlight javascript %}
{
  "presets": ["es2015"]
}
{% endhighlight %}

We then need to instruct gulp to use Babel. To do this, we need to rename the `gulpfile.js` to `gulpfile.babel.js`:

{% highlight bash %}
mv "gulpfile.js" "gulpfile.babel.js"
{% endhighlight %}

We can now use ES6 via Babel! An example of a typical gulp task using new ES6 features:

{% highlight javascript %}
'use strict';

import gulp from 'gulp';
import sass from 'gulp-sass';
import autoprefixer from 'gulp-autoprefixer';
import sourcemaps from 'gulp-sourcemaps';

const dirs = {
  src: 'src',
  dest: 'build'
};

const sassPaths = {
  src: `${dirs.src}/app.scss`,
  dest: `${dirs.dest}/styles/`
};

gulp.task('styles', () => {
  return gulp.src(paths.src)
    .pipe(sourcemaps.init())
    .pipe(sass.sync().on('error', plugins.sass.logError))
    .pipe(autoprefixer())
    .pipe(sourcemaps.write('.'))
    .pipe(gulp.dest(paths.dest));
});
{% endhighlight %}

Here we have utilised ES6 [import/modules], [arrow functions], [template strings] and [constants]. If you'd like to check out more ES6 features, [es6-features.org] is a handy resource.

[import/modules]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import

[arrow functions]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions

[constants]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const

[template strings]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings

[es6-features.org]: http://es6-features.org/


