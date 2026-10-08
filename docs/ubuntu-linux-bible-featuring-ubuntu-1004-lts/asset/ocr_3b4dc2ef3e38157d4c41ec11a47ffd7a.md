# Chapter 32: Setting Up a DNS Server

```
zone "vonhagen.org" (
  type master;
  file "/etc/bind/vonhagen.zone"
  check-name warn;
);

zone "168.192.in-addr.arpa" (
  type master;
  file "/etc/bind/168.192.in-addr.arpa"
);
```

include "/etc/bind/zones.rfc1918.local";

These entries include each of these files and identify them as the master server for the zone vonhagen.org, which uses IP addresses and the 192.168.* family. Information about the zone vonhagen.org is provided in the file /etc/bind/vonhagen.zone. Reverse lookup information for IP addresses in the 192.168.* family is provided in the file /etc/bind/bind.arpa. The entries that identify these files use fullnames because these files are stored in /etc/bind, not the server's default directory of /var/cache/bind as defined in the servers'/etc/bind/named.options file. As mentioned previously, /etc/bind/named.conf.local file also loads a local copy of the default /etc/bind/zones.rfc1918 file, which I have edited to remove null responses for the zone "168.192.in-addr.arpa", because valid values for these non-routable IP addresses are explicitly provided in the file /etc/bind/168.192.in-addr.arpa.

After updating your /etc/bind/named.conf.local file, all that remains is to reload this information into the name server and test the name server, as described in the next section.

# Restarting and Testing Your Name Server

The DNS server startup file for BIND 9 is the /etc/init.d/bind9. Although this startup script provides reload and force-reload options, these options use a name server control utility (rndc) that may not be properly configured (yet) on your system. For this reason, I tend to simply restart the BIND daemon with a familiar command like the following:

```
$ sudo /etc/init.d/bind9 restart
```

After supplying your password, you will see the familiar shutdown and startup messages from the script. You will then verify that the name server started correctly by checking for it in a process listing, using a command like the following:

```
$ ps axww | grep named
```

If your configuration and zone files are valid, you will see a named process running on your system. Congratulations—you're running a DNS server! If not, proceed to the next section for some debugging tips and return to this section to complete your testing.