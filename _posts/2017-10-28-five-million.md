---
layout: post
title: 5.6 Million SLOC
---

<div class="message">
I have contributed 5.6 Million Source Lines of code (SLOC) to open-source.
</div>

My <a href="//github.com/harrymt">GitHub profile</a> shows all my contributions. I used the the following command to calculate the SLOC:

{% highlight bash %}
curl https://api.github.com/users/harrymt/repos | \
  grep 'languages_url' | \
  awk '{print $2}' | \
  cut -d'"' -f2 | \
  xargs -L 1 curl
{% endhighlight %}

By language:

{% highlight bash %}
C
752,454

C++
15,404

CSS
90,447

HTML
1.1 Million (1,173,405)

Java
454,136

JavaScript
1.3 Million (1,373,071)

PHP
9,318

Python
1.7 Million (1,788,335)

Shell
27,511
{% endhighlight %}

Total:
5.6 Million (5684081)
