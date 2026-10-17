
在 `SYNC` 和 `NEARSYNC` 中，如果主数据库再次刷新其日志缓冲区，数据可能会缓冲在网络管道中，该管道由主机、网络和备用数据库组成。由于备用数据库没有空闲的日志缓冲区（`DB2_HADR_BUF_SIZE`）来接收，它无法进行确认。因此主库将被阻塞，等待确认。`SYNC` 和 `NEARSYNC` 模式不太可能发生拥塞，除非这些日志数据得到确认，否则主库不会发送更多日志。

在 `ASYNC` 模式下，主库将继续发送日志，直到网络管道填满。网络管道由主机的 TCP 缓冲区、备用机的 TCP 缓冲区、主备之间的网络路径以及 HADR 备用缓冲区组成。当主库无法发送更多日志时，就会发生拥塞。

大型作业重组可能会淹备库并导致拥塞，因为备用数据库正在重放大量的日志记录。主库负载具有尖峰，可能会被更大的缓冲区吸收。

你可以通过调优 TCP/IP 网络来增加 TCP/IP 缓冲，并增大 `DB2_HADR_BUF_SIZE` 注册变量以增加备库的日志缓冲区，从而缓解拥塞问题。但如果主库的持续日志速率超过了处理能力，更大的缓冲区也没有帮助。快照或 `db2pd` 将将连接状态报告为“congested”。拥塞由 `hadr_connect_status` 监控元素报告。

### 6.3.8 在 HADR 高可用集群软件中避免数据丢失

带有 HA 集群软件实现的 HADR 会自动执行 HADR 接管过程。如果检测到网络错误，主数据库将进入 `disconnected` 状态并允许事务继续。这种行为最大化了 HADR 数据库的可用性。尽管在数据库处于 `disconnected` 期间仍然提交事务，但这些事务不会到达备库，仅存在于主数据库。

如果在网络恢复之前主数据库宕机，自动接管过程将启动。由于主数据库宕机，备库将强制主强制接管。日志缺口将无法处理，尚未传输到备用数据库的日志记录将在新的主数据库上丢失。图 6-2 显示了当主库无法向备库传输日志时 HADR 数据库的行为。

注意：为了减少网络错误的可能性，我们建议您为 HADR 通信准备冗余网络。

为了避免数据丢失，只有当主节点崩溃时 HADR 处于 Peer 状态，才应执行自动故障转移。在执行 HADR 接管（`takeover`）之前，请确保 HADR 处于 Peer 状态，这意味着在 `SYNC` 或 `NSYNC` 模式下，数据库之间没有日志空隙。此处不讨论 `ASYNC` 模式，因为该模式的特性无法保证数据库的完整性。

通过妥善监控 HADR 状态并在 HACMP 集群环境中添加处理逻辑，我们可以确保在备用系统接管数据库后，提交的数据不会丢失。图 6-3 阐述了备用接管后保存提交数据的概念。

步骤如下：

- 1. 监控主数据库上的 `diag.log`。
- 2. 通知 HADR 状态。
- 3. 在接管脚本中添加完整性检查逻辑。

![](img/a97b7826c3cf736045d80f48b5520a20_170_0.png)

## 第 6 章 HADR 最佳实践 153

### 1. 监控主数据库上的 diag.log：

当 HADR 状态变为断开（`disconnected`）状态时，您必须立即检测到这种变化。最佳方法是监控主数据库上的 `db2diag.log` 消息。示例 6-1 显示了当从 `peer` 变为 `RemoteCatchupPending` 时，`db2diag.log` 中的某消息，这意味着主数据库已与 HADR 对断开并可以接受新事务，而备用数据库留在了后面。

#### 示例 6-1 HADR 状态从 Peer 变为 RemoteCatchupPending

```
2006-10-25-00.32.28.48734+540 E179519490C354 LEVEL: Event
PID : 8056 TID : 1 PROC : db2hadpr
(SAMPLE) 0
INSTANCE: hadrint NODE : 000 DB : SAMPLE
FUNCTION: DB2 UDB, High Availability Disaster Recovery
hdrSetState,probe:10000
CHANGE : HADR state set to P-RemoteCatchupPending (was P-Peer)
```

示例 6-2 显示了当状态从 `RemoteCatchupPending` 变为 `Peer` 时，`db2diag.log` 中的某消息。

#### 示例 6-2 HADR 状态从 RemoteCatchupPending 变为 Peer

```
2006-10-25-00.35.47.82384+540 E179520902C353 LEVEL: Event
PID : 8056 TID : 1 PROC : db2hadpr
(SAMPLE) 0
INSTANCE: hadrint NODE : 000 DB : SAMPLE
FUNCTION: DB2 UDB, High Availability Disaster Recovery
hdrSetState,probe:10000
CHANGE : HADR state set to P-NearlyPeer (was P-RemoteCatchup)
```

```
2006-10-25-00.35.47.830199+540 E179521256C344 LEVEL: Event
PID : 8056 TID : 1 PROC : db2hadpr
(SAMPLE) 0
INSTANCE: hadrint NODE : 000 DB : SAMPLE
FUNCTION: DB2 UDB, High Availability Disaster Recovery
hdrSetState,probe:10000
CHANGE : HADR state set to P-Peer (was P-NearlyPeer)
```

为了持续跟踪 `db2diag.log`，您可以使用 `tail` 命令。示例 6-3 了一个了一个示例脚本（`tail_hadr_status.ksh`）。当此监控程序通过跟踪 `db2diag.log` 中的消息检测到 HADR 状态变化时，它会将状态写入文件。例如，当 HADR 状态从 `peer` 变为非-`peer` 时，设置为“1”，当 HADR 状态从非-`peer` 恢复到 `peer` 时，设置为“0”。此状态标志允许备用系统在主节点宕机时知道 HADR 状态。

154 Linux, UNIX 和 Windows 上的 DB2 高可用性和可扩展性指南

##### 示例 6-3 tail_hadr_status.ksh

```
tail -0 -f $DIAGLOG | awk '
/CHANGE \: HADR status set to P-RemoteCatchupPending \(was \nP-Peer\)/ {system("{WRITE_STATUS}" 1")}
/CHANGE \: HADR status set to P-Peer \(was P-NearlyPeer\)/ {system("{WRITE_STATUS}" 0")}'
```

为了随时运行此监控脚本，请在主节点上使用 `nohup` 选项运行脚本：

```
#nohup tail_hadr_status.ksh &
```

我们在 A.3（第 409 页）提供了一个完整的 HADR 监控脚本，“`hadr_monitor.ksh`”。

- 2. 通知 HADR 状态：

示例 6-4 显示了更新标记文件脚本（`write_status.ksh`）的代码片段。该脚本作为函数（`write_status.ksh`）的形式包含在 `db2.log` 监控脚本 `tail_hadr_status.ksh` 中。参数值 `$1`（0 或 1）由 `tail_hadr_status.ksh` 给出，并由 `c1_nodecmd` 将其写入备用节点的标记文件中。

##### 示例 6-4 write_status.ksh

```
c1_nodecmd $1
```

- 3. 在接管脚本中添加完整性检查逻辑。

如果客户要求从备用读取数据，则变通方案是使用 Veritas Storage Foundation for DB2 HADR。有关此实施的更多细节，请参阅白皮书《IBM DB2 UDB HADR 环境中使用 Veritas 卷快照实现可访问备用数据库》，网址如下：

`ftp://ftp.software.ibm.com/software/data/pubs/papers/vrts-hadr.pdf`

本文描述了在 DB2 UDB HADR 环境中，为备用数据库提供完全可访问的时间点副本的解决方案的设计和实现。尽管该备用数据库副本是完全可访问的，但它与 HADR 节点分离，因此更新不会自动应用到主（HADR）数据库副本对。

该解决方案利用了一项名为“瞬时空间优化卷快照”（instant space optimized volume snapshot）的新功能，仅需少量额外磁盘空间即可创建存储的单点副本。仅需要更改块的存储。本文讨论了如何在不影响活动 HADR 数据库的情况下，激活备用数据库的时间点副本。空间优化卷快照功能允许在快照过程中无需对主数据库进行写挂起（`WRITE SUSPEND`），即可生成备用数据库的干净副本。
