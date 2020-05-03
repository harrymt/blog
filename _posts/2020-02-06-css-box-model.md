---
layout: post
title: Do you know the CSS box model?
tags:
  - CSS
---
How well do you know the CSS Box Model? Do you know the differences between the `box-sizing` properties?


Take this div, how is it rendered?

```css
div {
  width: 100px;
  height: 100px;

  padding: 5px;
  margin: 20px;
  border: 5px solid blue;
}
```

### box-sizing: border-box

- Add the `padding` and `border` to `width`
- Take away the `padding` and `border`, from the `width`.

![box-sizing: border-box;]({{site.baseurl}}/img/box-sizing-border-box.png)

### box-sizing: content-box

- Add the `padding` then `border` to `width`

![box-sizing: content-box;]({{site.baseurl}}/img/box-sizing-content-box.png)

## Summary

- `margin` is always outside the box
- `padding` and `border` are always outside of the `width`
- `width` changes when using `box-sizing: border-box;`

<p class="codepen" data-height="412" data-theme-id="default" data-default-tab="css,result" data-user="harrymt" data-slug-hash="GRJRPyy" style="height: 412px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="CSS Box Model">
  <span>See the Pen <a href="https://codepen.io/harrymt/pen/GRJRPyy">
  CSS Box Model</a> by Harry Mumford-Turner (<a href="https://codepen.io/harrymt">@harrymt</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
