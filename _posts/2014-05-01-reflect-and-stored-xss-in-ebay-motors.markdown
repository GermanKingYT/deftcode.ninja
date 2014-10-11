---
layout: post
title:  "Disclosure: Reflect and Stored XSS in eBay Motors"
date:   2014-05-01 09:20:01
categories: responsible-disclosure
permalink: post/reflect-and-stored-xss-in-ebay-motors/
---

### Description

During my research I've found a Multiple Cross-site Scriping in eBay Motors.

> eBay Motors is a specialty site on eBay that gives you the research, selection, and security to confidently purchase vehicles and parts from across the street or across the country.

### Proof of Concept of Stored XSS:

* First go to eBay Motors Garage page [eBay Motors](http://www.ebay.com/motors/garage/, "eBay Motors") and go to `My Vehicles`
* Then click to `Add new Vehicle`
* Insert this vector into `Add tags to your vehicle (optional)` input:

		\"onclick="alert(666)

* Click "Save Changes"
* Back to garage page then click to your vehicle to see the triggered payload

### Proof of Concept of Reflect XSS:

* Go to eBay Motors page at [eBay Motors - Parts Accessories](http://www.ebay.com/motors/Parts-Accessories/, "eBay Motors - Parts Accessories")
* Search for a Accessories
* Add this vector to `GET` URI parameter **&_sasl=[vector]**

		\"%20onclick="javascript:prompt(666);//"

* Final URL example:

		http://www.ebay.com/sch/Car-Truck-Parts-/6030/i.html?_nkw=2007%20BMW%20&_trksid=p2059388.m2833&_sasl=\"%20onclick="javascript:prompt(666);//

* Now you see the arbitrary code was executed

### Example demostration screen

**eBay Stored Cross-site Scriping**

<a href="/images/security/responsible-disclosure/ebay-xss-2.png">![eBay Stored XSS](/images/security/responsible-disclosure/ebay-xss-2.png)</a>

**eBay Reflect Cross-site Scriping**

<a href="/images/security/responsible-disclosure/ebay-xss.png">![eBay Reflect XSS](/images/security/responsible-disclosure/ebay-xss.png)</a>

### Disclosure:

* **28/04/2014** – First report to eBay Security Team about Stored Cross-site Scripting
* **02/05/2014** – Received a response from eBay
* **03/05/2014** – Second report to eBay Security Team about Reflect Cross-site Scripting
* **05/05/2014** – Received a response from eBay
* **12/07/2014** – Reply from eBay Security Team that informs me that the first bug was fixed
* **14/07/2014** – Reply from eBay Security Team that informs me that the second bug was fixed
* **20/07/2014** – Public disclosure

### Acknowledgement

Thanks eBay Security Team for the [Acknowledgement](http://ebay.com/securitycenter/ResearchersAcknowledgement.html, "eBay Acknowledgement - Federico Fazzi").
