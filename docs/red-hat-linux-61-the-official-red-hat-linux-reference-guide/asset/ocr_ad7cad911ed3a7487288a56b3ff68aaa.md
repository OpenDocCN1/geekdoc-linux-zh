# 12.5.1. Protocol Enhancements

BIND supports Incremental Zone Transfers (IXFR), where slave nameserver will only download the updated portions of a zone modified on a master nameserver. The standard transfer process requires that the entire zone be transferred to each nameserver for the smallest change. For very popular domains with very lengthy zone files and many slave nameservers, IXFR makes the notification and update process much less intensive.

Note that IXFR is only available when using dynamic updating to make changes to zone records. If manually editing zone files to make changes, AXFR is used. More information on dynamic updating is available in the BIND 9 Administrator Reference Manual. See Section 12.7.1 Installed Documentation for more information.

# 12.5.2. Multiple Views

Through the use of the view statement in named.conf, BIND can present different information depending on who is making the request.

This is primarily used to deny specific DNS entries from clients outside of the local network, while allowing queries from clients inside the local network.

The view statement uses the match-clients option to map IP addresses or entire networks and provide specific options and zone data.

# 12.5.3. Security

BIND supports a number of different methods to protect the updating and transfer of zones, on both master and slave nameservers:

+   - DNSSEC — Short for DNS SECUality, this feature allows zones to be cryptographically signed with a zone key.

In this way, the information about a specific zone can be verified as coming from a nameserver that it has signed with a private key, as long as the recipient has nameserver's public key.

BIND version 9 also supports the SIG(0) public/private key method of message authentication.

+   - TSIG — Short for Transaction SIGnatures, this feature allows a transfer from master to slave authorized only after verifying that a shared secret key exists on the master and slave nameservers.

This strengthens the standard IP address-based method of transfer authorization. An attacker would not only need to have access to the IP address to transfer the zone, but they would also need to know the secret key.

BIND version 9 also supports TKEY, which is another shared secret key method of authorizing zone transfers.

# 12.5.4. IP version 6

BIND version 9 can provide nameservice in IP version 6 (IPv6) environments through the use of A6 zone records.

If the network includes both IPv4 and IPv6 hosts, use the lwres lightweight resolver daemon on all network clients. This daemon is a very efficient, caching-only nameserver which understands the new A6 and DNAME records used under IPv6. See the lwres man page for more information.