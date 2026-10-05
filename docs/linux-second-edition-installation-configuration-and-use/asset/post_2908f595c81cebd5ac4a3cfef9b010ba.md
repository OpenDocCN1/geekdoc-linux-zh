
sender's address into the address book. The address book is stored in the text file ~/.addressbook.

> The address book is very useful for managing mailing lists. For example, you can define an entry 'sales' and enter all addresses of employees of the sales department. If you want to send an email to this group you only need to enter 'sales' as the address.

## Sorting messages, searching for texts

Messages are usually stored in a folder in the order in which they are received. With the SORTINDEX command (shortcut $) you can change the order. However, the new sorting order is not stored. A permanent sorting order – which is, however, applied to all folders – can be selected in the configuration menu (see above).

Unfortunately there is no real search function in pine. WHEREIN refers to visible text, that is to say, either to the list of email headers or to a specific email.

## Sending and receiving binary files with pine

If you want to send a file together with the email message you are writing, you must place the input cursor into the Attachment: field and execute the command Ctrl+J. Now, pine asks you for the name of the file you want to transmit, then for a comment about this file (a brief explanation of the file contents and/or data format). You can attach more than one file to an email message.

The opposite occurs when you receive an email message with an attached file. In this case, pine only displays the normal message. Some lines tell you that other files are attached to the message. You can now view these files with VIEWATTACH andor store them as separate files on your computer. For processing the first attachment, you must specify attachment number 2 (because pine assigns the number 1 to the normal message). Viewing an attached file only makes senses when the binary file is in text format (which tends to the exception).

Attached files are coded by pine in a special format. In order to prevent transmission problems, only ASCII characters are used, which increases the amount of transmitted data by about 25% compared with the actual size.

Old programs simply send binary files as encoded ASCII. Such emails can be recognized by the fact that, in an endless list of ASCII characters, a line of the form begin file.name can be found, pine cannot automatically extract binary files encoded in this way. You need to move the message with EXPORT another file and subsequently (after you have left pine) execute uudcode file (see also page 347).

## Forwarding emails (forward/bounce)

If you have several email accounts – for example at your university or in your company and a second private one – you may often wish to forward individual emails from one account to the other. As a rule, this is done by means of the FORWARD command. This command, however, has the disadvantage that the sender changes. An email message originally sent by XY now looks as though it had been sent by you (This is entirely correct; with FORWARD, you send an existing email as if it was a new one—maybe even with additions.) If you use the BOUNCE command instead of FORWARD, the sender remains unchanged. To make BOUNCE available, you need to activate the command in the pine configuration (see above, above).

If you do not want to forward individual emails, but all emails from one address to the other, you can usually employ the file /.forward for this purpose. (The prerequisite is that the email system of the receiver computer interprets this file correctly. This is the case in most Unix systems.)" The content of .forward typically looks like this:

```
hoferprovider.de
hofer
```

Here, incoming mail for the user 'hofer' (login name for the account in which .forward is located) is forwarded to the address hoferprovider.de. At the same time, a copy of the emails is stored locally (second line; otherwise you could read your emails only on your private account and not on your local computer).

## Processing groups of emails

If you receive a lot of emails, processing each individual message becomes tiresome. Often one wishes to delete all emails that satisfy a certain criterion together, or move them to a specific folder, and so. pine provides the appropriate commands. However, these must first be activated in the configuration (enable-aggregate-command-set, see above).

You can now select a group of emails with SELECT (keyboard shortcut use this variation in combination with the sort command), selection of all emails containing a certain text as sender, subject, and so on, selection of all emails of a specific range of dates, and so on. To select individual emails you can also use instead of this command refers to the email which currently contains the cursor. Selected messages are marked by an X in the left-hand column.

As a second step, you can now process all selected emails with APPLY—for delete delete store, or forward them, extract addresses, and so on.

## Alternatives to pine (elm, emacs)

pine has been extensively described as an important representative of text-oriented email clients. To conclude, we will give some brief information on alternatives to pine. The common denominator of these programs is that, like pine, they can be used in text mode and that they require configuration of sendmail and fetchmail (or equivalent programs).

## EMAIL

### elm

elm is not quite as user-friendly as pine, but still easy enough to operate. After the start-up elm creates the directory /.elm in which all elm-specific files are stored.

In order to prevent elm from using vi as its editor, you must either set the environment variables EDITOR and VISUAL in the profile file (see page 139) or specify the file name of your favorite editor in the editor= option of the configuration file /.elm/elmrc:

```
/.elm/elmrc
editor=/usr/bin/
```

elm is menu driven, with most important commands displayed at the bottom. Information about elm can be found in man page.

The mail mode of both Emacs has one particular feature which at first may be a little irritating; the programs read the entire file /var/spool/mail and transfer all messages. This behavior can be changed through configuration of /etc/mail.rc or ~/.rc.

### mutt

mutt is seen as the successor of elm. The most important differences are the extensive possibilities. Information about mutt is available on:

> http://cs.hm.edu/~mutt

### Using Emacs as a mail program

Properly speaking, GNU-Emacs XEmacs are text editors and not mail programs (Chapter 16 from page 537). However, by means of the commands READ MAIL or APREAD MAIL, both programs can be put into a very sophisticated mail mode (the user surface of XEmacs).

## 10.5 sendmail and fetchmail offline configuration

### Sending mail (sendmail)

The sendmail program is used to send email from one computer to the other. The application described here – sending of a couple of emails from one person to the Internet provider means letting sendmail run idle. The program is really designed for sending large amounts of mail, with numerous options allowing very complex operations to be controlled (automatic modification of sender and addressee, rejecting incorrect addresses, automatic warnings if mail cannot be delivered, and so on). In fact, the program is employed-wide by innumerable universities and Internet providers to deliver mails of each day.

These possibilities of application explain why configuration of sendmail is a fairly complex affair (this chapter cannot even outline, let alone explain). An alternative to sendmail is represented by.

Most Linux distributions are configured in such a way that sendmail is started as a background process (daemon) during the Init process (page 124).

Email that cannot be delivered immediately, because no Internet connection is active, is stored in the /var/spool/queue directory. sendmail periodically undertakes further delivery attempts. When email cannot be delivered for a longer period of time, sendmail sends a warning to the sender.

Even if your computer is only infrequently connected to the Internet via PPP, sendmail should run as a background process, since the program also deals with the
