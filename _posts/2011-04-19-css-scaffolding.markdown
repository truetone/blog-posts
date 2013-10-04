---
author: admin
comments: true
date: 2011-04-19 00:12:55+00:00
layout: post
slug: css-scaffolding
title: CSS Scaffolding
wordpress_id: 533
categories:
- css
- web development
---

Last week [I gave a talk](http://www.slideshare.net/kmloomis/minne-webcon-2011v5) at [MinneWebCon](http://minnewebcon.umn.edu) along with Ken Loomis and [Ethan Poole](http://ethanpoole.com/). My section of the talk dealt with [the CSS we use at work](http://sua.umn.edu/_web/css-styleguide.php). One of the main problems I've come to have with using CSS frameworks is that they put presentation back into the markup. Every CSS framework I've seen has classes like these:



	
  * ez-50 (ez-css)

	
  * container_12 (960GS)

	
  * grid_1 (960GS)

	
  * span-4 (Blueprint)


After years of adopting standards that keep presentation separate from the markup, frameworks like these ([and others](http://www.testking.com/techking/roundups/27-great-css-frameworks-you-must-check-out/)) put it right back into the code. Not only is that a bad practice, but it removes one of the chief benefits of CSS: the ability to change your presentation without touching the markup.

The most common problem these frameworks solve is laying out columns. So I came up with a handful of CSS classes that solve the same problem, but do so in a way that will allow you to alter the appearance of the pages _without altering the markup_.

These classes are applicable in a general way (i.e., within the content), so it's useful to keep them named as they are for that purpose. You can also copy these same styles to your ids to get the desired widths and column layout.Â I encourage you to write these styles into page ids whenever possible as that will make your page markup more semantic. You should think of these classes more like scaffolding than a framework. You can get started quickly, then modify them to meet your needs.Â [The minified file is only 412 bytes](http://anthonygthomas.com/wp-content/uploads/2011/04/framework.css.zip).<!-- more -->

[css]/* anthonygthomas.com/
   v1.0 | 20110417
   License: none (public domain)
*/

/******

 # Table of Contents #

## Define columns
### Last column
## Narrow column
### Last narrow column
## Wide column
## First column
## Column clearfix

 *******/

/* Define columns */
/* apply this to any block element */
.column {
    display: inline-block;
    float:left;
    margin-right: 2%;
    width: 48%;
}
    /* Last column */
    /* apply this to the last column */
    .column.last {
	margin-left: 2%;
	margin-right: 0;
	width: 48%;
    }

/* Narrow column */
.column.narrow {
    margin-right: 5%;
    width: 30%;
}
    /* Last narrow column */
    .column.narrow.last {
	margin-left: 0;
	margin-right: 0;
    }

/* Wide column */
.column.wide {
    margin-right: 4%;
    width: 66%;
}

/* First column */
.first {
    clear:left;
}

/* Column clearfix */
/* perishablepress.com/press/2009/12/06/new-clearfix-hack/ */
.column:after {
	visibility: hidden;
	display: block;
	font-size: 0;
	content: " ";
	clear: both;
	height: 0;
	}
* html .column             { zoom: 1; } /* IE6 */
*:first-child+html .column { zoom: 1; } /* IE7 */[/css]

[Here is a demo page](http://anthonygthomas.com/examples/test.html).


### The Classes




#### The column Class


[css]/* apply this to any block element */
.column {
    display: inline-block;
    float:left;
    margin-right: 2%;
    width: 48%;
}[/css]

This creates a 50% column for any block element. By default columns float left, so the next consecutive element with the same class will end up on the right side of the preceding element. To get rid of the 2% margin in the right column and add a 2% gutter to the left of the second column (for a total of a 4% gutter) use the `.last` class:

[css]/* apply this to the last column */
    .column.last {
	margin-left: 2%;
	margin-right: 0;
	width: 48%;
    }[/css]


#### The narrow Class (three columns)


This creates a 30% width column with a 5% right margin. To make the third column work correctly, you need to add a `last` class.

[css]/* Narrow column */
.column.narrow {
    margin-right: 5%;
    width: 30%;
}
    /* Last narrow column */
    .column.narrow.last {
	margin-left: 0;
	margin-right: 0;
    }[/css]


#### The wide Class


[css]/* Wide column */
.column.wide {
    margin-right: 4%;
    width: 66%;
}[/css]


#### The first Class


[css]/* First column */
.first {
    clear:left;
}[/css]

Apply this to the first column to force the element to wrap below it's preceding element.


#### The clearfix


This is a common "clearfix" method. You can find variations on this all over the web. [This one is from Perisable Press](http://perishablepress.com/press/2009/12/06/new-clearfix-hack/). Rather than selectively apply the class, I wrote into a class that I knew needed clearing.

[css]/* Column clearfix */
/* perishablepress.com/press/2009/12/06/new-clearfix-hack/ */
.column:after {
	visibility: hidden;
	display: block;
	font-size: 0;
	content: " ";
	clear: both;
	height: 0;
	}
* html .column             { zoom: 1; } /* IE6 */
*:first-child+html .column { zoom: 1; } /* IE7 */[/css]

This is not a completely tested framework. I make no guarantees that it will work in all old browsers.

The thing I encourage you to take away is that CSS frameworks--if used as-is--are not semantic. It's not hard to come up with your own, more semantic framework. Instead of thinking of these as grid systems, you should think of them as scaffolding. This is a good place to start. Take it from here and modify it to fit your own needs.
