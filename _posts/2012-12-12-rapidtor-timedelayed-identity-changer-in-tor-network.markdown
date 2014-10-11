---
layout: post
title:  "RapidTor – Timedelayed identity changer in TOR network"
date:   2013-10-02 08:50:04
categories: coding
permalink: post/rapidtor-timedelayed-identity-changer-in-tor-network/
---

### Description

With `RapidTor` you can change the identity in **Tor** network after how many seconds you wants, configure your torserver and `vidalia` or `polipo` with **ControlPort** support, after that use this class to login and change identity when you want.

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
[Direct Download](https://raw.githubusercontent.com/eurialo/rapidtor/master/rapidtor.c "Download RapidTor")
</span>