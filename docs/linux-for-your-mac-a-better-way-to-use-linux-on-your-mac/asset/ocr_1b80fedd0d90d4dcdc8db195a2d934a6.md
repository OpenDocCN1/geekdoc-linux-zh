automatically organize mail according to interest (such as saving mail from different mail lists, or e-mail subscription lists).

# # Using E-Mail Utilities

Every Linux distribution comes with dozens of electronic mail utilities. A few of the more useful programs include:

+   - audiosend Send an audio e-mail message
+   - biff Alert you when incoming mail arrives
+   - elm Another e-mail client
+   - frm Strip and display e-mail headers from your mailbox's e-mail
+   - hypermail Convert e-mail into HTML files
+   - printmail Format e-mail for printing
+   - procmail Process incoming mail
+   - readmsg Display mail messages from your inbox
+   - vacation Send automatic replies to incoming mail

Experiment with different utilities. You are sure to find a use for many of these mail utilities.

# ## Fighting SPAM

SPAM is one of the worst manifestations of the communications revolution, because it is much more personal and intrusive than postal junk mail. The good news is that legislators are finally listening to fed up consumers and many states now have laws with monetary penalties for the techno-idots who bombard our electronic mailboxes with their stupid hype.

You can use the procmail command to filter incoming mail to help reduce the clutter. This means that if you find yourself bombarded with unwanted messages that have some common element in the sender's address, subject line, or body of text, you can discard the mail quickly and easily.

In order to use procmail, create a file named .procmailrc in your home directory. This file should contain the following:

```
MAILDIR=$HOME/mail
PMDF=$HOME/.procmail
INCLUDERC=$HOME/.procmail/rc.mailfilter
```