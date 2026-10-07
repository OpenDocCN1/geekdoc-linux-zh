+   an IP address with an associated address mask. For example, 172.16.128/25 would match every address from 172.16.12.128 to 172.16.12.255.

**no_access** This defines the hosts that are denied access to the service. Hosts are defined exactly the same methods as those described above for the only_from attribute.

**access_times** This defines the time of day service is available, in the form hour:min-hour:min. A 24-hour clock is used. Hours are 0 to 23 and minutes are 0 to 59. Time restrictions have limited utility on an e-mail server. Users read e-mail 24 hours a day.

If neither only_from nor no_access is specified, access is granted to everyone. If both are specified, the most exact match applies—for example:

```
no_access      = 172.16.12.250
only_from      = 172.16.12.0
```

The only_from command in this example permits every system on network 172.16.12.0 to have access to the service. The no_access command takes away access for one system. It doesn't matter whether the no_access attribute comes before or after the only_from attribute. It always works the same way the more exact match takes precedence.

Listing 12.5 shows the server login from Red Hat 7 with some access controls added.

# Listing 12.5 xinetd Access Controls

```
# default: on
# description: logind is the server for the login(1) program. \
## The server provides a remote login facility with \\
# authentication based on privileged port numbers from \\
# trusted hosts.
service login
{
    socket_type      = stream
    wait            = no
    user            = root
    log_on_success  += USERID
    log_on_failure  += USERID
    only_from       = 172.16.12.0
    no_access       = 172.16.12.231
    server          = /usr/sbin/in.logind
```