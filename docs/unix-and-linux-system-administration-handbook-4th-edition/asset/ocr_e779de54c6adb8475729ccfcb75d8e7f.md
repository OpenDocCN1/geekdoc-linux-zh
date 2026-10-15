```
zone "example.com" (
    type master;
    file "filename";
    ...
```

The reverse zone statement should look like this:

```
zone "188.77.208.in-addr.arpa" {
    type master;
    file "filename";
    ...
```

+   - Make a note of the filenames listed as arguments to file in the forward and reverse zone definitions.

# Step 4b, for sites running NSD:

+   - Open the NSD configuration file, /etc/nsd/nsd.conf.

+   - Find the zone statement for your domain in nsd.conf (the name keyword identifies each zone).

+   - Verify that you are in fact on the master server. You can tell because the zone section for your domain will include a provide-xfr clause. If it contains a request-xfr clause, it's a slave server for that zone and you're on the wrong machine. The zone statement for the forward zone should look like:

```
zone:
  name: example.com
  zonefile: /var/nsd/primary/example.com
  provide-xfr: ip-addr tsig.key.name
  notify: ip-addr NOKEY
```

The reverse zone statement looks like:

```
zone:
  name: 188.77.208.in-addr.arpa
  zonefile: /var/nsd/primary/188.77.208.in-addr.arpa
  provide-xfr: ip-addr tsig.key.name
  notify: ip-addr NOKEY
```

+   - Make a note of the filenames listed as arguments to the zonefile keywords in the forward and reverse zone definitions.

# Step 5: Go to the zone file directory and edit the forward zone file. Find the records for the template host you identified earlier. They'll look something like this:

```
template    IN  A     208.77.188.100
            IN  MX   10 mail-hub
            IN  MX   20 template
```