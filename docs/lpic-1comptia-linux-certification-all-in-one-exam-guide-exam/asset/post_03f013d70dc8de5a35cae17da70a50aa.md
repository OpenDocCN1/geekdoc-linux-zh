
## E-mail Message Flow

1. First, the user composes a message using an e-mail client. The e-mail client software is called the *Mail User Agent (MUA)*. Common MUAs include Evolution, Mozilla Thunderbird, and Mutt. The key thing to remember is that the MUA has no idea how to get the message to the final recipient. Instead, it's configured to send outgoing messages to a mail server.

2. When the user selects Send, the MUA sends outgoing messages to a configured e-mail mail server using the Simple Mail Transfer Protocol (SMTP). SMTP is an upper layer, IP-based protocol that runs on port 25. The sole purpose of SMTP is to transfer e-mail messages between e-mail agents.

3. The message is transferred from the MUA to the *Mail Transfer Agent (MTA)* on the mail server. The MTA then decides what to do with the message. If it's intended for another user in your same organization, the message is held by the local MTA for delivery to the recipient's MUA. However, if it's intended for a recipient in a different domain, the MTA forwards the message via SMTP through the Internet to the MTA used by the message's recipient.

4. The destination MTA transfers the e-mail message to the *Message Delivery Agent (MDA)*, also called the *Message Store* for the system where the recipient resides. The MDA's job is to store the message until the MUA of the recipient requests it.

5. The recipient uses e-mail client software (another MUA) to connect to the Message Store and pulls down the message. To do this, it can use either the Post Office Protocol (POP) version 3 or the Internet Message Access Protocol (IMAP). Both protocols are supported by most MDAs and MUAs. POP3 downloads the message using port 110 and the message is deleted from the Message Store. IMAP does the same thing over port 143. However, IMAP has several advantages over POP3. First, IMAP allows you to download the entire message or only the message headers. IMAP also allows you to keep a copy of your messages in the Message Store. It also allows you to create custom folders in the Message Store for organizing messages.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_669_0.png)

**NOTE** Most Linux MTAs do not include any POP3 or IMAP functionality. To use most Linux MTAs with end-user MUAs, you must install and configure a POP3/IMAP daemon that grabs messages from the MTA and delivers them via the appropriate protocol to the MUA.

All Linux distributions include an MTA that runs by default on the system. Several MTAs are commonly implemented on Linux.

- **sendmail** The sendmail daemon is the oldest MTA used on Linux, but it's still the default MTA used by many distributions. It's been widely used for many years. The key thing to remember about sendmail is the fact that it's monolithic; instead, it's a single executable. However, when compared with other Linux MTAs, sendmail can be somewhat difficult to configure.

- **postfix** The postfix daemon is a popular MTA that has replaced sendmail on many Linux distributions (such as openSUSE). One of the key advantages of postfix over sendmail is the fact that it is modular, meaning that it is composed of multiple programs instead of one single executable. Each program has its own tasks that it is responsible for. It uses the master daemon in conjunction with multiple worker daemons that are only started when they are needed. When their tasks are complete, the master daemon automatically shuts them down. In effect, the master daemon and the worker daemons function together as a unit to process e-mail messages through the MTA. The process is shown in Figure 16-13.

1. If an e-mail message is sent to the Postfix MTA by a remote MTA or remote MUA, it is accepted into the system by the smt pd worker daemon. The smt pd daemon forwards the message to the cleanup daemon.

2. If an e-mail message is sent to the Postfix MTA by a user using the shell prompt on the local system, the following occurs:
   - It is accepted into the system by the postdrop daemon, which is also a postfix worker daemon.
   - The postdrop daemon places the e-mail message in the maildrop directory in `/var/spool/postfix`.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_670_0.png)

- The pickup daemon transfers the message from the maildrop directory and forwards it to the cleanup daemon.

3. The e-mail message, regardless of whether it originated remotely or on the local system, is then processed by the cleanup daemon.

4. The cleanup daemon places the e-mail message in the incoming queue, which is also `/var/spool/postfix`.

5. The cleanup daemon notifies the Queue Manager daemon (`qmgr`) that a message has been added to the incoming queue.

6. The `qmgr` daemon moves the e-mail message to one of five message queues, all of which are located in `/var/spool/postfix`:
   - **incoming** This queue contains incoming messages that have been processed by the cleanup daemon.
   - **active** This queue contains messages that arrived intact, were processed correctly, and are ready to be forwarded on to the next MTA or MDA.
   - **hold** This queue contains messages whose delivery, for some reason, has been put on hold.
   - **deferred** This queue contains messages that could not be delivered on the first attempt. The `qmgr` daemon will wait a while; then it will make several more delivery attempts.
   - **corrupt** This queue contains messages that were damaged somewhere in transit and are no longer readable.

7. The `qmgr` daemon then invokes the trivial-rewrite daemon, which identifies the next MTA or MDA to which the message should be sent.

8. The `qmgr` daemon then passes the message to the appropriate delivery agent. If the message is intended for a local user account, the local agent is used. If the agent intended for another MTA or an MDA, the smtp agent is used.

9. The selected agent transfers the e-mail message to the appropriate system.

- **qmail** The qmail MTA is also a modular MTA daemon that is frequently used as a replacement for sendmail. The qmail MTA is unique in that it was designed from the ground up with security in mind. Essentially, its modular architecture is composed of mutually untrusting components. This means each module in the MTA (such as the SMTP listener) will use a set of credentials that are unique to it. No two modules use the same credentials. Many administrators consider qmail, like postfix, easier to manage than sendmail. However, it’s not the default MTA used by any Linux distribution because it has components that are covered by a proprietary licensing agreement. In spite of this, qmail is greatly loved by those who use it. My niece is married to a system admin and he swears by qmail. You need to be aware that two additional mail protocols are implemented by qmail:
  - **Quick Mail Queueing Protocol (QMQP)** Allows the sharing of e-mail queues among different MTAs
  - **Quick Mail Transport Protocol (QMTP)** A transmission protocol similar to SMTP, but considered to be faster

- **Exim** For your LPIC-1/CompTIA Linux+ exam, you also need to be familiar with the Exim MTA. Exim is a non-modular MTA, composed of only a single program (similar to sendmail). However, it is considered to be much easier to configure and manage than sendmail. A limited number of Linux distributions use Exim as the default MTA.

As mentioned earlier, these MTAs can be used to receive sent e-mail messages from MUAs via SMTP. However, they can’t download messages to e-mail clients via POP3 or IMAP. To do this, you must install the imap package on your system using the software management utility of your choice. This package installs IMAP and POP3 daemons that you can use to transfer messages from your MTA to your e-mail client software.

Both of these daemons are managed using the xinetd daemon. You can enable these daemons using the /etc/xinetd.d/imap file. Once done, restart the xinetd daemon.

**NOTE** We’ll discuss xinetd in more detail in the next chapter.

Whichever MTA you choose to use, each is managed using the appropriate init script in your init directory. For example, the postfix init script is appropriately named postfix, while the sendmail init script is sendmail.

Now that you understand how e-mail works and the role of the MTA, let’s next look at commands you can use to manage MTAs on Linux.

## Using MTA Management Commands on Linux

Let’s first look at reading messages stored in your local MTA. When you log in to a shell session, you will receive a notification if there are mail messages waiting for you. You can read messages for local users from the local MTA directly from the command line using the mail command at the shell prompt. When you do, a list of messages is displayed. An example is shown in Figure 16-14.

**NOTE** Some services running on Linux are configured to send notification messages to the root user.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_672_0.png)
