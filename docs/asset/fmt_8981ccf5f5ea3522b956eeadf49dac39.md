
5月4日 20:43:14 beech.example.com ftppd[2974611]: 用户 mleenplik 在 2002年5月4日 20:43:14 900 秒后超时

# 第 V 部分：增强安全性

## 消息选择

在大多数情况下，你可能非常想对消息内容进行选择。以下 `grep` 命令检索了所有与用户账户 vroont 活动相关的记录：

```
* egrep *[^ ] *[^ ] *[^ ] *[^ ] *[^ ] *:vroont.*\*
/var/syslog/messages.3
```

5月7日 12:04:22 redmap.example.com sshd[3385918]: log: vroont 的密码验证已通过。

5月7日 12:04:36 redmap.example.com sudo : vroont : TTY=ttyq7 : PWD=/users/s/b/vroont/home : USER=root : COMMAND=/usr/local/bin/bash

5月7日 18:30:58 blackoak3.example.com sshd[15901]: log: vroont 的密码验证已通过。

5月7日 19:38:07 blackoak3.example.com sshd[21873]: log: vroont 的密码验证已通过。

5月7日 19:42:09 kerberos.example.com fakeika[178]: authenticate: 来自 192.168.60.39 的 vroont.top

5月7日 20:35:13 blackoak3.example.com sudo : vroont : TTY=pts/67 : PWD=/users/root : USER=root : COMMAND=/usr/local/bin/bash（等待，OCR 文本中出现了两次“5月7日 19:42:09”并有中断，让我们重新对齐日志流）

```
5月7日 19:42:09 kerberos.example.com fakeika[178]: authenticate: 来自 192.168.60.39 的 vroont.top
5月7日 20:35:13 blackoak3.example.com sudo : vroont : TTY=pts/67 : PWD=/users/root : USER=root : COMMAND=/usr/local/bin/bash
```

```
5月7日 20:46:31 blackoak2.example.com sshd[3092]: log: vroont 的密码验证已通过。
来自 blackoak3.example.com 的登录账户 vroont
```

```
5月7日 20:46:57 blackoak2.example.com sudo : vroont : TTY=pts/70 : PWD=/afs/example.com/users/vroont/home : USER=root : COMMAND=/usr/local/bin/bash
```

```
5月7日 20:49:33 blackoak1.example.com sshd[2308]: log: vroont 的密码验证已通过。
来自 blackoak3.example.com 的登录账户 vroont
```

```
5月7日 20:49:50 blackoak1.example.com sudo : vroont : TTY=pts/90 : PWD=/afs/example.com/users/vroont/home : USER=root : COMMAND=/usr/local/bin/bash
```

```
5月7日 20:56:32 blackoak1.example.com sshd[1373]: log: vroont 的密码验证已通过。
来自 blackoak3.example.com 的登录账户 vroont
```

# 第 19 章：日志监控与事件响应

决策往往涉及超出大多数系统管理员职责范围的权衡。让那些应该做决策的人同意某些行动方案。

噢，没错。任何此类政策都应该包含此类表述，要求系统管理员报告任何疑活动（即使该活动与你正在排查的特定问题无关）。该表述还应包含一条“不要射信者”的规则。

### 总结

本章的重点是，记录日志和检查日志——虽然枯燥且费力，但它是维护系统安全的最有效措施之一。然而，你可以使用自动化报告来大幅减少这些枯燥工作。始终记住，日志监控是必须的。一段时间后，你会发现自己对系统及其使用方式的理解远比其他时候要深得得多。当你能够在重大灾难还处于萌芽状态时阻止它们发生，这种理解往往是极具价值的。

## 附录 A

## www.wiley.com 存储了什么？

Wiley 提供了多个软件软件包和自定义脚本。你可以在 `http://www.wiley.com/compbooks/sery` 找到这些项目：

- 自动基于网络的备份配置

- DNS 配置

- 动态 IP (DHCP) 分配配置

- 电子邮件配置

- 防火墙配置

- Icecast/IceS 配置

- 互联网拨号连接

### 备份下载内容

下载 AMANDA 客户端和服务器配置文件。

### 拨号下载内容

下载示例 `diald` 和 `PPP` 脚本

### DNS 下载内容

下载示例 DNS 配置文件和区域文件

### DHCP 下载内容

下载示例 DHCP 配置文件

### 邮件下载内容

为内部和外部 sendmail 服务器提供了示例的 `sendmail.mc` M4 脚本（分别为 Chivas 和 Atlas）。

- Chivas（私有网络）`sendmail.mc` M4、mailertable 以及其他脚本

- Atlas（DMZ）`sendmail.mc` M4、mailertable 以及其他脚本

### 防火墙下载内容

提供以下文件的下载：

- 简单防火墙/iptables 脚本 (`fw.simpl`)

- 高级防火墙/iptables 脚本 (`fw.full`)

- 防火墙重置脚本 (`fw.reset`)

### Kickstart 下载内容

提供以下 Kickstart 文件的下载：

- 示例 Atlas kickstart (`ks.cfg`) 配置

- 示例 Chivas kickstart (`ks.cfg`) 配置

### Icecast/IceS 下载内容

在这里你可以下载创建流媒体服务器所需的配置文件。

- Icecast 和 Ices 版本 1 示例配置文件

- Icecast 和 Ices 版本 2 示例配置文件

## 附录 B

## 配置拨号上网连接

你**不需要高速技术**来将你的私有网络连接到互联网。旧技术——1990 年代的风格——可以提供小型网络互联网功能。当然，按照今天的标准，旧速度很慢，但至少你会有连接。本附录描述了如何使用调制解调器和点点协议（`PPP`）建立连接。

### 定位你的调制解调器

安装你的调调器来让我开心一下。如果有，请遵循调调器自带的说明。在将调制解调器插入主板或通过串口线连接它之后，你必须告诉 Linux 在哪里找到它；这意味着设置一个指向连接调调器的串口的设备文件。接下来的两个部分描述了如何使用 Microsoft Windows 或 Red Hat Linux 实用程序寻找调器。

![](img/75465a3c65cedf6b73d2aa7a566f6512_520_0.png)

> 避免使用 WinMods，这些仅为微软计算机设计的调制解调器。它们比普通调制解调器便宜，因为它们很懒（或者聪明，取决于你怎么看），并且依赖操作系统为它们完成大部分工作。Linux 驱动程序现在可以做到。

### 使用 Microsoft Windows 或 Red Hat Linux 实用程序寻找调制解调器

（注：此处原文文本似乎在标题后仅有图片，根据指令未翻译图片后续的占位符或未翻译内容，但保留了结构）

（注：由于原文中该段后没有具体文本，翻译已根据上下文逻辑处理，此处仅保留了标题翻译，对应的图片占位符按要求未翻译。）

- 6. 输入您的 ISP 用户名。

- 7. 输入您的 ISP 用户名密码。如图 6-3 所示。

- 8. 点击“自定义”(Customize)。将出现更详细的 PPP 配置显示。点击任何选项卡以查看更多信息。您通常不需要修改任何设置，但如果您需要，也可以进行修改。

- 9. 点击“连接”(Connect)。您的调制解调器将拨号您的 ISP，建立连接并协商登录过程。登录后，您的 Red Hat Linux 终端将连接到互联网。

- 10. 点击“接受”(Accept) 保存您的 PPP 配置，然后点击“退出”(Quit)。

- 11. 点击屏幕左下角的“退出”(Quit)。几秒钟后更改将生效；点击屏幕中间的“激活更改”(Activate changes)按钮。linuxconf 退出。

您的设置已保存并准备好使用。

## 激活连接

您可以使用 `linuxconf` 再次开启您的 PPP 连接，如“设置您的 PPP (ISP) 连接”节中的第 9 步所述。
