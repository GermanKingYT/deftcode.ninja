---
layout: page
title: "README"
permalink: readme/
---

deftcode.ninja
==============

Personal website Jekyll based template.

Start using template
--------------------

To start using the template you can serve It locally or with apache2, with Jekyll you can do It with:

	deftcode ~ $ jekyll serve --detach

Or with apache2 you must build the jekyll project: 

	deftcode ~ $ jekyll build
	Configuration file: /var/www/deftcode/_config.yml
	Source: /var/www/deftcode
	Destination: /var/www/deftcode/_site
	Generating... 
	done.

Then configure the apache2 virtualhost following the example below:

    deftcode ~ $ cat /etc/apache2/site-availables/000-default.conf
    # Example virtualhost of jekyll builds
	<VirtualHost *:80>
		ServerName deftcode.ninja
		DocumentRoot /var/www/deftcode/_site
	</VirtualHost>

Links
-----

* DEFTCODE: http://deftcode.ninja
