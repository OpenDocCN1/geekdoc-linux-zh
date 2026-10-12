```
```
type slave;
file "gnaware.com";
masters {
    205.82.148.254;
};
};
zone "ksl.com" {
type slave;
file "ksl.com";
masters {
    205.82.148.254;
};
};
```
```

Like the /etc/named.conf file on the primary server that points to the secondary server for allowable transfers, the configuration file on ns2.gnuware.com points to the primary DNS server, 205.82.148.254. Each forwarding entry also looks to the primary server for information regarding domain names and IP addresses.

If the primary server becomes unavailable for any reason, the secondary server can then provide the necessary information to any hosts with ns1 and ns2 for their primary and secondary name servers. Name server redundancy is crucial when many networked systems are attempting to resolve IP addresses or look up certain domains.

# # Starting the Named Daemon

If you are running the RPM version of BIND, you should start the named daemon, which constantly runs in the background, as an automated process. As with most daemons under the Red Hat release, there is an entry in /etc/rc.d/init.d that is configured to start the named daemon upon bootup. Starting and stopping the named daemon take the same syntax as most other daemons:

```
```
# /etc/rc.d/init.d/named start|stop|restart
```
```

If you make any changes to the db files, you not only need to increment the serial number, but also restart the named daemon. A similar option is to issue the ndc reload command. Make sure the ndc executable is in your path.