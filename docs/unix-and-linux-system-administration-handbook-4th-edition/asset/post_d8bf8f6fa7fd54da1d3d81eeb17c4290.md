
When an administrative boundary falls in the middle of a byte, you have to be sneaky. You must also work closely with the domain above or below you. The trick is this: for each possible host address in the natural in-addr.arpa zone, add a CNAME that deflects the lookup to a zone controlled by the owner of the appropriate subnet. This scheme makes for messy zone files on the parent, but it does let you delegate authority to the actual users of each subnet.

Here is the scheme in gory detail. The parent organization (in our case, the ISP) creates CNAME records for each possible IP address with an extra fake component (dot-separated chunk) that represents the subnet. For example, in the /26 scenario just described, the first quarter of the addresses would have a "0-63" component, the second quarter would have a "64-127" component, and so on. Here's what it looks like:

```
$ORIGIN 243.138.128.in-addr.arpa.
1           IN  CNAME  1.0-63
2           IN  CNAME  2.0-63
...
63          IN  CNAME  63.0-63
64          IN  CNAME  64.64-127
65          IN  CNAME  65.64-127
...
```

To delegate the 0-63 piece of the reverse zone to the customer that has been assigned that subnet, we'd add the following NS records:

```
0-63        IN  NS   ns1.customer1.com.
0-63        IN  NS   ns2.customer1.com.
...
```

customer1.com's site would have a zone file that contained the reverse mappings for the 0-63.243.138.128.in-addr.arpa zone.

For example,

```
1           IN  PTR   host1.customer1.com.
2           IN  PTR   host2.customer1.com.
...
```

By adding this extra component, we create a new "cut" at which to perform delegation. When someone looks up the reverse mapping for 128.138.243.1, for example, the CNAME record at 1.243.138.128.in-addr.arpa refocuses the search to the name 1.0-63.243.138.128.in-addr.arpa, which is controlled by the customer.

Early in the life of the CNAME hack, the $GENERATE command was added to BIND’s repertoire to facilitate the creation of resource records in the parent zone. For example, the following lines produce the records for the first subnet:

```
$ORIGIN 243.138.128.in-addr.arpa.
$GENERATE 0-63 $ CNAME $0-63
0-63      NS  ns1.customer1.com.
0-63      NS  ns2.customer1.com.
```

The $ in the $GENERATE command (itself a BIND extension) iterates from 0 to 63 and creates 64 different CNAME records. The other three /26 networks would be handled similarly.

## SRV records

An SRV record specifies the location of services within a domain. For example, the SRV record lets you query a remote domain for the name of its FTP server. Before SRV, you had to hope the remote sysadmins had followed the prevailing custom and added a CNAME for "ftp" to their server’s DNS records.

SRV records make more sense than CNAMEs for this application and are certainly a better way for sysadmins to move services around and control their use. However, SRV records must be explicitly sought and parsed by clients, so it will be a while before their effects are really felt. They are used extensively by Windows.

SRV records resemble generalized MX records with fields that let the local DNS administrator steer and load-balance connections from the outside world. The format is

```
service.proto.name [ttl] [IN] SRV pri wt port target
```

where service is a service defined in the IANA assigned numbers database (see iana.org/numbers.htm), proto is either tcp or udp, name is the domain to which the SRV record refers, pri is an MX-style priority, wt is a weight used for load balancing among several servers, port is the port on which the service runs, and target is the hostname of the server that provides the service. To avoid a second round trip, DNS servers usually return the A record of the target with the answer to a SRV query.

A value of 0 for the wt parameter means that no special load balancing should be done. A value of "" for the target means that the service is not run at this site.

Here is an example snitched from the RFC2782 and adapted for atrust.com:

```
_ftp._tcp        SRV  0  0 21   ftp-server.atrust.com.
; 1/4 of the connections to old box, 3/4 to the new one
_ssh._tcp        SRV  0  1 22   old-slow-box.atrust.com.
                 SRV  0  3 22   new-fast-box.atrust.com.
; main server on port 80, backup on new box, port 8000
_http._tcp       SRV  0  0 80   www-server.atrust.com.
                 SRV 10  0 8000 new-fast-box.atrust.com.
```

> SRV records are specified in RFC2782 (2000).
