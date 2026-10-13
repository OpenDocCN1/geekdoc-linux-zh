+   2. Change the group ownership of the directory:
+      ```
+      # chgrp daemon /var/spool/mqueue
+      ```
+   3. Change file permissions of the directory:
+      ```
+      # chmod 700 /var/spool/mqueue
+      ```
+   4. Restart sendmail:
+      ```
+      # /etc/rc.d/init.d/sendmail start
+      ```

# FORCING DELIVERY OF THE OLD QUEUE

You can forcibly process the old mail queue by running sendmail with the following flags:

```
```bash
# /usr/sbin/sendmail -odq /var/spool/mqueue.old -q -v
```
```

The -q0 flag specifies an alternate queue directory and the -q flag says to just run every job in the queue. The -v flag says to run in verbose mode so that you can monitor the progress of the queue processing. You can drop the -v flag if you want the queue to be processed silently without displaying progress information. After the old queue is emptied, you should remove the old queue directory:

```
```bash
# rmdir /var/spool/mqueue.old
```
```

# DETERMINING THE VERSION OF SENDMAIL

There are two ways of determining what version of sendmail you are running.

+   - Telnet to port 25 of the host running sendmail:
+   - In this example version 8.9.3 of sendmail is being used.
+   - Use the debug flag of sendmail, which forces display of the version number along with the domain name and the results of an address test:

```
```text
$ telnet somehost 25
Trying IP address 10.20.30.40
Connected to somehost
Escape character is '^]'.
220 somehost ESMTP Sendmail 8.9.3/8.9.3; Mon, 2 Aug 1999 11:39:34 -0700

telnet> q
```
```

```
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
```