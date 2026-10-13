
These rules can be used to create mail filters. A large percentage of routine mail-related work can be automated by applying such filters.

You can enable procmail as a local mailer for sendmail version 8 in one of two ways:

- As a replacement for the standard local mailer using the m4 configuration directive `FEATURE(local_procmail)`.
- As an additional mailer to the standard local mailer using the m4 configuration directive `FEATURE(procmail)`.

> **Note**
> Users can also install procmail and run it through their `.forward` files so that mail is processed by procmail when it hits their mailboxes. This is less efficient than running procmail as a sendmail local mailer.

More information about procmail can be found at `http://www.procmail.org/` and the latest version can be found at `ftp://ftp.procmail.org/pub/procmail/`.

> **Tip**
> procmail is at the core of a mailing list management package called SmartList. If you are already using procmail, consider SmartList as a possible mailing list system. While SmartList has fewer adherents than Majordomo and Listserv, the most widely used mailing list packages, you may find it preferable and easier to use.

## Troubleshooting

Several problems need to be considered with sendmail systems:

- Problems with `.forward` files
- Knowing when to manually process the mail queue
- Determining the version of sendmail being used
- SMTP connections taking too long
- Relaying denied errors
- Issues dealing with file and directory permissions
- Using wildcard mail exchangers

### Problems with `.forward` Files

When troubleshooting mail delivery problems to a particular user, check whether the user affected has a `.forward` file in their home directory. Often the problem may lie with misconfigured `.forward` files. For users with accounts on two or more machines, it is possible to create a mail loop by using a `.forward` on hostA to forward mail to hostB, and another `.forward` file on hostB to forward mail back to hostA.

### Manually Processing the Mail Queue

Sometimes a host cannot handle a message immediately. For instance, the remote host might be down or too busy, and accordingly is refusing connections. The sending host then saves the message in its mail queue and attempts to deliver it later.

Under normal conditions the mail queue is processed transparently. However, there are times when manual intervention becomes necessary. For example, if a major host is down for a long time the `/var/spool/mqueue` directory may fill up with hundreds or thousands of messages. In general sendmail will recover gracefully when the remote host comes up, but in the meantime performance can become seriously affected by the large size of the queue because sendmail may spend a large amount of time sorting the queue.

If this happens you can rename the current queue to a name such as `mqueue.old`, create a new queue for sendmail to use, and process the old queue manually when the remote host is up again using the following steps:

1. List the contents of the current queue.
2. Rename the current queue.
3. Create a new queue.
4. Force delivery of the old queue.

### Listing Contents of the Current Queue

You can use the `mailq` command to print the contents of the current queue. You can also use the command `mailq -bp` to display a list of the current queue contents.

The listing that is generated will include the queue ID, size, date, sender, and recipients of each message in the queue. Use this information to determine whether the queue is growing too large and you need to manually intervene.

### Renaming the Queue

If you need to manually intervene, use the following steps:

1. Stop sendmail with the following command:

    ```bash
    # /etc/rc.d/init.d/sendmail stop
    ```

2. Rename the queue as follows:

    ```bash
    # mv /var/spool/mqueue /var/spool/mqueue.old
    ```

### Creating a New Queue

To create a new queue, use the following steps:

1. Create a new directory:

    ```bash
    # mkdir /var/spool/mqueue
    ```

2. Change the group ownership of the directory:

    ```bash
    # chgrp daemon /var/spool/mqueue
    ```

3. Change file permissions of the directory:

    ```bash
    # chmod 700 /var/spool/mqueue
    ```

4. Restart sendmail:

    ```bash
    # /etc/rc.d/init.d/sendmail start
    ```

### Forcing Delivery of the Old Queue

You can forcibly process the old mail queue by running sendmail with the following flags:

```bash
# /usr/sbin/sendmail -oQ /var/spool/mqueue.old -q -v
```

The -oQ flag specifies an alternate queue directory and the -q flag says to just run every job in the queue. The -v flag says to run in verbose mode so that you can monitor the progress of the queue processing. You can drop the -v flag if you want the queue to be processed silently without displaying progress information. After the old queue is emptied, you should remove the old queue directory:

```bash
# rmdir /var/spool/mqueue.old
```

### Determining the Version of sendmail

There are two ways of determining what version of sendmail you are running.

- Telnet to port 25 of the host running sendmail. In this example version 8.9.3 of sendmail is being used.

  ```text
  $ telnet somehost 25
  Trying IP address 10.20.30.40
  Connected to somehost
  Escape character is '^]'.
  220 somehost ESMTP Sendmail 8.9.3/8.9.3; Mon, 2 Aug 1999 11:39:34 -0700

  telnet> q
  ```

- Use the debug flag of sendmail, which forces display of the version number along with the domain name and the results of an address test:

  ```text
  $ echo $Z | /usr/sbin/sendmail -bt -d0
  Version 8.9.3
  Compiled with: LOG MATCHGECOS MIME7TO8 MIME8TO7 NAMED_BIND NETINET
                 NETUNIX NEWDB NIS QUEUE SCANF SMTP USERDB
  =========== SYSTEM IDENTITY (after readcf) ===========
     (short domain name) $w = cstlx001
  (canonical domain name) $j = cstlx001.bwc.org
      (subdomain name) $m = bwc.org
           (node name) $k = cstlx001.bwc.org
  =======================================================
  ADDRESS TEST mode (ruleset 5 NOT automatically invoked)
  Enter <ruleset> <address>
  > 8.9.3
  ```

```text
collect: I/O errors on connection
Syslog shows sendmail logging the following errors:
"collect: I/O error on connection"
or
"reply: read error from host.name"
```

Generally, any errors generated using sendmail in this way can be ignored. They usually indicate that sendmail had problems communicating with a remote host at some time and message delivery will be retried.

### Connections to the SMTP Port Taking a Long Time

If you upgrade to sendmail version 8 from an earlier version of sendmail, you may find that SMTP connections can take a long time. On some systems, sendmail version 8 attempts a callback to the connecting host to validate the username. Normally, if the connecting host does not support this service, the connection should quickly fail. However, some types of firewalls and TCP/IP implementations wait for a timeout to occur which leads to the delay in establishing an SMTP connection with your sendmail system.

To fix this problem, disable the use of the IDENT protocol by setting the IDENT timeout to zero. Use the following m4 directive when configuring sendmail:

```text
define(`confTO_IDENT',`0s')dnl
```

If setting the IDENT timeout to zero fails to solve the problem, it may be related to misconfiguration of name servers. Double check your /etc/resolv.conf file and ensure that all name servers listed there are functional. If you control any of the name servers listed in resolv.conf on the sendmail system in question, double-check your root cache file to ensure it is up-to-date as outlined in Chapter 22, “DNS.”

### Relaying Denied Errors

If you receive relaying denied errors from your sendmail system, you need to add a list of fully qualified hostnames or IP addresses of each client allowed to send mail through the sendmail system to the file /etc/mail/relay-domains. Each hostname or IP address should appear on a separate line in the file. After editing the relay-domains file, send a SIGHUP signal to the sendmail daemon:

```text
# kill -HUP `cat /var/run/sendmail.pid`
```

> **Note**
> This problem and the related solution only apply to sendmail version 8.9 and higher.

### File and Directory Permissions for Sendmail Version 8.9 and Higher

For sendmail to run without complaining, you must ensure that the correct file and directory ownership and permissions are set as outlined in the following commands:

```text
# chown root / /etc /etc/mail /usr /var /var/spool /var/spool/mqueue
```
