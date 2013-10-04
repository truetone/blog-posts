---
author: admin
comments: true
date: 2008-11-23 15:07:09+00:00
layout: post
slug: incorporating-blueprint-css-into-your-new-wordpress-theme
title: Incorporating Blueprint CSS Into Your New Wordpress Theme
wordpress_id: 50
categories:
- Blueprint Framework
- css
- PHP
- web development
- wordpress
tags:
- blueprint
- css
- tutorial
- web development
- wordpress
---

If you're familiar with the [Blueprint CSS framework](http://www.blueprintcss.org/), you already know it can make your life a lot easier. So how do you get it into your [Wordpress](http://wordpress.org) theme? Luckily, Wordpress is designed to make your life easier too.

I'm assuming your know the basics of [Wordpress Theme Development](http://codex.wordpress.org/Theme_Development). That is, at the very least you need:



	
  * header.php

	
  * footer.php

	
  * index.php

	
  * style.css


Put those files in a folder named after your theme. And put that folder in `/wordpressroot/wp-content/themes/`.

Once you've gotten that far, download the Blueprint CSS Framework and drop the "blueprint" folder from that download into your theme's directory.

Finally, to include the new CSS files into your theme, just add this code to your header:

`<link rel="stylesheet" href="<?php bloginfo('stylesheet_directory'); ?>/blueprint/screen.css" type="text/css" media="screen, projection">
<link rel="stylesheet" href="<?php bloginfo('stylesheet_directory'); ?>/blueprint/print.css" type="text/css" media="print">
<!--[if IE]>
<link rel="stylesheet" href="<?php bloginfo('stylesheet_directory'); ?>/blueprint/ie.css" type="text/css" media="screen, projection">
<![endif]-->
<link rel="stylesheet" href="<?php bloginfo('stylesheet_url'); ?>" type="text/css" media="screen" />`

Pay attention to the order. You want to make sure that `href="<?php bloginfo('stylesheet_url'); ?>"` appears last in the list of style sheets. That's your `style.css` where you can tailor the CSS for your specific design.

That's it.
