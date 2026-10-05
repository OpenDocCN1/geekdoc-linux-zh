# The Domain Name Service CHAPTER 8

# Zone Data File Naming Conventions

A zone data file can be given any name. For maintainability, however, a naming convention should be used. This chapter uses the following conventions:

+   * The cache (root server) data file is called root.hint because the SuSE installation it created with that name. For the same reason, the reverse DNS file for the loopback at 127.0.0.1 is called 127.0.0.zone.
* Master forward DNS data files are the word named, followed by a period, followed by the entire domain name. For example, the master forward DNS data file for domain.cxm is named domain.cxm.
* Master reverse DNS zone files are the word named, followed by a period, followed by the IP number of the subnet. In instance, the reverse DNS zone data file for subnet 192.168.42 is named 192.168.42. Many people reverse the IP address to match the 42.168.192-in.arpa statement. The naming convention is entirely up to you.

# Zone Data Substitutions

As mentioned previously, the file statement in the named.conf zone record points to the zone data file describing the zone. Because the domain is specified by the named.conf zone record, that domain is substituted for the @ symbol anywhere it appears in the zone data file. The same is true for reverse DNS subnets. Furthermore, in the zone data file, any name ending in a period is assumed to be relative to the domain specified in named.conf. For instance, if the domain is specified in named.conf is domain.cxm, and the name numark appears unterminated by a period inside the zone data file, that word numark marks the same as the absolute version, numark.domain.cxm. (note the terminating period).

# Zone Data File Components

The zone's line in the /etc/named.conf points to a file containing the information that needs to answer queries on the zone's domain. The file format for these configuration files is a bit tricky, unfortunately, and requires care when you're setting it up. Be especially careful with periods—a misplaced period can quickly become difficult to track down.

The format of each line in the configuration file is as follows:

```
name IN record_type data
```

Here name is the hostname with which you are dealing. Any hosts that do not end in a period have the domain name appended to them automatically.

![](bbox=[0.868, 0.453, 0.991, 0.703])