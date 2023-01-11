---
layout: post
title: "Future of Codity platform and new functionalities of it"
description: "In this post, I discuss the future of Codity platform along with the new
functionalities of the platform as of today."
date: 2023-01-11
feature_image: images/future-codity.jpg
tags: [web editor, html, css, javascript, prototype, frontend]
---

# Future of Codity

During the past week, I was playing with the idea of actually being able to load javascript packages
from NPM, bundle and transpile and use them in the editor.
I will call it [Codity](https://codity.netlify.app/){:target="_blank"} Advanced editor. This is a
full-fledged editor with file management system so
that you can add different files to your project.
Beauty of it is that you can use proper import statements and Codity will go fetch those and bundle
your javascript project with a blazing fast speed.

Even though Codity is released, there are new and must have functionalities that are getting added
to it as per requests of the amazing community around it.
The functionalities added as of last post, are the following:
<!--more-->

## Emmet integration

Emmet[1] is the essential toolkit for web-developers. It lets you have snippets, expanding,
autocompletion and
re-using commonly used code chunks, so you can develop
faster and more efficient.

Example of it is when you type `div` and it expands it to `<div></div>`. Super helpful.

## Editor settings

You can now change the font size of the editor. In cases where you want to present something and
audience needs a bigger font size.

{% include image_caption.html imageurl="/images/editor-settings.png" title="Editor settings" caption="Editor settings" %}

You can also set the default layout, css preprocessor and javascript preprocessor. This will help if
you most often use these settings when
you start a new project. These settings will be persisted to your browser so as long as you use the
same computer and browser, you can trust that
the editor will get initialized with these settings.

## Theme

Codity now has a light theme and dark theme. Not so much to say today, but I am personally fan of
the
dark theme because it doesn't bother the eyes so much,
and it's good for the environment.
{% include image_full.html imageurl="/images/theme.png" title="Themes" caption="Themes mode" %}

## Profile section, view other's prototypes and collections

Now when you are signed up, all your saved prototypes will be shown in your profile page. Apart from
that you can create collections of prototypes.
{% include image_caption.html imageurl="/images/collections.png" title="Prototypes and collections" caption="Prototypes and collections" %}
I personally am working on a collection for amazing loading animations. Go ahead and try it now.

## Code formatting using Prettier

Prettier[2] is added as the code formatter for the editors. You just need to be in one editor and press
Command+Shift+o. There is a helper icon
on the right side of the footer in the editor that helps with available key bindings.

## References

1. [Emmet](https://emmet.io/){:target="_blank"}
2. [Prettier](https://prettier.io/){:target="_blank"}