---
layout: post
title: i3 with Xubuntu 14 04
date: 2017-05-25 22:13:45
categories: linux ubuntu
---

I went back to Ubuntu 14.04 after having some trouble installing old AMD propietary
drivers on my machine. This comes as no surprise to anyone who has dealt with these
old drivers, which support Xorg only up to version 1.17. thus making it quite a 
mess to make compatible with Arch and newer distributions like Ubuntu 16.xx.

Anyway. I of course wanted my i3 system back in place the way it was before.
Unfortunatelly, it is not so easy with a distribution that comes bundled with a 
DM as Xubuntu is as it was with Arch. Nevertheless, it is far from impossible.

It is worth mentioning that this is mostly based on [this guide](http://feeblenerd.blogspot.com.ar/2015/11/pretty-i3-with-xfce.html) 
although it was simplified, assumes you are confortable building or already have an i3 config and you don't need a
separate user for doing all this. If you're newer to i3 or Linux, you may want to follow that guide.


1. Get i3.
2. Make extra sure your xfce panel is not set up in 'Deskbar' mode. This will
   break everything for unkown reasons.
3. Install i3.
```
sudo apt-get install i3
```
4. If you want to continue using the xfce4 panel, you *have to* install the i3 workspaces
plugin to be able to change workspaces.
```
sudo add-apt-repository ppa:aacebedo/libi3ipc-glib
sudo add-apt-repository ppa:aacebedo/xfce4-i3-workspaces-plugin
sudo apt-get update
sudo apt-get install xfce4-i3-workspaces-plugin libi3ipc-glib
````
5. Go to "Session and Startup" on the xfce4 settings. Go to the Session tab. You should note
"xfwm4" and "xfdesktop" processes running. Change their "Restart Style" to "Never". Click "Save Session".
6. Go to "Application Autostart" tab and add an application which command must be "i3", everything else up to you.
7. Go to the "Keyboard" dialog on the xfce4 settings, "Application Shorcuts" tab, and remove everything. Nothing will
clash with your i3 shorcuts now :)
8. Log out and log in. Be happy.
9. Optional tip: when adding the i3-workspaces-plugin to your panel, you can actually change the color of the numbers. 
Right click on the panel, then "Panel"->"Panel Preferences", then "Items" tab and then doublec click on hte "i3
Workspaces Plugin" entry.


