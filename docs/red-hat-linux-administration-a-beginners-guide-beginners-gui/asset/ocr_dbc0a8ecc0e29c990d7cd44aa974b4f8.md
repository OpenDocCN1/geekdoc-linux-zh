Postfix provides a slightly smoother alternative with its **postsuper** tool, and you don't even need to restart the server. The **postsuper** utility provides a number of options for queue management beyond just deleting messages, and you're encouraged to read its documentation. For our purposes here, we're just going to use the **--d** option to remove the offending message.

```
[root@mail /root]# postsuper -d F1B441D01A8
```

# Flushing the Queue

If your site loses connectivity with the rest of the world (for instance, if your Internet connection is down), your MTA will quietly accept messages from your users for future delivery. When Sendmail or Postfix finds that it can once again contact other servers, it will quietly start processing the queue itself.

In most instances, you can leave the server alone and let it work through its queue. Sendmail and Postfix both do a great job of regulating themselves and making sure they process their queue without overwhelming the system or your network connection.

However, there are instances when you need the MTA to hurry up and get through its queue faster. One instance might be if the outage was long enough that it would take your MTA unreasonably long to process the queue at its normal rate, especially given the flood of new e-mails coming into the system. (After all, other sites trying to contact your mail server patiently queued their messages until they could connect. Now they're all delivering!)

In these instances, you need the MTA to churn through its queue much more quickly. To force Sendmail or Postfix to process its queue immediately, use the **sendmail --q** option. For example, to ask Sendmail to process its queue, you would enter

```
[root@mail /root]# sendmail -q
```

With Postfix you can either enter that exact same command, or use the native **postqueue** method. (Either command runs the exact same program.)

```
[root@mail /root]# postqueue -f
```

# Mail Logging

Keeping track of how much mail goes through your system is useful for two reasons: It provides a history of activity on the server, which is good when trying to track down bad behavior on the system (or bad behavior of the users on the system!); and it provides a quantifiable metric for the demands placed on the server. The latter is especially handy when trying to convince those with the spending power that a server needs to be upgraded!

Both Sendmail and Postfix use the **syslog** mechanism for logging its activity. Red Hat comes preconfigured so that any messages sent to **syslog** that are from the mailer are placed