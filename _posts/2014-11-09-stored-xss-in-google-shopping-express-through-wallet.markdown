---
layout: post
title:  "Disclosure: Stored XSS in Google Shopping Express"
date:   2014-11-09 00:43:08
categories: responsible-disclosure
permalink: post/stored-xss-in-google-shopping-express-through-wallet/
---

### Description

Found a Cross-site Scriping in Google Shopping Express Through It's Wallet data.

> Wikipedia: Google Shopping Express is a same-day shopping service ("shop local stores online and get items delivered on the same day") from Google that was launched on a free trial basis in San Francisco and Silicon Valley in spring 2013 and publicly in September that year. In spring 2014 it was expanded to New York and Los Angeles, and in fall 2014 to Chicago, Boston, and Washington, DC.

### Proof of Concept of Stored XSS:

* Go to the Google Shopping Express page [Google Shopping Express](https://www.google.com/shopping/express/ "Google Shopping Express")
* Click to "Deliver to", then "Manage delivery addresses"
* Add a new address through Google Wallet popup (this step is XSS filtered)
* Back to Google Shopping Express home and click again to "Deliver to"
* Edit the previously added address (this is needed to bypass the XSS filter applied in the fourth step)
* The vulnerability lives in the "City" input, so.. replace the city address with this XSS vector

		<img src=x onerror=prompt(1)>

* Save and back to Google Shopping Express home
* The payload was triggered
* (However you could add directly the vector in https://wallet.google.com ;)

<!--r34dm0r3-->

### Example demostration screen

**Google Shopping Express Stored Cross-site Scriping**

<a href="/images/security/responsible-disclosure/google-xss.png">![Google Shopping Express Stored XSS](/images/security/responsible-disclosure/google-xss.png)</a>

### Example demostration's video

<div class="photo_frame_center">
	<video width="480" height="360" controls>
		Sorry, your browser doesn't support embedded videos, 
		but don't worry, you can <a href="/video/security/responsible-disclosure/google-xss.ogv">Download It</a>
		and watch it with your favorite video player!
		<source src="/video/security/responsible-disclosure/google-xss.ogv" type='video/ogg; codecs="theora, vorbis"'>
	</video>
</div>

Watch in <a href="https://www.youtube.com/watch?v=oFeD74zwA00" class="lighter-red" title="Google Shopping Express XSS" target="_blank">YouTube</a>

### Disclosure:

* **09/11/2014** – Report to Google Security Team
* **10/11/2014** – Received a first feedback said that the report was triaged
* **10/11/2014** – Received a second feedback said that the vulnerability exists
* **11/11/2014** – Reply from Google Security Bot - The panel has decided to issue a reward of $5000
* **12/11/2014** – Public disclosure

### Acknowledgement

<a href="/images/security/responsible-disclosure/google-reward-mail.png">![Google Security Team - Reward](/images/security/responsible-disclosure/google-reward-mail.png)</a>

Thanks to Google Security Team for the [Google Hall Of Fame](http://www.google.com/about/appsecurity/hall-of-fame/reward/ "Google Hall Of Fame - Federico Fazzi").
