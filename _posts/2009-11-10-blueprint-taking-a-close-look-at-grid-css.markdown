---
author: admin
comments: true
date: 2009-11-10 02:31:23+00:00
layout: post
slug: blueprint-taking-a-close-look-at-grid-css
title: 'Blueprint: Taking a Close Look at grid.css'
wordpress_id: 191
categories:
- Blueprint Framework
- css
- web development
tags:
- blueprint
- Blueprint Framework
- css
---

### About Blueprint




> [Blueprint](http://blueprintcss.org/) is a CSS framework, which aims to cut down on your development time. It gives you a solid foundation to build your project on top of, with an easy-to-use grid, sensible typography, useful plugins, and even a stylesheet for printing.




### .container


[css firstline="18"]/* A container should group all your columns. */
.container {
width: 950px;
margin: 0 auto;
}[/css]

<!-- more -->


`container` is where it all begins. This establishes your centered div with a width of 950 pixels. If you've done much CSS, this should look pretty familiar:

[css]margin: 0 auto; /* This is what centers the div */[/css]

Not much else to say except all of your other columns should be inside a div with the `container` class. Let's move on.


### .showgrid


[css firstline="24"].showgrid { background: url(src/grid.png);  }[/css]

`showgrid` is a nice tool to display your columns when you're laying out a page. Simply add it to the `container` div like so:

[html]<div class="container showgrid">DIV contents</div>[/html]

Once you're satisfied with how things are positioned, remove `showgrid` from your classes.

Let's skip down to line 33 or so.


### .span-x


[css firstline="33"]/* Sets up basic grid floating and margin. */
div.span-1, div.span-2, div.span-3, div.span-4, div.span-5,
div.span-6, div.span-7, div.span-8, div.span-9, div.span-10,
div.span-11, div.span-12, div.span-13, div.span-14, div.span-15,
div.span-16, div.span-17, div.span-18, div.span-19, div.span-20,
div.span-21, div.span-22, div.span-23, div.span-24 {
  float: left;
  margin-right: 10px;
}[/css]

This just sets up your span-x columns to all float left. It's a bit counter-intuitive, but this makes them all wrap around to the right of each other. It also sets up the 10 pixel margin to the right of each one for a nice gutter. That is, except for `last`. `last` is always the last column and forces any div with a `span-x` class to go below it. It also has no right margin:

[css firstline="44"]div.last { margin-right: 0; }[/css]

Next the `span-x` widths are set:

[css firstline="46"]/* Use these classes to set the width of a column. */
.span-1  { width: 30px; }
.span-2  { width: 70px; }
.span-3  { width: 110px; }
.span-4  { width: 150px; }
.span-5  { width: 190px; }
.span-6  { width: 230px; }
.span-7  { width: 270px; }
.span-8  { width: 310px; }
.span-9  { width: 350px; }
.span-10 { width: 390px; }
.span-11 { width: 430px; }
.span-12 { width: 470px; }
.span-13 { width: 510px; }
.span-14 { width: 550px; }
.span-15 { width: 590px; }
.span-16 { width: 630px; }
.span-17 { width: 670px; }
.span-18 { width: 710px; }
.span-19 { width: 750px; }
.span-20 { width: 790px; }
.span-21 { width: 830px; }
.span-22 { width: 870px; }
.span-23 { width: 910px; }
.span-24, div.span-24 { width: 950px; margin: 0; }[/css]

Notice above that `span-24` takes up the full width with no right margin. Want a wider gutter than the pre-established 10 pixels? No problem.


### .append-x


[css firstline="72"]/* Add these to a column to append empty cols. */
.append-1  { padding-right: 40px; }
.append-2  { padding-right: 80px; }
.append-3  { padding-right: 120px; }
.append-4  { padding-right: 160px; }
.append-5  { padding-right: 200px; }
.append-6  { padding-right: 240px; }
.append-7  { padding-right: 280px; }
.append-8  { padding-right: 320px; }
.append-9  { padding-right: 360px; }
.append-10 { padding-right: 400px; }
.append-11 { padding-right: 440px; }
.append-12 { padding-right: 480px; }
.append-13 { padding-right: 520px; }
.append-14 { padding-right: 560px; }
.append-15 { padding-right: 600px; }
.append-16 { padding-right: 640px; }
.append-17 { padding-right: 680px; }
.append-18 { padding-right: 720px; }
.append-19 { padding-right: 760px; }
.append-20 { padding-right: 800px; }
.append-21 { padding-right: 840px; }
.append-22 { padding-right: 880px; }
.append-23 { padding-right: 920px; } [/css]

Remember, each of the `span-x` columns are 30 pixels wide with a 10-pixel right margin. Likewise the above `append-x` classes will add an additional column to the right. Just do the math. `span-1` adds 40 pixels. `span-2`, 80 pixels and so on. We can add columns to the left with the `prepend` classes in the same way.


### .prepend-x


[css firstline="97"]/* Add these to a column to prepend empty cols. */
.prepend-1  { padding-left: 40px; }
.prepend-2  { padding-left: 80px; }
.prepend-3  { padding-left: 120px; }
.prepend-4  { padding-left: 160px; }
.prepend-5  { padding-left: 200px; }
.prepend-6  { padding-left: 240px; }
.prepend-7  { padding-left: 280px; }
.prepend-8  { padding-left: 320px; }
.prepend-9  { padding-left: 360px; }
.prepend-10 { padding-left: 400px; }
.prepend-11 { padding-left: 440px; }
.prepend-12 { padding-left: 480px; }
.prepend-13 { padding-left: 520px; }
.prepend-14 { padding-left: 560px; }
.prepend-15 { padding-left: 600px; }
.prepend-16 { padding-left: 640px; }
.prepend-17 { padding-left: 680px; }
.prepend-18 { padding-left: 720px; }
.prepend-19 { padding-left: 760px; }
.prepend-20 { padding-left: 800px; }
.prepend-21 { padding-left: 840px; }
.prepend-22 { padding-left: 880px; }
.prepend-23 { padding-left: 920px; } [/css]

`prepend-1` adds 40 pixels to the left of a column. `prepend-2` adds 80 pixels and so on. As long as we're talking about positioning, let's skip ahead a little bit.


### .push-x & .pull-x


[css firstline="138"]/* Use these classes on an element to push it into the
   next column, or to pull it into the previous column.  */

.pull-1 { margin-left: -40px; }
.pull-2 { margin-left: -80px; }
.pull-3 { margin-left: -120px; }
.pull-4 { margin-left: -160px; }
.pull-5 { margin-left: -200px; }

.pull-1, .pull-2, .pull-3,
.pull-4, .pull-5, .pull-5 {
  float:left;
	position:relative;
}

.push-1 { margin: 0 -40px 1.5em 40px; }
.push-2 { margin: 0 -80px 1.5em 80px; }
.push-3 { margin: 0 -120px 1.5em 120px; }
.push-4 { margin: 0 -160px 1.5em 160px; }
.push-5 { margin: 0 -200px 1.5em 200px; }

.push-0, .push-1, .push-2,
.push-3, .push-4, .push-5 {
  float: right;
	position:relative;
}[/css]

`pull-x` and `push-x` function in a similar way to `append-x` and `prepend-x`, except they'll actually push columns into one another instead of creating a wider gutter. `push-1` pushes the page element over to the right by one, 40-pixel column. `pull-1` pulls the page element over to the left by one 40-pixel column.

We skipped over some stuff. Let's go back to it:


### .border


[css firstline="123"]/* Border on right hand side of a column. */
div.border {
  padding-right: 4px;
  margin-right: 5px;
  border-right: 1px solid #eee;
}[/css]

`border` adds a right-border to any page element. Notice the right padding, margin and 1-pixel border all add up to 10 pixels to maintain the standard 10-pixel gutter.


### .colborder


`colborder` does the same except the right margin spans an entire column:

[css firstline="130"]/* Border with more whitespace, spans one column. */
div.colborder {
  padding-right: 24px;
  margin-right: 25px;
  border-right: 1px solid #eee;
}[/css]

The right padding, margin and 1-pixel border add up to 50 pixels this time.


### .box


`box` creates a padded box inside a column.

[css firstline="170"].box {
  padding: 1.5em;
  margin-bottom: 1.5em;
  background: #E5ECF9;
}[/css]


### hr


`hr` gets a nice default setting to make sure it crosses your column:

[css firstline="177"]hr {
  background: #ddd;
  color: #ddd;
  clear: both;
  float: none;
  width: 100%;
  height: .1em;
  margin: 0 0 1.45em;
  border: none;
}
hr.space {
  background: #fff;
  color: #fff;
}[/css]

I'm actually going to skip to the end because the `clearfix` classes seem a bit outmoded after reading the [article they are based on](http://www.positioniseverything.net/easyclearing.html). [Read this article instead](http://www.sitepoint.com/blogs/2005/02/26/simple-clearing-of-floats/).


### .clear


`clear` simply forces a column to go beneath the column before it.

[css firstline="212"].clear { clear:both; }[/css]

That's it. Hopefully reading this will give you a good sense of what positioning classes are available in [Blueprint](http://blueprintcss.org/) and how to use them. Please leave a comment if anything needs clarification.
