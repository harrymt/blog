---
layout: post
title: Track mailto and tel clicks in Wordpress with Google Analytics
---

<div class="message">
How to <strong>easily</strong> add Google Analytics tracking code to <code>mailto:</code> and <code>tel:</code> anchor links.
</div>

It is useful to track when vistors interact with telephone and email links. With this [Wordpress Plugin](//wordpress.org/plugins/simple-tel-tracking/) you can easily track how many times people click on these in just 1 minute.

### Download a Wordpress Plugin

I created a Wordpress plugin to simply go through all the `mailto` and `tel` `<a>` elements on the page and add the [Google Analytics](https://analytics.google.com/analytics/web/) tracking code to `onclick`.

- [Download Wordpress Plugin](//wordpress.org/plugins/simple-tel-tracking/) to Track tel and mailto links.
- Add it to your site and enable the plugin

Before:

```html
<a href="mailto:harrymt@me.com">Contact me</a>
```

After:

```html
<a onclick="ga('send','event','Mailto Tracking: harrymt@me.com','Click/Touch');" href="mailto:harrymt@me.com">Contact me</a>
```

The plugin sends back to Google:

```javascript
ga(
  'send',
  'event',
  'Mailto Tracking: harrymt@me.com',
  'Click/Touch'
);
```

For tel links, it is the same.

Before:

```html
<a href="tel:+0759606141">Bristol 0759606141</a>
```

After:

```html
<a onclick="ga('send','event','Phone Call Tracking: 0759606141','Click/Touch');" href="tel:+0759606141">Bristol 0759606141</a>
```

The [plugin](//wordpress.org/plugins/simple-tel-tracking/) sends:

```javascript
ga(
  'send',
  'event',
  'Phone Call Tracking: 0759606141',
  'Click/Touch'
);
```

### Open Source

I built the plugin and made it [open source](//github.com/harrymt/simple-tel-tracking). Please [request](//github.com/harrymt/simple-tel-tracking/issues) a new feature or [improve it here](//github.com/harrymt/simple-tel-tracking/pulls).

Add the [Wordpress plugin](//wordpress.org/plugins/simple-tel-tracking/) to your site to track mailto and tel presses!
