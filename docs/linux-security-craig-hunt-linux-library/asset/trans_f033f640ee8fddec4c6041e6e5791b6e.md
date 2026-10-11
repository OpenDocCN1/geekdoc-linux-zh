

- `default` 行（通常位于文件末尾）定义了对于不匹配任何特定规则的 IP 块所采取默认操作。

Nessusd 服务在启动时读取配置文件。该文件通常位于 `/etc/nessus/nessusd.conf`。此文件中的每一行都可以是注释（以 `#` 符号开头）或符合以下格式的定义：

`变量名 = 值`

除非你决定将某些 Nessus 文件从 RPM 默认放置的位置移动到其他位置，否则建议使用配置文件的默认值开始。列表 5.4 展示了 nessusd.conf 文件中包含 Nessus 文件路径的变量。

## 列表 5.4 nessus.conf 目录路径定义

```
# Path to the security checks folder :
plugins_folder = /usr/lib/nessus/plugins

# Log file (or `syslog') :
logfile = /var/log/nessus/nessusd.messages

# Dump file for debugging output, use `-1` for stdout :
dumpfile = /var/log/nessus/nessusd.dmp

# Rules File :
rules = /etc/nessus/nessusd.rules

# Users Database :
users = /etc/nessus/nessusd.users
```

列表 5.4 中的变量用法如下：

- `plugins_folder` 变量指定了包含 Nessus 用于检查目标系统漏洞插件的文件夹。
- `logfile` 变量指定了 Nessus 应用程序将记录所有日志事件的日志文件。如果 `logfile` 的值为 `syslog`，所有事件将使用 Linux `syslog` 设施进行记录。
- `dumpfile` 变量指定了调试输出的目标文件。
- `rules` 变量指向 Nessus 守护进程规则集的位置。
- `users` 变量存储了对包含允许登录到 Nessus 应用程序的用户文件的引用。

一旦编辑了 nessusd.conf 文件，就该启动 nessusd 守护进程了。下一节将描述此操作的详细信息。

## 运行 Nessus 守护进程

默认情况下，Nessus 的 RPM 安装会创建一个名为 /usr/sbin/nessusd 的守护进程。Nessusd 守护进程监听客户端请求，以扫描一个或多个目标主机。

> **注意** 必须使用 root 用户启动 nessusd 守护进程。

Nessusd 守护进程的命令行用法如下：

```
nessusd [--background] [--config-file=config_file] [--listen=IP_address] [--port=port]
```

表 5.1 描述了 nessusd 命令行选项、其含义以及它们的默认值。

## 表 5.1 Nessus 守护进程命令行选项

| 选项 | 含义 | 默认值 |
| :--- | :--- | :--- |
| --background | 作为守护进程运行（启动并置于后台）。 | N/A |
| --config-file=config_file | 使用替代的配置文件。 | /etc/nessus/nessusd.conf |
| --listen=IP_address | 接受请求的地址。这会覆盖任何特定用户可能关联的规则。 | N/A |
| --port=port | 在替代端口上监听。 | 3001 |

通常，你只需发出以下命令即可启动 nessusd 守护进程；此命令中的 -D 选项指示守护进程在后台运行，从而将终端会话的控制权交还给你：

```
[ramon]$ sudo /usr/sbin/nessusd -D
```

此时，你可以启动 Nessus 客户端并开始扫描你的某些 Linux 服务器以查找安全漏洞。下一节将引导你完成该过程。

## 配置和运行 Nessus 客户端

由于你是一位 Linux 管理员，你可能会觉得运行 Linux 客户端比较舒适，它是所有客户端中最稳健的。首次调用它时，只需输入以下命令：

```
[ramon]$ /usr/bin/nessus
```

此时，会出现一个对话框，要求你创建一个新的口令（参见图 5.1）。这是保护你私密密钥的秘密。一旦你的私密密钥被解锁，客户端和服务器就会使用公钥认证来生成对称密钥，以保护所有后续通信。如果这不是你从该账户首次调用 Nessus，客户端只会要求你提供第一次指定的口令（图 5.2）。

![](img/3258bbaf790525f8c4eb25fabff7844a_151_0.png)

![](img/3258bbaf790525f8c4eb25fabff7844a_151_1.png)

![](img/3258bbaf790525f8c4eb25fabff7844a_151_2.png)

![](img/3258bbaf790525f8c4eb25fabff7844a_151_3.png)

如果口令正确，客户端将显示主菜单，默认情况下打开 Nessusd Host 选项卡。在此处，你将客户端指向适当的服务器。在图 5.3 的示例中，服务器是 `nessus.example.com`，用于登录的用户名是 `ramon`。

## 图 5.3 登录到 Nessus 服务器

![](img/3258bbaf790525f8c4eb25fabff7844a_152_0.png)

主 Nessus 客户端窗口中的下一个选项卡是 Plugins 选项卡，如图 5.4 所示。在此屏幕上，你可以选择当前位于插件文件夹（默认为 `/usr/lib/nessus/plugins`）中的所有插件。建议你点击“启用所有但危险插件”按钮。这将禁用列表底部的拒绝服务（Denial of Service）插件。如果你选择也运行此攻击，请确保你在目标服务器的维护窗口期间执行，因为这至少会暂时使服务器无法使用。

## 图 5.4 选择 Nessus 插件

![](img/3258bbaf790525f8c4eb25fabff7844a_153_0.png)

下一个感兴趣的选项卡是 Target Selection 选项卡。在此屏幕上，你可以指定要扫描漏洞的服务器。你可以使用逗号分隔的表示法，包括主机名、IP 地址或使用 /subnet 表示法的网络（例如，192.168.1.0/24）。图 5.5 展示了对两个目标主机 204.254.33.75 和 204.254.33.76 的扫描。

## 图 5.5 指定要扫描的目标主机

![](img/3258bbaf790525f8c4eb25fabff7844a_154_0.png)

要开始测试，只需点击“开始扫描”按钮。状态屏幕将出现，如图 5.6 所示。扫描将持续进行，直到 Nessus 服务器完成在 Plugins 选项卡屏幕上指定的所有测试为止。扫描的总持续时间会有很大差异，具体取决于要扫描的主机数量和测试的复杂度。

## 图 5.6 Nessus 扫描：状态窗口

![](img/3258bbaf790525f8c4eb25fabff7844a_155_0.png)

在测试结束时，Nessus 会提供一个摘要窗口（参见图 5.7），显示目标主机列表以及在每个主机上发现的安全漏洞、警告和注释的快速概览。只需选择感兴趣的主机，然后点击“另存为”下拉菜单。选择你喜欢的格式（HTML 是一个不错的选择），然后点击“另存为”按钮。然后，你可以使用你喜欢的 Web 浏览器查看完整的漏洞报告，如图 5.8 所示。

## 图 5.7 Nessusd 报告摘要

![](img/3258bbaf790525f8c4eb25fabff7844a_155_1.png)

## 图 5.8 查看 HTML Nessus 报告

![](img/3258bbaf790525f8c4eb25fabff7844a_156_0.png)

或者，你可以通过展开屏幕左侧 Summary 部分下的每一行，获取更多关于 Nessus 发现的每个漏洞的信息（参见图 5.9）。

看看图 5.9 中的报告。在此示例中，Nessus 已识别出目标机器上 FTP 服务器存在一个问题，攻击者可能会引起缓冲区溢出，导致在服务器上执行任意代码。此外，Nessus 还识别出另一个相关的漏洞，攻击者可以利用 FTP 服务器上的核心转储文件在文件系统的任何用户可读部分写入 /etc/shadow 文件的片段。

这些状态被标记为高优先级和中优先级，并且甚至提出了一个解决方案（不出所料，是升级到更新且更安全的版本）。

## Nmap

虽然 Nessus 的理念是提供一个 polished 的前端和可扩展的客户端-服务器架构，以允许多个用户同时审计网络，但 Nmap 工具为更具经验的网络管理员提供了一款强大且多功能的网络扫描工具。我发现 Nmap 是一个快速评估以下方面的绝佳工具：

- 某个子网中哪些主机在线
- 一系列目标系统上哪些端口（TCP、UDP）是开放的
- 这些系统运行的是什么操作系统

我使用前两种功能领域来确保我的局域网（LAN）上没有未经授权的系统在运行，并确保我的 Linux 服务器没有运行任何我不了解的服务。第三种功能让我能够准确查明疑似入侵者来自的系统类型。这是我报告访问违规或攻击时发送给入侵者域名权威机构的信息的一部分。

