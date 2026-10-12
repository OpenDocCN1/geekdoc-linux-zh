Now tell the server your password, using the **pass** command:

![](bbox=[0.13, 0.15, 0.25, 0.23])

> The system will echo back your password, so don’t do this if you have people looking over your shoulder!

*pass yourpassword*

where *yourpassword* is your password. The server responds with

+OK Mailbox open, X messages

where *X* represents the number of messages in your mailbox. You’re now logged in and can issue commands to read your mail.

Begin by listing the messages that are waiting, using the **list** command. Type

*list*

and the server will list all the messages in your mailbox. The first column represents the message number, and the second column represents the size of the message. The response for my mailbox currently looks like this:

```
+OK Mailbox scan listing follows
1 644
2 2303
3 2334
4 1599
5 2558
.
```

Now let’s try to actually read a message, using the **retr** command. The only parameter that **retr** needs is the message number to read. We’ll start simple: To read message 1, type

*retr 1*

The server responds with something like this:

```
+OK 644 octets
Return-Path: <michael@domain.com>
Delivered-To: michael@redbox.domain.com
Received: by redbox.domain.com (Postfix) with ESMTP id 2010D1ED3A
   for <michael@domain.com>; Mon, 28 Oct 2002 22:32:38 -0700
```