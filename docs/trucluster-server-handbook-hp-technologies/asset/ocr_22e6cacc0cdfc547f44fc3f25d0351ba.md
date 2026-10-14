```
Patches installed on the system came from following patch kits:
------------------------------------------------------------
- T64V51AS0001-20001114 OSP510
- T64V51AS0001-20001114 TCR510
- T64V51AS0002-20001204 OSP510
- T64V51AS0002-20001204 TCR510
- T64V51AS0003-20010521 OSP510
- T64V51AS0003-20010521 TCR510

NOTE
When a patch kit is listed, it does not necessarily mean
all patches on that kit are installed on your system.
```

Or

```
# grep KITNAME /var/adm/patch/log/event.log
KITNAME=<T64V50AS0001-20000718> TCR505, OSP505
KITNAME=<T64V50AS0001-20000718> OSP505, TCR505
KITNAME=<T64V51AS0001-20001114> TCR510, OSP510
KITNAME=<T64V51AS0001-20001114> OSP510, TCR510
KITNAME=<T64V51AS0002-20001204> OSP510, TCR510
KITNAME=<T64V51AS0002-20001204> TCR510, OSP510
KITNAME=<T64V51AS0003-20010521> TCR510, OSP510
KITNAME=<T64V51AS0003-20010521> OSP510, TCR510
```

Both examples show that Patch Kits 1, 2, and 3 are installed for Tru64 UNIX version 5.1 and TruCluster Server version 5.1. For more information on the separate Patch Kits, we refer you to each Patch Kit's Patch Summary and Release Notes document.

# 25.11 The Non-Rolling Patch Upgrade

While the current patch strategy of performing a Rolling Upgrade is designed to provide the greatest amount of availability, many systems managers have indicated that this high availability option is not utilized for mission critical services. Although the cluster is up and available, as soon as the installation of a Patch Kit starts, the cluster is considered to be down and therefore unavailable. Understandably, systems managers want a solution to apply patches that is simpler, quicker to implement, and minimizes the number of reboots.

The cluster engineers at HP have come up with an inventive solution to this new requirement. Instead of performing a Rolling Upgrade for a Patch Kit, they will provide new functionality to allow for a Non-Rolling Patch Upgrade.

How would this work? The dupatch program will be modified to provide the option of patching the entire cluster as a single unit. dupatch will be run on one member of the cluster and once it completes the management of the patches, it will issue a command to the other cluster members to perform the patch propagation, the patch configuration, and the building of the individual kernels for each of the cluster members. This also means that while the Non-Rolling Patch Upgrade is in progress, there should be no users or user applications running on the cluster.