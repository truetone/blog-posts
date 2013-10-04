---
author: admin
comments: true
date: 2010-09-06 02:01:08+00:00
layout: post
slug: baseline-theme-version-1-1
title: Baseline Theme Version 1.1
wordpress_id: 449
categories:
- Baseline Theme
- web development
- wordpress
tags:
- baseline theme
- web development
- wordpress
---

It had been a while since I'd done any Wordpress development, but I recently dusted off my Baseline theme to start a new project only to find that the jQuery libraries weren't loading properly. A quick bit of research revealed that new versions of Wordpress require a slightly different syntax when using jQuery, so I made a few changes.



	
  1. jQuery UI is now loaded using `wp_enqueue_script("jquery-ui");` instead of linking to Google's hosted copy.

	
  2. The code for loading Superfish uses this syntax:[javascript]jQuery(document).ready(function() {
        jQuery('ul.sf-menu').superfish();
    });[/javascript]

	
  3. Lists will now obey margins of neighboringÂ floating elements by default because I declared this in style.css:[css]div#content ul, div#content ol {
	list-style-position: inside;
}[/css]


Later versions of Wordpress don't support the '$' syntax normally used with jQuery. Wherever you would normally use '$' (such as `$(document).ready ();`), you have to use 'jQuery' instead (`jQuery.document.ready();`). There were a couple of other housekeeping items like reformatting style.css and creating a table of contents for it. Baseline should be all set to work with the latest versions of Wordpress again. [Download it here](http://baseline.truetoneenterprises.com).
