---
author: admin
comments: true
date: 2009-05-22 13:54:36+00:00
layout: post
slug: roll-your-own-cakephp-components
title: Roll Your Own CakePHP Components
wordpress_id: 103
categories:
- PHP
- web development
tags:
- Add new tag
- CakePHP
- components
- dry
- gtd
- mcv
- web development
---

As someone who is not formally trained as a programmer, I often understand concepts long before actually putting them into practice. _Don't Repeat Yourself _(DRY) seems simple enough. Of course I don't want to repeat myself while programming. Who wants to dig through lines of code to find a litte snippet of logic you once wrote? Still, when you're pressed for time, sometimes you just have to _Get Things Done_ (GTD). So best practices go through the window and you hammer out some spaghetti code so you can move on.

It's only recently, since I've slowed down to finally understand how to write [CakePHP](http://cakephp.org) [Components](http://book.cakephp.org/view/63/Introduction), that I've realized that DRY enhances GTD. Now that I've got it all straight in my head, I'm a component _evangelist_.

At this point I'm going to assume that you're familiar with MCV architecture and its benefits. Once in a while there's a bit of logic that you find yourself coding into a controller that you realize you're going to want to use in other controllers. It's not specific to the model. That's where components come in. They're bits of logic that can be used by more than one controller. Let's look at a simple one that converts mm/dd/yyyy dates to a Unix timestamp.

    
    
    



The function itself is not all that complicated. The thing is that I'm going to want to use this where ever I need to convert dates. Since the component is called "Date", it's named with the CakePHP convention for components: DateComponent. The file is called date.php and is saved in `app/controllers/components`.

Now we have to tell our controller(s) to use it. I'm using it across several controllers, so I'm adding it to `app/app_controller.php` by adding it to the `$components` var: `var $components = array('Date');`

Now I can access it in any controller like so: `$tmsmp = $this->Date->mkTimestamp($thedate, $thetime);`

The whole point is that components don't have to be complex, they're just code you want to reuse that doesn't necessary apply to one model. They will save you time and clean up your controllers.
