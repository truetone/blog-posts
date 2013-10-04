---
author: admin
comments: true
date: 2010-02-14 15:55:11+00:00
layout: post
slug: why-use-blueprint-and-the-960-grid-system-in-the-baseline-theme
title: Why Use Blueprint and the 960 Grid System in the Baseline Theme?
wordpress_id: 256
categories:
- Blueprint Framework
- css
- web development
- wordpress
tags:
- 960 Grid System
- Blueprint Framework
- css
- wordpress
---

### An Inventory of Blueprint's Style Resets and Useful Classes


A friend contacted me about using the [Baseline Wordpress theme](http://baseline.truetoneenterprises.com), but asked why I included both [Blueprint](http://www.blueprintcss.org/) and the [960 Grid System](http://960.gs). The short answer is that Blueprint has a number of browser resets that I like to take advantage of and 960 GS offers greater flexibility in terms of the width of columns and their gutter widths. Especially if you want to adhere to the [Golden Ratio](http://net.tutsplus.com/tutorials/other/the-golden-ratio-in-web-design/) for design. 960 pixels divides very neatly into 3.

Let's take a look at what Blueprint does to reset some things to establish a cross-browser baseline. <!-- more -->First of all, all browsers have their own default style sheet for styling HTML elements. For example, here is [Firefox's style sheet](http://anthonygthomas.com/firefoxs-default-style-sheet/) that defines how the browser will render HTML if you don't define any styles. Unfortunately, all browser's default style sheets vary. Blueprint resets everything to level the field. Let's take a look at `src/reset.css` in your Blueprint directory.

[css firstline="8"]/* --------------------------------------------------------------

   reset.css
   * Resets default browser CSS.

-------------------------------------------------------------- */

html, body, div, span, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, code,
del, dfn, em, img, q, dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td {
  margin: 0;
  padding: 0;
  border: 0;
  font-weight: inherit;
  font-style: inherit;
  font-size: 100%;
  font-family: inherit;
  vertical-align: baseline;
}

body {
  line-height: 1.5;
}

/* Tables still need 'cellspacing="0"' in the markup. */
table { border-collapse: separate; border-spacing: 0; }
caption, th, td { text-align: left; font-weight: normal; }
table, td, th { vertical-align: middle; }

/* Remove possible quote marks (") from <q>, <blockquote>. */
blockquote:before, blockquote:after, q:before, q:after { content: ""; }
blockquote, q { quotes: "" ""; }

/* Remove annoying border on linked images. */
a img { border: none; }
[/css]

I don't want to spend tons of time going over this except to say that the cascading nature of cascading styles means that no matter what your browser's default style sheet is, all of the tags above have now been reset.

Just as important is Blueprint's treatment of type. If we look at `src/typography.css`, we'll find that all of the font sizes have been reset. This is very important and saves lots of time getting things to look the same across browsers. First it resets font size for the body and sets the default font families to sans-serif:

[css firstline="8"]/* Default font settings.
   The font-size percentage is of 16px. (0.75 * 16px = 12px) */
body {
  font-size: 75%;
  color: #222;
  background: #fff;
  font-family: "Helvetica Neue", Arial, Helvetica, sans-serif;
}[/css]

Next the headings are all reset. First the font weight (curiously) is set to "normal" and the color set to #111 (black):

[css firstline="21"]h1,h2,h3,h4,h5,h6 { font-weight: normal; color: #111; }[/css]

Then the sizes and bottom margins are set:

[css firstline="23"]
h1 { font-size: 3em; line-height: 1; margin-bottom: 0.5em; }
h2 { font-size: 2em; margin-bottom: 0.75em; }
h3 { font-size: 1.5em; line-height: 1; margin-bottom: 1em; }
h4 { font-size: 1.2em; line-height: 1.25; margin-bottom: 1.25em; }
h5 { font-size: 1em; font-weight: bold; margin-bottom: 1.5em; }
h6 { font-size: 1em; font-weight: bold; }[/css]

After that, margins are removed from any images within headings:

[css firstline="30"]
h1 img, h2 img, h3 img,
h4 img, h5 img, h6 img {
  margin: 0;
}[/css]

After headings, we come to the `p` tag. Zero margin on top, left and right with a 1.5 em margin at the bottom of each paragraph:

[css firstline="39"]p           { margin: 0 0 1.5em; }[/css]

Next, alignment classes for images with 1.5 em margins and 0 padding:

[css firstline="40"]p img.left  { float: left; margin: 1.5em 1.5em 1.5em 0; padding: 0; }
p img.right { float: right; margin: 1.5em 0 1.5em 1.5em; }[/css]

Anchors come after that with a default blue color and black `hover` and `focus` pseudoclasses:

[css firstline="43"]a:focus,
a:hover     { color: #000; }
a           { color: #009; text-decoration: underline; }[/css]

`blockquote` get's a margin, gray color and italics:

[css firstline="47"]blockquote  { margin: 1.5em; color: #666; font-style: italic; }[/css]

The `strong` tag is bold--as it should be:

[css firstline="48"]strong      { font-weight: bold; }[/css]

The `em` and `dfn` tags are italicized and `dfn` is bold:

[css firstline="49"]em,dfn      { font-style: italic; }
dfn         { font-weight: bold; }[/css]

The `sup` and `sub` tags get a line height of zero:

[css firstline="51"]sup, sub    { line-height: 0; }[/css]

The `abbr` and `acronym` tags are gray and get a dotted bottom border (which I find a little curious):

[css firstline="53"]abbr,
acronym     { border-bottom: 1px dotted #666; }[/css]

`address` tags get the same margin as paragraphs but with italics:

[css firstline="55"]address     { margin: 0 0 1.5em; font-style: italic; }[/css]

The `del` tag (which you should be using instead of strike) gets a gray color:

[css firstline="56"]del         { color:#666; }[/css]

Preformatted (`pre`) tags get at 1.5 em top and bottom margin and a zero right and left margin. Also, `pre`, `code` & `tt` are set to monospace fonts at 1 em with a line-height of 1.5 em:

[css firstline="58"]pre 				{ margin: 1.5em 0; white-space: pre; }
pre,code,tt { font: 1em 'andale mono', 'lucida console', monospace; line-height: 1.5; }[/css]

After that we move on to lists. Nested lists (`ol` & `ul`) get a zero top and bottom margin with a 1.5 em right and left margin:

[css firstline="65"]li ul,
li ol       { margin:0 1.5em; }[/css]

All lists get a zero top margin, 1.5 em right margin, 1.5 em bottom margin and a 1.5 em left margin:

[css firstline="67"]ul, ol      { margin: 0 1.5em 1.5em 1.5em; }[/css]

Unordered lists default to a disc style and ordered lists are set to decimal for their list style:

[css firstline="69"]ul          { list-style-type: disc; }
ol          { list-style-type: decimal; }[/css]

Definition list margins are set. `dl` and `dt` tags are set to bold:

[css firstline="72"]dl          { margin: 0 0 1.5em 0; }
dl dt       { font-weight: bold; }
dd          { margin-left: 1.5em;}[/css]

Tables are up next. Tables themselves get a 1.4 em bottom margin and 100% width. Table headers (`th`) are bold with #c3d9ff background color. Table headings, table data (`td`) and caption get some padding. A table row (`tr`) "even" class is established with a different background color. Table footers (`tfoot`) are italicized and finally, `caption` is given a background color of #eee.

[css firstline="80"]table       { margin-bottom: 1.4em; width:100%; }
th          { font-weight: bold; }
thead th 		{ background: #c3d9ff; }
th,td,caption { padding: 4px 10px 4px 5px; }
tr.even td  { background: #e5ecf9; }
tfoot       { font-style: italic; }
caption     { background: #eee; }[/css]

Finally we get to "Miscellaneous Classes". `small`, `large` and `hide` classes are pretty self explanatory:

[css firstline="92"].small      { font-size: .8em; margin-bottom: 1.875em; line-height: 1.875em; }
.large      { font-size: 1.2em; line-height: 2.5em; margin-bottom: 1.25em; }
.hide       { display: none; }[/css]

Some useful classes are established next with `loud`, `highlight`, `added` and `removed`. The `quiet` class is simple set to gray.:

[css firstline="96"].quiet      { color: #666; }[/css]

`loud` is set to black:

[css firstline="97"].loud       { color: #000; }[/css]

`highlight` has a yellow background:

[css firstline="98"].highlight  { background:#ff0; }[/css]

`added` has a green background with white text:

[css firstline="99"].added      { background:#060; color: #fff; }[/css]

And `removed` has a dark red background with white text:

[css firstline="100"].removed    { background:#900; color: #fff; }[/css]

Finally, there are `first`, `last`, `top` and `bottom` classes. First just makes sure there is no margin or padding on the left:

[css firstline="102"].first      { margin-left:0; padding-left:0; }[/css]

`last` does the same, but on the right:

[css firstline="103"].last       { margin-right:0; padding-right:0; }[/css]

`top` does what first and last did, but on the top (of course):

[css firstline="104"].top        { margin-top:0; padding-top:0; }[/css]

And `bottom` does what first, last and top did, but does it on the bottom:

[css firstline="105"].bottom     { margin-bottom:0; padding-bottom:0; }[/css]

Finally, we're going to take a look at what Blueprint offers for forms. Let's take a look at src/forms.css. The first thing we have is some styling for `label`, `fieldset` and `legend` tags.

Labels are bold, `fieldset` has a 1.4 em padding and a 1.5 em bottom margin with a gray border. `legend` is also bold with a 1.2 em font-size:

[css firstline="12"]label       { font-weight: bold; }
fieldset    { padding:1.4em; margin: 0 0 1.5em 0; border: 1px solid #ccc; }
legend      { font-weight: bold; font-size:1.2em; }[/css]

Next `text` and `title` classes are established for input tags and they are given the same formatting as `textarea` and `select` tags:

[css firstline="20"]input.text, input.title,
textarea, select {
  margin:0.5em 0;
  border:1px solid #bbb;
}[/css]

Next pseudoclasses are formatted for `focus` on form elements to change the border to black.

[css firstline="26"]input.text:focus, input.title:focus,
textarea:focus, select:focus {
  border:1px solid #666;
}[/css]

Next up `input` `text` classes are set to 300px wide with 5px padding. The `input` `title` class is also given a 1.5 em font size. `textarea` is a little wider and higher with 5px of padding:

[css firstline="31"]input.text,
input.title   { width: 300px; padding:5px; }
input.title   { font-size:1.5em; }
textarea      { width: 390px; height: 250px; padding:5px; }[/css]

Last but absolutely not least are some nice form validation classes you can take advantage of. The `notice`, `success` and `error` classes function for just what their names suggest. By now I'm going to assume you can read the styles so I won't inventory these one by one except to say that they're nice, intuitive classes for form validation.

[css firstline="40"].error,
.notice,
.success    { padding: .8em; margin-bottom: 1em; border: 2px solid #ddd; }

.error      { background: #FBE3E4; color: #8a1f11; border-color: #FBC2C4; }
.notice     { background: #FFF6BF; color: #514721; border-color: #FFD324; }
.success    { background: #E6EFC2; color: #264409; border-color: #C6D880; }
.error a    { color: #8a1f11; }
.notice a   { color: #514721; }
.success a  { color: #264409; }[/css]

The point of all of this is that _none_ of these are reset by the 960 grid established in the Baseline theme. Blueprint does a really nice job of resetting your styles and also includes a handful of other useful classes. What it _doesn't_ offer that the 960 Grid System _does_ is flexibility with design width, column width and gutter width. _That's_ why I decided to rely on the 960 Grid System for establishing the columns and combine it with Blueprint for it's wonderful job of resetting the styles.

Plus, I've been meaning to document all of these styles in Blueprint for a while now. If you don't use my [Baseline theme](http://baseline.truetoneenterprises.com/), this may also provide useful in terms of documenting what Blueprint is doing for you. [Take a look at this page to see what some of the classes like `error` or `success` look like](http://anthonygthomas.com/articles/a-demo-of-some-of-blueprints-classes/).
