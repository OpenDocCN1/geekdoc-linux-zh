can be used by sendmail. If the server is already running, you can simply compile the configuration files and have any new settings take effect without restarting the server.

The following subsections provide details on each of these steps.

# ## Getting a domain name

For people to be able to send mail to the users on your mail server, you must have your own domain name. Chapter 24 describes how to get your own domain names and set up a DNS server. In particular, you want to make sure that the MX record for your domain on the DNS server points to the hostname of your mail server.

> **NOTE:** It is possible that your ISP will not allow you to have a private mail server on your residential Internet account. To enforce this, the ISP may block packets from being addressed to port 25. You may need to contact them to open that port before you can set up a mail server on that connection. Because many spamming and otherwise evil (or at least poorly controlled) e-mail servers try to hide behind dynamic IP addresses, many ISPs will neither allow e-mail addresses from dynamic IP addresses nor accept e-mail sent from those servers.

# ## Configuring basic sendmail settings (sendmail.mc)

Much of the configuration of your sendmail server comes from information in your `/etc/mail/sendmail.mc` file. Because this file sets sendmail default values that can be used in most cases, you may not have to do much with `sendmail.mc`. However, I recommend you step through this section so you understand how your mail server is configured. Also, you must edit this file for sendmail to function as a public server (it only listens on local ports by default).

Changes you make to the `sendmail.mc` file do not immediately take effect. First you must compile the `sendmail.mc` settings to generate the `/etc/mail/sendmail.cf` file. I describe how to do that in the section “Starting sendmail and generating database files.”

The resulting `/etc/mail/sendmail.cf` file contains over 1,800 lines of settings and comments that are used to direct the behavior of your sendmail daemon. The `m4` macros you use in the `sendmail.mc` file are different from the resulting settings in the `sendmail.cf` file.

> **NOTE:** The `m4` utility can be used to process text files containing macros in IEEE Standard 1003.1-2001 format (Section 12.2, Utility Syntax Guidelines). This compiler is particular about how you use single quotes versus backticks, so be careful editing `sendmail.mc`. For details on the `m4` utility, type `info m4`.

To find out which macros to use for a setting you find in the `sendmail.cf` file, refer to the `/usr/share/doc/sendmail*/README.cf` file.