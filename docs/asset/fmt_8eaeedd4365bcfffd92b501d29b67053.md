
`/usr/sbin/binlogd` is RUNNING

`/usr/sbin/mountd` is RUNNING

`/usr/sbin/nfsd` is RUNNING

`/usr/sbin/smnsd` is RUNNING

*****

*****  Checking the synchronization between members  *****

*****

`molari-ics0`: delay:0.000976 offset:0.000488  Sun Apr 21 00:59:10 2002

`check_cds1_config` : Checking installed CDSLs

`check_cds1_config` : Successfully verified CDSL configuration

## 10.5.2 检查连接管理器子系统

现在让我们检查连接管理器子系统。`clu_get_info(8)` 命令提供有关集群及其所有集群成员的详细信息。该命令也从 `clu_check_config` 命令中执行。

```text
# /usr/sbin/clu_get_info -full

Cluster information for cluster babylon5

Number of members configured in this cluster = 1

memberid for this member = 1

Cluster incarnation = 0xb63fd

Cluster expected votes = 2

Current votes = 2

Votes required for quorum = 1

Quorum disk = dsk5h

Quorum disk votes = 1

Information on each cluster member

Cluster memberid = 1

Hostname = molari.dec.com

Cluster interconnect IP name = molari-ics0

Cluster interconnect IP address = 10.0.0.1

Member state = UP

Member base O/S version = Compaq Tru64 UNIX V5.1A (Rev. 1885)

Member cluster version = TruCluster Server V5.1A (Rev. 1312)

Member running version = INSTALLED

Member name = molari

Member votes = 1

csid = 0x10001
```

The `clu_quorum(8)` command is used for configuring or deleting a quorum disk and adjusting the quorum disk votes, individual member node votes, and overall expected votes. This command can also be used to display information about what quorum is in a cluster. For more detailed information concerning the `clu_quorum` command, please read Chapter 17 on the Connection Manager or the `clu_quorum(8)` reference page.

In any event, let's look at quorum in our new single-node cluster using the `clu_quorum` command.

```text
# /usr/sbin/clu_quorum

Cluster Quorum Data for: babylon5 as of Sun Apr 21 01:27:16 PDT 2002

Cluster Common Quorum Data

Quorum disk: dsk5h

File: /etc/sysconfigtab.cluster

Attribute                File Value

expected votes                     2

Member 1 Quorum Data

Host name: molari.dec.com                     Status: UP

File: /cluster/members/member1/boot_partition/etc/sysconfigtab

Attribute    Running Value    File Value

current votes    2             N/A

quorum votes     1             N/A

expected votes   2             2

node votes       1             1

qdisk votes      1             1

qdisk major      19            19

qdisk minor      384           384
```

## 10.5.3 Check the Cluster Alias Subsystem

The `cluamgr(8)` command is used to manage and report information and statistics about cluster aliases. As this cluster was just created, there should only be information about one cluster alias – the default cluster alias. Let’s see what information is provided.

```text
# /usr/sbin/cluamgr -s all

Status of Cluster Alias: babylon5.dec.com

netmask: 0

aliasid: 1

flags: 7<ENABLED,DEFAULT,IP_V4>

connections rcvd from net: 30

connections forwarded: 22

connections rcvd within cluster: 17

data packets received from network: 8796

data packets forwarded within cluster: 1361

datagrams received from network: 2190

datagrams forwarded within cluster: 37

datagrams received within cluster: 3068

fragments received from network: 0

fragments forwarded within cluster: 0

fragments received within cluster: 0

Member Attributes:

memberid: 1, selw=3, selp=1, rpri=1 flags=11<JOINED,ENABLED>
```

As we can see, the cluster alias is “babylon5.dec.com” and it only has one cluster member in the cluster. This is evident by the `memberid` field.

More information on cluster aliases can be found in Chapter 16 on the Cluster Alias Subsystem.

## 10.5.4 Check the Device Request Dispatcher (DRD) Subsystem

The command used to configure and report on the DRD subsystem is the `drdmgr(8)` command. Let’s use the `drdmgr` command to look at the properties of the disk containing the `cluster_root` file system.

First, let’s find out what disk is used for the `cluster_root` domain.
