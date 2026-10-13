
相比之下，两个注释指令与 TCP 端口 514 关联：

```
$ModLoad imtcp.so

$InputTCPServerRun 514
```

当然，你必须确保本地日志服务器防火墙中的关联端口是开启的。如果你使用防火墙配置工具，请注意端口 514 未与任何标准“信任服务”关联。因此，你需要为 TCP 端口 514 设置如下自定义规则：

```bash
-A INPUT -m state --state NEW -m tcp -p tcp --dport 514 -j ACCEPT
```

在生产环境中，系统日志服务器可能需要巨大的资源。例如，企业级网站的日志每天很容易消耗数 GB 的数据。想象一下与并行 Web 服务器相关的日志服务器所需的空间。

# 配置系统接受来自远程系统的日志记录 282

与 `/etc/rsyslog.conf` 文件所需的更改相比，系统日志服务器的配置要简单得多。你只需要激活以下指令对中的一个。正如它们的名称所示，以下注释指令如果被激活，将在 UDP 端口 514 上监听：

```
$ModLoad imudp.so

$UDPServerRun 514
```

相比之下，两个注释指令与 TCP 端口 514 关联：

```
$ModLoad imtcp.so

$InputTCPServerRun 514
```

## 274 第 17 章：管理服务：DNS、FTP 和日志

使用不同的用于名称解析的 DNS 服务器，这可能会变得复杂。如果在使用 IPv6 网络，你还可以在 `listen-on-v6` 指令中包含适当网络适配器的 IPv6 地址。

另一个需要更改的条目是 `allow-query`；你可以不再将其限制在本地系统，而是将其范围扩展到 192.168.122.0/24 网络上的所有系统，如下：

```
allow-query { 127.0.0.1; 192.168.122.0/24; };
```

如果成功，你将在 `rndc status` 命令的输出中看到类似的条目：

```
CPUs found: 2

worker threads: 2

number of zones: 19
```
named (pid 7365) is running...

如果你看到的是类似“`rndc: neither /etc/rndc.conf nor /etc/rndc.key found`”的错误信息，说明你的系统受到了 Red Hat 在 bug 768798 中报告的问题的影响，文档见于 https://bugzilla.redhat.com。要解决此问题，请运行以下命令：

```
## rndc-confgen -a

# chgrp named /etc/rndc.key

# chmod g+r /etc/rndc.key
```

重启 `named` 服务，你应该应该能看到 `rndc status` 命令的上述输出了。你应该能够使用 `dig` 和 `host` 等命令从本地和远程系统测试结果。只是不要忘记指定你正在使用本地 IP 地址上的仅缓存 DNS 服务器。如果你用的是 RHEL 6.3，此问题可能在 RHBA-2012:0830-1 中得到解决，该客户更新在 http://thrn.redhat.com/errata/ 中有描述。

## 配置仅缓存名称服务器以转发 DNS 查询

从技术上讲，默认的仅缓存名称服务器已经转发了已缓存在本地数据库中的 DNS 查询。互联网的顶级根域名名称服务器被列在 `/var/named` 目录下的 `named.ca` 文件中。本地缓存中的查询会被转发到那里。但我认为，这并不是该目标的意图。`forwarders` 指令允许你配置本地 DNS 服务器的请求使用另一个（推测是）附近的服务器。

例如，以下指令指定指定的 IP 地址作为备用 DNS 服务器的位置：

```
forwarders {

  192.168.122.1

  192.168.0.1

}
```

尽管外表看起来如此，但 `forwarders` 指令在 DNS 服务器看来被视为一行。

## 使用其他 NTP 对等节点同步时间

如前所述，有两个 NTP 软件包。`ntpdate` 包是客户端。如果那是你唯一需要的，理论上你可以卸载服务器包 `ntp`。然而，安全包（如身份、策略和审计系统，IPA）依赖于 NTP 服务器。在默认的 RHEL 6 配置中，客户端和 `ntp.conf` 文件都用于识别外部 NTP 服务器。相关的条目类似于：

```
server 0.rhel.pool.ntp.org

server 1.rhel.pool.ntp.org

server 2.rhel.pool.ntp.org
```

CentOS 6 系统包含了基于 `centos.pool.ntp.org` 的不同 URL。如果你有一个没有安装 NTP 服务器的系统，你仍然可以让 `ntpdate` 客户端引用 `/etc/ntp/step-stickers` 文件中的外部服务器。只需将这些指令添加到该文件即可。假设 `ntpdate` 客户端被配置为至少在运行级别 3 和 5 启动，客户端将在启动过程中自动与这些外部 NTP 服务器同步。

当然，某些网络（例如考试室）可能无法访问互联网。在这种情况下，你可能需要设置 NTP 服务器，甚至是同一网络上的对等节点。可以认为目标中的“peers”一词暗示 NTP 服务器已经配置并可以从 whitehat.example.net 等系统访问。要设置对等节点，请将 server 指令替换为：

```
peer whitehat.example.net

peer somethingelse.example.net
```

## 276 第 17 章：管理服务：DNS、FTP 和日志

要启用节点通信，请查看文件中的两个指令并注意 `noeper` 和 `noquery` 选项，它们默认适用于 IPv4 和 IPv6 通信：

```
restrict default kod modify notrap noeper noquery

restrict -6 default kod modify notrap noeper noquery
```

要启用节点，你应该删除 `noeper` 和 `noquery` 选项：

```
restrict default kod modify notrap

restrict -6 default kod modify notrap
```

下一个 restrict 指令提供了对本地系统的无限制访问：

```
restrict 127.0.0.1

restrict -6 ::1
```

允许其他的 `restrict` 指令；你可以添加以下指令以支持来自本地网络的访问：

```
restrict 192.168.122.0 mask 255.255.255.0
```

## 认证总结

以下填空题可以帮助你衡量对本章节理解。如果你已经读到了这里，你应该知道如何配置 Red Hat 系统在启动时启动所有网络服务。

## 自测

以下填空题可以帮助你衡量对本章节理解。如果你已经读到了这里，你应该知道如何配置 Red Hat 系统在启动时启动所有网络服务。

## 实验

Red Hat 以电子化方式提供考试。因此，本章及后续章节的实验可以通过 gamma.example.net 系统获取，位于 GUI 桌面上的 `ChapterLabs/` 文件夹中。如果你在命令行控制运行，可以在 `/home/testeser/Desktop/ChapterLabs` 目录下找到实验。

每个实验的答案紧随自测填空题答案。

## 自测答案

生成并交付系统利用报告（处理器、内存、磁盘和网络）

- 1. 交付默认系统利用报告的脚本完整路径为 `/etc/cron.d/sysstat`。

# 配置系统日志到远程系统

- 2. 以下条目允许邮件日志项通过 UDP 端口 514 发送到 IP 地址为 192.168.122.130 的日志服务器：

```
mail.*@192.168.122.130:514
```
