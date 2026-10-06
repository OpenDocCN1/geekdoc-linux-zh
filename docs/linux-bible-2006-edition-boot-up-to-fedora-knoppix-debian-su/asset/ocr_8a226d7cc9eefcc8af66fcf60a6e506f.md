# Working with CUPS Printing

Tools such as CUPS Web-based Administration and Red Hat's Printer Configuration window effectively hide the underlying CUPS facility. There may be times, when you want to work directly with the tools and configuration files that come with CUPS. The following sections describe how to use some special CUPS features.

# Configuring the CUPS Server (cupsd.conf)

The cupsd daemon process listens for requests to your CUPS print server and responds to these requests based on settings in the /etc/cups/cupsd.conf file. The configuration variables in cupsd.conf file are in the same format as those in the Apache configuration file (httpd.conf).

Red Hat's Printer Configuration window adds access information to the cupsd. For other Linux systems, you may need to configure the cupsd.conf file manually. You can step through the cupsd.conf file to further tune your server. Let's take a look at some of the settings in the cupsd.conf file.

No classification is set by default. With the classification set to topsecret, you can have Top Secret displayed on all pages that through the print server:

+   Classification topsecret

Other classifications you can substitute for topsecret include: classified, confidential, secret, and undisclosed.

The ServerCertificate and ServerKey lines (commented out by default) can be set to indicate where the certificate and key are stored,:

```
ServerCertificate /etc/cups/ssl1/server.crt
ServerKey /etc/cups/ssl1/server.key
```

Activate these two lines if you want to do encrypted connections. Then add your certificate and key to the files noted.

Browsing is the feature where you broadcast information about your printer on your local network and listen for other print servers' information. Browsing is by default only for the local @LOCAL. You can allow CUPS browser information (BrowseAllow) for additional selected addresses. Browsing information is broad, by default, on address 255.255.255.255. Here's how these defaults appear in the cupsd.conf file:

```
Browsing On
BrowseProtocols cups
BrowseOrder Deny,Allow
BrowseAllow from @LOCAL
BrowseAddress 255.255.255.255
Listen *:631
```