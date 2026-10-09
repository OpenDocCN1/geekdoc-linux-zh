# ## NOTES ON CERTIFICATES

+   - As long as the server is identified by the name for which the certificate was issued, you can use the certificate on another server or IP address.
+   - A root certificate is the certificate that identifies the root certificate authority (root CA). Every browser contains a database of the public keys for the root certificates of the major signing authorities, including VeriSign and Thawte.
+   - It is possible to generate a root certificate and sign all your server certificates with this root CA. Regular clients can import the public key of the root CA so that they recognize every certificate signed by that root CA. This setup is convenient for a server with multiple SSL-enabled virtual hosts and no commercial certificates. For more information see www.modssl.org/docs/2.8/ssl_faq.html#ToC29 .
+   - A self-signed certificate does not enable clients to verify the identity of the server.

# ## AUTHENTICATION MODULES AND .htaccess FILES

To restrict access to a Web page, Apache and third parties provide authentication modules and methods that can verify a user's credentials, such as a username and password. Some modules support authentication against various databases including NIS (page 770) and LDAP (page 786).

User authentication directives are commonly placed in a **.htaccess** file. A basic **.htaccess** file that uses the Apache default authentication module (**mod\_auth**) follows. When placed in `/var/www/html`, this file causes Apache to request a password before a browser can access content in the `/var/www/html` directory hierarchy. Substitute appropriate values for the local server.

```
```bash
# cat .htaccess
AuthUserFile /var/www/html/.htpasswd
AuthGroupFile /dev/null
AuthName "Browser dialog box query"
AuthType Basic
require valid-user
```
```

The `/var/www/html/.htpasswd` is a typical absolute pathname of a **.htpasswd** file and **Browser dialog box query** is the string that the user will see as part of the dialog box that requests a username and password.

The second line of the preceding **.htaccess** file turns off the group function. The fourth line specifies the user authentication type **Basic**, which is implemented by the default **mod\_auth** module. The last line tells Apache which users can access the protected directory. The entry **valid-user** grants access to the directory to any user whose username appears in the Apache password file and who enters the correct password.

You can put the Apache password file anywhere on the system, as long as Apache can read it. It is safe to put this file in the same directory as the **.htaccess** file because,