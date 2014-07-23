---
layout: post
title: "Jekyll and working with the web."
date: 2014-07-23
---

At the moment most of my work so far at 8th Light has been independent toy programs written from scratch. Before I came here I was spending quite a bit of time getting familiar with a variety of web frameworks. One thing I enjoyed was the massive variety of tools available. It's fun to keep up with and figure out where a specific framework excels. 

Anyway, since I've been trying to make a post everyday, the front page of my blog was getting incredibly long. In accordance I decided to add pagination. Really just a couple lines of code, the documentation provided a solid start. Heres what I wound up:

{% highlight Django %}
<ul class="pager">
  {% if paginator.previous_page %}
		<li class="previous"><a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}">&larr; Previous</a></li>
  {% endif %}

  {% if paginator.next_page %}
		<li class="next"><a href="{{ paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' }}">Next &rarr;</a></li>
  {% endif %}
</ul>
{% endhighlight %}

I like working in the context of a framework. A well chosen framework provides a solid foundation and procedure for getting something done. It seems as if a lot of our work is done through the web and I can't wait to get back into it and working on a team! 