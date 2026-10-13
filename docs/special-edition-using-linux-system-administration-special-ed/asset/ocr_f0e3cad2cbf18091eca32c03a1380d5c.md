For instance an entry like the following:

```
foo.edu.     IN   NS   fake.foo.edu
```

will produce the following result:

```
foo.edu.     IN   NS   fake.foo.edu.foo.edu
```

Clearly this is far from what was intended. Notice the hostname `fake.foo.edu` is missing a dot at the end. Without the trailing dot the hostname is considered a relative name and the current domain name is appended to it. The resultant hostname therefore becomes `fake.foo.edu.foo.edu`.

Pay special attention to trailing dots when defining hostnames and domain names in zone files. Always test the entries you add to a zone file with nslookup to ensure the name resolution is what you expect it to be.

# FORGETTING TO INCREMENT THE SOA SERIAL NUMBER

This is a very common cause of DNS errors. After making changes to zone data you must remember to increment the serial number in the Start of Authority record. Without the serial number increment, the secondary name servers will not notice that a change has been made to the zone data on the primary name server, and the changes will not be downloaded by the secondary.

Any changes made on the primary name server’s zone data must be accompanied by a change in the SOA record’s serial number. The serial number must be incremented by at least one every time you make changes to the zone file. The secondary name servers for the domain check this number to decide whether an update to the zone information has been made on the primary name server. When it detects the serial number has been incremented, it downloads the updated zone files from the primary name server. Whenever you make changes to zone data, remember to test a secondary name server to ensure it recognized the change. How often the secondary name servers consult the primary to see whether changes need to be downloaded depends on the refresh value in the SOA record or the secondary name server.

If you need to force an immediate update of zone data on a secondary name server, restart named on that name server. When named starts on a secondary name server, it checks the serial numbers of the primary name server’s zone files, and downloads fresh copies of all updated zones.

# FORGETTING TO SIGNAL named AFTER MAKING CHANGES TO ZONE DATA

Sometimes you can forget to signal the primary name server after making changes to the named.conf file or the zone data files. The name server will not know that it needs to load the new data. As a result changes you have made will not take effect.

It is very important to check system logs to make sure the name server properly reinitialized, after you have made changes to zone data, and signaled named to restart. Syntax errors in the configuration or zone files may prevent named from starting up. It is also recommended to run