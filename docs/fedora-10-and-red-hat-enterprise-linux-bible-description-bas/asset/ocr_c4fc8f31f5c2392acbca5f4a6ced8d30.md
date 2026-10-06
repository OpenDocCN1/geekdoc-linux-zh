# Chapter 20: Setting Up an FTP Server 837

access to your server. To deal with the issue, you can use ephemeral port numbers (which provide random, temporary port numbers within a range of needed). For a description of the issue, refer to the FTP and Firewall page at http://www.nfcftp.com/nfcptd/doc/misc/ftp_and_firewalls.html.

# Getting More Information about FTP Servers

There are plenty of resources for gaining information about FTP servers. Here are some of your options:

+   * FAQ — To check out the vsFtpd FAQ, go to /usr/share/doc/vsfptd*/FAQ.
* RFCs — Requests Comments For the documents that define standard protocols with the Internet. The main RFC for FTP is RFC959. You can obtain RFCs from a variety of locations on the Internet, including the Internet RFC/FYI/STD/BCP Archives (http://www.faqs.org/rcfs).
* CERT — This organization provides useful documents for setting up FTP servers. Anonymous FTP Abuses how to respond and recover from FTP server abuse. It also tells how to deal with software piracy issues. Configuration Guidelines provide general guidance in setting up your FTP area, as well as specific challenges of setting up a writable FTP area. Both of those documents are available from the CERT Tech Tips page (http://www.cert.org/tech_tips).

> TIP: I strongly recommend reading the FTP documents from CERT. The tips in these documents will keep your FTP server secure, enabling you to offer the services that you want to share.

# Summary

The FTP service is the primary method of offering archives of document and software files to users over the Internet. The only FTP server package delivered with Fedora and RHEL is the Very Secure FTP (vsFtpd) server. The vsFtppd server relies on standard Linux file and user permissions to provide a simple, yet secure FTP environment to run in Fedora.