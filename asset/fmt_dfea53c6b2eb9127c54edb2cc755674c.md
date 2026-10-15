
```bash
smbclient //naba-dell-4400/Share password
added interface=192.168.0.2 bcast=192.168.0.255 nmask=255.255.255.0
Got a positive name query response from 192.168.0.4 ( 192.168.0.4 )
Domain-[LNB SOFTWARE] OS-\[Windows 5.1\ Server-\[Windows 2000 LAN Manager]
smb: \> dir
    DA        0 Sun Jan 12 15:47:36 2003
    DA        0 Sun Jan 12 15:47:36 2003
    Ashley    DA        0 Nov 23 11:32:04 2002
    bookmark.htm  A 117485 Sun Jun 23 13:48:22 2002
    brother-mfc-10-22-02.rms A 132633 Tue Oct 22 18:31:36 2003
    lines deleted...
    Photos                0 Mon Jan 6 19:54:54 2003

    38154 blocks of size 209152. 30719 blocks available
```

```bash
smb: \> quit
```

要查看 `smbclient` 命令列表，请在提示符处使用 `help`。表 19-2 是对许多常用 `smbclient` 命令的简要总结。为了熟悉 `smbclient`，请尝试执行尽可能多的这些命令。

# 表 19-2：常用 smbclient 命令

| 命令 | 说明 |
|---|---|
| ! | 执行 shell 命令（记住你是在 Linux 上运行 `smbclient`） |
| ? cmd | 显示命令列表或特定命令的帮助信息 |
| cancel id | 取消由 ID 标识的打印作业 |
| cd dir | 更改远程目录 |
| del file | 删除指定的文件 |
| dir file | 显示目录列表 |
| exit | 登出 Windows 服务器 |
| get rfile lfile | 将远程文件 (rfile) 复制到本地文件 (logfile) |
| help cmd | 提供命令的帮助（或显示命令列表） |
| lcd newdir | 更改本地目录（在 Linux PC 上） |
| lowercase | 切换执行命令时文件名自动转为小写的开关状态 |
| ls files | 列出服务器上的文件 |
| mask name | 对所有文件操作应用掩码（如 *.c） |
| md dirname | 在服务器上创建目录 |
| mget name | 获取所有匹配名称（如 *.doc）的文件 |
| mkdir dirname | 创建目录 |
| mput name | 将文件从 Linux PC 复制到服务器 |
550 第三部分：使用 Red Hat Linux 进行网络连接

| 表 19-2：（续） |
| 命令 | 说明 |
| --- | --- |
| newer file | 仅获取比指定文件新的文件 |
| print name | 打印指定的文件 |
| printmode mode | 设置打印模式（模式必须是文本或图形） |
| prompt | 切换提示符模式（类似于 ftp 中的命令） |
| put l rfile | 将本地文件 (lfile) 复制到远程文件 (rfile) |
| queue | 显示打印队列 |
| quit | 登出 Windows 服务器 |
| rd dir | 删除服务器上的指定目录 |
| recurse | 在文件获取和放置操作期间切换目录递归开关状态 |
| rm name | 删除所有文件 |
| rmdir dir | 删除指定的目录 |
| translate | 转换字符 |

## 第20 章：高级系统管理

当前的运行级别（run level）以及 `/etc/inittab` 文件的内容控制着哪些进程的启动。例如，Red Hat Linux 有七个运行级别：0, 1, 2, 3, 4, 5 和 6。按照惯例，其中某些级别表示在特定级别下运行的特定进程。例如，运行级别 1 表示单用户独立系统。运行级别 0 意味着系统停止，运行级别 6 意味着系统重启。运行级别 2 到 5 是具有不同能力水平的多用户模式，但运行级别 4 目前没有使用。

`init` 在每个运行级别执行特定的 shell 脚本序列。这些脚本通常被称为初始化脚本（initscripts），因为它们是由 `init` 执行的。

要检查当前的运行级别，请输入 `runlevel` 命令（如果没有以 root 用户登录，请输入 `/sbin/runlevel`）。以下是 `runlevel` 的典型输出：

```
+ - 5
```

输出的第一个字符显示上一个运行级别（N 表示没有上一个运行级别），第二个字符显示当前级别（5），表示系统当前处于运行级别 5。

默认运行级别对于文本模式登录会话为 3，对于图形登录界面为 5。`/etc/inittab` 文件带有 `defaultaction` 的行会激活默认运行级别。以下是 `/etc/inittab` 文件中将默认运行级别设置为 5 的行：

```
id:5:initdefault:
```

如果您将 5 改为 3，系统将启动到文本模式登录界面。

在急于编辑 `/etc/inittab` 文件之前，您应该尝试使用 `init` 命令来测试运行级别。例如，切换到运行级别 3，以 root 身份登录并输入以下命令：

```
init 3
```

### 检查 /etc/inittab 文件

`/etc/inittab` 文件是理解在各种运行级别下启动的进程的关键。您可以使用 `more` 命令查看文件内容，如下如下：

```
more /etc/inittab
```

使用 `more` 命令查看 `/etc/inittab` 文件的内容时，不需要以 root 用户登录。

以下是您的 Red Hat Linux 系统上 `/etc/inittab` 文件的列出，该文件配置为图形登录界面：

```
+ - inittab 此文件描述了 INIT 进程应如何在特定运行级别下设置系统。

- Author: Miquel van Smoorenburg, <miquel@drinking.nl.org> Marc Ewing 和 Donnie Barnes 为 RHS Linux 修改

+ # 默认运行级别。RHS 使用的运行级别为：

# 0 halt（不要将 initdefault 设置为此级别）

# 1 单用户模式

# 2 多用户模式，不带 NFS（如果没有网络，则与 3 相同）

# 3 完整多用户模式

# 4 未使用

# 5 GUI

# 6 reboot 重启（不要将 initdefault 设置为此级别）

id:5:initdefault:

+ # 系统初始化。

si::sysinit:/etc/rc.d/rc.sysinit

10:wait:/etc/rc.d/rc 0

11:wait:/etc/rc.d/rc 1

12:wait:/etc/rc.d/rc 2

13:wait:/etc/rc.d/rc 3

14:wait:/etc/rc.d/rc 4

15:wait:/etc/rc.d/rc 5

16:wait:/etc/rc.d/rc 6

+ # 捕捉 CLR-ALT-DELETE

ca::ctrlaltdel:/sbin/shutdown -t3 -r now

+ # 当我们的 UPS 我们断电时，假设我们还有几分钟电源。安排在 2 分钟后关机。

# 当然，这假设你已经安装了电源并且你的

# UPS 连接并正常工作。

p:powerfail:/sbin/shutdown -f -h +2 "Power Failure: System Shutting Down"

+ # 如果关机触发之前恢复了电源，则取消。

pr:12345:powerokwait:/sbin/shutdown -c "Power Restored, Shutdown Cancelled"

+ # 在运行级别中运行 gettys

1:2345:respawn:/sbin/mingetty tty1

2:2345:respawn:/sbin/mingetty tty2

3:2345:respawn:/sbin/mingetty tty3

4:2345:respawn:/sbin/mingetty tty4

5:2345:respawn:/sbin/mingetty tty5

6:2345:respawn:/sbin/mingetty tty6

+ # 在运行级别 5 中运行 xdm

# xdm 现在是一个独立的服务
```
