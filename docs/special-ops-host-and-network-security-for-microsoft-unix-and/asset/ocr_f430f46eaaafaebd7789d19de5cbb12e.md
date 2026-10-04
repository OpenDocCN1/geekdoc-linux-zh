# Securing Exchange and Outlook Web Access • Chapter 7

instructions for assigning a certificate to an SMTP virtual server are almost identical to the instructions for assigning a certificate to a POP3 or IMAP4 server, which was detailed earlier in this chapter. Once you have assigned the certificate to the SMTP virtual server, if this virtual server is going to be used only by remote POP3 or IMAP4 clients you should require SSL. This is enabled on the Access page (Communication button).

The second condition in situation where you may want to ensure TLS/SSL is if you want all SMTP traffic to be encrypted. Assign a certificate to all of the SMTP virtual servers in the organization, configure them to require TLS/SSL, and then on each SMTP virtual server’s Delivery property page click the Outbound security button. The Outbound Security dialog box (shown in Figure 7.23) has the TLS encryption check box.

# 7.23 Requiring Outbound TLS/SSL on the Properties of an SMTP Virtual Server

![](bbox=[0.353, 0.401, 0.646, 0.633])

If you have outbound communication to SMTP servers outside of your organization, you must create an SMTP virtual server that does not require outbound TLS/SSL. You then assign this SMTP virtual server to be used as a local bridgehead by the SMTP Connector.

# Changing the SMTP Banner

When you connect to a Windows 2000 SMTP virtual server, you are presented with the default SMTP banner. This banner is going to be quite similar to:

```
220 hnlex02.somorita_hnl.com Microsoft ESMTPS MAIL, Version:
5.0.2195.532
```

9 ready at Wed, 4 Sep 2002 00:26:18 -1000