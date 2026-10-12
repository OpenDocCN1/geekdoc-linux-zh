# ## Other Mail Servers Available for Red Hat Linux

The open-source version of sendmail is not the only mail server available for Red Hat Linux, but it is definitely the most common. Other servers are described in the following list, with URLs that provide further information.

+   * **Postfix** — The Postfix MTA is the only mail-server software besides Sendmail that comes with Red Hat Linux. Written by Wietse Venema (of tcp_wrappers fame), this free mail server was designed with security in mind and executes most functions as an unprivileged user in a restricted chroot environment. The server encompasses more than a dozen small programs (each performing a simple, distinct task) and several single-purpose queues. Information and source code can be found at www.postfix.org.

+   * **Exim** — The Exim MTA is a free mail server (under GNU) that runs on Linux and other UNIX systems. This MTA includes enhanced protection against unsolicited junk mail and mail bombs. Find out more about Exim from the Exim Home Page (www.exim.org).

+   * **Qmail** — Also conceived with security as a high priority, this mail server (written by Daniel J. Bernstein) offers secure and reliable message transfer, mailbox quotas, virtual domains, and antispam features. More information is available from www.qmail.org/top.html.

+   * **Sendmail (commercial version)** — Based on the same source code as open-source sendmail, this product is distributed as binary executables built specifically for Red Hat Linux (among other Linux and UNIX variants). Pricing for the Sendmail Advanced Message Server is based on the number of mailboxes you are serving. The product offers simple installation, Web-based management, and support. Details can be found at www.sendmail.com.

+   * **Smail** — Smail offers many of the same features as sendmail but is somewhat easier to configure and requires less memory. The source code can be downloaded from ftp://ftp.planix.com/pub/Smail/.

Incoming messages received by sendmail are processed and stored in the /var/spool/mail directory. Each file in this directory represents a valid user name on the local machine. The file is created automatically when you add a user. People with login accounts use this directory and their user account name as their incoming mailboxes (for example, /var/spool/mail/johnq).

Outgoing messages go in /var/spool/mqueue directory while waiting to be sent. Filenames in this directory follow a consistent naming scheme. The first two characters indicate what type of data is stored in the file (see Table 19-1). Subsequent characters form a