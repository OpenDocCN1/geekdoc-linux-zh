
SELinux 提供的另一种保护是服务可以连接的端口。使用 `semanage` 命令配合 `port` 参数和 `-l` 选项可以列出所有可用端口。在接下来的图 8.24 示例中，显示了哪些端口可以使用端口以及如何添加新端口：

```
root@rhel]# semanage port -l grep ^http_port_t
http_port_t    tcp    80, 81, 443, 488, 8008, 8009, 8443, 9000
root@rhel]# semanage port -a t http_port_t -p tcp 3333
root@rhel]# semanage port -l grep ^http_port_t
http_port_t    tcp    3333, 80, 81, 443, 488, 8008, 8009, 8443, 9000
```

# 图 8.24: 命令 semanage 的输出示例

SELinux 默认不允许 Web 服务器连接到外部目标。`getboolean` 命令显示当前状态，`setboolean` 命令允许更改值。接下来的图 8.25 显示了这两个命令的用法：

```
[root@rel]# getboolean httpd_can_network_connect
httpd_can_network_connect -> off
[root@rel]# setboolean httpd_can_network_connect on
[root@rel]# setboolean httpd_can_network_connect
httpd can network connect -> on
```

# 8.25 输出示例

AppArmor 在 Ubuntu 上默认安装并加载。在其他发行版中，可以从软件存储库安装它。AppArmor 使用应用程序的权限来确定所需的文件和权限。AppArmor 有两种执行模式：投诉/学习（learning）将记录违规行为，强制/限制（confined）将执行策略。命令

`apparmor_status` 显示关于加载了多少配置文件以及哪些配置文件处于强制模式的信息。图 8.26 显示了输出示例：

```
root@ubuntu:~ apparmor status |grep -v "^\"
apparmor module is loaded.
31 profiles are loaded.
31 profiles are in enforce mode.
0 profiles are in complain mode.
0 profiles are in kill mode.
0 profiles are in unconfined mode.
0 processes have profiles defined.
0 processes are in enforce mode.
0 processes are in complain mode.
0 processes are unconfined but have a profile defined.
0 processes are in mixed mode.
0 processes are in kill mode."
```

图 8.26：在 Ubuntu 22.04 上命令 `apparmor_status` 的输出示例

配置文件是位于 `/etc/apparmor.d/` 的简单文本文件。它引用一个完整的路径，但将斜杠（`/`）替换为点（`.`）。例如，文件 `/etc/apparmor.d/usr.bin.tcpdump` 的是命令 `/usr/bin/tcpdump`。

Armor 的日志位于 `/var/log/dmesg` 文件中，可以直接访问或通过 `dmesg` 命令访问。配置文件 `/etc/apparmor.d/usr.bin.tcpdump` 定义了一些类似下面的规则：

```
# for -F -w
audit deny @{HOME}/.* mrwl,
audit deny @{HOME}/.* rw,
audit deny @{HOME}/** mrwl,
audit deny @{HOME}/bin/ rw,
audit deny @{HOME}/** mrwl,
```

如果用户尝试在这些路径中的任何一个使用 `tcpdump` 命令打开文件，操作将会失败，并记录日志，如图 8.27 所示：

```
root@ubuntu:~# tcpdump -r ~/.test.cap
tcpdump:/root/.test.cap: Permission denied
root@ubuntu:~# dmesg | tail -1
[ 2187.389656 audit: time=1460 audit(1661799720.098:46) apparmor="DENIED" oper
ion="open" profile="tcpdump" name="/root/.test.cap" pid=2414 comm="tcpdump" re
quested mask="r" denied mask="r" fsuid=0 uid=10
```

# 图 8.27：测试 AppArmor 配置文件

可以使用 `aa-complain` 和 `aa-enforce` 命令（属于 `apparmor-utils` 软件包），将路径作为参数传递并将模式设置为 complain（投诉模式）或 enforce（强制模式）。图 8.28 显示了在使用 `aa-complain` 后，可以读取到一个：

```
root@ubuntu:~# aa-complain /usr/bin/tcpdump
Setting /usr/bin/tcpdump to complain mode.
Warning: profile tcpdump represents multiple programs
Warning: profile tcpdump represents multiple programs
root@ubuntu:~# tcpdump -r ~/.test.cap | head -1
reading from /test.cap, link-type EN10 (Ethernet), snapshot length
262144
19:01:39.118195 IP ubuntu.example.com.ssh ~ _gateway.37748: Flags [P.], seq 3026
156542:3026165774, ack 4280410064, win 55, options (nop,nop,TS val 264014061 e
cr 1533904080), length 132
```

# 图 8.28：使用命令 aa-complain

## 网络监控

网络监控包括持续观察或在某段时间内观察流量以检测问题。它也可以用于检测攻击或对与系统网络配置相关的故障排除。本节将重点介绍流行的工具 `tcpdump` 和 `wireshark`。

`tcpdump` 命令是一个强大的命令行数据包分析器，可以将捕获的数据保存到文件中，或从文件中读取数据。它允许在系统的特定接口或所有接口上进行读取。该命令可以带有选项和参数执行，并将显示在第一个网络接口上生成的流量。`tcpdump` 命令中的参数用于指定过滤器，以便仅捕获来自特定 IP 的数据包。常用选项如下表所示：

| 选项 | 说明 |
| :--- | :--- |
| `-A` | 以 ASCII 格式打印每个包（减去其链路头部）。 |
| `-c count` | 接收 `count` 个数据包后退出。 |
| `--count` | 读取文件时仅打印时间标记的数据包计数，而不是解析/打印包。 |
| `-D,--list-interfaces` | 打印系统上可用网络接口列表，以及 `tcpdump` 在哪些接口上捕获数据包。 |
| `-e` | 在每个 dump 行上打印链路层头部。对调试协议信息有用。 |
| `-i interface` | 使用指定的接口或使用 `any` 使用所有接口。 |
| `--interface=interface` | |
| `-n` | 不将地址转换为名称。 |
| `-r file` | 从文件读取数据包。 |
| `-w file` | 将原始数据包写入文件而不是打印。 |
| `-v` | 详细输出 |

表 8.4：`tcpdump` 命令的常用选项

以下图片显示了使用 `tcpdump` 命令的不同示例。

- 列出系统中使用的所有接口，如图 8.29 所示：

```
1. all
2. eth0
3. en0
4. lo
5. any
```

- 在 Ubuntu 22.04 上使用命令 `apparmor_status` 的输出示例（见图 8.26）。

- 使用 `aa-complain` 命令的示例（见图 8.28）。

- 测试 AppArmor 配置文件（见图 8.27）。

（注：由于原文文本在部分列表描述处存在断行或格式混乱，翻译已根据逻辑进行了对齐）
