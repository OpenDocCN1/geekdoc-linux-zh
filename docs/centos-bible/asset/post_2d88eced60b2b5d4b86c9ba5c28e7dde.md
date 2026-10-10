
# Part IV Networking

that you're not running a vulnerable sendmail daemon. Also, the expn and vrfy commands (which can be disabled via a configuration option) could give out more information than you'd care to distribute.

```
May 16 13:03:27 dale sendmail[699]: NOQUEUE: "wiz" command from localhost [127.0.0.1] (127.0.0.1)
May 16 13:03:29 dale sendmail[699]: NOQUEUE: "debug" command from localhost [127.0.0.1] (127.0.0.1)
May 16 13:03:37 dale sendmail[701]: NOQUEUE: localhost [127.0.0.1]: expn oracle
May 16 13:03:43 dale sendmail[702]: NOQUEUE: localhost [127.0.0.1]: vrfy oracle
```

## Configuring Sendmail

To configure the Sendmail facility, you edit configuration files in /etc/mail/ and /etc/ that are then used by the Sendmail startup script to generate database files. Those database files are, in turn, used by the sendmail daemon to control the behavior of your Sendmail server. Once Sendmail is configured, you can begin adding user accounts to have mailboxes on your server. The general steps I describe in this section for configuring Sendmail are:

- 1. **Getting a Domain Name** — You need a unique Internet domain name to assign to your mail server. You can purchase an Internet domain name from one of many different places, and then have DNS Mail eXchange (MX) records for your domain point to the mail server you are creating.

- 2. **Configuring Basic Sendmail Settings** — In this step, you edit the /etc/mail/sendmail.mc file. That file defines such things as the locations of other configuration and log files, as well as lets you configure some behavior of the sendmail daemon.

- 3. **Defining Outgoing Mail Access** — The most critical security issue associated with your mail server is which mail messages it will accept to relay to other mail servers. By editing the /etc/mail/access file, you can indicate the hosts and users from which your server will accept mail for local delivery or relay.

- 4. **Configuring Virtual Servers** — By default, Sendmail assumes that you are setting up the mail server for the domain of which the server is a member. To have Sendmail on a single computer be the mail server for multiple domains (referred to as *virtual servers*), you need to define each domain name in the /etc/mail/local-host-names file. (You must create local-host-names manually, since it is not in the sendmail package.)

- 5. **Configuring Virtual Users** — Using the /etc/mail/virtual/ustable configuration file, you can instruct the sendmail daemon what to do with the mail it receives for the users and domains that it's configured to handle. This file gives you a lot of flexibility to take mail addressed to a particular user and direct it to a particular mailbox, forward it to a different mail address, or reject that mail in various ways. To use virtual/ustable, you must create the file manually, since it is not in the sendmail package.

- 6. **Adding User Accounts** — You need to add a user account for every user that has a mailbox on your mail server.

- 7. **Starting Sendmail and Generating Database Files** — Starting the Sendmail service causes two major actions to happen. It runs the `sendmail` server daemon, and it compiles your configuration files into database files that can be used by Sendmail. If the server is already running, you can simply compile the configuration files and have any new settings take effect without restarting the server.

The following subsections provide details on each of these steps.

### Getting a Domain Name

For people to be able to send mail to the users on your mail server, you must have your own domain name. Chapter 24 describes how to get your own domain names and set up a DNS server. The critical issue for your mail server is to make sure that the MX record for your domain on the DNS server points to the address of your mail server.

> **NOTE**: It is possible that your ISP will not allow you to have a private mail server on your residential Internet account. To enforce this, the ISP may block packets from being addressed to port 25. You may need to contact them to open that port before you can set up a mail server on that connection. Because many spamming and otherwise evil (at least poorly controlled) e-mail servers try to hide behind dynamic IP addresses, many ISPs will neither allow e-mail addresses from dynamic IP addresses nor accept e-mail sent from those servers.

### Configuring Basic Sendmail Settings (sendmail.mc)

Much of the configuration of your Sendmail server comes from information in your `/etc/mail/sendmail.mc` file. Because this file sets Sendmail default values that can be used in most cases, you may not have to do much with `sendmail.mc`. However, I recommend that you step through this section so you understand how your mail server is configured.

Changes you make to the `sendmail.mc` file do not immediately take effect. First, you must compile the `sendmail.mc` settings to generate the `/etc/mail/sendmail.cf` file. I describe how to do that in the “Starting Sendmail and Generating Database Files” section.

The resulting `/etc/mail/sendmail.cf` file contains more than 1,800 lines of settings and comments that are used to direct the behavior of your `sendmail` daemon. The `m4` macros you use in the `sendmail.mc` file are different from the resulting settings in the `sendmail.cf` file.

> **NOTE**: The m4 utility can be used to process text files containing macros in IEEE Standard 1003.1-2001 format (Section 12.2, “Utility Syntax Guidelines”). This compiler is particular about how you use single quotes versus backticks, so be careful editing `sendmail.mc`. For details on the m4 utility, type `info m4`.

To find out which macros to use for a setting you find in the `sendmail.cf` file, refer to the `/usr/share/doc/sendmail*/README.cf` file.

> **CAUTION**: Because of the way *Sendmail* is configured in CentOS, you should not directly modify the *sendmail.cf* file. The *sendmail.cf* file is regenerated automatically when *Sendmail* restarts is *sendmail.mc* changes. As a result, any modifications made directly to *sendmail.cf* will be lost.

The following code samples are from the */etc/mail/sendmail.mc* file that accompanies the CentOS version of *Sendmail*.

> **NOTE**: Lines that begin with *dnl* (“delete to new line”) in the *sendmail.mc* file are comment lines. In most cases, I have left them out in the examples shown. Also, notice that *Sendmail* uses backticks as opening quotes and straight quotes as ending quotes.

```
divert(-1)dnl
include(`/usr/share/sendmail-cf/m4/cf.m4')dnl
VERSIONID(`setup for linux')dnl
OSTYPE(`linux')dnl
```

The first few lines of the *sendmail.mc* file do some housekeeping. The `divert` line removes extra output when the configuration file is generated. The `include` line causes rule sets needed by `Sendmail` to be included. The `VERSIONID` line identifies the configuration file as being for Linux systems, such as `CentOS` (although this setting is not checked, so it could be anything you like). The `OSTYPE`, however, must be set to `linux` to get the proper location of files needed by `Sendmail`.

```
dnl define(`confSMTP_LOGIN_MSG', '$j Sendmail; $b')dnl
dnl define(`SMART_HOST', `smtp.your.provider')
```

Here are two lines you can consider uncommenting (removing the `dnl` string). The `confSMTP_LOGIN_MSG` definition can be used to disguise the mail server you are using (change `Sendmail` to whatever). As for the second line, by default, the `sendmail` daemon tries to send your outgoing e-mails directly to the mail server to which they are addressed. If you want all e-mail to be relayed through a particular mail server instead, you can remove the comment (`dnl`, which stands for “delete to new line”) from the beginning of the `SMART_HOST` line above (leave the one at the end). Then, change `smtp.your.provider` to the fully qualified domain name of the mail server you want to use. Of course, you need to be sure that the `SMART_HOST` you define will accept relays from your mail server.

```
define(`confDEF_USER_ID', `8:12')dnl
```

Instead of running as the `root` user, the daemon runs as the `mail` user (UID 8) and `mail` group (GID 12), based on the `confDEF_USER_ID` line set previously. This is a good policy, because it prevents someone who might compromise your mail server from gaining root access to your machine.

```
dnl define(`confAUTO_REBUILD')dnl
define(`confIO_CONNECT', `1m')dnl
```
