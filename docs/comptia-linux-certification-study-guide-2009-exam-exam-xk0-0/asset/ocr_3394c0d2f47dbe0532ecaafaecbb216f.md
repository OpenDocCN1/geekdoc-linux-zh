issues that were inherent in the original releases. POP4 has been developed, but is not an approved standard at the time of writing. However, it is still not totally secure, and care should be taken when using it across an unsecured network.

The IMAP protocol has gained in popularity over the years, and is now offered by Web providers such as Gmail (as well as POP3) and for local servers such as Microsoft Exchange. IMAP will be much faster to download mail on a local network compared with POP3.

# How Mail Works

Any mail server in your organization will ideally need to handle both incoming and outgoing mails. The mail arrives at your mail server for the domain(s) it looks after, defined in part by the DNS MX record. Users within this domain will have usernames associated with their mail account. While you may find it useful to give people their first name like Fred and Mary, this will not work when the company grows larger. It is therefore useful to define a scheme before setting up the server, perhaps first.lastname (or whatever works for your organization). The full e-mail address will then be username@your domain. E-mail will then be stored on the server until the user successfully retrieves them using an e-mail client.

Outgoing mail will be handled slightly differently. If a user sends an e-mail destined for a local user, the mail server will simply put the e-mail in the appropriate user’s mailbox, where they can retrieve it as above. If it is for someone outside the domain, the mail server will look up the MX record of the target domain and then try to send or relay the mail message to that server.

# Sendmail

Sendmail has been around for a number of years and has grown in complexity to keep up with the demands of users in requiring more sophisticated mail. The following sections will outline how to set up a sendmail server.

# Starting and Stopping Sendmail

Sendmail is usually started upon boot, but can also be started and stopped afterwards. This is especially important when configuration changes are made, as sendmail will only read the configuration file once when it starts. The commands below are used to start, stop, and restart sendmail.

```
```
   service sendmail start
   service sendmail stop
   service sendmail restart
```
```