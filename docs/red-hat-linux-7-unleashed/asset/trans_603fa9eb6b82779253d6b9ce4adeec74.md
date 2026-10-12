

# **清单 12.3（续）**

```
# The following directive disables HTTP/1.1 responses to browsers which are in violation of the HTTP/1.0 spec by not being able to grok a basic 1.1 response.
BrowserMatch "RealPlayer 4\.0" force-response-1\.0
BrowserMatch "Java/1\.0" force-response-1\.0
BrowserMatch "JDK/1\.0" force-response-1\.0
```

```
# If the perl module is installed, this will be enabled.
<IfModule mod_perl.c>
Alias /perl/ /var/www/perl/
<Location /perl>
SetHandler perl-script
PerlHandler Apache::Registry
Options +ExecCGI
</Location>
</IfModule>
```

```
# Allow http put (such as Netscape Gold's publish feature)
# Use htpasswd to generate /etc/httpd/conf/passwd.
# You must uncomment these two lines at the top of this file as well:
#LoadModule mod_perl modules/mod_perl.so
#LoadModule mod_put.c
#
#Alias /upload /tmp
#<Location /upload>
# EnablePut On
# AuthType Basic
# AuthName Temporary
# AuthUserFile /etc/httpd/conf/passwd
# EnableDelete Off
# umask 007
# <Limit PUT>
# require valid-user
# </Limit>
#</Location>
```

```
# Allow server status reports, with the URL of http://servername/server-status
# Change the ".your_domain.com" to match your domain to enable.
# <Location /server-status>
SetHandler server-status
Order deny,allow
Deny from all
Allow from gnulix.org
</Location>
```

# 清单 12.3（续）

```
# Allow remote server configuration reports, with the URL of
# http://servername/server-info (requires that mod_info.c be loaded)
# Change the ".your_domain.com" to match your domain to enable.
#<Location /server-info>
    SetHandler server-info
    Order deny,allow
    Deny from all
    Allow from gnulix.org
</Location>

# Allow access to local system documentation from localhost
Alias /doc/ /usr/share/doc/
<Location /doc>
    Order deny,allow
    deny from all
    allow from localhost
    Options Indexes FollowSymLinks
</Location>

# There have been reports of people trying to abuse an old bug from pre-1.1
# days. This bug involved a CGI script distributed as a part of Apache..
# By uncommenting these lines you can redirect these attacks to a logging
# script on phf.apache.org. Or, you can record them yourself, using the script
# support/phf_abuse_log.cgi.
#
#<Location /cgi-bin/php*>
#     Deny from all
#     ErrorDocument 403 http://phf.apache.org/phf_abuse_log.cgi
#</Location>

#
# Proxy Server directives. Uncomment the following lines to
# enable the proxy server:
#<IfModule mod_proxy.c>
#ProxyRequests On

#<Directory proxy:>
#     Order deny,allow
#     Deny from all
#     Allow from .your_domain.com
#</Directory>

#
# Enable/disable the handling of HTTP/1.1 "Via:" headers.
# ("Full" adds the server version; "Block" removes all outgoing Via: headers)
# Set to one of: Off | On | Full | Block
#ProxyVia On

#
# To enable the cache as well, edit and uncomment the following lines:
# (no caching without CacheRoot)
#
#CacheRoot "/var/cache/httpd"
#CacheSize 5
#CacheGcInterval 4
#CacheMaxExpire 24
#CacheLastModifiedFactor 0.1
#CacheDefaultExpire 1
#NoCache a_domain.com another_domain.edu joes_garage_sale.com

#</IfModule>
# End of proxy directives.

### Section 3: Virtual Hosts
#
# VirtualHost: If you want to maintain multiple domains/hostnames on your
# machine you can setup VirtualHost containers for them.
#  (Please see the documentation at <URL:http://www.apache.org/docs/vhosts/>
#  for further details before you try to setup virtual hosts).
# You may use the command line option '-S' to verify your virtual host
# configuration.
#
# If you want to use name-based virtual hosts you need to define at
# least one IP address (and port number) for them.
#
#NameVirtualHost 12.34.56.78:80
#NameVirtualHost 12.34.56.78
#
# VirtualHost example:
# Almost any Apache directive may go into a VirtualHost container.
#
#<VirtualHost ip.address.of.host.some_domain.com>
#  ServerAdmin webmaster@host.some_domain.com
#  DocumentRoot /www/docs/host.some_domain.com
#  ServerName host.some_domain.com
#  ErrorLog logs/host.some_domain.com-error_log
#  CustomLog logs/host.some_domain.com-access_log common
#</VirtualHost>
#<VirtualHost _default_:*>
#</VirtualHost>
```

```
<IfDefine HAVE_SSL>

##
### SSL Virtual Host Context
###

# Apache will only listen on port 80 by default. Defining the virtual server
# (below) won't make it automatically listen on the virtual server's port.
Listen 443
<VirtualHost _default_:443>

# General setup for the virtual host
DocumentRoot "/var/www/html"

# SSL Engine Switch:
# Enable/Disable SSL for this virtual host.
SSLEngine on

# SSL Cipher Suite:
# List the ciphers that the client is permitted to negotiate.
# See the mod_ssl documentation for a complete list.
SSLCipherSuite ALL:+ADH:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP:+eNULL

# Server Certificate:
# Point SSLCertificateFile at a PEM encoded certificate.  If
# the certificate is encrypted, then you will be prompted for a
# pass phrase.  Note that a kill -HUP will prompt again.  A test
# certificate can be generated with 'make certificate' under
# built time.  Keep in mind that if you've both a RSA and a DSA
# certificate you can configure both in parallel (to also allow
# the use of DSA ciphers, etc.)
SSLCertificateFile /etc/httpd/conf/ssl.crt/server.crt
#SSLCertificateFile /etc/httpd/conf/ssl.crt/server-dsa.crt

# Server Private Key:
# If the key is not combined with the certificate, use this
# directive to point at the key file.  Keep in mind that if
# you've both a RSA and a DSA private key you can configure
# both in parallel (to also allow the use of DSA ciphers, etc.)
SSLCertificateKeyFile /etc/httpd/conf/ssl.key/server.key
#SSLCertificateKeyFile /etc/httpd/conf/ssl.key/server-dsa.key

# Server Certificate Chain:
# Point SSLCertificateChainFile at a file containing the
# concatenation of PEM encoded CA certificates which form the
# certificate chain for the server certificate. Alternatively
# the referenced file can be the same as SSLeCertificateFile
# when the CA certificates are directly appended to the server
# certificate for convenience.
#SSLCertificateChainFile /etc/httpd/conf/ssl.crt/ca.crt

# Certificate Authority (CA):
# Set the CA certificate verification path where to find CA
# certificates for client authentication or alternatively one
# huge file containing all of them (file must be PEM encoded)
# Note: Inside SSLCACertificatePath you need hash symlinks
# to point to the certificate files. Use the provided
# Makefile to update the hash symlinks after changes.
#SSLCACertificatePath /etc/httpd/conf/ssl.crt
#SSLCACertificateFile /etc/httpd/conf/ssl.crt/ca-bundle.crt

# Certificate Revocation Lists (CRL):
# Set the CA revocation path where to find CA files for client
# authentication or alternatively one huge file containing all
# of them (file must be PEM encoded)
# Note: Inside SSLCARevocationPath you need hash symlinks
# to point to the certificate files. Use the provided
# Makefile to update the hash symlinks after changes.
#SSLCARevocationPath /etc/httpd/conf/ssl.crl
#SSLCARevocationFile /etc/httpd/conf/ssl.crl/ca-bundle.crl

# Client Authentication (Type):
# Client certificate verification type and depth. Types are
# none, optional, require and optional_no_ca. Depth is a
# number which specifies how deeply to verify the certificate
# issuer chain before deciding the certificate is not valid.
#SSLVerifyClient require
#SSLVerifyDepth 10

# Access Control:
# With SSLRequire you can do per-directory access control based
# on arbitrary complex boolean expressions containing server
# variable checks and other lookup directives. The syntax is a
# mixture between C and Perl. See the mod_ssl documentation
# for more details.
#<Location />
#SSLRequire ( %{SSL_CIPHER} !~ "/^(EXP|NULL)" \
# and %{SSL_CLIENT_S_DN_OU} eq "Snake Oil, Ltd." \
# and %{SSL_CLIENT_S_DN_OU} in ("Staff", "CA", "Dev") \
# and %{TIME_WDAY} >= 1 and %{TIME_WDAY} <= 5 \
# and %{TIME_HOUR} >= 8 and %{TIME_HOUR} <= 20
# or %{REMOTE_ADDR} =~ m/^192\.76\.162\.[0-9]+$/
#</Location>

# SSL Engine Options:
# Set various options for the SSL engine.
#
# FakeBasicAuth:
# Translate the client X.509 into a Basic Authorisation. This means that
# the standard Auth/DBM/Auth methods can be used for access control. The
# user name is the 'one line' version of the client's X.509 certificate.
#
# Note that no password is obtained from the user. Every entry in the user
```

Apache 服务器
第 12 章
415

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_452_0.png)

