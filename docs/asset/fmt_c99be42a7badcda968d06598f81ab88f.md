
Heartbeat 然后将运行 `/etc/ha/resource.d/iptakeover status`，然后运行 `/etc/ha/resource.d/myresource start`。这使得你能够决定 IP 别名出现在哪个接口，根据需要修改路由表，并从单个脚本执行免费 ARP 广播。然而，通常不需要这样做——请在 `haresources` 文件中指定 IP 地址并让 Heartbeat 完成这些工作。

## haource 语法

`haresources` 文件中的每行可以包含一个多个资源名称。资源之间用空格分隔。参数之间用冒号分隔。例如，如果你需要 Heartbeat 向你的资源脚本发送特殊参数（假设为 `FILE1`）（在 `start`、`status` 或 `stop` 单词之前），你应该使用语法：

```
primary.mydomain.com myresource::FILE1
```

假设你在主服务器和备份服务器上都添加了此条目，Heartbeat 在主服务器启动时会运行 `/etc/ha/resource.d/myresource FILE1`，主服务器故障时在备份服务器上再次运行。当资源需要“释放”或停止时，Heartbeat 将运行命令 `/etc/ha/resource.d myresource stop`。

如果我们想将 `iptakeover` 脚本与 `myresource` 脚本及其 `FILE1` 参数结合起来，我们将使用：

```
primary.mydomain.com iptakeover myresource::FILE1
```

要向资源脚本发送多个参数，请将它们全部输入脚本名称后的同一行，每个参数之间用双冒号分隔。例如，向 `myresource` 发送 `FILE1`、`USERNAME=JOHN` 和 `L3` 参数，你的资源条目如下：

```
primary.mydomain.com iptakeover myresource::FILE1:USERNAME=JOHN::L3
```

`haresource` 语法在网上也有文档：http://wiki.trick.com/linux-ha/HeartbeatResourceAgent。

> 7 同时，正如我们在第三部分所示，你会希望将 IP 别名分配由 Heartbeat 控制，以便转移到负载均衡守护进程。

> 8 这假设脚本资源位于 `/etc/ha.d/resource.d` 目录而不是 `/etc/init.d` 目录——在这种情况下，命令将是 `/etc/rc.d/resource.d FILE1 start`。

到为止，我们只将资源描述为 `haresources` 文件中的独立条目。实际上，Heartbeat 将指定在单行上的所有资源资源视为一个资源组。当 Heartbeat 想要知道某个资源组是否正在运行时，它会询问该行中指定的第一个资源。通过向 `haresources` 文件中添加额外的行，可以添加多个资源组。

例如，如果 `haresources` 文件包含如下条目：

```
primary.mydomain.com iptakeover myresource::FILE1::UNAME=JOHN::L3
```

那么当 Heartbeat 正在确定此资源组的状态时，只会调用 `iptakeover` 脚本来查询状态。如果该行看起来如下：

```
primary.mydomain.com myresource::FILE1::UNAME=JOHN::L3 iptakeover
```

Heartbeat 将运行以下命令来确定资源组的状态（假设资源脚本位于 `/etc/ha.d/`）：

```
/etc/ha.d/resource.d/resource FILE1 UNAME=JOHN L status
```

> 如果你需要在守护进程在 IP 别名添加到系统之前启动，请使用如下条目并在资源脚本名称后输入 IP 地址：

```
primary.mydomain.com myresource IPaddr::200.100.103.3
```

# 资源脚本参数与资源组

为了将 Heartbeat 向脚本发送参数的能力与其创建多个资源组的能力结合，例如，你可以编写一个根据其传递的参数启动 `SERVICE-A` 和 `SERVICE-B` 的脚本。例如，让这个组合资源脚本名为 `resAB`，并假设它可以处理 `SERVICE-A` 或 `SERVICE-B` 后跟 `start`、`stop` 或 `status` 来控制两个守护进程。你可以创建如下条目：

```
primary.mydomain.com resAB::SERVICE-A

primary.mydomain.com resAB::SERVICE-B
```

使用此 `haresources` 文件条目，当 Heartbeat 想要知道这些资源组是否激活状态时，它将运行命令：

```
/etc/ha.d/resource.d/resAB SERVICE-A status

/etc/ha.d/resource.d/resAB SERVICE-B status
```

并且它通过执行以下命令来启动资源组：

```
/etc/ha.d/resource.d/resA8 SERVICE-A start

/etc/ha.d/resource.d/resA8 SERVICE-B start
```

## 使用 Heartbeat 进行负载均衡

使用 Heartbeat 和两台计算机，我们可以从主服务器提供一个守护进程（或服务），然后从备份服务器提供另一个服务。如果任何一台服务器故障，另一台将开始提供两个服务。

这是被称为“主主”（active-active）服务器配置的负载均衡形式，但要使用它，你必须确保每个系统都有处理网络负载所需的计算能力，以便在发生故障时能够提供两个服务。然而，这种配置在生产环境中管理和支持要困难得多。任何服务器都无法进行维护或升级，否则会导致至少一台服务器发生故障转移。图 8-1 显示了此类 Heartbeat 配置的示例图。

用于创建图 8-1 中配置的双行 `haresources` 条目（再次强调，主服务器和备份服务器始终应具有相同的 `haresources` 文件）如下：

```
primary.mydomain.com 209.100.100.3 sendmail

backup.mydomain.com 209.100.100.4 httpd
```

![](img/c9c8f3b9fc0249a24f3ff908555b145c_177_0.png)

图 8-1: Heartbeat 主主配置

一旦 Heartbeat 在两台服务器上运行，`primary.mydomain.com` 计算机将在 IP 地址 209.100.100.3 提供 `sendmail`，而 `backup.mydomain.com` 计算机将在 IP 地址 209.100.100.4 提供 `http`。如果备份服务器故障，主服务器将对 IP 地址 209.100.100.4 执行免费 ARP（Gratuitous ARP）广播并带 `start` 参数运行 `httpd`。（在此配置中，“primary”和“backup”名称实际上没有意义，因为两台计算机都充当着主服务器和备份服务器的角色）。客户端计算机将始终在 209.100.100.3 查找 `sendmail` 资源，并在 209.100.100.4 查找 `http` 资源，即使其中一台服务器宕机，一旦 Heartbeat 启动并将 IP 别名移动到另一台计算机，该资源仍然可用。

注意：这种配置比主备（active-standby）配置更难维护，因为除非在维护之前将所有资源转移到运行在单台服务器上，否则你将一直在“活动”系统上进行更改。

在使用本地数据（存储在任何服务器的本地磁盘驱动上的数据）时不推荐这种配置，因为必须使用复杂的数据复制和同步方法。

## 使用 Heartbeat 进行负载均衡：轮询 DNS

但如果你想从两台计算机都提供一个资源并让它们分担工作呢？这是书中所述集群的目标，可以通过第三部分描述的负载均衡软件来实现。然而，目前我们可以使用轮询 DNS 实现简单形式的负载均衡。

域名系统中一个称为轮询 DNS（round-robin DNS）的特性是允许你在两个（或多个）IP 地址上提供一种服务。例如，主机名首先在 209.100.100.3 和 209.100.100.4 上解析，并以轮询方式进行。

```
primary.mydomain.com   IN   209.100.100.3

backup.mydomain.com   IN   209.100.100.4
```

> 请参考 Evan Marcus 和 Hal Stern 编写的《Blueprints for High Availability》第 7 章，“Failover Configurations and Issues”。

`haresources` 文件中此类配置的条目看起来如下：

```
primary.mydomain.com 209.100.100.3 sendmail
```
