```
`[~]# firewall-cmd --permanent --ipset=test --get-entries 192.168.0.1`
```

You can add the IP set as a source to a zone to control all traffic coming in from any of the addresses listed in the IP set with a zone. For example, to add the test IP set as a source to the `drop` zone to drop all packets coming from all entries listed in the test IP set, use the following command as `root`:

```
```bash
[~]# firewall-cmd --permanent --zone=drop --add-source=ipset:test
success
```
```

The `ipset:` prefix in the source shows `firewalld` that the source is an IP set and not an IP address or an address range.

Only the creation and removal of IP sets is limited to the permanent environment, all other IP set options can be used also in the runtime environment without the `--permanent` option.

# ### 5.12.2. Configuring a Custom Service for an IP Set

To configure a custom service to create and load the IP set structure before `firewalld` starts:

+   1.  Using an editor running as `root`, create a file as follows:
+   ```bash
+   [~]# vi /etc/systemd/system/ipset_name.service
+   [Unit]
+   Description=ipset_name
+   Before=firewalld.service
+   
+   [Service]
+   Type=oneshot
+   RemainAfterExit=yes
+   ExecStart=/usr/local/bin/ipset_name.sh start
+   ExecStop=/usr/local/bin/ipset_name.sh stop
+   
+   [Install]
+   WantedBy=basic.target
+   ```

+   2.  Use the IP set permanently in `firewalld`:
+   ```bash
+   [~]# vi /etc/firewalld/direct.xml
+   <?xml version="1.0" encoding="utf-8"?>
+   <direct>
+     <rule ipv="ipv4" table="filter" chain="INPUT" priority="0">-m set \
+   -match-set <replaceable>ipset_name</replaceable> src -j DROP</rule>
+   </direct>
+   ```

+   3.  A `firewalld` reload is required to activate the changes:
+   ```bash
+   [~]# firewall-cmd --reload
+   ```
+   This reloads the firewall without losing state information (TCP sessions will not be terminated), but service disruption is possible during the reload.