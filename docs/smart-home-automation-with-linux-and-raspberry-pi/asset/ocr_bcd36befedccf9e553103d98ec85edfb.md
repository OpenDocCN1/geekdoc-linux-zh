Generally, the installation of these modules will also correctly configure them so that .php files are associated with the execution of the PHP module. If this is not apparent, you can enable the module with this:

```
a2enmod php5
```

In the very unlikely event of these not working, a log is kept in /var/log/apache2/error.log. A lot of important traffic relies on a working web server, so it is worth the time to ensure it’s stable.

# Virtual Sites

It is possible for one web server to serve web pages for more than one site, even if they are on the same IP address. This has been available since version 1.1 of the HTTP protocol (supported by all main browsers), which included the domain name into the request, as well as the IP address. In the home environment it’s quite uncommon, but it is useful because it allows you to split the incoming web traffic into two parts to divert the curious. You can have one site for general access by friends and family, containing a blog with photographs of your dog and children, and a second for HA control. You can begin by setting up two domains, perhaps through [DynDNS.org](https://www.dyndns.org) as you saw in Chapter 4, and making two distinct directories:

```
mkdir -p /var/www/sites/homepublic
mkdir -p /var/www/sites/homecontrol
```

You then create two configuration files, one for each site. Follow the convention here of prefixing each site with a number. This allows you to name your publicly accessible as 000-public, meaning it will served first in the case of any web configuration problems, or the site is accessed with only an IP address. Dropping back to the public site in this fashion has less scope for damage, but it makes it impossible to use the HA control web site to correct the problem. Most errors of this type, however, are fixable only through SSH, so they aren’t a problem.

These two files are /etc/apache2/sites-available/000-default containing the following:

```
```apache
<VirtualHost *:80>
    ServerName mypublicpresence.homelinux.org

    ServerAdmin webmaster@localhost

    DocumentRoot /var/www/sites/homepublic/

    <Directory /var/www/sites/homepublic>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride AuthConfig
        Order allow,deny
        allow from all
        deny from none
    </Directory>

</VirtualHost>
```
```

and /etc/apache2/sites-available/001-control containing the same thing but with homepublic replaced with homecontrol and an alternate ServerName. They are then enabled manually, and the web server is restarted with the trinity of the following, run as root:

```
a2ensite 000-default
a2ensite 001-control
apache2ctl graceful
```