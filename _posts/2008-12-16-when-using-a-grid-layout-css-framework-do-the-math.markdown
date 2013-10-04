---
author: admin
comments: true
date: 2008-12-16 18:09:19+00:00
layout: post
slug: when-using-a-grid-layout-css-framework-do-the-math
title: When Using a Grid Layout CSS Framework, Do the Math
wordpress_id: 74
categories:
- Blueprint Framework
- css
- web development
tags:
- Blueprint Framework
- css
- web development
---

I recently spent an entire weekend trying to troubleshoot why Internet Explorer 6 kept wrapping the rightmost DIV in my design to the bottom of the page when no other browser did. In my case, I was using the [Blueprint CSS framework](http://http://www.blueprintcss.org/) that creates twenty-four 30 pixel columns, each with a 10 pixel right margin (except the 24th column, which has no right margin), to make a nice 950-pixel wide grid. The whole purpose of using a CSS framework is that it's supposed to protect me from exactly the sort of problem I was having where different browsers display the page differently. I spent hours trying to figure out why Blueprint was failing in this case. Finally, on Sunday evening I figured it out. The enemy was not Blueprint. The enemy was me.

![Blueprint Grid](http://anthonygthomas.com/wp-content/uploads/2008/12/grid.png)

Above is an approximation of the Blueprint grid. (The thirty-pixel columns are in gray and the ten-pixel right margins in white.) [Read the tutorial file for details](http://anthonygthomas.com/2008/11/22/blueprint-css-tutorial-file/), but basically, by defining "span-16" as the class of your DIV, you wind up with a 630 pixel DIV with a ten-pixel right margin for a total of 640 pixels. Nice and neat, and it seemed perfect in my case since the photo I wanted to place on the right was 300 pixels wide. I even had ten pixels to spare. You're probably a lot smarter than me, so you've already figured it out. Unfortunately, I spent the better part of a weekend working in this problem. Finally I was reduced to counting columns and I realized _there's no way to get a 300-pixel DIV using 40 pixel columns!_ Firefox, Safari & higher versions of Internet Explorer were more forgiving and formatted the page as I wanted. Only Internet Explorer 6 interpreted the code strictly in this case. The other browsers corrected for my math error. I blamed Blueprint for failing and Internet Explorer 6 for misinterpreting my CSS when I was at fault all along.

Forty X 7 (span-7) = 280. Just short of my needed 300 pixels. Forty X 8 = 320. Twenty pixels too wide which left an unwanted margin on the right of my photo. When I finally figured all of this out, I was able to use a combination of Blueprint classes and my own classes to consistently format the page the way I wanted.

Lesson learned: Leverage your CSS grid framework as much as possible, but also add up your columns to your page elements don't get pushed around the page. It may still be necessary to define your own DIVS outside of the framework.
