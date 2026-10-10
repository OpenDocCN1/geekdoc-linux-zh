example.com. The rest of the file defines IP addresses for the private clients and public servers that are associated with the domain. Notice that the server at address 10.0.0.2 serves as a client on the LAN and a slave DNS server.

# **Setting Up the Zone Files (Outside)**

For the "outside" example.com.zone, you made a db.example.com.outside file using the same information from the "inside" file, with the following exceptions:

+   - Removed all references to private clients on the LAN. That way, someone poking around from the Internet can't get information about your private computers.
+   - Changed the addresses of the primary and slave DNS servers (ns1 and ns2) to 123.45.67.1 and 123.45.67.2, respectively. In that way, only public addresses for name servers are seen by the public. (Of course, you need to use your own public IP addresses instead of the examples 123.45.67.1 and 123.45.67.2.)

# **Setting Up the Zone Files (Reverse Lookup)**

The other new file in the example is the yourlan.db file, which contains the information necessary to perform reverse IP lookups for the computers on your LAN. Here's an example:

```
$TTL	36400
		IN SOA ns1.example.com hostmaster.example.com.
			2006042701 ; Serial
			28800 ; Refresh
			14400 ; Retry
			3600000 ; Expire
			86400 ) ; Minimum

		IN NS ns1.example.com
	1 IN PTR example.com.
	2 IN PTR red.example.com.
	3 IN PTR blue.example.com.
	4 IN PTR green.example.com.
	5 IN PTR yellow.example.com.

; EOF
```

The SOA record identifies 0.0.10.in-addr.arpa. as the start of authority for the zone. The NS line defines 0.0.10.in-addr.arpa. as the name server for the zone. Other records are pointers to hostnames that reverse-map on the 10.0.0. network. The records represent the address for the DNS server (example.com) and each of the clients on the LAN (red, blue, green, and yellow).

After you finish creating your own zone files, you can use the named-checkzone command to make sure that each zone file is formed correctly. Here is how you'd run the named-checkzone command (as root user) to check the two example.com zone files (be sure to type each command on one line, even though each is shown here on two):