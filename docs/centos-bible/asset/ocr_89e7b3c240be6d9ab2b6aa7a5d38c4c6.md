# Getting More Information about FTP Servers

There are plenty of resources for gaining more information about FTP servers. Here are some of your options:

+   - **FAQ** — To check out the vsFTPd FAQ, go to `/usr/share/doc/vsftpd*/FAQ`.

+   - **RFCs** — Requests For Comments are the documents that define standard protocols used with the Internet. The main RFC for FTP is RFC059. You can obtain RFCs from a variety of locations on the Internet, including the Internet RFC/FYIS/STD/BCP Archives (`www.faqs.org/rfcs`).

+   - **CERT** — This organization provides useful documents for setting up FTP servers. Anonymous FTP Abuses describes how to respond to and recover from FTP server abuse. It also tells how to deal with software piracy issues. Anonymous FTP Configuration Guidelines provides general guidance on setting up your FTP area, as well as specific challenges of setting up a writable FTP area. Both of those documents are available from the CERT Tech Tips page (`www.cert.org/tech_tips`).

> TIP I strongly recommend reading the FTP documents from CERT. The tips in these documents will help keep your FTP server secure, while enabling you to offer the services that you want to share.

# Summary

The FTP service is the primary method of offering archives of document and software files to users over the Internet. The only FTP server package delivered with CentOS is the Very Secure FTP (vsFTPd) server. The vsFTPd server relies on standard Linux file and user permissions to provide a simple, yet secure, FTP environment to run in CentOS.