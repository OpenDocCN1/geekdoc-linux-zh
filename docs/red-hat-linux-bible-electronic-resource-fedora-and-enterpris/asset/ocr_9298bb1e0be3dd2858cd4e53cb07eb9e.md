The Printer configuration window adds access information to the `cupsd.conf` file. You can step through the `cupsd.conf` file to further tune your CUPS server. Here are a few suggestions:

```
Classification topsecret
```

With the classification set to topsecret, you can have Top Secret displayed on all pages that go through the print server. Other classifications you can substitute for "topsecret" include: classified, confidential, secret, and unclassified.

```
ServerCertificate /etc/cups/ssl/server.crt
ServerKey /etc/cups/ssl/server.key
```

The ServerCertificate and ServerKey lines can be set up to indicate where the certificate and key are stored, respectively. Activate these two lines if you want to do encrypted connections. Then add your certificate and key to the files noted.

```
Browsing On
BrowseProtocols cups
BrowseAddress 255.255.255.255
Listen 127.0.0.1:631
```

Browsing is the feature whereby you broadcast information about your printer on your local network and listen for other print servers’ information. Browsing is on by default. Browsing information is also broadcast, by default, on address 255.255.255.255. You can allow or deny incoming CUPS browser information (BrowseAllow and BrowseDeny) for selected addresses. All incoming browser information is allowed, by default.

To allow Web-based CUPS administration, the cupsd daemon listens on port 631 of the local host (127.0.0.1). To allow anyone to access this service from your network (if he or she has the proper login and password), you can change the Listen line shown previously to Listen \*:631.

```
BrowseRelay source-address destination-address
```

With BrowseRelay, on, you can allow CUPS to browse information to be passed among two or more networks. This is a good way to allow users on several connected LANs to discover and use printers on other nearby LANs.

You can allow or deny access to different features of the CUPS server. An access definition for a CUPS printer (created from the Printer configuration window) might appear as follows:

```
<Location /printers/ns1-hpl>
Order Deny, Allow
Deny From All
Allow From 127.0.0.1
AuthType None
</Location>
```