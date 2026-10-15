# Slave Records

On the master DNS server, the master SOA zone file has entries in it to identify the host that holds the slave DNS server and to designate it as a DNS server. In this example, you would place the following in the mytrek.com zone file:

```
IN    NS    192.168.0.2
```

You would also place an entry for this name server in the mytrek.com reverse mapping file:

```
IN    NS    192.168.0.2
```

# Controlling Transfers

The master DNS server can control which slave servers can transfer zone information from it using the allow-transfer statement. Place the statement with the list of IP addresses for the slave servers to which you want to allow access. Also, the master DNS server should be sure its notify option is not disabled. The notify option is disabled by a "notify no" statement in the options or zone named.conf entries. Simply erase the "no" argument to enable notify.

# Incremental Zone Transfers

With BIND versions 8.2.2 and 9.0, BIND now supports incremental zone transfers (IXFR). Previously, all the zone data would be replaced in an update, rather than changes such as the addition of a few resource records simply being edited in. With incremental zone transfers, a database of changes is maintained by the master zone. Then only the changes are transferred to the slave zone, which uses this information to update its own zone files. To implement incremental zone transfers, you have to turn on the maintain-ixfr-base option in the options section.

```
maintain-ixfr-base yes;
```

You can then use the ixfr-base option in a zone section to specify a particular database file to hold changes.

```
ixfr-base "db.mytrek.com.ixfr";
```

# IP Virtual Domains

IP-based virtual hosting allows more than one IP address to be used for a single machine. If a machine has two registered IP addresses, either one can be used to address the machine. If you want to treat the extra IP address as another host in your domain, you need only create an address record for it in your domain's zone file. The domain name for the host would be the same as your domain name. If you want to use a different domain name for the extra IP, however, you have to set up a virtual domain for it. This entails creating a new zone statement for it with its own zone file. For example, if the extra IP address is 192.168.0.42 and you want to give it the domain name sail.com, you must create a new zone statement for it in your named.conf file with a new zone file. The zone statement would look something like the following. The zone file is called sail.com.