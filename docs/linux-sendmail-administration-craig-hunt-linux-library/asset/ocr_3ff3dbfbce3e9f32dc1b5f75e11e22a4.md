# In Sum 319

!robert@bobsnet.org
:0 A
crabook

This recipe searches for mail that is from someone named mikel and that has a subject of TCP/IP. A carbon copy is made of the mail and is mailed to robert@bobsnet.org. The other copy of the mail is stored in the crabook mailbox.

The fourth recipe is:

```
:0
* ^From.*@wespamu
/dev/null
```

This recipe shows how spam is deleted using procmail. All mail from wespamu is deleted by sending it to /dev/null—the null device.

The final recipe is:

```
:0 B
* .*pheromones
gawk -f spamscript > spam-suspects
```

This recipe illustrates how mail is passed to an external program for processing. All messages that contain the word “pheromones” anywhere in the message body are passed to awk for processing. In this example, awk runs a program file named spamscript that extracts information from the mail and stores it in a file named spanspects. You can imagine that the administrator of this system created an awk program named spamscript to extract all of the e-mail addresses from suspected spam.

This range of recipes illustrates the power and flexibility of procmail. Despite the obscure syntax of a procmailrc file, it may be the best tool for filtering e-mail.

The Sendmail feature local_procmail makes it easy to pass inbound mail through procmail for filtering. Some Linux vendors—Red Hat is an example—make the local_procmail feature a part of their default Sendmail configuration. In the fight against spam, you’ll need all the help you can get. Don't overlook procmail as an effective tool for mail filtering.

![](bbox=[0.943, 0.563, 0.981, 0.693])

# In Sum

Spam e-mail is an annoyance to your users who clog their mailboxes with trash that must be waded through and discarded. As a Sendmail administrator, you must part to

Maintaining a Healthy ServernPART 4