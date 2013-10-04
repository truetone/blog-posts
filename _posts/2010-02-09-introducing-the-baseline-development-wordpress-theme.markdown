---
author: admin
comments: true
date: 2010-02-09 01:53:16+00:00
layout: post
slug: introducing-the-baseline-development-wordpress-theme
title: Introducing the Baseline Development Wordpress Theme
wordpress_id: 233
categories:
- Blueprint Framework
- css
- JavaScript
- web development
- wordpress
tags:
- themes
- wordpress
---

I've come up with some habits that I've developed from building themes for Wordpress over the years. One, is to start with a nearly blank style sheet. I also like to hook in several JavaScript libraries and CSS frameworks from the start to take advantage of things like JQuery, Blueprint's CSS reset and Superfish menus.<!-- more -->

I've decided to build and release an XHTML 1.0 version and release it as a springboard for others who may want to take advantage of the same sets of tools. The theme isn't much to look at (that's the point), but it includes:



	
  * [Blueprint CSS framework](http://blueprintcss.org/)

	
  * [](http://blueprintcss.org/)[960 Grid System](http://960.gs/)

	
  * [](http://960.gs/)[JQuery 1.4.0](http://jquery.com/)

	
  * [JQuery UI 1.7.1](http://jqueryui.com/)

	
  * [](http://jquery.com/)[Superfish JQuery menu](http://users.tpg.com.au/j_birch/plugins/superfish/) (with [HoverIntent.js](http://cherne.net/brian/resources/jquery.hoverIntent.html))

	
  * [IE8 JavaScript Library](http://code.google.com/p/ie7-js/)

	
  * [](http://users.tpg.com.au/j_birch/plugins/superfish/)Widget-enabled sidebar

	
  * [Test Content file from WP-Candy](http://wpcandy.com/articles/easier-theme-development-with-the-sample-post-collection.html)

	
  * [Valid XHTML 1.0](http://validator.w3.org/check?uri=http%3A%2F%2Fbaseline.truetoneenterprises.com%2F)


[More information here](http://baseline.truetoneenterprises.com).

If you want to use all of these tools, you're all set. If you want to use a few, it's just a matter of removing them from header.php.

First off, I really like Blueprint's browser reset, so I wanted to include that here. I also like the flexibility the 960 Grid System offers in terms of column width. As a result, I've included them both.

[php htmlscript="true" firstline="9"]<link rel="stylesheet" href="<?php bloginfo('stylesheet_directory'); ?>/blueprint/screen.css" type="text/css" media="screen, projection" />
<link rel="stylesheet" href="<?php bloginfo('stylesheet_directory'); ?>/960.css" type="text/css" media="screen, projection" />
<link rel="stylesheet" href="<?php bloginfo('stylesheet_directory'); ?>/blueprint/print.css" type="text/css" media="print" />[/php]

If you don't wish to use any of these, simply remove them from header.php. Next up is the Superfish CSS:

[php firstline="12" htmlscript="true"]<link rel="stylesheet" href="<?php bloginfo('stylesheet_directory'); ?>/superfish/css/superfish.css" type="text/css" media="screen, projection" />[/php]

You must keep this if you're using Superfish. If you're not going to use Superfish, you should remove these lines too:

[php firstline="29" htmlscript="true"]<script type="text/javascript" src="<?php bloginfo('stylesheet_directory'); ?>/superfish/js/superfish.js"></script>
<script type="text/javascript" src="<?php bloginfo('stylesheet_directory'); ?>/superfish/js/hoverIntent.js"></script>[/php]

[js firstline="32" htmlscript="true"]<script type="text/javascript">

    $(document).ready(function() {
        $('ul.sf-menu').superfish();
    });

</script>[/js]

Next is Blueprint's Internet Explorer CSS reset:

[php firstline="13" htmlscript="true"]<!--[if IE]>
<link rel="stylesheet" href="<?php bloginfo('stylesheet_directory'); ?>/blueprint/ie.css" type="text/css" media="screen, projection" />
<![endif] -->[/php]

I've also had good luck using the IE8 JavaScript library, so that's included next:

[html firstline="17"]<!--[if lt IE 8]>
<script src="http://ie7-js.googlecode.com/svn/version/2.0(beta3)/IE8.js" type="text/javascript"></script>
<![endif]-->[/html]

Then JQuery and JQuery UI libraries:

[html firstline="21"]<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.4.0/jquery.min.js" type="text/javascript"></script>
<script src="http://ajax.googleapis.com/ajax/libs/jqueryui/1.7.1/jquery-ui.min.js" type="text/javascript"></script>[/html]

That's it. All the frameworks and libraries are loaded. If you don't think you'll need any one of them, you can just take them out. WARNING: The layout of the columns does rely on the 960 Grid System CSS file. If you take that out of the head the columns won't work and you'll break the layout.

Otherwise this should give you a good start that will allow you to take advantage of tons of cool JQuery stuff and leverages a very popular CSS Grid System for laying out columns. It should be easy to modify this theme to fit your own design.

[Download the theme here](http://baseline.truetoneenterprises.com).
