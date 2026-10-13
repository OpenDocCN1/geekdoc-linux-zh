power by looking through pending messages' contents. If you run a system in which you trust your users, be sure that they can trust you too!

The first such tool that comes with Sendmail is called mailq, and it's a way to list the current state of all messages waiting in the queue.

```
# mailq
/var/spool/mqueue (2 requests)
--Q-ID---  --Size--  --Q-Time--  --Sender/Recipient--  -----
f4H1Ahu36976  6246 Wed May 16 18:10  MAILER-DAEMON
    (Deferred: Operation timed out with mlists.acmecity.com.)
    <fred@acmecity.com>

f4GkWw16827  706 Wed May 16 13:58  www
    (host map: lookup (hotmail.com): deferred)
    bob@hotmail.com
```

Using mailq, you can keep an eye on what kind of mail transfer errors frequently occur on your system. If people often forget to specify complete email addresses or misspell common mail server hostnames, you can address that problem through education and tutorials that you send to your users or make publicly available; if you're getting a lot of hostname lookup errors, it might point to a configuration problem on your end. It's an excellent diagnostic tool.

The queue also gives you the ability to fix mistakes in messages on the way out. Let's say, for instance, that you had an entry like the second one in the mailq output shown earlier. The erroneous recipient domain is the result of a simple typo; you can either wait five days for Sendmail to give up trying to find hotamil.com and send it back to you as an error, or you can fix this problem right in the queue.

To do this, go into /var/spool/mqueue and look for the files matching the ID of the entry in the mailq output. These would be the files qf f4GkWw16827 and df f4GkWw16827; the first contains the message body, and the second contains the message headers in an interim format. Simply open up the file with the headers (qf f4GkWw16827) in a text editor, replace all occurrences of hotamil.com with hotmail.com, save the file, and wait for the next queue run. The message will go through cleanly this time.

If you can't wait that long, force a queue run by running sendmail -q -v. This gives you the added bonus of a look into exactly how Sendmail does its SMTP transactions with all the remote systems; with each message it processes, it will echo to the session all the output from the transaction, just as in our example at the beginning of the chapter. You'll get to see all the interesting greeting messages that various administrators program into their MTAs, visible only to other MTAs, and therefore often quite creative and silly. You can use Ctrl+C to exit at any time—messages are removed from the queue only after they've been successfully transferred.