
此命令启动了 `firewalld` 守护进程并将其设置为在启动时自动加载。

查看 `firewalld.service` 的状态。这不会显示 `firewalld` 的配置，例如哪些端口已开放或使用了哪些区域。

```
[root@testvm1:~] # systemctl status firewalld.service
```

```
● firewall.service - firewalld - 动态防火墙守护进程
Loaded: loaded (/usr/lib/systemd/system/firewalld.service);
enabled: preset
Drop-In: /usr/lib/systemd/system/service.d
  └─10-timeout-abort.conf, 50-keep-warm.conf

266
第 10 章 使用 Firewalld 管理 Firewalld
Active: active (running) since Sun 2025-01-12 16:03:25
EST: 17h ago
Invocation: bd91633a824f7a8ee6aa1122b7375e5
Docs: man:firewalld(1)
Main PID: 1210 (firewalld)
Tasks: 2 (limit: 9472)
Memory: 48.8M (peak: 49M)
CPU: 898ms
CGroup: /system.slice/firewalld.service
  └─1210 /usr/bin/python3 -S /usr/sbin/firewalld
  --nofork --npid
Jan 12 16:03:24 testvm1.both.org systemd[1]: Starting

firewall.service - firewal - 动态防火墙守护进程...

Jan 12 16:03:25 testvm1.both.org systemd[1]: Started

firewall.service - firewal - 动态防火墙守护进程。

Jan 13 09:29:59 testvm1.both.org systemd[1]: Started

firewall.service - firewal - 动态防火墙守护进程。
```

防火墙的命令行工具可以显示它是否正在运行，但仅于此，因此并没有特别帮助。该命令在用于自动化防火墙和网络操作的脚本中非常有用。

```
[root@testvm1:~#]# firewall-cmd --state
```

```
running
```

下一个命令显示所有支持的区域，按大写字母优先的顺序排序。

```
[root@testvm1:~#]# firewall-cmd --get-zones
```

```
FedoraWorkstation block dmz drop external home
internal nm-shared public trusted
```

267
第 10 章 使用 Firewalld 管理防火墙

需要知道的一个重要数据点是运行中的系统的默认区域是什么。

```
[root@testvm1:~#]# firewall-cmd --get-default-zone
```

```
public
```

这显示默认设置是最受限制的区域之一。

然而，此命令没有显示为安装的网络接口当前分配的区域。为此，我们执行以下操作，列出每个区域并显示分配给该区域的接口：

```
[root@testvm1:~#]# firewall-cmd --get-active-zones
```

```
public (default)
interfaces: enp03 enp08
```

我们现在知道虚拟机上的两个接口都在 `public` 区域。你的虚拟机可能只有一个接口 `enp03`。如果你正在使用物理 Linux 宿主机，接口将取决于物理硬件以及它在 PC 或 USB 总线上的安装位置。

这引导我们去确定 `public` 区域的实际配置。此命令部署了活动区域的配置。只有 `public` 区域是激活的。它还显示了分配给该区域的接口。

```
[root@testvm1:~]## firewall-cmd --zone=public --list-all
```

```
public (default, active)
target: default
ingress-priority: 0
egress-priority: 0
icmp-block-inversion: no
interfaces: enp0s3 enp0s8
sources:
services: dhcpv6-client mdns ssh
ports:
protocols:

268
forward: yes
masquerade: no
forward-ports:
source-ports:
icmp-blocks:
rich rules:
```

你可以看到 `public` 区域 Services 字段中列出的服务。查看 `public` 区域的永久设置。

```
[root@testvm1:~]## firewall-cmd --zone=public --list-all --permanent
```

```
public
target: default
icmp-block-inversion: no
interfaces:
sources:
services: dhcpv6-client mdns ssh
protocols:
forward: yes
masquerade: no
forward-ports:
source-ports:
icmp-blocks:
```

你看到区别了吗？没有分配接口，因为这只是配置，实际分配是在防火墙启动或重启时执行的。

269
第 10 章 使用 Firewalld 管理防火墙

# 添加区域

需要知道的一个重要数据点是运行系统的默认区域是什么。

```
[root@testvm1:~#]# firewall-cmd --get-default-zone
```

```
public
```

这显示默认设置是最受限制的区域之一。

然而，此命令没有显示为安装的网络接口当前分配的区域。为此，我们执行以下操作，列出每个区域并显示分配给该区域的接口：

```
[root@testvm1:~#]# firewall-cmd --get-active-zones
```

```
public (default)
interfaces: enp03 enp08
```

我们现在知道虚拟机上的两个接口都在 `public` 区域。你的虚拟机可能只有一个接口 `enp03`。如果你正在使用物理 Linux 宿主机，接口将取决于物理硬件以及它在 PC 或 USB 总线上的安装位置。

这引导我们去确定 `public` 区域的实际配置。此命令部署了活动区域的配置。只有 `public` 区域是激活的。它还显示了分配给该区域的接口。

```
[root@testvm1:~]## firewall-cmd --zone=public --list-all
```

```
public (default, active)
target: default
ingress-priority: 0
egress-priority: 0
icmp-block-inversion: no
interfaces: enp0s3 enp0s8
sources:
services: dhcpv6-client mdns ssh
ports:
protocols:
forward: yes
masquerade: no
forward-ports:
source-ports:
icmp-blocks:
rich rules:
```

你可以看到 `public` 区域 Services 字段中列出的服务。查看 `public` 区域的永久设置。

```
[root@testvm1:~]## firewall-cmd --zone=public --list-all --permanent
```

```
public
target: default
icmp-block-inversion: no
interfaces:
sources:
services: dhcpv6-client mdns ssh
protocols:
forward: yes
masquerade: no
forward-ports:
source-ports:
icmp-blocks:
```

你看到区别了吗？没有分配接口，因为这只是配置，实际分配是在防火墙启动或重启时执行的。

其实很简单。真正的问题在于我读过的东西似乎都把这个过程复杂化了。

## 实验 10-4：将网卡重新分配到不同的区域

从重启开始，然后验证网络接口的当前状态。

在更改任何事情——无论什么事——之前，验证其初始状态总是友好的。

```
[root@testvm1:~~]# firewall-cmd --get-zone-of-interface=enp0s3
```

```
corp
```

```
[root@testvm1:~~]# firewall-cmd --get-active-zones
```

```
interfaces: enp0s3
public (default)
interfaces: enp0s8
```

你可以通过从当前区域中移除 `enp0s3` 接口，将其重新分配到 `dmz` 区域。此操作会将该接口恢复到默认区域。

```
[root@testvm1:~~]# firewall-cmd --remove-interface=enp0s3
--zone=corp --permanent
```
```
success
```

```
[root@testvm1:~~]# firewall-cmd --remove-interface=enp0s3
--zone=corp
```
```
success
```

```
[root@testvm1:~~]# firewall-cmd --get-active-zones
```

```
public
interfaces: enp0s8 enp0s3
```

这是我们起初困惑的部分。现在将接口分配到 `dmz` 区域并验证更改。

```
[root@testvm1:~]# firewall-cmd --change-interface=enp0s3
--zone=dmz --permanent
```
```
success
```

```
[root@testvm1:~]# firewall-cmd --change-interface=enp0s3
--zone=dmz
```
```
success
```

```
@testvm1:~]# firewall-cmd --get-active-zones
```
```
dmz
interfaces: enp0s3
public
interfaces: enp0s8
```

再次重启并再次验证 `enp0s3` 是否已分配到 `dmz` 区域。`dmz` 区域允许哪些服务？

```
[root@testvm1:~]# firewall-cmd --list-services --zone=dmz
```

```
ssh
```

```
[root@testvm1:~]# firewall-cmd --info-zone=dmz
```
```
dmz (active)
target: default
icmp-block-inversion: no
interfaces: enp0s3
sources:
services: ssh
ports:
protocols:
forward: yes
masquerade: no
```

```
forward-ports:
source-ports:
icmp-blocks:
rich rules:
```

`dmz` 区域是任何允许入站连接的区域中信任度最低的。它只允许 SSH 作为入站连接。完全没有信任的两个区域是 `drop` 和 `block`。你可以在表 10-1 中查看差异。

注意，更改运行时区域（runtime zone）并非必要的，无需重新加载（reload）或使用 runtime-to-permanent 子命令。我们重启并不是完成任务所需的；它们只是为了让我们验证更改是可验证的，并且在重启后是持久的。

我们已经看到，准确了解向区域添加服务（端口）是如何工作的是非常重要的。这组指南基于我的实验，并描述了它们预期的工作方式：

- 1. `public` 区域是默认——嗯——默认的。默认区域是可以更改的。可以指定不同的区域作为默认区域，或者更改默认区域的配置以允许不同的服务和端口集。

- 2. 所有未专门分配到任何区域的接口都使用默认区域。在这种情况下，所有接口（无论是在虚拟机中只有一个，还是在复杂的路由器环境中十个或五个）无论如何都使用默认区域。通常在 Fedora 中，那是 `public` 区域。

如果更改了默认区域（例如从 `public` 区域更改为 `work` 区域），所有这些接口将立即开始使用 `work` 区域。

- 3. **所有接口都显式地分配了一个区域。** 这种情况最不容易引起意外的问题和混乱。更改默认区域不会以任何方式影响任何接口。接口可以重新分配到不同的区域，并且更改区域配置。

- 4. **某些接口显式地分配了一个区域，而其他接口没有。** 在这种情况下，更改默认区域仅影响未显式分配给区域的接口。所有未分配的区域将开始使用新的默认区域。

- 5. **删除接口的区域分配。** 该接口将变为分配并恢复到默认区域。

- 6. **更改默认区域的配置。** 所有使用默认区域的接口（通过显式分配到该区域或未分配）都会立即反映配置更改。

## 添加和删除服务

作为一个老——嗯，成熟的系统管理员，我倾向于从端口配合防火墙和网络服务的角度来思考。有时我需要查找与特定服务相关的端口号，但这并不大，因为它们都定义在 `/etc/services` 中，该文件在 `firewalld` 出现之前就已经存在。

## 实验 10-5：列出服务

查看 `/etc/services` 文件中的服务列表。

```
[root@testvm1 ~]# less /etc/services
```

`/etc/services`:

```
# Network services, Internet service
# IANA services: last updated 2021-01-19
# 注意目前 IANA 的策略是为 TCP 和 UDP 分配单个常用端口号；因此，大多数条目有两个条目
# 根据 RFC 177 更新
# IANA 端口分配可以从 http://www.iana.org/assignments/port-numbers 获取
# 常用端口(Well Known Ports)是 0-1023
# 注册端口(Registered Ports)是 1024-49151
# 动态和私有端口(Dynamic and Private Ports)是 49152-65535
# 每一行描述服务，格式为：
# service-name/port/protocol [aliases]
multiplexer/tcp
multiplexer/udp
echo/tcp
echo/udp
discard/tcp
discard/udp
systemd/tcp
systemd/udp
daytime/tcp
daytime/udp
cmdd/tcp
cmdd/udp
char/tcp
char/udp
ftp-data/tcp
ftp-data/udp
ftp/tcp
ftp/udp
ssh/tcp
ssh/udp
telnet/tcp
telnet/udp
```

此命令消除了注释行并计算剩余行数。

```
[root@testvm1]# grep -v ^# /etc/services | wc -l
```

```
1472
```

`services` 文件包含 1472 个条目。许多端口列出了 TCP 和 UDP 协议。我们也可以列出防火墙识别的服务。

```
[root@testvm1]# firewall-cmd --get-services
```

此命令的输出是 209 个空格分隔的服务列表。这些是可以按名称添加到区域的服务。

防火墙与服务工作得完美，但对于没有定义的，它也支持使用端口号。在实验 10-6 中，我们首先向区域添加端口然后将其删除。像这样操作端口需要同时端口号和协议规范（TCP 或 UDP）。

```
masquerade: no
forward-ports:
source-ports:
icmp-blocks:
rich rules:
[root@testvml1 zones]#
```

让我们进行测试以确保 `telnet` 服务按预期工作。

```
[root@testvml1:~] # telnet testvm1
telnet testvm1
Trying 192.168.0.101...
Connected to testvml1.
Escape character is '^'.
Kernel 6.12.9-200.fc41.x86_64 on an x86_64 (1)
testvml login:A
Password: <Enter user password>
Last login: Sun May 21 15:41:47 on :0
```

第 10 章 使用 Firewalld 管理防火墙

退出 `telnet` 连接。

```
[tuser@testvml1:~] $ exit
logout
Connection closed by foreign host.
[root@testvml1:~]#
```

从 `dmz` 区域中移除 `telnet` 服务并验证结果。

```
[root@testvml1 zones]# firewall-cmd --remove-service=telnet --zone=dmz
```
```
success
```
```
[root@testvml1 zones]# firewall-cmd --info-zone=dmz
```
```
dmz (active)
```
