
When you retrieve your mail, pine looks in the /var/spool/mail directory, and then extracts the messages from your mail file and puts them into the default folder, INBOX, in the directory named mail in your home directory. You can also create other folders and save and delete messages in different folders to organize your mail. Of course, you can also use the procmail approach discussed in the section “Configuring procmail and Writing Recipes to Fight Spam” later in this chapter to automate some of this process for you.

The folder index of your messages is displayed in a list, and you can select messages by scrolling up and down with the cursor keys (see Figure 11.6). From the main list of messages, you can delete, undelete, save, read, and export messages to your directory. To read a message, just hit the Enter key.

FIGURE 11.6
You can select messages through the message list of a pine mail folder.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_281_0.png)

The pine program has a number of command-line options and other features, such as built-in help, which you access with the question mark (?) from the pine main menu.

## Configuring and Using Netscape Messenger for Email

Netscape Messenger, a component of the Netscape Communicator suite of Internet clients, is a graphical electronic mail client for the X Window System. You can start this program from the Communicator menu in the Netscape Navigator window by clicking the Messenger button on Netscape’s component bar. You can also start it through the use of the -mail option with the netscape command like this:

```
# netscape -mail &
```

When the client launches (as shown in Figure 11.7), select the Edit menu, and then click the Preferences menu item. When the Preferences dialog box appears, click the Mail & Groups item, and then click the Identity list item. Type in your name and email address, as shown in Figure 11.8.

FIGURE 11.7
Netscape Messenger is an easy-to-use interface to electronic mail in X11.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_282_0.png)

FIGURE 11.8
Enter your name and email address, along with any other desired information (such as your organization), in the Messenger dialog box.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_282_1.png)

By default, Netscape Messenger sends the text of your email message formatted in HTML. This is okay if you're sending mail to another Netscape user but is a messy way to communicate with others who use mail, elm, or pine. Turn off the HTML message format by clicking the Messages list item under Mail & Groups and then deselecting the HTML messages push button under the Message Properties section of the Messages dialog box.

Next, click the Mail Server list item. This dialog box (shown in Figure 11.9) is used to set several critical items, such as server names and your ISP's mail retrieval protocol. Type your username (usually the name you use to log in to your ISP), and then type the name of your ISP's mail server in the Incoming mail server field (leave the outgoing server entry set to localhost). Next, click to select the type of mail server protocol used by your ISP.

FIGURE 11.9
You can use the Messenger Mail Server preferences dialog box to set critical information needed to retrieve and send mail.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_283_0.png)

Click the More Options button to change other settings, such as the default mail folder or how often you want Messenger to check for waiting email.

When finished, click OK to save your changes. In the main Messenger window, click the Get Msg button (shown in Figure 11.7). Messenger asks for your password. Click the OK button to retrieve your messages. New messages appear in a list in the Messenger window. To read a message, click the desired message in the message list, and its text appears in the bottom half of the Messenger window.

At this point, you can use the various Messenger buttons to reply to, forward, save, print, or delete the message. To compose a new message, click the New Msg button in Messenger's menu bar. The Messenger Compose window appears, as shown in Figure 11.10.

FIGURE 11.10
Compose new messages, address multiple recipients, and attach Web pages or files through Messenger's Compose window.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_284_0.png)

Click in the To: field to enter a recipient. To enter multiple recipients, press Enter after typing in an email address. Next, click in the Subject: field, and enter a subject. If you want to send an attachment with the message, click the Attach button in the compose window's menu bar, or select the File menu and the Attach menu item. Click your mouse in the blank area of the Compose window (below the formatting bar), and type in a message. When you finish, you can save the message as a draft, spellcheck the message, or send the message by clicking on the Send Now button.

## Subscribing to Mailing Lists

When you feel confident that your mail system is working, you might want to subscribe to a mailing list. Mailing lists are handled by automatic mail servers and work by relaying messages generated to all members of a mailing list. One smart way to subscribe to mailing lists is to sign up for a digest version in which the day's message traffic is condensed into a mailing once or twice a day.

You can find out more about mailing lists by browsing to the following:

http://www.lsoft.com/lists/listref.html

Chances are that you can find a mailing list (the preceding site enables you to search more than 21,000 of the 135,000 available lists at the time of this writing) of interest to you. Have fun!

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_285_0.png)

To participate in discussions about OpenLinux using email and to exchange information with other OpenLinux users, send a message to majordomo@rin.caldera.com with the following line in the body of the message:

```
subscribe caldera-users youremailaddress@yourisp.com
```

An electronic mail message asks you to confirm your subscription. Reply to the message according to its directions. For more information about this service, send a message to majordomo@rin.caldera.com with the word help in the body of the message. You receive a reply with lots of details about using Caldera's mailing lists. For the digest version of Caldera's OpenLinux list, send a message to majordomo@rin.caldera.com with the following line in the body of the message:

```
subscribe caldera-users-digest youremailaddress@yourisp.com
```

## Configuring procmail and Writing Recipes to Fight Spam

### NEW TERM
We're all used to getting junk mail or telemarketing calls. Day after day, we receive offers for credit cards, home equity loans, new long-distance service, or great deals on prime cuts of pot roast at the local food market. You can do something about unwanted postal mail, junk faxes, and telemarketing calls, but there's no current nationwide regulation regarding junk email, otherwise known as SPAM (not to be confused with the famous canned meat product).

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_285_1.png)

Fortunately, many State's Attorney General offices around the United States are heeding the hue and cry against spammers, or junk emailers. Some states, such as California, now have civil penalties that are enforced against these bonehead spammers. This type of action is long overdue!

### New Term
You can, however, use procmail, which is found under the /usr/bin directory, to filter your incoming mail. You need to create a directory, create several files, write a small script, and customize how your incoming mail is handled by writing short filters, or procmail recipes. It only takes you a minute or so to set up your system to organize incoming mail and dispose of junk mail.

The first step is to create a text file, called .procmailrc, in your home directory. Then, type in the following, specifying the name of your mail directory (if you use pine, the directory is mail), the location of the .procmail directory (which you'll soon create), and the name of your procmail filter file:

```
MAILDIR=$HOME/mail
PMDIR=$HOME/.procmail
INCLUDERC=$HOME/.procmail/rc.mailfilter
```

Save this file. Next, create a text file called .forward in your home directory. This file needs to contain the following line:

```
"|IFS=' ' && exec /usr/bin/procmail -f - || exit 75 #username"
```

This command line controls procmail, and you should use your username instead of "username." Now, make your .forward file world readable and your home directory world searchable with the chmod command. See the following example (making sure you're in your home directory):

```
# chmod 644 .forward
# chmod a+x .
```

You're almost done. Now, with the mkdir command, create a directory called .procmail, change directory into it, and create a text file called rc.mailfilter.

This file is to contain your procmail filters, or recipes. Although these recipes can be extremely complex (so complex, in fact, that you can write your own mail delivery service), this section presents simple recipes to get you started.

First, examine a sample message's mail headers (which contain the From:, To:, or Subject: lines). The British MG sports cars digest has the following subject line in each message:

```
Subject: mgs@autox.team.net digest #905 Mon Nov 17 10:09:07 MST 1997
```

Each digest message can contain almost 100,000 characters and is sent twice a day, so it is nice to have all these digests go into their own mail folder, which you can call mgdigest. To do this, you enter the following line in rc.mailfilter:

```
:0:
* "Subject:.*digest"
mgdigest
```
