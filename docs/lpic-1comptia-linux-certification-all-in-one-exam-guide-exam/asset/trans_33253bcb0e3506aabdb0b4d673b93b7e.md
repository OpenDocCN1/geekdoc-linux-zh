

您可以指定任何希望使用的 NTP 时间提供方的 IP 地址或 DNS 名称。它可以是以下任一类型：

- 网络上的 NTP 时间提供方
- 互联网上的公共 NTP 时间提供方。您可以访问 http://support.ntp.org/bin/view/Servers/WebHome 查看互联网上可用的公共 NTP 时间提供方列表。如有需要，您可以使用 **NTP 池时间服务器**。pool.ntp.org 域名使用 DNS 轮询机制，从自愿加入池中的时间提供方池中随机选择一个。这样，就不会有任何一个公共 NTP 服务器因处理时间同步请求而负载过重。若要使用此功能，只需在刚才讨论的本地时钟服务器指令之外，添加以下服务器指令：
  `server pool.ntp.org`

完成后，保存您的更改并关闭文件。但在实际启动 ntpd 守护进程之前，您需要与 NTP 时间提供方进行一次快速的、一次性的同步。这里的问题是“疯狂时间”（insane time）。如果您的系统时间与 NTP 时间提供方的时间偏差超过 17 分钟，在 NTP 正常工作之前，您必须将这两个系统的时间差异缩小到该时间窗口之内。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_665_0.png)

> **提示** 根据我的经验，“疯狂时间”是 Linux 管理员在配置 NTP 时遇到的头号问题。他们安装了 NTP 软件并正确配置，但却无法弄清楚为什么启动守护进程后时间始终不同步。

通过在 shell 提示符下输入 `ntpdate address_of_time_provider` 可以消除疯狂时间问题。这将执行初始同步，以便在启动守护进程之前使时间接近同步。如果您的系统和 NTP 时间提供方的时间差异很大，您可能实际上需要多次运行该命令。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_665_1.png)

> **提示** 在运行 ntpdate 命令之前，必须停止 ntpd 守护进程！

在新版本的 Linux 发行版上的 NTP 新版本中，也允许您使用 ntpd 守护进程本身的 ntp-timeset 选项来实现相同的功能。您不需要通过守护进程的 init 脚本指定 start、stop 或 restart，而是输入（在 openSUSE 系统上）`/etc/init.d/ntp ntp-timeset` 或在 shell 提示符下输入 `rntp ntp-timeset`。这样做时，会与时间提供方进行一次快速的时间同步，如下例所示：

```text
ws1:/ # rntp ntp-timeset
Time synchronized with pool.ntp.org
ws1:/ #
```

完成后，您可以使用发行版在相应 init 脚本目录中使用的 init 脚本启动 ntpd 守护进程。如果您的系统使用 rc 脚本，只需在 shell 提示符下输入 `rcntp start`，如下所示：

```text
ws1:/ # rcntp start
Time synchronized with pool.ntp.org
Starting network time protocol daemon (NTPD)                    done
ws1:/ #
```

您应该使用 **inserv** ntp 命令配置 ntpd 守护进程，以便在系统每次启动时自动启动。启动守护进程后，您可以使用 **tail** 命令检查 ntp 日志文件，以验证是否发生了错误。

NTP 守护进程启动后，您可以使用两个命令来跟踪 ntpd 守护进程的工作状态：

- `ntpq -p` 此命令查询 ntpd 守护进程的状态。以下是示例：

```text
ws1:/ # ntpq -p
     remote           refid            st when poll reach  delay  offset  jitter
==============================================================================
*LOCAL(0)          .LOCAL.             10 1   30  64   77  0.000   0.000  0.001
 199.249.223.123  129.7.1.66             2 u   26  64   77 105.307 -29.759  4.627
ws1:/ #
```

输出中的列包括以下内容：

- **remote** 指定时间提供方的主机名或 IP 地址
- **refid** 指定参考源的类型
- **st** 指定时间提供方的 stratum（层级）
- **when** 指定距上次时间轮询的秒数
- **poll** 指定两次时间轮询之间的秒数
- **reach** 显示在上次轮询中是否访问了该时间服务器。每次成功的轮询都会使此字段增加 1。
- **delay** 指定时间提供方响应请求所花费的时间（以毫秒为单位）
- **offset** 指定本地系统时钟与时间提供方之间的时间差（以毫秒为单位）
- **jitter** 指定时间偏差的大小（以毫秒为单位）
- **ntrace** ntrace 实用工具追踪时间消费者如何从提供方接收时间。它列出时间提供方的名称、其 stratum 以及其相对于本地系统时钟的时间偏移量。

让我们在下面的练习中实践 NTP 的操作。

624

## 练习 16-2：配置 NTP

**视频** 有关更多信息，请观看练习 16-2。

在这个练习中，您将练习配置 NTP 以从 us.pool.ntp.org 获取时间。为了完成这个练习，您的 Linux 系统必须能够访问互联网。请完成以下操作：

1. 打开一个终端会话，并使用 `su –` 切换到您的 root 用户账户。
2. 在 shell 提示符下，使用您的发行版适当的包管理实用程序验证系统上是否已安装 ntp 包。如果尚未安装，请使用适当的步骤从您的发行版 DVD 或网站安装 ntp 包。
3. 在 shell 提示符下，输入 `vi /etc/ntp.conf`。
4. 向下滚动到以下行：

```text
server        127.127.1.0 #local clock (LCL)
fudge         127.127.1.0 stratum 10 #LCL is unsynchronized
```

5. 按 INSERT。
6. 在 fudge 行下方添加一个新行。
7. 在新行上添加以下指令：

```text
server us.pool.ntp.org
```

该指令用于配置 ntp 服务，使您本地计算机的时间与互联网上公共 ntp 服务器的时间同步。

8. 按 ESC；然后输入 `:exit`。
9. 通过在 shell 提示符下输入 `ntpdate us.pool.ntp.org` 执行一次性同步。如果 ntpdate 在您的发行版中不受支持，请在您的 init 脚本目录中运行带有 ntp-timeset 参数的 ntp init 脚本。例如，`rcntp ntp-timeset`。
10. 通过在 shell 提示符下输入 `/etc/init.d/ntp restart`、`/etc/rc.d/init.d/ntp restart` 或 `rcntp restart` 启动 ntp 服务。您应该看到守护进程正在启动以及它正在从 us.pool.ntp.org 获取时间的消息。
11. 通过在 shell 提示符下输入 `chkconfig –s ntp 35` 配置 ntp 守护进程，使其在运行级别 3 和 5 时自动启动。
12. 通过在 shell 提示符下输入 `chkconfig –l ntp` 检查 ntp 守护进程的状态。您应该看到运行级别 3 和 5 设置为 ON。

这就是 NTP 的全部内容。接下来，我们将讨论如何在 Linux 上管理电子邮件。

## 管理 MTA

在大多数现代组织中，电子邮件已成为通信的支柱。如果您有任何怀疑，只需访问任何邮件服务器已宕机的组织。所有富有生产力的工作都会陷入停滞。

由于电子邮件已成为大多数网络中不可或缺的一部分，您需要了解如何管理邮件服务器。此外，许多 Linux 服务，如 cron，依赖本地邮件服务器向本地用户发送消息。因此，为了您的 Linux+/LPIC-1 考试，您需要熟悉在 Linux 系统上管理邮件传输代理 (MTA)。在本章的这一部分，我们将讨论以下主题：

- 电子邮件的工作方式
- 在 Linux 上使用 MTA 管理命令

让我们从讨论电子邮件的工作方式开始。

### 电子邮件的工作方式

要理解 MTA 如何工作以及如何部署它，您必须首先理解电子邮件流程本身是如何工作的。

您必须理解的第一件事是，电子邮件系统由几个模块化组件组成。每个组件在向收件人投递消息的过程中扮演不同的角色。当电子邮件消息从发件人发送到收件人时，会发生以下步骤。这些步骤在图 16-12 中展示。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_668_0.png)

