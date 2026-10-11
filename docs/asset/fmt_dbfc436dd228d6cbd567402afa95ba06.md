
TID : 298889976 PROC : db2agent (SAMPLE) 0

INSTANCE: db2inst1

NODE : 000

APPL : DB2INST1

AFFID : *_LOCAL.db2inst1.0631231208

FUNCTION: DB2UDB, High Availability Disaster Recovery,hdrEduStartup,probe:21152

MESSAGE : HdrStartup has completed.

2006-10-31.14.37.17.133766-E472045631

LEVEL: Event

PID : 29494

TID : 298889976 PROC : db2hadpr (SAMPLE) 0

INSTANCE: db2inst1

NODE : 000

FUNCTION: DB2UDB, High Availability Disaster Recovery,hdrSetHdrState,probe:10000

CHANGE : HADR state set to P-Remotecatchup (was P-RemotecatchupPending)

2006-10-31.14.37.14.144621-E1475456313

LEVEL: Warning

PID : 29494

TID : 298889976 PROC : db2hadpr (SAMPLE) 0

INSTANCE: db2inst1

NODE : 000

FUNCTION: DB2UDB, High Availability Disaster Recovery,hdrEduP,probe:20445

MESSAGE : near peer catchup starts at 00000088880c

2006-10-31.14.37.14.161868-E14785930

LEVEL: Warning

PID : 29494

TID : 298889976 PROC : db2hadpr (SAMPLE) 0

INSTANCE: db21

NODE : 000

FUNCTION: DB2UDB, High Availability Disaster Recovery,hdrTransitionToPeer,probe:10645

MESSAGE : near peer catchup starts at 00000088880c

2006-10-31.14.37.17.250094-E451F90329

LEVEL: Event

PID : 29494

TID : 298889976 PROC : db2hadpr (SAMPLE) 0

INSTANCE: db2inst1

NODE : 000

FUNCTION: DB2UDB# `db2diag.log`

使用 `db2diag.log` 的过滤输出，示例 4-9 中的命令用于查看主节点是否为备用节点。这对于执行 `db2 takeover` 命令之前的备用节点特别有用。

##### 示例 4-9 在 HADR 主节点上持续运行的状态检查

```tail -f db2diag.log | awk '/CHANGE : HADR state set to P-RemotecatchupPending (was P-NearlyPeer)/{print 1}/CHANGE : HADR state set to P-Peer (was P-NearlyPeer)/{print 0}'```

示例 4-10 显示了使用 `db2diag` 过滤 `db2diag.log` 输出的示例，以及从服务器看到的相应输出。

##### 示例 4-10 db2diag 过滤 db2diag.log 中的特定时间输出

```
db2diag -funcname="hdr" -f "%{month}-%{day} %(hour)%{min)%{sec} %(process)% %(changeevent)\t%{message}"

10-11-16.17 db2agent (SAMPLE) 0 INFO: HADR Start has begun.

10-11-16.17 db2agent (SAMPLE) 0 HADR state set to None (was Normal)

10-11-16.18 db2agent (SAMPLE) 0 HADR_LOCAL_HOST mapped to 9.43.86.68

10-11-16.18 db2agent (SAMPLE) 0 HADR_REMOTE_HOST Polonium mapped to 9.43.86.69

10-11-16.18 db2agent (SAMPLE) 0 INFO

10-11-16.18 db2agent (SAMPLE) 0 HADR state set to P-Boot (was None)

10-11-16.18 db2agent (SAMPLE) 0 INFO: Primary Start.

10-11-16.18 db2agent (SAMPLE) 0 HADR state set to RemoteCatchupPending (was P-Boot)

10-11-16.18 db2agent (SAMPLE) 0 INFO: RemoteCatchup

10-11-16.18 db2agent (SAMPLE) 0 remote catchup starts at 00000088880c

10-11-16.18 db2agent (SAMPLE) 0 HADR state set to P-Peer (was P-Peer)

10-11-16.18 db2agent (SAMPLE) 0 peer catchup starts at 00000088880c

10-12-09.20 db2agent (SAMPLE) 0 HADR state set to P-NearlyPeer (was P-NearlyPeer)

10-12-09.20 db2agent (SAMPLE) 0 Zero bytes received. Remote end may have closed connection

10-12-20.18 db2agent (SAMPLE) 0 HADR primary recv error.

10-12-09.20 db2agent (SAMPLE) 0 HADR state set to P-RemoteCatchupPending (was P-Peer)

10-12-09.59 db2agent (SAMPLE) 0 HADR state set to P-RemoteCatchup (was P-RemoteCatchupPending)
```

有关监控 HADR 的更多细节，请参考《DB2 9.1 Data Recovery and High Availability Guide and Reference, SC-10288》。

### 4.6 监控总结

关于 `snapshot`、`db2pd`、管理视图和表以及 `db2diag.log` 的这些章节总结了 DB2 Control Center 中的 Manage HADR 对话框等 GUI 界面之外跟踪 HADR 监控元素的方法。

如所见，每种方法都有其最适合场景：

- `get snapshot` 和 `db2pd` 输出可以互换使用，但有一些细微考虑。虽然 `get snapshot` 包含所有的监控元素而不仅仅是 HADR，且输出可能会填充几行，但它只需要 `SYMON` 最小权限，而 `db2pd` 需要 `SYSADM`。然而，这两种方法都需要数据库连接，因此目前均无法在备用数据库上运行。

### 5.1 客户端自动重路由概述

当客户端与数据库服务器之间的通信丢失时，客户端将接收到通信失败，并导致应用程序因错误终止。如果高可用至关重要，你应该实现冗余设置以及切换到冗余设置的能力。客户端自动重路由是 DB2 的一项功能，它允许 DB2 客户端通过将连接重路由到备服务器，从与 DB2 服务器的连接丢失中恢复。这种自动连接重路由不需要任何人工干预即可完成。

#### 5.1.1 结合 HADR 的 DB2 客户端自动重路由

图 5-1 展示了结合 HADR 的客户端自动重路由。

![](img/a97b7826c3cf736045d80f48b5520a20_133_0.png)

图 5-1 HADR 中的客户端自动重路由实现

要启用客户端自动重路由功能，需要配置 DB2 服务器可以访问的备位置名称。使用 `UPDATE ALTERNATE SERVER FOR DATABASE` 命令可以定义特定数据库的备服务器位置。

```
db2 update alternate server for database db2 using hostname XYZ port yyyy
```
