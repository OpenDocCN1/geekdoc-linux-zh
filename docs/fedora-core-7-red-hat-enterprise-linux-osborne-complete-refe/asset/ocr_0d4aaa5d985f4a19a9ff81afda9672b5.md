If you want to turn on a service that is off by default, you can set its **disable** attribute to **no** and restart **xinetd** (alternatively, use **system-config-services On Demand** panel). The entry for the **Tftp FTP** server, **tftpd**, is shown here. An initial comment tells you that it is off by default, but then the **disable** attribute turns it on:

```
service tftp
{
    socket_type       = dgram
    protocol          = udp
    wait              = yes
    user              = root
    server            = /usr/sbin/in.tftpd
    server_args       = -s /tftpboot
    disable           = yes
    per_source        = 11
    cps               = 100 2
    flags             = IPv4
}
```

# TCP Wrappers

TCP wrappers add another level of security to **xinetd**-managed servers. In effect, the server is wrapped with an intervening level of security, monitoring connections and controlling access. A server connection made through **xinetd** is monitored, verifying remote user identities and checking to make sure they are making valid requests. Connections are logged with the **syslogd** daemon (see Chapter 27) and may be found in **syslogd** files such as */var/log/secure*. With TCP wrappers, you can also restrict access to your system by remote hosts. Lists of hosts are kept in the *hosts.allow* and *hosts.deny* files. Entries in these files have the format *service:hostname:domain*. The domain is optional. For the service, you can specify a particular service, such as FTP, or you can enter **ALL** for all services. For the hostname, you can specify a particular host or use a wildcard to match several hosts. For example, **ALL** will match on all hosts. Table 21-8 lists the available wildcards. In the following example, the first entry allows access by all hosts to the Web service, **http**. The second entry

| Wildcard | Description |
|---|---|
| ALL | Matches all hosts or services. |
| LOCAL | Matches any host specified with just a hostname without a domain name. Used to match on hosts in the local domain. |
| UNKNOWN | Matches any user or host whose name or address is unknown. |
| KNOWN | Matches any user or host whose name or address is known. |
| PARANOID | Matches any host whose hostname does not match its IP address. |
| EXCEPT | An operator that lets you provide exceptions to matches. It takes the form of list1 EXCEPT list2 where those hosts matched in list1 that are also matched in list2 are excluded. |

TABLE 21-8 TCP Wrapper Wildcards