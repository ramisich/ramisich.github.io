---
layout: post
title: "Journey I took to develop TP-Link plug controller for Samsung Galaxy watches"
description: "In this post, I walk you through my thought process and system and coding to make it work."
date: 2022-12-09
feature_image: images/tp-link-plug.png
tags: [hobby, Samsung Gear s3, Galaxy watches, Home automation]
---

I recently started working with home automation devices and in the past week, I connected one of my lamps to a TP-Link smart plug. Obviously this was used to be able to control the lamp and also schedule it so that at a given time, it turns on and off.

I have a Samsung Gear s3 watch and I thought it would be awesome if I could control the plug from the comfort of my wrist. I want to share with you the way I managed to do it.

<!--more-->
The challenges I had to face were firstly that I had to see if TP-Link had an API that I could use from within my code to turn the plug on and off and to my surprise it did not. Long ago I worked on a Samsung app 
that you could turn on and off your Philips hue lights. It was fairly simple given that Philips Hue has an API well documented to call and manage the lamps. So I had to find the way to see how the plug protocol works.
Thankfully other people had decoded the protocol that is used by TP-Link which helped me in my journey. Second challenge I realized was the fact that I had to do some socket programming to discover and also send commands to the plug.
Tizen is the operating system that is used in Samsung watches ,and it supports both(html, css and Javascript) and C/C++ to right apps for it. Obviously for me the easiest thing was to utilize the web stack since I'm very familiar with ,and it's around a couple of years that I haven't touched C and C++. But the problem is that you can not do socket programming on the web stack since it does not support nodeJS to write socket code. It's as if you write code for a browser.
So I had to start refreshing my C language knowledge and do it in C.

> One lesson worth learning here is that, if you put your mind on something and really persist and follow through, even though you might get disappointed by some obstacles along the way,
>  (Tizen being hard to work with on C/C++ and not really adopting with new technologies, e.g. Node), You will make impossible, possible.


## How I managed to talk to TP-Link Plug
After reading some materials and code sources on the web [1], I realized that TP-Link accepts commands through the TCP port `9999`. The commands need to be sent encrypted with an encryption algorithm that I found on the web.
I would not put any code here since you can search and found them on the web [2] and I rather want to tell you the story.

Next thing was to actually find the plug in my home network. Most of the smart devices actually broadcast their existence by saying that I am here on this address and port. Knowing the port,
I managed to send a broadcast on UDP port `9999` on `255.255.255.255` address. Decrypting the result back gave me information such as what is the device name, and some other information about the plug and hence I got the Ip address of the plug on my network.
Using the IP and knowing the port I could send commands via tcp to that Ip and the port mentioned above.

## Tizen side
I wrote a c program to test the connection and also sending a couple of commands to get the state of the plug and turn it on and off, all good. Now going to Tizen. For Samsung and tizen platform,
 there is an IDE which your can write the code, and install the developed app either on an actual device or an emulator. Unfortunately me having a mac and Ventura macOS, I could not run the app 
on the emulator, but on the bright side, installing the development app on the actual watch is quite easy and quick.

Since I have never written code in Tizen for c language and as you might guess, there is UI part plus the application logic, so I had to go learn a bit on how things work. Good news is that 
they actually have a good documentation [3] on how the lifecycle of the application works and also the UI frameworks that you can use to create the elements and attach the event listeners to them.
After about 2 days of reading and experimenting I took a stab on writing the actual code and with the help of some other sample applications from the Tizen studio I managed to make it work.

The whole workflow is super simple. When you open the app on your watch, It searches for TP-Link plug, detects its IP address, gets the plug name, show it in the app with a switch that turns the plug on and off.
Take a look at the video on how the app works in real life.

## Demo
Here is a demo of me working with the app to turn the lamp connected to the plug on the wall, on and off.
<iframe width="560" height="315" src="https://www.youtube.com/embed/JDAjv9oCkUk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Further work
I would like to put the app on the Galaxy store so that others can use it as well. It should be fairly simple since I already have put 2 similar apps in the store. One need to create a certificate using
the tizen studio. The process is well documented in the Tizen documentation.
## References
1. [Reverse Engineering the TP-Link HS110](https://www.softscheck.com/en/blog/tp-link-reverse-engineering/){:target="_blank"}
2. [TP-Link smart plug api](https://github.com/BobNisco/tplink-smartplug-api){:target="_blank"}
3. [Getting Started with EFL UI Programming](https://docs.tizen.org/application/native/guides/ui/efl/getting-started/){:target="_blank"}
