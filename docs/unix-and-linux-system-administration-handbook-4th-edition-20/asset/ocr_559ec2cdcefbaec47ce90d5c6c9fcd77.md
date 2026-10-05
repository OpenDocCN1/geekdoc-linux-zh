# Sample BIND logging configuration

+   - **Many timeouts resolving xxx: disabling EDNS.** This message can result from a broken firewall not admitting UDP packets over 512 bytes or not admitting fragments. It can also indicate problems at the specified host. Verify that the problem is not your firewall and consider redirecting these messages to the null channel.

+   - **Unexpected RCODE (SERVAIL) resolving xxx.** This can be an attack or, or more likely, a sign of something repeatedly querying a zone.

+   - **Bad referral.** This message indicates a miscommunication among a zone's name servers.

+   - **Not authoritative.** For a slave server is unable to get authoritative data for a zone. It's pointing to the wrong master, or perhaps the master had trouble loading the zone in question.

+   - **Rejected zone.** `named` rejected a zone file because it contained errors.

+   - **No NS RRs.** A zone file did not include NS records after the SOA record. It could be that the records are missing, or that they don't start with a tab or other whitespace. In the latter case, the records are not attached to the zone of the SOA record and are therefore misinterpreted.

+   - **No default TTL set.** The preferred way to set the default TTL for records is with a $TTL directive at the top of the zone file. This error message indicates that the $TTL is missing; it is required in BIND 9.

+   - **No root server for class.** Your server is having trouble finding the root name servers. Check your hints file and the server's Internet connectivity.

+   - **Address already in use.** The port on which `named` wants to run is already being used by another process, probably another copy of `named`. If you don't see `named` around, it might have crashed and left an `rndc` control socket open that you'll have to track down and remove. A good way to fix the problem is to stop the `named` process with `rndc` and then restart named:

```
$ sudo rndc stop
$ sudo /usr/sbin/named ...
```

+   - `updating zone xxx: update` A dynamic update was attempted but refused, most likely because of the `allow-update-policy` in `named.conf` for this zone. This is a common error message and often caused by misconfigured Windows boxes.

Sample BIND logging configuration

The following snippet from the ISC `named.conf` file for a busy TLD name server illustrates a comprehensive logging regime.