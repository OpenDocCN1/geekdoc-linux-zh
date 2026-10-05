# The virtuosetable 161

> **TIP** If you don’t have anything else in your database, you probably want an entry like the one for network 129.6 for your own network. As discussed above, Sendmail blocks all mail relaying, even mail from your clients. You use the access database and an entry like 129.6 RELAY to enable relaying for every hosted attached to your local network.

Once you build your access list, it must be converted into a database before Sendmail can use it. Use the makemap command to do the job, as shown below.

```
makemap hash /etc/mail/access.db < /etc/mail/access.txt
```

This command reads the entries in a text file named /etc/mail/access and uses them to build a hash database in the file named /etc/mail/access.db.

The local-host-names and relay-domains files and the aliases and access databases are probably the most important databases that were configured in the redhat.com configuration. They are not the only databases configured two. Two others, virtuosetable and mailertable, are configured in redhat.com. Ofthese, virtuosetable is the most useful.

# The virtuosetable

The virtuosetable is a database that routes mail for virtual mail domains. A virtual mail domain is similar to a virtual host in the Apache Web server. In the same way that a Web server can be configured to serve Web pages for host computers that do not physically exist, the Sendmail server can be configured to provide service for mail domains that do not have any existence beyond the Sendmail server itself. Creating a virtual mail domain allows you to advertise a meaningful name to the outside world without having to create all the services to support a full domain.

# Defining a Virtual Domain

Each entry in the virtuosetable has two fields: a virtual domain and a delivery address. The first field contains the virtual domain name found in the e-mail address. The second field contains the address to which the mail is really delivered. The virtual domain contained in the first field can be a complete address in the form of user@domain or it can be a partial address in the form @domain. When the @domain format is used, mail is sent to any user in the specified domain is routed to the mail address contained in the second field. Some sample virtuosetable entries are shown in Listing 6.9.

![](bbox=[0.913, 0.277, 0.976, 0.385])