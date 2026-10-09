
## **named.conf**
You will want to use IP addresses that are unique to your installation. You may want to change the settings of the notify statements. The **named.conf** file in this example limits the IP addresses that **named** answers queries from and sets up logging (next page).

```bash
$ cat /etc/bind/named.conf
    options {
        directory "/etc/bind";
        // recursion NO;
        allow-query {127.0.0.1; 192.168.0.0/24};
    };
    zone "" IN {
        type hint;
        file "db.root";
    };
    zone "0.168.192.in-addr.arpa" IN {
        type master;
        file "named.conf.local";
        notify NO;
    };
    zone "sam.net" IN {
        type master;
        file "sam.net";
        notify NO;
    };

    logging{
        channel "misc" {
            file "/var/log/bind/misc.log" versions 4 size 4m;
            print-time YES;
            print-severity YES;
            print-category YES;
        };
        channel "query" {
            file "/var/log/bind/query.log" versions 4 size 4m;
            print-time YES;
            print-severity NO;
            print-category NO;
        };
        category default {
            "misc";
        };
        category queries {
            "query";
        };
    };
```

The **allow-query** statement in the Options clause specifies the IP addresses of systems the server answers queries from. You must include the local system as 127.0.0.1 if it will be querying the server. The server is authoritative for the zone **sam.net**; the zone file for **sam.net** is /etc/bind/sam.net.

## Logging
Logging is turned on by the Logging clause. Logging is separate from named messages, which go to syslog. The Logging clause in the preceding example opens two logging channels: one that logs information to /var/log/bind/misc.log and one that logs information to /var/log/bind/query.log. When either of these logs grows to 4 megabytes (size 4m in the file statement), it is renamed by appending .1 to its file name and a new log is started. The numbers at the ends of other, similarly named logs are incremented. Any log that would have a larger number than that specified by the versions keyword (4 in the example) is removed. See logrotate (page 622) for another way to maintain log files.

The print statements determine whether the time, severity, and category of the information are sent to the log; specify each as YES or NO. The category determines what information is logged to the channel. In the previous example, default information is sent to the misc channel and queries are sent to the query channel. Refer to the named.conf man page for more choices.

## **named.conf.local**
The origin for the reverse zone file (**named.conf.local**) is 0.168.192.in-addr.arpa (as specified in the Zone clause that refers to this file in **named.conf**). Following the SOA and NS resource records, the first three PTR resource records equate address 1 in the subnet 0.168.192.in-addr.arpa (192.168.0.1) with the names gw.sam.net, www.sam.net, and ftp.sam.net, respectively. The next three PTR records equate 192.168.0.3 with mark.sam.net, 192.168.0.4 with mail.sam.net, and 192.168.0.6 with ns.sam.net.

```bash
$ cat /etc/bind/named.conf.local
$TTL       3D
@         IN      SOA     ns.sam.net. mgs@sobel11.com. (
                             2010110501  ; serial
                             8H          ; refresh
                             2H          ; retry
                             4W          ; expire
                             1D)         ; minimum
        IN      NS      ns.sam.net.
1         IN      PTR     gw.sam.net.
1         IN      PTR     www.sam.net.
1         IN      PTR     ftp.sam.net.
3         IN      PTR     mark.sam.net.
4         IN      PTR     mail.sam.net.
6         IN      PTR     ns.sam.net.
```

## **sam.net**
The zone file for **sam.net** takes advantage of many BIND features and includes TXT (page 830), CNAME (page 828), and MX (page 828) resource records. When you query for resource records, named returns the TXT resource record along with the records you requested. The first of the two NS records specifies an unqualified name (ns) to which BIND appends the zone name (sam.net), yielding an FQDN of ns.sam.net. The second nameserver is specified with an FQDN name that BIND does not alter. The MX records specify mail servers in a similar manner and include a priority number at the start of the data field, where lower numbers indicate preferred servers.

```text
$ cat sam.net
;
zone "sam.net"
;
TTL		3D
@		IN	SOA	ns.sam.net. mgs@sobel11.com. (
			2010110501		; serial
			8H				; refresh
			2H				; retry
			4W				; expire
			1D )
						; minimum
TXT	"Sobe11 Associates Inc."
ns	NS		; Nameserver address (unqualified)
ns	NS	ns.max.net.; Nameserver address (qualified)
mx	MX	10 mail	; Mail exchange (primary/qualified)
mx	MX	20 mail.max.net.; Mail exchange (2nd/qualified)

localhost IN A	127.0.0.1

www	IN	CNAME ns
ftp	IN	CNAME ns

gw	IN	A	192.168.0.1
		TXT	"Router"

ns	IN	A	192.168.0.6
		MX	10 mail
		MX	20 mail.max.net.

mark	IN	A	192.168.0.3
		MX	10 mail
		MX	20 mail.max.net.
		TXT	"MGS"

mail	IN	A	192.168.0.4
		MX	10 mail
		MX	20 mail.max.net.
```

Some resource records have a value in the Name field; those without a name inherit the name from the previous resource record. In a similar manner, the previous resource record may have an inherited name value, and so on. The five resource records following the SOA resource record inherit the `@`, or zone name, from the SOA resource record. These resource records pertain to the zone as a whole. In the preceding example, the first TXT resource record inherits its name from the SOA resource record; it is the TXT resource record for the sam.net zone (give the command `host -t TXT sam.net` to display the TXT resource record).

Following these five resource records are resource records that pertain to a domain within the zone. For example, the MX resource records that follow the A resource record with the Name field set to mark are resource records for the **mark.sam.net.** domain.

The A resource record for `localhost` is followed by two CNAME resource records that specify `www(sam.net.)` and `ftp(sam.net.)` as aliases for the nameserver `ns.sam.net.`. For example, a user connecting to `ftp.sam.net` will connect to `192.168.0.6`. The resource records named `gw`, `ns`, `mark`, and `mail` are resource records for domains within the `sam.net` zone.

Before restarting `named`, create the directory for the log files and give it permissions and ownership as shown below. If you are running `named` in a chroot jail, create the `bind` directory in `/var/lib/named/var/log`.

```bash
$ sudo mkdir /var/log/bind
$ sudo chown bind:bind /var/log/bind
$ ls -ld /var/log/bind
drwxr-xr-x 2 bind bind 4096 2010-04-26 17:43 /var/log/bind
```

With the log directory in place, and the `named.conf`, `db.root`, `named.conf.local`, and `sam.net` zone files in `/etc/bind` (or in `/var/lib/named/etc/bind` if you are running `named` in a chroot jail), restart `named` and check the log files. The file `/var/log/syslog` should show something like the following (the example shows `named` started in a chroot jail):

```text
# cat /var/log/syslog
***
Apr 26 18:05:19 plum named[22119]:  9.7.0-P1 -u bind -t /var/lib/named
Apr 26 18:05:19 plum named[22119]:  found 1 CPU, using 1 worker thread
Apr 26 18:05:19 plum named[22119]:  loading configuration from '/etc/bind/named.conf'
Apr 26 18:05:19 plum named[22119]:  listening on IPv4 interface lo, 127.0.0.1#53
Apr 26 18:05:19 plum named[22119]:  listening on IPv4 interface eth0, 192.168.0.10#53
Apr 26 18:05:19 plum named[22119]:  command channel listening on 127.0.0.1#953
Apr 26 18:05:19 plum named[22119]:  command channel listening on ::1#953
***
```

The `misc.log` file may show errors that do not appear in the syslog file:

```text
# cat /var/log/bind/misc.log
... 01:05:19.932 general:  info:  zone 0.168.192.in-addr.arpa./IN:  loaded serial 1010110501
... 01:05:19.933 general:  info:  zone sam.net./IN:  loaded serial 1010110501
... 01:05:19.933 general:  notice:  running
```

# A SLAVE SERVER
To set up a slave server, copy the `/etc/bind/named.conf` file from the master server to the slave server, replacing the **type master** statement with **type slave** and adding a **masters ( 1.2.3.4; );** directive. Remove any zones the slave server will not be acting as a slave for, including the root (.) zone, if the slave server will not respond to recursive queries. If necessary, create the `/var/log/bind` directory for log files as explained at the end of the previous section.

Slave servers copy zone information from the primary master server or another slave server. The **notify** statement specifies whether you want a master server to notify slave servers when information on the master server changes. Set the (global)
