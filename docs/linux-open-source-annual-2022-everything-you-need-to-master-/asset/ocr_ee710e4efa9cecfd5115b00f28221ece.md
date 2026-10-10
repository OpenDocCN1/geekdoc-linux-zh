# ## Essential features

Can our web servers run right out of the box – or not?

ut of the box, they all work. However, since we have different and changing needs, we can look at what they come with and how that will work for us. For testing HTML and browser-interpreted code such as CSS and JavaScript they all display static content, by default. But, as soon as we need to add a server-side language like PHP, we not only need that to be installed, but, need the server to communicate and use it effectively. Well, only a couple small tweaks are really required for all packages to make this possible. Once a minute or two is taken to configure PHP, so we can run database applications such as Wordpress, the rest of the details that must be considered are speed optimisation and security. So, let’s go through the list and see what we have post installation.

With Apache, the modules that are enabled by default include germs such as core, module, so, module, alias, module, auth_basic, module, deflate, module, dir, module, env, module, php7_module and rewrite, module. In addition to the out-of-the-box modules, Apache has many other that can be enabled with a single command, which includes SSL and mod\_expire. Nginx boasts some good ones, too, like fastcgi, ssl, gzip and geoip. Lighttpd also has an array of modules used by default which are mod\_access, mod\_alias, mod\_compress, mod\_redirect and mod\_.

![](bbox=[0.49, 0.1, 0.97, 0.29])

> Many useful modules are enabled by default and we can also examine the headers with a browser to show features and some data we should hide.

rewrite. These can be found in the /etc/lighttpd/lighttpd.conf file. Openlitespeed also works out of the box, even though it lags behind Nginx and Lighttpd. In addition, Openlitespeed requires more intermediate usage in order to customise it further. Tomcat works for simple static files and WAR files and, as such, it’s the go-to solution for testing these apps.

# ### VERDICT

| | APACHE | TOMCAT |
|---|---|---|
| NginX | 9/10 | Openlitespeed | 7/10 |
| Lighttpd | 8/10 |  |

Apache is the only server that a noob can dive into and configure with basic commands. The others are more aimed at intermediate users.

# ## Security features

Can we host a site safely?

hen we start our web server and test local pages, we are the only ones accessing our website with port 80. However, as soon as deploy a site online, we need to take security more seriously since our router will forward port 80, so outside users can access the site. Let’s do a quick run-through of our web servers and see what changes we need to make.

With a default Apache installation, we should make several changes; like installing the mod\_security module and making several changes to the /etc/apache2/conf-enabled/security. conf and /etc/apache2/apache2.conf files. With the /etc/apache2/conf-enabled/security.conf file, we should uncomment ServerSignature Off and ServerTokens Prod. We can also edit the apache2.conf file to turn off directory browsing and limit large requests to protect from denial-of-service attacks. With Nginx, we can open the file /etc/nginx/nginx.conf and set server\_tokens off to hide the server version. In addition, we have the ability to restrict pages by IP so our admin accounts are bullet-proof. We can also gimp away at the default config file. Openlitespeed is very good at controlling files by default. We had to edit the config file to be able to use subfolders and so on. To add more layers of protection, we can install mod\_security module and use bandwidth and connection throttling.

With Lighttpd, we can edit the lighttpd.conf file to our liking. Thus, we can set numbers for max connections, max keep alive, SSL, max connections per IP and prevent image hijacking. Tomcat needs quite a few configuration adjustments to deploy a live website. We can hide the server header, enable SSL/TLS and enforce HTTPS. We can also not run Tomcat as root, disable the SHUTDOWN port, disable sending of the X-Powered-By HTTP header, disable Tomcat from displaying directory listings and limit the availability of connector. In addition, we should change our php.ini file with expose\_php = Off. For further testing, we can always install wapiti and other monitoring tools like Monitor to test and monitor our local websites. Going a step further, we can use Kali Linux and perform penetration testing.

# ### VERDICT

| APACHE | 8/10 | TOMCAT | 7/10 |
|---|---|---|---|
| Nginx | 9/10 | Openlitespeed | 7/10 |
| Lighttpd | 9/10 |  |  |

Config files for Nginx, Lighttpd and Apache make it easy to add more security.

![](bbox=[0.5, 0.57, 0.97, 0.74])

> Simple editing and uncommenting lines for a main server config file will help to tighten up security for your website deployment.