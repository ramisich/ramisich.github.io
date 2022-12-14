---
layout: post
title: "[in-progress] A new frontend quick prototyping platform for UI and web development"
description: "In this post, I discuss the details about the quick prototyping tool that I'm building"
date: 2022-12-14
feature_image: images/web-editor.png
tags: [web editor, html, css, javascript, prototype, frontend]
---

In my personal development time, I started working on a project that I always wanted to work on and that is a web prototyping platform/editor for frontend and UI designers and 
developers to quickly prototype and examine a piece of code in html, css and Javascript. I named it [Codity](https://ramisich.github.io/web-editor){:target="_blank"}[1]. This has helped us today in the team with a simple test of checking some css properties 
to see how an image will look like when these styles are applied. 

There are a couple of these websites in the web such as codepen and jsfiddle that one
can do the same, but I took it on, not only for my learnings/sharing but also to build a platform is not as cluttered as those websites plus usability for others to reuse the editors. Following is how I 
managed to create the editor at its current state ....
<!--more-->


## The web editor library to use for the actual editors
There are a couple of open source code editor components that I could choose from and I chose Codemirror[2]. Codemirror is not only easy to start with, but also it's quite extensible.
It supports accessibility, mobile support, syntax highlighting, autocompletion and pretty much most if not all the features that a desktop IDE has.
Ace[3] is another high performance code editor on web. It is actually quite powerful. Both are written in javascript but because of my experience with Codemirror in the past, It's author 
and the surrounding community, I chose codemirror.

## Planning
Since it is a hubby project, I started with just a simple UI to present html, css and javascript panes. There is also the preview pane that when you write your code in the editor, 
It updates automatically and in realtime with the rendered output of the code in the editor panes. This greatly helps with quickly testing and prototyping instead of spinning up your 
dev environment which most of the time slows you down with all the build times for something quick.

List of things that I have in mind to develop is as follows:
* Ability to store the prototypes so that it can be shared by others asynchronously
* Adding popular preprocessors for html, css and javascript (e.g. LESS, SCSS)
* Adding functionality to format the code so that it looks pretty
* Creating export and preview so that one can share a prototype in other websites and webpages
* Adding authentication/authorization so that one can save their prototypes
* Adding support for including different css and javascript libraries for prototypes
* Adding documentation on how to use the tool
* Creating a library for others to include the extended code editor in their projects

# Deployment
I am using NextJS[4] which is a ReactJS framework that makes it easy to develop the frontend part of the platform. The project code is in GitHub. I hooked the GitHub with action containers to Netlify[5] so 
that the code is deployed to Netlify servers. 

Later, my plan is to create a proper CI/CD workflow that would build and deploy the code to Google cloud (GCP). This will help with other projects to be able to only focus on 
developing new features rather than focusing on the operational side of things.

Thanks for reading and greatly appreciate your feedbacks.

## References
1. [Codity web editor](https://ramisich.github.io/web-editor){:target="_blank"}
2. [Codemirror](https://codemirror.net/){:target="_blank"}
3. [Ace editor](https://ace.c9.io/){:target="_blank"}
4. [NextJS React framework](https://nextjs.org/){:target="_blank"}
5. [Netlify](https://www.netlify.com/){:target="_blank"}
