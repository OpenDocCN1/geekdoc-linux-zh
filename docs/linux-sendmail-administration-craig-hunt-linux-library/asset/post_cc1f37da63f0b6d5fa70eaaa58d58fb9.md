
# Chapter 2 Understanding E-Mail Architecture

Another level of aliasing occurs after the recipient is processed through the aliases database defines mail forwarding for the entire system. The .forward file, which can be created in any user's home directory, defines mail forwarding for an individual user. Once Sendmail identifies the user to which the mail will be delivered, it looks for a .forward file in the user's home directory. If the .forward file is found, the mail is forwarded to the e-mail address contained in that file. If the file is not found or empty, the mail is delivered directly to the user's account.

> NOTE The aliases database, the local-host-names file, and the .forward file are all described in Chapter 6, "Using Sendmail Databases."

The Sendmail terms "forwarding" and "relaying" are often used interchangeably, but there is a slight difference. Forwarding refers to the act of transferring to another host mail that was originally addressed to the local host. For example, if mail addressed to norm the local host is sent to normane@hawk.foobirds.org as a result of aliasing, it would say the mail has been forwarded to hawk.foobirds.org. Relaying, which is the next topic, is subtly different.

# Mail Relaying

Relaying occurs when mail is transferred onward toward its destination and the source nor the destination of the mail is the address of the local system. For example: If a server named wen.foobirds.org receives mail from ibis.foobirds.org that is addressed to craig@wrotethebook.com and re-sends mail to the host wrotethebook.com, it is acting as a mail relay.

At one time mail relaying was the default configuration for Sendmail systems, but not. Spammers used unsuspecting mail servers to relay their spam in order to hide the true origin of the nuisance mail. Now the default configuration is to relay no mail at all. In Figure 2.1, the sample systems use this default configuration. Each system sends its own e-mail. None of the systems accepts mail for relaying from any other system. It is up to you to loosen those restrictions if you need to provide mail relay for some of your clients. (Proper relay configuration is described in Chapter 11.) In Figure 2.2, the server is configured as a relay for the systems on the local area network.

By default, Sendmail does not relay mail. A server accepts mail addressed to the server itself or any of its local hostname aliases. It rejects all other mail. To relaying, the specific names of the hosts or domains that should be allowed to relay mail must be provided by Sendmail. The hostnames of relay clients can be provided in the relay-domains file or through the access database. Both of these files are covered in Chapter 6.

![](img/9639113aa446fb8976cb3d377f7aafdd_71_0.png)

# A Client

One possible role for a Linux system running Sendmail that is frequently overlooked is the role of a client. By default, every Linux system is a Sendmail server. It is a limited server, because it is set up to handle only mail from users who are directly logged in to the system, but it is a server nonetheless. Turning a Linux system into a true client takes some configuration effort, while the nullclient configuration is touched upon in Chapter 9, the true focus of this book is to properly configure the Sendmail server functions for every Linux system from a laptop to an enterprise server.

# In Sum

The SMTP protocol runs on top of the TCP protocol. TCP is a reliable, connection-oriented protocol. It ensures that mail is always delivered, and it means that SMTP delivers mail to the remote system without dependence on intervening systems. This is a great mail-delivery model because it provides immediate feedback from the remote server whether or not the mail was successfully delivered. However, this system demands a remote system that is fully capable of accepting SMTP mail. Unfortunately, that is not always the case. Sendmail queries DNS and uses the MX records it provides to route mail to a fully capable server for systems that cannot handle their own SMTP mail.

The fact that both direct delivery to end systems and delivery to intervening mail servers are available to Sendmail creates the possibility of a variety of e-mail architectures. There are clients and servers, and the servers can be described in several different ways. Servers that collect inbound mail are described as hubs or mailbox servers. Servers that handle outbound mail are called relays or simply servers. To clarify the vagueness of this language, Internet standards define the functions of message user agents (MUAs), message submission agents (MSAs), and message transfer agents (MTAs).

Even with the narrowly defined terms MUA, MSA, and MTA, there can be confusion because most functions do not match any definition exactly. Various functions overlap across systems and are not easily tied in neat packages. The easiest way to making the language of e-mail architecture simple is to use a little judgment. Don't be too rigid in interpreting the meaning of a term. Always look at things in context. Sendmail frequently uses the same word to describe two different things. Context is the clue to understanding.

Sendmail is the software that turns a Linux system into an e-mail server. It acts as an MSA and an MTA and can even be used as an MUA. Chapter 3, “Running Sendmail,” looks at how Sendmail is installed on a Linux system and how it is run once it is installed.

# Running Sendmail

Chapter 2, “Understanding E-Mail Architecture,” illustrates the importance of Sendmail for a Linux system. Sendmail implements the SMTP protocol for Linux systems. It sends and receives SMTP mail for the system, and it acts as an interface between the user's mail program and the Internet. These vital tasks make Sendmail a basic component of most Linux systems.

Sendmail is an essential part of a Linux system that it is usually installed by default and run at start-up. If it is not installed on your system, you need to know how to install it. Additionally, you need to know how to compile the Sendmail program for those times when you want to install the latest source code distribution of Sendmail on an existing Linux system. This chapter covers both of these topics. It also examines how and why the Sendmail process runs at start-up daemon, and you'll look at the tools used to control whether or not starting the Sendmail daemon is part of the Linux boot process on your system.

# Running Sendmail at Start-Up

Sendmail runs in two distinct modes: real-time mode for outbound mail and daemon mode for inbound mail and queue processing. When a mail user agent (MUA) has mail to send, it creates an instantiation of the Sendmail program to deliver that piece of mail. If it cannot successfully deliver the mail long enough to deliver that one piece of mail, it writes the mail to the mail queue and terminates. Most Sendmail processes have a short life. The Sendmail daemon, on the other hand, runs the entire time the system is running, constantly listening for inbound mail and periodically processing the queue to deliver undelivered mail. The Sendmail daemon, like other daemons, is started at boot time.

The ps command reveals whether or not Sendmail is running on your system:

```
[root]# ps -C Sendmail
PID TTY      TIME CMD
542 ?       00:00:36 sendmail
```

The low process ID (PID) shows that this process was started during the boot. Running this ps command on Linux will show that Sendmail is running because, generally, Sendmail becomes part of the boot process when you first install Linux. Many systems are running the Sendmail daemon unnecessarily. It is not necessary to run Sendmail as a daemon in order to send mail. Running the sendmail command with -bd option is required only if your system directly receives SMTP mail. A Linux mail client can collect inbound mail from the mailbox using POP or IMAP and relay outbound mail through the mail relay server without running the Sendmail daemon. Deciding which systems should run the Sendmail daemon is part of planning your e-mail architecture. Unneeded daemons consume system resources and provide holes through which intruders can slide. Take care when selecting systems really any daemon, including Sendmail.

It is possible to disable Sendmail after the system is installed, and there are easy tools to do this. These tools vary on the type of start-up procedures used. Some Linux systems use BSD-style start-up procedures, while others use V-style procedures.

On Linux distributions that use V-style boot procedures, the script that starts Sendmail is usually found in the /etc/rc.d/init directory, where it is stored under a name as sendmail, or mta. On distributions that use BSD-style boot procedures, the commands that start Sendmail are stored in one of the rc scripts. For example, on Solaris 4.0, the commands to start Sendmail are found in the /rc.m script located in the /etc/rc.d directory. Regardless of the name of the script used for this purpose, some start-up script is used to start Sendmail at boot time.
