---
layout: 	post
published: 	true
title:  	"Saving application state in AS3 AIR Mobile"
intro:  	"Storing your current state objects dynamically in flash.net.SharedIObject and reloading your application-state when initializing your application."
thumb:  	"/images/posts/air-application-save-state-in-sharedobject.jpg"
date:   	2013-05-30 00:00:00 +0100
categories:	[as3, away3d, starling, adobe air]
---
The class below can be used for storing and retrieving object from a [SharedObject][sharedobject]{:target="_blank"}. 
<br/>Fictive usage example code:

{% highlight as3 %}
// Creating object
var objectToStore:YourClass = new YourClass();
objectToStore.property = "value";

// Store it
Store.Set("key", objectToStore);

// And retrieving it again.
var objectFromStore:YourClass = Store.Get("key") as YourClass;

// Get proof...
trace(objectFromStore.property); // Should output "trace"
{% endhighlight %}

The class used for storing and retrieving your objects dynamically

{% highlight as3 %}
package Memory 
{
    import flash.net.registerClassAlias;
    import flash.net.SharedObject;
    import flash.utils.getDefinitionByName;
    import flash.utils.getQualifiedClassName;

    public class Store 
    {
        private static var sharedObject:SharedObject = SharedObject.getLocal("MemoryGame");
        
        public static function Set(key:String, value:Object):void
        {
            var classAlias:String = getQualifiedClassName(value);
            var classObject:Class = Class(getDefinitionByName(getQualifiedClassName(value)));
            registerClassAlias(classAlias, classObject); 
            
            sharedObject.data[key] = value;
            sharedObject.flush();
        }
        
        public static function Get(key:String):*
        {
            var value:Object = sharedObject.data[key];
            var classAlias:String = getQualifiedClassName(value);
            var classObject:Class = Class(getDefinitionByName(getQualifiedClassName(value)));
            registerClassAlias(classAlias, classObject); 
            
            return value as classObject;
        }
        
        public static function Remove(key:String):void
        {
            delete sharedObject.data[key];
            sharedObject.flush();
        }
        
        public static function Clear():void
        {
            sharedObject.clear();
        }
    }
}
{% endhighlight %}

[sharedobject]: http://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/SharedObject.html