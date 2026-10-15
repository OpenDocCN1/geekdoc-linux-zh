
### 监控说明

HP-UNIX MIB 的助记符根 OID 为 `iso.org.dod.internet.private.enterprises.hp.nm`。如果您打算编写自己的 SNMP 应用程序，您需要知道 HP-UNIX MIB 的数值根 OID 为 `1.3.6.1.4.1.11.2`。

HP 的 EMS HA Monitors 产品使用此 MIB 来监控系统上当前的用户和作业数量以及空闲文件系统空间的大小。

此 MIB 是查找有关系统上运行的特定进程的信息的有用场所，例如它们的 CPU 利用率、优先级和驻留集大小。但是，您可能很难使用 MIB 浏览器遍历大量的进程表条目；最好从自定义 SNMP 应用程序查询此信息。

请注意，此 MIB 包含有关 NFS 无盘集群的信息，但不包含有关 HP 高可用性集群或 EPS 集群的信息。有关这些集群的信息将在以下各节中提供。

## HP 集群 MIB

HP 集群 MIB 是由惠普提供的私有 MIB。它定义了高可用性和 EPS 集群的集群成员信息。

### MIB 定义

列表 A-7 展示了由惠普定义的 HP 集群 MIB 的完整规范。

#### 列表 A-7 HP 集群规范。

```text
enterprises
[11] hp
[2] nm
[3] system
[1] general
[6] hpmpCluster
[1] hpmpClusterObjects
[1] hpmpGenInfo
[1] hpmpNumClusters
[2] hpmpClusterTable
[1] hpmpClusterEntry
[1] hpmpClusterIndex*
[2] hpmpClusterName
[3] hpmpClusterType
[4] hpmpClusterDescr
[5] hpmpClusterSWVersion
[6] hpmpClusterState
[7] hpmpClusterLastStateChange
[8] hpmpClusterLastReconfig
[9] hpmpClusterPrimaryNode
[10] hpmpNodeStatus
[11] hpmpNodeLastEvent
[12] hpmpNodeLastEventTime
[13] hpmpClusterUpTime
[2] hpmpMemberInfo
[1] hpmpCNodeTable
[1] hpmpCNodeEntry
[1] hpmpNodeID*
[2] hpmpNodeName
[3] hpmpNodeRole
[2] hpmpClusterTypes
[1] hpmpServiceGuard
[2] hpmpNFSDiskless
[3] hpmpMCSE
[4] hpmpLockManager
[3] hpmpTypeSpecific
```

### 监控说明

如果您打算编写自己的 SNMP 应用程序，HP Cluster MIB 的根 OID 为 `1.3.6.1.4.1.11.2.3.1.6`。您可以使用此 MIB 来确定哪些系统属于集群的一部分，以及集群软件已运行了多长时间。

与 `MC/ServiceGuard` 和 `MC/LockManager` 集群相关的特定字段在下节中描述。EPS 集群没有任何独特的 MIB 变量。请注意，此 MIB 不包含关于 NFS 或“无盘”集群的信息。

## HP MC/ServiceGuard MIB

HP MC/ServiceGuard MIB 是 HP Cluster MIB 的扩展，提供了特定的 MC/ServiceGuard 高可用性产品的额外 MIB 变量。也许更好的名称是 HP HA MIB，因为它也支持 HP MC/LockManager 高可用性产品。

### MIB 定义

列表 A-8 显示了由 Hewlett-Packard 定义的 HP MC/ServiceGuard MIB 的完整规范。

**列表 A-8** HP MC/ServiceGuard 规范。

```text
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

续
