Date: Tue, Jul 17 2001 10:50:32 -600
From: nicholass@hostname.localdomain
To: panzasan@hostname.localdomain
Subject: Meeting Postponed?
Sancho, Perez just dropped by my office. Please call us regarding the status of the meeting Don Quixote scheduled for tonight at Lady Dulcinnea's. The Don told us yesterday that he thought the meeting was a 'go' but that he had not received confirmation from the Lady yet. Is it still on? Meanwhile, are you keeping a close watch over him? We don't need another 'windmill' episode.

Nicholas and Perez

Here are few subcommand options---also called subcommands because they invoke their own functionality---for reading mail:

+   * To read the first message in the listing, press Enter or type 1 and then press Enter.
+   * To skip the first message and read the second message, type 2 and press Enter.
+   * To read the first new message in any listing, type t and press Enter.
+   * To read the messages in sequence, simply press Enter after starting at your chosen first message. Then, press Enter after reading each message in turn.

You can also type the following letters (among others) at the & prompt while reviewing your messages:

+   | f   | lists the headlines of messages in the mailbox   |
+   |-----|---------------------------------------------------|
+   | d   | deletes messages                                  |
+   | m   | forwards messages                                 |
+   | r   | sends a reply                                     |
+   | q   | exits mail and leaves unread messages in the queue|
+   | s   | appends a message to a file                       |

To obtain a full list of available subcommands to use while in mail, type ? at the & prompt.

Now, what if Sancho wanted to check messages that he has received and read in the past? The mail -f command displays a list of messages in his personal mailbox (that is, in the /home/panzasan/mbox file). Normally, when he quits the mail program, undelated (but already read) messages are written back to that mbox file and not back to the (incoming) /var/spool/mail/panzasan file from which all the new messages came. By