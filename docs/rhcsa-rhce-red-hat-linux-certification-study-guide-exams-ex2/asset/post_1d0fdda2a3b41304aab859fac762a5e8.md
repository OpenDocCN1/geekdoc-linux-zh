
The output should list the default and individual virtual hosts. For example, I see the following output from one of my server1.example.com RHEL 6 systems:

```
VirtualHost configuration:
wildcard NameVirtualHosts and _default_ servers:
*:80 is a NameVirtualHost
default server vhost1.example.com (/etc/httpd/conf/httpd.conf:1010)
port 80 namevhost vhost1.example.com (/etc/httpd/conf/httpd.conf:1010)
port 80 namevhost vhost2.example.com (/etc/httpd/conf/httpd.conf:1017)
*:443 is a NameVirtualHost
default server vhost1.example.com (/etc/httpd/conf.d/ssl.conf:75)
port 443 namevhost vhost1.example.com (/etc/httpd/conf.d/ssl.conf:75)
port 443 namevhost vhost2.example.com (/etc/httpd/conf.d/ssl.conf:105)
Syntax OK
```

If a "using 127.0.0.1 for ServerName" error appears, you haven't assigned a value for the ServerName directive. In addition, you may want to set up the /etc/hosts file, or a DNS server for the local network, with the IP addresses for domain names like vhost1.example.com and vhost2.example.com.

## Secure Virtual Hosts

If you're configuring a secure web server that conforms to the HTTPS protocol, Red Hat provides a different configuration file for this purpose: ssl.conf in the /etc/httpd/conf.d directory. If this file isn't available, you need to install the mod_ssl RPM. Before editing this file, back it up. The first active directive loads the SSL module:

```
LoadModule ssl_module modules/mod_ssl.so
```

Make sure the following Listen directive is active:

```
Listen 443
```

As suggested by the title, this configuration file includes a number of passphrase dialogues. Generally, no changes are required to these directives:

```
SSLPassPhraseDialog builtin
SSLSessionCache shmcb:/var/cache/mod_ssl/scache(512000)
SSLSessionCacheTimeout 300
SSLMutex default
SSLRandomSeed startup file:/dev/urandom 256
SSLRandomSeed connect builtin
SSLCryptoDevice builtin
```

Before the virtual host containers, you'll need to include a NameVirtualHost directive for Port 443 before you can configure multiple virtual hosts in this file. It's the same directive used in the main Apache configuration file, just pointed to the standard HTTPS port:

```
NameVirtualHost *:443
```

Now you can set up virtual hosts with the directives that follow. The default ssl.conf file also has a model virtual host container. But it is incomplete and a bit difficult to read with all of the comments. So a sample of the revised ssl.conf configuration file, focused on the virtual host container for the vhost1.example.com system, is shown in Figure 14-9.

In the default version of the ssl.conf file, examine the <VirtualHost _default_:443> container. Compare it to the <VirtualHost *:80> container in httpd.conf. Some changes are required. First, you should replace _default_ in the VirtualHost container with an asterisk (*):

```
<VirtualHost *:443>
```

### FIGURE 14-9

Secure virtual host container for vhost1.example.com

```
##
NameVirtualHost *:443

<VirtualHost *:443>
    DocumentRoot /www/securedocs/vhost1.example.com
    ServerName vhost1.example.com
    ErrorLog logs/ssl_error_log
    TransferLog logs/ssl_access_log
    LogLevel warn

    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:RC4+RSA:+HIGH:+MEDIUM:+LOW
    SSLCertificateFile /etc/pki/tls/certs/localhost.crt
    SSLCertificateKeyFile /etc/pki/tls/private/localhost.key

    <Files ~ "\.(cgi|shtml|html|php3)\$">
        SSLOptions +StdEnvVars
    </Files>

    <Directory "/var/www/cgi-bin">
        SSLOptions +StdEnvVars
    </Directory>

    SetEnvIf User-Agent ".*MSIE.*" \
    nokeepalive ssl-unclean-shutdown \
    downgrade-1.0 force-response-1.0

    CustomLog logs/ssl_request_log \
    "%t %h %{SSL_PROTOCOL}x %{SSL_CIPHER}x \"%r\" %b"

</VirtualHost>
```

You should also include ServerAdmin, DocumentRoot, and ServerName directives. Example directives that would be consistent with the virtual hosts created in the preceding section include

```
ServerAdmin webmaster@vhost1.example.com
DocumentRoot /www/securedocs/vhost1.example.com
ServerName vhost1.example.com
```

While the DocumentRoot directive can be set to any directory, it's appropriate if only for organizational purposes, to keep the files associated with each virtual host in a dedicated directory.

The standard error log directives can be changed. In fact, if you want log information for each secure web site to be set up in different files, they should be changed. But for our purposes, you can stick with the default options shown here. Based on the ServerRoot directive from the httpd.conf file, these log files can be found in the /var/log/httpd directory.

```
ErrorLog logs/ssl_error_log
TransferLog logs/ssl_access_log
LogLevel warn
CustomLog logs/ssl_request_log \
    "%t %h %{SSL_PROTOCOL}x %{SSL_CIPHER}x \"%r\" %b"
```

The SSL directives in the file are based on the default certificates for the localhost system. Shortly, you'll see how to configure a new SSL certificate. The following five directives, in order, activate SSL, use the more secure SSL version 2, support a variety of encryption ciphers, point to the default SSL certificate, as well as the SSL key file.

```
SSLEngine on
SSLProtocol all -SSLv2
SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:RC4+RSA:+HIGH:+MEDIUM:+LOW
SSLCertificateFile /etc/pki/tls/certs/localhost.crt
SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
```

The stanza that follows relates to files with extensions associated with dynamic content. For such files, along with any files in the standard CGI directory, standard SSL environment variables are used:

```
<Files ~ "\.(cgi|shtml|phtml|php3)$">
    SSLOptions +StdEnvVars
</Files>
<Directory "/var/www/cgi-bin">
    SSLOptions +StdEnvVars
</Directory>
```

The following stanza deals with situations associated with the Microsoft Internet Explorer as a browser client:

```
SetEnvIf User-Agent ".*MSIE.*" \
  nokeepalive ssl-unclean-shutdown \
  downgrade-1.0 force-response-1.0
```

Of course, the virtual host container ends with the following directive:

```
</VirtualHost>
```

When Apache is configured with a secure site, regular GUI clients that access that site get a warning about the secure web host like that seen for so many web sites on the Internet, as shown in Figure 14-10.

## Create a New SSL Certificate

While the default SSL certificate listed in the ssl.conf configuration file can work for basic configuration, you may want to either create a specialized local certificate or otherwise use an actual certificate purchased from a certificate authority (CA) such as VeriSign and Thawte.

### FIGURE 14-10

A warning about secure hosts

![](img/9139201cfcaf4292284a0eed074928e5_799_0.png)

Navigate to the /etc/pki/tls/certs directory. Note the file named Makefile in that directory. The code in that file can be used by the make command to create a new certificate for each virtual host. Unless you purchase an actual certificate from a CA, clients will still see screens such as that shown in Figure 14-10.

But you may need to know how to set up a "self-signed certificate." To that end, the following command, when run from the /etc/pki/tls/certs directory, automatically generates a private key and a certificate for the cited FQDN, as shown in Figure 14-11.

```
# genkey vhost2.example.com
```

The genkey command is convenient, as when the process is complete, it automatically writes the key to the /etc/pki/tls/private directory and writes the certificate to the /etc/pki/tls/certs directory.

> Exam Watch
> The published outline for the Red Hat prep course for the RHCE (RH254) specifies the deployment of "an SSL-encapsulated web service." SSL certificates are part of that deployment process. If you're asked to create a certificate during an exam, keep the size of the key to the minimum allowed. The process of generating even 512-bit keys can take several minutes.

### FIGURE 14-11

Prompts for a self-signed certificate

![](img/9139201cfcaf4292284a0eed074928e5_800_0.png)
