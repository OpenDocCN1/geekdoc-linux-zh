Listing 11.1 shows that identd is preconfigured to run inetd on a Caldera 2.3 server system. Many Linux systems run identd on demand from inetd or xident. A few run identd as part of the boot; for example, Red Hat changed to running identd at boot time as part of release 6.2. A quick ps command can check if the identd daemon is running on your Linux system. If your system doesn't run identd by default, either at boot time or on demand, add it to your configuration.

When identd is running, the remote server can query any TCP connections from your server by sending the username and destination port pair to the identification server. Your system responds by sending the username associated with the connection or an error. Spammers do not like to have their real usernames known. Providing their names to their victims makes it hard for spammers to stay in business.

> If you masquerade usernames for security reasons, your security people may not want you to run identd because it will expose the real usernames. However, masquerading should be used to create consistent, readable addresses, I recommend running identd if you masquerade user names.

# Properly Configure Mail Relay

In addition to discouraging local users from generating spam, you need to discourage remote users from using your server as a tool for distributing spam. Nobody likes spammers and the people know it. They do their best to hide the true source of the spam by relaying their junk mail through other people's servers. If your mail server allows relaying, spammers will make use of it.

To discourage, the default configuration of Sendmail from version 8.9 handles local mail but does not relay messages for any outside sources. Blocking relaying in most works because most systems are not mail servers—they're desktop or Unix systems dedicated to a single user. Because the user's mail originates from the system that is running identd, the mail is handled as local mail and relaying for outside systems is not required. Also, the definition of local mail is fairly broad. As we saw in Chapter 6, “Using Sendmail Databases,” every host listed in class w is considered to be the local host. Therefore, the default configuration works in many cases.

# Relaxing Relay Restrictions

However, blocking all relaying doesn't work in every case, particularly if the system is a mail server. Most of the mail server delivers originates on its clients—this might be

![](bbox=[0.933, 0.573, 0.981, 0.653])