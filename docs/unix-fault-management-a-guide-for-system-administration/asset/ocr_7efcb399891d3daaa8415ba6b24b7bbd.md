Additional fields specific to MC/ServiceGuard and MC/LockManager clusters are described in the following section. EPS clusters don't have any unique MIB variables. Note that this MIB does not include information on NFS or “diskless” clusters.

# ## HP MC/ServiceGuard MIB

The HP MC/ServiceGuard MIB is an extension of the HP Cluster MIB, providing additional MIB variables specific to the MC/ServiceGuard high availability product. A better name might have been the HP HA MIB, because it also supports the HP MC/LookManager high availability product.

# ### MIB Definition

Listing A-8 shows the complete specification for the HP MC/ServiceGuard MIB, as defined by Hewlett-Packard.

# **Listing A-8**  HP MC/ServiceGuard specification.

```
```
enterprises
    [11]  hp
        [2]  nm
            [3]  system
                [1]  general
                    [6]  hpmcCluster
                        [3]  hpmcTypeSpecific
                            [1]  hpmcSGCluster
                                [0]  hpmcSGTraps
                                    [1]  hpmcSGSubagentUp
                                    [2]  hpmcSGReconfig
                                    [3]  hpmcSGClusterUp
                                    [4]  hpmcSGClusterDown
                                    [5]  hpmcSGConfigChange
                                    [6]  hpmcSGPkgStart
                                    [7]  hpmcSGPkgUp
                                    [8]  hpmcSGPkgHalt
                                    [9]  hpmcSGPkgDown
                                    [10] hpmcSGSvcDown
                                    [11] hpmcSGPkgFlags
                                    [12] hpmcSGIPAddrUp
                                    [13] hpmcSGIPAddrDown
                                    [14] hpmcSGLocalSwitch
                                    [15] hpmcSGSubnetUp
                                    [16] hpmcSGSubnetDown
                                    [17] hpmcSGNodeUp
                                    [18] hpmcSGNodeHalted
                                    [19] hpmcSGNodeFailed
                                    [1]  hpmcSGObjects
```
```