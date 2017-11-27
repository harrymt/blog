---
layout: post
title: Static Analysis for Writing
tags: [writing]
---

<div class="message">
Sublime linter for english prose.
</div>

We lint our source code, analyse our programs, so why not our writing?

![Write good example]({{site.baseurl}}/img/write-good-example.png)

Of course there are online checkers, such as [Grammarly](https://www.grammarly.com/). But these aren't integrated into our editors and take away our software developer control.

[Write Good](https://github.com/btford/write-good). A naive linter for English prose. Gives us back this control, letting us integrate this node package into our text editors, like sublime text.

Integrate this with sublime (requires [nodejs](https://nodejs.org/en/), and [sublime linter](http://sublimelinter.readthedocs.io/en/latest/)):

- `npm install -g write-good`, to globally install write-good
- Package Control -> `SublimeLinter-contrib-write-good`

[Write Good Sublime Linter Plugin](https://github.com/ckaznocha/SublimeLinter-contrib-write-good) takes a 20 seconds to install. Gives you lots of helpful hints for writing well!

<img src="https://t1.gstatic.com/images?q=tbn:ANd9GcTb7-D5cUUucjlJkD-BlXRS0GvBZ47txkHmRnyey34kjfA6omTn" width="250">

The write-good plugin and the 'On Writing Well' book helped me massively while writing my MSc thesis at [UoB](http://www.bris.ac.uk/).
