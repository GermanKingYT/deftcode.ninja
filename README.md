deftcode.ninja
==============

Personal website Jekyll based template.

Start using template
--------------------

To start using the template you can serve It locally or with apache2, with **Jekyll** you can do It with:

	deftcode ~ $ jekyll serve --detach

Or with apache2 you must build the jekyll project: 

	deftcode ~ $ jekyll build -s /var/www/deftcode -d /var/www/deftcode/_site
	Configuration file: /var/www/deftcode/_config.yml
	Source: /var/www/deftcode
	Destination: /var/www/deftcode/_site
	Generating... 
	done.

Then configure the **apache2** virtualhost following the example below:

    deftcode ~ $ cat /etc/apache2/site-availables/000-default.conf
    # Example virtualhost of jekyll builds
	<VirtualHost *:80>
		ServerName deftcode.ninja
		DocumentRoot /var/www/deftcode/_site
	</VirtualHost>

Development
-----------

First prepare the environment running:

    deftcode ~ $ bundle install
    Fetching gem metadata from https://rubygems.org/..........
    Fetching version metadata from https://rubygems.org/...
    Fetching dependency metadata from https://rubygems.org/..
    ...
    Using jekyll-watch 1.2.1
    Using jekyll 2.5.3
    Using jekyll-assets 0.13.0
    Bundle complete! 3 Gemfile dependencies, 44 gems now installed.
    Use `bundle show [gemname]` to see where a bundled gem is installed.

After make the changes run the following **bundle** command to *build* the static site to *_site* directory.

    deftcode ~ $ bundle exec jekyll build

**NOTE**: Using directly the *jekyll build* command could trigger an **LoadError**, so use *bundle exec* instead!

Continue to **Start using template**..

Important
---------
Don't forget to remove the Google Analytics script from **_includes/head.html**!

Links
-----

* DEFTCODE: http://deftcode.ninja
