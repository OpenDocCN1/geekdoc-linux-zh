
| Email Client | User Interface | Description |
|---|---|---|
| `/usr/bin/pine` | Character | pine is a screen-oriented message-handling tool. In its default configuration, pine offers an intentionally limited set of functions geared toward the novice user, but it also has a growing list of optional power-user and personal-preference features. pinef is a variant of pine that uses function keys rather than mnemonic single-letter commands. |
| `/usr/bin/mutt` | Character | mutt is a small but very powerful text-based program for reading electronic mail under Linux or UNIX operating systems, including support for color terminals, MIME, and a threaded sorting mode. |
| `/usr/X11R6/bin/xfmail` | X Window | xfmail is an application for sending and receiving email under X. It’s partially compatible with MH-style mailboxes but it does not require that any MH tools be installed on the system. xfmail supports POP and SMTP mail protocols and it has full MIME support. |
| Netscape Messenger | X Window | This is an email handler that is part of Netscape Communicator. |

## CHARACTER-BASED EMAIL CLIENTS

A character-based email client is one that is not graphical in nature. In other words, it’s not pretty but it is very functional for those who like to keep their hands on the keyboard rather than on a mouse. Character-based email clients are typically ones that are used when a user is logged in directly to the system that hosts the email server.

> **Note:** Some character-based email clients, such as mutt, have or are adding capabilities to use such protocols as IMAP, which enable the email client to retrieve messages from the email server without being directly logged in to it.

## NETSCAPE MESSENGER

Many graphical email clients are available with Linux. Of course, user preferences and opinions vary, but the email client that is part of Netscape Messenger might be the easiest to configure and use. Two basic components must be configured to set up email with Netscape Messenger. To configure the necessary components of email, click on the Edit menu within the Netscape Navigator browser and then select Preferences. When the initial dialog box appears, select Mail & Newsgroups.

Be sure to click the arrow next to the heading Mail & Newsgroups in order to see the complete list of options within this category.

A list of the following options is displayed:

- Identity
- Mail Servers
- Newsgroups Servers
- Addressing
- Messages
- Copies and Folders
- Formatting
- Return Receipts
- Disk Space

Selecting Identity produces a screen similar to the one that is depicted in Figure 25.1.

**Figure 25.1** Identity setup for Netscape Messenger Mail Handling.

![](img/c741b1b6b6eccaba2ad43454c979a7f8_482_0.png)

The second component that must be configured is the Mail Server. Configuring this component enables the capability to receive email. Clicking Mail Servers in the Mail & Newsgroups category presents a screen that enables you to add or modify mail servers. Click Add to display the screen that is depicted in Figure 25.2.

**Figure 25.2** Mail server setup for Netscape Messenger Mail Handling.

![](img/c741b1b6b6eccaba2ad43454c979a7f8_483_0.png)

Add the hostname, complete with the domain name, as the server name; also add your username. Your username is the same as the user ID that was created as your account name on the Linux server.

> **Note**
>
> The mail server must be set up to support IMAP, Movemail, or POP in order for the mail handler in Netscape Communicator to receive email. See the “Delivery Agents” section later in this chapter for details on how to set up IMAP or POP. Use of the internal Netscape Movemail will not be covered by this text.

## KMail

The KMail utility is included with KDE and is a very friendly, easy-to-use agent. Before you can use it though, you will need to configure it.

KMail configuration is performed by selecting File→Settings. This will bring up a Settings dialog box with several tabs. The appropriate setting for most users will be covered in the next few paragraphs.

The Identity tab contains the settings used to put the appropriate headers on your outgoing mail. Although none are mandatory, customary practice is to include your name as you would like others to know you, your email address, and your reply-to address if different from your email address. In some cases you might want to include your organization or company and signature file (standard is .signature).

The Network tab sets up outgoing and incoming mail. This tab’s fields are mandatory. In the Sending Mail section, most readers will select SMTP and put their ISP’s outgoing mail server address. Unless you’ve been instructed otherwise, do not change the port to other than 25. You won’t use sendmail as your MTA unless your system has a legitimate DNS MX RR pointing to it. If the previous sentence was unintelligible then you almost certainly are not a valid Internet mail host. In the bottom half of the Network box you need to configure your Incoming Mail. Again, this will usually point to your ISP’s mail (usually a POP3 host). If you are using a utility like fetchmail to spool mail or if your system is an Internet mail host, you will point to your local mailbox for mail.

The Composer tab has one setting that, although not mandatory, is polite and should be selected: Word wrap at column. The number here is normally set at 72, but can go to 80 (not recommended). Turning this feature off can result in some mail users who don’t have incoming word wrap turned on sending you an often impolite reminder to wrap your outgoing mail.

One default setting on the Misc tab should be explained. This setting is “Automatically send receive and read confirmation.” Although you might want to leave this checked, be advised that spammers love this because it confirms to them that you are a valid email address. It will prompt them to keep you in their list of valid email addresses. So unless you enjoy receiving megabytes of spam, you might want to turn this feature off.

## MAIL TRANSPORT AGENT CONFIGURATION

Although email clients are becoming more and more sophisticated and user-friendly, they remain the simplest part of the whole email process. The email client handles the step that is the equivalent of someone dropping off their letter at the post office or retrieving it from the mailbox in their front yard. In other words, it’s the easy part. The mail transport agent, on the other hand, handles the most complicated aspects of email. In the conventional mail scenario, the MTA is the equivalent of the postal service. The postal service receives the letter, determines how it is to be routed, delivers it to the appropriate local office, and gets it on the correct mail truck to be delivered. The transport agent for email works in a similar fashion. The MTA receives the email from an email client, determines how to route it, transports it to the appropriate MTA for the given recipient, and places it in a retrievable location for the addressee. The configuration of the MTA is complicated by the fact that it needs to be prepared to handle a number of system and network configurations. This is enough of the theory, however—here’s a look at what is required.

> **Note**
>
> In most cases, your MTA should be turned off unless you are a legitimate Internet mail receiver or are using fetchmail to get your mail from your ISP. Also, you won't be able to specify your local host's MTA to send messages on the Internet unless you have a registered domain name and have DNS MX records pointing to your system as a legitimate Internet Mail Exchanger. Most MTAs today won't accept mail from an unregistered host, thanks to the incredible problems surrounding unsolicited commercial email (UCE), aka SPAM.

### SENDMAIL CONFIGURATION FILES

The primary configuration file for sendmail operation is the `/etc/mail/sendmail.cf` (or sometimes the `/etc/sendmail.cf`) file. This file is very complex and should only be modified if you are certain of the changes that you are making.

> **Note**
>
> Starting with sendmail v 8.10.0, all configuration files have been relocated to `/etc/mail/` for uniformity, although the different distributions may elect to put them elsewhere.

> **Tip**
>
> As with all system administration, it is a good practice to make a back-up copy of this file before making any modifications.

The `sendmail.cf` file can be modified in one of two ways: by editing it directly or by modifying the m4 configuration file and regenerating a new `sendmail.cf` file. The m4 utility is a macro processor. Rather than having to know all the aspects of the `sendmail.cf` file, the m4 configuration file offers a method of identifying and configuring the desired components (in somewhat simpler terms), and then processing them with the m4 utility to create a new `sendmail.cf` file.

> **Tip**
>
> For more information on the m4 utility, type `info m4` at a shell prompt. A comprehensive README document can also be found in the `/usr/share/sendmail/cf` directory.

### M4 CONFIGURATION FILES

The m4 configuration file that is used to generate the default `/etc/mail/sendmail.cf` is stored in the `/usr/share/sendmail/cf/cf` directory. The m4 configuration file used for Caldera’s OpenLinux sendmail setup is `generic-col2.2.mc`. The file for Debian is `debproto.mc`, and the file for Red Hat is `/usr/lib/sendmail-cf/cf/redhat.mc`.

A new sendmail configuration file can be generated using this file as follows (note that on Caldera and Red Hat systems, the package `sendmail-cf` must be installed):

```
Caldera:

# cd /usr/share/sendmail/cf/cf
# m4 ../m4/cf.m4 generic-col2.2.mc > /etc/sendmail.cf
```
