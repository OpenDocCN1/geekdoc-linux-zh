As you can see in Figure 23-1, a Linux email server is normally broken into three separate functions:

+   ♦ The mail transfer agent (MTA)
+   ♦ The mail delivery agent (MDA)
+   ♦ The mail user agent (MUA)

The job of the MTA is to deliver mail messages between different mail servers on the Internet—most likely you and Aunt Betty use different Internet service providers (ISPs), each with its own email server. The job of the MDA is to move mail received by the MTA to the appropriate user’s local mailbox. Finally, the job of the MUA is to allow individual users access to their own mailboxes to read and send messages.

The lines between these three functions can sometimes be fuzzy. Some email packages combine functionality for the MDA and MTA functions, while others combine the MDA and MUA functions. The following sections describe these basic email agents and show how they are implemented in Linux systems (and specifically in Ubuntu) in more detail.

# Mail Transfer Agent

The MTA software is responsible for handling both incoming and outgoing mail messages on a mail server. For each outgoing mail message, the MTA determines the destination of the recipient addresses. If the destination host is the local machine itself, the MTA can either deliver the message directly to the recipient’s local mailbox or pass the message off to the local MDA program for delivery.

However, if the destination host is a remote mail server, the MTA must establish a communication link with the remote host to transfer the message. Similarly, for incoming messages, the MTA must be able to accept connection requests from remote mail servers and receive messages destined for local users.

Many types of protocols can be used to transfer messages between two remote MTAs. The most common protocol used for Internet mail transfer is the simple mail transfer protocol (SMTP). This protocol is used only for passing messages to mail servers. It’s not normally used for retrieving messages from an individual mailbox.

There are three popular MTA packages you’ll often find on Linux servers:

+   ♦ sendmail
+   ♦ qmail
+   ♦ Postfix

Each of these MTA packages provides the same basic functions of using SMTP to send and receive mail messages. However, there are a few differences among them. The following sections describe these three MTA programs.

# sendmail

The sendmail MTA program is one of the most popular Linux MTA programs available. The program was originally written and supported by Eric Allman, but the Sendmail Consortium (http://www.sendmail.org) currently maintains the source code for