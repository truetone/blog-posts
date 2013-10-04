---
author: admin
comments: true
date: 2010-02-16 21:19:32+00:00
layout: post
slug: baseline-theme-version-1-0-1
title: Baseline Theme Version 1.0.1
wordpress_id: 360
categories:
- web development
- wordpress
tags:
- baseline theme
- web development
- wordpress
---

There is a new version of the [Baseline Theme](http://baseline.truetoneenterprises.com). In the last few days of tinkering with it and modifying it for use with this website, I noticed a small bug. The [Blueprint](http://blueprintcss.org/) IE reset was acting funny in conjunction with the [IE8 JavaScript](http://code.google.com/p/ie7-js/). I chose to make IE8.js the default with the option of including Blueprint's reset instead.<!-- more --> Here is the pertinent change in header.php:

[php htmlscript="true" firstline="14"]<?php

/*

Add this to the HTML below if you want to use Blueprint's IE reset style sheet. The IE8 JavaScript should
fix the same things so you shouldn't need both. This is here if you'd rather use it than the JavaScript.

<!--[if IE]>
<link rel="stylesheet" href="<?php bloginfo('stylesheet_directory'); ?>/blueprint/ie.css" type="text/css" media="screen, projection" />
<![endif] -->

*/

?>

<!-- Remove this JavaScript link if you decide to use Blueprint's CSS reset instead. I recommend using this instead. -->

<!--[if lt IE 8]>
<script src="http://ie7-js.googlecode.com/svn/version/2.0(beta3)/IE8.js" type="text/javascript"></script>
<![endif]-->[/php]

[You can download the theme here](http://baseline.truetoneenterprises.com).
