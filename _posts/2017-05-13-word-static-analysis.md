---
layout: post
title: Static Analysis for Writing
tags: [writing]
---

<div class="message">
A linter for english prose.
</div>

We lint our source code, analyse our programs, so why not our writing?

![Write good example]({{site.baseurl}}/img/write-good-example.png)

Of course there are online checkers, such as [Grammarly](https://www.grammarly.com/). But these aren't integrated into our editors and take away our software developer control.

### Linters

- [`write-good`](https://github.com/ckaznocha/SublimeLinter-contrib-write-good)
- [`alex`](https://github.com/wooorm/alex)

#### Write Good

[Write Good](https://github.com/btford/write-good). A naive linter for English prose. Gives us back this control, letting us integrate this node package into our text editors, like sublime text.

Integrate this with sublime (requires [nodejs](https://nodejs.org/en/), and [sublime linter](http://sublimelinter.readthedocs.io/en/latest/)):

- `npm install -g write-good`, to globally install write-good
- Package Control -> `SublimeLinter-contrib-write-good`

[Write Good Sublime Linter Plugin](https://github.com/ckaznocha/SublimeLinter-contrib-write-good) takes a 20 seconds to install. Gives you lots of helpful hints for writing well!

#### Alex

![Alex Linting](https://raw.githubusercontent.com/wooorm/atom-linter-alex/master/screencast.gif?token=AA5pFhwJyhXtc0a3GdKXaLfWqyIQvN0Mks5V5dJUwA%3D%3D)

This plugin [`Alex`](http://alexjs.com/) helps you find gender favouring, polarising, race related, religion inconsiderate, or other unequal phrasing.


<img src="https://t1.gstatic.com/images?q=tbn:ANd9GcTb7-D5cUUucjlJkD-BlXRS0GvBZ47txkHmRnyey34kjfA6omTn" width="200">

These plugins combined with this book 'On Writing Well', helped me massively while writing my masters thesis at [University of Bristol](http://www.bris.ac.uk/).
