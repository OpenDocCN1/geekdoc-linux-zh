# Testing Your NIS Client Configuration

After the /etc/yp.conf and /etc/nsswitch.conf files have been properly configured and the ypbind daemon is set up, you should be able to use the ypcat command 
dump a map from the NIS server to your screen. To do this, type the following command:

```
[root@client-A ~]# ypcat passwd
yang:$1hq0_..<TRUNCATED>..pia210:1001:1001:Yang:/home/yyang/yyang/bin/bash
```

This dumps the password map to your screen—that is, of course, if you are sharing your password via NIS. If you are not sharing it, pick a map that you are sharing, and use the ypcat command with filename.

If you don't see the map dumped out, you need to double-check your client and server configurations and try again.

# Configuring a Secondary NIS Server

As your site grows, you'll undoubtedly find that you need to distribute the NIS service
 to multiple hosts. NIS supports this through the use of secondary NIS servers.
Servers require no additional maintenance unless they are configured, because the\master NIS server sends updates when you rebuild the maps (with the make
command, as described in "Editing the Makefile" earlier in this chapter).

There are three steps to setting up a secondary NIS server:

+   - Set the NIS domain name.
- Set up the NIS master to push to the slave.
- Run ypinit to initialize the slave server.

# Configuring the Domain Name

As configuring a master NIS server, you should establish the NIS domain name
before starting up the initialization process for a secondary server (server-B):

```
[root@server-B ~]# domainname my_domain_name
```

Here, my_domain_name is the NIS domain for your site.

Of course, the secondary server's domain name must be set up so that it automatically
becomes established at boot time. In the Fedora version of Linux, or in your
sample system, you can do this by setting the NISDOMAIN variable in the /etc/config/network file. Otherwise, you can edit the ypbind daemon startup management/script
file (for example, /usr/lib/systemd/system/ypersv.service in the systemd world) so that
one of the first things it does is set the domain name there.