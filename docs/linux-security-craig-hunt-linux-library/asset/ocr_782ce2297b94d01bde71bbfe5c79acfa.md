# **Listing 11.1 TIS e-mail acknowledgment of license agreement**

```
From: fwtk-req@tislabs.com
Date: Wed, 24 Jan 2001 08:18:08 -0500 (EST)
To: rhontanon@sybex.com
Subject: Response to your fwtk-request request

Thank you for your interest in our Firewall Toolkit. You will find
the current source in the following 'hidden' directory on
ftp.tislabs.com:
/pub/firewalls/toolkit/dist/fwtk-02d13d

Please change directory directly to the entire path provided. This
directory will exist for at least 12 hours. If you are unable to
download before this time period expires, you can send another
request to fwtk-request@tislabs.com to receive a new path.

If you are unable to establish a connection on ftp.tislabs.com,
your IP address may not have the appropriate reverse mapping of
address to hostname in the Domain Name System.

As a security precaution, we do not allow connections to our ftp
server that do not have this DNS information properly configured. Please
contact your System Administrator in regard to correcting
this.

~NAI Labs
```

**NOTE** Note that in order for you to download the FWTK software, your host must have a valid reverse DNS (PTR) record. The TIS FTP server will not allow you to access it if it can't match your IP address to a known host name.

Once you receive the e-mail (it should only take 5-10 minutes), log on to the TIS FTP site (see Listing 11.2) and go to the directory specified in the body of the message. You need to download (in binary form) two files:

+   - The main FWTK distribution (fwtk.tar.Z)
+   - The documentation archive (fwtk-doc-only.tar.Z)

# **Listing 11.2 Downloading FWTK from the TIS FTP site**

```
[ramon]$ ftp ftp.tislabs.com
Connected to portal.gw.tislabs.com.
```