# mod_ssl

SSL (Secure Sockets Layer), which is implemented by the mod_ssl module, has two functions: It allows a client to verify the identity of a server and it enables secure two-way communication between a client and a server. SSL is used on Web pages in conjunction with forms that require passwords, credit card numbers, or other sensitive data.

Apache uses the HTTPS protocol—not HTTP—for SSL communication. When Apache uses SSL, it listens on a second port (443 by default) for a connection and performs a handshaking sequence before sending the requested content to the client.

Server verification is critical for financial transactions. After all, you do not want to give your credit card number to a fraudulent Web site posing as a known company. SSL uses a certificate to positively identify a server. Over a public network such as the Internet, the identification is reliable only if the certificate contains a digital signature from an authoritative source such as VeriSign or Thawte. SSL Web pages are denoted by a URI beginning with https://.

Data encryption prevents malicious users from eavesdropping on Internet connections and copying personal information. To encrypt communication, SSL sits between the network and an application and encrypts communication between the server and the client.

# Setting Up mod_ssl

The mod_ssl package is installed as part of the apache2 package—you do not need to install it separately. The /etc/apache2/mods-available/ssl.conf file configures mod_ssl; ssl.load, which is in the same directory, loads it. You must enable the module with the command a2enmod ssl. The first few directives in this file set various parameters for SSL operation.

You can set up a virtual host for SSL in the sites-available directory and enable it using a2ensite (page 906). As with any virtual host, a virtual host for SSL holds directives such as ServerName and ServerAdmin that need to be configured. In addition, it holds some SSL-related directives. See the example on page 940.

# Using a Self-Signed Certificate for Encryption

If you require SSL for encryption and not verification—that is, if the client already trusts the server—you can generate and use a self-signed certificate, bypassing the time and expense involved in obtaining a digitally signed certificate. Self-signed certificates generate a warning when you connect to the server: Most browsers display a dialog box that allows you to examine and accept the certificate. The exim4 daemon also uses certificates (page 736).

The following example creates a self-signed certificate. (See the procedure at www.modssl.org/docs/2.8/ssl_faq.html#To2.82if apache2-ssl-certificate is missing from the system. You do not need to send in the CSR for a self-signed certificate.)