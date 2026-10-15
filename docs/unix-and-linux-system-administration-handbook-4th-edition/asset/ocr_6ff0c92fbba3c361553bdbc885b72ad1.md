tool through a -D command-line flag to named. Details can be found in the doc/README-DBUS file in the Red Hat BIND package.

# Table 17.18 BIND files in Linux

| File | Directory | Description |
|---|---|---|
| resolv.conf | /etc | Resolver library configuration file |
| named, lwres | /usr/sbin | Name server daemon |
| lwresd | /usr/sbin | Lightweight resolver |
| named.conf | /etc | named config file (RHEL and SUSE) |
|  | /etc/bind | named config file (Ubuntu) |
| named-checkconf | /usr/sbin | Checks the syntax of the config file |
| named-checkzone | /usr/sbin | Checks the syntax of zone files |
| namedGetForwarders | /usr/sbin | Red Hat only, for Network Manager tool |
| namedSetForwarders | /usr/sbin | Red Hat only, for Network Manager tool |
| nsswitch.conf | /etc | Service switch file |

Linux uses a switch file, /etc/nsswitch.conf, to specify how hostname-to-IP address mappings should be performed and whether DNS should be tried first, last, or not at all. If no switch file is present, the default behavior is

```
hosts: dns [!UNAVAIL=return] files
```

The !UNAVAIL clause means that if DNS is available but a name is not found there, the lookup attempt should fail rather than continuing to the next entry (in this case, the /etc/hosts file). If no name server were running (as might be the case during the boot process), the lookup process would consult the hosts file.

Our example distributions all provide the following default nsswitch.conf entry:

```
hosts: files dns
```

There is really no "best" way to configure the lookups—it depends on how your site is managed. In general, we prefer to keep as much host information as possible in DNS rather than in NIS or flat files, but we also try to preserve the ability to fall back to the static hosts file during the boot process if necessary.

![](bbox=[0.21, 0.885, 0.27, 0.945])

Ubuntu is the most up-to-date of our Linux distributions, with its distributed package being just a few months old. Programs and files have owner root and group owner "bind" with permissions set to allow access if named is invoked as user "bind" instead of root.

Some useful sample files are stashed in /etc/bind. Included are a named.conf file and zone files for root hints, localhost, the broadcast addresses, and private address space. The supplied named.conf includes the files named.conf.options and named.conf.local. It sets BIND's default directory to /var/cache/bind; as shipped, the directory exists but is empty.