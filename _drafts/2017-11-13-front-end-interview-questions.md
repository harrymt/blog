---
layout: post
title: Front-End Interview Questions
---

<div class="message">
HTML, CSS, JavaScript and PHP interview questions.
</div>

Recently I have had the opportunity to interview candidates for a junior front-end developer position.

- tldr: [My CSS and HTML Questions](https://codepen.io/harrymt/pen/wPBqBB)

It is difficult what technical questions to ask as they can be too easy or too hard.

Essentially I want to know they can code, so I thought of some questions that I was asked during a [3 day workshop](http://workintheweb.com/) I attended.

Our front-end position required 4 things.

- HTML
- CSS
- JavaScript
- PHP
- CMS experience

#### 1. HTML

{% highlight html %}

<a class="btn">Primary</a>

<a class="btn btn-secondary">Secondary</a>

{% endhighlight %}


#### 2. CSS


{% highlight less %}
@primary: #03A9F4;
@secondary: white;

.btn {
  background-color: @primary;
  border-radius: 2px;
  border: 1px solid darken(@primary, 10%);
  color: @secondary;
  font: 11px system-ui;  
  margin: 10px;
  padding: 7px;
  text-align: center;
  width: 100px;
}

.btn-secondary {
  background-color: @secondary;
  color: @primary;
}
{% endhighlight %}


{% highlight less %}
// Bonus

.btn:hover {
  background-color: darken(@primary, 10%);
  color: @secondary;
  cursor: pointer;
}

// Display
body {
  display: flex;
  justify-content: center;
  margin-top: 50px;
}

{% endhighlight %}


#### 3. JavaScript

#### 4. PHP

#### 5. CMS Experience

Candidates should talk about any interaction or development, e.g. custom modules/plugins, with the following CMS:
- Drupal
- Wordpress
- Magento
