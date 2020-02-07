---
published: false
layout: post
title: Do you know the CSS box model?
tags:
  - CSS
---
How well do you know the CSS Box Model and the differences between different `box-sizing` properties?


#### box-sizing: border-box

- Add the padding then border to width
- Takeaway the padding and border from the width.

![box-sizing: border-box;]({{site.baseurl}}/img/box-sizing-border-box.png)

#### box-sizing: content-box

- Add the padding then border to width

![box-sizing: content-box;]({{site.baseurl}}/img/box-sizing-content-box.png)

- Margin is always outside the box
- Padding and Border are always outside of the width
- Width property changes when using `box-sizing: border-box;`

<p class="codepen" data-height="412" data-theme-id="default" data-default-tab="css,result" data-user="harrymt" data-slug-hash="GRJRPyy" style="height: 412px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="CSS Box Model">
  <span>See the Pen <a href="https://codepen.io/harrymt/pen/GRJRPyy">
  CSS Box Model</a> by Harry Mumford-Turner (<a href="https://codepen.io/harrymt">@harrymt</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
