---
title: "Automating your workflow with Grunt"
layout: post
excerpt: "Learn how to automate your workflow with Grunt, reducing all those tedious tasks you repeat multiple times a day."
published: true
date: 2013-07-30
---

<p class="lead">Learn how to automate your workflow with Grunt, reducing all those tedious tasks you repeat multiple times a day.</p>

## The need for automation

Recently I've been looking to improve my workflow to automate the tasks I repeat on a day-to-day basis. I also wanted to standardise projects across a team, set up a project structure and make sure the necessary tasks are done correctly. CodeKit has served me well, however there remain a few issues I wanted to address; the ability to automate more and be able to work cross-platform without needing to configure different apps to match a project structure. Say hello to [Grunt](http://gruntjs.com/).

## What is Grunt?
To sum up Grunt, it's a task runner built on [Node.js](http://nodejs.org/)—*don't let this put you off!* Node.js is simple to install—just visit the site, download the install package and run it. If you're on Mac, you can also install it with [Homebrew](http://brew.sh/). You'll then want to install the Grunt CLI. I won't go into great detail as they have a great [getting started guide](http://gruntjs.com/getting-started), so to summarise:

1. Make sure Node.js is installed. This will also install the Node Package Manager (NPM).
2. Install the Grunt CLI globally. `npm install -g grunt-cli`.
3. You'll then need to create two files in the root of your project, `package.json` and `Gruntfile.js`. I'll explain what these two files do next.

_Before I continue, it's worth noting you may need to run some install commands as admin. For example, Mac users will need to use `sudo`:_

{% highlight bash %}
sudo npm install -g grunt-cli
{% endhighlight %}

## Setting up your project
The `package.json` file contains all the information about the project, such as the name and version. It also lists the dependancies used by the project. A basic `package.json` will look like this:

{% highlight js  %}
{
  'name': 'project-name',
  'version': '0.1.0',
  'devDependencies': {
    'grunt': '~0.4.1',
  }
}
{% endhighlight %}

This is basically telling us the project name, version number (using the [Semantic Versioning](http://semver.org/) system) and that `grunt` is a required dependency. To install dependencies, simply run:

{% highlight bash %}
npm install
{% endhighlight %}

This installs all dependencies to the `node_modules` folder.

## Configuring Grunt tasks
Now we move onto setting up the `Gruntfile.js` file. It can become quite a large file if there are lot of tasks, so to start off I'll demonstrate a basic task which will compile your Sass (.scss) files. Firstly, you will need to install the [Sass plugin](https://github.com/gruntjs/grunt-contrib-sass):

{% highlight bash %}
npm install grunt-contrib-sass --save-dev
{% endhighlight %}

Adding `--save-dev` to the command automatically adds it to your `package.json` file so you don't need to worry about adding it manually. Below is a basic configuration to compile Sass—including a development config and a distribution config.


{% highlight js  %}
// Wrapper function
module.exports = function(grunt) {

  // Read package.json
  grunt.file.readJSON('package.json');

  //Initialize grunt
  grunt.initConfig({

    // Sass task
    sass: {

      // Sass development options
      dev: {
        options: {
          style: 'expanded',
        },
        files: {
          'css/main.css': 'css/sass/global.scss'
        }
      },

      // Sass distribution options
      dist: {
        options: {
          style: 'compressed'
        },
        files: {
          'css/main.css': 'css/sass/main.scss'
        }
      }
    },

  });



  // Load tasks
  grunt.loadNpmTasks('grunt-contrib-sass');


  // Create Default Task
  grunt.registerTask('default', [
    'sass:dev' // Compile Sass with dev settings
  ]);

  // Create Distribution Task
  grunt.registerTask('dist', [
    'sass:dist' // Compile Sass with distribution settings
  ]);
}
{% endhighlight %}

If you're familiar with JavaScript and JSON, it should be simple enough to understand. If not, it's not as scary as it may look! Let's take a closer look at what's going on...


### The wrapper function

{% highlight js  %}
// Wrapper function
module.exports = function(grunt) {

  // Read package.json
  grunt.file.readJSON('package.json');

  //Initialize grunt
  grunt.initConfig({
    [...]
  });

}
{% endhighlight %}

The wrapper function contains two key parts. Firstly to read the project details we specified earlier in `package.json` and then to initialize the Grunt configuration. This is where we configure Grunt tasks.

### Task configuration

So, our Sass task looks a little like this:

{% highlight js  %}
// Sass task
sass: {

  // Sass development options
  dev: {
    options: {
      style: 'expanded',
    },
    files: {
      'css/main.css': 'css/sass/global.scss'
    }
  },

  // Sass distribution options
  dist: {
    options: {
      style: 'compressed'
    },
    files: {
      'css/main.css': 'css/sass/global.scss'
    }
  }
},
{% endhighlight %}

Here we have two tasks configured within the Sass task, `dev` and `dist`. Both these are able to have custom options passed through, meaning it's possible to compile Sass differently based on its environment. _How awesome is that?_

Keeping it simple, I've only set up one option which is basically telling Grunt how to compile for each environment. Of course, there are many more options available which can be found at the plugins [GitHub](http://github.com/gruntjs/grunt-contrib-sass) page. This is the same for all Grunt plugins—be sure to check their respective GitHub pages for a full list of options.

After setting up the options, we tell Grunt the destination file `css/main.css` and the source file `css/sass/global.css`. You can use the `css/sass/global.scss` to import all other Sass files in the project:

{% highlight js  %}
files: {
  'css/main.css': 'css/sass/global.scss'
}
{% endhighlight %}

### Loading the tasks

Before Grunt can run the tasks, we need to load them—each dependency will need to be loaded in the same way. This is simply done by the following:

{% highlight js %}
grunt.loadNpmTasks('grunt-contrib-sass');
{% endhighlight %}




### Creating the tasks

Next, we create the actual tasks which we run from Terminal. Below is a set up for both development and distribution tasks.

{% highlight js  %}
// Create Default Task
grunt.registerTask('default', [
  'sass:dev' // Compile Sass with dev settings
]);

// Create Distribution Task
grunt.registerTask('dist', [
  'sass:dist' // Compile Sass with distribution settings
]);
{% endhighlight %}

As the development settings are likely to be used often, I use the `default` task to run any development settings. The default task is run by typing `grunt`, which is shorter to type than, say, `grunt dev`. Saves a few characters!

When your project is ready for deploying, run `grunt dist` and voila! Your code is now ready to go.

## Watch it!
Now we have our tasks set up, we can get Grunt to watch files for changes, execute tasks and then reload the page for us. Firstly, install [Grunt watch](https://github.com/gruntjs/grunt-contrib-watch):

{% highlight bash %}
npm install grunt-contrib-watch --save-dev
{% endhighlight %}

Configure the task:

{% highlight js  %}
// Watch files
watch: {

  // Watch .scss files
  sass: {
    files: ['css/sass/**/*.scss'],
    tasks: ['sass:dev'],
  },

  // Live reload files
  livereload: {
    options: { livereload: true },
    files: [
      'css/**/*.css',
      '**/*.html',
    ]
  }
},
{% endhighlight %}

Load the plugin:

{% highlight bash %}
grunt.loadNpmTasks('grunt-contrib-watch');
{% endhighlight %}

Now we can simply type `grunt watch` into Terminal and it will watch for changes to any `.scss` files, then run the `sass:dev` task automatically. To reload the browser, [LiveReload](http://livereload.com) is configured to watch any changes to `.css` files. I've also specified to reload any `.html` files so you can see how it works. You will need to install the [LiveReload extension](http://feedback.livereload.com/knowledgebase/articles/86242-how-do-i-install-and-use-the-browser-extensions-) for either Safari, Chrome or Firefox.

## Taking it further
This is only a very small amount of what Grunt is capable of. I'd recommend reading through the documentation and checking out the [Grunt plugins](http://gruntjs.com/plugins) available (there are lots!) to see what else Grunt can do.

I've set up a Grunt starter project which I use as a base—you can find it on [GitHub](https://github.com/markgoodyear/grunt-starter). Feel free to adapt it, improve it and learn from it. Currently, it includes:

- JavaScript linting, concatenation and minification
- Sass compiling with development and production options
- Sass sourcemaps (requires Sass 3.3.0)
- Rasterizing .svg files
- Compress .jpg/.jpeg, .png and .svg files
- Reload the browser on file changes

_What are you waiting for? Get Grunting!_
