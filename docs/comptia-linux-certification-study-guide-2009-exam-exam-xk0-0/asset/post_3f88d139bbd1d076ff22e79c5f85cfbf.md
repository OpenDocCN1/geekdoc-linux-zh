
## 1. Start the CUPS interface by typing the URL `http://localhost:631` into a browser.
## 2. Click on the **Administration** tab.
## 3. Under the *Basic Server Settings*, make sure that the option *Allow users to cancel any job (not just their own)* is checked.
## 4. Click on **change settings**.
## 5. When prompted, type the **super username** and **password**.
## 6. The CUPS server will restart, and then any user can cancel a job.

# Mail

The e-mail server will be an important part of any network, and very useful in a small or home office environment. A distinction should be made between the e-mail server and client – a well-configured e-mail server will be able to have a number of different clients seamlessly connecting to it. This will be very useful in organization where there are mixed systems (Linux, Microsoft Windows, Apple Macs, and so forth). This section will only touch on the clients where it is necessary to see the application working, and will not concern itself with their configuration.

This chapter describes the setting up of the `sendmail` mail transport system; however, there are many others available for Linux, such as postfix, which are very popular. Learning the basics with one will, however, give you a very good advice on how to set up different servers. The first step in setting up a mail server for a domain does not involve the server at all. Initially, the DNS for your domain needs to be configured to ensure that there is a valid MX record pointing at your mail server (or where it will be).

The main transport mechanism for e-mail around the Internet and between e-mail servers is the Simple Mail Transfer Protocol (SMTP), which operates on port 25. The basic protocol has been around a number of years, although a number of extensions have been added for authentication and error reporting, among others. The mail is transferred from one e-mail server to another using a Mail Transfer Agent (MTA); sendmail, postfix, and others are classed as MTAs.

The Post Office Protocol (POP) and Internet Message Access Protocol (IMAP) protocols can be used by the local e-mail clients to retrieve their e-mail from a remote server. Currently, these are the two most prevalent protocols for e-mail retrieval. These can be used to connect to your local server, as well as Web-based mail servers such as Gmail. POP3 is the latest approved standard release of POP, and has addressed some of the security issues that were inherent in the original releases. POP4 has been developed, but is not an approved standard at the time of writing. However, it is still not totally secure, and care should be taken when using it across an unsecured network.

The IMAP protocol has gained in popularity over the years, and is now offered by Web providers such as Gmail (as well as POP3) and for local servers such as Microsoft Exchange. IMAP will be much faster to download mail on a local network compared with POP3.

# How Mail Works

Any mail server in your organization will ideally need to handle both incoming and outgoing mails. The mail arrives at your mail server for the domain(s) it looks after, defined in part by the DNS MX record. Users within this domain will have usernames associated with their mail account. While you may find it useful to give people their first name like Fred and Mary, this will not work when the company grows larger. It is therefore useful to define a scheme before setting up the server, perhaps first.lastname (or whatever works for your organization). The full e-mail address will then be username@your domain. E-mail will then be stored on the server until the user successfully retrieves them using an e-mail client.

Outgoing mail will be handled slightly differently. If a user sends an e-mail destined for a local user, the mail server will simply put the e-mail in the appropriate user’s mailbox, where they can retrieve it as above. If it is for someone outside the domain, the mail server will look up the MX record of the target domain and then try to send or relay the mail message to that server.

# Sendmail

Sendmail has been around for a number of years and has grown in complexity to keep up with the demands of users in requiring more sophisticated mail. The following sections will outline how to set up a sendmail server.

# Starting and Stopping Sendmail

Sendmail is usually started upon boot, but can also be started and stopped afterwards. This is especially important when configuration changes are made, as sendmail will only read the configuration file once when it starts. The commands below are used to start, stop, and restart sendmail.

```bash
service sendmail start
service sendmail stop
service sendmail restart
```

# Sendmail Configuration

The basics of sendmail configuration will be given here, but it should be noted that `sendmail` is very complex with whole books devoted to the correct set up. Mistakes in the sendmail configuration file can cause sendmail to stop processing mail, so performing a backup is advisable. The main sendmail configuration file is `sendmail.cf`, which is now normally located in `/etc/mail/sendmail.cf` (and in `/etc/sendmail.cf` in some older versions of Linux). This file can be edited directly, but the syntax can be confusing and, as stated above, mistakes may stop the server from working.

A common method of producing the sendmail.cf file is through use of the m4 macro processor, which works on the configuration parameters in the file `/etc/mail/sendmail.mc`. While a lot easier than editing the sendmail.cf file directly, it is by no means simple. Methodical working through the file and observing the logs when you start sendmail are recommended. As the complete list of commands is large, we will concentrate on a few often-used ones.

# Smart Hosts

While the relative cost of an always-on Internet connection, such as cable or leased line, has reduced in the past few years, this is favored by a lot of companies. However, this is not the case in many parts of the world. In addition, what happens if you are trying to send e-mail to a company who has their e-mail server turned off? In these cases, you can configure `sendmail` to pass mail onto another sender rather than delivering it directly. In the sendmail.mc file, the following need to be added:

```m4
dnl # define the Smart Host
define(`SMART_HOST', 'smtp.smarthost.org')
```

In the above, the line starting `dnl` means *do not list*, and basically tells the m4 macro processor to put the rest of the line in as a comment. The define section will tell sendmail to pass its mail to the server `smtp.smarthost.org` for onward delivery.

# Mail Delivery Intervals

You may wish sendmail to deliver mail at certain times as opposed to it trying to deliver the e-mail instantly it receives it, as the default is. This may be useful to reduce the load on the network, or if you do not have an always-on connection. The sendmail.mc file should be edited as follows.

```m4
dnl # define sendmail to delay delivery
define(`confDELIVERY_MODE', `d')
```

Building the sendmail.cf file with m4  
Once you have built the sendmail.cf file, you must run it through the m4 macro processor to generate the sendmail.cf file.

```bash
m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

# Mail Relaying

Setting up mail relaying is an essential task that needs to be undertaken to ensure that your server is not used by spammers. Basically, you want to relay (or deliver) all mail that originates from your domain to the target domain. If your domain is http://mycorp.com, then you need to add this into the /etc/mail/relay-domains file. As it is relatively easy to spoof the from address, you need to be more specific on who can use your mail server. The configuration file /etc/mail/access can be more specific on who can use the relay server. This file can be used to configure a number of actions such as RELAY, REJECT, and DISCARD. The file is a simple 2 column list, which needs to be converted into a sendmail-compatible file. A sample file is shown below:

| Host/IP | Action |
| :--- | :--- |
| localhost | RELAY |
| 10.10.100.12 | RELAY |
| 10.10.100.13 | RELAY |
| mycorp.com | RELAY |

This will be converted into a sendmail format file named /etc/mail/access.db:

```bash
cd /etc/mail
make
```

# Postfix

An alternative to sendmail is Postfix, which was designed to be simpler to configure than sendmail. Although there are several hundred configuration parameters that are controlled by the main configuration file /etc/postfix/main.cf, the variables in the postfix.cf file are defined and used in a similar way to shell variables.

```bash
parameter = value
new_parameter = $parameter
```

The domain that is used in outbound mail is defined in the myorigin parameter, which by default defaults to the local machine name. You obviously need to change this [unless you are setting up the server for a small site, such as a home office]. The server can accept mail for a number of domains, and these will be specified in the mydestination parameter. As with sendmail, you must ensure you only relay mail from hosts or network you know and trust. This is undertaken using the mynetworks parameter.
