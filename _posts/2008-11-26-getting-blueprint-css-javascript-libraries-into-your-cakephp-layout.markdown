---
author: admin
comments: true
date: 2008-11-26 19:55:58+00:00
layout: post
slug: getting-blueprint-css-javascript-libraries-into-your-cakephp-layout
title: Getting Blueprint CSS & JavaScript Libraries Into Your CakePHP Layout
wordpress_id: 59
categories:
- Blueprint Framework
- CakePHP
- css
- JavaScript
- PHP
- web development
tags:
- Blueprint Framework
- CakePHP
- JavaScript
- jquery
- libraries
- PHP
- tutorial
- web development
---

Updated 12/3/2008

The other day I wrote about [getting the Blueprint CSS framework into your Wordpress theme](http://anthonygthomas.com/2008/11/23/incorporating-blueprint-css-into-your-new-wordpress-theme/). If you're developing in [CakePHP](http://cakephp.org), it's even easier to link multiple style sheets and JavaScript libraries to your [layout file](http://book.cakephp.org/view/96/Layouts).

`<?php`

`$css = array('blueprint/screen', 'blueprint/ie', 'style');
$jslibraries = array('prototype', 'scriptaculous', 'jquery');``
echo $html->css('blueprint/print', 'stylesheet', 'media="print"');``
echo $html->css($css, 'stylesheet', 'media=â€screen, projectionâ€');
echo $javascript->link($jslibraries);`
`?>`

Let's take these one at a time.

`$css = array('blueprint/screen', 'blueprint/ie', 'style');`

[CakePHP's html helper](http://book.cakephp.org/view/205/HTML) will load any css file you specify. First, make sure the css files are in `app/webroot/css`. Then put any css files you want to link to your layout in an array like I have above. You might have noticed that I didn't include print in my array. That's because we want to add an media="print" as a separate attribute that the other style sheets won't have.

Once they're loaded into your array, simply put `echo $html->css($css);` in the head of your layout. The output will be:
`<link rel="stylesheet" type="text/css" href="/app/webroot/css/blueprint/screen.css" />
<link rel="stylesheet" type="text/css" href="/app/webroot/css/blueprint/ie.css" />
<link rel="stylesheet" type="text/css" href="/app/webroot/css/style.css" />`

We still haven't linked our print style sheet. Make sure you link the print style sheet above the others so they override it. We can add `media="print"` by putting this into our layout head:

`echo $html->css('blueprint/print', 'stylesheet', 'media="print"');`

So now:

`$css = array('blueprint/screen', 'blueprint/ie', 'style');
``echo $html->css('blueprint/print', 'stylesheet', 'media="print"');``
``echo $html->css($css, 'stylesheet', 'media=â€screen, projectionâ€');`

Results in:

`<link rel="stylesheet" type="text/css" href="/cvp-msi/https/app/webroot/css/blueprint/print.css" media="print" />
<link rel="stylesheet" type="text/css" href="/cvp-msi/https/app/webroot/css/blueprint/screen.css" media="screen, projection" />
<link rel="stylesheet" type="text/css" href="/cvp-msi/https/app/webroot/css/blueprint/ie.css" media="screen, projection" />
<link rel="stylesheet" type="text/css" href="/cvp-msi/https/app/webroot/css/style.css" media="screen, projection" />`

Two things to note. In `$html->css($path, $attributes)`, the first argument is the path from `app/webroot/css`. The second argument is html attributes.

Linking JavaScript libraries is very similar.

`$jslibraries = array('prototype', 'scriptaculous', 'jquery');`

This will link to `prototype.js`, `scriptaculous.js` and `jquery.js` respectively as long as there in `app/webroot/js`.

Put `echo $javascript->link($jslibraries);` into the head of your layout and you're done. You have all three JavaScript libraries at your disposal.

Other good resources:



	
  * [CakePHP Core Helpers](http://book.cakephp.org/view/181/Core-Helpers)

	
  * [Developing With CakePHP](http://book.cakephp.org/view/27/Developing-with-CakePHP)

	
  * [CakePHP API JavaScript link Helper](http://api.cakephp.org/class_javascript_helper.html#cab1eb59cacd608ec02e79cfd8710094)

	
  * [CakePHP API CSS link Helper](http://api.cakephp.org/class_html_helper.html#b8e7fe2bca7be4c25f9a660038131f00)


