---
layout: post
title:  "RapidTor – Timedelayed identity changer in TOR network"
date:   2013-10-02 08:50:04
categories: coding
permalink: post/rapidtor-timedelayed-identity-changer-in-tor-network/
---

### Description

With `RapidTor` you can change the identity in **TOR** network after how many seconds you wants, configure your torserver and `Vidalia` or `Polipo` with **ControlPort** support, after that use this Class to make login and change identity whenever you want.

### Configuration And Usage

    host = 'localhost'      # server tor host
    port = 9051             # need ControlPort enabled
    passwd = 'torpasswd'    # your tor server password
    delay = 5               # change my identity after 5 secs..
    enable_cache = 1        # 1=enable, 0=disable

{% highlight bash %}
usage: python rapidtor.py
{% endhighlight %}

### Sources

<span id="sources-list">
[View on GitHub](https://github.com/eurialo/rapidtor/ "GitHub RapidTor")
[Direct Download](https://raw.githubusercontent.com/eurialo/rapidtor/master/rapidtor.py "Download RapidTor")
</span>