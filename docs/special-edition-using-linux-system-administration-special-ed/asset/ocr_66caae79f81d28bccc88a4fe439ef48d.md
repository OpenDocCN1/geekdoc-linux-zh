```
```text
    <IP address of secondary 1>;
    <IP address of secondary 2>;
    ...
};
```
```

This restricts zone transfers for all domains for which the server acts as the primary master. Alternatively, you can restrict zone transfers on a zone-by-zone basis in the zone sections of the named.conf file:

```
```text
zone "foo.edu" {
    type master;
    file "zone.foo.edu";
    allow-transfer {
        <IP address of secondary 1>;
        <IP address of secondary 2>;
        ...
    };
};
```
```

It is a good security measure to restrict zone transfers to designated slave servers only. This prevents hackers from listing the contents of your zones and obtaining host demographic information about your network. The less you can let the hacker know about your network the safer you are.

# RESTRICTING ZONE TRANSFERS FROM SECONDARY SERVERS

In addition to restricting zone transfers from the primary master to the secondary name servers, you should also restrict zone transfers from secondary servers.

If you are using dynamic updates, restrict dynamic updates for the domain using the allow-update directive in the zone sections of the named.conf file on the primary server:

```
```text
zone "foo.edu" {
    type master;
    file "zone.foo.edu";
    allow-update {
        <IP address of updater 1>;
        <IP address of updater 2>;
        ...
    };
};
```
```

In addition, you can prevent spoofing by denying recursion with the recursion directive in the options section of your name servers:

```
```text
recursion no;
```
```

# RESTRICTING QUERIES TO YOUR NAME SERVER

You can restrict queries for records outside the authoritative zone for which your server is the primary master or secondary name server to a restricted list of hosts (usually only hosts on the internal network or in the domains in the authoritative zones). To implement this type of