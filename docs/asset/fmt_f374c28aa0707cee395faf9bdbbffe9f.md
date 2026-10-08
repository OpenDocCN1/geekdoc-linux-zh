
从文件输出中可以看到，有两个客户端拥有活动租约。在查看租约文件时，你应该注意 `dhcpd.leases` 文件中的所有时间都是 UTC (GMT)。之所以这样做是因为该时区没有夏令时，这使其在国际范围内都是可用的。如果你尝试使用此文件进行故障排除，请务必注意这一点。最后一个的小提示是，确保在启动或重启服务之前使用 `configtest` 选项来测试配置文件的语法。这可以防止在尝试启动服务时发生任何错误。

# 现实世界技巧

你可能希望考虑设置备用 DHCP 服务器作为故障转移。当你的主服务器故障时，它可以为你提供备份（但不要仅仅依赖这台备用服务器；要确保你已经测试过它）。如果你创建了备用服务器，应该遵循 80/20 原则：80% 的 IP 地址应该在主 DHCP 服务器上使用，20% 在备用服务器上使用。

# 网络时间协议

你你知道现在几点吗？如果你不知道，也没关系，因为我们将断开网络时间协议 (NTP) 服务。该服务负责维护你的系统，这在任何环境中都非常重要，因为许多功能都依赖于时间（日志、错误消息、应用程序等）。使用 NTP 时，你的系统可以遵循一些规则。它们包括

- 主 NTP 服务器向备用 NTP 服务器或客户端提供时间
- 备用 NTP 服务器向客户端提供时间；帮助主 NTP 服务器负载均衡
- NTP 同级节点提供并接收时间
- NTP 客户端从主或备用 NTP 服务器接收时间

# 红帽®考试上手指南：RHCSA™ 和 RHCE® 认证指南与实验手册

根据《红帽考试备考指南》，你需要能够让客户端与更高层级（stratum）进行同步。`stratum` 术语定义了从 1 到 15 级的可用用于同步的时间服务器。层 1 时间服务器是最准确的。为了负载均衡和冗余，你可能希望配置一个主 NTP 服务器和一个备用 NTP 服务器来与层 1 时间服务器（位于你的网络中）同步。现在，让我们仔细观察 NTP 的服务器端和客户端。

# 安装时间服务器

通常，NTP 包作为红帽系统的一部分已经安装了，但如果你以后需要，知道如何安装它总是好的。

- 第 1 步。如果需要，请安装该包：
```
# yum install -y ntp
```
- 第 2 步。验证包是否已安装：
```
# rpm -qa | grep ntp
ntp-4.2.4p8.el6.x86_64
```
- 第 3 步。确保服务在系统启动时启动：
```
# chkconfig ntpd on
```
- 第 4 步。验证服务是否在启动时启动：
```
# chkconfig ntpd --list
ntpd 0:off 1:off 2:on 3:on
```

*(注：由于提供的文本存在大量重复，以上翻译已根据您的要求对所有行进行了处理。)*

# 步骤 1. 查询你需要更改的布尔值：
```bash
# getsebool -a | grep ntp
tpd_disable_trans fi off
```

# 步骤 2. 禁用 SELinux 保护：
```bash
# setsebool -P ntpd_disable_trans=1
```

# 步骤 3. 验证布尔值已更改：
```bash
# getsebool -a | grep ntp
tpd_disable_trans fi on
```

# NTP 安全

在设置 NTP 服务器时，NTP 安全已经在配置文件中为你预定义。让我们查看 `/etc/ntp.conf` 文件的一部分。注意以下两行：
```
restrict default kod modify notrap nopeer noquery
restrict 127.0.0.1
```
这些安全设置防止来自任何时间服务器的访问更改。它们还限制接口在本地回环接口上执行管理职责。列出的选项如下：

- `kod` 防止“死亡之吻”（kiss of death）数据包
- `modify` 防止其他时间服务器进行更改
- `notrap` 禁用消息的捕获（trap）
- `nopeer` 防止其他系统成为服务器的 NTP 对等节点
- `noquery` 禁止来自其他 NTP 服务器的查询

所有选项都提供了更好的安全性，但有时可能会限制某些功能。你可以删除任何你不希望对 NTP 服务器产生影响的选项。在排排除故障时，此文件也是查看的好地方，可以检查是否这些选项阻止了信息同步到你的 NTP 服务器。如果你想添加另一个管理接口，可以简单地向 `/etc/ntp.conf` 文件添加 `restrict` 选项：
```
restrict 172.168.1.0 mask 255.255.255.250
```
现在，你可以从本地子网上的任何系统对此 NTP 服务器进行更改和服务。如果你进行了任何更改，请忘记重启 NTP 服务。

# NTP 故障排除

当你想要排排除 NTP 服务时，有几个命令可以帮助你。首先，如果你想手动更新时间，可以使用 `ntpdate` 命令。

语法：`ntpdate <server>`

> ### 迁移提示
> RHEL6 默认安装了 `ntpdate` 包，而 RHEL5 没有。
> ### 警告：在运行 `ntpdate` 命令之前，你必须停止 NTP 服务！

- **步骤 1.** 停止 NTP 服务：
> # service ntpd stop
> shutting down ntpd:
- **步骤 2.** 指定你想要同步的上游服务器：
> # ntpdate 0.rhel.pool.ntp.org
> 23 Aug 16:29:15 ntpdate[7047]: adjust time server 209.234.249.11 offset 0.031852 sec
- **步骤 3.** 再次启动服务：
> # service ntpd start
> Starting ntpd:
- **步骤 4.** 使用 `date` 命令验证时间是否准确：
```bash
# date
Mon Aug 23 16:29:34 GMT 2010
```

下一个故障排除命令是 `ntpq`，它允许你查询其他 NTP 服务器。这里，唯一关注的是 `-p` 选项，它用于轮询其他 NTP：
```bash
# ntpq -p
remote                refid              st t when poll reach      delay offset jitter
===============================================================================
pool-test.ntp.0 .INIT.     16 u      64    0  0.000 0.000 0.061
knowledge.globa .INIT.     16 u      64    0  0.000 0.000 0.061
bindcat.fhsdu .INIT.     16 u      64    0  0.000 0.000 0.061
LOCAL(0)             .LOCL.     10 1      64    0  0.000 0.000 0.061
```

最后，你还可以深入追踪 NTP 服务器获取同步时间的来源。为此你可以使用 `ntptrace` 命令。

# 语法：`ntptrace <server>`

你可以指定之前的公共互联网服务器，以确定该服务器在各种同步统计数据中的层级（stratum）有多高：
```bash
# ntptrace 0.rhel.pool.ntp.org
@.rhel.pool.ntp.org: stratum 2, offset -0.000210, sync distance 0.
```

## 总结

为你的网络提供网络服务对于其他系统的交互至关重要。在本章中，我们描述了如何通过 `xinetd` 提供 IP 地址、时间和多服务管理。这些组件中的每一个都在构成你为网络提供的服务方面发挥了作用。尽管这些许多服务没有在备考指南中具体介绍，但它们是任何网络中至关重要的组件，并有助于整合网络上的其他服务。下一章将介绍电子邮件服务。

## 复习题

- 1. `xinetd` 服务是做什么的？
2. 编辑 `/etc/xinetd.d/ftftp` 文件并启用该服务与运行 `chkconfig tftp on` 命令是相同的。对还是错？
3. 使用什么命令进行同步？
4. `xinetd` 服务是做什么的？
5. 使用什么命令进行同步？
6. 使用什么命令进行同步？
7. 使用什么命令进行同步？
8. 使用什么命令进行同步？
9. 使用什么命令进行同步？

*(注：OCR 源中的复习题似乎已损坏/重复；我已保留结构的同时尽可能清理了明显的拼写错误。)*

# Red Hat® 考试实战指南：RHCSA™ 和 RHCE® 认证指南与实验手册

> 迁移提示
> 在 RHEL5 之前，Sendmail 是红帽操作系统的默认邮件程序，但随着 RHEL6 的发布，这已更改为 Postfix。
> 考试提示
> 在考试中，只要系统运行正常并满足所需任务，你可以使用 Postfix 或 Sendmail。如前面的提示所示，Sendmail 不再是默认程序了，因此即使你并不真正熟悉它，学习 Postfix 可能会更容易。

**步骤 1**。要开始操作，你只需要验证 Postfix 是否已正确安装：
```
# rpm -qa | grep postfix
postfix-2.6.6-2.el16.x86_64
```
如果由于原因没有安装该包，你应该现在使用以下命令进行安装：
# yum install -y postfix

**步骤 2**。服务应该已经设置为在系统启动时启动，因此你只需要验证一下：
```
# chconfig postfix --list
postfix 0:off 1:off 2:on 3:on 4:on 5:on
6:off
```
如果服务没有设置为在启动时启动，你可以使用以下命令启用它：
# chconfig postfix on

由于 Postfix 服务默认已安装，所以你真的不需要做太多就可以开始了。

> 迁移提示
> 由于 RHEL5 将 Sendmail 设置为默认邮件程序，在配置 Postfix 之前，你需要采取一些额外的步骤。

**步骤 1**。安装 Postfix 包，因为默认情况下没有该包：
# yum install -y postfix

**步骤 2**。验证包是否已正确安装：
# rpm -qa | grep postfix
postfix-2.3.3-2.1.el5_2

**步骤 3**。由于你将使用 Postfix 代替默认的 Sendmail，你还需要停止 Sendmail 服务：
```
# service sendmail stop
Shutting down sm-client: [ OK ]
Shutting down sendmail: [FAILED]
```

**步骤 4**。你还需要防止它在系统启动时启动：
```
# chkconfig sendmail off
```

**步骤 5**。验证：
```
# chkconfig sendmail --list
sendmail 0:off 1:off 2:off 3:off 4:off 5:off 6:off
```

**步骤 6**。将默认邮件程序更改为 Postfix：
```
# alternatives --config mta
```
有 2 个提供 'mta' 的程序。

| 选择 | 命令 |
|---|---|
| *+1 | /usr/sbin/sendmail.sendmail |
| 2 | /usr/sbin/sendmail.postfix |

按回键保留当前选择 [+]，或输入选择数字：2

**步骤 7**。验证当前的默认邮件是否为 Postfix：
```
# alternatives --display mta | grep current
link currently points to /usr/sbin/sendmail.postfix
```

# 配置 Postfix

Postfix 实际上会启动一个名为 master 的服务，它是它的主服务。这个 master 自身会启动另外三个服务：nmqgr、pickup 和 smtp。nmqgr 服务负责邮件传输、中继和投递。pickup 服务传输消息，smtp 服务提供入站邮件。在处理 Postfix 时有许多需要了解的内容，让我们来看吧。

以下是 Postfix 的管理命令：

- `mailq`: 允许查看邮件队列（* 表示活动，! 表示挂起）
- `postmaster`: Postfix 查找表管理
- `supersuper`: 允许对 Postfix 队列执行维护工作
- `postfixconf`: Postfix 配置工具

Postfix 的主配置文件位于 `/etc/postfix` 目录：

| 文件 | 描述 |
|---|---|
| `master.cf` | 包含 master 服务的设置 |
| `main.cf` | 打开 Postfix 的主配置文件 |
| `access` | 提供访问控制 |
| `transport` | 将电子邮件地址映射到中继主机 |

`master.cf` 文件被分为八列：

- `service`: 标识服务的名称
- `type`: 命名使用的传输机制
- `private`: 命名仅供 Postfix 使用的服务
- `unpriv`: 命名非 root 用户运行的服务
- `chroot`: 指明邮件队列是否应在 chroot 环境运行
- `wakeup`: 指定服务的唤醒间隔
- `maxproc`: 指明服务可以执行的最大进程数
- `command`: 命名要执行的命令以及参数

在 `master.cf` 文件中，列按以下顺序排列：
`<service> <type> <private> <unpriv> <chroot> <wakeup> <maxproc> <cmd>`

> 考试提示
> 默认的 `/etc/postfix/main.cf` 不允许 Postfix 来自本地系统以外的任何网络连接。

在更改配置文件中的任何选项之前，确保 Postfix 服务未运行。现在让我们来看 Postfix 的默认选项：
```
# -n 35 /etc/postfix/master.cf
# Postfix master 进程配置文件。有关文件格式的详细信息，请参见 master(5) 手页（命令: "man 5 master"）。
# ==================================================================
# service type private unpriv chroot wakeup maxproc cmd
# (yes) (yes) (yes)
# ==================================================================
# service type private unpriv chroot wakeup maxproc cmd
# service type private unpriv chroot wakeup maxproc cmd
# service type private unpriv chroot wakeup maxproc cmd
# service type private unpriv chroot wakeup maxproc cmd
# service type private unpriv chroot wakeup maxproc cmd
# service type private unpriv chroot wakeup maxproc cmd
# service type private unpriv chroot wakeup maxproc cmd
# service type private unpriv chroot maxproc cmd
# service inet
```

`master.cf` 文件分为八列：

- `service`: 标识服务的名称
- `type`: 命名使用的传输机制
- `private`: 命名仅供 Postfix 使用的服务
- `unpriv`: 命名非 root 用户运行的服务
- `chroot`: 指明邮件队列是否应在 chroot 环境运行
- `wakeup`: 指定服务的唤醒间隔
- `maxproc`: 指明服务可以执行的最大进程数
- `command`: 命名要执行的命令以及参数

在 `master.cf` 文件中，列按以下顺序排列：
`<service> <type> <private> <unpriv> <chroot> <wakeup> <maxproc> <cmd>`

> 考试提示
> 默认的 `/etc/postfix/main.cf` 不允许 Postfix 接收本地系统以外的任何网络连接。

在更改配置文件中的任何选项之前，确保 Postfix 服务未运行。现在让我们来看 Postfix 的默认选项：
```
# -n 35 /etc/postfix/master.cf
# Postfix master 进程配置文件。有关文件格式的详细信息，请参见 master(5) 手页（命令: "man 5 master"）。
# ==================================================================
# service type private unpriv chroot wakeup maxproc cmd
# (yes) (yes) (yes)
# ==================================================================
# service inet
```

## 第 20 章：邮件服务

| service | | type |
| private |
| unpriv |
| chroot |
| wakeup |
| maxproc |
| command |

`master.cf` 文件分为八列：

- `service`: 标识服务的名称
- `type`: 命名使用的传输机制
