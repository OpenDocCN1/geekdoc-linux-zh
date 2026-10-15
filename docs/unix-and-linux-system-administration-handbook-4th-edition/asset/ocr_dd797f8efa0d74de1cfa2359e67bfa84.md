This command re-signs the zone and writes a file called dlvset-example.com. containing a DLV record ready for the DLV provider's zone.

NSD/Unbound users must generate the DLV record themselves. Copy the .ds file created when you generated your KSK key and change the record type from DS to DLV. Then adjust the name field. For example, change

```
example.com.      3600 IN DS  25069 1 0 dbf80886b716863de09...
```

to

```
example.com.dlv.isc.org.  3600 IN DLV 25069 1 0 dbf80886b716863de09...
```

The changes are shown in bold.

Once you've collected the DLV record and the key files used to sign your zone, go to the dlv.isc.org web page and follow the directions to have isc.org be your DLV server. ISC makes you jump through some hoops to verify that you own your domain, are authorized to manage it, and have provided its public key securely. But the process is not difficult.

ISC will give you some new lines for your trusted-keys clause in named.conf:

```
trusted-keys {
    div.isc.com 257 3 5 "hex mumbo jumbo of the key goes here";
    div.isc.com 257 3 5 "hex mumbo jumbo of another key goes here";
    ...
}
```

BIND users must also add a line to the named.conf options section:

```
dnssec-lookaside "." trusted-anchor "dlv.isc.org";
```

For NSD, add the DLV record to the zone and re-sign the zone. To enable DLV validation in unbound, get dlv.isc.org's KSK DNSKEY record from the ISC web site or from SecSpider and verify its signature. (SecSpider verifies that keys are consistent as seen from multiple locations; see page 652.) Don't just dig for the key, as that's insecure until you have DNSSEC deployed. Put the key in a file in unbound's working directory, say, dlv.isc.org.key, and add the line

```
dlv-anchor-file: "dlv.isc.org.key"
```

to your unbound.conf file in the server section.

# DNSSEC key rollover

Key rollover has always been a thorny issue in DNSSEC. In fact, the original specifications were changed specifically to address the issue of the communication needed between parent and child zones whenever keys were created, changed, or deleted. The new specifications are called DNSSEC-bis.

ZSK rollover is relatively straightforward and does not involve your parent zone or any trust anchor issues. The only tricky part is the timing. Keys have an expiration time, so rollover must occur well before that. However, they also have a TTL,