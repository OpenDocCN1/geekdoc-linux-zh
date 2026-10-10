
# Sending and Receiving Mail: mail Command

The `mail` command is interactive and is used to both send and receive mail messages.

## To Send Mail

To send a message to another user on the same system, the format is

```
$ mail username<Enter>
```

To send a message to more than one user on the same system, enter all user names after the `mail` command, separating each by one space:

```
$ mail username1 username2<Enter>
```

To send a message to a user on another system, type the username followed by @ and the name of the system:

```
$ mail username@hostname<Enter>
```

To send a message to more than one user on another system, separate each `username@hostname` entry by one space.

Example 3.11 shows how one user can send mail to another user on the same system (that is, on the same host) and to one on a different system. Notice that whenever the `mail` command is invoked, the system responds with a `Subject:` prompt. Type a description line that will appear in the receiver's list of incoming mail, and then press Enter again. Now you can type whatever you want to communicate to the receiver.

When you have finished your message, press Enter and then press the combination Ctrl-D. The system responds with a `Cc:` prompt. If you want to send copies of the message to others, type their usernames. When you are finished, press Ctrl-D again. The system sends the message and responds with a shell prompt (usually $ and a cursor).

**Example 3.11 Sending Mail with the mail Command**

Knowing that Sancho is on the system today, Don Quixote sends a message to him:

```
$ mail panzasan<Enter>
Subject: Meeting at El Toboso<Enter>
Sancho! Don't forget the meeting tonight at Lady Dulcinéa's!
Signed, Quixote de La Mancha
<Ctrl>-d
Cc: <Enter>
```

What if our noble knight Quixote wishes to send a message to a user on another system? Knowing that Dulcinéa is working at her home office in El Toboso, here's what he might enter:

```
$ mail dulcineae@eltoboso<Enter>
Subject: Meeting Still OK, My Lady?<Enter>
Is it still OK for you me (your devoted knight-Errant), my squire, and our comadres to meet with you tonight at our casa in El Toboso? We wish to discuss our plans for future noble exploits.
I have already taken the liberty to inform Sancho, Nicholas the Barber and Peréz the Curate. I will inform the others after I receive your blessing.
Signed, Quixote de La Mancha
<Ctrl>-d
Cc: <Enter>
```

## To Receive Mail

Whenever you log in, the system lets you know whether you have mail messages waiting in the `username` file (where `username` refers to your username) in the `/var/spool/mail/` directory.

The "You have mail" notification and the mail messages themselves are not displayed simultaneously when a new message arrives. System administrators can customize the shell (in other words, the system) to check on all mailbox files periodically; for example, once every 600 seconds. If the shell detects a new message in a user's `/var/spool/mail/username` file, it then displays the "You have mail" notification. System administrators can customize other aspects of this mail notification, as well. That said, to view new messages, the format is simply

```
$ mail<Enter>
```

The `mail` program responds with a listing of the new messages in the file. Note that once you invoke the `mail` program, it has its own specific prompt (`&`), which tells you that it is now running. Let's use an example to explore `mail` a little more.

# Example 3.12 Receiving mail with mail

![](img/cae5c706c216875d12d4b7d28144cc71_95_0.png)

Figure 3.1 Receiving, reading and storing mail.

Sancho is working on tty6 when he receives the following system message:

You have mail in /var/spool/mail/panzasan.

Note that here, the username file is panzasan.

Sancho's system is configured to check for mail every 10 minutes. It has apparently done so and has given him the new mail notification. To check the mail, Sancho enters

```
$ mail<Enter>
Mail version 8.1.6/6/93 Type ? for help
"/var/spool/mail/panzasan" 2 messages 1 new
U 1 quixote@hostname.local Tue Jul 17 10:50 10/267 "Meeting at El
Toboso"
N 2 nicholas@hostname.local Tue Jul 17 11:05 16/311 "Meeting Postponed?"
&
```

Note the U and N designations at the beginning of each listed message in Example 3.12. U means unread (a holdover message from a previous time when the user viewed his or her mail but did not read that particular message). The N designation means new.

When presented with the & prompt, Sancho knows that he can immediately check his unread messages simply by pressing Enter. He does so to read the first message, which he had not read the last time he checked his mail.

```
&<Enter>
Message 1:
From quixoted Tue Jul 17 10:15:47 2001
Date: Tue Jul 17 2001 10:15:47 -600
To: panzasan@hostname.localdomain
Subject: Meeting at El Toboso<Enter>
Sancho! Don't forget the meeting tonight at Lady Dulcinéa's!
Signed, Quixote de La Mancha
```

Sancho then reads the new message 2 by typing:

```
& 2<Enter>
```

(Because he had already finished reading message 1, he could have just pressed Enter here, too.)

```
Message 2:
From nicholas Tue Jul 17 10:50:32 2001
Date: Tue, Jul 17 2001 10:50:32 -600
From: nicholass@hostname.localdomain
To: panzasan@hostname.localdomain
Subject: Meeting Postponed?
Sancho, Perez just dropped by my office. Please call us regarding the status of the meeting Don Quixote scheduled for tonight at Lady Dulcinéa's. The Don told us yesterday that he thought the meeting was a 'go' but that he had not received confirmation from the Lady yet. Is it still on? Meanwhile, are you keeping a close watch over him? We don't need another 'windmill' episode.

Nicholas and Perez
```

Here are few subcommand options---also called subcommands because they invoke their own functionality---for reading mail:

- To read the first message in the listing, press Enter or type 1 and then press Enter.
- To skip the first message and read the second message, type 2 and press Enter.
- To read the first new message in any listing, type t and press Enter.
- To read the messages in sequence, simply press Enter after starting at your chosen first message. Then, press Enter after reading each message in turn.

You can also type the following letters (among others) at the & prompt while reviewing your messages:

| Command | Description |
| :--- | :--- |
| f | lists the headlines of messages in the mailbox |
| d | deletes messages |
| m | forwards messages |
| r | sends a reply |
| q | exits mail and leaves unread messages in the queue |
| s | appends a message to a file |

To obtain a full list of available subcommands to use while in mail, type ? at the & prompt.

Now, what if Sancho wanted to check messages that he has received and read in the past? The `mail -f` command displays a list of messages in his personal mailbox (that is, in the `/home/panzasan/mbox` file). Normally, when he quits the mail program, undelivered (but already read) messages are written back to that `mbox` file and not back to the (incoming) `/var/spool/mail/panzasan` file from which all the new messages came. By starting the `mail -f` aspect of mail, he can review and deal with these messages in the same way he dealt with the new or unread messages in `/var/spool/mail/panzasan` by using `mail`. Figure 3.1 illustrates a typical mail reception and storage process.

# Sending Messages to the Screen: write and wall Commands

Both of the commands discussed in this section provide the capability to contact other users on the system:

- **write** enables you to contact one or more specific users
- **wall** enables you to contact all users on the system

Let's discuss each in turn.

### The write Command

The mail command showed us how to send messages to others' mailboxes and how to receive and manipulate messages in our mailbox. By contrast, the **write** command displays a message immediately on the specified user's screen. You can send messages to a user on the local system or on another system on the network (simply replace **username** with **username@hostname**). If, by using `who` or `finger`, you determine that your target user is logged in on more than one terminal, you can display your message on all the terminals unless you just want to specify the terminal(s) to which you want your message to be sent, as follows:

```
$ write username ttyname/number<Enter>
```

Otherwise, to reach the target user on any and all terminals, the syntax is just the following:

```
$ write username<Enter>
```

For a specific user to receive the message, however, he or she must be logged in at the time and must not have refused permission for the message to appear on his or her terminal. By default, Linux does not turn off the **write** permission; that task is accomplished by the user with the **msg** command (covered later in this chapter).
