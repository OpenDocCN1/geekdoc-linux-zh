
Of course, these could be the same Linux system, and they often are. In the example, two different systems are used to emphasize the two major server roles.

## Figure 2.2 A PC client configuration

![](img/9639113aa446fb8976cb3d377f7aafdd_62_0.png)

Often the simple view of the configuration seen from a Windows client does not reflect the true e-mail architecture of a network. In the next section, we examine two sample networks to put together the components of e-mail architecture into context.

## Sample Mail Architectures

The first sample architecture can be seen in Figure 2.3. It shows an engineering department in which every user has a Linux desktop. The cloud represents the outside world. The directional arrows indicate the flow of mail into and out of each system. This figure illustrates, each Linux system is acting as its own server. It collects inbound mail and sends outbound mail for its own users. It does not, however, act as a relay or hub for any client systems or for any users on other systems.

## Chapter 2 Understanding E-Mail Architecture

## Figure 2.3 A sample engineering department

![](img/9639113aa446fb8976cb3d377f7aafdd_63_0.png)

This configuration is surprisingly easy to create because it's the default configuration of a Linux system running Sendmail. The default Linux configuration runs the Sendmail daemon, which provides an SMTP listener on port 25 to collect inbound mail, and all of the MUAs running on Linux know about Sendmail and use it to send outbound mail. Further, the default Sendmail configuration blocks relaying from outside systems.

The configuration for the engineering department is simple, but maintenance is complex. Every system needs to be kept up to date with the latest Sendmail patches. In a department with just a few systems this is not too bad, but if the network grows very large, keeping all of the systems updated could be a big headache. To cope with a configuration like this you need sophisticated users who can help with the maintenance, which is why we showed this as a configuration for a small engineering department. Less sophisticated users require a more complex architecture.

Figure 2.4 shows a sales department. Pre- and post-sales technical personnel and all sales people get Linux desktops. Sales trainees and clerical personnel get Windows desktops. The dashed arrows indicate that the Windows clients periodically retrieve mail from the server using POP or IMAP; the solid arrows to the Linux clients indicate that mail is immediately forwarded to clients via SMTP.

The server is configured as both a relay and a mailbox server. The relay configuration is carefully created so that all systems within the local network can relay through the server but no remote systems can relay mail though the server. The server is also configured to forward all of the mail it receives for its Linux clients to those clients. The Linux clients are configured to send all outbound mail through the server. (In Sendmail configuration, all mail can be sent through a single server by defining a SMART_HOST value in the configuration of the client.)

## Figure 2.4 A sample sales department

![](img/9639113aa446fb8976cb3d377f7aafdd_64_0.png)

The fact that all mail flows through one server simplifies maintenance. Patches can be applied to a single system and yet benefit the entire network. Mail can be filtered at a single point. If a firewall is put in place, it only needs to allow mail through to a single system. The biggest problem with this configuration is that it creates a potential point of failure.

In these two sample networks, Sendmail systems are used as both clients and servers. Sendmail performs multiple tasks that are essential for efficient mail delivery, and Sendmail systems take on multiple roles in the e-mail architecture.

## Sendmail’s Roles

MSA, MTA, relay, and server are all terms used to describe the functions of components within the e-mail architecture. These words will appear again and again throughout this book. Understanding them is essential. Sendmail also has its own language to describe the functions it performs. Mailers, rewriters, rewrite rules, and aliasing are all words used to describe the work that Sendmail does. To read this book and understand the role of Sendmail, you need to know what each of these terms means. This section introduces “Sendmail speak” and links this new terminology to the roles that Sendmail plays in the e-mail architecture.

The tasks that a Sendmail server performs can be divided into two basic functional groups: the roles that Sendmail performs as a message submission agent and as a message transport agent. The distinctions between these roles can be subtle, and the roles sometimes overlap. But these two basic roles incorporate all of the tasks performed by a Sendmail server and help explain what various configuration values do and why they need to be defined. Much of the Sendmail configuration is used to specify how Sendmail should handle its duties as a message submission agent.

## A Message Submission Agent

The functions of Sendmail described in this section might not meet the RFC definition of an MSA, but they come close. An MTA that accepts a message directly from an MUA and takes an active role in formatting a complete mail message is an MSA.

- accepts mail from an MUA
- determines the delivery program for the mail
- reformats the mail addresses for the selected mailer
- adds the headers required by the mailer
- sends the message to the mailer for delivery

In this book I'm using "message submission agent" (the MUA) to describe the role that Sendmail fills as the interface between the user's e-mail program (the MUA) and the mail delivery program (the MTA). Even when Sendmail is the MTA, things must be done to the mail received from the MUA to prepare for delivery, and of course, Sendmail is not the only MTA that can run on a Linux system. A user can create a wide variety of mail with an e-mail program. The mail entered by the user could be local mail bound for another user; it could be Internet mail bound for a remote user; it could be data bound for a Linux program; to prepare for delivery. (See Appendix A, "Macro Command Reference," for a full list of the mailers supported by Sendmail.) All that a supported mail program running on a Linux system needs to do is pass the mail message to Sendmail. Sendmail is equipped to select the appropriate delivery agent and to properly prepare the mail for delivery.

## Sendmail Mailers

The mail delivery programs are called mailers in Sendmail terminology. The mailers available to Sendmail are defined inside the Sendmail configuration file. A mailer definition assigns an internal mailer name to a mail delivery program. These names are arbitrary, but most Linux systems use the standard mailers defined by the default Sendmail configuration. Chapter 5, "Understanding a Vendor Configuration," describes each of the mailers. A mailer definition also provides Sendmail with the full pathname of the delivery program and the command-line arguments Sendmail should use when it launches the mailer. If the delivery program is Sendmail itself, as it is for all of the SMTP mailers, symbolic name, either IPC, which stands for Inter-Process Communication, or TCP, which stands for Transmission Control Protocol, is used instead of a pathname. Mailer definitions take up substantial portion of the Sendmail configuration. Each mailer provides the instructions that Sendmail needs to properly prepare a message for the mailer. This includes the commands used to process sender and recipient addresses. There are also flags associated with each mailer. The flags define optional processing required by the mailer and identify the message needed for the mailer. The number and type of headers vary from mailer to mailer. The Sendmail configuration contains several mailers. Sendmail must select the correct mailer to deliver a piece of mail.

## Determining the Delivery Triple

When Sendmail receives a piece of mail from an MUA, it determines what mailer will deliver the mail. Sendmail determines this from the delivery address. It does this by literally converting the delivery address into a delivery triple. A delivery triple contains up to three values:

- the recipient's e-mail address
- the name of the mail server to which the mail will be sent
- the internal name of the mailer that will deliver the mail

You can see the delivery triple that is produced for any given address by running the sendmail command with the -bv option and the address you processed. Listing 2.1 shows the output of sendmail -bv for two different addresses.

## Listing 2.1 Examining the Delivery Triple

```
$craig$ sendmail -bv ed@xy.com
ed@xy.com... deliverable: mailer smtp, host xy.com, user ed@xy.com
$craig$ sendmail -bv craig
craig... deliverable: mailer local, user craig
```
