# Part IV Networking

```
that you're not running a vulnerable sendmail daemon. Also, the expn and vrfy commands (which can be disabled via a configuration option) could give out more information than you'd care to distribute.

May 16 13:03:27 dale sendmail[699]: NOQUEUE: \\"wiz\\" command from localhost [127.0.0.1] (127.0.0.1)
May 16 13:03:29 dale sendmail[699]: NOQUEUE: \\"debug\\" command from localhost [127.0.0.1] (127.0.0.1)
May 16 13:03:37 dale sendmail[701]: NOQUEUE: localhost [127.0.0.1]: expn oracle
May 16 13:03:43 dale sendmail[702]: NOQUEUE: localhost [127.0.0.1]: vrfy oracle
```

# Configuring Sendmail

To configure the Sendmail facility, you edit configuration files in /etc/mail/ and /etc/ that are then used to by the Sendmail startup script to generate database files. Those database files are, in turn, used by the sendmail daemon to control the behavior of your Sendmail server. Once Sendmail is configured, you can begin adding user accounts to have mailboxes on your server. The general steps I describe in this section for configuring Sendmail are:

+   1.  **Getting a Domain Name** — You need a unique Internet domain name to assign to your mail server. You can purchase an Internet domain name from one of many different places, and then have DNS Mail eXchange (MX) records for your domain point to the mail server you are creating.

+   2.  **Configuring Basic Sendmail Settings** — In this step, you edit the /etc/mail/sendmail.mc file. That file defines such things as the locations of other configuration and log files, as well as lets you configure some behavior of the sendmail daemon.

+   3.  **Defining Outgoing Mail Access** — The most critical security issue associated with your mail server is which mail messages it will accept to relay to other mail servers. By editing the /etc/mail/access file, you can indicate the hosts and users from which your server will accept mail for local delivery or relay.

+   4.  **Configuring Virtual Servers** — By default, Sendmail assumes that you are setting up the mail server for the domain of which the server is a member. To have Sendmail on a single computer be the mail server for multiple domains (referred to as *virtual servers*), you need to define each domain name in the /etc/mail/local-host-names file. (You must create local-host-names manually, since it is not in the sendmail package.)

+   5.  **Configuring Virtual Users** — Using the /etc/mail/virtual/ustable configuration file, you can instruct the sendmail daemon what to do with the mail it receives for the users and domains that it's configured to handle. This file gives you a lot of flexibility to take mail addressed to a particular user and direct it to a particular mailbox, forward it to a different mail address, or reject that mail in various ways. To use virtual/ustable, you must create the file manually, since it is not in the sendmail package.