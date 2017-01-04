---
layout: 	post
published: 	true
title:  	"Setting up Memcached on my Raspberry Pi"
intro:  	"Memcached is an open source, high-performance, distributed memory object caching system. I intend to use it for speeding up my web applications running on a Raspberry Pi."
thumb:  	"/images/posts/memcached.png"
date:   	2012-05-08 12:56:27 +0100
categories:	[memcached, raspberry-pi]
---
This website is running on my [Raspberry Pi][raspberry-pi]{:target="_blank"} with a 700 MHz ARM processor and 256Mb memory, these are not very high specs therefore i'm using Memcached. Memcached is a distributed memory caching system that is often used to speed up dynamic (database-driven) websites by caching data and objects in RAM to reduce stress on the webserver. This article handles the installation and configuration of [Memcached][memcached]{:target="_blank"} on my Raspberry Pi running [Raspbian][raspbian]{:target="_blank"} (based on Debian Wheezy).

I am installing the software from packages, [documentation available at Google Code][memcached-docs]{:target="_blank"}, with apt-get.

{% highlight sh %}
apt-get install memcached
{% endhighlight %}

After the installation has completed you can see the stats with the following command:

{% highlight bash %}
echo "stats settings" | nc localhost 11211
{% endhighlight %}

This will give you a list with the following stats:

{% highlight bash %}
STAT maxbytes 67108864
STAT maxconns 1024
STAT tcpport 11211
STAT udpport 11211
STAT inter 127.0.0.1
STAT verbosity 0
STAT oldest 0
STAT evictions on
STAT domain_socket NULL
STAT umask 700
STAT growth_factor 1.25
STAT chunk_size 48
STAT num_threads 4
STAT num_threads_per_udp 4
STAT stat_key_prefix :
STAT detail_enabled no
STAT reqs_per_event 20
STAT cas_enabled yes
STAT tcp_backlog 1024
STAT binding_protocol auto-negotiate
STAT auth_enabled_sasl no
STAT item_size_max 1048576
STAT maxconns_fast no
STAT hashpower_init 0
STAT slab_reassign no
STAT slab_automove no
END
{% endhighlight %}

This shows that the Memcached is now listening on port 11211 with localhost connections only. We will change this to the, catch-all, IP 0.0.0.0 by changing the line: "-l 127.0.0.1" to "-l 0.0.0.0" in the file "/etc/memcached.conf". After changing the config you can see if we can now make a connection from external machines use the following command:

{% highlight bash %}
netstat -ln4t | grep :11211
{% endhighlight %}

[memcached]: http://memcached.org/
[memcached-docs]: http://code.google.com/p/memcached/wiki/NewInstallFromPackage
[raspbian]: http://www.raspbian.org/
[raspberry-pi]: http://www.raspberrypi.org/