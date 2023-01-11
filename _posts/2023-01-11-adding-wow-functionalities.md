---
layout: post
title: "Codity, the fastest online web editor"
description: "In this post, I discuss the details about the quick prototyping tool called Codity,
it's features"
date: 2022-12-25
feature_image: images/codity.png
tags: [web editor, html, css, javascript, prototype, frontend]
---

Today, I am happy to announce that [Codity](https://codity.netlify.app/){:target="_blank"} web editor is released. Following is the vision of
Codity.
> Codity web editor is born out of curiosity to make it easier for web designers and developers
> around the world, to quickly prototype and test their
> html, css and javascript code as fast as possible and be able to share it with millions of other
> developers and people.

In this post I will be going through its features, technologies I used to make it, examples and also
challenges and learnings but first, take a look
at an example prototype:

[Pixel art: Homer Simpson](https://codity.netlify.app/prototypes/7hG1KJg7qIZSJbLqzJD07){:
target="_blank"} [code by Yago Estévez].
<!--more-->

If you are frontend developer, please go ahead and test it and put some html, css and js code if you will to see who it works before proceeding.
I would be very happy to get your opinions about it in the comment section below.

# Technologies

Whole editor platform is built on top of React and NodeJS. I used Next.js[1] framework since it
gives you both the client side and also the backend for frontend
where I could implement many apis used in the editor.

For database, I'm using CockroachDB[2] because of it's ease of use and integration with Next.js.
talking about databases, I found it easier to use
a good ORM to make it easier to talk to the database and for that I found Prisma[3] quite
intriguing. It supports migrations, and it automatically applies
them to the remote database. Following is the simplest example of the schema layout for Codity.

<pre>
<code class="language-javascript">model User {
  id            BigInt          @id @default(autoincrement())
  email         String          @unique
  password      String
  username      String
  prototypes    Prototype[]
}

model Prototype {
  id BigInt          @id @default(autoincrement())
  html               String
  css                String
  js                 String
  p_id               String @unique
  css_libs           String[]
  js_libs            String[]
  html_preprocessor   String @default("none")
  css_preprocessor   String @default("none")
  js_preprocessor    String @default("none")
  author             User? @relation(fields: [authorId], references: [id])
  authorId           BigInt?
}
</code></pre>

The whole site is deployed to Netlify. Seriously what is better than that for the scope of this
project at the moment.

<hr />

## Features

#### Editor panes

Let me put it as a story on how the features were added and what was my thought process. Simply put,
first thing was to add the html, css and javascript
editor panes. For that I used codemirror as I discussed in
my [previous post](https://ramisich.github.io/A-new-frontend-quick-prototyping-platform-for-UI-web-development){:
target="_blank}.
The new version is 6 and has a great community around it, so it was worth the try.

#### Authentication and Authorization

Of course a platform is not a platform without users. After researching for a while, I found an
absolute great
open source project called NextAuth.js[4] which is literally built for adding support for oAuth
which was exactly what I wanted.
It has great features and work with lots of providers such as Google, GitHub and Twitter. I can't
recommend it more. It took me about
a day to have everything all setup whereas before I had to put a couple of days reading
documentations and sample codes to be able to do the same.

#### Preprocessors

Next thing was to add preprocessor for css and javascript. For css I went for SCSS which is the most
popular of all and for JS, I chose Babel. The list
of preprocessors are more than that and I will add them one by one based on their popularity.
There are node modules already built for compiling your SCSS and Babel code and here is where
Next.js comes in handy since you could have your apis for compiling these
in the backend and call them from frontend under the same framework. There is no need to have your apis on another cloud. All
in one place. Sweeeeet!

#### Editor and language settings

Finally, there are editor settings that can be used such as changing the layout to be horizontal
versus vertical, changing font-size and basically
adding preprocessors and external libraries for css and js.

{% include image_caption.html imageurl="/images/preprocessors.png" title="css settings" caption="CSS
settings including preprocessor and external libraries" %}

## Challenges

While I was developing the editor, I had to refresh my memory on how to do a proper layout and on how to
make an editor with a splitter that user can resize to
make the preview bigger or the coding area larger. I used css FlexBox since it makes it really easy
to define shrinking and expanding of the elements, and it takes care of the rest. It took a while
until I made it work.

Secondly challenge was making sure that the lifecycle hooks in React are called and performed
properly. As any React developer knows,
React made it super easy to create reactive single page applications by giving a lot of features and
freedom to the developer but with a small
mistake, it can become a hurdle. So all I did was to make sure that I have a proper code structure
as in having proper domain models, repositories and services so
to know where I am looking and where the custom react hooks are.

Thirdly, I had issue with Prisma as I was learning it for the first time. Specifically when there
are relation (as in the code snippet above).
It was at first difficult to follow their documentation on how to add a prototype and connect it to
a user. By checking the actual generated code for the schema I managed to find the missing pieces
and connected the dots.

All in all, I have had great pleasure and learnings while doing this project!


<hr />

## Future

Following this hubby project, here is a list of things I would like to add:

* Adding social features such as being able to comment and collaborate. This includes a platform for
  users to be able to talk, teach and learn.
* Adding functionality to format the code so that it looks pretty.
* Creating export and preview so that one can share a prototype in other websites and webpages.
* Creating a library for others to include the extended code editor in their projects.
* Adding Profile pictures either by getting them from the providers if user decides to authenticate
  via social media or a feature to upload their image.

Thanks for reading this post! Please comment and share it so that it reaches more people.

## References

1. [Next.js](https://nextjs.org/){:target="_blank"}
2. [CockroachDB](https://www.cockroachlabs.com/){:target="_blank"}
3. [Prisma - Next-generation Node.js and TypeScript ORM](https://www.prisma.io/){:target="_blank"}
4. [NextJS React framework](https://nextjs.org/){:target="_blank"}
5. [NextAuth.js](https://next-auth.js.org/){:target="_blank"}
