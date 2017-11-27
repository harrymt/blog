---
layout: post
title: How to Host unlimited Side Projects for free
tags: [github, javascript]
---

<div class="message">
Host unlimited side projects using GitHub pages!
</div>

I host all my side projects [on GitHub](//github.com/harrymt), which totals to [5.6 Million lines](/blog/2017/10/28/five-million.html) of open-source code!

<a href="//github.com/pages">GitHub pages</a> makes it easy to get a new side project up and running within minutes. Follow these simple steps.

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

Now you can navigate to a url and see the site, such as:

```
http://username.github.io/repo_name
```

## 2. Clone a boilerplate repo (optional)

Having a boilerplate as starter code makes setting up side projects even faster.

I create and manage a <a href="//github.com/harrymt/grunt-boilerplate">boilerplate</a> using <a href="//gruntjs.com">GruntJS</a> to handle all dependencies and help with processing <a href="//http://sass-lang.com">Sass</a>.


<a class="button button-huge" href="//github.com/harrymt/grunt-boilerplate">Download</a>

The boilerplate uses Grunt to optimise the project. For example the below snippet minifies the index.html file to decrease load times.

**Gruntfile.js**

```javascript

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

```


## 3. Start the side project

Now you can start making <a href="//github.com/harrymt/mark">front end side project</a>. But bare in mind GitHub static sites allows Jekyll, HTML, CSS and JS.

## Some of my side projects

- [Simple Tel Tracking](/blog/2017/11/10/add-google-analytics-code-to-tel-links-wordpress.html) - Add Google Analytics tracking code email and telephone numbers in Wordpress
- [Harrys Habits](//github.com/harrymt/harryshabits) - A chatbot to help you form new healthy habits
- [Rate My Plate](//github.com/harrymt/rate-my-plate) - A twitter bot to rate the environemental impact of your food
- [This blog](//github.com/harrymt/blog) - All of these posts are hosted on GitHub pages and open source
