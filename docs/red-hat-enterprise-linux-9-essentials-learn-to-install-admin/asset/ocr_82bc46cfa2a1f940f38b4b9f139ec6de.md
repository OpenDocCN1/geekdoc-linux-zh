# 30. Configuring a RHEL 9 Postfix Email Server

Along with acting as a web server, email is one of the primary uses of a RHEL 9 system, particularly in business environments. Given the importance and popularity of email, it is surprising to some people to find out how complex the email structure is on a Linux system. This complexity can often be overwhelming to the RHEL 9 newcomer.

The good news is that much of the complexity is there to allow experienced email administrators to implement complicated configurations for large-scale enterprise installations. However, for most Linux administrators, setting up a basic email system is relatively straightforward so that users can send and receive electronic mail.

This chapter of Red Hat Enterprise Linux 9 Essentials will explain the basics of Linux-based email configuration and step through configuring a basic email environment. To provide the essentials, we will leave the complexities of the email system for more advanced books on the subject.

# 30.1 The Structure of the Email System

Several components make up a complete email system. Below is a brief description of each one:

# 30.1.1 Mail User Agent

The typical user will likely be most familiar with this part of the system. The Mail User Agent (MUA), or mail client, is the application that is used to write, send and read email messages. Anyone who has written and sent a message on any computer has used a Mail User Agent of one type or another.

Typical Graphical MUAs on Linux are Evolution, Thunderbird, and KMail. For those who prefer a text-based mail client, there are also the more traditional Pine and mail tools.

# 30.1.2 Mail Transfer Agent

The Mail Transfer Agent (MTA) is the part of the email system that transfers email messages from one computer to another (either on the same local network or over the internet to a remote system). Once configured correctly, most users will only directly interact with their chosen MTA if they wish to re-configure it. Many MTA choices are available for Linux, including Sendmail, Postfix, Fetchmail, Qmail, and Exim.

# 30.1.3 Mail Delivery Agent

Another part of the infrastructure typically hidden from the user, the Mail Delivery Agent (MDA), sits in the background and performs filtering of the email messages between the Mail Transfer Agent and the mail client (MUA). The most popular form of MDA is a spam filter to remove all