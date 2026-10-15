
protects against chicken-and-egg problems if unbound cannot look up the name without access to the destination zone.

You can have as many stub zones as you want.

### Forwarding

```
forward-zone:
  name: domain-name          [none]
  forward-host: server-name  [none]
  forward-addr: ip-address@port [none]
```

The forward-zone option lets unbound act as a forwarder, forwarding all queries (or just some, depending on the value of the name parameter) to another server to help that server build up a bigger cache. Forwarding occurs only if unbound cannot answer a query from its own cache. See page 569 for general information about forwarders and reasons why you might want to use them.

There may be multiple forward-zone statements. If you specify the name as . (a single period), all queries are forwarded.

## 17.12 UPDATING ZONE FILES

To change a domain's data (e.g., to add or delete a host), you update the zone data files on the master server. You must also increment the serial number in the zone's SOA record. Finally, you must get your name server software to pick up and distribute your changes. This final step varies depending on your software:

- BIND: Run rndc reload to signal named to pick up the changes. You can also kill and restart named, but if your server is both authoritative for your zone and recursive for your users, this operation discards cached data from other domains.
- NSD: Run nsdctl rebuild, followed by nsdctl reload. NSD does no caching, so it is not adversely affected by being restarted.

Updated zone data is propagated to slave servers of BIND masters right away because the notify option is on by default. In NSD, you must configure the notify ACL to get this (desirable) effect. If notifications are not turned on, your slave servers will not pick up the changes until after refresh seconds, as set in the zone's SOA record (typically an hour later).

If you have the notify option turned off, you can force BIND slaves to update themselves by running rndc reload on each slave. This command makes the slave check with the master, see if the data has changed, and request a zone transfer. The corresponding NSD command is nsdctl reload.

Don't forget to modify both the forward and reverse zones when you change a hostname or IP address. Forgetting the reverse files leaves sneaky errors: some commands work and some won't.

Changing the data files but forgetting to change the serial number makes the changes take effect on the master server (after a reload) but not on the slaves.

Do not edit data files on slave servers. These files are maintained by the name server and sysadmins should not meddle with them. It’s fine to look at the BIND data files as long as you don’t make changes. The NSD files are databases and so cannot be directly inspected. However, changes are by default written back to the text zone files by nsd-patch.

BIND allows zone changes to be made through a programmatic API, as specified in RFC2136. This feature, called dynamic updates, is necessary to support auto-configuration protocols like DHCP. The dynamic update mechanism is described on page 640.

### Zone transfers

DNS servers are synchronized through a mechanism called a zone transfer. A zone transfer can include the entire zone (called AXFR) or just the recent changes (called IXFR). By default, zone transfers use the TCP protocol on port 53. BIND logs transfer-related information with category ‘xfer-in’ or ‘xfer-out’; NSD includes it in the regular logging stream.

A slave that wants to refresh its data requests a zone transfer from the master server and makes a backup copy of the zone data on disk. If the data on the master has not changed, as determined by a comparison of the serial numbers (not the actual data), no update occurs and the backup files are just touched. (That is, their modification times are set to the current time.)

Both the sending and receiving servers remain available to answer queries during a zone transfer. Only after the transfer is complete does the slave begin to use the new data.

When zones are huge (like com) or dynamically updated (see the next section), changes are typically small relative to the size of the entire zone. With IXFR, only the changes are sent (unless they are larger than the complete zone, in which case a regular AXFR transfer is done). The IXFR mechanism is analogous to the patch program in that it makes changes to an old database to bring it into conformity with a new database.

In BIND, IXFR is the default for any zones configured for dynamic update, and named maintains a transaction log called zonename.jnl. You can set the options provide-ixfr and request-ixfr in the server statements for individual peers. The provide-ixfr option enables or disables IXFR service for zones for which this server is the master. The request-ixfr option requests IXFRs for zones for which this server is a slave.

```
provide-ixfr yes ;      # In BIND server statement
request-ixfr yes ;     # In BIND server statement
```
