
under the message view area that includes the attachment list, and there are two menus, Edit and Attachments, above the message view area.

On the Edit menu, there is a Copy option and a Select All option. You must highlight the text you want to copy before you select Copy. The text you highlighted is copied into memory and you can then paste it into other applications that can receive text. The Select All option highlights all the text in the message at once.

The Attachments menu has four options: Save As, Select All, Open, and Print. Save As saves the attachment to the hard drive without opening it. The attachment's name can be changed during the save process. Select All highlights (selects) all the attachments in the attachment list. The Open option opens the attachment with the proper application (provided that your system has software installed that can read the file and open it). When you choose Print, the Print dialog box appears. It has the following features:

- **File** Displays the name of the file.
- **Printer** Displays the name of the printer to send the job to. Enter the name of the printer you want to use.
- **Copies** Enter the number of copies to print.
- **Banner Page Title** Choose this to print text at the top of each page (which isn't the same as a banner page).
- **Banner Page Numbers** Choose this to print the page number at the bottom of each page.

One useful Mailer option is to save e-mail messages as text. To do so, open the message in the main Mailer window and choose the Save As Text command from the Message menu. Outgoing mail can be saved as text from the Save As command on the File menu (when the Compose window is open).

Mailer can also attach e-mail to the end of existing text documents. Let's say a corporate manager has a file named johnrecords in his home directory, and John sends a weekly status report to the manager. Each week, the manager can open the message containing the status report, choose Save As from the File menu, and click the Append button in the Save As dialog box. This will add John's e-mail message to the end of the file named johnrecords.

## Customizing Mailer

You customize Mailer by using selections from the Options menu. In the following sections, we'll explain some of the selections in more detail.

To create an alias, which is a name that you enter that points to a valid e-mail address, do this:

1. Click the To button in the New Message dialog box and select Aliases from the drop-down menu. The Mailer—Mail Options dialog box appears.
2. Enter the alias in the Alias text box. An alias can be any valid text string.
3. Enter the valid e-mail address in the Address text box.
4. Then click the Add button.

### The Basic Command

Figure 13.7 shows the Mail Options dialog box that appears when you choose the Basic command from the Options menu. You can use this dialog box to make simple configuration changes that affect the performance of Mailer. At the top of the dialog box is a section labeled Mailbox Updates. You can use it to define how often the mail server will be checked for new mail. The default time is 300 seconds (5 minutes). If, for some reason, you need to check your mail more often, you can set this time period to a lower value. The only problem with setting it to a lower value is that you will increase network traffic if you are using an IMAP server. If you are using the local mail spool instead of an IMAP server, it will increase your hard disk activity.

![](img/256e02a6afce528d264a8d911fa0ff20_542_0.png)

The Basic Mail Options dialog box also gives you the choice of saving copies of your sent e-mail to a file. The text box next to the Save a Copy of Outgoing Mail In check box displays the name of the backup file for your mailbox. This file is named sent.mail1. If your company has a policy of destroying e-mail messages, you might want to edit this file on a regular basis and destroy old messages. You cannot save attachments in this file, only the text portion of your outgoing e-mails.

This file can be used by a system administrator to restore a damaged e-mail system. The default time to save the sent.mail1 file is every 30 minutes. This should be sufficient for most e-mail users. Power users might need to save this more often.

> **TIP** Save your sent_mail1 file on a disk located on another server. Then, if your hard disk crashes and you lose your e-mail, you’ll have the means to recover it. The easiest way to save sent_mail1 to another disk is to create a simple script or cron job that copies this file to an NFS-mounted directory. Be careful when doing this so that you don’t accidentally give other users access to your mail file.

The section of the Basic Mail Options dialog box that applies to the Message Header List gives you the option to select how many e-mail headers will be shown. The next section, Destroy Deleted Messages, allows you to destroy messages that have been deleted.

One issue that comes up in the corporate world is the concept of destroying e-mail effectively. Most people think that if they delete an e-mail message, the message is gone. Wrong! Most e-mail programs have an undelete or trash directory that saves a copy of the supposedly deleted e-mail message. Mailer also has this feature. There are times when it is nice to have the ability to recover an accidentally deleted e-mail message. However, if you decide you need to destroy your e-mail messages, you can modify the default behavior of Mailer to destroy the messages you’ve deleted when you exit the program. This is done in the Basic Mail Options dialog box.

> **TIP** It is fine to delete mail, but be aware that mail can be elsewhere on the server, even though you have deleted it. It can still be on backup tapes on the mail server or on the server it came from.

At the bottom of the dialog box, you can specify an IMAP e-mail server if you haven’t specified one before.

## The Compose Window Command

To perform more advanced customization of the Mailer program, select the Compose Window command from the Options menu. The Compose Window Mail Options dialog box (shown in Figure 13.8) has options you can use to customize the pop-up window that is shown when you compose a new message. The Compose window has a default width of 80 characters. The default size can be enlarged to take advantage of large-screen monitors. The attachment list appears with the Compose window when an attachment is added to the e-mail message, but you can choose not to show it. When you reply to a message, the standard character (called the indent character) that is used to distinguish your text from the text of the original message is the > sign. The indent character can be changed to any character that you prefer.

One of the features of Unix e-mail is the $HOME/DeadLetters directory. It keeps a copy of the e-mail messages you are currently working on. Usually, you will not be able to recover from this directory after a crash or you will find it empty. The $HOME/DeadLetters directory should have only the letters that were open for writing at the time of the crash. After a letter has been saved and closed or sent, the copy is removed from the directory.

![](img/256e02a6afce528d264a8d911fa0ff20_544_0.png)

In the bottom section of the Compose Window Mail Options dialog box, you can customize the header fields in your messages. You should not use these options unless there is a strong need to do so. Incorrect header fields in an e-mail message can cause the e-mail system to crash or not work for your messages. (Manipulating the headers of e-mail messages is an advanced topic and beyond the scope of this book.)

## The Advanced Command

Mailer has some more advanced configuration options. They are accessed by choosing the Advanced command from the Options menu. The Advanced Mail Options dialog box is shown in Figure 13.9.

The options in the Advanced Mail Options dialog box are as follows:

| Option | Description |
| :--- | :--- |
| **Warn if Message Exceeds 1000 Kbytes** | Enable this option to have a pop-up warning message displayed if you try to send an e-mail message that exceeds the size that is indicated. After the warning message is displayed, you are given three choices: Send, Cancel, and Help. |

![](img/256e02a6afce528d264a8d911fa0ff20_545_0.png)
