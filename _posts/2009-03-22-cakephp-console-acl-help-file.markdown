---
author: admin
comments: true
date: 2009-03-22 15:30:08+00:00
layout: post
slug: cakephp-console-acl-help-file
title: CakePHP Console ACL Help File
wordpress_id: 95
categories:
- ACL
- CakePHP
- PHP
- web development
tags:
- CakePHP
- cli
---

Every now and then I want to view my help files in pretty, formatted HTML instead of plain text in a text editor or terminal window. Right now I'm working on setting up some Access Control Lists (ACL) in the [CakePHP Console](http://book.cakephp.org/view/108/the-cakephp-console). ACL is a powerful, yet sometimes hard-to-grasp concept. I always figure that if I want a resource like this, there has to be someone else out there who does, so for your reference and mine, here it is. (By the way, to get to this from the console, simply type `cake acl help`.)

Usage: `cake acl <command> <arg1> <arg2>...`
-----------------------------------------------
Commands:

`create aro|aco <parent> <node>`
Creates a new ACL object <node> under the parent specified by <parent>, an id/alias.
The <parent> and <node> references can be in one of the following formats:



	
  * - <model>.<id> - The node will be bound to a specific record of the given model

	
  * - <alias> - The node will be given a string alias (or path, in the case of <parent>),


i.e. 'John'.Â  When used with <parent>, this takes the form of an alias path,
i.e. <group>/<subgroup>/<parent>.
To add a node at the root level, enter 'root' or '/' as the <parent> parameter.

`delete aro|aco <node>`
Deletes the ACL object with the given <node> reference (see 'create' for info on node references).

`setParent aro|aco <node> <parent>`
Moves the ACL object specified by <node> beneath the parent ACL object specified by <parent>.
To identify the node and parent, use the row id.

`getPath aro|aco <node>`
Returns the path to the ACL object specified by <node>. This command is useful in determining the inhertiance of permissions for a certain object in the tree.
For more detailed parameter usage info, see help for the 'create' command.

`check <aro_id> <aco_id> [<aco_action>] or all`
Use this command to check ACL permissions.
For more detailed parameter usage info, see help for the 'create' command.

`grant <aro_id> <aco_id> [<aco_action>] or all`
Use this command to grant ACL permissions. Once executed, the ARO specified (and its children, if any) will have ALLOW access to the specified ACO action (and the ACO's children, if any). For more detailed parameter usage info, see help for the 'create' command.

`deny <aro_id> <aco_id> [<aco_action>]or all`
Use this command to deny ACL permissions. Once executed, the ARO specified (and its children, if any) will have DENY access to the specified ACO action (and the ACO's children, if any). For more detailed parameter usage info, see help for the 'create' command.

`inherit <aro_id> <aco_id> [<aco_action>]or all`
Use this command to force a child ARO object to inherit its permissions settings from its parent. For more detailed parameter usage info, see help for the 'create' command.

`view aro|aco [<node>]`
The view command will return the ARO or ACO tree. The optional id/alias parameter allows you to return only a portion of the requested tree. For more detailed parameter usage info, see help for the 'create' command.

`initdb`
Uses this command : `cake schema run create DbAcl`

`help [<command>]`
Displays this help message, or a message on a specific command.


### The 'create' help file


Usage: cake acl <command> <arg1> <arg2>...
-----------------------------------------------



	
  * Commands:

	
    * `create aro|aco <parent> <node>` ``

	
      * Creates a new ACL object `<node>` under the parent specified by `<parent>`, an id/alias. The `<parent> and <node>` references can be in one of the following formats:

	
        * - `<model>.<id>` - The node will be bound to a specific record of the given model

	
        * - `<alias>` - The node will be given a string alias (or path, in the case of `<parent>`), i.e. 'John'.Â  When used with `<parent>`, this takes the form of an alias path, i.e. `<group>/<subgroup>/<parent>`. To add a node at the root level, enter 'root' or '/' as the `<parent>` parameter.











