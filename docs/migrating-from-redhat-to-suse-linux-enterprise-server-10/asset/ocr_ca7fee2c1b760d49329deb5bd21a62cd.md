+   6. Configure the OCFS2 cluster services.
+      Make sure that **Cluster to start on boot** is the same as the entry in `/etc/ocfs2/cluster.conf`

```
```bash
da10:~ # /etc/init.d/o2cb configure
Configuring the O2CB driver.
This will configure the on-boot properties of the O2CB driver.
...
Load O2CB driver on boot (y/n) [y]: <ENTER>
Cluster to start on boot (Enter "none" to clear) [mycluster]: <ENTER>
Use user-space driven heartbeat? (y/n) [n]: <ENTER>
Writing O2CB configuration: OK
```
```

+   7. Start the storage cluster services automatically.
+      The following commands create the links in `/etc/init.d/rcx.d/` needed to start the services at boot time.

```
```bash
da10:~ # chkconfig -a o2cb
da10:~ # chkconfig -a ocfs2
```
```