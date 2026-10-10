# USING ELECTRONIC MAIL



+   6  When you finish editing, save the changes into the file and quit the editor. Do this with the usual commands:
+   
+   ( Esc :wg (Return)
+   
+   This will put you back in the mail program. You may see a prompt of some sort:
+   
+   ( continue )

+   7  Send the message. This is done the usual way:
+   
+   ( Return )
+   ( Control- D )
+   
+   You may be asked to specify carbon copies.
+   
+   Cc:

+   8  Send the carbon copies, if any. Press (Return) if you do not wish to send any copies:
+   
+   Cc: (Return)
+   
+   This will get you out of the mail program and back into the UNIX shell:
+   
+   $ 

# 14.4 Your Mailboxes

The mail program uses two kinds of mailboxes. Your *system mailbox* is a file that holds mail you have received but have not read, deleted, or saved to another file. On many systems, this file is located in the `/var/spool/mail` directory, and has the same name as your user ID. For example, if your user ID is *jdoe*, then your system mailbox is the file `/var/spool/mail/jdoe`.

In addition to the system mailbox, you may have a *personal mailbox*. This is a file named `mbx` in your home directory. Any mail messages you have read but not deleted or saved in another file are automatically put into your `mbx` file when you quit the mail program.

If you use either the Bourne Shell or Korn Shell, your shell checks your system mailbox periodically and notifies you of any new messages:

New mail has arrived.

You can also use the `biff` or `xbiff` program to alert you when new mail arrives. These programs are discussed in the exercises.