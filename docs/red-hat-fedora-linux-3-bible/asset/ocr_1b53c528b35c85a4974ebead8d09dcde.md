```
# nslookup -sil ftp.yourdomain.com

```
Server:		123.45.67.1
Address:	123.45.67.1#53

Name:	ftp.yourdomain.com
Address: 123.45.67.3
```
```

The output from the `nslookup` command includes the name of the computer fulfilling the request and its IP address, along with the name and address of the computer you’re asking for. (The `-sil` option prevents a message that `nslookup` might soon be removed from Fedora Linux.) Try `nslookup` with an IP address (such as `10.0.0.1`) to make sure reverse lookup works.

To check the status of the named server that is running on your local system, use the same script that starts `named`. Type the following to check the status of your DNS server daemon:

```
```
# /etc/init.d/named status
number of zones: 5
debug level: 0
xfers running: 0
xfers deferred: 0
soa queries in progress: 0
query logging is OFF
server is up and running
```
```

If you can’t reach the computers that your DNS server is serving by name or IP address, you should make sure that each client’s address records are correct. You can also try to ping each client and server computer using the full host name or IP address.

# ## Getting More Information about BIND

For details on many other BIND options that I don’t describe in this chapter, you can refer to several places, as the following list relates:

+   * `/usr/share/doc/bind-9*/arm` — Contains HTML and XML versions of the BIND 9 Administrator Reference Manual.
+   * **Man pages** — Type the `man` command, following it by `named` or `named.conf`. These man pages contain terse descriptions of options and variables that relate to the `named` daemon and `named.conf` file, respectively.
+   * **Internet Software Consortium** (<https://www.isc.org/products/BIND/>) — The ISC Web site contains information and downloads related to BIND. On this site, find links to BIND mailing lists, security advisories relating to BIND, and BIND history.