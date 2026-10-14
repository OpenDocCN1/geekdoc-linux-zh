
keep the mail you've already read in the /var/spool/mail/hermie file, so it moves read mail to a separate file called mbox in your own home directory.

To access the messages in the mbox file, you have to use the command

```
mail -f mbox
```

Kind of annoying, ain't it? But at least the mail program looks and acts the same regardless of which mail file you're working with.

## OTHER MAIL COMMANDS

Let's get back into the mail program and have some fun with the two messages that we didn't read before with this scenario (again, bold type represents your input):

```
mail

Mail version 5.6 6/1/95. Type ? for help.
"/var/spool/mail/hermie": 1 message 1 new
>U 1 D.Rhodes@spam.net Mon Feb 10 15:37 "Make Money Fast!"
U 2 Chris@qwerty.com Mon Feb 10 15:37 "Tennis, Anyone?"
& 2
Message 2:
Date: Mon, 10 Feb 1997 15:37:52 -0500
From: Chris@qwerty.com
To: hermie@fritz.com
Subject: Tennis, Anyone?
Wanna whack a few a 4:30 today? -Chris
& reply
Subject: Re: Tennis, Anyone?
Sure, I'll see you on the lower courts at 4:30.
'D
EOT
& header
U 1 D.Rhodes@spam.net Mon Feb 10 15:37 "Make Money Fast!"
>U 2 Chris@qwerty.com Mon Feb 10 15:37 "Tennis, Anyone?"
& delete 1
& q
Saved 1 message in /home/hermie/mbox
```

We've introduced several new commands here, so let's take a closer look at the five operations that were performed in this mail session:

- As soon as I started the mail program, the mail headers were displayed, showing that both messages are marked U for unread. I displayed message 2 by entering a 2 at the prompt.
- The reply command responded with an appropriate Subject line for message 2, “Subject: Re: Tennis, Anyone?,” and waited for me to enter the text of my message to Chris. Pressing CTRL-D makes EOT appear and sends my reply.
- The header command displays the message headers. I’ve used it here to show the difference in the status flags. The > indicates that message 2 is current, and the message is marked as O for old.
- I deleted the first message with delete 1 without even reading it, since the Subject line was rather dubious.
- And as a parting gesture, the q command told me that another message was squirreled away in that mbox file. At this point, if I issued the mail command again, the system would respond:

```
No mail for hermie
```

Poor hermie. He needn’t drink Draino, though—he can always send himself some more mail. ;)

## THE PINE MAIL SYSTEM

Pine is an email handler that is much friendlier than the plain ol’ mail command. Pine sports a full-screen interface and a context-sensitive list of commands on each screen. Even though it’s text-based (no GUI) it’s very easy to use and has enough features to satisfy almost any user. I personally use Pine in a Unix environment, even though I access the Internet from a Windows machine.

In case you’re wondering why an email system would be named after a tree, here’s the scoop. Pine was originally based on another email program called Elm (short for “ELectronic Mail”), written by Internet pioneer Dave Taylor. The name Pine was first an acronym for “Pine Is Not Elm,” but today the official title is Program for Internet News and Email. (Revisionists: 1, Geeks: 0—film at 11.)

## STARTING PINE

To fire up the Pine program, use the following command, and you'll see the Pine main menu screen:

```
% pine
PINE 4.10 MAIN MENU          Folder: INBOX  3 Messages
? HELP                     - Get help using Pine
C COMPOSE MESSAGE          - Compose and send/post a message
I MESSAGE INDEX            - View messages in current folder
L FOLDER LIST              - Select a folder OR news group to view
A ADDRESS BOOK             - Update address book
S SETUP                    - Configure or update Pine
Q QUIT                     - Exit the Pine program

Copyright 1989-1999. PINE is a trademark of the U. of Washington

? Help                     P PrevCmd      R ReINotes
0 OTHER CMDS  > [ListFldrs] N NextCmd      K KBlock
```

Typically, I press I to jump right into my INBOX, but Pine also offers several options: pressing C to send a message, L to see a list of my saved mail folders, or A to manage my address book. (We'll touch on those options later.)

If you want to bypass this opening screen, you can add the -i flag to your pine command and go directly to the INBOX screen.

## THE PINE INBOX

The INBOX folder is where you'll spend most of your time in Pine. Following is a sample screen showing three messages. Pine displays a message number, the date sent, the real name of the sender (if available), the size (in bytes), and the Subject line of each message in your INBOX.

The first message is flagged with an A, which indicates that I've already read and answered it. The other two are each flagged with an N because they are new messages. Messages that have been read but not answered are blank in the flag column.

So what about the plus (+) signs in front of certain messages? These tell me that these messages were addressed directly to me (your address appears in the To field, even though you don't see that field
