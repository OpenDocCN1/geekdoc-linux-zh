
```text
1. $TTL 2D
2. 1.168.192.in-addr.arpa. IN SOA gateway.world.cosmos.
                              root.world.cosmos. (
3.                              2001040901       ; serial
4.                              2D               ; refresh
5.                              2H               ; retry
6.                              1W               ; expiry
7.                              2D )             ; minimum
8.
9.                              IN NS            gateway.world.cosmos.
10.
11. 1                            IN PTR          gateway.world.cosmos.
12. 2                            IN PTR          earth.world.cosmos.
13. 3                            IN PTR          mars.world.cosmos.
```

## File 51: Reverse Lookup

**Line 1:** `$TTL` defines the standard TTL that applies to all entries here.

**Line 2:** ‘Reverse lookup’ should be activated with this file for the network `192.168.1.0`. Since the zone is called ‘1.168.192.in-addr.arpa’ here, it is, of course, undesirable to add this to the host name. Therefore, these are all entered complete with domain and ending with ‘.’. The rest corresponds to the previous example described for world.cosmos.

**Line 3–7:** See the previous example for world.cosmos.

**Line 9:** This line also specifies the name server responsible for this zone. This time, however, the name is entered completely with domain and ending with ‘.’.

**Line 11–13:** These are the pointer records which are linked to an IP address at the respective host name. Only the last part of the IP address is entered at the beginning of the line missing the last ‘.’. Now, if the zone is appended to this and the in-addr.arpa is neglected, the entire IP address will be backwards.

In this form, the zone files are usable both for BIND8 and BIND9. Zone transfers between different versions should not normally be an issue.

## DNS Sample Configuration

In the sample configuration of a name server illustrated here, we will make the following assumptions: your domain name is world.cosmos, you have a gateway host which establishes the Internet connection, and there are two company internal networks connected to one another. This host will be our name server and will receive the name “gateway”. Your network appears as follows:

Network 1 includes the hosts:

- gateway IP 192.168.1.1
- earth IP 192.168.1.2
- mars IP 192.168.1.3

Network 2 includes the hosts:

- gateway IP 192.168.0.1
- sun IP 192.168.0.2
- moon IP 192.168.0.3

The hosts earth and mars are only connected with sun and moon via the gateway, just as all hosts can only access the Internet via gateway.

The following files are needed to configure the name server:

- **named.conf** the central configuration file
- **world.zone** contains the host table
- **192.168.1.zone** for the subnetwork with the hosts earth and mars
- **192.168.0.zone** for the subnetwork with the hosts sun and moon
- **localhost.zone** contains the IP address of the local host
- **127.0.0.zone** loopback
- **root.hint** contains the Internet root servers

The `localhost.zone`, `127.0.0.zone`, and `root.hint` files are automatically created during installation of BIND 8.
The file `/etc/named.conf` will have to be adjusted as in File 52.

```conf
acl internal { 127.0.0.1; 192.168.1/24; 192.168.0/24; };

options
{
    directory "/var/lib/named";
    allow-query { internal; };
    forwarders { 10.0.0.1; };
#   listen-on port 53 { 127.0.0.1; 192.168.0.1; 192.168.1.1; };
#   query-source address * port 53;
    cleaning-interval 120;
    statistics-interval 0;
    notify no;
};

zone "world.cosmos" in {
    type master;
    file "world.zone";
};

zone "0.168.192.in-addr.arpa" in {
    type master;
    file "192.168.0.zone";
};

zone "1.168.192.in-addr.arpa" in {
    type master;
    file "192.168.1.zone";
};

zone "localhost" in {
    type master;
    file "localhost.zone";
};

zone "0.0.127.in-addr.arpa" in {
    type master;
    file "127.0.0.zone";
};

zone "." in {
    type hint;
    file "root.hint";
};
```

### File 52: File named.conf

acl is the access control list that defines from which IP addresses access can be made to the DNS server.
The directory entry specifies where the other configuration files are located. `/var/lib/named/` is the default.
The process ID of named is stored in the pid-file.
`listen-on` Port defines the port from which the name server receives requests.
zone entries specify the configuration files to which IP addresses and host names are assigned to one another. These files will have to be set up in the next step in the `/var/lib/named/` directory.
The complete host table is entered in the `world.zone` file (see File 53). It consists of the following:

```text
$TTL 2D

world.cosmos. IN SOA        gateway    root.world.cosmos (
                            2001040501 ; serial
                            1D         ; refresh
                            2H         ; retry
                            1W         ; expiry
                            2D )       ; minimum

                            IN NS      gateway
                            IN MX      10 sun

gateway     IN A           192.168.0.1
            IN A           192.168.1.1
sun         IN A           192.168.0.2
moon        IN A           192.168.0.3
earth       IN A           192.168.1.2
mars        IN A           192.168.1.3
```

### File 53: The File /var/lib/named/world.zone

The option `$TTL` specifies the “time to live”. “SOA” stands for “start of authority” and introduces the preset record: host name, e-mail address (where the “@” sign is replaced with a “.”), serial number (date and double-digit version number), and TTL. “NS” marks the name server. “A” signals that the IP addresses of the hosts will follow in the domain. The name server “gateway” has two IP addresses, because it belongs to two subnetworks.
In the next two zone files, the reverse lookup takes place for both subnetworks. See the sample files 54 and 55 on the facing page.

```text
$TTL 2D

0.168.192.in-addr.arpa. IN SOA gateway.world.cosmos. root.world.cosmos. (
                              2001040501     ; serial
                              1D             ; refresh
                              2H             ; retry
                              1W             ; expiry
                              2D )           ; minimum

       IN NS                 gateway.world.cosmos.

1      IN PTR                gateway.world.cosmos.
2      IN PTR                sun.world.cosmos.
3      IN PTR                moon.world.cosmos.
```

### File 54: The File 192.168.0.zone

```text
$TTL 2D
1.168.192.in-addr.arpa. IN SOA gateway.world.cosmos. root.world.cosmos. (
                              2001040501     ; serial
                              1D             ; refresh
                              2H             ; retry
                              1W             ; expiry
                              2D )           ; minimum

       IN NS                 gateway.world.cosmos.

1      IN PTR                gateway.world.cosmos.
2      IN PTR                earth.world.cosmos.
3      IN PTR                mars.world.cosmos.
```

### File 55: The File 192.168.1.zone

Now, start the name server as root with the command `rcnamed start`. Other hosts in the network only need to set up the name service with the YaST2 Control Center under ‘Network/Basic’ → ‘Host Name & DNS’.

Now, if you enter `nslookup earth` in a console, you should see an output of the name server with IP address and the IP address of the host earth. If the name server is not functioning, you will find the cause in the `/var/log/messages` file.

## For More Information

- Documentation on package bind8: file: `/usr/share/doc/packages/bind8/html/index.html`.
- A sample configuration can be found at: `/usr/share/doc/packages/bind8/sample-config`
- The man page for named (`man 8 named`) in which the relevant RFCs are named and the man page for `named.conf` (`man 5 named.conf`).
