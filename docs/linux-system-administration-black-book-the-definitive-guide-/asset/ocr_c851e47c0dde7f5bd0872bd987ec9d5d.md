make this time frame too long, because the main down time for the master would be while you are restarting it to load new zone data. Once again, you have to enter this value in seconds. For a five-minute wait to try again, you might use:

```
300 ; 5 minutes
```

+   - *expire*—This variable tells any slave name servers how long to trust downloaded zone information before grabbing a new copy. The slave server needs to get a new version of the zone file at this point even if the serial number has not changed. Once every two months is often sufficient for this, but it still has to be entered in seconds. Assuming a 30-day month, the line might be:

```
5184000 ; 60 days
```

+   - *minimum*—This expresses the minimum amount of time a caching name server should store any record gleaned from this zone file. After this time span passes, the record is deleted according to the server’s own settings. Typically, people use a value of one day, or:

```
86400 ; 1 day
```

After the SOA resource record, the remaining file is populated with other types of resource records. The types available are listed in Table 11.4. Each record type has its own format.

An A record has the full format:

```
host            ttl             class         A         Ipadress
```

# **Table 11.4** Resource record types in zone files.

| Type | Purpose |
| :--- | :--- |
| A | Specifies the IP address assigned to a host. |
| CNAME | Assigns a nickname (canonical name) to a host. |
| HINFO | Indicates the type of hardware this host is running on. |
| MX | Specifies where mail should be delivered to for this domain. |
| NS | Specifies the machine that provides name service for the domain. |
| PTR | Maps names to IP addresses. |
| SOA | Specifies the initial settings defining this zone. |
| WKS | Indicates which well-known services are available at which addresses. |