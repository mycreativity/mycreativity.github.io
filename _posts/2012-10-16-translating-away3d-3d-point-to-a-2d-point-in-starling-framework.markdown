---
layout: 	post
published: 	true
title:  	"Translating Away3D 3D point to a 2D point in Starling framework"
intro:  	"For an iOS game i am building with the Adobe Air SDK, using Away3D and Starling frameworks, i want to have interaction between the 3D and 2D objects. This is a small demo that shows the interaction between the frameworks. The demo is available as download."
thumb:  	"/images/posts/away3d-point-to-2d-starling-point.jpg"
date:   	2012-10-16 00:00:00 +0100
categories:	[as3, away3d, starling, adobe air]
---
<object classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000" width="640" height="280" id="demo" align="middle">
    <param name="movie" value="/files/DemoAway3DWithStarling.swf">
    <param name="menu" value="false">
    <param name="scale" value="noScale">
    <param name="allowFullscreen" value="true">
    <param name="allowScriptAccess" value="always">
    <param name="bgcolor" value="">
    <param name="wmode" value="direct">
    <!--[if !IE]>-->
    <object type="application/x-shockwave-flash" data="/files/DemoAway3DWithStarling.swf" width="640" height="280">
        <param name="movie" value="/files/DemoAway3DWithStarling.swf">
        <param name="menu" value="false">
        <param name="scale" value="noScale">
        <param name="allowFullscreen" value="true">
        <param name="allowScriptAccess" value="always">
        <param name="bgcolor" value=""> 
        <param name="wmode" value="direct">
    <!--<![endif]-->
        <a href="/web/20140113143631/http://www.adobe.com/go/getflash">
            <img src="/web/20140113143631im_/http://www.adobe.com/images/shared/download_buttons/get_flash_player.gif" alt="Get Adobe Flash player">
        </a>
    <!--[if !IE]>-->
    </object>
    <!--<![endif]-->
</object>
The example above (you can rotate the cube by dragging your mouse) consist of 3 layers, a Starling background instance with a particle instance, an Away3D viewport with the rotating cube and a foreground Starling layer that has a line 'attached' to a segment of the Away3D cube.

Starling translates the updated 3D point from Away3D every frame through a static function called "[GetVerticeWorldPosition][verticeposition]{:target="_blank"}". That function returns the Vector3D of the segment requested on the Mesh. The Vector3D x and y properties can then be used in a 2D point.

The example used on this page is build in Flashdevelop and can be downloaded below.

<ul class="downloads">
    <li>
        <a href="/files/translating-away3d-3d-point-to-a-2d-point-in-starling-framework.zip" target="_blank">away3d-point-to-a-starling-2d-point.zip [132.68 KB]</a>
    </li>
</ul>

[verticeposition]: http://away3d.com/forum/viewthread/1447