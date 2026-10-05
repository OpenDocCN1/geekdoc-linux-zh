# Listing 10.6 Running mailq in Verbose Mode

```
[root]# mailq -v
/var/spool/mqueue (4 requests)
---Q-ID-------Size-------Q-Time-------Sender/Recipient---
aE1FNdp00879 10 480000 Nov 1 07:23 jill
(Warning: could not send message for past 4 hours)
craig.ani.foobirds.org
aE1DVq00821 108 570026+ Nov 1 10:13 kathy
(Deferred: goat.mailq.org.: Network is unreachable)
jay@goat.mailq.org
aE1EC3P00796 112 660032+ Nov 1 09:12 kathy
(Deferred: goat.mailq.org.: Network is unreachable)
jay@goat.mailq.org
a1Cej500742 190 750033+ Nov 1 07:40 craig
(Deferred: goat.mailq.org.: Network is unreachable)
sara@goat.mailq.org
```

Beyond that the users who sent these messages have received warning messages, the verbose output adds little of interest for a system administrator. The numeric priority that Sendmail has assigned to each message is meaningless. Sendmail calculated the value correctly, and if it hadn't you wouldn't know. Furthermore, you have no reason to fiddle with these priorities. If you want to move something out of the queue, you don't do it by messing with the priorities; you do it by manually running a queue process and selecting the message to be delivered.

# Manually Running the Queue

As we saw in Chapter 3, the queue is normally processed periodically, and the interval between queue runs is configured as part of the basic Sendmail setup, using the -q command line. In Chapter 3, we saw configurations with -q set to 1h and 15m for a 1-hour queue run or a 15-minute queue run, respectively. Setting a queue interval at boot time and letting Sendmail handle it automatically is how is normally done. By using the information you learn about the queue from the mailq command, you can manually, select, the queue if necessary.

Manually processing the queue is as simple as entering the command sendmail -q. This causes Sendmail to immediately process everything in the queue. To watch the progress of the queue, add -v to the sendmail command line. Of course, you may not want to process everything in the queue. Using the information gained from the mailq report, you can select individual messages or groups of messages using the queue ID, the sender address, or the recipient address as arguments to the -q option on the sendmail command line. Listing 10.7 is an example of using mailq to validate arguments for the sendmail