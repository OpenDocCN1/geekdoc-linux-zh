# Time to Live Value

The very first entry in the zone file is usually the zone's time to live (TTL) value. Caching DNS servers cache the responses to their queries from authoritative DNS servers. The authoritative servers not only provide the DNS answer but also provide the information's time to live, which is the period for which it's valid.

The purpose of a TTL is to reduce the number of DNS queries the authoritative DNS server has to answer. If the TTL is set to three days, then caching servers use the original stored response for three days before making the query again.

# DNS Resource Records

The rest of the records in a zone file are usually BIND resource records. They define the nature of the DNS information in your zone files that's presented to querying DNS clients. They all have the general format:

# Name Class Type Data

There are different types of records for mail (MX), forward lookups (A), reverse lookups (PTR), aliases (CNAME), and overall zone definitions, Start of Authority (SOA). The data portion is formatted according to the record type and may consist of several values separated by spaces. Similarly, the name is also subject to interpretation based on this factor.

# The SOA Record

The first resource record is the Start of Authority (SOA) record, which contains general administrative and control information about the domain. It has the format:

```
Name Class Type Name-Server Email-Address Serial-No Refresh Retry Expiry Minimum-TTL

@     IN    SOA ns1.split.ac.in.  hostmaster.split.ac.in. ( 
                              2004100801 ; serial #
                              4H         ; refresh
                              1H         ; retry
                              1w         ; expiry
                              1d  )      ; minimum
```

> In the above figure Name - @, Class – IN (Internet Class) Type-SOA, Name-Server – ns1.split.ac.in., email-Address-hostmaster.split.ac.in., Serial No-2004100801, Refresh-4H, retry-1W, Minimum –TTL-1D

# Troubleshooting Bind

One of the most common culprits of BIND problems is incorrectly located in chroot files. If you have the BIND chroot package installed, make sure that the configuration files are located in the chroot directory.

Following is a quick list of errors that indicate your files may not be located correctly.

+   - The named daemon starts without loading any zone files. Here is a sample of the /var/log/messages file that shows that named doesn't load them:

```
Nov  9 17:35:41 netmon named[1211]: starting BIND 9.2.3 -u named -t
/var/named/chroot
Nov  9 17:35:41 netmon named[1211]: using 1 CPU
Nov  9 17:35:41 netmon named[1211]: loading configuration from
```