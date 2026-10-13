by Makefile and the integrated nature of the resource configuration files in /etc. To start the Sendmail server, simply go into /etc/mail and enter make start:

```
# make start
( ./etc/defaults/rc.conf; source_rc_confs; if [
'$ {sendmail_enable}' = 'YES' -a -r /etc/mail/sendmail.cf ];
then /usr/sbin/sendmail ${sendmail_flags}; fi )
```

Because this command echoes its actions, you can see that it pulls in relevant configuration details from the systemwide resource configuration files—in which flags such as -q30m (do a queue run every thirty minutes) and -bd (run as a background daemon) are centrally specified. It will even refuse to start the process if the sendmail_enable variable in the rc.conf files is set to NO.

Restarting or stopping the master process is equally simple:

```
# make restart
/bin/kill -HUP `head -1 /var/run/sendmail.pid`
# make stop
/bin/kill -TERM `head -1 /var/run/sendmail.pid`
```

You can see what state each Sendmail process is in by using ps in wide mode in conjunction with grep; each process reports its position in the queue as an argument against its name in the process table. The following example shows the master process (51248) and a process in the middle of a queue run (54150):

```
51248 ?? Ss 0:00.17 sendmail: accepting connections (sendmail)
54150 ?? I 0:00.02 sendmail: /f4Q6KWV16827
@mail.backstreetboys.com.: user open (sendmail)
```

# The Message Queue

Messages waiting to be sent by Sendmail sit in /var/spool/mqueue. In Sendmail's default configuration, a new sendmail -q process is started every 30 minutes, stepping through each queued message and attempting to deliver it to its destination. This continues for five days: At the end of which, an undeliverable message is returned to the sender with the relevant error headers attached.

If you have some messages in your queue, which you almost certainly will if you've been using the system for any length of time, you can browse through them at will. Unlike opaque systems such as Microsoft Exchange in which queue files are kept in a database without an easy way to tweak or even see the files waiting to be sent, Sendmail provides both. Queued messages are just plain-text files, capable of being read and edited by regular text editors. This gives the administrator great control over how the mail system operates; however, it also provides an opportunity for the administrator to abuse his