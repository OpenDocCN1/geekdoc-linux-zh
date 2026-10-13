
# 配置系统接受来自远程系统的日志

- 3. 用于与日志服务器通信的默认端口号是 `514`。

# 安装提供服务所需的包

- 4. 与 DNS 服务器关联的包名为 `bind`。

# 配置 SELinux 以支持该服务

- 5. 这是一个陷阱题，因为唯一与 DNS 服务相关的 SELinux 布尔值（`boolean`）影响主服务器，因此正确答案应该是“无 (`none`)”甚至直接留空。

# 配置服务在系统启动时启动

你可以在这里休息一下。你已经走到这里了——你已经如何配置每个网络服务在 Red Hat 系统启动时启动。

# 配置服务的基本运行

- 6. 端口 `123` 是 NTP 服务的标准。

# 为服务配置基于主机和基于用户的安全性

- 7. `/etc/ntp.conf` 文件中的 `restrict` 指令用于按主机限制对 NTP 服务器的访问。

# 配置仅缓存的名称服务器

- 8. 这是另一个陷阱题，因为默认的 `named.conf` 文件已经配置为本地系统的仅缓存名称服务器。

# 配置仅缓存的名称服务器转发 DNS 查询

- 9. `forwarders` 指令用于指定远程 DNS 服务器的 IP 地址，以转发查询。

# 使用其他 NTP 对等节点同步时间

- 10. `/etc/ntp.conf` 文件中的 `peer` 指令指定了要同步的其它服务器。

## 实验答案

## 实验 I

如果你理解了这个实验，答案应该很容易。如果你理解了 `sar` `man` 页面上的示例，你就知道要查看 `sar` `man` 页面中与 CPU 使用率相关的开关（`switch`）。`-u` 开关通向以下命令（你可能需要用不同日期的报告替换 `sa2`）：

```
# sar -d /var/log/sa/sa21 -u ALL
```

当然，为了将该信息获取到指定的文件中，必须进行重定向输出：

```
# sar -d /var/log/sa/sa21 -u ALL > /root/cpu_report.txt
```

## 实验 2

这非常简单；它要求编辑 `/etc/cron.d/sysstat` 文件并将最后一行修改为如下：

```
12 2 * * root /usr/lib64/sa/sa2 -A
```

不要忘记使用类似 `chkconfig sysstat on` 的命令确保 `sysstat` 服务正在运行，并设置为在重新启动时在适当运行级别下启动。

## 实验 3

配置系统日志服务器只需要几处更改。要设置 UDP 通信，打开 `/etc/rsyslog.conf` 文件并激活以下指令：

```
$ModLoad imudp.so

$UDPServerRun 514
```

当然，访问需要在本地防火墙中开放 `514` 端口。你可以使用防火墙配置工具设置自定义规则，例如使用 `whitehat.example.net` 系统的 IP 地址：

```
-A INPUT -m state --state NEW -m udp -p udp -s 192.168.122.130 --dport 514 -j ACCEPT
```

不要忘记使用 `chkconfig rsyslog` 命令确保 `rsyslog` 服务正在运行并在重启时在适当级别启动。

## 实验 4

在 `whitehat.example.net` 上，你可以利用 `rsyslog.conf` 的默认版本。为了此目的，我激活了所有行，修改了最后一行以匹配 `gamma.example.net`，并设置单行使用 UDP 协议。

```
WorkDirectory /var/sp # spool 文件的位置

$ActionQueueFileName # spool 文件名前缀

$ActionQueueMaxDiskSpace 1g # 限制使用空间

$ActionQueueSaveOnShutdown # 关机时保存到磁盘

$ActionQueueType run # 异步运行

$ActionQueueRetryCount -1 # 主机宕机时无限重试

* @192.168.122.20:514
```

不要忘记确保 `rsyslog` 服务正在运行并在客户端的适当级别启动。

## 实验 5

在此实验中，你拥有 `/named.conf` 配置优势。你需要做的是修改指令包含 `gamma.example.net` 的网络 IP 地址：

```
listen 53 { 127.0.0.1; 192.168.122.20 };
```

修改 `allow-query` 指令包含本地 IP 地址：

```
allow-query { localhost; 192.168.122.0/24 };
```

为此系统的仅缓存名称服务器配置特殊的防火墙规则；为此，在配置工具中使用 `iptables` 命令添加以下作为自定义规则：

```
-A INPUT -m state --state NEW -m tcp -p tcp -s 192.168.122.20 --dport 53 -j ACCEPT

-A INPUT -m state --state NEW -m udp -p udp -s 192.168.122.20 --dport 53 -j ACCEPT
```

接受来自特定 IP 地址的变体是可以接受的。你应该能够从所有系统测试结果。类似下面的命令仅对 `gamma.example.net` 和 `whitehat.example.net` 系统有效：

```
dig @192.168.122.20 gamma.com
```

当然，你需要确保 `named` 服务在重启时运行并激活。如果需要，你也可以为每个系统 `/etc/resolv.conf` 设置名称服务器，但并不是实验的要求。

## 实验 6

这是一个两步实验。尽管实验描述是如此，你必须在 `/etc/ntp.conf` 文件设置 `gamma.example.net` 服务器，从第一个指令中移除 `nopeer` 和 `noquery` 选项。

然后你需要如下为本地网络指定 `restrict` 选项：

```
restrict 192.168.122.0 mask 255.255.255.0 not
```

你需要设置同步服务器。注释的 `server` 指令对于此目的足够了；如果没有激活（如下所示），通过删除井号 (`#`) 使它们激活：

```
server 0.rhel.pool.ntp.org

server 1.rhel.pool.ntp.org

server 2.rhel.pool.ntp.org
```

保存结果并重启 NTP 服务。使用 `ntpq -p` 命令检查结果。如果成功，你将看到来自三个不同服务器的输出。

现在你可以去 `whitehat.example.net` 上的 NTP 客户端。使用 `/etc/init.d/ntpd stop` 和 `chkconfig ntpd off` 的命令禁用 NTP 服务。然后在 `/etc/ntp` 目录下的 `peers` 文件添加以下行：

```
gamma.example.net
```

现在运行 `/etc/init.d/ntpdate start` 命令。如果成功，你会看到以下消息：

```
ntpdate: Synchronizing with time server:      [ OK ]
```

你可以在 `/var/log/messages` 文件中确认。如果有问题，你会看到类似“can't find host server”的消息。如果成功，你可能会看到：

```
step time 192.168.122.20 offset -0.000043 sec
```
