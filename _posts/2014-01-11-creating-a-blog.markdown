---
layout: post
title:  "Creating my blog."
date:   2014-01-11
---

﻿I've been toying with the idea of creating a blog for some time. I am not an avid participant in social media and therefor don't have the largest social presence on the Internet. I've toyed with quite a few frameworks and tools while toying with the idea of creating a blog. I've decided to discuss some of the technologies I liked and have utilized for other purposes since my journey began. 

To start, I'm pretty new to web development although I have created static pages and themed simple message boards in the past. I started toying around with raw PHP after I learned to create a dynamic website in my semester long Software Engineering course. While the class was not focused on teaching us to learn PHP code, I took the opportunity to learn the language. Our instructor discouraged us from using any third party frameworks. Although it was not pleasant, I believe the experience made me  appreciate all the cool tools that I've found since completing that project. 

After getting frustrated with the lawlessness of PHP I started looking at Python frameworks. I started playing with `web.py` but found the project had been mostly abandoned and couldn’t really find support or interest in the framework besides some dated posted on the internet. Shortly afterwards I started playing with the `Flask` framework. Through this framework I discovered many tools that were pretty standard that I have utilized in projects since. 

One tool that I discovered while experimenting with the `Flask` framework was a template engine named Jinga2. While creating my first dynamic website, one of the biggest problems I experienced was with organization. Grouping PHP and HTML code in single page-specific source files resulted in a mess that was hard to re-factor. Although I realized this early in the development process, due to a rapidly approaching deadline, my team and I decided to simply fill the remaining requirements and deliver a usable, yet hard to maintain project. I later utilized the template engine, `Twig`, while re-factoring that same page for another course. Additionally I discovered the goodness of a proper ORM, `SQL-Alchemy`. 

However, this blog is not a dynamic website. After creating an blog utilizing the MVC design pattern built on top of Flask, I decided that it was simply too involved for a simple blog. Authentication, while not difficult to implement, seemed like overkill for a single user blog. Using a database for such simple content seemed like a pain. Not to mention hosting a Python page is simply a hassle, free hosts do exist but I did not enjoy the few that I tried. While I could host the site myself, my Internet is not so reliable and my bandwidth is limited. 

I’d been reading a bit about static site generators and decided to go with `Jekyll` to create my web blog. I simply brainstormed and implemented a slightly personal theme on the page using `Twitter Bootstrap` and its ready to go. I tweaked the settings for a short while and ﻿voila I have something that works. It requires no database, no dealing with a plugin or custom implementation for authentication, and almost most importantly, I don’t have to register with another host. I can simply use my github account. 

Although I look forward to creating and delivering a larger scale website on top of the Flask framework, for this small website I believe Jekyll will be sufficient.
