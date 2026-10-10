```
;
; Query time: 24 msec
; SERVER: 10.0.0.1#53(10.0.0.1)
; WHEN: Mon Oct  9 02:12:32 2007
; MSG SIZE  rcvd: 129
```

Sections in the output from `dig` include a question section and an authority section. The results show name server assignments and addresses associated with the domain you're querying about. The `nslookup` command is another tool you can use to look up domain information. In the following example, `nslookup` looks up the server that is resolving `ftp.yourdomain.com`.

```
# nslookup -sil ftp.yourdomain.com
Server:	123.45.67.1
Address:	123.45.67.1#53

Name:	ftp.yourdomain.com
Address: 123.45.67.4
```

The output from the `nslookup` command includes the name of the computer fulfilling the request and its IP address, along with the name and address of the computer you're asking for. (The `-sil` option prevents a message that `nslookup` might soon be removed from Fedora and RHEL.) Try `nslookup` with an IP address (such as `10.0.0.1`) to make sure reverse lookup works.

To check the status of the named server that is running on your local system, use the same script that starts `named`. Type the following to check the status of your DNS server daemon:

```
# /etc/init.d/named status
number of zones: 5
debug level: 0
xfers running: 0
xfers deferred: 0
soa queries in progress: 0
query logging is OFF
recursive clients: 0/1000
tcp clients: 0/100
server is up and running
```

If you can't reach the computers that your DNS server is serving by name or IP address, you should make sure that each client's address records are correct. You can also try to `ping` each client and server computer using the full hostname or IP address.

# Getting More Information about BIND

For details on many other BIND options that I don't describe in this chapter, you can refer to several places, as the following list relates: