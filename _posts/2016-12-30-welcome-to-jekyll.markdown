---
layout: 	post
published: 	true
title:  	"Setting up Memcached on my Raspberry Pi"
intro:  	"Memcached is an open source, high-performance, distributed memory object caching system. I intend to use it for speeding up my web applications running on a Raspberry Pi."
thumb:  	"/images/posts/memcached.png"
date:   	2012-05-08 12:56:27 +0100
categories:	[memcached, raspberry-pi]
---
This website is running on my [Raspberry Pi][raspberry-pi] with a 700 MHz ARM processor and 256Mb memory, these are not very high specs therefore i'm using Memcached. Memcached is a distributed memory caching system that is often used to speed up dynamic (database-driven) websites by caching data and objects in RAM to reduce stress on the webserver. This article handles the installation and configuration of [Memcached][memcached] on my Raspberry Pi running [Raspbian][raspbian] (based on Debian Wheezy).

I am installing the software from packages, [documentation available at Google Code][memcached-docs], with apt-get.

{% highlight shell %}
$> apt-get install memcached
{% endhighlight %}

[memcached]: http://memcached.org/
[memcached-docs]: http://code.google.com/p/memcached/wiki/NewInstallFromPackage
[raspbian]: http://www.raspbian.org/
[raspberry-pi]: http://www.raspberrypi.org/