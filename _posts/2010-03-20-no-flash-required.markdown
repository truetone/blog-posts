---
author: admin
comments: true
date: 2010-03-20 17:30:30+00:00
layout: post
slug: no-flash-required
title: No Flash Required
wordpress_id: 421
categories:
- css
- JavaScript
- JQuery
- web development
tags:
- css
- JavaScript
- jquery
- web develop
---

### UPDATE II


I just updated the theme of this site so:



	
  1. It uses even less JavaScript (all animations and transformations are done w/ CSS3 tranforms)

	
  2. It's HTML5


More on both those points in a post soon. The upshot is that this post refers to a past theme and may be confusing.

![JPEF of the nav menu from anthonygthomas.com](http://anthonygthomas.com/wp-content/uploads/2010/03/nav.jpg)I just added a pretty sweet bit of eye candy to my nav menu using strictly CSS & JQuery. [The method is here](http://net.tutsplus.com/tutorials/html-css-techniques/how-to-build-a-lava-lamp-style-navigation-menu/). [The code is here](http://github.com/JeffreyWay/SpasticNav).

You do need to have a either a webKit or Mozilla browser for it to work properly. The point is that there are fewer and fewer things that Flash can do that can't be done with HTML, JavaScript and CSS. In fact, just about every single bit of animation I've had done in Flash over the last couple of years could be recreated with JQuery & CSS3.


### UPDATE


Since I couldn't get the z-index to function properly in Internet Explorer, I used [JQuery's .browser property](http://api.jquery.com/jQuery.browser/) so the function only runs in supported browsers--namely, Mozilla or WebKit. The function actually degraded fairly well, except for Internet Explorer's buggy handling of z-index. For reference, I've included my version of the plug-in because it has this and other subtle variations.<!-- more -->

[javascript](function($) {
	if ($.browser.webkit || $.browser.mozilla) {

		$.fn.spasticNav = function(options) {

			options = $.extend({
				overlap : 2,
				speed : 500,
				reset : 1500,
				color : '#BDD2FF',
				easing : 'easeOutExpo'
			}, options);

			return this.each(function() {

			 	var nav = $(this),
			 		currentPageItem = $('.current_page_item', nav),
			 		blob,
			 		reset;

			 	$('<li id="blob"></li>').css({
			 		width : currentPageItem.outerWidth(),
			 		height : currentPageItem.outerHeight() + options.overlap,
			 		left : currentPageItem.position().left,
			 		top : currentPageItem.position().top - options.overlap / 2,
			 		backgroundColor : options.color
			 	}).appendTo(this);

				$('.current_page_item a').css('z-index', 1000);

			 	blob = $('#blob', nav);

				$('li:not(#blob)', nav).hover(function() {
					// mouse over
					clearTimeout(reset);
					blob.animate(
						{
							left : $(this).position().left,
							width : $(this).width()
						},
						{
							duration : options.speed,
							easing : options.easing,
							queue : false
						}
					);
				}, function() {
					// mouse out
					reset = setTimeout(function() {
						blob.animate({
							width : currentPageItem.outerWidth(),
							left : currentPageItem.position().left
						}, options.speed)
					}, options.reset);

				});

			}); // end each

		};

	}

})(jQuery);[/javascript]
