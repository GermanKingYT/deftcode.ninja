---
layout: post
title:  "Prestashop 1.6.0.6 - DOM based Cross-site Scripting"
date:   2014-06-10 12:32:18
categories: security
permalink: post/prestashop-dom-based-xss/
---

The version 1.6.0.6 of Prestashop is vulnerable to `DOM Based XSS`, the page location at
`/index.php?controller=stores` show you the locations of the stores, this feature can be enabled from the admin panel by `Preferences / Store Contacts`.

### Vulnerable function is stored in the Core JS cached version (see stores.js)

`snippet:`

{% highlight js %}
function searchLocations()
{
  $('#stores_loader').show();
  var address = document.getElementById('addressInput').value;
  var geocoder = new google.maps.Geocoder();
  geocoder.geocode({address: address}, function(results, status) {
    if (status === google.maps.GeocoderStatus.OK)
      searchLocationsNear(results[0].geometry.location);
    else
    {
      if (!!$.prototype.fancybox)
        $.fancybox.open([
        {
          type: 'inline',
          autoScale: true,
          minHeight: 30,
          content: '<p class="fancybox-error">' + address + ' ' + translation_6 + '</p>'
        }
        ], {
          padding: 0
        });
      else
        alert(address + ' ' + translation_6);
    }
    $('#stores_loader').hide();
  });
}
{% endhighlight %}

The variable `address` is not properly sanitized, therefore a **Cross-site Scripting** can be executed by injecting a simple vector like that:

{% highlight js %}
<input value=alert(1) autofocus>
{% endhighlight %}

### Example demostration screen in Prestashop online Demo

<a href="/images/security/responsible-disclosure/prestashop-xss.png">![Prestashop Demo XSS](/images/security/responsible-disclosure/prestashop-xss.png)</a>

### Disclosure:

* **08/06/2014** – Report to Prestashop Bugtraq
* **09/06/2014** – Fixed by commit [29d8cf1576cadd321d131f33735c4635759c10f5][commit-id]
* **10/06/2014** – Public disclosure

[commit-id]: https://github.com/PrestaShop/PrestaShop/commit/29d8cf1576cadd321d131f33735c4635759c10f5 "GitHub Commit-ID"