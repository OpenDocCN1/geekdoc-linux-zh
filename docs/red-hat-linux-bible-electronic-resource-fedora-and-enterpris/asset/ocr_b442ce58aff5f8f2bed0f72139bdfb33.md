You can use this information to monitor the activities on your server. For example, if someone is trying to break into your system, you can see multiple failed login attempts. You can also see if you are getting more anonymous FTP requests than you can handle.

# ### Logging file transfers

If there are file transfers during the session, they are logged to the /var/log/xferlog. In that file you can see both incoming and outgoing file transfers. Here are two examples of log entries in the /var/log/xferlog file:

```
```
Sat Aug 23 21:26:20 2003 1 oak 1625 /in/log b i r mike ftp 1 root c
Sat Aug 23 21:27:23 2003 1 pine 124 /pub/a.txt a o r mike ftp 1 root c
```
```

In the first example, the transfer occurred at 21:26:20 on Saturday, August 23, 2003. The transfer time was only one (1) second. The remote host name is oak, and the size of the file is 1625 bytes. The transferred file was named log and was put in the /in directory on the FTP server. The type of transfer was binary (b). The underscore (_) indicates that no special action (such as file compression or decompression) was taken. The i shows that it was an incoming transfer. The user was a real user (r) named mike. The service invoked was ftp. Authentication was done using RFC931 authentication (1). The user id returned by the authentication method was root. The c indicates that the transfer was completed.

In the second example, several items are of interest. The remote computer name was pine. The file was transferred using an ASCII transfer method (a). The file /pub/a.txt was transferred from the file server (o).

# ## Getting More Information about FTP Servers

There are plenty of resources for gaining more information about FTP servers. Here are some of your options:

+   - **FAQ** — The latest version of the WU-FTPD frequently asked questions list is available from www.wu-ftpd.org/wu-ftpd-faq.html. To check out the vsFTPd FAQ, go to /usr/share/doc/vsftpd\*/FAQ.

+   - **RFCs** — Requests for comments are the documents that define standard protocols used with the Internet. The main RFC for FTP is RFC959. You can obtain RFCs from a variety of locations on the Internet, including the Internet RFC/FYI/STD/BCP Archives: www.faqs.org/rfcs.

+   - **CERT** — This organization provides useful documents for setting up FTP servers. Anonymous FTP Abuses describes how to respond to and recover from FTP server abuse. It also tells how to deal with software piracy issues. Anonymous FTP Configuration Guidelines provide general guidance in setting up your FTP area, as well as specific challenges of setting up a writable FTP area. Both of those documents are available from the CERT Tech Tips page (www.cert.org/tech\_tips).