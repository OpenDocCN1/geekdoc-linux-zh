
# 12 配置网络服务

## VNC 服务器与客户端

**图 12-34：** 在 Linux 系统上启用的 VNC。

`vncserver` 命令有多种选项。

| 选项 | 允许你执行的操作 |
| --- | --- |
| `-name {desktop name}` | 指定桌面名称。 |
| `-geometry {resolution}` | 指定远程桌面的分辨率。 |

| 选项 | 允许你执行的操作 |
| --- | --- |
| `-depth {depth}` | 指定桌面的像素深度。接受的值为 8、15 和 24。 |
| `-pixelformat {format}` | 指定像素格式，例如 `RGB` 和 `BGR`。 |

## vncviewer 命令

`vncviewer` 命令用于查看 VNC 客户端。有多种选项可用于指定 `vncviewer` 参数。

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_531_0.png)

**图 12-35：** `vncviewer` 命令用于连接到 VNC 服务器。

`vncviewer` 命令有多种选项。

| 选项 | 允许你执行的操作 |
| --- | --- |
| `-display {Xdisplay}` | 指定 X 显示器。 |
| `-listen {port}` | 查找来自 VNC 服务器的反向连接。 |
| `-Shared` | 保持多个 VNC 连接开启。 |
| `-FullScreen` | 以全屏模式启动 VNC 客户端。 |
| `-via {gateway}` | 创建到网关系统的隧道并将客户端连接到主机。 |

## rdesktop 工具

`rdesktop` 是一个根据 GPL 协议发布的开源工具。它允许运行 Linux 的客户端系统登录到网络上运行 Microsoft Windows 的系统。它支持微软的远程桌面协议（RDP）。可以使用 `rdesktop` 命令登录到远程 Windows 系统。

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_532_0.png)

**图 12-36：** Linux 系统借助 `rdesktop` 帮助登录到 Windows 系统。

### 语法

`rdesktop` 命令的语法为 `rdesktop [options] server[:port]`。

## rdesktop 命令

下表列了一些常用的 `rdesktop` 选项。

| 选项 | 用途 |
| --- | --- |
| `-u {username}` | 指定用户名。 |
| `-p {password}` | 指定密码。 |
| `-f` | 以全屏模式启动。 |
| `-g {width}x{height}` | 指定分辨率。 |

RDP 是一种多通道协议，允许用户连接到操作系统。

远程监控（RMON）允许你监控集线器和交换机。

## 过程参考：使用安全 Shell

将文件安全地传输到另一台计算机：

1. 以用户身份登录 CLI。
2. 使用 `scp` 工具传输文件时，输入 `scp {options} {source file or folder name} (user name@hostname) | {IP of the destination}:/{destination file} or {folder name}`。
3. 如果有提示，请将主机添加为受信任主机。
4. 传输文件时，输入密码。

- 3. 输入 VNC 服务器密码，该密码将供连接到此服务器的客户端使用。
- 4. 确认密码。
- 5. 记录显示的 `{server name}:{screen number}`。

### 参考参考：使用 VNC Viewer 连接到 VNC 服务器

要使用 VNC viewer 连接到 VNC 服务器：

- 1. 在客户端系统的 GUI 中以 `root` 身份登录。
- 2. 要查看 VNC 服务器，在终端中输入 `vncviewer {server name}:{screen number}`。
- 3. 要连接到 VNC 服务器，在 VNC 身份验证窗口的 `Password` 文本框中输入服务器密码。

## 活动 12-5：使用安全外壳 (SSH) 进行通信

开始之前：

1. 在 `srvA` 上，你已通过 CLI 以 `root` 身份登录。
2. 显示了第一个终端。
3. 在命令行处，将 `meeting_report` 文件从 `/08509Data/Configuring_Network` 目录复制到 `srvA` 的根目录。
4. 要生成密钥，输入 `ssh-keygen -d`。
5. 要在 `/root/.ssh` 中生成密钥 `id_rsa` 和 `id_rsa.pub`，按三次 `Enter` 键。
6. 清除终端屏幕。

场景：

你的办公室安排了一场讲座。作为系统管理员，用户要求你在讲堂室的系统与他们的系统之间建立安全连接，以便他们远程访问自己系统上的 `meeting_report` 文件。你决定配置 SSH 以建立连接并使用身份验证密钥对其进行加密。

1. 连接到网络上的另一台计算机。
   a. 要连接到服务器，在命令行处输入 `ssh root@192.168.0.2`
   b. 若要继续，输入 `yes`
   > 如果提示要继续连接，输入 `yes`。
   c. 如果提示，在 `root@192.168.0.2` 的密码提示处，输入 `p@ssword`
   d. 验证是否显示了上次登录时间。
   e. 要查看 `meeting_report` 文件的内容，输入 `cat meeting_report`
   f. 输入 `logout`

2. 使用 SSH 创建隧道。
   a. 要使用 SSH 创建隧道，在 `srvB` 上，输入 `ssh -L 3128:192.168.0.2:3128 root@192.168.0.2`
   b. 如果提示要继续连接，输入 `yes`
   c. 如果提示，在 `root@192.168.0.2` 的密码提示处，输入 `p@ssword`
   d. 验证是否显示了上次登录时间。
   e. 输入 `logout`

3. 使用 SSH 密钥验证隧道。
   a. 要生成密钥，输入 `ssh-keygen -d`
   b. 在 `/root/.ssh/` 中生成密钥 `id_dsa` 和 `id_dsa.pub`
   > 如果提示要覆盖文件，输入 `y`。
   c. 要将公钥复制到服务器，输入 `scp /root/.ssh/id_dsa.pub root@192.168.0.2:/root/.ssh/authorized_keys`
   d. 如果提示，在 `root@192.168.0.2` 的密码提示处，输入 `p@ssword`
   e. 观察文件是否已复制到服务器。

4. 将密钥从服务器复制到客户端。
   a. 要连接到 `srvA`，输入 `ssh root@192.168.0.2`
   > 如果提示要继续连接，输入 `yes`。
   b. 如果提示，在 `root@192.168.0.2` 的密码提示处，输入 `p@ssword`
   c. 要将公钥复制到客户端，输入 `scp /root/.ssh/id_dsa.pub root@192.168.0.X:/root/.ssh/authorized_keys`
   d. 在 `Enter passphrase for key` 提示处，按 `Enter`。
   e. 如果提示，在 `root@192.168.0.X` 的密码提示处，输入 `p@ssword`
   f. 如必要要继续，在提示处输入 `yes`
   g. 观察文件是否已复制到客户端。
   h. 要退出服务器，输入 `logout`

## 活动 12-6：实现 VNC

开始之前：
在 `srvA` 上完成：

1. 你已通过 CLI 以 `root` 身份登录。
2. 切换到 GUI。
3. 以 `root` 身份登录。
4. 显示终端窗口。
5. 在开始此活动之前，确保已安装软件包 `vnc-4.1.2-9.el5.i386.rpm` 和 `vnc-server-4.1.2-9.el5.i386.rpm`。否则，你可以使用命令 `yum localinstall /hel/server/vnc*` 安装软件包。
6. 要启动 VNC 服务器，在终端窗口中输入 `vncserver`。
7. 输入连接到此服务器的客户端所使用的 VNC 服务器密码。
8. 确认密码。
9. 记录显示的屏幕编号。
   ![](img/b54ed9904f9bb8a2eb5097106fbafd6_538_0.png)
10. 创建目录，输入 `mkdir /employee`。
11. 清除终端窗口，输入 `clear`。

开始之前：
在 `srvB` 上完成：

1. 你已通过 CLI 以 `root` 身份登录。
2. 切换到 GUI。
3. 如必要，安装 viewer 包。

场景：
作为系统管理员，你想维护用户及其 IP 地址列表以跟踪资源。你发现用户详情尚未更新。

1. 使用 `vncviewer` 命令连接到 VNC 服务器。
   a. 要查看 VNC 服务器，输入 `vncviewer 192.168.0.2:X`
   b. 在 VNC 身份验证窗口的 `Password` 文本框中，输入 `p@ssword`
   c. 将鼠标定位终端。
2. 在 `/employee` 目录中创建文件。
   a. 导航目录，输入 `cd /employee`
   b. 创建文件，输入 `vi employee192.168.0.X`
   > 学生应在此处输入提供的屏幕编号。
   c. 切换到插入模式，按 `I`。
   d. 输入 `Name=XXXXX`
   > 学生应在 `employee192.168.0.X` 处输入系统编号。
   e. 输入 `IP=192.168.0.X`
   > 学生应在此处输入系统编号。
   f. 退出模式，按 `Esc`。
   g. 保存并关闭文件。
   h. 退出 VNC 服务器，点击 `Close` 按钮。
3. 验证文件已成功创建。
   a. 切换到 `srvA`。
   b. 在终端窗口中切换目录，输入 `cd /employee`
   c. 查看文件内容，输入 `cat employee192.168.0.X`
   > 学生应在此处输入系统编号。
   d. 观察文件内容，表明文件创建成功。
   e. 清除终端窗口，输入 `clear`。

## 课程 12 复习

在本课程中，你配置并管理了各种网络服务。你现在能够发布信息、远程管理系统、通过邮件或聊天通信、促进技术共享以及控制访问。

1. 在网络上集中管理 IP 地址有什么优点？
2. 在网络上启用 DNS 之前必须考虑的点。

# 13 配置基础互联网服务

课程时长：2 小时

# 课程目标

在本课程中，你将配置基础互联网服务：

- 配置电子邮件服务。
- 控制互联网服务。

### 引言

在上一节课程中，你配置了网络服务。现在，你想实现一种面向业务的服务，允许你在网络上的各种平台上共享资源并通信。在本课程中，你将配置基础互联网服务。

互联网提供了各种服务，如电子邮件、文件共享和下载以及网页浏览。组织的员工通常需要访问互联网并在各种平台上进行通信。作为系统管理员，你想实现一种提供应用程序间互操作性并涉及成本效益的简单服务。互联网服务有助于在各种网络之间安全地共享和传输资源。

本课程涵盖了 CompTIA Linux+ Powered LPI 认证的全部或部分：

- 主题 A：
  - 目标 108.3, 目标 109.1
- 主题 B：
  - 目标 109.1, 目标 110.2
- 主题 D：
  - 目标 110.2

# 主题 A：配置电子邮件服务

在上节中，你配置了基础网络服务。现在你需要通过互联网共享信息，因为这是最简单、标准的通信方式，并通过定义电子邮件过程提供客户端和服务器电子邮件服务。在本主题中，你将配置电子邮件服务。

不久前，组织仅使用互联网邮件端口和邮政服务进行业务通信。然而，今天我们通过电子邮件和即时消息进行电子通信。了解邮件如何运行对于实现电子邮件服务至关重要。

### 邮件协议

定义：

邮件协议是允许从邮件服务器发布电子邮件的规则。使用邮件协议，电子邮件可以存储在服务器上，或在读取时传输到客户端计算机。邮件协议允许用户在服务器上创建和管理文件夹、搜索消息或删除消息。`POP`、`IMAP` 和 `SMTP` 是最常用的邮件协议。

示例：

![](img/b54ed9904f9bb8a2eb5097106fbafd6_543_0.png)

图 13-1：使用 `POP`、`IMAP` 和 `SMTP` 协议发布电子邮件。

### SMTP

简单邮件传输协议 (`SMTP`) 是一种定义了一系列规则的协议，允许向服务器发送电子邮件的程序与从客户端接收电子邮件的程序之间进行交互。邮件传输代理 (`MTA`) 或邮件用户代理 (`MUA`) 充当 `SMTP` 客户端。`SMTP` 服务器监听端口 `25` 以接收客户端响应。`SMTP` 使用 `TCP` 传输消息并使用 `IP` 进行路由。它包含许多状态码，用于设置服务器与客户端通信的特定条件。它还包含一组用于服务器与客户端通信的命令。

## CompTIA® Linux+ (基于 LPI)

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_544_0.png)

**图 13-2:** 客户端使用 `SMTP` 的通信。

除了文本消息外，还可以通过扩展 `SMTP` (`ESMTP`) 使用电子邮件传输图形和附件。`SMTP` 客户端使用扩展 `HELLO` (`EHLO`) 命令与服务器通信，服务器用三种状态码之一进行响应：成功、失败或错误。

## 邮件置打印 (Mail Spooling)

置打印是一种处理电子邮件消息传输延迟的方法。如果电子邮件传输出现延迟，源计算机上的 `SMTP` 会将消息放入队列。如果没有延迟，源计算机上的 `SMTP` 将通过 `TCP` 连接将电子邮件消息发送到目标计算机。目标计算机上的 `SMTP` 接收电子邮件并将其放入用户的邮箱中。当目标计算机的用户向源计算机的用户发送回复时，会发生反向的过程。

## POP3

邮局协议第 3 版 (`POP3`) 用于通过端口 `110` 上的 `TCP` 连接检索电子邮件消息。`POP` 客户端连接到服务器并检索所有消息。它将其作为新消息存储在客户端 PC 上，从服务器上删除它们，并断开连接。它支持 `MIME` 格式的电子邮件消息。通常，`POP3` 支持以明文格式传输消息和密码。它还通过端口 `995` 上的 `TCP` 使用 `SSL` 协议加密消息来提供验证。

## IMAP

互联网消息访问协议 (`IMAP`) 用于通过端口 `143` 上的 `TCP` 连接检索电子邮件消息。客户端从服务器检索所有消息，服务器保留这些消息直到用户删除它们。尽管该协议以明文格式传输消息和密码，但它支持通过端口 `993` 上的 `TCP` 对消息进行 `SSL` 加密。此外，它支持 `MIME` 格式的电子邮件消息。

## 邮件队列

定义：
邮件队列是需要计算机处理的电子邮件消息的等待区域。
邮件队列的组织方式是：第一个添加到队列的项目也是第一个从队列发送的项目。

示例：

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_545_0.png)

图 13-3: 电子邮件消息排列在队列中。

## 邮件传输代理 (MTA)

定义：
邮件传输代理 (`MTA`) 是互联网上用于 `SMTP` 发送电子邮件消息的程序。它们使用 `SMTP` 指明消息传输的成功或失败，并为失败的消息形成顺序队列。当不允许在服务器端存储邮件队列时，`MTAs` 经常使用 `SMTP` 的派生协议本地邮件传输协议 (`LMTP`)。`MTAs` 允许客户端处理邮件队列而不是服务器，并且不提供邮箱处理功能。

示例：

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_545_1.png)

图 13-4: 电子邮件消息通过 `MTA` 的路由。

## MTA 的类型

`MTA` 支持虚拟主机、传输失败时自动重发消息以及 `Spamassin`——一种用于识别垃圾邮件的邮件过滤器。每个 `MTA` 都支持各种功能，为服务器提供默认的访问控制。

| 名称 | 描述 |
| :--- | :--- |
| `Sendmail` | 一种支持多种 Unix 类似系统的标准 `MTA`。它的设计使其作为一个单个实体运行。它移植了各种 `MTA` 和 `MDA`。它是一个从早期一直使用的 `MTA`。 |
| `Postfix` | 一种快速、安全且易于管理的 `MTA`。它与 `Sendmail` 类似但在内部功能上有所不同。与 `Sendmail` 不同，`Postfix` 支持模块化功能。它是一个免费的开源 `MTA`，可以作为 `Sendmail` 的替代方案。 |
| `Exim` | 一种灵活且免费获取的 `MTA`。与其他 `MTA` 不同，它具有广泛的功能，允许管理员通过系统控制邮件传输。最新版本已开发为基于 ACL（访问控制列表）的系统，提供了更详细、更灵活的控制。它有助于在 `MTA` 中集成反病毒和反垃圾邮件措施。 |
| `qmail` | 第一个管理大型邮件列表的安全邮件传输代理。它由多个模块组成，这些模块可以被任何包含相同接口的新模块替换。它引入了通配符概念，允许用户发布多个邮件地址用于发送。 |

## Sendmail 配置文件

安装 `Sendmail` 时，会在 `/etc/mail` 目录中创建配置文件。`sendmail.cf` 文件是 `Sendmail` 的配置文件。由于该文件很大，最好避免直接编辑该文件。相反，你可以对 `sendmail.mc` 文件进行更改，稍后使用 `m4` 工具更新 `sendmail.cf` 文件。

## Postfix 配置文件

`Postfix` 配置文件在 `/etc/postfix` 目录中创建。`main.cf` 和 `master.cf` 是两个主要的 `Postfix` 配置文件。`main.cf` 定义配置参数，`master.cf` 定义守护进程。大多数配置参数都设置为默认值。`master.cf` 主要定义客户端程序连接到服务的进程以及在请求服务时运行的守护进程。

## Qmail 配置文件

除 `.qmail` 文件外，所有 `Qmail` 配置文件都存储在 `/var/qmail/control` 目录。`.qmail` 文件位于 `-alias` 目录下。`.qmail` 文件用于控制邮件投递。

## Exim 配置文件

`exim` 配置文件创建在 `/etc/exim` 目录。`exim.conf` 文件是 `exim` 的主配置文件。

## Sendmail 模拟层命令

`smrsh` 程序是一个用于限制用户恶意行为并限制用户执行程序的 shell 工具。它是 `/bin/sh` 的替代品，并安装在 `/usr/bin/smrsh` 目录。当 `smrsh` 与 `Sendmail` 使用时，`smrsh` 目录允许 `Sendmail` 执行的 `smrsh` 程序的命令集被称为 `Sendmail` 模拟层命令。禁止执行的某些程序是 `sh`、`c` 和 `perl`。

## MUA

定义：

示例：

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_547_0.png)

图 13-5: `MUA` 充当用户与 `MTA` 之间的接口。

## MDA

定义：

邮件投递代理 (`MDA`) 是将传入的电子邮件投递到目标接收者邮箱的程序。`MDA` 使用 `SMTP` 发送新邮件，使用 `IMAP` 检索消息。它还在本地机器上对消息进行分发和排序，以便 `MUA` 访问。

示例：

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_548_0.png)

图 13-6: 电子邮件通过 `MDA` 投递到客户端。

## 邮件转发

邮件转发是一种自动转发电子邮件消息的功能。它也可以将邮件重定向到一个或多个地址。

## 电子邮件邮件过程

电子邮件邮件过程描述了创建、传输和存储消息的涉及的步骤。电子邮件邮件过程涉及五个阶段。

1. 发送者编写要发送的消息。发送者的 `MUA` 以电子邮件格式格式化消息，并使用 `SMTP` 将消息发送到发送者的 `MTA`。
2. 发送者的 `MTA` 检查 `SMTP` 提供的目标地址。根据目标地址，它通过 `UDP` 向 `DNS` 服务器发送针对特定域名的请求。`DNS` 服务器返回列有该域名支持的邮件交换器的 `MX` 记录。
3. 根据 `DNS` 服务器的响应，发送者的 `MTA` 使用 `SMTP` 将消息发送到接收者的 `MTA`。
4. 接收者的 `MTA` 再次将消息发送给接收者的 `MDA`，`MDA` 将其投递到存储所有接收者消息的队列中。
5. 最后，接收者的 `MUA` 通过称为邮件检索代理 (`MRA`) 的检索代理，使用如 `POP3` 和 `IMAP` 等协议从队列中检索消息。接收者然后打开收到的消息。

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_549_0.png)

图 13-7：从一个系统向另一个系统发送电子邮件的过程。

## 如何配置电子邮件服务

### 程序参考：安装 Postfix

要安装 `Postfix`：

1. 以 `root` 身份登录。
2. 挂载包含 `postfix` 的红帽企业 Linux 安装介质。
3. 导航到 `/media/(介质名称)/Server` 目录。
4. 要安装 `postfix`，在命令行中输入 `rpm -ivh postfix-(version).{release}.i386.rpm`。
5. 要验证 `postfix` 是否已安装，输入 `rpm -qi postfix`。

### 程序参考：为入站邮件服务配置 Postfix

要配置 `Postfix` 以接收入站邮件：

1. 以 `root` 身份登录。
2. 设置完全限定域名（FQDN）。
   a. 输入主机 `hostname {完全限定域名}`。
   b. 打开 `/etc/sysconfig/network` 文件并确保已更新完全限定域名。
3. 使用 `vi` 编辑器打开 `/etc/postfix/main.cf` 文件。
4. 要接收来自远程服务器的邮件，请设置系统。
   a. 找到 "inet_interfaces = all" 指令并取消该行的注释。
   b. 找到 "inet_interfaces = localhost" 指令并注释该行。
5. 要指定由 `postfix` 邮件服务器控制的域名列表，找到 "mydestination = $myhostname, localhost.$mydomain, localhost,$mydomain, mail.$mydomain, $mydomain"。
6. 保存并关闭文件。
7. 要启动 `postfix` 服务，输入 `service postfix start`。
8. 要验证 `postfix` 服务器是否正在监听所有接口，输入 `netstat -plt | grep master`。
9. 要在系统启动时启用 `postfix` 服务，输入 `chkconfig postfix on`。

### 程序参考：为出站邮件消息配置 Postfix

要配置 `postfix` 以发送出站邮件消息：

1. 以 `root` 身份登录。
2. 导航到 `/etc/postfix` 目录。
4. 为出站邮件消息进行域名伪装。
   a. 找到 "myorigin" 并取消其注释。
   b. 若要伪装 `root` 用户，输入 `masquerade_exceptions = root`。
5. 保存并关闭文件。
6. 要重启 `postfix` 服务，输入 `service postfix restart`。

### 程序参考：使用 Sendmail 或 Exim 配置电子邮件别名

要使用 `Sendmail` 或 `Exim` 设置别名：

1. 使用 `vi` 编辑器打开 `/etc/aliases` 文件。
2. 添加电子邮件别名。别名可以是本地用户或文件名、命令、包含文件或外部地址。
   - `(用户名):别名(1), [别名2,别名3...]`
   - 为本地系统上存在的用户名添加别名。`(用户名):(该用户的别名)`。
   - 为您想要转发消息的外部地址添加别名。`(用户名):(电子邮件地址)`。
   - 为您想要转发消息的用户列表添加别名。用户列表在单独的文件中指定。`(用户名) :include:(包含用户名的文件路径):(文件名)`。
   - 为您希望追加该用户收到的消息的文件添加文件名。`(用户名):(文件路径)/(文件名)`
   - 或者，添加一个别名以启用从标准输入接收消息的 `Sendmail` 处理命令。`(用户名):<command>`。
3. 保存并关闭文件。
4. 要更新别名数据库文件，输入 `newaliases`。

### 程序参考：使用 Postfix 配置电子邮件别名

使用 `Postfix` 配置电子邮件别名：

1. 使用 `vi` 编辑器打开 `/etc/postfix/main.cf` 文件。
2. 验证 `alias_maps` 变量是否定义了别名文件的位置。`alias_maps = hash:/etc/aliases`
3. 保存并关闭文件。
4. 使用 `vi` 编辑器打开 `/etc/aliases` 文件。
5. 为本地系统上存在的用户名添加别名。`(用户名):{该用户的别名}`。
6. 保存并关闭文件。
7. 要更新别名数据库文件，输入 `newaliases`。
8. 要重启 `postfix` 服务，输入 `service postfix restart`。

### 程序参考：配置本地别名

要配置本地别名：

1. 以 `root` 身份登录。
2. 使用 `vi` 编辑器打开 `/etc/postfix/main.cf` 文件。
3. 找到 `alias_maps` 指令并验证该指令是否定义了别名文件的位置，格式为 `alias_maps = hash:/etc/postfix/aliases`。
4. 找到 `alias_database` 指令并验证该指令是否定义了别名文件的位置，格式为 `alias_database = hash:/etc/postfix/aliases`。
5. 保存并关闭文件。
6. 使用 `vi` 编辑器打开 `/etc/postfix/aliases` 文件。
7. 添加电子邮件别名，`(用户名):{alias1}, alias2, alias3`
   - 为本地系统上存在的用户名添加别名。`(用户名):{该用户的别名}`
   - 为要转发邮件的外部电子邮件地址添加别名。`(用户名):email地址`
   - 为包含要转发邮件的用户列表的文件添加别名。`(用户名):include:{包含用户名的文件路径}`
   - 为从标准输入接收消息的 `Sendmail` 命令添加别名。`(用户名):(command)`。
8. 保存并关闭文件。
9. 要更新别名数据库文件，输入 `newaliases`。
10. 要重启 `postfix` 服务，输入 `service postfix restart`。

### 程序参考：配置别名

要配置虚拟别名：

1. 以 `root` 身份登录。
2. 别名的配置语法。
   a. 使用 `vi` 编辑器打开 `/etc/postfix/main.cf` 文件。
   b. 找到 `mydestination` 指令并定义由邮件服务器控制的域名。`mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain, mail.$mydomain, $mydomain`
   c. 保存并关闭文件。
   d. 使用 `vi` 编辑器打开 `/etc/aliases` 文件。
   e. 添加虚拟别名，`(用户名):email地址`
   f. 保存并关闭文件。
   g. 要更新别名数据库文件，输入 `postfix /etc/alias`。
   h. 要重启 `postfix` 服务。

### 程序参考：配置出站邮件消息

要配置 `postfix` 以发送出站邮件消息：

1. 以 `root` 身份登录。
2. 导航到 `/etc/postfix` 目录。
4. 为出站邮件消息进行域名伪装。
   a. 找到 "myorigin" 并取消其注释。
   b. 若要伪装 `root` 用户，输入 `masquerade_exceptions = root`。
5. 保存并关闭文件。
6. 要重启 `postfix` 服务，输入 `service postfix restart`。

### 程序参考：使用 Postfix 配置电子邮件别名

使用 `Postfix` 配置电子邮件别名：

1. 以 `root` 身份登录。
2. 使用 `vi` 编辑器打开 `/etc/postfix/main.cf` 文件。
3. 验证 `alias_maps` 变量是否定义了别名文件的位置。`alias_maps = hash:/etc/aliases`
4. 保存并关闭文件。
5. 使用 `vi` 编辑器打开 `/etc/aliases` 文件。
6. 为本地系统上存在的用户名添加别名。`(用户名):{该用户的别名}`。
7. 保存并关闭文件。
8. 要更新别名数据库文件，输入 `newaliases`。
9. 要重启 `postfix` 服务，输入 `service postfix restart`。

### 程序参考：配置本地别名

要配置本地别名：

1. 以 `root` 身份登录。
2. 使用 `vi` 编辑器打开 `/etc/postfix/main.cf` 文件。
3. 找到 `alias_maps` 指令并验证该指令是否定义了别名文件的位置，格式为 `alias_maps = hash:/etc/postfix/aliases`。
4. 找到 `alias_database` 指令并验证该指令是否定义了别名文件的位置，格式为 `alias_database = hash:/etc/postfix/aliases`。
5. 保存并关闭文件。
6. 使用 `vi` 编辑器打开 `/etc/postfix/aliases` 文件。
7. 添加电子邮件别名，`(用户名):{alias1}, alias2, alias3`
   - 为本地系统上存在的用户名添加别名。`(用户名):{该用户的别名}`
   - 为要转发邮件的外部电子邮件地址添加别名。`(用户名):email地址`
   - 为包含要转发邮件的用户列表的文件添加别名。`(用户名):include:{包含用户名的文件路径}|{文件名}
   - 为从标准输入接收消息的 `Sendmail` 命令添加别名。`(用户名):(command)`。
8. 保存并关闭文件。
9. 要更新别名数据库文件，输入 `postfix /etc/alias`。
10. 要重启 `postfix` 服务，输入 `service postfix restart`。

5. 要为接收者定义限制，请输入 `smtpd_recipient_restrictions = check_sender_access hash:/etc/postfix/recipient_access, [由逗号分隔的零或多个邮件客户端限制列表]`。
6. 保存并关闭文件。
7. 导航到 `/etc/postfix` 目录。
8. 打开发送者、接收者或客户端访问文件。
9. 定义限制条件。
   - 要允许中继继，输入 `{domain name} RELAY`。
   - 要接受来自指定域的邮件消息，输入 `{domain name} OK`。
   - 要拒绝来自指定域的邮件消息，输入 `{domain name} REJECT`。
   - 要拒绝来自发送者的邮件并显示任意消息，输入 `{domain name} ERROR: {### message}`。
   - 要在接收消息后丢弃它们，输入 `{domain name} DISCARD`。
10. 保存并关闭文件。
11. 要构建相应的访问数据库，输入 `postmap (发送者或接收者或客户端访问文件) <postmap (发送者或接收者或客户端访问文件)`。
12. 要重启 `postfix` 服务，输入 `service postfix restart`。

## 活动 13-1：配置 Postfix

开始之前：

1. 在 `srvA` 上，切换到 GUI。选择 `System->Administration->Network`。在 Network Configuration（网络配置）对话框中，选择 DNS 选项卡。
2. 在 Hostname（主机）文本框中，输入 `srvA.globalcompany.com` 并按 `Tab` 键。输入 `192.168.0.2` 作为主 DNS 和 DNS 路径。
3. 选择 Hosts（主机）选项卡并点击 `New`（新建）。在 Add / Edit Hosts 对话框中，在 Address（地址）文本框中，输入 `192.168.0.2` 作为 IP 地址。在 Hostname（主机）文本框中，输入 `srvA.globalcompany.com` 作为主机名。在 Aliases（别名）文本框中，输入 `srvA.globalcompany.com` 作为别名。
4. 在 Add / Edit Hosts 对话框中，点击 `OK`。选择 device（设备）选项卡。保存配置并点击 `Activate`（激活）以重启网络服务。
5. 在 `system-config-network` 消息框中，点击 `Yes`。
6. 在 `system-config-network` 消息框中，点击 `OK`。
7. 在 `srvB` 上，切换到 CLI。你已以 `root` 身份登录 CLI。显示了第一个终端。要停止 `sendmail` 服务，在命令行中输入 `service sendmail stop`。若要在系统启动期间禁用 `sendmail` 服务，输入 `chkconfig sendmail stop`。清除终端。
8. 在 `srvB` 上，切换到 GUI。选择 `System->Administration->Network`。在 Network Configuration 对话框中，选择 DNS 选项卡。在 Hostname 文本框中，输入 `srvB.globalcompany.com` 并按 `Tab` 键。输入 `192.168.0.2` 作为主 DNS 和 DNS 路径。
9. 选择 Hosts 选项卡并点击 `New`。在 Add / Edit Hosts 对话框中，在 Address 文本框中，输入 `192.168.0.3` 作为 IP 地址。在 Hostname 文本框中，输入 `srvB.globalcompany.com` 作为主机名。在 Aliases 文本框中，输入 `srvB` 作为别名。在 Add / Edit Hosts 对话框中点击 `OK`。
10. 选择 Devices 选项卡并点击 `Edit`。在 Ethernet Device 对话框中，选择静态 IP addresses 对象。点击 Address 文本框，输入 `192.168.0.3` 作为 IP 地址，并按 `Tab` 键。在 subnet mask（子网掩码）框中，输入 `255.255.255.0` 并按 `Tab` 键。在 Default gateway address（默认网关地址）文本框中，输入 `192.168.0.2` 并点击 `OK`。
11. 保存配置并点击 `Activate` 以重启网络服务。要关闭网络配置窗口，选择 `File->Quit`。切换到 `srvA` 的 CLI。清除终端屏幕。
12. 在 `system-config-network` 消息框中，点击 `Yes`。
13. 在 `system-config-network` 消息框中，点击 `OK`。

场景：

你的公司已经为 `globalcompany.com` 了使用 `Sendmail` 的邮件服务器。现在，由于组织增长，访问邮件服务器的用户数量增加，影响了服务器的性能。作为系统管理员，你决定将邮件服务器从 `Sendmail` 迁移到 `Postfix`。

1. 安装 `Postfix`。
   a. 在标记为 `srvA` 的系统上，输入 `yum localinstall /rhelsource/Server/postfix-2.3.3-2.1.el5_2.i1386.rpm` 并安装 `postfix-2.3.3-2.1.el5_2.i1386.rpm` 包。
   b. 若要继续，输入 `y`。
   c. 要将 `postfix` 设置为默认 `MTA`，输入 `alternatives --set mta /usr/sbin/sendmail.postfix`。

2. 在标记为 `srvA` 的服务器上配置入站邮件。
   a. 进入 `/etc/postfix` 文件夹。
   b. 使用 `vi` 编辑器打开 `main.cf` 文件。
   c. 找到行 `inet_interfaces = all` 并取消注释。
   d. 找到行 `inet_interfaces = localhost` 并将其注释。
   e. 要切换到命令模式，按 `Esc` 键。
   f. 找到代码 `$mydestination = $myhostname`。
   g. 取消注释行 `$mydestination = $myhostname, localhost.$mydomain, localhost, 以及 #mail.$mydomain, www.$mydomain, ftp.$mydomain.`。

3. 在标记为 `srvA` 的服务器上配置邮件别名。
   a. 找到指令 `alias_maps = hash;/etc/aliases`。
   b. 找到 `alias_database = hash;/etc/aliases` 指令并将文件位置更改为 `/postfix/`。
   c. 找到指令 `alias_database = hash;/etc/aliases` 指令。
   d. 取消注释行 `$mydestination = $myhostname, localhost.$mydomain, localhost, 以及 #mail.$mydomain, www.$mydomain, ftp.$mydomain.` 将文件位置更改为 `/postfix/`。
   f. 要切换到命令模式，按 `Esc` 键。
   g. 保存并关闭文件。
   h. 使用 `vi` 编辑器打开 `aliases` 文件。
   i. 输入 `root`。
   j. 输入 `root`。
   k. 要切换到命令模式，按 `Esc` 键。
   l. 保存并关闭文件。
   m. 更新 `aliases` 文件。
   n. 启动 `postfix` 服务。
   o. 要构建别名数据库，输入 `postmap /etc/aliases`。
   p. 启动 `postfix` 服务。

4. 检查配置。
   a. 从 `srvA` 切换到 `srvB`。切换到 CLI。
   b. 在标记为 `srvB` 的系统上，输入 `telnet globalcompany.com 25`。
   c. 输入 `HELO globalcompany.com`。
   d. 输入 `MAIL FROM: root@globalcompany.com`。
   e. 输入 `RCPT TO: chris@globalcompany.com`。
   f. 显示“Test mail - Postfix”。
   g. 退出邮箱。
   h. 清除终端。

5. 在 `srvA` 上定义限制条件。
   a. 使用 `vi` 编辑器打开 `main.cf`。
   b. 在文件末尾输入：
      ```
      smtptd_sender_restrictions = check_sender_access
      hash=/etc/postfix/sender_access
      ```
   c. 在文件末尾输入：
      ```
      smtptd_recipient_restrictions = check_recipient_access
      hash=/etc/postfix/recipient_access, reject_auth_destination
      ```
   d. 要切换到命令模式，按 `Esc` 键。
   e. 保存并关闭文件。
   f. 使用 `vi` 编辑器打开 `sender_access` 文件。
   g. 要在接收消息后丢弃它们，输入 `junk@gmail.com ERROR: 550 MAIL DISCARDED`。
   h. 要切换到命令模式，按 `Esc` 键。
   i. 保存并关闭文件。
   j. 构建发送者数据库，输入 `postmap /etc/postfix/sender_access`。
   k. 使用 `vi` 编辑器打开 `recipient_access` 文件。
   l. 要拒绝 `Eric` 的邮件，输入 `eric@globalcompany.com REJECT`。
   m. 要切换到命令模式，按 `Esc` 键。
   n. 保存并关闭文件。
   o. 构建接收者数据库，输入 `postmap /etc/postfix/recipient_access`。
   p. 重启 `postfix` 服务。
   q. 清除屏幕。

6. 检查来自 `junkmail.com` 的邮件是否被拒绝。
   a. 从 `srvA` 切换到 `srvB`。切换到 CLI。
   b. 在标记为 `srvB` 的系统上，输入 `telnet globalcompany.com 25`。
   c. 输入 `HELO globalcompany.com`。
   d. 输入 `MAIL FROM: junk@junkmail.com`。
   e. 输入 `RCPT TO: chris@globalcompany.com`。
   f. 显示错误消息“451 4:3.5 Server configuration error”，表示垃圾邮件过滤器正在工作。
   g. 退出 Telnet 连接。

7. 检查接收者 `Eric` 是否被允许发送邮件。
   a. 在标记为 `srvB` 的系统上，输入 `telnet globalcompany.com 25`。
   b. 输入 `HELO globalcompany.com`。
   c. 输入 `MAIL FROM: chris@globalcompany.com`。
   d. 输入 `RCPT TO: eric@globalcompany.com`。
   e. 显示错误消息“Recipient address rejected: Access denied.”。
   f. 退出 telnet 连接。
   g. 清除终端屏幕。

# 主题 B：控制互联网服务

在上一个主题中，你配置了电子邮件服务。互联网提供了许多服务和优势。这使得互联网成为几乎所有组织必不可缺的工具。在本主题中，你将控制互联网服务。

互联网服务对于业务的有效运行至关重要。互联网服务的任何中断或问题都可能导致工作瘫痪，并为组织带来高昂成本。作为 Linux 管理员，你的主要职责是确保互联网服务始终无问题地运行。

## xinetd 守护进程

`xinetd` 守护进程控制网络上的系统服务，并基于客户端-服务器架构。`xinetd` 的配置文件中列出了各种服务。当守护进程接收到对特定服务的请求时，它会检查配置文件并启动包含该服务的相应服务器。这使得能够在网络上进行更快速的服务管理，因为请求被即时处理。由 `xinetd` 管理的服务包括文件共享、`Telnet`、`rsync` 和时间管理。这些服务的设置可以使用 `/etc/xinetd.conf` 文件或位于 `/etc/xinetd.d` 目录下的特定服务文件进行控制。

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_559_0.png)

**图 13-8：** `xinetd` 守护进程控制客户端和服务器上的服务。

## Telnet

**定义：**

`Telnet` 是一种终端仿真协议，允许站点的用户模拟远程主机上的会话。换句话说，它允许用户通过网络登录到另一台计算机。它通过将用户终端的按键转换为远程主机识别的指令，并将输出传回用户的终端并以远程主机的原生格式显示来实现。该服务是透明的；它给用户一种感觉，认为他们的终端直接连接到远程主机上。远程计算机需要安装一个 `Telnet` 服务器。

示例：

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_560_0.png)

**图 13-9：** 与远程 `Telnet` 服务器通信的 `Telnet` 客户端。

### Telnet 的缺点

`Telnet` 不是一个非常安全的协议，因为它以明文传输密码。由于 `SSH` 更好的安全性，`Telnet` 已经在很大程度上被 `SSH` 取代。

## /etc/xinetd.conf 文件

`/etc/xinetd.conf` 文件是 `xinetd` 守护进程的配置文件，包含了由守护进程管理的服务列表。每当请求启动或停止某个服务时，守护进程都会引用该文件。该文件被分为不同的部分，每个部分包含相应服务的设置。服务可以是单线程或多线程的。

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_560_1.png)

**图 13-10：** 带有各种配置设置的 `/etc/xinetd.conf` 文件。

可以使用许多选项配置 `/etc/xinetd.conf` 文件以满足用户需求。下表列出了一些常用的选项。

| 选项 | 能够实现的功能 |
| --- | --- |
| `service` | 指定服务名称。 |
| `wait` | 指定服务是单线程还是多线程。 |
| `user` | 指定在服务器上运行的进程的 UID。 |
| `server` | 指定调用服务时要启动的可执行文件。 |
| `disable` | 指定服务是启用还是禁用。 |

#### 语法

在 `xinetd` 配置文件中指定服务的语法为 `{属性赋值操作符} 值。

## libwrap.so 库

`libwrap.so` 文件是链接到由 `xinetd` 守护进程控制的服务库。有三个主要的二进制库文件：`libwrap.so`、`libwrap.so.0` 和 `libwrap.so.0.7.6`。这些文件位于 `/usr/lib` 目录中，控制 TCP 服务和额外的网络访问服务，包括网络访问配置文件中的找到设置。

## /etc/xinetd.d 目录

`/etc/xinetd.d` 目录包含由 `xinetd` 管理的服务配置脚本。该目录列出的某些服务包括 `ftp`、`kerberos` 和 `rsync`。每个服务都可以使用该目录中的配置文件进行单独配置。服务配置文件中的选项与 `/etc/xinetd.conf` 文件中的选项相似。

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_561_0.png)

图 13-11：`xinetd.d` 目录包含用于 `xinetd` 管理的服务的配置文件。

## xinetd 访问控制

`xinetd` 守护进程有一组函数用于控制对其管理的服务的访问。
这些访问控制有两种类型：基于主机的和基于时间的。

| 访问控制类型 | 描述 |
|---|---|
| 基于主机的访问控制 | 通过在 `xinetd` 服务配置文件中使用 `no_access` 和 `only_from` 选项来限制主机来实现。在实施基于主机的访问控制时，使用主机访问控制来指定主机模式。主机可以用 IP 地址、子网掩码范围、网络名称或主机名的形式进行指定。 |
| 基于时间的访问控制 | 通过向服务配置文件中添加 `access_times` 选项来实现。 |

## 服务和应用程序访问控制

服务访问控制和应用程序访问控制是用于限制某些服务和应用程序的守护进程，这些访问控制通过引用 `libwrap.so` 文件中的主机名或 IP 地址来限制访问。这些守护进程的示例包括 `squid` 和 `httpd`。

## 如何控制互联网服务

### 过程参考：配置由 xinetd 管理的服务

配置由 `xinetd` 管理的服务：

1. 以 `root` 身份登录。
2. 列出由 `xinetd` 管理的服务，`ls /etc/xinetd.d/`
   > 在旧版本的 Linux 中，`/etc/xinetd.d/` 文件被称为 `/etc/inetd.d/`。
3. 管理启动时的 `xinetd` 守护进程。
   - 确保 `xinetd` 守护进程已配置。
4. 检查 `xinetd` 守护进程的状态，`service xinetd status`。
5. 启动 `xinetd` 守护进程，`service xinetd start`。
6. 停止 `xinetd` 守护进程，`service xinetd stop`。
7. 重启 `xinetd` 守护进程，`service xinetd restart`。
8. 重新加载 `xinetd` 守护进程，`service xinetd reload`。
9. 管理由 `xinetd` 控制的服务。
   - 在启动时启用或禁用服务，`chkconfig {service name} {on|off}`。
10. 使用位于 `/etc/xinetd.d` 中的配置文件管理服务。
   - a. 编辑特定服务的配置文件，`vi /etc/xinetd.d/{service configuration}`。
   - b. 禁用或启用服务，编辑 `disable = {yes|no}` 行。
   - c. 定义覆盖 `xinetd` 守护进程管理的所有服务的特定设置，编辑 `<赋值操作符> <value>`。
   - d. 保存并关闭文件。
   - e. 应用更改重新加载 `xinetd` 守护进程，`service xinetd reload`。

### 过程参考：在 /etc/xinetd.conf 文件中定义全局设置

在 `/etc/xinetd.conf` 文件中定义全局服务设置：

1. 以 `root` 身份登录。
2. 编辑 `xinetd` 配置文件，`vi /etc/xinetd.conf`。
3. 保存并关闭文件。
4. 应用更改并重启 `xinetd` 守护进程，`service xinetd restart`。

### 过程参考：配置 xinetd 管理服务的访问控制

配置 `xinetd` 管理服务的访问控制：

1. 以 `root` 身份登录。
2. 在 `/etc/xinetd.conf` 文件中定义特定服务的访问控制。
   - a. 定义允许访问特定服务的远程主机，`only_from = {list of IP addresses}`，
   - b. 定义禁止访问特定服务的远程主机，`no_access = {list of IP addresses}`，
3. 保存并关闭文件。
4. 应用更改并重启 `xinetd` 守护进程，`service xinetd restart`。

- 2. 使用 `Telnet` 发送邮件消息并观察结果，以确保 `SMTP` 服务器正常运行。
   a. 要指定主机名，输入 `HELO {server name}`。
   b. 要指定发件人邮箱地址，输入 `MAIL FROM: email address`。
   c. 要指定收件人邮箱地址，输入 `RCPT TO: email address`。
   d. 输入 `DATA`。
   e. 输入主题和消息。用句结束消息。

## 活动 13-2：启用服务访问控制

开始之前：

1. 在 `srvA` 上，你已以 `root` 身份登录到 CLI。
2. 要导航到根目录，输入 `cd /root`。
3. 要清空终端屏幕，输入 `clear`。

**场景：** 你在 OGC 担任系统管理员。你的机构有多个分支机构，你希望让在不同分支机构的员工能够相互通信。你想使用 `telnet` 协议传输文件并添加隧道功能。此外，你还需要配置该服务在系统启动时自动启动。最后，你必须确保无法从 IP 地址为 `192.168.0.205` 的系统访问该服务，因为它会被未经授权的用户访问。

1. 在系统上安装 `telnet` 服务。
   a. 要安装 `telnet` 服务，输入 `yum localinstall /resource/Server/telnet*`。
   b. 观察事务摘要（Transaction Summary）显示有一个包待安装。同时，观察总下载大小为 35 k。
   c. 要下载并安装该包，输入 `y`。
   d. 观察到显示消息“Complete”，表示 `telnet` 服务已安装。

2. 启用 `telnet` 服务器。
   a. 要打开 `telnet` 配置文件，输入 `vi /etc/xinetd.d/telnet`。
   b. 观察显示的默认配置项。同时，观察到由于 `disable=yes`，该服务已禁用。
   c. 要导航到“disable = yes”行，输入 `/dis`。
   d. 切换到插入模式。
   d. 将 `disable = yes` 改为 `disable = no`。

3. 为 `telnet` 服务启用访问控制。
   a. 在新行上，按 `Tab` 键。
   b. 输入 `only_from` 并按 `Tab` 键。允许仅从 `192.168.0.0/24` 访问该服务。
   c. 按 `Tab` 键并输入 `no_access`。要拒绝所有用户从 `192.168.0.205` 访问服务，按 `Tab` 键并输入 `=192.168.0.205`。
   d. 切换到命令模式。
   e. 保存并关闭文件。

4. 配置 `xinetd` 启动启动。
   a. 要启动 `xinetd` 服务，输入 `service xinetd start`。
   b. 要启用 `xinetd` 服务随系统启动，输入 `chkconfig xinetd on`。
   c. 清空终端屏幕。

## 第 13 节后续

在本节中，你配置了电子邮件服务并控制了互联网服务。现在，你将能够为跨网络的资源通信、共享和传输实现一种成本效益的解决方案。

1. 你会在你的机构中配置哪种邮件检索协议？为什么？
2. 在你的机构中实施 `sendmail` 有什么优势？

# 14 Linux 安全性

课程时长：1 小时 30 分钟

# 课程目标

在本节中，你将实施措施来保护 Linux 系统。

你将：

- 实现加密服务。
- 保护用户帐户。
- 实现 `iptables`。
- 实现安全目的的审计。
- 描述入侵检测系统（IDS）。

## 简介言

在上一节中，你配置了基础互联网服务。所有网络服务，无论多么基础，都需要安全保护。薄弱的安全性会导致来自不满的员工、黑客或竞争对手的损害或损失。在本节中，你将保护连接到网络的 Linux 系统。

为了妥善地保护 Linux 系统，管理员必须理解不同威胁将影响系统。需要实施特定的安全措施，允许管理员控制敏感数据的传输，并限制未经授权的用户访问网络。

本节涵盖了 CompTIA+ Linux+（由 LPI 支持）认证的全部或部分内容：

- 主题 A：
  - 目标 110.2，目标 110.3
- 主题 B：
  - 目标 105.1，目标 107.1，目标 110.1，目标 110.2
- 主题 E：
  - 目标 110.1

# 主题 A：系统安全基础

在上一节中，你处理了互联网和电子邮件服务。这些服务容易受到黑客的威胁，可能会导致严重问题。组织网络的安全漏洞无法通过破坏或数据窃取来妥协，这会严重影响业务。通过保护系统并以安全格式发送数据（只有数据接收者才能理解），可以避免这些情况。在本主题中，你将检查系统安全的基础。

计算机安全是业务战略的关键部分，组织不断要求更高层次的保护。在网上，可以实现各种 Web 和邮件服务。这些服务促进了数据传输，但始终存在数据窃取的风险。如果没有适当的安全机制，传输敏感数据是不可能的。

### 密钥

在登录远程机器时，主机会发送你的公钥和服务器密钥进行身份验证。你的系统查找 `known_hosts` 文件以查找条目，如果找到了条目，将授予你访问权限。

![](img/b54ed9904f9bb8a2eb509710fb2afd6_569.png)

图 14-1：使用密钥保护数据。

密钥有两种类型：公钥和私钥。

| 密钥类型 | 描述 |
| :--- | :--- |
| 公钥 | 随请求传输的密钥。与私钥进行比较。只有当两者相关时，验证通过。 |
| 私钥 | 保留在本地不传输的密钥。随消息发送。 |

## 身份验证

身份验证验证用户身份真实。在数据通信中，验证发送者以确保数据来自来源。也要验证接收者，以确保数据去往目的地。

有多种确保身份验证的方法。

| 方法 | 描述 |
| :--- | :--- |
| `known_hosts` 文件 | 当连接主机时，主机发送你的公钥和服务器密钥进行身份验证。你的系统查找 `known_hosts` 文件以查找条目，如果找到了条目，将授予你访问权限。 |
| `SSH` 服务器 | 自动生成身份验证所需的公主机和服务器密钥的服务器。服务器密钥每小时重新生成一次以确保安全。 |
| 挑战握手认证协议 (`CHAP`) | 使用密钥加密用户名和密码信息并将其传输到网络的安全认证协议。`CHAP` 支持使用点对点协议（`PPP`）封装的线路。 |
| 密码认证协议 (`PAP`) | 用于登录网络的安全认证协议。在 `PAP` 中，未加密的用户名和密码通过网络传输到服务器。这些信息将与网络上所有用户的用户名和密码表进行比对。`PAP` 仅支持 `PPP` 线路。 |
| `Kerberos` | 一种用于客户端/服务器应用程序的网络认证服务。`Kerberos` 为登录网络的每个用户创建一个密钥或票据。票据被嵌入消息中以识别发送者。 |

- 单因素认证提供的是“你所知道的”，例如密码或 PIN 码。它基于从记忆中回忆某些信息或将信息写下来。这种认证方式的效果最低。
- 双因素认证，将“你拥有的”与“你所知道的”相结合。例如，你的 ATM 卡结合 PIN 码即可访问你的银行账户。
- 三因素认证，还通过生物识别提供用户的身份证明。它使用生理识别特征，如指纹、人声识别或签名识别。这是最有效的认证类型。

## 生物识别认证

为了提高系统的可靠性水平并方便用户使用（超越密码认证），可以引入生物识别认证。当此类系统被添加到身份验证方案中时，它被认为是强身份认证。之所以被称为“强认证”，是因为用户不仅通过数字方式被识别，还通过其生理特征（通过指纹扫描、虹膜扫描或手部几何结构）。

## 加密

加密是一种控制用户访问信息的方法，通过将数据配置为未经授权的用户无法解释的代码。然而，对于授权用户来说，这些数据以原始形式出现。密码也可以与加密一起用于保护数据。各种协议，如 `SSH`、`SSL` 和 `SECURENET`，被用于实现网络加密。

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_571_0.png)

图 14-3：使用加密保护数据。

## 加密解决方案

加密计算机数据的授权用户必须拥有用于加密数据的密钥才能进行解密。可以使用特定的算法通过不同的解决方案对数据进行加密。

| 解决方案 | 描述 |
| --- | --- |
| `Blowfish` | 一种对称块密码，提供强加密并使用最长达 56 字节的密钥（448 位密钥）。其特性包括：
- 对强密钥的支持、处理和密码学。
- 能够擦除文件和清除空磁盘空间的安全性。 |
| `3DES` | 一种块密码算法（读音为 "triple dez"），可以使用密钥对数据进行加密和解密。`3DES` 使用 `DES`（数据加密标准）的三阶段，使其成为一个非常安全的选项。任何由 `DES` 加密的内容都有 72,000,000,000,000（或 72 亿）种可能的密钥。 |
| `MD5` | 消息摘要算法 5 (`MD5`) 是一种命令行程序，使用 `MD5` 算法生成并验证消息摘要（数字签名）。 |

`MD5` 算法用于数字签名应用，在这些应用中，大文件在用公钥加密系统下的私钥（密钥）加密之前，必须以安全的方式压缩。
`MD5` 也用于检查文件的完整性。

## 随机数生成

随机数生成是一种加密方法，其中内核被用于生成随机数并在传输前分配给文件。只有当接收者匹配这些数字时，传输才完成。控制随机数生成的算法是伪随机数生成（PRNG）算法。在 Red Hat Linux 中，内核文件 `/dev/random` 和 `/dev/urandom` 充当随机数生成器。利用排列和组合的概念，这些内核能够从单个源数字生成数百万位数的数字。

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_572_0.png)

**图 14-4：** 使用随机数生成方法保护数据。

## 密码哈希

密码哈希用于一种加密方法，其中任意数据被封装在附加到文件上的指纹中。这个固定字符串被称为哈希值、校验和或消息摘要。可以通过验证哈希值来检查文件中数据的真实性。当对文件进行修改时，其哈希值也会发生变化。各种算法，如 `md2`、`md5`、`sha` 和 `sha` 被用于实现密码哈希函数。

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_573_0.png)

图 14-5：使用密码哈希方法保护数据。

各种工具被用于检查文件的哈希值。

| 工具 | 能够让你 |
| --- | --- |
| `shasum` | 检查文件是否存在不正确的 `sha` 校验和。该工具的语法为 `shasum --check (文件名)`。 |
| `md5sum` | 检查文件是否存在不正确的 `md5` 校验和。该工具的语法为 `md5sum --check (文件名)`。 |

## 对称加密

对称加密仅使用单一密钥执行，该密钥同时用于加密和解密。各种工具被用于执行对称加密。

| 工具 | 用途 |
| --- | --- |
| `passwd` | 修改登录密码。已登录的用户只能更改自己的登录密码，而不能其他用户的。然而，这不适用于 `root` 用户。当你在命令行提示符处输入 `passwd` 命令时，会要求你输入当前密码，然后是想要设置的新密码。新密码将在下次登录系统时生效。 |
| `gpg` | 使用 GNU 隐私守护 (GnuPG) 加密系统加密消息。该工具具有各种命令和选项。该工具的语法为 `gpg [options] (command) [arguments]`。 |

| 工具 | 用途 |
| --- | --- |
| `openssl` | 通过创建密钥、证书和签名使用 `SSL` 协议加密和解密消息。该工具的语法为 `openssl {command} [arguments]`。 |
| `make` | 生成数字证书和密钥对。此命令必须在 `/etc/pki/tls/certs/` 目录下运行。该工具的语法为 `make file digital certificate` |

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_574_0.png)

图 14-6：对称加密的密钥生成。

## 非对称加密

非对称加密使用密钥对形式的两个密钥执行。其中一个密钥用于加密，另一个密钥用于解密。

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_574_1.png)

图 14-7：非对称加密的密钥生成。

非对称加密涉及两种主要协议：协议 1 和协议 2。一次只能实现一种协议。

| 协议 | 描述 |
| ------|---|
| 协议 1 | 发送者和接收者之间交换单一密钥。
1. 接收者首先生成密钥对，包含公钥和私钥。
2. 请求随后以加密形式连同接收者的公钥发送给发送者。私钥留在接收者。
3. 发送者接收请求，验证接收者发送的公钥，并以加密形式连同接收者的公钥返回请求的信息。
4. 接收者接收带有公钥的信息，并通过其私钥进行解密。 |
| 协议 2 | 数字签名与密钥加密结合使用。数字签名是发送者消息摘要加密时生成的唯一标识。
1. 发送者首先生成密钥对，包含公钥和消息摘要，使用发送者生成数字签名。
2. 公钥传输到网络上的所有系统。随后接收者向发送者发送请求。
3. 发送者接收请求，并加密形式连同其数字签名返回信息。
4. 接收者接收信息，并通过其公钥验证发送者的数字签名。 |

## 伪公钥

伪公钥由未经授权的用户生成以绕过公钥加密。它们被用于解密他们不应访问的信息。通过使用公钥指纹、形成信任组以及通过受信任的证书机构颁发数字证书，可以防止伪密钥的生成。

# 数字证书类型

数字证书是一种对称加密方法。目前有两种主要类型的数字证书。

| 证书类型 | 描述 |
|---|---|
| 证书颁发机构 | 证书颁发机构证书由共同且信任的证书颁发机构 (`CA`) 在收到证书签名请求 (`csr`) 后生成。这种方法的优点是可以防止伪造数字证书。 |
| 自签名 | 自签名证书由用户自行生成，并包含用户的公钥作为签名。因此，任何用户都可以创建自签名证书。然而，这种证书不提供对用户或组织身份的保证。 |

> `X.509` 格式是公钥证书的标准格式。

# 软件包完整性

Linux 中的每个软件包都分配有一个公钥，该公钥会与软件包一起安装。软件包完整性是检查软件包是否包含这些公钥的方法，以确保软件包来自信任的供应商。在安装软件包之前，有必要进行软件包完整性测试，因为从不可靠源安装软件包可能会导致安装不当和病毒攻击。`yum` 命令始终从 Red Hat 在线存储库连同公钥安装软件包。

`rpm` 命令用于检查文件完整性。

| 命令 | 功能 |
|---|---|
| `rpm --verify (package name)` | 检查软件包是否已安装。 |
| `gpg --import` | 将公钥导入 `rpm` 数据库。 |
| `/etc/pki/rpm/rpm-gpg/RPM-GPG-KEY-redhat*` | |
| `rpm --checksig (package name)` | 检查软件包是否具有有效签名。 |
| `rpm --addsign (package name)` | 为软件包分配有效签名。 |

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_577_0.png)

# RADIUS

远程拨号接入用户服务 (`RADIUS`) 是一种客户端/服务器协议，用于实现网络上的集中认证、授权和计费。用户信息存储在中央数据库中，所有远程服务器共享。当用户发送访问服务或资源的请求时，`RADIUS` 允许远程访问服务器与中心服务器（存储在服务器的 `/etc/passwd` 文件中）进行通信，以验证用户的凭据。它通常利用用户的登录和密码，通过 `MD5` 算法加密密码来实现密码的安全传输。`RADIUS` 服务由互联网服务提供商 (`ISP`) 使用。

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_578_0.png)

图 14-9：在网络提供远程认证服务的 `RADIUS` 协议。

# 作为网络访问服务器的 RADIUS 服务器

当网络包含多个远程访问服务器时，可以将其中一个配置为 `RADIUS` 服务器，并将所有其他服务器配置为 `RADIUS` 客户端。`RADIUS` 客户端将所有认证请求传递给 `RADIUS` 服务器进行验证。用户配置、远程访问策略和使用日志可以集中在。在这种配置中，远程访问服务器通被称为网络访问服务器 (`NAS`)。

# TCP Wrappers

定义：

TCP wrappers 是保护层，定义了允许和不允许连接到某些网络服务的主机计算机。TCP wrappers 软件包包含 `/lib/libwrap.so.0` 库。被 TCP wrappers 封装的服务使用 `libwrap.so.0` 库编译。TCP wrappers 独立于其所保护的网络服务运行。

示例：

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_579_0.png)

图 14-10：带有保护层的 TCP wrappers。

# 如何实现加密服务

### 过程引用：配置加密

配置加密：

1. 以 `root` 身份登录。
2. 打开文件，进入 `/etc/{application}/{configuration file}`。
3. 找到包含加密详情的行。
4. 如必要，取消该行的注释。
5. 修改该行以更改加密类型。
6. 保存文件并退出编辑器。
7. 重启应用程序或设备的守护进程使更改生效。

### 过程引用：实现密码学服务

实现密码学服务：

1. 以 `root` 身份登录。
2. 实现密码学服务：
   - 生成随机数，输入 `openssl rand {options}`（伪随机字节数）。
   - 生成消息摘要。
     - 要计算并检查 `SHA1` 消息摘要，输入 `shasum [options] {file name}`。
     - 要计算并检查 `MD5` 消息摘要，输入 `md5sum [options] {file name}`。
     - 输出指定文件的消息摘要，输入 `openssl digest {digest options} {file name}`。
   - 使用 `gpg` 命令实现对称加密。
     - 要使用对称加密加密文件，输入 `gpg --symmetric {file name}`。

> `~/.gnpg` 是存储使用 `gpg` 命令创建的私钥和公钥的目录。

- 使用 `openssl` 命令实现加密。
  a. 加密并将输出存储在另一个文件中，输入 `openssl enc -salt -in {file name} -out {output file}`。
  b. 根据提示输入对称加密密码。

### 过程引用：验证软件包完整性

使用 `rpm` 命令验证软件包完整性：

1. 以 `root` 身份登录。
2. 将公钥导入 `rpm` 数据库，输入 `gpg --import /etc/pki/rpm/rpm-gpg/RPM-GPG-KEY-redhat*`。
3. 检查软件包是否已安装，输入 `rpm --verify (package name)`。
4. 检查软件包是否具有有效签名，输入 `rpm --checksig (package name)`。
5. 为软件包分配有效签名，输入 `rpm --addsign (package name)`。

### 过程引用：生成数字证书

生成数字证书：

1. 以 `root` 身份登录。
2. 使用 `openssl` 命令生成密钥：
   a. 生成公钥或私钥，输入 `openssl genrsa -out {file name}.key`。
   b. 生成证书请求，输入 `openssl req -new -key {file name}.key -out {file name}.csr`。
   c. 生成自签名证书，输入 `openssl req -x509 -new -key {file name}.key -out {file name}.crt -days 365`。

## 活动 14-1：配置加密

**开始之前：**
1. 在 `srvA` 上，你已以 `root` 身份登录 CLI。
2. 显示了第一个终端。

**场景：**
在分析日志文件时，你发现访问 `SSH` 服务的尝试失败。你决定配置 Linux 服务器，使其在通过 `SSH` 传输数据之前使用 `Blowfish` 对信息加密。

1. 编辑 `/etc/ssh/ssh_config` 文件。
   a. 要打开文件，输入 `vi /etc/ssh/ssh_config`
   b. 找到文本 "Cipher."。
   c. 取消注释行 `# Cipher 3des.`。
   d. 在同一行上删除 "3des."。
   e. 按 `I` 切换到插入模式。
   f. 按 `Spacebar` 并输入 `blowfish`
   g. 要保存并关闭文件，按 `Esc` 并输入 `:wq`

2. 重启 `sshd` 服务。
   a. 输入 `service sshd restart`
   b. 要检查服务是否启动，输入 `service sshd status`
   c. 验证 `openssh-daemon` 正在运行。
   d. 要清除终端屏幕，输入 `clear`

# 主题 B：安全用户账户

你现在已经熟悉了加密和基础系统安全。下一步是使用安全的计算环境来保护用户。在这个主题中，你将保护用户账户的安全。

鉴于 Linux 作为安全操作系统的声誉，人们可能有一种内在的倾向，以随意的态度对待用户安全。然而，作为一名 Linux 管理员，建立组织政策以帮助在你的 Linux 用户社区中建立最佳实践是非常重要的。通过这样做，你将限制灾难发生的可能性，特别是当你的用户群增长时。

## 环境文件

在 Linux 中，可以自定义多个环境文件。

| 文件 | 描述 |
| --- | --- |
| `/etc/hosts.allow` | 允许访问某些服务和主机。 |
| `/etc/hosts.deny` | 拒绝访问某些服务和主机。 |
| `/etc/limits` | 当系统安装了影子密码时，限制用户的资源。 |
| `/etc/login.defs` | 在安装了影子密码的系统上设置用户登录功能。 |
| `/etc/passwd` | 显示用户的用户名、真实姓名、主目录、加密密码和其他信息。 |
| `/etc/securetty` | 标识允许 `root` 用户登录的安全终端。 |
| `/var/log/secure` | 跟踪用户登录。建议定期检查此文件。 |

## /etc/login.defs 文件

`/etc/login.defs` 文件与影子密码配合使用，设置初始路径和其他参数，包括用户必须更改密码的频率以及什么级别的密码是可以接受的。

## 登录级别

在 Linux 中，你可以为资源提供 `root` 级或用户级的访问。默认情况下，`root` 用户具有对系统上所有信息的登录权限，而其他用户具有有限的登录权限。

| 登录级别 | 描述 |
| --- | --- |
| Root 登录 | Root 用户被视为一个特定的用户账户，UID 为 0。它拥有系统上其他用户都不具备的权限。具体来说，`root` 用户可以在系统的任何地方导航，更改任何文件，并操作系统控制，包括用户账户、存储设备和内核参数。系统管理员通常会有一个具有普通用户权限的所有者账户和一个 `root` 账户。根据经验，在从 `root` 用户账户工作之前，你应该尽可能在你的 UID 下进行操作。 |
| 用户登录 | 创建用户账户时必须考虑安全性。用户名（或登录 ID）和密码存储在两个文件中：`/etc/passwd` 和 `/etc/shadow`，并被设置了受限的访问权限以增加安全性。用户账户文件 `/etc/passwd` 设置为除 `root` 用户以外的所有人的只读文件。 |

## Root 用户的别名

如果你使用 `Bash` shell，可以作为一种预防措施为 `root` 创建一个别名。在这种情况下，别名是 `.bashrc` 文件中的一项，你可以在其中为特定的默认命令定义额外的操作。例如，用于删除或移除文件的 `rm` 命令可以赋予一个别名，根据你设置的标准提示你提供额外信息。

## su 命令

替换或切换用户（switch user, `su`）命令用于在不注销登录的情况下更改登录会话的所有者。它通常用于在普通用户和 `root` 用户之间切换所有者，以更改管理工作所需的访问权限。

![](img/b54ed9904f9bb8a2eb5097106fb2afd6_585_0.png)

**图 14-11:** 使用 `su` 命令切换用户。

## 登录 shell 与非登录 shell

登录 shell 是在用户登录期间创建的 shell。相反，非登录 shell 是你从一个登录 shell 内部调用的 shell。例如，从登录 shell 运行 `su` 命令会调用非登录 shell。然而，`GNOME` 终端中的 `su` 命令和执行的脚本都是非登录 shell。`logout` 命令只能在登录 shell 中运行，而 `exit` 命令可以在登录 shell 和非登录 shell 中运行。

### id 命令

你可以使用 `id` 命令查看标识信息。

## sudo 命令

`sudo` 命令允许用户以另一个用户的安全权限运行程序。它通常用于执行需要管理权限的任务。`sudo` 在 `/etc/sudoers` 文件中配置，该文件定义了哪些用户或组可以运行哪些命令。`sudo` 命令的语法为 `sudo [options] command`。例如，如果用户有，`sudo -h`。

```
