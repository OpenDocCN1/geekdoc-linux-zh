# ## DOMAIN

If you are configuring a large number of mail servers for a single site, you may want to look into setting up a domain macro for your site. (See the **/usr/share/sendmail-cf/domains/** directory for examples.) These macros are essentially site-specific entries that you can set up and share across your network so that other administrators do not have to repeat certain configuration options.

For example, if you wanted to set up a domain configuration for your site and call it **mysite.m4**, you would use the **DOMAIN** macro as follows:

```
DOMAIN(`mysite')
```

For most sites, this is unnecessary and not worth the extra work of setting up a new domain entry in the **domains** directory.

# ## MAILER

In the first section, we discussed the differences between mail transfer agents (MTAs) and mail delivery agents (MDAs). Sendmail is an MTA only, and thus it requires another program to perform the actual mail delivery. The **MAILER** macro allows you to specify the program that will perform the delivery of messages.

There are three mailers we are interested in: **local**, **smtp**, and Procmail. The **local** mailer is meant for messages that need to be delivered to local mailboxes. The **smtp** mailer is for messages that need to be relayed to other sites instead of delivered locally. For example, if you have a single mail server and many clients in your network, you may want to configure your firewall so that the only host that is allowed to communicate through the firewall on the SMTP port (25) is your mail server. This means all of the clients on your network need to relay through your mail server, thus the need for an SMTP mailer.

The last mailer is the most interesting. Procmail is an extremely flexible general-purpose mail-filtering tool. Best of all, it is written with security issues in mind, which makes Procmail an excellent replacement for the default local mailer that comes with Linux.

> > NOTE
> > Sendmail supports more mailers than I have presented here; however, their usage is more likely to be the exception rather than the rule. If you are running into exceptions, it is better that you read through the **README.cf** file yourself rather than depend on my interpretation (and simplification) of it.

For example, to use the **smtp** mailer for relays and Procmail for local delivery, you need the following lines in your **.me** file: