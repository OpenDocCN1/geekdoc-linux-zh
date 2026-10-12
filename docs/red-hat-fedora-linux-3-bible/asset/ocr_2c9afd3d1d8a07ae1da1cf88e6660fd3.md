The sendmail binary packages are included in the Fedora distribution. The sendmail, sendmail-cf, and sendmail-doc packages are on the Fedora Core 3 DVD that comes with this book. From the Fedora RPMS directory on the DVD, the following command installs the packages:

```
# rpm -Uhv sendmail*
```

# ### Starting sendmail

Once installed, the sendmail service is turned on by default. To start sendmail immediately, you can either reboot the machine or just run `service sendmail start` to start the server. The procedure for starting and stopping sendmail is no different from that of any other server process.

# #### Other Mail Servers for Fedora or Red Hat Linux

The open-source version of sendmail is not the only mail server available for Fedora and other Red Hat Linux systems, but it is definitely the most common. The following list describes other servers and provides URLs for further information:

+   - **Postfix** Like Sendmail, the Postfix MTA is also included with Fedora. Written by Wietse Venema (of tcp_wrappers fame), this free mail server was designed with security in mind and executes most functions as an unprivileged user in a restricted chroot environment. The server encompasses more than a dozen small programs (each performing a simple, distinct task) and several single-purpose queues. You can find more information and source code at www.postfix.org.

+   - **Exim** The Exim MTA is a free mail server (under GPL) that runs on Linux and other UNIX systems. Exim was added to Fedora in Fedora Core 2. This MTA includes flexible features for checking and routing mail. Find out more about Exim from the Exim Home Page (www.exim.org).

+   - **Qmail** Also conceived with security as a high priority, this mail server (written by Daniel J. Bernstein) offers secure and reliable message transfer, mailbox quotas, virtual domains, and antispam features. More information is available from www.qmail.org/torptop.html.

+   - **Sendmail (commercial version)** Sendmail, Inc. (www.sendmail.com) offers products based on the same source code as open-source sendmail, aimed at enterprise e-mail installations. Products include Mailstream Manager (which includes support for enterprise-wide, high-volume mail service with anti-spam and anti-virus features), MailCenter (offering IMAP/POP, Webmail and intelligent inboxes) and Workforce Mail (scalable, policy-based email service for the enterprise).

+   - **Smail** Smail offers many of the same features as sendmail but is somewhat easier to configure and requires less memory. Smail is most appropriate for small to medium size mail servers. The Smail project page is available at