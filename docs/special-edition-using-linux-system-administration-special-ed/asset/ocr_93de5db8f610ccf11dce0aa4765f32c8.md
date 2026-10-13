practice is to use the date as the serial number in the format YYYYMMDDNN where YYYY is the year, MM is the month, DD is the day of the month, and NN is a specific revision on the given day. This means that up to 100 changes (from 00-99) can be made on any given day to the zone file.

+   - **The refresh value:** Indicates how often secondary name servers should consult the primary to see whether changes need to be downloaded. Typically, this value is in seconds but can be specified in other units such as 8H, which indicates 8 hours.
+   - **The retry value:** Indicates how long a secondary name server should wait after a failed attempt at a zone transfer from the primary before trying again. Typically, this value is in seconds but can be specified in other units such as 2H, which indicates 2 hours.
+   - **The expiry value:** Indicates the maximum amount of time a secondary name server can use the zone information before it must refresh its zone information from the primary. Typically, this value is in seconds but can be specified in other units such as 1W, which indicates 1 week.
+   - **The minimum value:** Indicates the time to live (TTL) value. A name server must retain an answer from the primary server in its cache for at least this amount of time before it can query the server again for the same information. Typically, this value is in seconds but can be specified in other units such as 1D, which indicates one day.

The remainder of this zone file contains four types of records:

+   - NS records
+   - A records
+   - CNAME records
+   - MX records

The NS record indicates a server acting as a name server for the zone. Zone files can contain more than one record indicating the primary and secondary servers for the domain. In this case, a single record exists of the form:

```
IN  NS  <host name>
```

> **Note:** You should have A records for any name server which is part of the domain being defined by the zone file. If you use a backup name server which is part of another domain, no A record is needed in the zone file and instead will appear in the zone file for the primary name server of the other domain.

The A records associate default hostnames in the domain with IP addresses. For instance, the record

```
fake    IN  A   192.168.1.1
```