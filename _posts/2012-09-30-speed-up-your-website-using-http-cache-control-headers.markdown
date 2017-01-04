---
layout: 	post
published: 	true
title:  	"Speed up your website using HTTP Cache-Control headers"
intro:  	"Besides using server side memory caching of objects to reduce the stress on my Raspberry pi i also use HTTP caching of my webpages. This article contains a simple example."
thumb:  	"/images/posts/304-not-modified.png"
date:   	2012-09-30 00:00:00 +0100
categories:	[cache, headers]
---
Besides using [server side memory caching][memcached] of objects to reduce the stress on my Raspberry pi i also use HTTP caching of my webpages.

The class below can be used for HTTP Caching. It has a static function called 'Init' that needs 2 parameters, a timestamp of the date that the page (or any other file requested by the browser) was last modified and the maximum age, in seconds, that this page can be held in cache by the browser.

{% highlight php %}
<?php
class HttpCache 
{
    public static function Init($lastModifiedTimestamp, $maxAge)
    {
        if (self::IsModifiedSince($lastModifiedTimestamp))
        {
            self::SetLastModifiedHeader($lastModifiedTimestamp, $maxAge);
        }
        else 
        {
            self::SetNotModifiedHeader($maxAge);
        }
    }
    
    private static function IsModifiedSince($lastModifiedTimestamp)
    {
        $allHeaders = getallheaders();
        
        if (array_key_exists("If-Modified-Since", $allHeaders))
        {
            $gmtSinceDate = $allHeaders["If-Modified-Since"];
            $sinceTimestamp = strtotime($gmtSinceDate);
            
            // Can the browser get it from the cache?
            if ($sinceTimestamp != false && $lastModifiedTimestamp <= $sinceTimestamp)
            {
                return false;
            }
        }
        
        return true;
    }
    
    private static function SetNotModifiedHeader($maxAge)
    {
        // Set headers
        header("HTTP/1.1 304 Not Modified", true);
        header("Cache-Control: public, max-age=$maxAge", true);
        die();
    }
    
    private static function SetLastModifiedHeader($lastModifiedTimestamp, $maxAge)
    {
        // Fetching the last modified time of the XML file
        $date = gmdate("D, j M Y H:i:s", $lastModifiedTimestamp)." GMT";
        
        // Set headers
        header("HTTP/1.1 200 OK", true);
        header("Cache-Control: public, max-age=$maxAge", true);
        header("Last-Modified: $date", true);
    }
}
{% endhighlight %}

[memcached]: /setting-up-memcached-on-my-raspberry-pi