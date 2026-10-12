
When **ftpshut** is issued to the system, it creates a file that stores the necessary information. The **ftprestart** command removes this file for all servers, either canceling the impending shutdown or removing the shutdown file and restarting the FTP server. The **ftprestart** only has one optional argument, **-V**, to show version information.

## Using */var/log/xferlog* to View a Log of Server Transactions

The *xferlog* file gives a log of what transactions have occurred with the FTP server. Depending on the settings in the */etc/ftpaccess* file, the contents of this file can contain the files sent or received by who with a date stamp. Table 22.5 lists the fields of this file. The same information can also be found in the corresponding man page included in the *wu-ftpd* RPM.

TABLE 22.5 */var/log/xferlog* Fields

| Field | Description |
| --- | --- |
| current-time | Current local time in the form of *DDD MMM dd hh:mm:ss YYYY*, where *DDD* is the day of the week, *MMM* is the month, *dd* is the day of the month, *hh* is the hour, *mm* is the minutes, *ss* is the seconds, and *YYYY* is the year. |
| transfer-time | Total time in seconds for the transfer. |
| remote-host | Remote hostname. |
| file-size | Size of the transferred file in bytes. |
| filename | Name of the file. |
| transfer-type | A single character indicating the transfer type. The types are a for ascii transfers. b for binary transfers. |
| special-action-flag | One or more character flags indicating any special action taken by the server. The values are C for compressed files. U for uncompressed files. T for TARed files. - for no special action taken. |
| direction | Indicates whether the file was sent from or received by the server. |
| access-mode | The way in which the user logged in to the server. The values are a anonyomous guest user. g guest user, corresponding to the *guestgroup* command in the */etc/ftpaccess* file. r real user on the local machine. |
| username | If logged in as a real user, the username. If the access mode was guest, the password is given. |
| service-name | The name of the service used, usually FTP. |
| authentication-method | Type of authentication used. The values are 0: none. 1: RFC931 Authentication (a properly formed email address). |
| authenticated-user-id | This is the user ID returned to the server based on the authentication method used to access the server. An * is used when an authenticated user ID cannot be found. |
| completion-status | A single character field indicating the status of the transfer. The values are c: completed transfer. i: incomplete transfer. |

An example of this file is seen in Listing 22.6.

LISTING 22.6 Sample /var/log/xferlog File with Inbound and Outbound Logging

Mon Sep  3 07:13:05 2001 1 localhost.localdomain 100
/var/ftp/pub/README b o a testing@test.com ftp 0 * c
Mon Sep  3 02:35:35 2001 1 helios 8 /var/ftp/pub/configuration a
_ o a testing@test.com ftp 0 * c
Mon Sep  3 02:35:35 2001 1 helios 8 /var/ftp/pub/temp.txt a o a
testing@test.com ftp 0 * c
Mon Sep  3 02:35:35 2001 1 helios 8 /var/ftp/pub/tftp-server-
0.17-14.i386.rpm a o a testing@test.com ftp 0 * c
Mon Sep  3 02:35:35 2001 1 helios 8 /var/ftp/pub/wu-ftpd-2.6.1-
22.i386.rpm a o a testing@test.com ftp 0 * c

## Related Fedora and Linux Commands

You'll use these commands to install, configure, and manage FTP services in Fedora Core:

- epiphany—A graphical GNOME browser supporting FTP
- ftp—A text-based interactive FTP command
- ftpcopy—Copy directories and files from a FTP server
- ftpcp—Retrieve data from remote FTP server, but do not overwrite existing local files
- gftp—A graphical FTP client for GNOME
- konqueror—KDE's graphical web browser
- lftp—An advanced text-based FTP program
- nautilus—Red Hat's graphical file explorer and browser
- ncftp—A sophisticated, text-based FTP program
- sftp—Secure file transfer program
- smbclient—Samba FTP client to access SMB/CIFS resources on servers
- system-config-services—Red Hat's system service GUI admin utility
- vsftpd—The Very Secure FTP daemon
- webcam—A webcam-oriented FTP client included with xawtv

## Reference

http://www.wu-ftpd.org/—WU-FTP Official website

http://fedora.redhat.com/—Red Hat's Official Fedora Core website

http://www.cert.org/—Computer Emergency Response Team

http://www.openssh.com/—The OpenSSH home page and source for the latest version of OpenSSH and its component clients, such as sftp

http://www.cert.org/tech_tips/anonymous_ftp_config.html—CERT Anonymous FTP Configuration Guidelines

http://vsftpd.beasts.org/—Home page for the vsftpd FTP server

ftp://vsftpd.beasts.org/users/cevangs/—Download site for the latest releases of the vsftpd server

# CHAPTER 23

## Handling Electronic Mail

Communication by electronic mail—commonly referred to as email—is easily the most popular activity on the Internet and intranets. Email is fast, free (apparently), and easy to use. Hidden behind that seeming ease, however, is a complex infrastructure that can be accessed and controlled with the power of Fedora Core Linux.

In this chapter, you learn how to configure Fedora Core to act as an email server. You also take a close look at the various email clients that Fedora Core makes available for your use, and you learn some techniques for working with them. Although you might not ever need to administer a mail server, understanding how they work can make you a better mail user.

## How Email Is Sent and Received

Email is sent as plain text across networks using SMTP. SMTP is used for sending mail from one network to another. Extensions to the protocol add authentication and error messages to the basic protocol. The mail transfer agent (MTA) works behind the scenes to send and receive email between computers. Some MTAs are Sendmail, Postfix, Fetchmail, Exim, or Qmail.

SMTP helps each computer along the way figure out how to get all the mail delivered to its destination. It is a remarkable system when you think about how complex a task it is asked to accomplish.

Here is a simplified example of how email is successfully processed and sent to its destination:

1. user1@lion.org composes and sends an email message to user2@cheetah.org.
2. The MTA at lion.org receives user1's email message and queues it for delivery behind any other messages that are also waiting to go out.
3. The MTA at lion.org contacts the MTA at cheetah.org on port 25. After cheetah.org acknowledges the connection, the MTA at lion.org sends the mail message. After cheetah.org accepts and acknowledges receipt of the message, the connection is closed.
4. The MTA at cheetah.org places the mail message into user2's incoming mailbox; user2 is notified that she has new mail the next time she logs on.

Of course, several things can go wrong during this process. Here are a few examples:

What if user2 doesn't exist at cheetah.org? In this case, the MTA at cheetah.org will reject the email and notify the MTA at lion.org of what the problem is. The MTA at lion.org will then generate an email message and send it to user1@lion.org, informing her that no user2 exists at cheetah.org (or perhaps just silently discard the message and give the sender no indication of the problem, depending on how the email server is configured).

What happens if cheetah.org doesn't respond to lion.org's connection attempts? (Perhaps the server is down for maintenance.) The MTA at lion.org notifies the sender that the initial delivery attempt has failed. Further attempts will be made at intervals decided by the server administrator until the deadline is reached, and the sender will be notified that the mail is undeliverable.

## IN THIS CHAPTER

- How Email Is Sent and Received
- Basic Sendmail Configuration and Operation
- Introducing Postfix
- Using Fetchmail to Retrieve Mail
- Choosing a Mail Delivery Agent
- Mail Daemons
- Alternatives to Microsoft Exchange Server
- Reference

## The Mail Transport Agent

Working behind the scenes to move mail between computers on different networks, several different MTAs are available for Fedora Core—each with its own strengths and weaknesses. Some are extremely powerful, but very difficult to configure and somewhat slow; others are very fast and easy to configure, but do not contain as many features. The following sections provide more details about some of the more common MTAs available for use with Fedora.

## Sendmail

The vast majority of email traffic on the Internet is handled by an MTA called Sendmail, the default MTA shipped with Fedora (and a number of other Unix distributions). Sendmail has the advantage of being installed and well-supported in your Fedora system. The commercial version (not included with Fedora) sports a GUI configuration utility, as well.

Sendmail is one of the oldest and most powerful MTAs in existence, but it has a few disadvantages. It is somewhat slow; in a high load environment, other MTAs, including Postfix and Qmail, typically can handle a much greater volume of messages per second. Sendmail is also notoriously convoluted; configuration files are extremely cryptic. (The best-selling book on Sendmail is more than 1,000 pages in length.)

Fortunately, the default configuration of Sendmail as provided by Fedora Core works fine for most basic installations, and only minor changes are needed to configure it for a basic
