---
layout: post
title:  "Disclosure: Yahoo! Finance Cross-site Scripting"
date:   2014-10-02 20:04:21
categories: responsible-disclosure
permalink: post/yahoo-finance-cross-site-scripting/
---

### Description

Found a `Stored Cross-site Scriping` in `Yahoo! Finance`.
(Tested on all sub-domains `*.yahoo.finance.com`).

> At Yahoo Finance, you get free stock quotes, up to date news, portfolio management resources, international market data, message boards, and mortgage rates that help you manage your financial life.

### Proof of Concept of Stored XSS:

* Go to [Yahoo! Finance](https://it.finance.yahoo.com/ "Yahoo! Finance")
* Create new portfolio and show It
* Click to `"Add/modify codes"`
* Generate the vector payload

		<img/src=1 onerror=alert(1)>

* Encode this vector through `URL Hexadecimal` bytes sequence

		%3c%69%6d%67%2f%73%72%63%3d%31%20%6f%6e%65%72%72%6f%72%3d%61%6c%65%72%74%28%31%29%3e

* Append the vector below to the inputs and click `"Add code"`
* Back to Portfolio Home
* Click to link `"Reorder"`
* Paylaod was triggered

#### Example of portfolio sort link:

https://it.finance.yahoo.com/portfolio/pf_**XX**/sort
where **XX** = `id of created portfolio`

### Example demostration screen

<a href="/images/security/responsible-disclosure/yahoo-xss.png">![Yahoo Stored XSS](/images/security/responsible-disclosure/yahoo-xss.png)</a>

### Disclosure:

* **28/08/2014** – Report to Yahoo! Security Team through [Hackerone.com](https://hackerone.com/, "Hackerone")
* **29/09/2014** – Received a response from Yahoo
* **01/10/2014** – Reply from Yahoo! Security Team that informs me that the bug was fixed and reward me with $600
* **07/10/2014** – Public disclosure

### Acknowledgement

Thanks Yahoo! Security Team for the add to [Wall Of Fame](https://hackerone.com/yahoo/thanks "Yahoo! Wall Of Fame - eurialo").
