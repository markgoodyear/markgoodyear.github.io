---
title: "Using ES6 with gulp"
excerpt: "Learn how to use ES6 in your gulpfile"
layout: post
published: true
date: 2015-06-24
---

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
To leverage ES6 you will need to install Babel as a dependancy to your project:

{% highlight bash %}
npm install babel --save-dev
{% endhighlight %}

Once this has finished, we need to instruct gulp to use Babel. To do this, we need to rename the `gulpfile.js` to `gulpfile.babel.js`:

{% highlight bash %}
mv "gulpfile.js" "gulpfile.babel.js"
{% endhighlight %}

We can now use ES6! An example of a typical gulp task using new ES6 features:

{% highlight javascript %}
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


