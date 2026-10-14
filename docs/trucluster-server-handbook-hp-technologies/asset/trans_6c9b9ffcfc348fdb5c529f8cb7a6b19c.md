

```
# evmget -f "[id = 4817]" | evmshow -D

格式化消息：
login: ROOT login on /dev/pts/1

事件数据项：
事件名称      : sys.unix.syslog.auth
优先级        : 200
PID           : 302
PPID          : 1
事件 ID       : 4817
时间戳        : 29-Mar-2001 12:44:36
主机 IP 地址  : 192.168.0.69
主机名        : sheridan
用户名        : root
格式          : login: ROOT login on /dev/pts/1
参考          : cat:evmexp.cat:200

变量项：
无
```

```
# evmget -f "[id = 4817]" | evmshow -d

EVM 事件名称: sys.unix.syslog.auth ================================

Syslog 授权事件由安全集成架构（SIA）组件发布，用于报告诸如通过“su”命令授予用户超级用户权限或拒绝访问等操作。

授权事件应由系统管理员进行监控。

==============================================================

格式化消息：
login: ROOT login on /dev/pts/1

事件数据项：
事件名称      : sys.unix.syslog.auth
优先级        : 200
PID           : 302
PPID          : 1
事件 ID       : 4817
时间戳        : 29-Mar-2001 12:44:36
主机 IP 地址  : 192.168.0.69
主机名        : sheridan
用户名        : root
格式          : login: ROOT login on /dev/pts/1
参考          : cat:evmexp.cat:200

变量项：
无
==============================================================
```

## Tru64 UNIX 集群钩子：NIFF、NetRAIN 和 LAG

在本章中，我们将讨论基础 Tru64 UNIX 操作系统中包含的各种网络组件，这些组件可用于提高可用性和吞吐量。

我们将介绍以下组件：

| 组件 | 章节 |
| --- | --- |
| 网络接口故障查找器（NIFF） | 9.1 |
| 独立网络接口冗余阵列（NetRAIN） | 9.2 |
| 链路聚合 | 9.3 |

### 9.1 网络接口故障查找器（NIFF）

网络接口故障查找器是 Tru64 UNIX 的一个新组件，用于监控网络接口的连接问题。为了在 Tru64 UNIX 独立环境中监控网络接口，你需要使用 `niffconfig(8)` 命令告知 NIFF。

> **注意：**
> 在 TruCluster Server 环境中，已配置的网络接口由 NIFF 自动监控。

一旦通过 `niffconfig` 添加接口，NIFF 的内核级部分——称为流量监控线程（`nifftmt(7)`）——就会监控该接口。如果接口未能响应，`nifftmt` 会向 EVM 发布一个事件。

用户级 NIFF 守护进程（`niffd(8)`）订阅由 `nifftmt` 生成的 EVM 事件。当出现连接问题时，`niffd` 的职责是在被 `nifftmt` 标记为不活跃的接口上生成流量，以验证该接口是否真正宕机。

NIFF 与 NetRAIN（见下文）结合使用，为独立系统提供高可用性网络解决方案。在集群中，集群别名（CLUA）子系统和集群应用可用性（CAA）子系统也会使用 NIFF。我们将在第 16 章和第 23 章分别更详细地介绍 CLUA 和 CAA。

要添加一个由 NIFF 监控的接口，请键入以下命令（将 `tu0` 替换为你希望监控的接口）。

```
niffconfig -a tu0
```

要检查 NIFF 眼中的接口状态，你可以使用 `-u` 或 `-v` 开关，如以下示例所示：

```
niffconfig -u
Interface:  tu0, status: UP
```

![](img/a0df85c2e542a8d6c913113908553aa4_230_0.png)

```
# niffconfig -v
Interface: tu0, description: , status: UP, event: ALERT, state: GREEN
t1: 20, dt: 5, t2: 60, time to dead: 30, current_interval: 20, next time: 20
```

图 9-1 显示了 `nifftmt` 到 `niffd` 的通信路径。

`nifftmt` 线程每隔 t1 秒检查一次被监控的接口。如果 `nifftmt` 检测到连接问题，它会向 EVM 发布一个 `sys.unix.hw.net.niff.alert` 事件，然后每隔 dt 秒开始检查被监控的接口。`niffd` 守护进程从 EVM 接收 `sys.unix.hw.net.niff.alert` 事件，并开始在接口上生成流量，直到它收到 `sys.unix.hw.net.niff.down` 或 `sys.unix.hw.net.niff.up` 事件。如果经过 t2 秒后，被监控接口的计数器仍未增加，则该接口被标记为 DEAD，并由 `nifftmt` 发送 `sys.unix.hw.net.niff.down` 事件。

#### 9.1.1 NIFF 事件

NIFF 事件定义在 `/usr/share/evm/templates/sys/hw.net.evt` 中。以下是已注册的 NIFF 事件：

```
# evmwatch -A -i -f "[name *.niff]" -t "[@priority] @name"
[600] sys.unix.hw.net.niff.down
[300] sys.unix.hw.net.niff.up
[200] sys.unix.hw.net.niff.alert
```

有关 NIFF 的更多信息，请参阅 Tru64 UNIX 5.0A 和 5.1 版的《Tru64 UNIX 网络管理指南》，或 V5.1A 版的《Tru64 UNIX 网络管理：连接指南》。你也可以查阅 `niff(7)`、`nifftmt(7)`、`niffd(8)` 和 `niffconfig(8)` 的参考手册页。

### 9.2 独立网络接口冗余阵列（NetRAIN）

Tru64 UNIX 提供了一种将多个网络接口卡（NIC）分组在一起，使其作为一个高可用性网络运行的方法，通常称为独立网络适配器冗余阵列或 NetRAIN。

NetRAIN 是一个虚拟接口，通过将两个或多个 NIC 分组为一个数组来工作，操作系统将其视为一个接口。每个 NetRAIN 接口只使用一个 IP 地址，并且任何时刻只有一个活跃的 NIC（有关多个活跃 NIC 共用同一个 IP 地址的内容，请参阅下一节中的“链路聚合”）。如果活跃的 NIC 出现故障，空闲的 NIC 便会联机。其酷炫之处在于，如果你恰好通过 NetRAIN 接口连接到系统

