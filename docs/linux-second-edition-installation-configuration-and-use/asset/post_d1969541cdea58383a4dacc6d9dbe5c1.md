
# Signature

It is a matter of politeness in the Internet community to finish off emails and news articles with a few lines of text which, apart from data such as company name, address, and so on, may also contain personal statements ('I love Linux'). To relieve you from having to enter the text repeatedly, most email programs automatically insert the contents of the file ~/.signature at the end of the message.

# Binary files

Email messages usually consist only of ASCII text, which does not cause problems to any of the email programs. In addition, all modern email programs support the mail standard MIME. This abbreviation stands for Multipurpose Internet Mail Extensions. MIME can be used for easy transfer of binary files. In some email programs, you can view images and HTML files directly when your addressee has a program that supports MIME.

Problems arise when the coded file is displayed directly as text. This will look more or less like the following list:

```
---137161636-894403337-790290599:#100
Content-Type: TEXT/PLAIN; CHARSET=US-ASCII; NAME="picture.ps"
Content-Transfer-Encoding: BASE64
Content-ID: .3.89.9501170859.B100hofer.muenchen
Content-Description: Image
I0Z2JRYAyJLENCgWIDENCgNCAWIDLEgTGECAwMDAg4cMDAMCAIdDAMDAIDEAyLIAyAYQgMTY41DE20CA20ASNASCA2MDAQgMgMQDoxIdQgMCAXOx
MCAwUljAwMDAwIDMgTTAID3MSNCAMjkq2psa2psamramxbgtGqGtq
---137161636-894403337-790290599:#100--
[EO3B]
```

# uuencode and uudetcode

The commands uuencode and uudetcode are a relic from the past, when MIME had not yet been established as a standard. They are used to convert a binary file into ASCII format or to recreate the binary file from an ASCII file. In this way, it is possible to send binary files with stone-age email programs. In the unlikely event that you receive an email or send one yourself, here is the syntax of the two commands:

```
user$ uuencode file name > uufile
user$ uudetcode uufile
```

uuencode encodes files and stores the result in uufile. name specifies which file name should be stored within the encoded file. Generally, the same name is specified for file name; uudetcode can restore the file name without further information.

# 10.2 Netscape Messenger

The Netscape component of Netscape allows you to read and write email and news. From the Netscape main window, you start Messenger with COMMUNICATOR MESSENGER or with MAIL|

Before you can use Messenger to enter your full name and your email address in the EDIT|PREFERENCES|MAIL|IDENTITY dialog sheet. Some further specifications are optional, such as the file name of the signature, or the reply address. (This is only required when the absentee should not send a reply to your sender address to a different one.)

![](img/b30873dd3d753687a59253fb9ad26a0b_375_0.png)

## 10.1 Reading email with Netscape.

### Configuration as a stand-alone system

If you want to use the mail functions without additional programs such as sendmail or fetchmail3, the following settings are required on the MAIL SERVERS dialog:

INCOMING MAIL SERVERS: here you specify the Internet address of your Internet provider's POP server (pop.provider.de for the sample user page 305). As USER, you must indicate the login name for the POP account. This may or not be the same name as your email address (that is hofer). When you establish a connection for the first time, you are prompted for a password. If you want Netscape to remember this password forthwith, you must activate the appropriate option. (The encrypted password is stored in /.netscape/preferences.js.)

The option CHECK FOR MAIL EVERY ... MINUTES should be deactivated - it does not make sense in offline operation. Finally, you can specify whether your email should remain on your Internet provider's server. This setting is extremely useful for first experiments (otherwise, an email might occasionally get lost in the configuration muddle), but it absolutely needs to be deactivated on, or your email list from the provider's will will grow until all your available storage space is filled.

# NETSCAPE MESSENGER 349

Under OUTGOING MAIL SERVER you enter the name of your provider's server to which all your email to be sent for delivery (mail.provider.de for the sample userhofer).

If you do not specify a different directory, all email folders (including Inbox) are usually stored in the directory ~/nsmail/.

![](img/b30873dd3d753687a59253fb9ad26a0b_376_0.png)

Figure 10.2 Configuration as a stand-alone system.

### Configuration as a client for sendmail/fetchmail

If Netscape is only to be used for reading local email (sendmail and fetchmail) deal with forwarding of messages, see page 359), some configuration details look slightly different:

As INCOMING MAIL SERVER you now use the movemail program, which is supplied together with Netscape. Use USER you need to specify the name under which your email is stored in /var/spool/mail (as a general rule, your local login name). You should activate the option CHECK FOR EVERY MINUTE - it certainly does not involve a lot of effort to check the contents of a local file once minute.

While reading email messages, Netscape creates a lock file in /var/spool/mail. However, this only works, if the program is allowed to write data in this directory. Therefore, the rights for /var/spool/mail may have to be extended:

```
root chmod +w /var/spool/mail
```

This has the disadvantage, that any user can now arbitrarily store files in this directory. The only alternative would to use an external mail program with SETUID privileges which reads the messages from the directory.

As OUTGOING MAIL SERVER you specify localhost. You can do without entering the OUTGOING MAIL USER NAME.

# Usage

Usage of Messenger should not pose any problems. Two further points regarding utilization of a stand-alone system: to read mail, you establish an Internet connection and execute the command FILE|GET NEW MESSAGES. Subsequently you can terminate the PPP connection.

Now you can read your emails in peace. When you write replies, you use FILE|SEND LATER for sending them. Only after you have finished writing your email messages you establish a connection to your provider and execute FILE|SEND UNSENT MESSAGES.

# 10.3 KDE Mail

The kmail program belongs to KDE, but can course be used independently. It provides similar functions as Netscape with the additional advantage of KDE integration (drag & drop). A bonus is the fairly good keyboard handling. On the other hand, kmail is not as mature as Messenger and provides fewer configuration options (which, however, makes configuration easier).

![](img/b30873dd3d753687a59253fb9ad26a0b_377_0.png)

Figure 10.3 Reading email with kmail.

Some email folders (inbox, outbox, sent-mail, and trash) are automatically created in the directory ~/.Mail at the first startup. The configuration of the program is carried out with FILE|SETTINGS. On the IDENTITY dialog sheet, you specify your full name and your email address.

### Configuration as a stand-alone system

SENDING MAIL on the NETWORK dialog sheet, you specify the address of your provider's server as SMTP server (mail.provider.de for the sample user hofer). Usually, the correct port number is 25.

INCOMING MAIL: here you must create a new POP account, which can you name as you wish. The entries for user, password, and POP server should not pose a problem. As a rule, the port number is 110.

NEW COMPOSER: activate the option SEND LATER, so that completed email messages are only sent when you execute the comand FILE SEND QUUED.

### Configuration as a client for sendmail/fetchmail

SENDING MAIL: here you only need to activate the SENDMAIL option.
INCOMING MAIL: here, too, you cannot cause much damage - create al local mailbox and specify the path to the local email directory (usually /var/spool/mail/user).

# Usage

As Messenger, usage should be obvious. To check for new messages, you execute FILE CHECK MAIL. (In stand-alone operation, you must activate PPP first). To send repliers, the already mentioned comand SEND QUUED is used.

# 10.4 pine

pine is one of the classic email clients under Linux and Unix. The program runs in text mode which, the age of graphical user interfaces, is seen as a disadvantage by some users. However, do not disregard the advantages:

- pine is a relatively 'old' program, that means it is mature and stable.
- pine can be operated very efficiently via the keyboard. You will appreciate this advantage when you process huge quantities of email.
- pine also runs in a text console or via telnet or login.(If your computer has permanent connection to the Internet, this is a crucial aspect: you can login world-wide with telnet to process your email.)

Unfortunately, the handling of pine is not as intuitive as that of the preceding programs, so this section is rather long. Do not be deterred by it!

> Further information on pine (including an excellent collection of FAQs) can found on the Internet:

http://www.washington.edu/pine

# Configuration

In contrast to the programs (Netscape and kmail) described above, pine cannot be used as a stand-alone program for offline operation. The use of pine requires either
