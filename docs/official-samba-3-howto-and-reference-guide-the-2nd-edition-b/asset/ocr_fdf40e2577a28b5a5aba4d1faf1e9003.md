This process joins the server to the domain without separately having to create the machine trust account on the PDC beforehand.

This command goes through the machine account password change protocol, then writes the new (random) machine account password for this Samba server into a file in the same directory in which a smbd password file would be normally stored. The trust account information that is needed by the DNS is written into the file /usr/local/samba/private/secrets.tdb or /etc/samba/secrets.tdb.

This file is created and owned by root and is not readable by any other user. It is the key to the domain-level security for your system and should be treated as carefully as a shadow password file.

Finally, restart your Samba daemons and get ready for clients to begin using domain security. The way you can restart your Samba daemons depends on your distribution, but in most cases the following will suffice:

```
```bash
root # /etc/init.d/samba restart
```
```

# ### 6.3.2 Why Is This Better Than security = server?

Currently, domain security in Samba does not free you from having to create local UNIX users to represent the users attaching to your server. This means that if domain user DOMfred attaches to your domain security Samba server, there needs to be a local UNIX user fred to represent that user in the UNIX file system. This is similar to the older Samba security mode security = server, where Samba would pass through the authentication request to a Windows NT server in the same way as a Windows 95 or Windows 98 server would.

Please refer to Chapter 23, “Winbind: Use of Domain Accounts”, for information on a system to automatically assign UNIX UIDs and GIDs to Windows NT domain users and groups.

The advantage of domain-level security is that the authentication in domain-level security is passed down the authenticated RPC channel in exactly the same way that an NT server would do it. This means Samba servers now participate in domain trust relationships in exactly the same way NT servers do (i.e., you can add Samba servers into a resource domain and have the authentication passed on from a resource domain PDC to an account domain PDC).

In addition, with security = server, every Samba daemon on a server has to keep a connection open to the authenticating server for as long as that daemon lasts. This can drain the connection resources on a Microsoft NT server and cause it to run out of available connections. With security = domain, however, the Samba daemons connect to the PDC or BDC only for as long as is necessary to authenticate the user and then drop the connection, thus conserving PDC connection resources.