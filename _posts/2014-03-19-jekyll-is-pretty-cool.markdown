---
layout: post
title:  "Jekyll is pretty cool!"
date:   2014-03-19
---

Just finished putting some additional content on my blog. It's finally starting to look like a website. Anyway, for a static website generator theres some pretty cool features included in [Jekyll][jekyll-page]. For example, for my [projects page][work-page] I was able to define the data in a seperate file in a directory called `_data` and then just loop through it with the liquid templating engine. It almost feels like using a database to populate the website! It's quite nice when you don't have to repeat yourself.

The templating engine works pretty similarly to Django's templating engine, handlebars, jinga2, etc. Just as an example, this is more or less how I utilized this feature of Jekyll. 

{% highlight Django %}
{% raw %}
{% for project in site.data.projects %}
  {{ project.name }}
  {{ project.description }}
  {{ project.github }}
{% endfor %}
{% endraw %}
{% endhighlight %}

Initially I planned on putting some visual tweaks on the site with javascript and jQuery. I wasn't quite happy with the result, especially on mobile. Trying to keep this site looking decent on mobile. Anyway, I'll have to find a more substantial project to work on with a JS MVC framework to get some good experience working with that. 

[jekyll-page]: http://jekyllrb.com/
[work-page]: http://aspalding.github.io/work/