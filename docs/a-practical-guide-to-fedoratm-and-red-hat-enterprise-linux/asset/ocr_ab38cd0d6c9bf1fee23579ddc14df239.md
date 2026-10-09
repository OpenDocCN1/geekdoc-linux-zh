# # NETWORKING DIRECTIVES

**HostnameLookups**
*Specifies whether Apache puts a client's hostname or its IP address in the logs.*
`HostnameLookups On | Off | Double`
**On:** Performs DNS reverse name resolution (page 862) to determine the hostname of each client for logging purposes.
**Off:** Logs each client's IP address.
**Double:** To provide greater security, performs DNS reverse name resolution (page 862) to determine the hostname of each client, performs a forward DNS lookup to verify the original IP address, and logs the hostname. Denies access if it cannot verify the original IP address.
Contexts: **server config, virtual host, directory**
Default: **Off**

**Lookups can consume a lot of system resources**
Use the **On** and **Double** options with caution: They can consume a lot of resources on a busy system. You can use a program such as `logresolve` to perform reverse name resolution offline for statistical purposes.

If you perform hostname resolution offline, you run the risk that the name might have changed; you usually want the name that was current at the time of the request. To minimize this problem, perform the hostname resolution as soon as possible after Apache writes the log.

**Timeout**
*Specifies the amount of time Apache waits for network operations to complete.*
`Timeout num`
where `num` is the number of seconds that Apache waits for network operations to finish.
Contexts: **server config**
Default: **60**

**UseCanonicalName**
*Specifies the method the server uses to identify itself.*
`UseCanonicalName On | Off | DNS`
**On:** Apache uses the value of the `ServerName` directive (page 942) as its identity.
**Off:** Apache uses the name and port from the incoming request as its identity.
**DNS:** Apache performs a DNS reverse name resolution (page 862) on the IP address from the incoming request and uses the result as its identity. Rarely used.
This directive is important when a server has more than one name and needs to perform a redirect. Fedora/RHEL does not set this directive because it does not set the `ServerName` directive (page 942). Once you set `ServerName`, change `UseCanonicalName` to **On**. See page 962 for a discussion of redirects and this directive.
Contexts: **server config, virtual host, directory**
Default: **Off**