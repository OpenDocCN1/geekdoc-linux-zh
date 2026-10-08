```
ftp                IN        CNAME     turtle.mytrek.com.
www                IN        A         192.168.0.1
                   
rabbit             IN        A         192.168.0.2
                   
lizard             IN        A         192.168.0.3
                   IN        HINFO     MAC MACOS
localhost          IN        A         127.0.0.1
```

The first two lines are comments about the server for which this zone file is used. Notice that the first two lines begin with a semicolon. The class for each of the resource records in this file is IN, indicating these are Internet records. The SOA record begins with an `@` symbol that stands for the zone’s domain. In this example, it is **mytrek.com**. Any host or domain name used throughout this file that is not terminated with a period has this domain appended to it. For example, in the following resource record, **turtle** has no period, so it automatically expands to **turtle.mytrek.com**. The same happens for **rabbit** and **lizard**. These are read as **rabbit.mytrek.com** and **lizard.mytrek.com**. Also, in the SOA, notice that the e-mail address for hostmaster uses a period instead of an `@` symbol; `@` is a special symbol in zone files and cannot be used for any other purpose.

# Nameserver Record

The next resource record specifies the name server for this zone. Here, it is **mytrek.com**. Notice the name for this resource record is blank. If the name is blank, a resource record inherits the name from the previous record. In this case, the NS record inherits the value of `@` in the SOA record, its previous record. This is the zone’s domain, and the NS record specifies **turtle.mytrek.com** as the name server for this zone.

```
IN           NS      turtle.mytrek.com.
```

Here the domain name is inherited. The entry can be read as the following. Notice the trailing period at the end of the domain name:

```
mytrek.com.  IN     NS        turtle.mytrek.com.
```

# Address Record

The following address records set up an address for the domain itself. This is often the same as the name server, in this case 192.168.0.1 (the IP address of **turtle.mytrek.com**). This enables users to reference the domain itself, rather than a particular host in it. A mail exchanger record follows that routes mail for the domain to the name server. Users can send mail to the **mytrek.com** domain and it will be routed to **turtle.mytrek.com**.

```
IN           A         192.168.0.1
```

Here the domain name is inherited. The entry can be read as the following:

```
mytrek.com.  IN      A         192.168.0.1
```

# Mail Exchanger Record

The next records are mail exchanger (MX) records listing **turtle.mytrek.com** and **fast.mytrek.com** as holding the mail servers for this zone. You can have more than one mail exchanger record for a host. More than one host may exist through which mail