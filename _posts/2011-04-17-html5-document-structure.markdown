---
author: admin
comments: true
date: 2011-04-17 17:42:09+00:00
layout: post
slug: html5-document-structure
title: HTML5 Document Structure
wordpress_id: 515
categories:
- css
- html
- web development
---

Since I've started working with HTML5 Â a bit, I've had to adjust my thinking about page structure. HTML 5 page structure differs from HTML 4 or XHTML _significantly_. (X)HTML document structure should look like this:<!-- more -->

[caption id="attachment_518" align="aligncenter" width="273" caption="Proper document structure in HTML 4 and XHTML. (http://cssglobe.com/post/1213/how-to-use-headings-in-html)"][![html headings diagram](http://anthonygthomas.com/wp-content/uploads/2011/04/headings-273x300.gif)](http://cssglobe.com/post/1213/how-to-use-headings-in-html)[/caption]

This has changed in HTML5. [HTML5 has "outlining elements" that essentially reset the page hierarchy](http://dev.opera.com/articles/view/new-structural-elements-in-html5/). This is a little tough to get your head around if you've spent as many years as I have using the page structure in the figure above. A diagram of an HTML5 document might look like this:

[caption id="attachment_521" align="aligncenter" width="273" caption="A demonstration of HTML5 "sectioning" elements."]![HTML5 Document Structure](http://anthonygthomas.com/wp-content/uploads/2011/04/html5.png)[/caption]

Notice the difference? It's fairly subtle, but most recognizable in the `section` element. In (X)HTML, the headings in the article section would be subject to the same hierarchy as the rest of the document so article headings would have to start with `h3` or maybe even `h4`. In HTML5, `nav`, `section`, `article` and `aside` are "sectioning" elements, so they can have their own hierarchy of headings. Notice that the `header` HTML5 tag is not a sectioning element, so it's `h1` still rules the page.

**Note:** No browsers support this outlining algorithm. (I know.) It's coming, so I think it's important to get our heads around it now.
