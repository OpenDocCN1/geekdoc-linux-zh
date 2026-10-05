# BASICS 343

leased line. This book deals primarily with the first species, that is, Linux as a private workstation.

If you do not want to spend much time on configuration, and thus opt for an all-rounder among the email programs, and thus for a program that unifies the tasks of mail transport agent and mail user agent. Besides Netscape, the KDE program mail2 also offers this kind of service.

The alternative is to configure a more or less "classical" email system (from the Unix point of view) and optimize it for offline operation. In this case, you will have to familiarize yourself with the programs sendmail and fetchmail. These two programs transmit your email messages to the provider and collect the messages to you.

Although the sendmail/fetchmail variation involves significantly more configuration effort, it definitely has its advantages: first, you now have an unlimited choice of email clients. For example, you can now use the extremely efficient email program (the author's favorite). A later switch to another email program is easily possible. Second, the system can be better automated, that is, sending and receiving of email can be carried out by means of scripts.

This book — as it could be any other way — deals with both variations.

+   Netscape:
Configuration for stand-alone operation: page 348
Configuration as a client for sendmail/fetchmail: page 349

+   KDEMail:
Configuration for stand-alone operation: page 350
Configuration as a client for sendmail/fetchmail: page 351

+   pine:
Configuration as a client for sendmail/fetchmail: page 351

+   sendmail and fetchmail:
Configuration for offline operation: page 359

> A separate mail client for GNOME, named Balsa, is currently developed. Unfortunately, the program could not be taken into account in this edition.

# Where is mail stored?

Caution — this question sounds simpler than it is! The answer is twofold: first, we will discuss email reading, then email sending.

# Reading messages with POP

Let us assume that you have a POP account with an Internet provider. (POP stands for Post Office Protocol and is currently the most common protocol to collect messages from Internet providers.) If a friend sends you an email, the first message arrives at the server of your Internet provider.