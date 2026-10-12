
After running this program, a file called classifiedworks.db is created in the current directory. After I move the file to the working directory of the named server on the ns2.evoknow.com machine, the secondary DNS configuration for the classifiedworks.com domain is complete.

## Configuring the reverse DNS server

If you own your network IP addresses, you will have to do reverse DNS for them. For example, if you own an IP network called 206.171.50.0 and use it in your forward DNS configuration for a domain called evoknow.com, you will have to set up a reverse DNS zone for this network. Here is how.

- 1. First, modify the /etc/named.conf file to include a new zone as follows:
- 2. Now you need to create db.206.171.50 in the working directory of the named server. Note that the filename for the reverse DNS zone can be anything, but it is customary to use the db.network-address names. This file is similar to the other zone files I have shown so far; the only difference is that it will have PTR records instead of A, CNAME, and so on. Listing 15-3 shows an example of the db.206.171.50 file.

```
zone "50.171.206.in-addr.arpa" {
    type master;
    file "db.206.171.50";
};
```

Notice the special zone name (50.171.206.in-addr.arpa) used in the preceding zone configuration. To create a reverse DNS zone name, you must reverse your network number and append in-addr.arpa at the end of the name.

Listing 15-3 An example reverse DNS zone file (db.206.171.50)

```
@   IN  SOA ns.evoknow.com. kabir.evoknow.com. (
        1999020100  ; Serial
        7200        ; Refresh - 2 hours
3600      ; Retry  - 1 hour
43200     ; Expire - 12 hours
3600 )    ; Minimum - 1 hour
```

```
IN NS ns.evoknow.com.
```

```
51.50.171.206.in-addr.arpa.  IN PTR ns.evoknow.com.
52.50.171.206.in-addr.arpa.  IN PTR mail.evoknow.com.
53.50.171.206.in-addr.arpa.  IN PTR www.evoknow.com.
```

Here, the PTR records are provided to map three different IP addresses to three different hostnames. You can also specify the preceding PTR records in shortened form as follows:

```
51  IN  PTR ns.evoknow.com
52  IN  PTR mail.evoknow.com
53  IN  PTR www.evoknow.com
```

In most cases, your ISP will own the IP addresses for your network and should be prepared to provide master reverse DNS service. However, there is one special network for which you must provide reverse name service: 127.0.0, which is used for the local loopback interface IP (127.0.0.1). Because no one has authority over this loopback network, everyone must provide reverse DNS service themselves. This is why you will always need to have a special zone statement in your /etc/named.conf file that looks like the following:

```
zone "0.0.127.in-addr.arpa" {
    type master;
    file "named.local";
};
```

- 3. You will also have to have the named.local zone file in the working directory of your name server. This file is shown in Listing 15-4.

## Listing 15-4 The named.local file

```
@  IN  SOA  localhost.  root.localhost. (
    1999020100  ; Serial
    7200        ; Refresh - 2 hours
    3600        ; Retry  - 1 hour
    43200       ; Expire - 12 hours
    3600 )      ; Minimum - 1 hour

    IN  NS  localhost.

1   IN  PTR  localhost.
```

## Configuring a cache-only slave DNS server

Technically, all DNS servers are cache-enabled; that is, DNS servers use cache by default. However, if you do not want to provide DNS service for any Internet domains and desire only to improve DNS query performance for your network, you can run a cache-only DNS server. Such a server will have an /etc/named.conf file as shown in Listing 15-5.

## Listing 15-5 An example /etc/named.conf file

```
zone "." {
    type hint;
    file "named.ca";
};

zone "0.0.127.in-addr.arpa" {
    type master;
    file "named.local";
};
```

The first zone statement specifies that the name server use the named.ca file to determine root name server names at startup. And the second zone statement provides the reverse name service for the local loop-back network. That's all you need to create a cache-only name server.

## Controlling the DNS server

The named distribution comes with a nifty program called ndc that provides a simple command-line interface for controlling the name server. Using this tool you can start and stop the name server; reload DNS configuration files, and also view statistics.

## Starting the name server

Your name server should start automatically at boot. If it does not start automatically, you need to take the following steps:

- 1. Log into your name server system as root and change directory to `/etc/rc.d/init.d`. Make sure that you have a script called named in this directory. If you are missing this script, you should reinstall the BIND distribution RPM from your Red Hat CD-ROM.
- 2. After you have confirmed that you have the `/etc/rc.d/init.d/named` script, change to your default system run level's (see `/etc/inittab`) rc directory. For most systems the default run level is 3; if yours is also the same, change directory to `/etc/rc.d/rc3.d/`.
- 3. Make a symbolic link called SXXnamed that points to the `/etc/rc.d/init.d/named` script. Replace XX in SXXnamed with a high number such as 55 or 85 to ensure that the system does not try to start the name server before network interfaces are set up properly. For example, to make a symbolic link called S55named to point to the named script, you can run the following command:

```
ln -s /etc/rc.d/init.d/named S55named
```

After you have created this link, your system will start the name server every time you boot your system. If, however, you prefer to run the name server manually, you can use the ndc program as follows:

```
ndc start
```

## Reloading new name server configuration

After you modify any of the zone files or the /etc/named.conf file, you must restart the name server to make the changes effective. You can force the name server to reload the new configuration as follows:

```
ndc reload
```

Don't forget to modify the serial number in the SOA record for any zone file you modify, or else the name server will not load the new configuration. To restart the name server by killing it first, you can use restart instead of reload in the preceding line.

## Stopping the name server

If for any reason you need to stop the name server, just run the ndc command as follows:

```
ndc stop
```

## Viewing name server statistics

You can use the ndc program to generate various name server statistics in the working directory of the name server. Run the following command:

```
ndc stats
```

This command will create a file called named.stats in the name server's working directory. This statistics file will show various items of information, including the number of queries per resource record.

## Testing Your DNS Server

Every time you modify your DNS information, do not forget to test the configuration using a name server query tool. In this section I discuss how you can test your name server configurations by using the dig utility.

![](img/9eb7e89292d2f85707b4d49102c865b7_488_0.png)

Many tools are available for manually querying name servers, including dig. If you would like to have a few commonly used query tools, install the bind-utils RPM distribution from your Red Hat CD-ROM. The bind-utils distribution comes with dig, dnsquery, host, nslookup, and more.

Say that you just registered a new domain with Internic and have already set up the necessary DNS configuration on your name server. After restarting the name server, you want to test the configuration via dig. You can run dig using the following syntax:

```
dig @nameserver domain [query_type]
```

The nameserver can be a DNS server's host name or IP address. If you're running dig on the same machine as the DNS server you wish to test, you don't need to specify the DNS server using @nameserver as long as your /etc/resolv.conf has a line that makes the target DNS server the default name server for that machine. The domain in the above syntax is the domain name or the host name for which you want to find a DNS record of type query_type. By default query_type is set to A (Address) record. For example:

```
dig @ns.aminews.com evoknow.com ns
```

Here the DNS server ns.aminews.com is asked to locate NS record for evoknow.com domain. Let's look at another example:

```
dig www.evoknow.com A
```

Here the default DNS server (i.e., the one set in /etc/resolv.conf) is being asked to locate the A (Address) record for a host name called www.evoknow.com.

As you can see, you can use dig to dig up your DNS configuration quite easily by pointing it to the right name server and asking for the query types that you wish to check.
