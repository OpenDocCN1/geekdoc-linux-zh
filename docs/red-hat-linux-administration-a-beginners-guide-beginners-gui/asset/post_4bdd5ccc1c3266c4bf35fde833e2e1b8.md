
Apache provides a way to get around this using the `ServerName` directive. By specifying what you want Apache to return as the host name of the web server, a system with a name like dioxin can have an alias of www, invisible to users of the site. Here is an example of the `ServerName` directive:

```apache
ServerName www.eng.domain.org
```

## Server Administrator

It's often a good idea, for a couple of reasons, to use an e-mail alias for a web site's administrator. First, there may be more than one administrator. By using an alias, it's possible for the alias to expand out to a list of e-mail addresses. Second, if the current administrator leaves, you don't want to have to make the rounds of all those web pages and change the name of the site administrator.

Assuming you have set up the e-mail alias so that `www@domain.com` represents your web administrator(s) (see Module 13 for doing this in Linux), you need to edit the ServerAdmin line in the `httpd.conf` file so that it reads as follows:

```apache
ServerAdmin www@domain.com
```

## Prefork MPM

As I mentioned earlier, the Multi-Processing Module (MPM) is a new feature in Apache that allows closer integration with the native networking features of each operating system. The trick is that, unlike regular Apache modules, you can only select one MPM, and you have to do so when Apache is compiled. While some of the available MPMs are just not relevant to us on Linux (`mpm_winnt`, for example) there are still a few different features implemented at the MPM level. The hybrid process/threading model I mentioned earlier is one example. For compatibility reasons, the Apache package included with Red Hat has been compiled with the prefork MPM, as it follows the same process model that was used in the Apache 1.3 series. Unfortunately, if you want to use a different MPM, you'll have to recompile Apache. Even sticking with the prefork MPM, there are a number of settings that you can adjust for performance.

Using the prefork model, Apache will start a number of processes and have them wait around for incoming connections. Each process can handle a number of requests from the same client. When the load grows, more processes are forked to handle the additional connections. When the load dies down, extraneous idle processes are killed off. With this in mind, the following options should start to make more sense.

This is the number of processes that Apache will fork as a starting point when it first starts up:

```apache
StartServers        8
```

Apache will always keep at least this many processes around:

```apache
MinSpareServers     5
```

This is the upper limit for idle processes:

```apache
MaxSpareServers    20
```

If there are more than these, Apache starts killing off some of them.

Apache will not start more processes than this maximum, even if the site is extremely busy:

```apache
MaxClients        150
```

This limits the number of client requests that a single process will handle:

```apache
MaxRequestsPerChild   1000
```

## IP Address and Port Selection

By default, Apache is set up to wait for connections to port 80 on any IP address assigned to the machine. If you want to change that behavior, you’ll be interested in the Listen directive. With this you can change what port is listened to or limit which IP addresses (assuming you have more than one) attention is paid to, as shown in the following examples:

```apache
Listen 8080
Listen 192.168.0.42:80
```

## Modules

As I mentioned earlier, loading modules to add additional functionality is where Apache’s real power shines through. This is accomplished with the LoadModule directive, specifying the module name (as indicated in its documentation) and the location of the library file. There are a good number of modules enabled in the default configuration, and it may be worth commenting out some of the ones you’re not really using. (In case it’s not already obvious, httpd.conf uses # as its comment character.)

```apache
LoadModule cgi_module modules/mod_cgi.so
#LoadModule speling_module modules/mod_speling.so
```

## Directory and Alias

You may have noticed by now that there are a number of HTML-like bracketed directives in httpd.conf, especially when there is a need to specify suboptions. The most prominent of these is the <directory>...</directory> block, which allows you to specify a different set of options for a particular directory than for the rest of your site. This is most helpful for grouping a set of files with special needs together, such as Common Gateway Interface (CGI) programs. You will also find this often used in conjunction with the Alias directive, which allows you to map a portion of your web space to a particular physical directory (separate from your document root).

```apache
Alias /icons/ "/var/www/icons/"
<Directory "/var/www/icons">
Options Indexes MultiViews
AllowOverride None
Order allow,deny
Allow from all
</Directory>
```

## Executable Scripts

The `ScriptAlias` directive works much like `Alias`, with the notable exception that accessing any file in the `ScriptAlias` directory will cause it to be executed rather than blindly returned to the client.

```apache
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"
```

> **NOTE**
> Obviously, it’s impossible to cover everything about the Apache HTTP server in a few short pages. The software’s online manual comes with the distribution and will give you the information you need. It’s written in HTML, so you can access it in a browser. Simply point to `http://localhost/manual/` or check out `http://httpd.apache.org/docs-2.0/`.

## Configuring Virtual Domains

One of the most used features of Apache is its ability to support virtual domains—that is, to allow multiple domains to be hosted from the same IP address. This is accomplished thanks to the HTTP 1.1 protocol, which specifies the desired site in the HTTP header rather than relying on the server to know what site to fetch based on its IP address.

> **NOTE**
> Don’t forget that it is not merely enough to configure a virtual domain using Apache. You must also get the domain itself from a company that sells domain names like Register.com. Once you have the domain name, you can either use your registrant’s DNS server or you can set up your own DNS server. Either way, you will need to establish the necessary entries so that `www.yourdomain.com` points to your web server. Of course, if you are just playing around and don’t want to set up a site for real, you can simply set up a local DNS server and create fictitious domains and IP addresses, or even just add the necessary entries to the `/etc/hosts` file.

To set up a new virtual domain, open the `httpd.conf` file in your favorite text editor and scroll toward the end of the file. The `NameVirtualHost` directive needs to be uncommented to allow Apache to differentiate client requests by the supplied domain name.

```apache
NameVirtualHost *
```

The * means that this will apply to all IP addresses Apache is listening to. Just below that you will find an example of a virtual host entry that has been commented out and looks something like this:

```apache
# VirtualHost example:
# Almost any Apache directive may go into a VirtualHost container.
# The first VirtualHost section is used for requests without a known
# server name.
#
#<VirtualHost *>
#	ServerAdmin webmaster@dumny-host.example.com
#	DocumentRoot /www/docs/dummy-host.example.com
#	ServerName dummy-host.example.com
#	ErrorLog logs/dummy-host.example.com-error_log
#	CustomLog logs/dummy-host.example.com-access_log common
#</VirtualHost>
```

Simply clone this entry and substitute in your own information. Many of the settings available for the basic server can have different values specified for each virtual host or can inherit the values used by the main server configuration. For example, a virtual host entry could look like this:

```apache
#
# Virtual Host Settings for company1.com and sideproject.org
#
<VirtualHost *>
	ServerName company1.com
	ServerAdmin webmaster@company1.com
	DocumentRoot /var/www/company1/html
	ErrorLog /var/log/httpd/company1/error_log
	CustomLog /var/log/httpd/access_log common
</VirtualHost>

<VirtualHost *>
	ServerName sideproject.org
	ServerAdmin webmaster@sideproject.org
	DocumentRoot /var/www/sideproject/html
	ErrorLog /var/log/httpd/sideproject/error_log
	CustomLog /var/log/httpd/access_log common
</VirtualHost>
```

Note that you have to do this for each host you want visible. So if you want to have both example.com and www.example.com resolve to the same web page, you need to set up a second virtual host setting for www.example.com, as well. (Both **www.example.com** and **example.com** can have the same configuration information, but they must remain separate virtual host entries.)

Once you have the information in there, simply restart Apache using the `/usr/sbin/apachectl` restart command, and you're off!
