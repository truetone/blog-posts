---
author: admin
comments: true
date: 2010-05-24 21:27:51+00:00
layout: post
slug: an-unexpected-problem-with-cakephp-and-email-elements
title: An Unexpected Problem with CakePHP and Email Elements
wordpress_id: 434
categories:
- CakePHP
- email elements
- PHP
tags:
- CakePHP
- email elements
- PHP
---

For several months now I've been triggering functions in my [CakePHP](http://cakephp.org) controllers [using crontabs](http://www.lost-in-code.com/programming/php-code/cakephp-crontab/). It's especially handy for summarizing data and sending out reports via email. I'm about to change jobs and I'm trying to set up as many systems as I can to help staff manage our data after I leave. Part of that means writing a few more crons to send out more emails. Today while trying to do just that, I ran into something unexpected that held me up for an hour or so until I had an epiphany on my way home. For the purposes of this post, I'm assuming you've already set up a cron dispatcher and know how to trigger cron jobs.

For one more week I'm working in a research clinic. One of the things we need to keep track of is who is late in getting us a sample. We need to check for blood and throat samples (which come from swishing some saline around in the mouth). This can be done by hand, but soon the study will grow and the number of participants will make that hard to manage. So I just want to check to see who is late and send out an email to staff to let them know.

This function exists in my Patient controller:<!-- more -->

[php highlight="50,51,52,53"]
function cron_delinquency() {

	if (!defined('CRON_DISPATCHER')) // make sure the request comes through the cron dispatcher
	{
		$this->redirect('/'); exit('Invalid Request');
	}
	/* this looks up active patients who do not have an patient_id ending in "D". "D" indicates they are a donor and we only need one specimen from them. */
	$active = $this->Patient->find('list', array(
		'conditions' => array(
			'Patient.id LIKE \'T%\' AND Patient.id NOT LIKE \'%D\'',
			'Patient.withdrawn != \'y\'',
			'Patient.active="1"'),
		));
	$in = '\''; /* the patient_id's start with a "T" meaning all the patient_id's need to be enclosed in quotes */

	$in .= implode('\', \'', $active); // implode the list of patient_id's

	$in = $in . '\''; // end it all with a quote

	$blds = $this->Patient->Specimen->find('list', array( // find the blood specimens for this group of patients
		'conditions' => array(
			'Specimen.patient_id IN (' . $in .')',
			'Specimen.type' => array('BLD')
			),
		'fields' => array('patient_id', 'draw_date'),
		'order' => array('patient_id' => 'ASC', 'draw_date' => 'ASC')

		));

	$thrs = $this->Patient->Specimen->find('list', array( // find the throat samples for this group of patients
		'conditions' => array(
			'Specimen.patient_id IN (' . $in .')',
			'Specimen.type' => array('THR')
			),
		'fields' => array('patient_id', 'draw_date'),
		'order' => array('patient_id' => 'ASC', 'draw_date' => 'ASC')

		));

/* My Patient model has a function to filter arrays and return only those that are older than the proved Unix timestamp. */
	$delinquentBlood = $this->Patient->find_delinquent($blds, 2419200); // 2419200 = 4 weeks; 3628800 = 6 weeks
	$delinquentThroat = $this->Patient->find_delinquent($thrs, 3628800);

	if(count($delinquentBlood) > 0 || count($delinquentThroat) > 0) // if we find any who are delinquent
	{

		asort($delinquentBlood); // sort them
		asort($delinquentThroat);

		$data['delinquentBlood'] = $delinquentBlood;
		$data['delinquentThroat'] = $delinquentThroat;
		$data['bloodCounter'] = count($delinquentBlood);
		$data['throatCounter'] = count($delinquentThroat);

		$this->set('data', $data);

		$this->Email->to 	  = $to;
		$this->Email->from		= 'LCIS <xxxxxxx@umn.edu>';
		$this->Email->subject	= 'PPG Delinquency Report: ' . $bloodCounter ." Subjects With Blood Specimens Due; " . $throatCounter . " With Throat Specimens Due.";
		$this->Email->sendAs	= 'html';
		$this->Email->template	= 'viptm_delinquency';
		$this->Email->send();
	}
}
[/php]

It's that highlighted bit that was really giving me trouble. Previously I had been setting those variables like so:

[php]$this->set(compact('delinquentBlood', 'delinquentThroat', 'bloodCounter', 'throatCounter'));[/php]

Ordinarily this would work with any other view, but the email element I have set up for this function was acting as if they variables weren't set at all. _It wasn't until I put them in an array called `$data`, that I could use them in my email element_. It was puzzling and it took me about an hour to figure that out, but once I did my email reports came with beautiful data.
