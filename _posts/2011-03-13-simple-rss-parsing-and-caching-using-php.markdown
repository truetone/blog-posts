---
author: admin
comments: true
date: 2011-03-13 02:23:28+00:00
layout: post
slug: simple-rss-parsing-and-caching-using-php
title: Simple RSS Parsing and Caching Using PHP
wordpress_id: 481
categories:
- PHP
- rss
- web development
---

I feel like I should begin by stating that my college degree is in English Literature. In other words, I am not formally trained to be a programmer. Still I've spent many years working in PHP. It can be liberating to find out that something you thought would be complicated, is actually not that hard when broken down into discrete steps.

This whole adventure started for me when I went looking for a way to parse an RSS feed. Contrary to those who proclaim that [RSS is dead](http://www.google.com/search?sourceid=chrome&ie=UTF-8&q=rss+is+dead), at it's heart, RSS is XML. As such it's a useful method to access content. In my case, I wanted to parse my blog RSS feed as well as my most recent [Tweets](http://twitter.com/truetone). That was revelation number one.



> RSS is XML > XML has a structure that can be put into objects in PHP



To many of my friends and colleagues, this may seem incredibly simple. To me it was a revelation that opened up a new door. I've never tried to create an RSS parser before. Suddenly it was less daunting. (Aside: For me, simple truths often come as revelations. To know me is to know this.)
<!-- more -->


### Parsing the RSS Feed



It turns out that PHP 5 has some really handy tools for dealing with HTML and XML in the [DOMDocument](http://php.net/manual/en/class.domdocument.php) class.

First, we create an array to store the XML. Next instantiate `DOMDocument` and call the `load` function:

[php]$doc = new DOMDocument();
$doc->load($url);[/php]

Then it's as simple as looping through the XML nodes and storing what you want in the `$xml` array. For this use `getElementsByTagName`:

[php]foreach ($doc->getElementsByTagName('item') as $node)
{
    //do stuff
}[/php]

In my case I knew the most I wanted was a simple list with title, description, link and date. Thus:

[php]foreach ($doc->getElementsByTagName('item') as $node)
{
    $rss = array ( 
        'title' => $node->getElementsByTagName('title')->item(0)->nodeValue,
        'description' => $node->getElementsByTagName('description')->item(0)->nodeValue,
        'link' => $node->getElementsByTagName('link')->item(0)->nodeValue,
        'date' => $node->getElementsByTagName('pubDate')->item(0)->nodeValue
        );
    }
}[/php]

Now each loop loads the information I want into an array called `$rss`. Next just push that into the `$xml` array:

[php]foreach ($doc->getElementsByTagName('item') as $node)
{
    $rss = array ( 
        'title' => $node->getElementsByTagName('title')->item(0)->nodeValue,
        'description' => $node->getElementsByTagName('description')->item(0)->nodeValue,
        'link' => $node->getElementsByTagName('link')->item(0)->nodeValue,
        'date' => $node->getElementsByTagName('pubDate')->item(0)->nodeValue
        );
      array_push($xml, $rss);
    }
}[/php]

Finally I serialized the data to store it in a cache file. So we end up with:

[php]protected function getFeed($url)
{
    $xml = array();
    $doc = new DOMDocument();
    $doc->load($url);
    foreach ($doc->getElementsByTagName('item') as $node)
    {
      $rss = array ( 
        'title' => $node->getElementsByTagName('title')->item(0)->nodeValue,
        'description' => $node->getElementsByTagName('description')->item(0)->nodeValue,
        'link' => $node->getElementsByTagName('link')->item(0)->nodeValue,
        'date' => $node->getElementsByTagName('pubDate')->item(0)->nodeValue
        );
      array_push($xml, $rss);
    } //endforeach element ids
    return serialize($xml);
  }
}[/php]

So now we can deal with the RSS information. Next we just have to create a way to cache it so the feed isn't unnecessarily pulled in over and over. This is when another liberating revelation came my way. I began to look for methods of caching and I saw the following advice on a forum:



> Get the feed. Write it to a text file. For each new request, check the mod time of the text file. It enough time has passed, update the file.



There are probably more complex caching algorithms than this, but it seemed like a good place to start. So I wrote a caching function. It takes an array with two parameters. The name of the service as the array key and the url of the RSS feed. First we check to see if a cache file exists, and if it does, we check to see whether or not it has expired. I chose an arbitrary span of 60 seconds for my cache file:

[php]public function checkCache($data=array())
{
    foreach ($data as $service => $feed)
    {
      $path = '/tmp/' . $service . '.cache';
      if ((!file_exists($path) || time() - filemtime($path) > 60) && $cache = fopen($path, 'w+'))
      {
           // do stuff
      }
    }
}[/php]

So if there is no file, or the requisite time has expired and the file can be opened we call the aforementioned `getFeed` function to get the feed data, write it to the file and send it to the webpage:

[php]$rss_contents = $this->getFeed($feed);
fwrite($cache, $rss_contents);
fclose($cache);
return unserialize($rss_contents);[/php]

If the cache doesn't need to be updated, we simply read it and send the data that way:

[php]$cache = fopen($path, 'r');
return unserialize(file_get_contents($path)); // remember to unserialize since we serialized it initially
fclose($cache);[/php]

The whole function looks like this:

[php]public function checkCache($data=array())
{
  foreach ($data as $service => $feed)
  {
    $path = '/tmp/' . $service . '.cache';
    if ((!file_exists($path) || time() - filemtime($path) > 60) && $cache = fopen($path, 'w+'))
    {
      $rss_contents = $this->getFeed($feed);
      fwrite($cache, $rss_contents);
      fclose($cache);
      return unserialize($rss_contents);
    }
    else
    {
      $cache = fopen($path, 'r');
      return unserialize(file_get_contents($path));
      fclose($cache);
    }
  }
}[/php]

The entire class together looks like this:

[php]<?php
class RssParser
{
  public function checkCache($data=array())
  {
    foreach ($data as $service => $feed)
    {
      $path = '/tmp/' . $service . '.cache';
      if ((!file_exists($path) || time() - filemtime($path) > 60) && $cache = fopen($path, 'w+'))
      {
        $rss_contents = $this->getFeed($feed);
        fwrite($cache, $rss_contents);
        fclose($cache);
        return unserialize($rss_contents);
      }
      else
      {
        $cache = fopen($path, 'r');
        return unserialize(file_get_contents($path));
        fclose($cache);
      }
    }
  }
  
  protected function getFeed($url)
  {
    $xml = array();
    $doc = new DOMDocument();
    $doc->load($url);
    foreach ($doc->getElementsByTagName('item') as $node)
    {
      $rss = array ( 
        'title' => $node->getElementsByTagName('title')->item(0)->nodeValue,
        'description' => $node->getElementsByTagName('description')->item(0)->nodeValue,
        'link' => $node->getElementsByTagName('link')->item(0)->nodeValue,
        'date' => $node->getElementsByTagName('pubDate')->item(0)->nodeValue
        );
      array_push($xml, $rss);
    } //endforeach element ids
    return serialize($xml);
  }
}[/php]

Finally, we instantiate it in the page where we're going to use it and loop through it:

[php]<?

include_once('/path/to/rss_parser.class.php'); // include the php file with the class

$parser = new RssParser(); // instantiate the class
$blog_feed = $parser->checkCache(array('blog' => 'http://yourdomain.com/feed/')); // load the RSS
?>
<ul>
<?
foreach ($blog_feed as $key => $items)
{
    if ($key < 5): ?>
	<li><a href="<?= $items['link'] ?>"><?= $items['title'] ?></a></li>
    <?php
    endif;
} //endforeach
?>
</ul>[/php]

Done!



### Caveats



Depending on your server configuration, you may need to put the class in your public directory. If you need to do that, make sure you put it in a directory with '750' permissions.

Also, your PHP configuration may not allow you to open urls with `fopen`. In that case, I suggest you use the [cURL library](http://us2.php.net/manual/en/book.curl.php).

This is a very simple RSS parsing and caching engine, but it works and it's a good start to working with PHP and XML.
