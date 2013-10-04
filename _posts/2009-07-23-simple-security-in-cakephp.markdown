---
author: admin
comments: true
date: 2009-07-23 01:23:38+00:00
layout: post
slug: simple-security-in-cakephp
title: Simple Security in CakePHP
wordpress_id: 134
categories:
- CakePHP
- components
- PHP
- web development
tags:
- CakePHP
- security
---

When I started to dig in to investigate using the [Security Component](http://book.cakephp.org/view/175/Security-Component) of [CakePHP](http://cakephp.org), I was a bit daunted. It took me quite a while to get my head around [ACL](http://book.cakephp.org/view/171/Access-Control-Lists) after all. Then I found [this article](http://teknoid.wordpress.com/2008/11/05/make-your-cakephp-forms-a-lot-more-secure/). Here's the crux:


> The Security component will create a hash based on the form fields produced by our Form Helper. If someone tampers with the form fields (by adding or removing or changing any field), the hash is not going to match with the expected one and the add() action will fail.

Yep, itâ€™s that simple.


Really? It just can't be that easy, can it? Yes. It can. I simply added the Security Component to my controller like so:

    
    var $components = array('Security');


Sure enough, when I reloaded a page with a form in my browser, this hidden field was there:

    
    <input type="hidden" id="TokenFields1483167134" value="f513aebc448fabe42c7feedf31d43fa5bd71ec79%3An%3A0%3A%7B%7D" name="data[_Token][fields]"></input>


I installed a Firefox Add-on that allowed me to tamper with the POST data, and when I submitted the form, it failed, or in CakePHP terms, it was "[Blackholed](http://book.cakephp.org/view/267/blackHole-object-controller-string-error)." Awesome.

This isn't going to protect me from all attacks, but it certainly is a good, easy start to implementing security in my application.
