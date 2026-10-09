
## /etc/init.d 目录

位于 /etc 目录中的 init.d 目录存储了服务的初始化脚本。这些脚本被称为 System V 脚本，用于控制特定运行级别（runlevel）下服务的启动。这些运行级别被称为 System V 运行级别。在系统初始化开始时，通过 /etc/inittab 文件中的符号链接调用这些脚本。System V 脚本非常灵活，可以根据用户需求进行配置。init.d 目录中列出的一些服务包括 anacron、cups 和 bluetooth。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_448_0.png)

/etc/init.d 目录

![](img/477ccb2f05b6ba1b2d563ea74f18c197_448_1.png)

*图 11-2：系统和服务初始化脚本位于 init.d 目录中。*

## 语法

运行 /etc/init.d 目录中服务脚本的语法为 `/{服务名称} (start/stop/status/restart)`。

## chkconfig 命令

chkconfig 命令可用于控制每个运行级别中的服务。它通过服务初始化脚本中的符号链接来控制服务。它还可以用于在系统启动时启动或停止服务。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_448_2.png)

chkconfig 命令

![](img/477ccb2f05b6ba1b2d563ea74f18c197_449_0.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_449_1.png)

图 11-3：chkconfig 命令及其功能。

chkconfig 命令具有各种选项。表格中列出了一些常用选项。

| 选项 | 功能 |
| --- | --- |
| `--level` | 指定需要启用或禁用服务的运行级别。 |
| `--add` | 将服务添加到由 chkconfig 命令管理的服务列表中。 |
| `--del` | 从由 chkconfig 命令管理的服务列表中删除服务。 |
| `--list` | 列出所有运行级别中由 chkconfig 命令管理的服务。 |
| `on` | 在系统启动时启动服务。 |
| `off` | 在系统启动时停止服务。 |
| `reset` | 重置服务状态。 |

## 语法

chkconfig 命令的语法为 `chkconfig {选项} {服务名称} ({on}/off/reset)`。

## /etc/sysconfig 目录

/etc/sysconfig 目录包含应在系统启动时启动的服务的配置文件。这些文件包含描述系统启动时如何初始化这些服务的设置。/etc/sysconfig 目录中列出的一些服务包括 bluetooth、cups、irda 和 kdump。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_450_0.png)

## system-config-services 命令

system-config-services 命令允许你在当前运行级别中启动和停止系统服务。它是一个基于 X 的图形实用工具，应在 GUI 终端上运行。该命令打开 **Service Configuration**（服务配置）窗口，其中显示两个主要选项卡：**Background Services**（后台服务）选项卡，用于控制后台服务和守护进程；以及 **On Demand Services**（按需服务）选项卡，用于控制由 xinetd 命令管理的服务。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_451_0.png)

图 11-5：system-config-services 命令的输出。

## inetd 命令

![](img/477ccb2f05b6ba1b2d563ea74f18c197_451_1.png)

*inetd* 命令，也称为 Internet“超级服务器”，是一个系统服务守护进程，允许你启动访问不同 Internet 服务所需的程序。当你请求特定的 Internet 服务时，inetd 将启动所有相关服务。它通过运行一个守护进程来支持多个相关服务，而无需同时运行所有守护进程，从而减少系统负载。inetd 命令使用 /etc/inetd.conf 文件来配置服务。在大多数最新版本的 Linux 发行版中，inetd 已不再使用，并被 *xinetd* 命令取代。

## 如何配置服务

![](img/477ccb2f05b6ba1b2d563ea74f18c197_451_2.png)

### **操作参考：使用 chkconfig 命令配置服务**

要使用 chkconfig 命令配置不同运行级别中的服务：

1. 以 root 身份登录。
2. 配置不同运行级别中的服务。
   - 输入 `chkconfig --list {服务名称}` 以显示在每个运行级别中服务名称是应停止还是启动。
   - 输入 `chkconfig --add {服务名称}` 将服务添加到 chkconfig 管理中。
   - 输入 `chkconfig --del {服务名称}` 将服务从 chkconfig 管理中移除。
   - 输入 `chkconfig --level {级别} {服务名称} {on|off}` 以停止或启动指定运行级别中的服务。

## 活动 11-1

## 启用特定服务

### 开始之前：

1. 你已在 GUI 中以 root 身份登录。
2. 终端窗口已显示。
3. 输入 `cd /` 切换到 `/` 目录。
4. 输入 `service bluetooth stop` 停止 bluetooth 服务。
5. 输入 `chkconfig --level 2345 bluetooth off` 在所有运行级别中关闭 bluetooth 服务。
6. 关闭终端窗口。
7. 切换到 CLI。
8. 以 root 身份登录。

### 场景：

作为系统管理员，你在其中一台系统中启用了 Bluetooth 支持，以便用户使用其 Bluetooth 设备。用户现在抱怨 Bluetooth 设备未被系统识别。你意识到问题发生在系统重启后。你需要防止问题再次发生。

| 你要做什么 | 如何操作 |
|---|---|
| 1. 更改不同运行级别中 bluetooth 服务的状态。 | a. 输入 `chkconfig --list bluetooth` 以检查不同运行级别中 bluetooth 服务的状态。<br> b. 观察到 bluetooth 服务在所有运行级别中均被禁用。<br> c. 输入 `chkconfig --level 2345 bluetooth on` 以启用 bluetooth 服务在运行级别 2 到 5 中运行。<br> d. 输入 `chkconfig --list bluetooth` 以检查服务状态是否已更新。<br> e. 观察到 bluetooth 服务现在在运行级别 2 到 5 中已启用。 |
| 2. 启动 bluetooth 服务。 | a. 输入 `service bluetooth status` 以检查服务的当前状态。<br> b. 观察到输出显示 `hcid` 和 `sdpd` 均已停止。<br> ![](img/477ccb2f05b6ba1b2d563ea74f18c197_453_0.png)<br> ![](img/477ccb2f05b6ba1b2d563ea74f18c197_453_1.png)<br> c. 输入 `service bluetooth start` 以启动 bluetooth 服务。<br> d. 观察到“Starting Bluetooth services”旁边显示“OK”状态，这表明 bluetooth 服务已启动。<br> e. 输入 `service bluetooth status` 以检查 bluetooth 服务的状态。<br> f. 观察到显示消息“hcid (pid (process id)) is running”和“sdpd (pid (process id)) is running”，这表明服务已启动。<br> g. 清除终端屏幕。 |

## 主题 B

## 监控系统日志

你配置了系统服务以提高系统效率。为了确保对系统服务所做的更改正确应用，你需要跟踪你所做的每项更改的状态。在本主题中，你将监控系统日志。

作为系统管理员，你需要检查对系统所做的所有更改是否已应用，以确保系统运行正常。在管理系统服务时，手动跟踪对不同服务所做的每项更改在实践中是不可能的。你可以使用系统日志文件来跟踪这些更改。

## 系统日志

**定义：**

*系统日志* 是由 syslogd 实用程序跟踪和维护的系统活动记录。syslogd 实用程序作为守护进程运行。系统日志通常在启动时开始。系统日志消息包括日期、传递消息的进程以及实际消息。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_454_0.png)

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_454_1.png)

图 11-6：系统日志及其消息。

## 日志服务

*日志服务* 是一个用于跟踪系统中生成的日志或错误的守护进程。日志消息存储在一个名为*日志文件*的单独文件中，该文件存储在 /var/log 目录中。主日志文件是 /var/log/messages。除了这个日志文件外，一些服务还会创建自己的日志文件。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_455_0.png)

## 中央网络日志服务器

**定义：**

*中央网络日志服务器* 是一种用于实现集中式日志服务的服务器。该服务器接收来自网络中 Linux 或 Windows 服务器以及网络设备（如路由器、交换机、防火墙和工作站）的所有 syslog 消息。该服务器记录数据挖掘和在线警报，执行日志分析并生成报告。

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_455_1.png)

## 自动化日志分析

在维护会话期间，你可以编写 Perl 或 Bash 脚本自动化日志分析，而无需手动解析大型日志文件。例如，你可以编写一个 Perl 脚本来自动解析邮件日志文件，并通知你被拒绝的电子邮件消息。请确保为脚本创建 crontab 条目。

