
## Chapter 11. Email

## Caution

Self-signed certificates should be used for testing purposes only. Any server used in a production environment should use an SSL certificate granted by a CA.

To create a self-signed SSL certificate for IMAP, change to the /usr/share/ssl/certs/ directory and type the following command as root:

```
make imapd.pem
```

Answer all of the questions to complete the process.

To create a self-signed SSL certificate for POP, change to the /usr/share/ssl/certs/ directory, and type the following command as root:

```
make ipop3d.pem
```

Again, answer all of the questions to complete the process.
Once finished, use the /sbin/service command to start the appropriate daemon (imaps or pop3s). Then, set the imaps or the pop3 service to start at the proper runlevels using an initscript utility, such as Services Configuration Tool (redhat-config-services) wrapper enabled. Refer to Section 1.4.2 Runlevel Utilities for more about initscripts.

Alternatively, the stunnel command can be used as an SSL encryption around the standard, non-secure daemon, imapd or pop3d.
The stunnel program uses OpenSSL libraries included with Red Hat Linux to provide strong cryptography and protect the connections. It is best to apply to a Certificate Authority (CA) for an SSL certificate, but it is also possible to create a self-signed certificate.

To create a self-signed SSL certificate, change to the /usr/share/ssl/certs/ directory, and type the following command:

```
make stunnel.pem
```

Again, answer all of the questions to complete the process.
Once the certificate is generated, it is possible to use the stunnel command to start the imapd mail daemon using:

```
/usr/sbin/stunnel -d 993 -l /usr/sbin/imapd imapd
```

Once this command is issued, it is possible to open an IMAP email client and connect to the email server using SSL encryption.
To start the pop3 using the stunnel command, type the following command:

```
/usr/sbin/stunnel -d 993 -l /usr/sbin/pop3d pop3d
```

For more information about how to use stunnel, read the stunnel man page or refer to the documents in the /usr/share/doc/stunnel-<version-number>/directory.

## 11.6. Additional Resources

The following is a list of additional documentation about email applications.

## Chapter 11. Email

## 11.6.1. Installed Documentation

Information on configuring Sendmail is included with the sendmail sendmail-cf packages.

- /usr/share/doc/sendmail/README.cf Contains information on m4, file locations for Sendmail, supported mailers, how to access enhanced features, and more.
- /usr/share/doc/sendmail/README Contains information on the Sendmail directory structure, IDent protocol support, details on directory permissions, and the common problems these permissions can cause if misconfigured.

In addition, the sendmail and aliases pages contain helpful information covering Sendmail options and the proper configuration of the Sendmail /etc/mail/aliases file.

- /usr/share/doc/fetchmail-<version-number> Contains a full list of Fetchmail features in the FEATURES file and an introductory FAQ document.
- /usr/share/doc/procmail-<version-number> Contains a README file that provides an overview of Procmail, a FEATURES file that explores every program feature, and an FAQ file with answers to many common questions.

When learning how Procmail works and creating new recipes, the following Procmail pages are invaluable:

- procmail Provides an overview of how Procmail works and the steps involved with filtering email.
- procmailrc Explains the rc file format used to construct recipes.
- procmailex Gives some useful, real-world examples of Procmail recipes.
- procmailsc Explains the weighted scoring technique used by Procmail to see if a particular recipe matches a certain score.

- /usr/share/doc/spamassassin-<version-number>/ This directory contains a large amount of information pertaining to SpamAssassin. Replace <version-number> with the version number of the spamassassin package.

## 11.6.2. Useful Websites

- http://www.redhat.com/mirrors/HOWTO/Mail-Administrator-HOWTO.html Provides an overview of how email works, and examines email solutions and configurations on the client and server sides.
- http://www.redhat.com/mirrors/HOWTO/Mail-User-HOWTO/ Looks at email from the user's perspective, investigates various popular email client applications and gives an introduction to topics such as aliases, forwarding, auto-replying, mail lists, and spam.
- http://www.redhat.com/mirrors/HOWTO/mini/Secure-POP+SSH.html Demonstrates how to retrieve POP using SSH with port forwarding, to that the emails and messages are transferred securely.
- http://www.sendmail.net/ Contains news, interviews, and articles concerning Sendmail, including an expanded breakdown of the many options available.
- http://www.sendmail.org/ Offers a thorough technical breakdown of Sendmail features and configuration examples.
- http://tuxedo.org/esr/fetchmail The home page for Fetchmail, featuring an online manual, and a thorough FAQ.

http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with links to demaill
http://www.procmail.org/ — The home page for Procmail with with to demaill


## Chapter 12. Berkeley Internet Domain (BIND)

On the Internet, the FQDN of a host can be broken down into different sections. These sections are organized into a hierarchy like a tree, with a main trunk, primary branches, secondary branches, and so forth. Consider the following FQDN:

```
bob.sales.example.com
```

When looking at how a FQDN is resolved to find the IP address that relates to a particular system, read the name from right to left, with each level of the hierarchy divided by periods (.). In this example,
