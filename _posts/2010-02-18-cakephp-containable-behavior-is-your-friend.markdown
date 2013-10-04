---
author: admin
comments: true
date: 2010-02-18 16:21:04+00:00
layout: post
slug: cakephp-containable-behavior-is-your-friend
title: 'CakePHP: Containable Behavior is Your Friend'
wordpress_id: 369
categories:
- CakePHP
- containable behavior
- PHP
- web development
tags:
- behaviors
- CakePHP
- containable
- optimization
- PHP
- SQL
---

When it comes to optimizing your CakePHP queries, you need to abandon Recursive and adopt Containable.

In the example below I have the following models:



	
  * Patient

	
  * Specimen

	
  * Result

	
  * ResultType


The associations in the model are:

	
  * Result

	
    * belongsTo

	
      * ResultType

	
        * hasMany

	
          * Result







	
      * Patient

	
        * hasMany

	
          * Result

	
          * Specimen







	
      * Specimen

	
        * belongsTo

	
          * Patient




	
        * hasMany

	
          * Result














<!-- more -->


### $paginate in the Result Controller




#### Original version


[php highlight="12"]var $paginate = array(
		'fields' => array(
			'ResultType.type',
			'Specimen.draw_date',
			'Result.id',
			'Result.patient_id',
			'Result.specimen_id',
			'Result.result',
			'Result.created',
			'Result.modified'
			),
		'recursive' => 0,
		'limit' => 50);[/php]


#### The Same Thing Using Containable


[php highlight="11,12,13,14,15,16,17,18,19,20,21,22,23"]var $paginate = array(
		'fields' => array(
			'id',
			'patient_id',
			'specimen_id',
			'result',
			'created',
			'modified'
			),
		'limit' => 50,
		'contain' => array(
			'ResultType' => array(
				'fields' => array(
					'ResultType.type',
					'ResultType.id'
					)
				),
			'Specimen' => array(
				'fields' => array(
					'Specimen.id',
					'Specimen.draw_date'
					)
				)
			)
		);[/php]


### The SQL




#### SQL Generated from the Original $paginate var


[sql highlight="7,8,19,20"]SELECT COUNT(*) AS `count`
FROM `results` AS `Result`
LEFT JOIN `result_types` AS `ResultType`
ON (`Result`.`result_type_id` = `ResultType`.`id`)
LEFT JOIN `specimens` AS `Specimen`
ON (`Result`.`specimen_id` = `Specimen`.`id`)
LEFT JOIN `patients` AS `Patient`
ON (`Result`.`patient_id` = `Patient`.`id`)
WHERE 1 = 1

/* 1879 milliseconds */

SELECT `ResultType`.`type`, `Specimen`.`draw_date`, `Result`.`id`, `Result`.`patient_id`, `Result`.`specimen_id`, `Result`.`result`, `Result`.`created`, `Result`.`modified`
FROM `results` AS `Result`
LEFT JOIN `result_types` AS `ResultType`
ON (`Result`.`result_type_id` = `ResultType`.`id`)
LEFT JOIN `specimens` AS `Specimen`
ON (`Result`.`specimen_id` = `Specimen`.`id`)
LEFT JOIN `patients` AS `Patient`
ON (`Result`.`patient_id` = `Patient`.`id`)
WHERE 1 = 1
ORDER BY `Result`.`created` desc
LIMIT 50

/* 2106 milliseconds */[/sql]


#### SQL Generated Using Containable Behavior


[sql]SELECT COUNT(*) AS `count`
FROM `results` AS `Result`
LEFT JOIN `result_types` AS `ResultType`
ON (`Result`.`result_type_id` = `ResultType`.`id`)
LEFT JOIN `specimens` AS `Specimen`
ON (`Result`.`specimen_id` = `Specimen`.`id`)
WHERE 1 = 1

/* 10 milliseconds */

SELECT `Result`.`id`, `Result`.`patient_id`, `Result`.`specimen_id`, `Result`.`result`, `Result`.`created`, `Result`.`modified`, `ResultType`.`type`, `ResultType`.`id`, `Specimen`.`id`, `Specimen`.`draw_date`
FROM `results` AS `Result`
LEFT JOIN `result_types` AS `ResultType`
ON (`Result`.`result_type_id` = `ResultType`.`id`)
LEFT JOIN `specimens` AS `Specimen`
ON (`Result`.`specimen_id` = `Specimen`.`id`)
WHERE 1 = 1
ORDER BY `Result`.`created` desc
LIMIT 50

/* 19 milliseconds */[/sql]


### The Difference


The first set of queries took nearly 4 seconds. The second: 29 milliseconds. Containable just gives you so much more control over what's selected in your query. UsingÂ `recursive => 0` still joined the patients table both times because it was associated in the model--even though in this case we didn't need it. Using the Containable Behavior in the second example removed the patients table from the queries altogether.

This is one of the key pitfalls of using a framework like CakePHP; You can get things running quickly, but you have to go back and optimize. Otherwise you can build a heavy load on the server.


### Resources





	
  * [CakePHP](http://cakephp.org)

	
  * [The Containable Behavior](http://book.cakephp.org/view/474/Containable)

	
  * [The Recursive Model Attribute](http://book.cakephp.org/view/439/recursive)


