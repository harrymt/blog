---
layout: post
title: 5.6 Million SLOC
---

<div class="message">
I have contributed 5.6 Million Source Lines of code (SLOC) to open-source.
</div>

My <a href="//github.com/harrymt">GitHub profile</a> shows all my contributions. I used the the following command to calculate the SLOC:

{% highlight bash %}
curl https://api.github.com/users/harrymt/repos | grep 'languages_url' | awk '{print $2}' | cut -d'"' -f2 | xargs -L 1 curl
{% endhighlight %}

By language:

{% highlight bash %}
C
752454

C++
15404

CSS
90447

HTML
1173405

Java
454136

JavaScript
1373071

PHP
9318

Python
1788335

Shell
27511
{% endhighlight %}

Total:
5684081 / 5.6 Million
