# POP AND IMAP Servers

This set-GID technique will limit the damage that someone could do to reading, altering or removing everyone's mail. Those using PGP would be at risk only for it being removed. The IMAP server is very similar to POP but is separate code so it will have different buffer overflow vulnerabilities.

POP3 and IMAP supports TCP Wrappers via libwrap. Unless employees need to download e-mail from the office, either TCP Wrappers or IP Chains should be used to block access to your server from outside your organization.

To enable SSL-wrapped IMAP and POP3 on a Linux server, follow these steps:

+   1. Add the services to /etc/services if not already present:

```
imaps 993/tcp
pop3s 995/tcp
```

+   2. Creating the two files in the /etc/xinetd.d directory owned by root with either mode 644 or 600 (xinetd-based systems).

```
imaps:
# The IMAP service allows remote users to access their
# mail using an IMAP client with SSL support such as
# Netscape Communicator or fetchmail.
terservice imaps
{
  socket_type      = stream
  wait            = no
  user            = root
  server          = /usr/sbin/imapsd
  log_on_success  = DURATION USERID
  log_on_failure += USERID
  disable         = no
}
```

pop3s:

```
# The POP3s service allows remote users to access their
# mail using an POP3 client with SSL support such as
# fetchmail.
service pop3s
{
  socket_type      = stream
  wait            = no
  user            = root
  server          = /usr/sbin/ipop3sd
  log_on_success  = USERID
  log_on_failure += USERID
  disable         = no
}
```