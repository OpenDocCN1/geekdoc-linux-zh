
nispasswd nispasswd (1) - change NIS+ password information
nispasswd nispasswdd (1m) - NIS+ password update daemon
nispasswd passwd (1) - change login password and password attributes
nispasswd passwd (4) - password file
nispasswd pwcopy (1m) - installs and updates /etc/shadow
nispasswd with information from /etc/passwd

rpc.nispasswd rpc.nispasswd (1m) - NIS+ password update daemon
rpc.yppasswd rpc.yppasswd (1m) - server for modifying NIS password file
yppasswd yppasswd (1) - change your network password in the NIS database
yppasswd rpc.yppassdd (1m) - server for modifying NIS password file

This command produces a long list of "man" pages from a database, including sections 1 and 4 for passwd that our find command produced. In order to use the "-k" option, a "man" page database must have been produced by your system administrator by issuing the catman command.

I am obviously a big advocate of using "man" pages, because I included many "man" pages at the end of chapters throughout the book. Anytime you see the "man" page icon, there is a "man" page for the command in the chapter number referenced in the icon. Although the "man" page for your UNIX variant may be different from the one appearing in the book, the commands on most UNIX variants are similar, and the "man" pages act as an excellent reference.

## Electronic Mail

All UNIX variants come with electronic mail programs. You can use one of the electronic mail programs on your system to send and receive electronic mail from other users on the system. You can also communicate with users on other systems and across the internet if your system administrator has set up this capability. In this chapter, we'll cover the basics of sending and receiving electronic mail. I cover this very early in the book because you may receive a message after your first login indicating that you have received mail messages and you'll want to read them. You may receive a welcome message or a request to change your password immediately after your first login.

The most basic electronic mail program, and one that exists on every UNIX variant on which I have worked, is mail. This is a very easy program to use that requires very little explanation. In the following example, I invoke the mail program, issue "?" to print a list of mail commands, read a message from Tom, reply to his message, and save the original message:

![](img/75f39fc91296b889c0653851accdfd46_58_0.png)

![](img/75f39fc91296b889c0653851accdfd46_58_1.png)

```text
* Welcome to sys1

Last unsuccessful login: Mon Mar  8 09:32:13
Last login: Mon Sep 27 07:21:01



**********************************************************************
* This is a private system operated for use by our company only.    *
**********************************************************************

* Welcome to sys1

You have mail.

TERM set to vt100
sys1:/home/martyp
martyp $ mail
Mail [5.2 UCB] Type ? for help.
/var/spool/mail/martyp": 1 message 1 new
>N  1 tomf      Mon Sep 27 07:23  11/392  "12:00 Phone Call"
? ?
Control Commands:
 q               Quit - apply mailbox commands entered this session.
 x               Quit - restore mailbox to original state.
 ! <cmd>         Start a shell, run <cmd>, and return to mailbox.
 cd [<dir>]      Change directory to <dir> or $HOME.
Display Commands:
 t [<msg_list>]  Display messages in <msg_list> or current message.
 n               Display next message.
 f [<msg_list>]  Display headings of messages.
 h [<num>]       Display headings of group containing message <num>.
Message Handling:
 e [<num>]       Edit message <num> (default editor is ex).
 d [<msg_list>]  Delete messages in <msg_list> or current message.
 u [<msg_list>]  Recall deleted messages.
 s [<msg_list>] <file>                 Append messages (with headings) to <file>.
 w [<msg_list>] <file>                 Append messages (text only) to <file>.
 pre [<msg_list>]     Keep messages in system mailbox.
Creating New Mail:
 m <addrlist>      Create/send new message to addresses in <addrlist>.
 r [<msg_list>]    Send reply to sender and recipients of messages.
 R [<msg_list>]    Send reply only to senders of messages.
 a                 Display list of aliases and their addresses.
==================================================================== Mailbox Commands =====================================================================
? t
Message  1:
From tomf Mon Sep 27 07:23:30
Date: Mon, 27 Sep 1999 07:23:30 -0700
From: <tomf>
To: martyp
Subject: 12:00 Phone Call

Please call me at 12:00 CA time to discuss trip.
Tom
? R
To: tomf
Subject: Re:  12:00 Phone Call

I'll call you then.
Marty
Cc:
? s
"/home/martyp/mbox" [Appended] 11/392
? q
sys1:/home/martyp
martyp $
```

This mail session is typical. We first used mail to invoke the electronic mail program. We are informed that there is one message from tomf with the subject 12:00 Phone Call. We then use ? to get a list of mail commands. I selected this particular system for the mail examples because of the clear help messages that are produced with ?. We then use t to display the message we received, R to reply to tomf the sender of the message, s to save and delete the message, and finally quit with q. A file called mbox has been produced that contains all of the saved messages.

You can see from this example how easily you can handle the messages in your mailbox. It may be, however, that you wish to view summary information of the messages you have saved and deleted. The file mbox in my home directory was created to store messages that were saved and then deleted. We can view summary information of these messages using the option "-f" and mbox as an input file as shown in the following example:

```text
martyp $ mail -f mbox
Mail [5.2 UCB] Type ? for help.
"mbox": 4 messages
 1 tomf             Sun Sep 26 18:14   11/343   "Training"
>2 donnak           Mon Sep 27  07:23   12/402   "Performance"
 3 carollync        Mon Sep 27  07:27   12/380   "Software Update"
 4 tomf             Mon Sep 27  07:38   11/357   "12:00 Phone Call"
```

You can see in this example that there were four messages saved in mbox that we can work with simply by specifying the number of the file (1-4). The current message is indicated by the right arrow >. Information is available on the date and time of delivery of the message, the size of the message in lines and characters, and the subject of the message. Saving and deleting files with s ensures that a copy of the file is maintained so that you can later access it.

A slightly more advanced electronic mail program is on some systems, called mailx. When run, mailx produces a list of messages for you rather than displaying them one at a time as mail does. The mailx list of messages is similar to the list we just saw with deleted and saved messages using mail -f mbox. With mailx, you get the status of whether or not you have read the messages. You get a single character preceding each message indicating that the message is N for new, O for old messages that have been read, and U for unread messages. On some systems, such as the Red Hat Linux system used for many of the examples in this book, you get the list of messages when you run mail just as you would when you run mailx on other systems. The following example shows what you would see when you run mailx:

```text
martyp $ mailx
Mail [5.2 UCB]  Type ? for help.
"/var/spool/mail/martyp": 2 messages 1 new 2 unread
  U  1 tomf           Mon Sep 29 08:40  13/394 "Networking"
>N  2 donnak          Mon Sep 29 08:49  10/342 "Interoperability"
 ?
```

The first message is U for unread. The second message is N for new. The right arrow is next to the new message.

You are not restricted to saving messages to the default file mbox. You can organize your messages by saving them to different files. The following example shows saving a message to the file trip:

```text
martyp $ mailx
Mail [5.2 UCB] [AIX 4.1]  Type ? for help.
"/var/spool/mail/martyp": 2 messages 2 unread
>U  1 tomf           Mon Sep 27 08:49  11/352 "NY trip"
  U  2 donnak          Wed Sep 29 04:44  11/354 "login change"
 ?
Message  1:
From tomf Mon Sep 27 08:49:09
Date: Mon, 27 Sep 08:49:08 -0700
From: <tomf>
To: martyp
Subject: NY trip

I am going to change the date of the NY trip.
? s trip
"trip" [New file]  11/352
? q
Held 1 message in /var/spool/mail/martyp
martyp $ 
```
