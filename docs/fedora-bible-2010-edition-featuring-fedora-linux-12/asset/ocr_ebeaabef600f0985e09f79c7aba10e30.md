![](bbox=[0.18, 0.09, 0.88, 0.46])

Figure 16-5: Temporarily stop printing or print test pages from the Printers page.

# # Configuring the CUPS server (cupsd.conf)

The cupsd daemon process listens for requests to your CUPS print server and responds to those requests based on settings in the /etc/cups/cupsd.conf file. The configuration variables in cupsd.conf file are in the same form as those of the Apache configuration file (httpd.conf). After changing cupsd.conf, restart the server for changes to take effect.

The Printer Configuration window above accesses information to the cupsd.conf file. You can step through the cupsd.conf file to further tune your CUPS server. A few suggestions follow.

```
ServerCertificate /etc/cups/ssl/server.crt 
ServerKey /etc/cups/ssl/server.key
```

The ServerCertificate and ServerKey lines (not set by default) can be set up to indicate where the certificate and key are stored, respectively. Activate these two lines if you want to do encrypted connections. Then add your certificate and key to the files noted. Keep in mind that these keys are for the CUPS Web interface and are not used for sending print jobs.

```
Browsing On 
BrowseProtocols cups 
BrowseOrder Deny,Allow 
BrowseAllow from @LOCAL
```