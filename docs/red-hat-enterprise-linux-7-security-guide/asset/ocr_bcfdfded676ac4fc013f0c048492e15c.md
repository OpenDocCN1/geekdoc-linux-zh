the root user).

# 4.3.10.4. Disable Postfix Network Listening

By default, Postfix is set up to only listen to the local loopback address. You can verify this by viewing the file /etc/postfix/main.cf.

View the file /etc/postfix/main.cf to ensure that only the following inet_interfaces line appears:

```
inet_interfaces = localhost
```

This ensures that Postfix only accepts mail messages (such as cron job reports) from the local system and not from the network. This is the default setting and protects Postfix from a network attack.

For removal of the localhost restriction and allowing Postfix to listen on all interfaces the inet_interfaces = all setting can be used.

# 4.3.10.5. Configuring Postfix to Use SASL

The Red Hat Enterprise Linux 7 version of Postfix can use the Dovecot or Cyrus SASL implementations for SMTP Authentication (or SMTP AUTH). SMTP Authentication is an extension of the Simple Mail Transfer Protocol. When enabled, SMTP clients are required to authenticate to the SMTP server using an authentication method supported and accepted by both the server and the client. This section describes how to configure Postfix to make use of the Dovecot SASL implementation.

To install the Dovecot POP/IMAP server, and thus make the Dovecot SASL implementation available on your system, issue the following command as the root user:

```
[~]# yum install dovecot
```

The Postfix SMTP server can communicate with the Dovecot SASL implementation using either a UNIX-domain socket or a TCP socket. The latter method is only needed in case the Postfix and Dovecot applications are running on separate machines. This guide gives preference to the UNIX-domain socket method, which affords better privacy.

In order to instruct Postfix to use the Dovecot SASL implementation, a number of configuration changes need to be performed for both applications. Follow the procedures below to effect these changes.

# Setting Up Dovecot

+   1. Modify the main Dovecot configuration file, /etc/dovecot/conf.d/10-master.conf, to include the following lines (the default configuration file already includes most of the relevant section, and the lines just need to be uncommented):

```
service auth {
unix_listener /var/spool/postfix/private/auth {
mode = 0660
user = postfix
group = postfix
}
}
```