---
author: admin
comments: true
date: 2008-06-20 18:55:33+00:00
layout: post
slug: wow-acl-is-hard
title: Wow. ACL is Hard
wordpress_id: 34
categories:
- ACL
- CakePHP
- PHP
- web development
tags:
- access control lists
- CakePHP
- modified preorder tree traversal algorithm
- web development
---

That is Access Control Lists. I've been developing with [CakePHP](http://cakephp.org) this spring and summer and it was all going very well until I actually needed to control access to the application. It's not even that CakePHP falls short here. There are apparently tons of built-in tools for managing access. They're just poorly documented and the community is relatively new so no one has built a complete plug in. If you're looking for a solution like I was, I'm afraid I'm not going to give you the best answer here. I did find something that works, so read on. Especially if you're learning ACL or Modified Preorder Tree Traversal Algorithm (MPTTA) for the first time.

Disclosure: I'm not formally trained as a programmer/developer. Everything I've learned, I've taught myself. So there are definitely some silos in my knowledge as I've learned things on the basis of necessity. I have, however, been developing in PHP for over six years. So it's not all that bad.

So the learning curve for implementing ACL has been relatively steep for me. First, I had to get my head around the concept. The big picture is easy. [What we're after is a tree of access with 'admin' at the root and everything else branching off from that with diminishing access](http://book.cakephp.org/view/171/access-control-lists). That's not hard to conceptualize. What is hard is putting that into practice.

I messed around with this for a long time before stumbling upon [this tutorial about the Modified Preorder Tree Traversal Algorithm](http://www.sitepoint.com/article/hierarchical-data-database/2). Stop now. Read it. Come back.

Now you should understand the concepts that drive CakePHP's ACL. Unfortunately here is also where we depart from using CakePHP's tools. At least until a decent plug-in comes along that allows you to manage Access Request Objects (ARO) and Access Control Objects (ACO) via a good, web-based interface.

After many attempts with [various solutions that are currently avaliable](http://bakery.cakephp.org/tags/view/acl), I finally settled on [Authake](http://conseil-recherche-innovation.net/authake).

Pros:



	
  * Works in CakePHP 1.2

	
  * User, ARO & ACO adminstration is a snap

	
  * Access control works immediately without modifying anything you've built in your app.


Cons:

	
  * Installation requires you replace the entire CakePHP engine with Authake's modified version. This will make upgrading CakePHP a lot harder.

	
  * The developer has abandoned it in favor of developing in RoR. No hope for future versions unless the community continues development. Personally, I'd prefer a plug-in like[ Jeff Loiselle's ACL Management Plugin](http://bakery.cakephp.org/articles/view/acl-management-plugin) that I could just drop right into app/plugins without replacing the entire installation. ([The issue I have with Jeff's are all listed on his "Known Bugs" list](http://dev.newnewmedia.com/cakephp/admin/acl). Namely, "does not show inherited permissions, does not show full path in finder & does not have crud fields". Unfortunately, those are three very major elements of managing ACL.)


If you are reading this in the not so distant future and someone had developed a plugin that has an admin area like Authake's but drops into app/plugins like Jeff's plugin, please, _please_ let me know.
