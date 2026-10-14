+   As soon as the software subset installation is complete, the individual subsets are configured as part of the system.

```
Configuring "TruCluster Migration Components" (TCRMIGRATES20)
Configuring "TruCluster Reference Pages" (TCRMANS20)
Running : /usr/sbin/mkwhatis : in the background...
Configuring "TruCluster Base Components" (TCRBASES20)
Use /usr/sbin/clu_create to create a cluster.
```

+   We can then verify that all the TruCluster Server software subsets are properly installed before we start to create the cluster.

```
# /usr/sbin/setld -i | grep -i TCR
TCRBASES20      installed          TruCluster Base Components (TruCluster(TM) Software)
TCRMANS20       installed          TruCluster Reference Pages (TruCluster(TM) Software)
TCRMIGRATES20   installed          TruCluster Migration Components (TruCluster(TM) Software)
```

# 10.3 Install the Tru64 UNIX and TruCluster Server Patches

Before we start the creation of the cluster, there are quite often patches or late fixes to the Tru64 UNIX and/or TruCluster Server software. As the installation of patches using HP's dupatch(8) facility installs patches for all "installed" software subsets instead of all "configured" or "active" software subsets, it would be most efficient to install the patches at this point in the process.

As of this writing, the latest patches for Tru64 UNIX and TruCluster Server can be obtained from the following website: http://www.support.compaq.com/patches

If you're asking, "Why are they installing patches now instead of after the creation of the cluster?" there are two answers. First, it takes less time to install patches at this point in the process than after the cluster is created as we do not have to go through the time-consuming process of performing a rolling upgrade of the cluster². The second and more important reason is that when we actually create the cluster, we want to have the best and most up-to-date software available to do so.

> ² Note a "No Roll" patch procedure is available in V5.1A patch kit 2 and later which will allow for a faster patching process in a cluster. See Chapter 25 for more information.