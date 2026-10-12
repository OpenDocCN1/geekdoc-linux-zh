+   Display threads — Click on a small callout icon in the Thunderbird message pane. Then, instead of simply sorting your messages by date, subject, or sender, messages are sorted by threads (so all messages created in response to a message are sorted together).

+   Junk Mail Controls — Select Tools ☛ Junk Mail Controls to configure how Thunderbird deals with messages that appear to be junk mail. From the Junk Mail Controls window, select to Delete or Move to the "Junk" folder any messages you mark as junk mail.

To manage your junkmail, click in the junk mail column (a circle with a line through it) next to a message that comes into your mailbox that is junk mail. By marking messages as junk mail, you can train Thunderbird's adaptive junk mail filter to learn when a message is junk mail and mark new messages that come in as such. Select Tools ☛ Run Junk Mail Controls on Folder to apply junk mail filtering to the current folder.

+   HTML messages — You have the options of creating HTML markup in the mail messages you compose. When you write a mail message, from the Compose window you can choose what type of text to use, change font sizes, add bullets or numbers, set text justification, and add emoticons (to name a few features) (Note that in many news groups and mailing lists you should not use HTML markup since some people like to use text-only mail clients to access those groups).

After using the Thunderbird e-mail client, the biggest improvement over other graphical email clients I have used is performance. Sorting and searching messages is much faster than I've experienced on other clients. Switching to different mail folders and opening messages also seems to work much faster.

# Text-based mail programs

There are many text-based mail programs for reading, sending, and working with your mail. Many of these programs have been around for a long time, so they are full of features and have been well debugged. As a group, however, they are not very intuitive. The following sections describe some text-based commands.

> TIP: Most of these programs use the value of your $MAIL environment variable as your local mailbox. Usually, that location is /var/spool/mail/user, where user is your user name. To set your $MAIL so that it points to your Mozilla mailbox (so you can use either Mozilla Mail or a text-based mail program), add the following line to one of your startup files:
> `export MAIL=$HOME/.mozilla/default/*/Mail/hostname/Inbox`
> If you usually use Mozilla for mail, set this variable temporarily to try out some of these mail programs.

# Mail readers and managers

Mail readers described below are text-based and use the entire screen. Although some features are different, menu bars show available options right on the screen.