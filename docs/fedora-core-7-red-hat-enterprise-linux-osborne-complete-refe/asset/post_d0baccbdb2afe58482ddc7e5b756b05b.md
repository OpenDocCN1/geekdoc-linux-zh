
DNS servers automatically. Any changes you make to the master server are automatically transferred to its slave servers. This transfer of information is called a *zone transfer*. Zone transfers are automatically initiated whenever the slave zone's refresh time is reached or the slave server receives a notify message from the master. The *refresh time* is the second argument in the zone's SOA entry. A notify message is automatically sent by the master whenever changes are made to the master zone's configuration files and the `named` daemon is restarted. In effect, slave zones are automatically configured by the master zone, receiving the master zone's zone files and making them their own.

## Slave Zones

Using the previous examples, suppose you want to set up a slave server on **rabbit.mytrek.com**. Zone entries, as shown in the following example, are set up in the `named.conf` configuration file for the slave DNS server on **rabbit.mytrek.com**. The slave server is operating in the same domain as the master, and so it has the same zone name, **mytrek.com**. Its SOA file is named *slave.mytrek.com*. The term “slave” in the filename is merely a convention that helps identify it as a slave server configuration file. The `masters` statement lists its master DNS server—in this case, 192.168.0.1. Whenever the slave needs to make a zone transfer, it transfers data from that master DNS server. The entry for the reverse mapping file for this slave server lists its reverse mapping file as *slave.192.168.0*.

```
zone "mytrek.com" {
    type slave;
    file "slave.mytrek.com";
    masters { 192.168.0.1;
    };
}

zone "1.168.192.IN-ADDR.ARPA" {
    type slave;
    file "slave.192.168.0";
    masters { 192.168.0.1;
    };
}
```

## Slave Records

On the master DNS server, the master SOA zone file has entries in it to identify the host that holds the slave DNS server and to designate it as a DNS server. In this example, you would place the following in the **mytrek.com** zone file:

IN   NS  192.168.0.2

You would also place an entry for this name server in the **mytrek.com** reverse mapping file:

IN   NS  192.168.0.2

## Controlling Transfers

The master DNS server can control which slave servers can transfer zone information from it using the `allow-transfer` statement. Place the statement with the list of IP addresses for the slave servers to which you want to allow access. Also, the master DNS server should be sure its **notify** option is not disabled. The **notify** option is disabled by a "notify no" statement in the options or zone **named.conf** entries. Simply erase the "no" argument to enable notify.

### Incremental Zone Transfers

With BIND versions 8.2.2 and 9.0, BIND now supports incremental zone transfers (IXFR). Previously, all the zone data would be replaced in an update, rather than changes such as the addition of a few resource records simply being edited in. With incremental zone transfers, a database of changes is maintained by the master zone. Then only the changes are transferred to the slave zone, which uses this information to update its own zone files. To implement incremental zone transfers, you have to turn on the **maintain-ixfr-base** option in the options section.

```
maintain-ixfr-base yes;
```

You can then use the **ixfr-base** option in a zone section to specify a particular database file to hold changes.

```
ixfr-base "db.mytrek.com.ixfr";
```

## IP Virtual Domains

IP-based virtual hosting allows more than one IP address to be used for a single machine. If a machine has two registered IP addresses, either one can be used to address the machine. If you want to treat the extra IP address as another host in your domain, you need only create an address record for it in your domain's zone file. The domain name for the host would be the same as your domain name. If you want to use a different domain name for the extra IP, however, you have to set up a virtual domain for it. This entails creating a new **zone** statement for it with its own zone file. For example, if the extra IP address is 192.168.0.42 and you want to give it the domain name **sail.com**, you must create a new **zone** statement for it in your **named.conf** file with a new zone file. The **zone** statement would look something like this. The zone file is called **sail.com**:

```
zone "sail.com" in {
    type master;
    file "sail.com";
};
```

In the **sail.com** file, the name server name is **turtle.mytrek.com** and the e-mail address is **hostmaster@turtle.mytrek.com**. In the name server (NS) record, the name server is **turtle.mytrek.com**. This is the same machine using the original address that the name server is running as. **turtle.mytrek.com** is also the host that handles mail addressed to **sail.com** (MX). An address record then associates the extra IP address 192.168.0.42 with the **sail.com** domain name. A virtual host on this domain is then defined as **jib.sail.com**. Also, **www** and **ftp** aliases are created for that host, creating **www.sail.com** and **ftp.sail.com** virtual hosts.

```
; Authoritative data for sail.com
;
$TTL 1d
@ IN SOA turtle.mytrek.com. hostmaster.turtle.mytrek.com. (
93071200 ; Serial (yyMMddxx)
10800 ; Refresh 3 hours
3600 ; Retry 1 hour
360000 ; Expire 1000 hours
86400 ); Minimum 24 hours
IN NS turtle.mytrek.com.
IN MX 10 turtle.mytrek.com.
IN A 192.168.0.42 ;address of the sail.com domain
jib IN A 192.168.0.42
www IN A jib.sail.com.
ftp IN CNAME jib.sail.com.
```

In your reverse mapping file (/var/named/1.168.192), add PTR records for any virtual domains.

```
42.1.168.192 IN PTR sail.com.
42.1.168.192 IN PTR jib.sail.com.
```

You also have to configure your network connection to listen for both IP addresses on your machine (see Chapter 5).

## Cache File

The *cache* file is used to connect the DNS server to root servers on the Internet. The file can be any name. On many systems, the cache file is called **named.ca**. Other systems may call the cache file **named.cache** or **roots.hints**. The cache file is usually a standard file installed by your BIND software, which lists resource records for designated root servers for the Internet. You can obtain a current version of the **named.ca** file from the **rs.internic.net** FTP site. The following example shows sample entries taken from the **named.ca** file:

```
; formerly NS.INTERNIC.NET
;
. 360000 IN NS A.ROOT-SERVERS.NET.
A.ROOT-SERVERS.NET. 360000 A 198.41.0.4
;
; formerly NS1.ISI.EDU
;
. 360000 NS B.ROOT-SERVERS.NET.
B.ROOT-SERVERS.NET. 360000 A 128.9.0.107
```

If you are creating an isolated intranet, you need to create your own root DNS server until you connect to the Internet. In effect, you are creating a fake root server. This can be another server on your system pretending to be the root or the same name server.

## Dynamic Update: DHCP and Journal Files

There are situations where you will need to have zones updated dynamically. Instead of your manually editing a zone file to make changes in a zone, an outside process updates the zone, making changes and saving the file automatically. Dynamic updates are carried out both by master zones updating slave zones and by DHCP servers providing IP addresses they generated for hosts to the DNS server.

A journal file is maintained recording all the changes made to a zone, having a **.jnl** extension. Should a system crash occur, this file is read to implement the most current changes. Should you want to manually update a dynamically updated zone, you will need to erase its journal file first; otherwise, your changes would be overwritten by the journal file entries.

You allow a zone to be automatically updated by specifying the **allow-update** option. This option indicates the host that can perform the update.

```
allow-update {turtle.mytrek.com};
```

Alternatively, for master zones, you can create a more refined set of access rules using the **update-policy** statement. With the **update-policy** statement, you can list several grant and deny rules for different hosts and types of hosts.

### TSIG Signatures and Updates

With BIND 9.x, TSIG signature names can be used instead of host names or IP addresses for both **allow-update** and **update-policy** statements (see the following sections on TSIG). Use of TSIG signatures implements an authentication of a host performing a dynamic update, providing a much greater level of security. For example, to allow a DHCP server to update a zone file, you would place an **allow-update** entry in the zone statement listed in the **named.conf** file.

The TSIG key is defined in a key statement, naming the key previously created by the **dnssec-keygen** command. The algorithm is HMAC-MD5, and the secret is the encryption key listed in the **.private** file generated by **dnssec-keygen**.

```text
key mydhcpserver {
algorithm HMAC-MD5;
secret "ONQAfBfBLnvWU9G8hrQq/WA==";
};
```

The key name can then be used in an **allow-update** or **allow-policy** statement to specify a TSIG key.

```
allow-update { key mydhcpserver};
```

### Manual Updates: nsupdate

You can use the update procedure to perform any kind of update you want. You can perform updates manually or automatically using a script. For DHCP updates, the DHCP server is designed to perform dynamic updates of the DNS server. You will need to configure the DHCP server appropriately, specifying the TSIG key to use and the zones to update.

You can manually perform an update using the **nsupdate** command, specifying the file holding the key with the **-k** option.

```
nsupdate -k myserver.private
```
