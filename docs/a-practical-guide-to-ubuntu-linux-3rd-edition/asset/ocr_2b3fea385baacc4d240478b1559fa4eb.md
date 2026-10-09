Context: **server config**
Specify in **httpd.conf**
Default: 5
Ubuntu: 5 (prefork MPM) or 2 (worker MPM)

# ## NETWORKING DIRECTIVES

**HostnameLookups**
*Specifies whether Apache puts a client's hostname or its IP address in the logs.*

**HostnameLookups On | Off | Double**

**On:** Performs DNS reverse name resolution (page 831) to determine the hostname of each client for logging purposes.

**Off:** Logs each client's IP address.

**Double:** To provide greater security, performs DNS reverse name resolution (page 831) to determine the hostname of each client, performs a forward DNS lookup to verify the original IP address, and logs the hostname. Denies access if it cannot verify the original IP address.

Contexts: **server config**, **virtual host**, directory
Specify in **httpd.conf**
Default: Off
Ubuntu: Off

# Lookups can consume a lot of system resources

> Use the **On** and **Double** options with caution: They can consume a lot of resources on a busy system. You can use a program such as logresolve to perform reverse name resolution offline for statistical purposes.
> 
> If you perform hostname resolution offline, you run the risk that the name may have changed; you usually want the name that was current at the time of the request. To minimize this problem, perform the hostname resolution as soon as possible after writing the log.

**Timeout**
*Specifies the amount of time Apache waits for network operations to complete.*

*Timeout* *num*

where *num* is the number of seconds that Apache waits for network operations to finish. You can usually set this directive to a lower value; five minutes is a long time to wait on a busy server. The Apache documentation says that the default is not lower “because there may still be odd places in the code where the timer is not reset when a packet is sent.”

Context: **server config**
Specify in **httpd.conf**
Default: 300
Ubuntu: 300