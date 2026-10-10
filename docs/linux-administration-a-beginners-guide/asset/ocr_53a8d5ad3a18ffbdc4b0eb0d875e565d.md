+   - allow-transfer
+   - notify
+   - also-notify

Using any of these options in a zone configuration will affect only that zone. See the “Options” subsection in the discussion of /etc/named.conf earlier in this chapter for more information on how these options work.

# Updating the /etc/named.conf for a Secondary Zone

The zone entry format for secondary servers is very similar to that of master servers. For forward resolution, here is the format:

```
zone domain-name {
    type slave;
    masters { IP-address-list; };
};
```

where the domain-name is the exact same name as the primary name server, and the IP-address-list is the list of IP addresses where the primary name server for that zone exists.

A recommended additional option you can list in a secondary zone configuration is

```
file path-name;
```

where path-name is the full path location of where the server will keep copies of the primary’s zone files. By keeping a local copy, you can reduce bandwidth needs for updates and improve performance.

# Additional Options

A secondary zone configuration may also use some of the configuration choices from the options statement. These options are

+   - check-names
+   - allow-update
+   - allow-query
+   - allow-transfer
+   - max-transfer-time-in
+   - notify
+   - also-notify

See the “Options” subsection in the discussion of /etc/named.conf earlier in this chapter for more information on how these options work.