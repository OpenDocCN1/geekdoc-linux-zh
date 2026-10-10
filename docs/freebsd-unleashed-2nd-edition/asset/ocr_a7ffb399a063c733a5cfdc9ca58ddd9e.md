```
/etc/mail/aliases
```

There is a mailbox in /var/mail for every user on the system; however, someone having an e-mail address on your machine doesn’t require that they have an account. You can always set up aliases to map incoming e-mail addresses to any other address, whether it’s another account on your machine, an address somewhere else on the Internet, or even a pipe to a file or program. The default /etc/mail/aliases contains examples of all these. An alias line contains the alias name, a colon, a space or tab, and the target address or pipe:

```
tiger: bob@stripes.com
fsmith: frank
pager: "|/usr/local/bin/pageeme"
dump: ">>/home/frank/dump2me"
mylist:include:/home/frank/list.txt
```

This last example is an “include” alias, which reads in a list of addresses from a plain-text file at the specified location. This is an easy way to manage a mailing list. Just make changes to the included file, and the alias will always be up to date.

Traditionally, and as a matter of “netiquette,” a system has a number of administration aliases for various purposes that are all aliases for root. Some of these “pseudo-accounts” include abuse (the address for reporting junk mail or malicious activity originating at your server), postmaster (the person who runs the mail server), and webmaster (the person in charge of the Web server). Some of these are already aliased to root in the default configuration, and others you may have to enable by uncommenting them.

After you make any change to /etc/mail/aliases, you have to rebuild the aliases.db file, which is a hash table version of the aliases file that provides fast lookups (as with /etc/master.passwd, which we discussed in Chapter 9, “Users, Groups, and Permissions”). You can use the traditional newaliases command to do this, or for consistency’s sake with the rest of the maintenance tasks, use make aliases:

```
# make aliases
/usr/sbin/sendmail -bi
/etc/mail/aliases: 25 aliases, longest 10 bytes, 254 bytes total
chmod 0640 /etc/mail/aliases.db
```

The command shown here will not return any output if the aliases database is up to date.

> **NOTE**
> Using global aliases isn’t the only way to redirect mail from one local address to another, or to an external address. For instance, if a user wants all his incoming mail to be forwarded automatically to some external address, you could use /etc/mail/aliases to do the trick, but this involves root access. There’s a better way, if the user has a full account on the system.