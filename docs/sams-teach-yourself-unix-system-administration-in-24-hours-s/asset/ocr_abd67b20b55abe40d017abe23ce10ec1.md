```
0AA18380 4651 Tue Mar 26 16:39 <lori@salesinminutes.net>
    (Deferred: Connection timed out with delphi.mail.eds.com.)
<mirish@delphi.com>
```

The first line shows the total number of requests in the outbound mail queue—147—and then each request is listed with its queue-ID, size (in bytes), when it entered the queue, a sender/recipient list, and a status, if known.

The first message in the queue, for example, has been queued for about three hours (use date to get the current date and time, then compare it to the timestamp shown), which, given that the system is trying to send mail every 10 minutes, means that it's already tried approximately 18 times to deliver this message and failed.

The message is being sent by xaith to office@iandstudio.com, and the specific error is reply: read error from mail.iandis. This particular error usually indicates that the remote system is out of disk space or otherwise unable to receive mail, though its SMTP daemon is listening and answering queries that come in.

Notice on the second entry that the queue-ID value has a trailing asterisk. This means that there's an active sendmail trying to deliver it right now. If it's delivered successfully, this entry will vanish from the queue. Notice that there's no queue error message, suggesting that this is the first time that the system has tried to deliver this e-mail.

Compare that to the fourth entry, which also has an asterisk indicating that sendmail is actively trying to deliver it, but because there's an error message (Deferred: Connection refused by fmailh8.real-net.net), you can see that it's been in the queue for at least one delivery cycle.

Actually, the fourth entry is the most interesting because it's from MAILER-DAEMON. This tells us that a message came into our system for a specific user from send@mailh8.real-net.net, and it then bounced locally. The bounced message (which automatically has MAILER-DAEMON as the sender) is queued to go back to the sender, but the MX record for real-net.net is fmailh8, which isn't accepting connections.

> A cockeyed setup like the fourth entry strongly suggests a spam message to me: It's coming from one mail server, from a generic address (user send?), and the responding MX record for the sender domain is rejecting connections. Hmmm....