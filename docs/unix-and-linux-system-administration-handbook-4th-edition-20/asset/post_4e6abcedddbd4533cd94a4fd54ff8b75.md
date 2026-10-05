
## Configuring Apache to use SSL

You are prompted to enter and confirm a passphrase to encrypt the server key. Back up the server.key to a secure location (readable only by root), and be sure to remember the passphrase you entered. The curious can view the numeric details of the key with this command:

```
$ openssl rsa -out -text -in server.key
```

Next, create a Certificate Signing Request (CSR) that incorporates the server key you just generated:

```
$ openssl req -new -key server.key -out server.csr
```

Enter the fully qualified domain name of the server when you are prompted to enter a "common name." For example, if your site's URL is https://company.com, enter "company.com" as your common name. Note that you need a separate certificate for each hostname—even to the point that "www.company.com" is different from "company.com". Companies typically register only one common name; make sure any SSL-based links point to that hostname.

You can view the details of a generated CSR with the following command:

```
$ openssl req -text -text -in server.csr
```

You can send the server.csr file to the CA of your choice to be signed. It is not necessary to preserve your local copy. The signed CSR returned by the CA should have the extension .crt. Put the signed certificate in a directory with your httpd files, for example, /usr/local/apache2/conf/ssl.crt.

## Configuring Apache to use SSL

HTTP requests come in port 80, and HTTPS requests use port 443. Both HTTPS and HTTP traffic can be served by the Apache process. However, SSL does not work with name-based virtual hosts; each virtual host must have a specific IP address. (This limitation is a consequence of SSL designs.)

To set up Apache for SSL, make sure that the SSL module is enabled by locating the httpd.conf or adding the line

```
LoadModule ssl_module modules/mod_ssl.so
```

Add a VirtualHost for the SSL port:

```
<VirtualHost 128.138.243.150:443>
ServerName www.company.com
ServerAdmin webmaster@www.company.com
DocumentRoot /var/www/htdocs/company
ErrorLog logs/www.company.com-ssl-error_log
CustomLog logs/www.company.com-ssl_access.log combined
ScriptAlias /cgi-bin/ /var/www/cgi-bin/
SSLEngine on
SSLCertificateFile /usr/local/apache2/conf/ssl/server.crt
SSLCertificateKeyFile /usr/local/apache2/conf/ssl/server.key
</VirtualHost>
```

Note: after the IP address and the SSL directives that tell Apache where to find your private key and signed certificate. When you restart Apache, you will be asked to enter the passphrase for your server.key file. Because of this interaction, httpd can no longer start automatically when the machine is booted. If you want, you can remove the encryption from your private key to:

```
$ cp server.key server.key.bak
$ openssl rsa -in server.key -out server.key
$ chmod 400 server.key
```

Of course, anyone who obtains a copy of your unencrypted key can impersonate your site. For more information about SSL, see the following resources:

```
http://apache.org/docs/2.2/ssl/faq.html
http://apache.org/docs/2.2/mod_ssl.html
```

## 23.5 CACHING AND PROXY SERVERS

The Internet and the information on it are still growing. Ergo, the bandwidth and computing resources to support it are growing as well. How can this state of affairs continue? The only way to deal with this growth is to use replication. When it's on a national, regional, or site level, Internet content needs to be readily available from a closer source. It doesn't make sense to transmit the same popular web page across an expensive link millions of times each day. Fortunately, at least at the site level, a proxy lets you cache and manage outbound requests.

Here's how it works: Web browsers connect to the proxy server to request an object from the Internet. The proxy server makes the request on the client's behalf or provides the object from its cache, and returns the result to the client. Proxy servers of this type are often used to enhance security or to filter content. In a proxy-based system, only one machine needs access to the Internet through the organization's firewall. At schools, a proxy server can also filter inappropriate material so it doesn't fall into the wrong hands. Many commercial and freely available proxy servers are available today. Some of these systems are purely software based, and others are embedded in hardware appliances. An extensive list of proxy technologies can be found at web-caching.com/proxy-caches.html.

### Setting up Squid

The next couple of sections describe a popular standalone cache. We also delve briefly into the proxy features of the mod_cache module.

## Using the Squid cache and proxy server

Squid is a caching and proxy server that supports several protocols, including HTTP, FTP, and SSL. Proxy service is nice, but Squid's caching features are really worth getting about. Squid not only caches information from user requests but allows construction of a hierarchy of Squid servers using the Internet Cache Protocol (ICP) to communicate information about what is in their caches.

With this feature, administrators can build a system in which local users connect to an onsite caching server to obtain content from the Internet. If another user at that site has requested the same content, a copy can be returned at LAN speed (usually 100 MB/s or greater). If the local Squid server doesn't have the object, the proxy contacts the regional caching server. As in the local case, if not, the caching server for the country or continent is contacted, and so on. Users perceive a performance improvement, so they are happy.

For many, Squid offers economic benefits. Users tend to share web discoveries; significant duplication of external requests can occur at reasonable size. One study has that running a caching server can reduce external requirements up to 40%.

To make effective use of Squid, you'll likely want to force your users to use the cache. Either configure a default proxy through Active Directory (in a Windows-based environment) or configure your router to redirect all web-based traffic to the Squid cache using the Web Cache Communication Protocol, WCCP.

## Setting up Squid

Squid is easy to install and configure. Since Squid needs space to store its cache, you should run it on a dedicated machine that has plenty of free memory and disk space. A configuration for a large cache would be a machine with 32GiB of RAM and 8TB of disk.

You may be able to use precompiled Squid binaries for your system, or to download a fresh copy of Squid from squid-cache.org. If you choose to compile it yourself, run the configure script at the top of the source tree before you unpack the package.

- 1. Why "Squid"? According to the FAQ, "all the good names were taken."
- 2. Unfortunately, some sites mark all their pages as being uncacheable, which prevents Squid from working its magic. In a similar vein, Squid isn't able to cache dynamically generated pages.

![](img/579efec8c67772f31ecf34844bbb71a2_1023_0.png)

## Chapter 23 Web Hosting

/usr/local/squid. If you prefer some other location, use the --prefix=dir option to configure. After make configure has completed, run make all and then make install.

Once you've installed squid, you must localize the squid.conf configuration file. See the QUICKSTART file in the distribution directory for a list of the changes you need to make to the sample squid.conf file.

You must also run squid -z by hand to build and zero out the directory structure in which cached web pages will be stored. Finally, you can start the server with the RunCache script; it will normally be started by a script when the machine boots.

To test squid, configure your desktop browser to use the Squid server as a proxy. This option is usually found in the browser's preferences panel.

## Reverse-proxying with Apache

For security or load balancing, it's sometimes useful for web hosting sites to proxy inbound requests (that is, requests to your web servers that are coming in browsers on the Internet). Since this is backward from the typical use of a web proxy (handling outbound requests from browsers at your site), an inversion is called reverse proxy.

One popular configuration puts a reverse proxy on your site's DMZ network to accept Internet users' requests for services such as web-based email. The proxy then passes these requests along to the appropriate internal servers. This approach has advantages:

- It eliminates the temptation to allow direct connections to servers that are not in the DMZ.
- You need to configure only a single DMZ server, rather than one server for each accessible service.
- You can control the accessible URLs at a central choke point, providing some security benefit.
- You can log inbound requests for monitoring and analysis.

Configuring Apache to provide reverse proxy service is relatively straightforward. Inside a VirtualHost clause in Apache's httpd.conf file, you use the ProxyPass and ProxyPassReverse directives.

- ProxyPass maps a remote URL into the URL space of the local server, making that part of the local address appear to be a mirror of the remote server. (In this scenario, the "local" server is the DMZ machine and the "remote" server is the server on your interior network.)
- ProxyPassReverse hides the real server by "touching up" HTTP headers that transit the proxy.
