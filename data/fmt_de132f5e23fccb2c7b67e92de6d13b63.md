
> 你可以在流行的开源软件网站上（如 [www.linuxalt.com](http://www.linuxalt.com)）搜索流行的 macOS 或 Windows 程序的 Linux 等效程序。

> 除了运行在操作系统上的软件外，其他几个特征也区分了操作系统，例如用户账户的细节、磁盘文件命名规则以及计算机如何启动的技术细节。这些特征都由操作系统的软件部分控制，有时由内核控制，有时由非内核软件控制。

## 调查用户界面

之前，我们注意了文本模式和图形用户界面的区别。尽管大多数用户为了易用而喜欢 GUI，但 Linux 保留了强大的文本模式传统。第 5 章将详细描述 Linux 的文本模式工具，而第 4 章“常用 Linux 程序”涵盖了 GUI 操作的基本原理。现在掌握文本模式和图形用户界面的基础知识是重要的，因为界面问题会在中间章节中偶尔出现。

## 使用文本模式用户界面

在过去，有时今天，Linux 计算机也会引导进入文本模式。系统完全启动后，屏幕将显示一个简单的文本模式登录提示，可能如下：

```
Fedora 30 (Workstation Edition)
Kernel 5.0.9-301.fc30.x86_64 on an x86_64 (tty1)
login:
```

> 要尝试文本模式登录，你必须先在计算机上安装 Linux。Linux Essentials 考试本书都不涵盖安装；请咨询你的发行版文档了解更多

此类登录提示的细节在不同系统之间不同。此示例包含了若干信息：

- OS 名称和版本：`Fedora Linux 30`
- 计算机名称：`essentials`
- 用于登录的硬件设备：`tty1`
- 登录提示本身：`login:`

> 如果看到 GUI 提示，可以通过按下 `Ctrl+Alt+F2` 或 `Ctrl+Alt+F3` 获取文本模式提示。按下 `Ctrl+Alt+F1` 或 `Ctrl+Alt+F7` 返回 GUI 登录提示。

登录此类系统时，需要在登录提示处输入用户名。系统提示输入密码。如果你输入有效的用户名和密码，计算机可能会显示登录信息，然后是 shell 提示符：

```
rich@essentials:~$
```

在本书中，当命令单独成行时，我们会省略命令的大部分提示符。然而我们会保留美元符号（`$`）提示符，表示普通用户命令。某些命令必须以 `root` 身份输入用户账户，即 Linux 管理员用户。对于此类命令，我们将提示符更改为井号（`#`），因为大多数 Linux 发行版都会对 `root` 用户的提示符进行类似的更改。

# 第 13 章“创建用户和组”更详细地介绍了 Linux 账户，包括 `root` 用户账户。

Shell 提示符的细节因安装版本而异，但你可以在 shell 提示符处输入文本模式命令。例如，你可以输入 `ls`（list 的缩写）来查看当前目录下的文件列表。最基本的命令可以通过删除元音（有时还有辅音）来缩短，以尽可能地减少执行命令所需的打字量。但这带来的遗憾副作用是让许多命令变得相当晦涩。

有些命令不显示任何信息，但大多数命令会产生某种输出。例如，`ls` 命令会生成文件列表：

```
$ ls
chapter01.doc figure01.png
```

此示例显示了当前目录下的两个文件：`chapter01.doc` 和 `figure01.png`。你可以使用额外的命令来操作这些文件，例如使用 `cp` 复制它们或使用 `rm`（删除）它们。第 5 章（熟悉命令行）和第 7 章（管理文件）描述了一些常用的文件操作命令。

某些文本模式程序会接管显示器，以提供持续更新或允许你灵活地与数据交互。例如，图 1.1 显示了 `nano` 编辑器，它在第 10 章“编辑文件”中有更详细的描述。当 `nano` 工作时，你可以使用键盘上的方向键移动光标，通过输入添加文本等。

```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/var/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
np:x:7:7:np:/var/spool/lp:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/nologin
uuc:x:9:9:uuc:/var/uu:/usr/sbin/nologin
sync:x:10:10:sync:/bin:/bin/sync
ucp:x:11:11:ucp:/var/spool/ucp:/usr/sbin/nologin
backup:x:12:12:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:list:/var/list:/usr/sbin/nologin
data:x:39:39:data:/var/lib:/usr/sbin/nologin
message:x:40:40:message:/var/spool/news:/usr/sbin/nologin
gnatsd:x:41:41:gnatsd:/var/lib/gnatsd:/usr/sbin/nologin
system:x:42:42:system:/system:/usr/sbin/nologin
system-교:x:43:43:system-교:/dev/system:/usr/sbin/nologin
bus:x:44:44:bus:/var/cache/bus:/usr/sbin/nologin
ircd:x:45:45:ircd:/var/run/ircd:/usr/sbin/nologin
polkit:x:46:46:polkit:/var/lib/polkit:/usr/sbin/nologin
gud:x:47:47:gud:/var/lib/ud:/usr/sbin/nologin
systemd-network:x:48:48:systemd-network:/var/lib/systemd-network:/nologin
systemd-bus:x:49:49:systemd-bus:/var/lib/systemd:/nologin
systemd-proxy:x:50:50:system-proxy:/var/lib/system-proxy:/usr/sbin/nologin
syslog:x:51:51:syslog:/var/log:/usr/sbin/nologin
avahi:x:52:52:avahi:/var/cache/avahi:/usr/sbin/nologin
pd-network:x:53:53:ppd-network:/var/cache/ppd-network:/usr/sbin/nologin
apt:x:54:54:apt:/var/cache/apt:/usr/sbin/nologin
ssdd:x:55:55:sdd:/var/lib/sdd:/usr/sbin/nologin
lightdm:x:56:56:lightdm:/var/lib/lightdm:/usr/sbin/nologin
network:x:57:57:network:/var/cache/network:/usr/sbin/nologin
avahi-manager:x:58:58:avahi-manager:/var/lib/avahi:/usr/sbin/nologin
avahi-daemon:x:59:59:avahi-daemon:/var/lib/avahi:/usr/sbin/nologin
messaged:x:60:60:messaged:/var/lib/messaged:/usr/sbin/nologin
dbus:x:61:61:dbus:/var/lib/dbus:/usr/sbin/nologin
geome:x:62:62:geome:/var/lib/geome:/usr/sbin/nologin
polkit:x:63:63:polkit:/var/lib/polkit:/usr/sbin/nologin
sdd-dispatcher:x:64:64:sdd-dispatcher:/var/lib/sdd-dispatcher:/usr/sbin/nologin
pulse:x:65:65:pulse:/var/run/pulse:/usr/sbin/nologin
```
