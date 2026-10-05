module provided by the libapache-mod-php package, and its installation automatically enables the module.

Apache 2 includes the SSL module required for secure HTTP (HTTPS) out of the box. It first needs to be enabled with a2enmod ssl, and the required directives must be added to the configuration files. A configuration example is provided in /etc/apache2/sites-available/default-ssl.conf. See http://httpd.apache.org/docs/2.4/mod/mod_ssl.html for more information.

The full list of Apache modules can be found online at http://httpd.apache.org/docs/2.4/mod/index.html.

With its default configuration, the web server listens on port 80 (as configured in /etc/apache2/ports.conf), and serves pages from the /var/www/html/ directory by default (as configured in /etc/apache2/sites-enabled/000-default.conf).

# Configuring Virtual Hosts

A virtual host is an extra entity for the web (say www.kali.org and www.offensive-security.com) because the HTTP requests embedded both the name of the website requested and the URL localhost (this feature is known as name-based virtual hosts).

The default configuration for Apache 2 enables name-based virtual hosts. In addition, a default virtual host is defined in the /etc/apache2/sites-enabled/000-default.conf file; this virtual host will be used if no host matching the request sent by the client is found.

> Requests concerning unknown virtual hosts will always be served by the first defined virtual host, which is why the package ships a 000-default.conf configuration file, which sorts first among other files that you might create.

Each extra virtual host is described by a file stored in /etc/apache2/sites-available/. The file is usually named the hostname of the website followed by a .conf suffix (for example: www.example.com.conf). You can enable the new virtual host with a2ensite www.example.com. Here is a minimal virtual host configuration for a website files are stored in /srv/www/example.com/www/ (defined with the DocumentRoot option):

```
<VirtualHost *:80>
ServerName www.example.com
ServerAlias example.com
```