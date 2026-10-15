

“用于基于 TCP/IP 的互联网网络管理的管理信息库：MIB-II。” MIB 是一种树状结构，用于标识网络节点正在使用的数据（统计信息、计数器、接口状态等）。图 15.2 展示了 MIB-II 的 MIB 树。

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_294_0.png)

请注意，每个叶节点（称为 SNMP 对象）通过其在 MIB 树中的位置来标识。因此，Linux 节点上的 eth0 可以被标识为： .iso.org.dod.internet.mgmt.mib-2.interfaces.ifTable.ifEntry.ifIndex.2

eth0 也可以使用与刚才列出的对象 ID 等价的对象 ID 来标识。这里使用对象 ID 显示了树的一部分： .1.3.6.1.2.1.2.ifTable.ifEntry.ifIndex.2

当使用 MIB-II 时，大多数 SNMP 软件包只允许用户指定 MIB-II 树内的路径，因此： .iso.org.dod.internet.mgmt.mib-2.interfaces.eth0 也可以被标识为： interfaces.ifTable.ifEntry.ifIndex.2

## SNMP 通信

SNMP 定义了五种在管理器和代理之间进行通信的消息类型：get、get next、set、response 和 trap。

GET、GET NEXT 和 SET 命令均由管理器向代理发出。GET 命令用于轮询代理 MIB 结构中特定对象的特定值。GET NEXT 命令用于指示代理轮询 MIB 结构中的下一个值。SET 命令由管理器使用，用于告知代理将特定对象的值设置为管理器发送的值。

RESPONSE 消息是代理发出的通信消息，作为对 GET、GET NEXT 和 SET 命令的响应。

TRAP 消息是唯一由代理发起的 SNMP 消息，用于向管理器发送告警消息。例如，如果接口失去物理连接，代理通常会发送一条 TRAP 消息，其中带有相应的对象标识符（OID）。

下一节将介绍如何使用 Linux 命令行工具来使用这些命令。

## SNMP 认证

由于 SNMP 可用于监控和管理网络节点，因此需要某种安全手段来确保网络节点不容易受到攻击。

SNMP 定义了两种安全访问级别：public 和 private。public 级别授予对节点的只读访问权限，private 级别则授予对节点的完全控制权限（读和写）。不幸的是，这些级别的访问信息以明文形式传输。

## SNMP 安全

互联网工程任务组（IETF）确实试图通过协议第 2 版来提高 SNMP 的安全性，但成员们无法就安全需求达成一致，这导致了第 2 版产生了两个分支，部分安全需求留待后续创建：V2u 和 V2c。第 3 版工作组正试图通过标准跟踪规范来修复这一弱点（参见 http://www.ietf.org/html.charters/snmpv3-charter.html）。

## Linux 上的 SNMP

Linux 的 SNMP 以前由两个软件包支持：ucd-snmp 和 CMU SNMP 项目。尽管这两个软件包在互联网上仍然可用，但 Linux 的 SNMP 开发已转移到 NET-SNMP 软件包。

## NET-SNMP

可在 http://net-snmp.sourceforge.net/ 获取的 NET-SNMP 软件包就是早先称为 ucd-snmp 的 SNMP 软件包。当前发行版 4.2.1 仍然被称为 ucd-snmp 软件包，但未来的所有发行版都将使用新名称。NET-SNMP 软件包为 Linux 提供了 SNMP 代理、SNMP 库，以及用于发出 SNMP 命令和陷阱的 SNMP 命令行工具。

除了支持标准 MIB-II 之外，NET-SNMP 代理还直接支持监控磁盘使用情况，并提供支持以确保进程正在运行。当磁盘使用量变低或某个特定进程停止执行时，代理将向管理站发送陷阱。代理还可以利用脚本为陷阱功能增加更多能力。

下一节简要介绍 NET-SNMP 的安装。

## 安装

要安装 NET-SNMP 发行版，请从 http://net-snmp.sourceforge.net/ 的下载部分所指位置下载当前版本的软件包。在本书出版时，4.2.1 是当前版本。将下载的发行版放在 Linux 系统中用于保存源文件的适当位置。本示例使用 /usr/src/。

安装应以 root 用户身份执行。

