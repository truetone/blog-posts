---
author: admin
comments: true
date: 2010-02-15 19:58:38+00:00
layout: post
slug: blueprint-optional-fancy-type-plugin
title: Blueprint Optional Fancy-Type Plugin
wordpress_id: 312
categories:
- Blueprint Framework
- css
- web development
- wordpress
tags:
- baseline theme
- Blueprint Framework
- css
- wordpress
---

The [Baseline Development Wordpress Theme](http://baseline.truetoneenterprises.com) has [Blueprint](http://blueprintcss.org/) plugged in already. There are some optional Blueprint plugins you can take advantage of. We'll take a look at the fancy-type plug-in.<!-- more -->

First of all, to link it in just add this to header.php:

[php htmlscript="true"]<link rel="stylesheet" href="<?php bloginfo('stylesheet_directory'); ?>/blueprint/plugins/fancy-type/screen.css" type="text/css" media="screen, projection" />[/php]

The first thing this will do for you is indent your paragraphs:

[css]/* Indentation instead of line shifts for sibling paragraphs. */
   p + p { text-indent:2em; margin-top:-1.5em; }
   form p + p  { text-indent: 0; } /* Don't want this in forms. */[/css]

Next up is the `alt` class for some fancy type:

[css firstline="15"]
/* For great looking type, use this code instead of asdf:
   <span class="alt">asdf</span>
   Best used on prepositions and ampersands. */

.alt {
  color: #666;
  font-family: "Warnock Pro", "Goudy Old Style","Palatino","Book Antiqua", Georgia, serif;
  font-style: italic;
  font-weight: normal;
}[/css]

You also get a class for fancy quote marks:

[css firstline="27"]/* For great looking quote marks in titles, replace "asdf" with:
   <span class="dquo">&#8220;</span>asdf&#8221;
   (That is, when the title starts with a quote mark).
   (You may have to change this value depending on your font size). */

.dquo { margin-left: -.5em; } [/css]

Reduced size type with incremental leading:

[css firstline="35"]/* Reduced size type with incremental leading
   (http://www.markboulton.co.uk/journal/comments/incremental_leading/)

   This could be used for side notes. For smaller type, you don't necessarily want to
   follow the 1.5x vertical rhythm -- the line-height is too much.

   Using this class, it reduces your font size and line-height so that for
   every four lines of normal sized type, there is five lines of the sidenote. eg:

   New type size in em's:
     10px (wanted side note size) / 12px (existing base size) = 0.8333 (new type size in ems)

   New line-height value:
     12px x 1.5 = 18px (old line-height)
     18px x 4 = 72px
     72px / 5 = 14.4px (new line height)
     14.4px / 10px = 1.44 (new line height in em's) */

p.incr, .incr p {
	font-size: 10px;
	line-height: 1.44em;
	margin-bottom: 1.5em;
}[/css]

And finally the `caps` class:

[css]/* Surround uppercase words and abbreviations with this class.
   Based on work by JÃ¸rgen Arnor GÃ¥rdsÃ¸ Lom [http://twistedintellect.com/] */

.caps {
  font-variant: small-caps;
  letter-spacing: 1px;
  text-transform: lowercase;
  font-size:1.2em;
  line-height:1%;
  font-weight:bold;
  padding:0 2px;
}[/css]

[Go here to take a look at what these classes do in practice](http://anthonygthomas.com/articles/blueprint-fancy-type-classes/).
