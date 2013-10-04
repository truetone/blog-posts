---
author: admin
comments: true
date: 2008-11-26 03:38:06+00:00
layout: post
slug: wordpress-auto-update-is-ok-but-the-command-line-is-faster
title: Wordpress' Auto Update Is OK, But The Command Line Is Faster
wordpress_id: 56
categories:
- web development
- wordpress
tags:
- cli
- tutorial
- wordpress
---

I recently found a great article about [upgrading Wordpress from the command line](http://www.cyberciti.biz/tips/howto-upgrade-wordpress-from-linux-unix-shell-prompt.html). If you're familiar with a command line interface at all, it's by far the simplest way to upgrade your Wordpress install.

You can apply the same method to upgrading your Wordpress plugins.



	
  1. Log in to your web server and `cd` to the Wordpress plugins directory:`
cd httpdocs/wp-content/plugins`
Your syntax may vary depending on your server.

	
  2. Download the new version of the plugin. In my case I'm upgrading the [Social Homes plug in](http://http://wordpress.org/extend/plugins/social-homes/).
`wget http://downloads.wordpress.org/plugin/social-homes.2.3.zip`

	
  3. Back up your current plugin directory
`tar -zcvf social-homes.tar.gz social-homes`

	
  4. Unzip the zip file of the new version
`unzip social-homes.2.3.zip`

	
    * You'll be prompted to confirm you want to overwrite the files in the social-homes directory
`replace social-homes/COPYING.txt? [y]es, [n]o, [A]ll, [N]one, [r]ename:`

	
    * Type 'A' and hit return to overwrite the old files with the new ones.




	
  5. Log into Wordpress to make sure the upgrade worked by going to the "Plugins" panel in the admin area.

	
  6. Clean up your mess
`rm social-homes.2.3.zip
rm social-homes.tar.gz`


You're done. You've successfully upgraded your plugin. This process can be much faster than downloading the plugin to your local directory, deactivating it in Wordpress and uploading the new one. Especially if the plugin is a large one.
