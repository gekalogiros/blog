---
title: "Planning your startup project"
date: 2015-02-11T11:05:03+01:00
showDate: true
draft: false
tags: ["blog","story"]
---

This article will be devoted to a major task that should be considered before designing the next $$$$-billion start-up. It's all about planning technologies, processes, the future, monetization, databases everything. When you develop technology products, many things can go wrong and you should be ahead by following a strict plan.

Below I cite the plan that I usually follow when building the ideas I have (unsuccessfully most of the times but I believe this is a good plan though!):

- Brainstorming:

Talk about your idea with friends or colleagues! Be specific about what you want to achieve and how. Sometimes just little details can turn an idea from doable to impossible! At this stage you should start thinking of deploying a task management open source tool on your server. Start writing simple user stories about what a user expect to see on the website you want to develop.


- Technologies

Now, that you know what you want to do you should choose the technologies that will be used in your development cycle. Again, be specific about what you want because a small detail could destroy everything. Take into consideration the scalability you want to achieve and how you can select wisely options that do not cost too much. For example, if you want to use a specific framework with a specific database then you probably have to get a Virtual Private Server and set everything from scratch. This is time-consuming but probably it is the only way of achieving what you want. if your application aims to support large amounts of data probably you should think of getting an AWS instance or use tools such as HADOOP and MAP-REDUCE technologies. My advice will be always the following: Choose Tools that are documented in-depth and don't be the beta-testers for technologies that might be excellent but are difficult to be used because of lack of documentation or support.


- Database

Most of the people start developing the front-end or the back-end without having designed the core of each application which is the Database!!!! The more planned the things are, the more weaknesses will come to light before starting development!


- Back-End/Front-End

For all the Engineers, the fun is on this stage! Be creative and start developing usable and beautiful things. At this stage I always go back and forth. Normally I start by having a basic user-interface developed on javascript, html5 and a template engine (Check MVC pattern it is awesome and will help you creating maintainable code!).  Afterwards, I start creating the back-end and fixing inconsistencies on the front-end.


- Mobile

Start-up without appearance on mobile phone is like having chips without ketchup. This is fun! Be creative again!!!


- Testing

This stage is like a playground! Break everything without worrying if it is bad or not! Find critical errors and Fix them!


- Continuous Integration

Create scripts that execute daily tasks and reporting back to you inconsistencies such as the status of the app, deprecated bits etc.

