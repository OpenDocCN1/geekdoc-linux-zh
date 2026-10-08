# GENERAL REMARKS ON CONFIGURATION OF A NAME SERVER 479

often equivalent to the failure of the whole network. Consequently, there should be several name servers active in each zone, of which one should be the primary name server and all others secondary name servers. It may be sensible to distribute these computers across several network segments, so that at least one name server remains reachable even in the event of a router or hub failure. a secondary server is practically maintenance-free because it fetches its data from the primary server. You should, however, occasionally check the log files.

# 20.2 Migrating from BIND4 to BIND8

If you have already running BIND as a name server, you may still be running version 4 of BIND. Since there have been many updates, bug fixes and security fixes, it might be a good idea to switch to BIND8 in the near future. It is not much work, and if you have any problems it is easy to revert to the old version.

The only thing that has really changed is the syntax and the name of the primary configuration file. It was formerly named named.boot and is now called named.conf. You'll find that the script named-bootconf in the BIND8 distribution will create a reasonable configuration for BIND8 from your existing BIND4 configuration.

```
(Linux):# named-bootconf < named.boot > named.conf
```

+   **Listing 20.1** Running named-bootconf.

You'll need to check two things: named-bootconf may have problems with comments in your old configuration that will appear in the wrong place in the new configuration. Second, look at the general configuration, since BIND8 is much more灵活. For details see the following section.

# 20.3 General remarks on configuration of a name server

In comparison with a DNS client, the file /etc/host.conf can remain unchanged, as well as the file /etc/resolv.conf. In this case, the server is also its own client, although this is likely to be required in most cases anyway. It is also possible to use a name server other than the one on the local computer. This is sometimes used on firewall or gateway systems.

First, the file /etc/named.conf must be adapted to your own zone. An example for a primary name server can be found in Listing 20.1. This file