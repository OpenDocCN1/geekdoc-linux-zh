
## DISTRIBUTION-SPECIFIC INFORMATION

Caldera, Red Hat, and Debian will each have kppp as long as the KDE packages have been installed. If not, GNOME has a similar tool called gpppon (GNOME PPP on). This utility will be available in any system that includes GNOME and has this utility installed. Debian also includes several other PPP tools, including pppconfig, quickppp, and ppxp (which also has a Tk and X interface). The pppconfig script automates much of what was previously discussed regarding setting up automatic demand dialing (Debian just uses a different chatscript’s directory location).

## TROUBLESHOOTING

- *I set up my automatic dialing just like the example in the book, but I can’t seem to get connected. I can hear it talking to another modem, but then nothing happens.*

  Your ISP is probably looking for something other than what you’re sending or is sending something you’re not looking for. Use a program like cu or another program where you can watch what the ISP is sending (you should also see this in /var/log/messages with debug). Remember that the expect/send sequence is case sensitive. Add any required sequences. At least one ISP uses username instead of login.

- *I did the previous step, and I’m sure the expect/send sequence is correct and in the correct case, but then suddenly the PPP daemon dies.*

  The expect chat sequence might be replying too quickly. Try adding a one-second delay in between the expect and the send. Also try using '\d\c' as the last line.

- *I can’t seem to get the modem to dial out. I put in debug and now I see something about tcsetattr being incorrect.*

  Most likely, you haven’t chosen the correct modem. If you are using /dev/modem, make sure this is a symlink pointing to the correct ttyS device, or the modem is not present. Also make sure the serial module is loaded.

- *I’m getting an error when I start pppd about the kernel not supporting PPP.*

  You probably haven’t installed the ppp_async module. You might also want to install the ppp_deflate and bsd_comp modules as well. Also install either ppp_async or ppp_synctty.

- *When I try to use demand dialing, pppd fails.*

  When using pppd with demand dialing, make sure you’ve built the kernel with slip support or modprobe slip. The demand dialing requires two things: the slip module to set up a pseudo-slip connection to watch for a connection attempt, and a line such as 192.168.10.10:192.168.10.11 in your /etc/ppp/peers/provider (or /etc/ppp/options) file. This provides a temporary target for packets to go to which will trip the automatic dialing.

![](img/c741b1b6b6eccaba2ad43454c979a7f8_477_0.png)

## CHAPTER 25 — EMAIL CLIENTS AND SERVERS

### In this chapter

- Email—What Is It?  460
- How Does Email Work?  460
- User Agents  461
- Mail Transport Agent Configuration  465
- Delivery Agents  472
- Encryption and Pretty Good Privacy (PGP)  474
- Troubleshooting  482

### Email—What Is It?

Setting up electronic mail (email) services on a Linux system is really quite simple. Depending on your objectives, email can be operational upon completing the Linux installation. However, that is not to say that email configuration and operation are simple by any means. The internals of email configuration and the process by which it works are quite complex.

Email, in simple terms, is merely an automated way of delivering conventional mail. In fact, thinking of it in terms of the conventional mail that is delivered by the postal service can actually help you understand what email is and how it works. Conventional mail delivery can be thought of in three distinct parts: sending mail, receiving mail, and transporting mail between one or more intermediate stations en route to its final destination. As a postal service customer, you are typically only involved in either sending mail or receiving it. The steps in between are, for the most part, transparent to you as a customer of the postal service. The postal service handles the intermediate steps of determining how your letter is to be handled and where it is to be delivered. After it is delivered, the recipient retrieves the letter from the mailbox.

> **Note**  
> The topic of email can fill a book. This chapter contains only very basic information. Although slightly Caldera-centric, the text also examines differences in default Debian and Red Hat installations and distribution-specific implementations. Underneath, it all works the same.

### How Does Email Work?

Email works in much the same way as conventional mail. Three distinct agents are involved in this process: the email client (sender), the mail transport agent, and the mail delivery agent (recipient). The email client is often referred to as the *Mail User Agent (MUA)* and the transport agent is often referred to as the *Mail Transport Agent (MTA)*. Each of these agents and their respective tasks are listed in Table 25.1.

**Table 25.1 — Electronic Mail Components**

| Agent | Component | Description |
|---|---|---|
| User Agent (MUA) | Sender | Formats the message, addresses the message, and delivers the message to the Mail Transport Agent. |
| Transport Agent (MTA) | Message Handler | Accepts messages from User Agents and other Transport Agents. Routes the message over appropriate network. Resolves aliases and forwarding. |
| Delivery Agent (DA) | Recipient | Delivers messages to destination accessible by recipient. |

The sender of an email constructs a message, using an email client, and addresses it to a recipient. After the email client sends the message, the Mail Transport Agent (MTA) takes over the process. This is equivalent to dropping off a letter at the post office. Of course, the MTA for email is nothing more than a sophisticated program, unlike the postal service, which has a host of employees and sorting machines and a fleet of vehicles. Caldera, Debian, and Red Hat all use a program called *sendmail* as the default Mail Transport Agent, and although this could change in the future, *sendmail* will likely always be included. Debian also offers Postfix and Zmailer, and Red Hat packages are available for Smail and others, but *sendmail* is still the one that is most commonly used.

> **Note**
>
> *sendmail* was written by Eric Allman at the University of California, Berkeley, and is the most popular email Transport Agent on Linux and UNIX platforms.

The Transport Agent accepts the mail from a user agent, determines the address of the recipient, and delivers the message to the Transport Agent that services email for the recipient. The Delivery Agent is really nothing more than an email client or user agent. However, depending on the setup of incoming email for a given client, an additional component might be necessary. You can be logged in directly to the machine that acts as the email server and read your email on that system, or you can read your email on your desktop system using either Internet Message Access Protocol (IMAP) or Post Office Protocol (POP). You can find more information about these two protocols in the section “Delivery Agents.”

### USER AGENTS

The User Agent is that aspect of email that involves you, individually, as either the sender of a message or the recipient of a message. This is typically the email client that is used to read incoming messages or to compose outgoing messages. The job of the User Agent is really quite simple. In the case of outgoing messages, it’s a matter of providing a method for you to compose a message, address the message to the desired recipient or recipients, and then send the message on its way. Many email clients are available with Linux—both character-based clients and graphical, X Window–based clients. Outbound mail is operational by default after the Linux installation is complete. The only setup that is required is the configuration of an account for each individual user. With the account configured, you can log in and send email. Of course, you’ll need to access an email client in order to complete that task. Choosing an email client is just a matter of preference, and although there is no default email client, there are several from which to choose. Table 25.2 lists some of the many email clients that are available with Linux.

**Table 25.2 — List of Email Clients Available with Linux**

| Email Client | User Interface | Description |
|---|---|---|
| `/bin/mail` | Character | mail is an intelligent mail processing system that has a command syntax reminiscent of ed, with lines replaced by messages. |
| `/usr/bin/elm` | Character | elm is an interactive screen-oriented mailer program that supersedes mail and mailx. |
