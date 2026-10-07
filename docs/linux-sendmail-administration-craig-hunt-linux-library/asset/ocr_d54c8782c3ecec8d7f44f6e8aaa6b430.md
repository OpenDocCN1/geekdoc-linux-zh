# Little-Used Databases

The genericstable is the only database that I use that Red Hat did not include in the configuration. The other three databases that Red Hat did not configure are very seldom used.

# Little-Used Databases

The three remaining databases have very little use in current configurations because they deal with outdated networks, outdated syntax, or rare situations. These three databases are:

+   - dominateable domaintable is intended to ease the transition from an old domain name to a new domain name by translating the old name to the new name on all mail. You are rarely in the situation where you must change domain names, but if you are this database can help. The old domain name is the key and the new domain name is the value returned for the key. For example, assume we changed the domain name for the sales division from sales.business.com to marketing .business.com. We could put the following line in the domaintable to handle the address mapping:

```
sales.business.com marketing.business.com
```

The domaintable source file must be converted to a hash type database with makemap before Sendmail can use it. Also, support for the domaintable must be added to the configuration with the FEATURE(`domaintable`) command before Sendmail will even attempt to use the file.

+   - uucpdomain The uucdomain database converts email addresses from the .UUCP pseudo-domain into old-fashioned UUCP bang addresses. The key to the database is the hostname from the .UUCP pseudo-domain. The value returned for the key is the bang address. It is very unlikely that you will use this database. Most sites no longer use UUCP for mail, and those that do not use bang addresses. Bang addresses are almost never used anymore because current UUCP mailers handle email addresses that look like Internet addresses.

+   - bitdomain BITNET is an IBM-mainframe-to-IBM-mainframe network that was created at a time when IBM did not offer TCP/IP protocols for their mainframes. The bitdomain database converts BITNET hostnames to legal Internet hostnames. BITNET is outdated. You will not use at your site.

Well, that finally it: a almost different files and databases, more databases than you will ever want or use. Most of them are built using the makemap command.

![](bbox=[0.933, 0.273, 0.996, 0.383])