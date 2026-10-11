```
Organization Name (eg, company) [Internet Widgets Pty Ltd]:**Ramons****$**
  **Pile O Bits**
 Organization Unit Name (eg, section) []:
 Common Name (eg, your name or your server's hostname) []:**redhat.hontanon.com**
 Email Address []:**rhontanonn@sybex.com**
```

Note that the make testcert command also invokes the openssl utility to create a new certificate and sign it with the private RSA key you created in Listing 7.7. The -days 365 option specifies that you want to create a certificate that will be valid for a year. You need to supply the passphrase that you supplied when the key was generated so you can decode it and use it to sign the newly created certificate. You also have to supply the following information to go into the X.509 certificate:

+   * Country name
+   * State or province name
+   * Locality name
+   * Organization name
+   * Common name
+   * E-mail address

These are the attributes that will be associated with your server's X.509 certificate and that will be visible from Web browsers when they connect to your site.

You have now successfully created a new server private key, along with a new certificate. Since Apache caches the certificate when it starts up, you need to restart the Apache daemon for the change to take effect, as shown in Listing 7.9.

# Listing 7.9  Restarting the Apache server with the new certificate

```
[ramon]$ sudo /etc/rc.d/init.d/httpd restart
   Shutting down httpd: [  OK  ]
   Starting httpd: [  OK  ]
```

The first time a Web browser contacts the Apache HTTPS server, the user is prompted with a dialog box, asking them to verify the authenticity of the certificate, since it is self-signed and not signed by any well-known certification authority.

Figure 7.5 shows the dialog box displayed by Netscape Navigator whenever a site sends a digital certificate for the first time. Instruct your users to click the More Info button and verify that the fingerprint shown corresponds with the one from your certificate (Figure 7.6). A certificate's fingerprint is a unique summary of the certificate's contents, in a format that can be easily compared visually to a trusted reference. If your customers are concerned about the validity of the certificate, they can validate the fingerprint with you via