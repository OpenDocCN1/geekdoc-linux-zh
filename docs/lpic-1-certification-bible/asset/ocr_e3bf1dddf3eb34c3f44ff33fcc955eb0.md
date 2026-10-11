# The CNAME record

The CNAME record is used to alias a host to another name. The syntax is as follows:

```
`alias      [ttl]      IN CNAME hostname`
```

For example:

```
`www          IN CNAME brain`
```

This example would give the alias of www to the host named brain. CNAMEs can point to other CNAMEs, and can be nested.

# The LOC record

The LOC is a rarely used record that shows the physical location of a service. The syntax is as follows:

```
`Name [ttl] IN LOC latitude longitude [alt [size [hp [up]]]]`
```

# The SRV record

The SRV record shows the locations of services in a domain. Using these records a user could look to see which hosts provide a service, such as FTP. The syntax is as follows:

```
`Service.protocol_name [ttl] IN SRV priority weight port target_host`
```

For example:

```
`ftp.tcp IN SRV 0 0 21 ftp.mydomain.org.`
```

This specifies that the FTP service is available on port 21/TCP of ftp.mydomain.org. The priority works like MX records, and the weight is used for load balancing.

![](bbox=[0.13, 0.695, 0.21, 0.72])

> Microsoft Windows 2000 makes extensive use of the SRV record.

# The TXT record

The TXT record adds any text information you want to the DNS information. The syntax is as follows:

```
`name [ttl] IN TXT "info"`
```

For example:

```
`Info IN TXT "Put the information in quotes"`
```