
# Exhibit D Solaris containers example

| Container 1 | Container 2 | Container 3 |
| --- | --- | --- |
| Global zone | Web server zone | Proprietary application zone |
| Default resource pool 1 CPU Fair share scheduling | | Proprietary resource pool 1 CPU |

Exhibit D shows three containers, one for the proprietary software, the web server, and the original (global) Solaris instance. In addition, there are three zones, one for the proprietary application, the web server, and global. There are two resource pools, each with one CPU.

The web server and the global zone share the default resource pool, which contains one CPU and uses the fair share scheduling algorithm. Each of the zones has one share (not depicted), meaning that CPU resources will be divided evenly between the global and web server zones. The proprietary application uses a separate resource pool with a dedicated CPU.

Solaris provides several command-line tools for managing containers, zones, and resources. Most importantly, zones and resource pools have a configuration tool and an administration tool: zonecfg, zoneadm, poolcfg, pooladm.

You must construct resource pools with pooladm before you can assign them to a zone. Enable pools with the -e flag, then run pooladm with no arguments to view the current status:

```
$ sudo pooladm -e
$ sudo pooladm
```

```
system default system.comment
int system.version 1
boolean system.bind.default true
string system.poold.objectives wt-load
```

...

We've truncated the lengthy output; the command continues to print the resource pool information and available CPU status. The default pool is called pool_default, and it includes all available CPU resources.

The poolcfg command creates a new pool. In the series of commands below, we allocate a single CPU to the proprietary resource set, assign the resource set to a new resource pool, and activate the pool.

```
solaris$ sudo poolcfg -c 'create pset proprietary-pset (uint pset.min=1; uint
pset.max=1)'
solaris$ sudo poolcfg -c 'create pool proprietary-pool'
solaris$ sudo pooladm -c
```

We can now create a zone with the zoneadm and zonecfg commands. Running zonecfg opens a new configuration shell for the zone. Conveniently, the tool supports-like features such as <tab> completion and cursor movement hot keys.

At a minimum, the zone must be:

- Created
- Given a source path for the zone files and systems;
- Given an independent IP address;
- Assigned to one of the system's active NICs;
- Assigned the resource pool we created above.

Here's how:

```
solaris$ sudo zonecfg -z proprietary-zone
zonecfg.proprietary-zone> set zonepath=/zones/proprietary-zone
zonecfg.proprietary-zone> set autoboot=true
zonecfg.proprietary-zone> add net
zonecfg.proprietary-zone.net> set address=192.168.10.123
zonecfg.proprietary-zone.net> set physical=e1000g0
zonecfg.proprietary-zone.net> end
zonecfg.proprietary-zone> set pool=proprietary-pool
 verify
zonecfg.proprietary-zone> commit
zonecfg.proprietary-zone> exit
```

Note that the zonecfg prompt shows you the object you're currently working on.

At this point the zone has been configured, but it is not actually installed or ready to run. This is a full Solaris system, and it needs to have packages installed, just as a normal system would. The zoneadm utility handles installs, boots, and performs other operations on the zone.

```
solaris$ sudo zoneadm -z proprietary-zone install
Preparing to install zone <proprietary-zone>
Creating list of files to copy from the global zone.
...
solaris$ sudo zoneadm -z proprietary-zone boot
global
proprietary-zone
```

# AIX workload partitions

## 1001 (Note: Page number or ID)

Now the zone is running, and an invocation of zlogin -C proprietary-zone will connect to its console. The boot process for a zone is like that of a physical system, connecting with zlogin before bootstrapping complete displays output the boot process. We must perform all the normal configuration for a new system, such as choosing login options and an authentication method.

The remaining task is to create a zone for our web server. The server zone will share the default resource pool with the global zone, it's not necessary to create a new pool. Instead, we would just create the zone with zonecfg as above, but with set-pool-pool-default.

There is considerably more depth to zones and containers that we've shown here. Advanced features that administrators should be aware of include migration of zones between physical systems (although migrations are not supported), ZFS resources for smaller whole-root zones, and "branded zones" that support running binaries from other platforms (e.g., Linux) on a Solaris kernel.

## 24.6 AIX WORKLOAD PARTITIONS

IBM has been in the virtualization game a long time. They pioneered the concept in the 1960s, but it wasn't until the release of AIX 6.1 that virtualization was included. WPARs (Workload Partitions) allow multiple instances of AIX to run on a single physical server, sharing resources while maintaining isolation.

WPARs can be of two types:
- Shared kernel: shares the kernel with the global root WPAR.
- Dedicated kernel: has its own kernel (though less common).

To manage WPARs, the `mkwpar` command is used to create them. The `lswpar` command is used to list them, and `stopwpar` and `rmwpar` are used to stop and remove them.

## Chapter 24 Virtualization

You create a system WPAR with the `mkwpar` command. The only required argument is `-n` to name it. Thus, `mkwpar -n mario` creates a partition.

The `lswpar` command is used to list WPARs from the global environment:

```
aix5 lswpar
```

| Name | Type | Hostname |
| --- | --- | --- |
| mario | A | /wpar/mario |

To attach a root to the console, use `clogin mario`. This simple example leaves a number of considerations and customization opportunities. For one, new software cannot be installed in the WPAR because the /usr and /opt filesystems are by default.

To create a more usable instance, you can buff up your `mkwpar` command with some additional arguments. The version below creates a WPAR with the following attributes:

- The name of the WPAR is mario (-n).
- Name resolution settings are inherited from the global instance (-r).
- Private, writable /opt and /usr filesystems are created (-I).
- The WPAR uses the IP address 192.168.10.15 on the en0 interface (-N).
- The CPU allocated to this WPAR will be a minimum of 5%, a soft maximum of 15%, and an absolute limit of 25% (-R).

```
aix5 mkwpar -n mario -r -I -n interface=en0 address=192.168.10.15 netmask=255.255.255.0 broadcast=192.168.10.255 -R active=yes CPU=5%-15%,25%
```

Application WPARs are handled very similarly. Instead of `mkwpar`, application WPARs are created with `wparexec`. Parameters are generally identical to those of `mkwpar`, rather than providing a name, you provide the execution as an argument. For example, to run Apache in its own application WPAR, simply use `wparexec/usr/local/sbin/httpd`.
