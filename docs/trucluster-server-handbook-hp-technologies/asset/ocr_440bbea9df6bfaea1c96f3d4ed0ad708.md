Notice that rc.config is a CDSL and thus is member-specific. Also notice that rc.config requests the execution of a cluster common script named rc.config.common (approximately five lines down, bolded, in the above file). Thus systems in a cluster can be fed a variety of system-specific configuration items through /etc/rc.config as well as cluster common attributes through /etc/rc.config.common. (Details can be found in Chapter 6).

So when would we use this new rc.config.common file, and how do we add entries to it and otherwise interact with it? Traditionally, rc.config was altered through the rcmgr command. Yeah, we know. You probably just used vi(1) on the rc.config file. Technically you should be using the rcmgr command. This is especially important now that the file has been broken up into the cluster common and the member-specific parts. The rcmgr command has options that allow you to designate whether the changes are to be applied cluster wide (rc.config.common) or to a specific system (rc.config). The command options are "-c" (cluster wide) and "-h" (host specific). There is a third option on the rcmgr command that designates a site-specific rc.config file (rc.config.site). This file may contain variables describing characteristics of site-specific software.

# 19.3.7.3 The sysconfigtab File

There are other system configuration options that need to be addressed as well. Tru64 UNIX reads the contents of the /etc/sysconfigtab file to access system attributes and driver characteristics. This file is member-specific so that each member of the cluster may be tweaked as appropriate for the applications it will be running. Just as with rc.config, there will also be a cluster-wide version of sysconfigtab called /etc/sysconfigtab.cluster. So if all cluster members are exactly the same, the bulk of the system attributes can be reflected in the /etc/sysconfigtab.cluster file. Most system attributes placed in the cluster-wide file get merged into the member-specific /etc/sysconfigtab file upon boot (see /sbin/init.d/clu_min).

```
# fin /etc/sysconfigtab
/etc/sysconfigtab -> ../cluster/members/(memb)/boot_partition/etc/sysconfigtab
```

```
# ls -l /etc/sysconfigtab
-rwxr-xr-x 1 bin bin 22756 Dec 31 20:18 /etc/sysconfigtab
```