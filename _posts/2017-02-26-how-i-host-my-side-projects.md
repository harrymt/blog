---
layout: post
title: How to Host unlimited Side Projects for free
---

<div class="message">
Host unlimited side projects using GitHub pages!
</div>

With <a href="//github.com/pages">GitHub pages</a> it is really easy to get a new side project up and running within minutes. Just follow these simple steps.

1. Create repo & activate GitHub Pages
2. (optional) Clone a <a href="//github.com/harrymt/grunt-boilerplate">boilerplate repo</a>
3. Start side project

## 1. Create Side project Repo and Activate GitHub Pages

When you create a repo, the name you choose will be the URL of the website, so choose something sensible.

<img src="{{ site.baseurl }}/img/create-github-repo.png">
<p class="img-caption">Create a repo with the name of the side project.</p>

Next activate GitHub pages, by going to the repo settings, scrolling down and clicking enable github pages.

<img src="{{ site.baseurl }}/img/activate-github-pages.png">
<p class="img-caption">Create a repo with the name of the side project.</p>

Now you can navigate to a url like http://username.github.io/repo_name and see the site!

## 2. (optional) Clone a boilerplate repo

Having a boilerplate as starter code makes setting up side projects even faster.

I create and manage a <a href="//github.com/harrymt/grunt-boilerplate">boilerplate</a> using <a href="//gruntjs.com">GruntJS</a> to handle all dependencies and help with processing <a href="//http://sass-lang.com">Sass</a>.


<a class="button button-huge" href="//github.com/harrymt/grunt-boilerplate">Download</a>

The boilerplate uses Grunt to optimise the project. For example the below snippet minifies the index.html file to decrease load times.

**Gruntfile.js**
{% highlight javascript %}

  grunt.initConfig({
    htmlmin: { // Minify HTML
      dist: {
        options: {
          removeComments: true,
          collapseWhitespace: true
        },
        files: {
          'index.html': 'build.html' // 'destination': 'source'
        }
      }
    },
  });

  grunt.loadNpmTasks('grunt-contrib-htmlmin'); // Minify HTML

  grunt.registerTask('default', ['htmlmin']);

{% endhighlight %}


## 3. Start the side project

Now you can easily start a <a href="//github.com/harrymt/mark">front end side project</a>. As unfortunately GitHub pages only allows static sites and client side Javascript.
