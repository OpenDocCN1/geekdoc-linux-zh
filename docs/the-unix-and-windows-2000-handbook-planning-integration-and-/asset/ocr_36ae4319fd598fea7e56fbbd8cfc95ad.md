```sh
#!/usr/sbin/sendmail -bd -q30m
```

The -bd option causes Sendmail to run as a daemon, and -q30m requires Sendmail to process the pending queue every 30 minutes. Other options include -d for debugging and -v for verbose mode.

Client UNIX workstations (not mail servers) do not require Sendmail running in the background as a daemon. Email from a client workstation is delivered to the mail server immediately. If the mail server is not available, the message will be queued.

# QUEUE

Sendmail will attempt to deliver mail immediately. When immediate delivery is not possible, Sendmail will hold the message and attempt to deliver it at a later time (-q60m option). Queued messages are placed in a holding directory (/var/spool/mqueue) and are referred to as queued. A message is broken into separate files in the queue directory. Each filename begins with a single character identifier (Table 9.4), followed by the letter F, and then a unique identifier for each separate message. Sendmail accepts a command-line option to process the queue. In the example in the “Starting Sendmail” section, we used -q30m. This option instructs Sendmail to attempt delivery of all messages in the queue every 30 minutes.

Email queued on client UNIX workstations must also be processed. Queued email on a client is the result of the client not being able to contact the mail server. Since the client is not running the Sendmail daemon, another method of processing the queue must be utilized. On the client UNIX workstation, add the following line to root’s crontab:

```
0 * * * * /usr/sbin/sendmail -q
```

This command ensures that the mail queue is processed every hour and that queued email will be delivered to the mail server when it is available.

The mailq command (/usr/sbin/sendmail -bp) prints out a summary of the mail queue. An example of its output is provided here:

```
Mail Queue (2 requests)
--Q-ID--  --Size--  --Q-Time--  --Sender/Recipient---------
0AA14869     843 Tue Dec 28 14:57 <webb@sniglets.com>
                 (Deferred: Connection timed out with mail.nowhere.net.)
                 george@nowhere.net
0AA14794    1780 Tue Dec 28 14:53 <ox@sniglets.com>
                 (Deferred: Connection timed out with mail.somewhere.com.)
                 user@somewhere.com
```

The first line provides a total number of email messages in the queue. The remaining lines provide information on each message in the queue. The first line for each message contains the identifier (ID), size of the message, date/time the message was placed in the queue, and the sender of the