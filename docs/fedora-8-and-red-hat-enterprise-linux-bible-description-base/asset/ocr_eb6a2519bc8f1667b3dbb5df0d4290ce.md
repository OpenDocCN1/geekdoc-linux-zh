*in.telnetd* daemon to present the telnet login prompt. Once it is on, only users with real logins to the computer can log in to the computer — anonymous users are not supported. Users who log in using telnet are presented with a shell interface for accessing the computer.

Fedora and RHEL also include login daemons that provide Kerberos 5 support. Kerberos 5 provides a higher level of security that is available with other login servers. Kerberos 5-enabled login servers include KLogin (Kerberos 5) and EKLogin (Kerberos 5 with encryption).

The rlogin service has been available for UNIX systems for a long time, though it is generally less secure than the other login services described here. The rlogin service is off by default on your Fedora or RHEL system.

A newer addition to the login servers available with Fedora and RHEL is the OpenSSH server. This service is on by default. To access this service, use applications that come with the openssh-client software package, such as the *ssh*, *sftp*, and *slogin* remote login commands. Many Linux administrators use OpenSSH tools, as opposed to older remote login tools such as *rlogin* and *telnet*. OpenSSH is more secure because it encrypts network traffic to protect passwords and data from being sniffed (while *telnet* and *rlogin* send data in clear text).

> CAUTION: Not only is the SSH service on by default, but unlike other login services, it will allow root login over the network. If you are uncomfortable with that, you should change the PermitRootLogin yes line in the /etc/ssh/sshd_config file as follows:
>     PermitRootLogin no

# ## E-mail servers

The most common protocols used to download e-mail from a mail server to a client workstation are Post Office Protocol (POP3) and Internet Message Access Protocol (IMAPv4). If you configure Fedora or RHEL as your mail server, you can configure the device package to provide POP and IMAP services.

Dovecot is an IMAP/POP3 mail server that works with both maildir and mbox formats. You use IMAP or POP3 if your users get their mail from their own desktops instead of by running their mail clients on the mail server. By default, all POP or IMAP services are off. Choose the POP or IMAP server you would like to use from those provided in the e-mail reader servers listing in Table B-1.

The default mail-transfer agent that comes with Fedora and RHEL is called sendmail. If sendmail software is installed, the sendmail service is started automatically. However, you must configure various files in the /etc/mail directory for the service to work beyond the localhost.

Postfix is an alternative to sendmail, as is the exim mail transport agent. Using the alternatives feature (described earlier in this appendix and in Chapter 10), you can easily make any of