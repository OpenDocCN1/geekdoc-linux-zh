
subject lines, sender, recipient, or message body. Click Find Now to search for the keyword. After viewing the messages, click Clear to have the other messages reappear.

- **Filter messages** — You can take action on an e-mail message before it even lands in your Inbox. Click Tools → Filters. A Filters window appears that lets you add filters to deal with incoming or outgoing messages. Click Add to create criteria and set actions.
  - For example, you could have all messages from a particular sender, subject, date, status, or size sorted to a selected folder. Or you could have messages matching your criteria deleted, assigned a color, or respond by playing a sound clip.

> **CROSS-REFERENCE** Refer to Chapter 19 for information on using Spamassassin, along with Evolution filters, to sort out SPAM from your real e-mail messages. Evolution also includes built-in junk e-mail filtering, using Bayesian statistical analysis.

Besides the features mentioned in the previous list, Evolution supports many common features, such as printing, saving, and viewing e-mail messages in various ways. The help system that comes with Evolution (click the Help button) includes a good manual, FAQ, and service for reporting bugs.

## Mozilla Mail client

The Mozilla Mail client program provides a simple interface for using e-mail in Fedora Core. You can access the Mozilla Mail window from your Mozilla browser window by choosing **Tasks → Mail & Newsgroups**. Figure 9-7 shows an example of the Mozilla Mail window that is ready to use mail and news.

![](img/b22364e57409c2481ba806e4e6b9309c_358_0.png)

Figure 9-7: Manage your e-mail from the Mozilla Mail window.

As with Evolution e-mail, you need to provide some information about your mail account before you can connect to your mail server and use Mozilla Mail.

> **TIP:** A new Junk Mail feature was recently added to Mozilla Mail. With Junk Mail, Mozilla Mail automatically tags any message it believes to be junk mail with a blue recycle-bin icon. Using the Junk Toolbar, you train the Junk Mail feature by telling it when a message is or isn't junk mail. After you have identified which messages are junk mail, you can automatically move incoming junk mail to the Junk folder.

### Connecting to the mail server

You must identify information about yourself and your mail server before you can download or send mail messages. The first time you open Mozilla Mail, an Account Wizard appears. Select to set up an e-mail account; then enter the following information as you are prompted for it.

- **Your Name** — The name to appear on messages you send (for example, John Smith).
- **Your E-mail Address** — The *name@domain* address that is assigned to you.
- **Incoming Mail Server** — The name or IP address of the mail server from which you get your messages. You also need to know what type of server it is (POP or IMAP). POP and IMAP servers require a login and password. POP stands for Post Office Protocol. IMAP stands for Internet Message Access Protocol.
- **Outgoing Mail Server** — If there is a different outgoing mail server, you need the name or IP address of that server. Likewise, you will probably need login and password information to send mail through that server. You can choose to use Secure Sockets Layer (SSL) to protect your outgoing messages (if it is supported by the server).

After the wizard has created the account, you are prompted for the password for your account on the mail server. Using that password, Mozilla Mail will download all your messages from the mail server. It will try to download messages again every 10 minutes. Or, you can click the Get Msgs button to download messages immediately.

If you want to change how often mail is downloaded, or other features of your account, click **Edit → Mail & Newsgroup Account Settings**. Under the e-mail account you added are categories to change the set-up and behavior of the account. (Click Server Settings to change how often, if at all, new messages are automatically downloaded from the mail server.)

### Managing incoming mail

There are various ways to store and manage the e-mail messages in Mozilla Mail. The following is a quick rundown of how to use Mozilla Mail for managing incoming mail:

- Your e-mail messages are typically stored on a mail server that is contacted over the network. To download your mail messages immediately from the mail server, click **File → Get New Messages** (or click **Get Msgs** on the toolbar).
- Mail messages are stored in folders under the Mail Folders heading in the left column. There should be a separate heading for each mail account you have. For each mail account, incoming messages are stored (by default) in your Inbox folder. You can create additional folders to better keep track of your mail (right-click on inbox, then select New Folder to add a folder). Other folders contain drafts of messages set aside for a time (Drafts), templates for creating messages (Templates), messages you have sent (Sent), and messages that you have discarded (Trash).
- Messages are sorted by date for the folder you select, in the upper-right corner of the display. Click on the heading over the messages to sort by subject, sender, or priority.
- When you select a message, it appears in the lower-right corner of the display.

### Composing and sending mail

To compose e-mail messages, you can either start from scratch or respond to an existing e-mail message. The following are some quick descriptions of how to create outgoing mail:

- To create a new message, choose File → New → Message (or Compose on the toolbar).
- To reply to a mail message, click on the message on the right side of your screen, and then choose Message → Reply (to reply only to the author of the message) or Message → Reply to All (to reply to everyone listed as copied on the message).
- To forward a mail message, choose Message → Forward. You can also forward a message and have it appear in the text (Message → Forward As → Inline) or as an attachment (Message → Forward As → Attachment).

In each case of outgoing mail, a mail Compose window appears, in which you compose your e-mail message. As you compose your message in the Compose window, you can:

- Add e-mail addresses from your personal address book (or from one of several different directory servers) by choosing Options → Select Addresses. A list of your stored addresses appears for you to choose from. Click Collected Addresses to see a list of addresses that have been collected from e-mail messages you have received.
- Add attachments to the message (such as a word processing file, image, or executable program) by choosing File → Attach File. After that, you can select a file from your file system to attach. (You can also choose File → Attach Web Page to choose the URL of a Web page that you want to attach.)
- Add certificates or view security information about your mail message by selecting View → Message Security Info. In the window that appears, you can view general security information about the message.

When you are finished composing the message, click Send to send the message. If you prefer, queue the message to be sent later by choosing File → Send Later. (Send Later is useful if you have a dial-up connection to the network and you are not currently online.)

> **TIP:** If you want to quit and finish the e-mail message later, you can choose File → Save As → Draft. Then click the X in the upper-right corner to close the window. When you are ready to resume work on the message, click the Draft folder in the Mozilla Mail window and double-click the message.

## Thunderbird Mail client

As a companion to its Firefox Web browser, the Mozilla project created the Thunderbird Email client. If you installed Thunderbird (thunderbird package) from the Fedora Core 3 DVD that comes with this book, you can launch it from your red hat menu by selecting Internet → Thunderbird Email.

The first time you run Thunderbird, an import wizard opens, allowing you to import preferences, account settings, address books and other data from other e-mail clients. Have information about your e-mail account (user name, incoming and outgoing servers, and so on) ready so you can enter before Thunderbird starts up. Figure 9-8 shows an example of the Thunderbird window.

![](img/b22364e57409c2481ba806e4e6b9309c_361_0.png)

**Figure 9-8:** Thunderbird is an efficient e-mail client that includes advanced junkmail and message filtering.

In many ways, the layout and selections in the Thunderbird client are similar to those in Evolution. In general, however, Thunderbird seems to offer better performance than Evolution. Here are some features of Thunderbird that may interest you:
