
然后，我讨论了如何使用 Linux 系统实施防火墙。第一步是设计它将如何工作。一旦确定了将允许什么类型的流量以及将拒绝什么流量，你可以使用`net-filter`基础设施实施防火墙，这通常默认编译到 Linux 内核中。`net-filter`基础设施使用表、链和规则的概念。`filter`表用于创建包过滤规则。`filter`表包括`FORWARD`、`INPUT`和`OUTPUT`链。`filter`表中的每个链都可以配置为`ACCEPT`、`DROP`、`QUEUE`和`REJECT`策略。这是使用`iptables`命令完成的。使用`iptables`创建防火墙时，通常做法是使用`-P`选项设置默认规则，这些规则通常相当严格。然后你使用`iptables`来配置对默认规则的例外。

除了基线之外，你还可以使用系统日志文件来排查系统中的问题。你的系统日志文件存储在`/var/log`中。此目录中一些重要的日志文件包括：

- `boot.log`
- `boot.msg`
- `fail.log`
- `firewall`
- `last.log`
- `mail`
- `messages`
- `warn`
- `wtmp`
- `xinetd.log`
- `cron`
- `dmesg`
- `mail.log`
- `secure`
- `rpmlogs`

并非所有发行版都使用相同的日志文件。在 Linux 系统中，日志记录由`syslogd`守护进程处理。`syslogd`管理日志文件的方式可以使用`/etc/syslog.conf`文件进行自定义。大多数 Linux 发行版配置为定期自动轮转日志文件，以防止它们增长过大。`cron`守护进程定期运行`logrotate`实用工具来执行此操作。`logrotate`如何轮转特定日志文件是使用`/etc/logrotate.conf`文件和位于`/etc/logrotate.d/`中的各个服务的配置文件进行配置的。

你可以配置`syslogd`将所有日志记录事件发送到运行在另一台 Linux 系统上的`syslogd`守护进程。许多管理员会在他们的网络中设置一台系统作为日志主机，所有 Linux 管理员都会将他们的日志文件发送到这里。这样做将集中你的日志文件，并且使得入侵者更难以修改日志文件来掩盖他们的踪迹。你通过在`/etc/syslog.conf`文件的开头添加以下命令来配置远程日志记录：

```
*.*    @IP_address_of_loghost
```

你还需要将日志主机上`/etc/sysconfig/syslog`文件中`SYSLOGD_PARAMS`指令的值设置为`-r`。

然后，我讨论了可用于查看基于文本的日志文件的实用工具。虽然你可以使用`less`、`cat`和`more`，但`tail`和`head`实用工具可以更有效地查看日志文件。`tail`实用工具显示文件的最后几行。`head`实用工具显示文件的第一几行。你还可以使用`grep`在日志文件内搜索内容。你可以使用`tail`的`-f`选项来监控日志文件中的新条目。

然后，我讨论了如何使用 Linux 日志文件检测入侵尝试。你应该定期查看你的日志文件，寻找表明入侵尝试的异常。最适合此任务的日志文件包括：

- `/var/log/wtmp`
- `/var/log/faillog`
- `/var/log/lastlog`
- `/var/log/messages`

你还可以使用`who`和`finger`实用工具查看谁正在使用 Linux 系统。

我通过讨论如何配置`xinetd`和`inetd`结束了这一章。`xinetd`和`inetd`都是超级守护进程。它们管理系统中的其他网络服务守护进程。当请求网络服务时，`xinetd`（或`inetd`）守护进程启动该服务并将请求转发给它。当请求完成且不再需要该服务时，`xinetd`（或`inetd`）将其从内存中卸载。

`xinetd`守护进程使用`/etc/xinetd.conf`文件进行配置。`xinetd`管理的各个服务可以使用位于`/etc/xinetd.d`目录中的适当配置文件进行启用或禁用。

为了增加额外的安全性，你可以使用 TCP Wrappers 来控制对你的网络服务的访问。使用 TCP Wrappers，`xinetd`守护进程运行`tcpd`守护进程，而不是网络服务本身。`tcpd`守护进程检查`/etc/hosts.deny`和`/etc/hosts.allow`文件，以确定请求主机是否被允许使用该服务。如果是，`tcpd`加载请求的守护进程。

`inetd`守护进程使用`/etc/inetd.conf`文件进行配置。所有由`inetd`管理的服务都在这一个配置文件中配置。该文件中的每一行配置一个由`inetd`管理的服务。在`inetd.conf`中使用的语法如下所示：

```
service_name socket_type protocol flags user executable arguments
```

你可以像使用`xinetd`一样使用 TCP 包装器（TCP wrappers）配合`inetd`。这允许你使用`/etc/hosts.allow`和`/etc/hosts.deny`文件来控制对主机上运行的网络服务的访问。

### 快速复习

- 许多组织忽视物理安全，将系统放置在未受保护的区域。
- 服务器需要最高级别的物理安全，应锁定在严格管控物理访问的服务器机房中。
- 工作站需要比服务器更高程度的访问控制。
- 应保护工作区域本身的访问权限，以防止未经授权的人员访问用户的工作站。
- 由于用户倾向于在系统无人看管时保持工作站登录状态，因此应实施屏幕保护程序密码。
- 应培训用户在离开系统前锁定工作站或完全注销。
- 你可以使用`nohup`命令加载进程，使它们即使你从`shell`提示符注销后也能继续运行。
- 用户、组和权限是控制系统访问的主要手段。
- 根用户（`root`）应仅用于完成根任务；所有其他任务都应使用标准用户账户完成。
- 在根用户登录期间，系统绝不应处于无人看管状态。
- 当你需要完成需要根级访问的任务时，可以使用`su`命令切换到根用户账户。
- 你可以使用`exit`命令切换回你的常规用户账户。
- 你可以使用`sudo`命令允许特定用户以`root`身份运行命令，而无需向他们提供你的`root`密码。
- 你使用`/etc/sudoers`文件来指定哪些用户可以以`root`身份运行哪些命令。
- 使用`visudo`实用程序编辑`/etc/sudoers`，该程序会检查你的语法，以确保你未在文件中犯语法错误。
- 需要培训用户避免使用容易猜到的密码。
- 应培训用户使用强密码，强密码使用：
    - 六个或更多字符
    - 数字加上字母
    - 大写字母和小写字母
    - 字典中找不到的单词
- 你可以使用`chage`命令配置密码老化。
