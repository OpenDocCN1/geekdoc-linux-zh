The following lines are what should be added to the `qpopper.conf` file:

```
set tls-support = st1s
set tls-server-cert-file = /etc/mail/certs/cert.pem
```

If you want, you can emulate a Certifying Authority yourself to create a self-signed certificate that you can use to make sure the system works. However, SSL-enabled clients won’t trust this certificate and will require the user to manually approve it before continuing.

First, create the test CA’s private key (making sure to remember the passphrase you enter) and then create the CA certificate:

```
# openssl genrsa -des3 -out ca.key 1024
...
# openssl req -new -x509 -days 365 -key ca.key -out ca.crt
```

Now, you can self-sign the certificate request you created earlier (`req.pem`):

```
# openssl x509 -req -CA ca.crt -CAkey ca.key -days 365 -in req.pem
>-out signed-req.pem -CAcreateserial
```

This should allow you to run an SSL-enabled Qpopper server and test its functionality. Make sure to get the real CA-signed certificate at some point!

# ## For More Information

The official Web site for Qpopper is http://www.eudora.com/qpopper. It has a lot of useful information, including a PDF document (in the Documentation section) that definitively describes all the possible configuration options of Qpopper. It’s written from a Linux viewpoint, so many of the pathnames quoted in the documentation are slightly different from your installation.

Even more information, particularly on the use of configuration files, can be found in the man `qpopper` page.

# # Configuring an IMAP Server with IMAP-UW

The Internet Message Access Protocol (IMAP) is an alternative to POP that some users prefer. You will probably want to support it on your mail server, along with POP and SMTP services, to make the package complete. The fundamental difference between IMAP and POP is that whereas POP downloads each message from the server and stores it in the mail program, IMAP mail is accessed and manipulated wholly on the server.

An IMAP client, like a server-side shell-based mail client, can have multiple mail folders and transfer messages between them as if they are local. Messages are transferred to the client only when requested, and they are not deleted unless the user explicitly deletes