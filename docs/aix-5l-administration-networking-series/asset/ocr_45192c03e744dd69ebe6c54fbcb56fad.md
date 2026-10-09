intuitive interface, these GUIs often directly support mail delivery protocols such as POP and IMAP. However, command-line MUAs remain important, even in an environment where end users have advanced graphical interfaces, because they can be used easily in shell scripts to automate system reporting. Command-line utilities are also handy for debugging MTA configuration issues.

In the following sections, where reference is made to an MUA, assume basic UCB mail functionality and options. Default configuration options for this program are defined via the `/usr/lib/Mail1.rc` file. Each user may override the global defaults by resetting the options in a local `$HOME/.mailrc` file. The following is a configuration file for MUA:

```
# /usr/lib/Mail.rc
# Options
set ask askok dot save keep crt
# Don't display the following header lines
ignore Received Message-Id Resent-Message-Id
ignore Status Mail-From Return-Path Via
```

# Mail Delivery Agents and Protocols

While **sendmail** will queue mail for delivery and route mail to other systems, it does not actually deliver the mail to the end user. For this task, **sendmail** relies on a *mail delivery agent (MDA)*. Using an external program for delivery allows for greater flexibility in supporting both legacy systems and evolutionary change. In this way, **sendmail** supports UUCP users (a legacy system) and **procmail** users (a newer delivery agent that supports greater user customization). Although not included in the AIX base operating system, **procmail** is provided free from IBM on the *AIX Toolbox for Linux Applications* CD-ROM detailed in Chapter 16. In the *sendmail* configuration file, the MDA is referred to as a **MAILER**, and **mailutil** is the default MDA for local delivery.

Additional remote mail delivery protocols, POP and IMAP, have become very popular. These protocols allow mail users the potential to access their mailboxes from any computer on the network, regardless of hardware architecture or operating system. The difference between them lies in how they treat the mailbox: POP implements a distributed mailbox, pulling new messages from a central server; IMAP implements remote access to a centralized mailbox. IMAP makes the central mailbox available to the users, keeping both read and unread messages in the central location. POP typically allows the user to download new messages to whatever computer that user happens to be using at that moment, never to be available again from any other computer. For this reason, IMAP is more popular in open campus environments. POP and IMAP daemons are distributed with recent versions of the AIX base operating system.

# SENDMAIL COMPONENTS

The standard MTA on AIX is **sendmail** (version 8.11 as of AIX 5.1). The **sendmail** program was originally written by Eric Allman at the University of California, Berkeley,