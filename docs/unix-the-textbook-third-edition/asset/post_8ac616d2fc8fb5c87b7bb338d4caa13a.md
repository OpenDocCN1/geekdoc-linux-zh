
## iocage create

A full jail has a fully independent ZFS dataset suitable for network replication (ZFS send/recv).

Clone (thin): Thin jails are lightweight clones created with:

```
# iocage create -c
```

Thin jails are cloned from the appropriate release at creation time and consume only a fraction of the space, preserving only the changing data.

Base: iocage basejails use independent read-only ZFS file system clones to achieve the same functionality.

To create a basejail:

```
# iocage create -b
```

Basejails reclone their base file systems at each startup. They are ideal for environments where patching or upgrades are required at once to multiple jails.

Template: Template is simply a jail where the template property is set to “yes.”

To turn a jail into a template:

```
# iocage set template=yes UUID|TAG
```

After this operation the jail can be listed with:

```
# iocage list -t
```

To deploy a jail from this template:

```
# iocage clone TEMPLATE_UUID tag=mynewjail
```

Templates can be converted back and forth by setting the template property.

Empty: Empty jails are intended for unsupported jail setups or testing.

To create an empty jail:

```
# iocage create -e
```

These are ideal for experimentation with unsupported releases or LINUX jails.

## 25.2.5 Best Practices

These are some generic guidelines for working with iocage-managed jails.

- Using PF (PF packet filter firewall) as a module: This is the default setting in the generic kernel.
- Always use an easily-recognizable tag for your jails and templates!

This will help you avoid mistakes and easily identify jails.

Set the notes property: Set the notes property to something meaningful, especially for templates and jails you might use only once in a while.

Check your firewall rules: When using IP or Internet Protocol firewall (IPFW) inside a VNET jail put firewall_enable="YES" firewall_type="open" into /etc/rc.conf at the start. This way you can exclude the firewall from blocking. Lock it down once you have tested everything. Also check PF firewall rules on the host if you happen to mix both.

Get rid of old snapshots: Remove snapshots you do not need, especially from jails where data is changing a lot!

Use the chroot subcommand: In case you need to access or modify files in a template or a jail which is in a stopped state, use:

```
# iocage chroot UUID | TAG
```

This way, you do not need to start the jail or convert the template.

## 25.2.6 Advanced Usage

Clones: When a jail is cloned, iocage creates a ZFS clone file system. Clones are cheap lightweight snapshots.

A clone depends on its source snapshot and file system. If you wish to destroy the source jail and preserve its clones, you need to promote the clone first, otherwise the source jail cannot be destroyed.

Create a clone: Clone myjail to myjail2 as follows:

```
# iocage clone myjail tag=myjail2
```

To clone a jail from an existing snapshot:

```
# iocage clone myjail@snapshotname tag=myjail3
```

Promoting a clone: To promote a cloned jail:

```
# iocage promote UUID | TAG
```

This step will reverse the clone and source jail relationship. Basically, the clone will become the source and the source jail will be demoted to a clone.

Then, you can remove the demoted jail with:

```
# iocage destroy UUID | TAG
```

Updating jails: Updates are handled with the freebsd-update utility. Jails can be updated while they are stopped or running.

To update a jail to the latest patch level:

```
# iocage update UUID | TAG
```

This will create a back-out snapshot of the jail automatically.
When you have finished updating and the jail is working correctly, simply remove the snapshot:

```
# iocage snapremove UUID|TAG@snapshotname
```

In the case where the update breaks the jail, simply revert back to the snapshot:

```
# iocage rollback UUID|TAG@snapshotname
```

If you wish to test updating without affecting a jail, create a clone and update it in the same way as outlined previously.

To clone a jail:

```
# iocage clone UUID|TAG tag=testupdate
```

Upgrading jails: Upgrades are handled with the freebsd-update utility. By default, the upgrade command will try to upgrade the jail to the host's release version (uname -r).

Based on the jail type property, upgrades are handled differently for basejails and nonbasejails.

Upgrading a nonbasejail: To upgrade a normal jail (nonbasejail) to the host's release:

```
# iocage upgrade UUID | TAG
```

This will upgrade the jail to the same release as the host.
To upgrade to a specific release:

```
# iocage upgrade UUID|TAG release=10.2-RELEASE
```

Upgrade basejail: To upgrade a basejail, first verify whether the jail is a basejail:

```
# iocage get type UUID|TAG
```

This command should return type "basejail".
The upgrade can be forced while the jail is online by the following:

```
# iocage upgrade UUID|TAG
```

This will forcibly reclone the basejail file systems while the jail is running (no downtime) and update the jails with the changes from the new release.

```
# iocage set release=10.1-RELEASE UUID|TAG
```

This will cause the jail to reclone its file systems from Release 10.1 on the next jail start.
This will not update the jail's files with changes from the next release!
