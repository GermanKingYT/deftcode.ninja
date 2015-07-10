---
layout: post
title:  "Verbind – Discover fastly a remote bind version"
date:   2015-05-24 16:05:00
categories: security coding
permalink: post/verbind-discover-fastly-a-remote-bind-version/
---

### Description

**Verbind** is a `case-study tool` to retrieve the `version` of remote **bind** service by executing a simple `dns query` request by following the **rfc** standard.

### Howto

{% highlight bash %}
deftcode ~ $ ruby verbind.rb deftcode.local
> Requesting for version.bind to address: deftcode.local
+ Bind version found: 9.8.4-rpz2+rl005.12-P1
{% endhighlight %}

### References

* RFC-1035: <a href="http://tools.ietf.org/html/rfc1035/" title="RFC-1035" target="_blank">http://tools.ietf.org/html/rfc1035/</a>
* DNS Protocol: <a href="http://www.networksorcery.com/enp/protocol/dns.htm" title="DNS Protocol" target="_blank">http://www.networksorcery.com/enp/protocol/dns.htm</a>

### Source

<span id="sources-list">
[View on GitHub](https://github.com/eurialo/verbind/ "Verbind GitHub")
</span>
