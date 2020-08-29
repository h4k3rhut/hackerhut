---
layout: post
title: Installation of METASPLOIT in Raspberry-pi 3/Zero with Raspbian
date: 2017-12-20 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: RaspberianOS-Metasploit.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Raspberry-pi, Metasploit]
---
We all  know the importance of Metasploit in a Hacker/Red team personal's life, if the metasploit is with a raspberry pi then it's like cherry on cake. The combination will be deadly as it is more mobile and easy to use.

So what's the problem???

The problem is the installation. So here is the solution.....

# Requirements

* Raspberry pi (3 or Zero )
* Micro SD card flashed with Raspbian OS [download raspbian](https://www.raspberrypi.org/downloads/raspbian/ )
* HDMI cable, key board and mouse (not require for headless setup)
* Internet connection(ethernet or wifi)
* Power supply to Raspberry pi

## Process

* Setup Raspberry pi(Zero or 3) components, boot up and connect to internet either with HDMI cable and keyboard & mouse Or headless( lot of tutorial available in youtube to setup headless).

* Go to terminal for metasploit set up(if you are using through headless then you are by default in Terminal)
* Update the Raspbian OS.

```
sudo apt-get update
```
* if you want then upgrade also.

```
sudo apt-get upgrade
```
* Then just fullfill the dependancies.

 ```
 sudo apt-get install build-essential libreadline-dev libssl-dev libpq5 libpq-dev libreadline5 libsqlite3-dev libpcap-dev subversion git-core autoconf postgresql pgadmin3 curl zlib1g-dev libxml2-dev libxslt1-dev libyaml-dev nmap
 ```
 * Enter the below command to add the build repository and install the Metasploit Framework package
 
 ```
 sudo curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall && chmod 755 msfinstall && ./msfinstall
 ```
 
 * It will take 15 mins(according to internet speed, so take a break). After the installation completes, open the terminal and type the below to start Metasploit console.
 
 ```
 ./msfconsole
 ```
 
 Or
 
 ```
 msfconsole
 ```
 
 * It will ask you to set up new database, Type y or yes to continue.
 
 
 * BOOM ... Now you setted up Metasploit completely & you are in msf console..
 
 * To check the database status type the below command in msf console.
 
 ```
 db_status
 ```
 
 * If everything gone perfect, you will see this:
 
``` [*] postgresql connected to msf ```

* ENJOY....
