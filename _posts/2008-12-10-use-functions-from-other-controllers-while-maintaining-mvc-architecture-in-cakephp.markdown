---
author: admin
comments: true
date: 2008-12-10 23:52:01+00:00
layout: post
slug: use-functions-from-other-controllers-while-maintaining-mvc-architecture-in-cakephp
title: Use Functions from Other Controllers While Maintaining MVC Architecture in
  CakePHP
wordpress_id: 66
categories:
- About the Author
- CakePHP
- PHP
- This Site
- web development
tags:
- CakePHP
- dry
- mvc
- PHP
- web development
---

### UPDATE (7/22/2009)


requestionAction may not be the best solution. [Read this](http://teknoid.wordpress.com/2009/01/17/can-we-talk-enough-about-requestaction/).

At my day job, I'm working on an application to keep track of specimens for our lab. A specimen is sent to the lab, then divided into aliquots which are put into boxes and stored in freezers. The previous sentence ought to give you some idea of the architecture of the database, which in turn drives the Model for my application.

To take a step back for a second, I'm developing the application using the [CakePHP framework](http://cakephp.org) which uses [MVC architecture](http://en.wikipedia.org/wiki/Model-view-controller).

As you may have guessed I have specimen, aliquot, boxes and freezers tables. In turn then, I have Specimen, Aliquot, Box and Freezer Models.

The trick here is that I want to alert users when there are aliquots in the system that have not yet been assigned to boxes. It's a simple query:

    
    SELECT COUNT(aliquot.id)
    FROM aliquots
    WHERE aliquots.box_id IS NULL


The problem is that I want the number of unstored aliquots to be displayed on every page in the left column as a persistent reminder that there are are aliquots that need to be put away. I want to do that in a way that maintains the MVC architecture and doesn't violate the [DRY philosophy](http://en.wikipedia.org/wiki/Don%27t_repeat_yourself).

Since the query is run on the aliquots table and each view is generally specific to it's own model, I either have to run a recursive query to access data across models--which adds overhead--or implement the solution below which lightens the load a bit and is a more elegant bit of code. ([Tip of the hat to Jon Bennet for offering the solution](http://groups.google.com/group/cake-php/browse_thread/thread/b302d650fa9ec36e/82fd46c3d4e9eeec#82fd46c3d4e9eeec).)

[The solution involves CakePHP's requestAction()](http://api.cakephp.org/class_object.html#c40a38b60a3748b9cf75215b92ee3db1).

I can define the method in my aliquots controller and call it from anywhere. So if aliquots_controller.php has a method that retrieves the data from the model (in this case called 'unstored') I can simply put the following code into my layout:

    
    $unstored = $this->requestAction('aliquots/unstored');
    if(!empty($unstored)) {
    echo $html->link('<strong>' . $unstored['unstored'] . ' aliquots have not been stored.</strong>', '/aliquots/store');
    }


I only have to define the method once to use it throughout my application. Problem solved.
