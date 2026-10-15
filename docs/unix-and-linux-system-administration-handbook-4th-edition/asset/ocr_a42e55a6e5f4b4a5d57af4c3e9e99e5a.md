# Table 12.3 Important binaries, directories, and configuration files used by Ignite-UX

| Filename | Purpose |
|---|---|
| /etc/bootptab | Acts as a plain-text "database" for bootpd |
| /opt/ignite/inst1_boottab | Records IP addresses for booting PA-RISC clients |
| /opt/ignite/bin/bootbys | Updates clients that are already running HP-UX |
| /opt/ignite/bin/make_config | Creates config info file using an installation depot |
| /opt/ignite/bin/make_depots | Creates install depots from some source media |
| /opt/ignite/bin/manage_index | Adds a depot to the Ignite-UX index |
| /opt/ignite/sbin/setup_server | Shares /var/opt/ignite/clients over NFS |
| /var/opt/ignite/clients | Stores client configuration files (dir) |
| /var/opt/ignite/data | Traditionally used for installation depots (dir) |
| /var/opt/ignite/INDEX | Indexes all installation depots known to Ignite-UX |

The make_depots command extracts installation packages and sets them up as an operating environment depot for installation to clients. After you create a depot, run make_config to read the depot's contents and create a configuration file that describes them. The configuration becomes known to Ignite-UX by way of the manage_index command, which adds configurations to an INDEX file. A sample series of commands for version 11i v3 is shown below.

```
hp-ux% cd /opt/ignite/bin
hp-ux% sudo ./make_depots -s /dev/dsk/c2t2d0
    -d /var/opt/ignite/depots/Rel_B.11.31/oe_media
hp-ux% sudo ./make_config -s /var/opt/ignite/depots/Rel_B.11.31/core_media
    -c /var/opt/ignite/data/Rel_B.11.31/oe_media.cfg
hp-ux% sudo ./manage_index -n "HP-UX B.11.31 Default" -c "11i v3"
hp-ux% sudo ./manage_index -a
    -f /var/opt/ignite/data/Rel_B.11.31/oe_media.cfg -c "11i v3"
```

Before the server can be used by clients, you must enable BOOTP and share the clients directory. Individual clients must also be added to the inst1_boottab or bootptab file, depending upon whether they are PA-RISC or Itanium machines.

To share the config directory via NFS, just run /opt/ignite/sbin/setup_server. Behind the scenes, this command just creates an NFS share in /etc/dfs/sharetab.

You can turn on BOOTP by uncommenting the bootps line in /etc/inetd.conf. Then ask inetd to reread its configuration by running /usr/sbin/inetd -c.