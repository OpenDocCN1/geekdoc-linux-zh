
```text
Host: 192.168.5.1    Status: Up
Host: 192.168.5.2    Status: Up
Host: 192.168.5.3    Status: Up
Host: 192.168.5.4    Status: Up
Host: 192.168.5.5    Status: Up
Host: 192.168.5.6    Status: Up
Host: 192.168.5.7    Status: Up
Host: 192.168.5.8    Status: Up
Host: 192.168.5.9    Status: Up
Host: 192.168.5.10   Status: Up
Host: 192.168.5.11   Status: Up
Host: 192.168.5.12   Status: Up
Host: 192.168.5.13   Status: Up
Host: 192.168.5.14   Status: Up
Host: 192.168.5.15   Status: Up
Host: 192.168.5.16   Status: Up
Host: 192.168.5.17   Status: Up
Host: 192.168.5.18   Status: Up
Host: 192.168.5.19   Status: Up
Host: 192.168.5.20   Status: Up
Host: 192.168.5.21   Status: Up
Host: 192.168.5.22   Status: Up
Host: 192.168.5.23   Status: Up
Host: 192.168.5.24   Status: Up
Host: 192.168.5.25   Status: Up
Host: 192.168.5.26   Status: Up
Host: 192.168.5.27   Status: Up
Host: 192.168.5.28   Status: Up
Host: 192.168.5.29   Status: Up
Host: 192.168.5.30   Status: Up
```

假设我们想使用 IP 地址以外的内容。这里有一个使用主机名作为 `host_name` 的命令：

```bash
nmap -sP -OG - 192.168.5.0/24 | grep 'Status: Up' | sed -e 's.*/\([^]]*\*/\1/' | WriteHosts.pl
```

此实例将主机名和 IP 地址传递给 `WriteHosts.pl`，后者负责写入配置。所有特定信息都可以从网络查询中提取并使用 `NACE` 格式化为 `Nagios` 配置，用于将主机分配到主机组。

如你所见，可以使用 `-c` 和 `-G` 添加联系人和主机组指令。`-h` 切换告诉 `Namespace` 创建一个主机条目，而不是主机组条目或简单的转储域名。`-x` 切换可用于添加任意数量的自定义指令。在上面的示例中，我使用它来添加一个主机模板。最后一个参数是一个 IP 范围，它会遍历该 IP 范围并将它们全部输出到 `stdout`。这是一个轻量级且直观的工具，对于第一次接触 `Nagios` 的人来说特别有用。

`Namespace` 和 `NACE` 配合得很好。例如，`Namespace` 可以用于创建初始主机配置文件，而 `NACE` 的 `ReturnHostsFromConfig.pl` 脚本可以读取主机并使用 `SNMPServiceQuery.pl` 为它们创建服务文件。

## GUI 配置工具

`Nagios` 有许多目不缭花的图形化配置前端。其中最有前景的两个是由一家名为 `Groundwork` 的公司管理的开源项目。`Groundwork` 在过去几年里将 `Nagios` 扩展为名为 `Groundwork Foundation` 的商业监控应用程序，它直接与四大监控应用竞争：`Openview`、`Patrol`、`Unicenter` 和 `Tivoli`。`Fruity` 和 `Monarch` 都是免费的开源 `Nagios` GUI 前端，由 `Groundwork` 的人员管理。这两款工具的外观精美且运行良好。

需要注意的是，通常情况下 GUI 配置工具并不一定能让没有接触过 `Nagios` 的人变得更容易。例如，向某人提示一个标记为“波动检测”（flap detection）的复选框，并不比文本文件中相同的内容更有意义。不要犯用 GUI 代替训练的错误；它不会达到你预期的效果。

## Fruity

`Fruity` 由 `Taylor Dondon` 编写，他在 `Groundwork` 全职工作，作为本书的技术评审员提供了很大帮助。`Fruity` 是一个 `PHP` 应用，可以通过浏览器访问，并使用 `MySQL` 存储自己的 `Nagios` 配置副本。`Fruity` 为 `Nagios 2.x` 编写，安装非常简单。只需将其重启到你的 `Nagios` 数据库目录，并编辑 `includes/config.inc` 文件即可。当然，由于 `Fruity` 是一个 `PHP/MySQL` 应用，你需要在 `Web` 服务器上安装支持 `MySQL` 的 `PHP` 以及 `MySQL`。在完成所有安装后，你必须手动为 `Fruity` 创建数据库，并从压缩包包含的文件中导入表。

## GUI 配置工具

图 5.1 是 `Fruity` 界面的截图。`Fruity` 是一个非常直观的 GUI；界面设计隐藏了一些强大的功能，例如设置继承其他对象的模板的能力。`Fruity` 是让初级管理员快速上手以及将配置分发给对文本操作不敏感的人的极佳工具。`Fruity` 可以导入现有配置，并且在你告诉它之前，它不会修改配置。在写入文件时，它会先备份现有配置。

![](img/7c754ef117b945190cb5d61f0388dd22_107_0.png)

**图 5.1** 关于 SNMP 的更多内容请见第 6 章“监控”。`Fruity` GUI 中的主机定义。

## Monarch

`Monarch` 是“Groundwork Monitor Architect”的缩写，是一个 `Perl/CGI/AJAX`。它使用了商业版 `Groundwork Foundation` 程序相同的配置引擎。`Monarch` 从浏览器运行，并支持 `Nagios 2.x` 和 `1.x`。`Monarch` 还将 `Nagios` 配置存储在 `MySQL` 数据库中，并包含一个安装脚本，用于配置数据库并将所有内容放在需要的位置。在安装方面，`Monarch` 比 `Fruity` 稍微麻烦一点。在运行设置脚本之前必须安装一些前提条件，包括 `Perl` 模块。

图 5.2 是 `Monarch` 中同一个主机的截图。注意 Profile（配置）选项卡。`Monarch` 在 `Nagios` 配置中引入了 Profile 的概念，在我看来这是一个受欢迎的补充。`Monarch Profile` 就像超级模板；它们根据角色来捕获主机。例如，一个 Web 服务器可以被看作的服务、主机组成员、联系人和升级策略的集合。`Monarch Profile` 为特定的服务、组成员、联系人以及几乎任何其他内容的组合命名。然后将该配置分配给一个或多个主机。这种基于角色的 `Nagios` 配置方法非常酷，可以为大型环境的用户节省大量时间。配置新主机变得非常简单，只需 `Monarch` 指定其名称、别名和地址，并将主机分配给预先存在的配置。

![](img/7c754ef117b945190cb5d61f0388dd22_108_0.png)

**图 5.2** 关于 SNMP 的更多内容请见第 6 章。`Monarch` GUI 中的主机定义。

与 `Fruity` 类似，`Monarch` 可以导入现有配置，并在你告诉它之前不会修改 `Nagios` 配置。还可以通过 `Monarch` 通过命令启动 `Nagios` 配置的备份，这很有帮助。

本章绝不是自动化配置工具的详尽列表。还存在许多其他优秀工具，它们可能非常契合你特定的技能组合。例如，如果你精通 `Perl`，我建议你查看 `CPAN` (`www.cpan.org`) 上可用的 `Nagios` 配置模块。也许 `Nagios` 最棒的一点就是环绕着它的丰富优秀工具。请查看 `Nagios Exchange` (`www.nagiosex.org`) 上的配置部分。

## 第 6 章

## 监控

欢迎来到实战阶段。到目前为止，我一直在说 `Nagios` 是如何工作的。这一章为你提供了一个理解什么是良好基础。正如第 4 章“配置 `Nagios`”所述，每个主机定义都包含一个 `check_command`，用于指定要使用的命令。这通常默认使用 `check_alive` 命令，而该命令又使用 `ping`。因此，正如第 2 章所述，除非需要，否则不会调度主机检查命令。在实践中，在服务检查失败之前，不会运行主机检查命令。因此，尽管这些检查出于不同的目的，但让我们演示如何设置一个简单的 `ping` 检查。主机和联系人已经定义，第一步是在 `check_commands` 文件中定义命令。正如第 4 章所述，定义将服务定义与外部监控程序连接起来。`ping` 检查的命令定义可能如列表 6.1 所示。

## 本地查询

目前为止，任何监控中最常见的服务检查都是经典的 ICMP 请求，通常被称为 `ping`。虽然 `ping` 设置简单，但对于初学者来说可能有些困惑，因为从表面上看，它们似乎被过度使用了。`Nagios` 至少要求每个主机有一个服务。最常见的设置的服务是 `ping` 服务，因为它的定义简单，而且如果你使用的是示例配置，则已经定义了一个 `ping` 检查。

### 6.2 Check_ping 服务定义。

```
define service{
  host_name Server
  service_description check_ping
  check_command check_ping!500.0,20%!1000.0%60
  max_check_attempts 5
  normal_check_interval 5
  retry_check_interval 3
  check_period 24x7
  notification_interval 30
  notification_period 24x7
  notification_options W,c,r
  contact_groups admins
}
```

此服务定义了每 5 分钟对服务器运行一次 `check_ping` 命令，每天 24 小时，每周 7 天。如果发生任何问题，`Nagios` 会在 3 分钟后再次检查该服务 4 次以验证问题是否仍然存在。验证后，`Nagios` 开始每隔 30 分钟向 `admins` 组发送一次通知，每天 24 小时，每周 7 天，直到服务恢复在线。

列表 6.2 中的许多选项在模板内部指定更为更好，为了简洁起见，本章中的其他服务定义假设你使用了模板，例如列表 6.3 中的模板。请参考第 4 章中的“Templates”部分，关于模板以及如何使用它们的讨论。

### 6.3 本章中其他示例使用的模板。

```
define service{
  name chapter6template
  max_check_attempts 5
  normal_check_interval 5
  retry_check_interval 3
  check_period 24x7
  notification_interval 30
  notification_period 24x7
  contact_groups admins
  register 0
}
```

列表 6.2 的 `check_command` 指令中 `check_ping` 之后的是参数列表。服务定义中的参数通常指定阈值并用逗号分隔，因此这里有两个参数。第一个参数 `500, 20 percent` 表示，如果 `ping` 数据包的往返时间大于 500 毫秒，或者丢包率大于 20%，`Nagios` 应该生成一个警告。（该参数没有显式说明它是警告阈值，因为 `$ARG1$` 宏是 `check_ping` 命令定义中的切换参数，服务列表中列出的第一个参数定义了警告阈值。）我知道这一点是因为我在命令行上运行了 `/usr/local/nagios/libexec/check_ping -h` 命令并阅读了帮助语法描述。请查看附录 C，“Command-Line Options”，获取常用插件的命令行选项列表。

## 端口查询 (Port Queries)

在 ICMP 回显之后，端口查询是大多数监控服务器执行的下一个常见服务检查。这些插件尝试在给定主机的给定端口打开 TCP 或 UDP 连接。端口查询由 `check_tcp` 或 `check_udp` 插件执行。命令定义看起来类似于列表 6.4 中的定义。

### 6.4 通用的 check_tcp 定义。

```
define command{
  command_name      check_tcp
  command_line      $USER$/check_tcp -H $HOSTADDRESS$ -p $ARG1$
}
```

与可能会生成警告的 `ping` 命令不同，端口查询的结果通常是端口可用或不可用。由于没有太大歧义空间，因此不需要 `-w` 或 `-c`。只需要指定主机名和端口号。端口检查的“全有或全无”性质影响了警告时的通知（在警告无法发生的情况下）。因此，列表 6.5 中相应的服务描述与列表 6.2 中的 `check_ping` 服务定义不同，它指定了不同的通知选项且不包含阈值选项。

### 6.5 Check_http 服务定义。

```
define service{
  host_name            jkwebServer
  service_description  check_http
  check_command        check_tcp!80
  notification_options  c,r
  use                  chapter6template
}
```

同样注意列表 6.5 中的服务描述是 `check_http` 而不是 `check_tcp`。这是因为服务描述将作为 `Nagios` Web UI 中服务的名称出现，而 `check_tcp` 并不是对实际监控内容的有效描述。

## 本地查询 (Local Queries)

人们在实践中有两种使用 `check-tcp` 方法。第一种是使用单个 `check-tcp` 命令定义并在服务定义中指定端口和服务描述，正如我们在列表 6.4 和 6.5 中所做的那样。另一种方法为你想要监控的服务编写特定的命令定义。这样，你可以为 `check_tcp` 添加一些特定协议的选项，不需要在服务检查中指定端口，并且服务描述可以与检查名称匹配。

重新执行列表 6.4 和 6.5 中的 `check_http` 服务；它将让你了解特定协议命令定义的含义。列表 6.6 是一个 `check_http` 命令定义，它使用 `check_tcp` 但硬编码为检查 HTTP 端口。

### 6.6 一个特定协议的 check_tcp 命令定义。

```
define command{
  command_name    check_http
  command_line    $USER$/check_tcp \ 
  -e 'HTTP/1.0 200 OK' -H$HOSTADDRESS$ -p 80 -s 'GET / HTTP/1.0'
}
```

我们的新命令定义利用 `-s` (send) 实际上向给定主机的指定端口发送某些文本。这里的换行是因为 HTTP 协议期望这样做。此命令使用 `-e` (expect) 来指定我们期望从服务器返回的内容。显然，这些文本是协议特定的，对于 HTTP 或 HTTPS 服务之外的任何内容都无法工作，尽管这些本可以作为通用服务的参数指定，但这样做意味着你用通用定义检查的每个服务都需要指定 `expect` 选项。这里的教训是，当你确实必须执行协议特定操作时，使用新的命令定义通常更整洁。

执行协议特定查询的一个有趣的副作用是警告可能会再次出现。例如，如果服务是用的，但返回了 `HTTP/1.0 302`（HTTP 重定向），那么 `check_tcp` 会认为这是“意外输出”并生成警告。列表 6.7 是一个带有 `shiny check_http` 的服务定义。

### 6.7 Shiny check_http 服务定义。

```
define service{
  host_name            webServer
  service_description  check_http
  check_command        check_http
  notification_options  W,c,r
  use                  chapter6template
}
```

尽管列表 6.5 中的服务描述是 `check_http` 而不是 `check_tcp`。这是因为服务描述将作为 `Nagios` Web UI 中服务的名称出现，而 `check_tcp` 不是对实际监控内容的有效描述。

## 查询多个端口 (Querying Multiple Ports)

正如列表 6.6 所暗示的，`check_tcp` 有很多功能，但有一点不能扫描端口。许多应用程序在多个端口上监听，使用单个服务查询所有端口是一个常见需求。当我遇到插件的限制时，我问自己的第一个问题是封装（wrapper）是否有帮助。

为 `Nagios` 插件编写封装是一项悠久的传统。在这种语境下，封装是指调用另一个程序或一组程序来实现其目的。自从有了 `Nagios` 插件以来，管理员一直在通过脚本封装来扩展其功能。有关插件如何工作以及创建封装过程的逐步说明，请参见第 2 章中的“Plugins”部分。列表 6.8 是 `check_tcp` 和 `check_udp` 的脚本封装，允许你在单个命令定义中查询多个端口的可用性。

### 6.8 一个 check_tcp 封装。
