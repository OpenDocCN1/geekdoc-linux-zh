# Chapter 7 • Securing Exchange and Outlook Web Access

> > WARNING
> When requesting a certificate, when you specify the CN (common name) make sure you use the FQDN that the clients will use when they access the server.

# Enabling SSL for POP3, IMAP4, or NNTP Clients

Once you have decided what you want to do about a certificate authority, you can use the Exchange System Manager to issue certificates to all Exchange IMAP4, POP3, and NNTP virtual servers on which you secure communications. To issue a certificate, you must have the FQDN that your clients will be using when they connect to that particular server. For example, if you are configuring an Exchange 2000 front-end server that will be used by POP3 clients, you would configure the POP3 virtual server on the front-end server to use SSL. You would need to assign a FQDN to that front-end server. In this example, I use mail.somorita.com. I would need to follow these steps to assign a certificate to the front-end POP3 virtual server.

+   1. Using System Manager, open up the front-end server's Protocols container and the POP3 container. Right-click on the POP3 virtual server and choose Properties.
2. Click the Access property page and then the Certificate button. When the wizard starts, click Next.
3. If you have already got the certificate on the server for another protocol, or if you have a backup of a certificate Assign an existing certificate, or Import a certificate from a Key Manager backup file. Since this is probably the first time you have configured SSL, click Create a new certificate and click Next.
4. If you are going to send the request to another certificate authority, click Prepare the request now, but wait it later. (This option will create a certificate file that you can send on to certificate authority.) If you have installed the Windows 2000 certificate server as an “Enterprise” server, you can click Send the request immediately to an online certification authority. Then click Next.

![](bbox=[0.068, 0.941, 0.294, 0.971])