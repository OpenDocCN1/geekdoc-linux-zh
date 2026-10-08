After we invoked **mailx**, a "Return" caused the first message to be read.

The file **trip** was created when this message was saved with **s trip**, and now we can store all related messages in the file **trip**.

Messages saved to a file can be printed with the **lp** command. We'll talk about **lp** later in the book in the system administration chapter; however, at this time it is sufficient to know that files can be printed to the default printer by issuing the command **lp** *filename*. To print the file **trip**, we would issue the command **lp trip**.

Sending electronic mail is just as easy as reading it. The simplest way to send a message is to type **mailx** or **mail** and the *username* of the person to whom you wish to send the message. We'll do just this in the message below to *tomf*:

```
```
martyp $ mail tomf
Subject: Pickup
I'll be at the airport in NY to give you a ride.
Marty
Cc:
martyp $
```
```

A ^D (control D) was used to end the mail message. This message will be in the mailbox of *tomf*. You can send messages using Internet naming if your system has enabled this functionality. The following example shows sending the same message to *tomf* to his Internet electronic mail address:

```
```
martyp $ mail tomf@tomcompany.com
Subject: Pickup
I'll be at the airport in NY to give you a ride.
Marty
Cc:
martyp $
```
```

The ability to send messages to other systems and to Internet addresses requires that your system administrator set up this functionality.