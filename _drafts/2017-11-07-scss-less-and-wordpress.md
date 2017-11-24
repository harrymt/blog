---
layout: post
title: Use SCSS or LESS with Wordpress
---

<div class="message">
3 ways to preprocess your CSS with Wordpress.
</div>

[SCSS](http://sass-lang.com/) and [LESS](http://lesscss.org/) are CSS preprocessors. Use them and get CSS variables, nesting and lots of good features!

Here are 2 methods for using LESS or SCSS in your Wordpress development flow.

### 1. Using Grunt.js or Gulp.js

Pros: Faster
Cons: Need to have access to the command line


### 2. Using a php pre-processor

Pros: No cmd line neccessary
Cons: Slower? Harder to te




---
layout: post
title: Use SCSS or LESS with Wordpress
---

<div class="message">
3 ways to preprocess your CSS with Wordpress.
</div>

[SCSS](http://sass-lang.com/) and [LESS](http://lesscss.org/) are CSS preprocessors. Use them and get CSS variables, nesting and lots of good features!

Here are 2 methods for using LESS or SCSS in your Wordpress development flow.

### 1. Using Grunt.js or Gulp.js

Pros: Faster
Cons: Need to have access to the command line


#### Install Grunt

Note: this command might require sudo, because it installs grunt globally.

```bash
$ npm install -g grunt-cli
```


#### Setup a Gruntfile.js

```bash
$ cd wp-content/themes/<theme_name>
$ npm init
<Fill out fields>
$ npm install grunt --save-dev
$ touch Gruntfile.js
```

#### Sass or less

Sass and less are very similar. This tutorials I’ll use sass.

**Sass**

```bash
$ npm install grunt-contrib-sass --save-dev
```

**Less**

Find usage here https://github.com/gruntjs/grunt-contrib-less
```bash
$ npm install grunt-contrib-less --save-dev
```


### 2. Using a php pre-processor

Pros: No cmd line neccessary
Cons: Slower? Harder to tell when it actually processed



