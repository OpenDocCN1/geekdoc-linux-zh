
![](img/c00dda504be4d70c6e7dd488ae0af42a_235_0.png)

# 别忘记 IPTABLES

记得我们之前必须告诉 `IPTables` 允许连接进入我们的基础 Web 服务器吗？猜猜看……端口 `443` 是 HTTPS 端口，所以我们需要将该添加到 `IPTables` 权限中并保存以备后用。

```
[root@local]# iptables
-I INPUT 1 -p tcp -m state
-state NEW --dport 443 -j ACCEPT
[[root@local]# iptables-save
> /etc/sysconfig/iptables
```

这就完成了。我们现在可以在浏览器中通过 HTTPS 连接访问我们的服务器了。当然，我们预计它会抱怨证书不是由 CA 颁发的（见右侧）。

我们可以通过点击浏览器中相应的链接来检查证书信息——在我们的示例中，它确实显示了我们几页前创建证书时输入的详细信息。点击警告我们就进入了。

![](img/c00dda504be4d70c6e7dd488ae0af42a_236_0.png)

上方：浏览器将弹出安全警告

![](img/c00dda504be4d70c6e7dd488ae0af42a_236_1.png)

上方：检查证书是否正确

![](img/c00dda504be4d70c6e7dd488ae0af42a_236_2.png)

上方：我们的页面现在受 SSL 保护。

![](img/c00dda504be4d70c6e7dd488ae0af42a_237_0.png)

![](img/c00dda504be4d70c6e7dd488ae0af42a_238_0.png)

# 出现问题时该怎么办

当然，总会有某个时刻出现问题。Linux 通常是一个非常稳定的平台，但始终存在问题的可能性——也许是硬件罢工，但更有可能是用户人为造成的（我们稍后会回到这一点）。做一些愚蠢的事情并破坏系统配置导致其停止工作并不罕见，那么当问题出现时我们该怎么办呢？

# 如果你无法远程登录

Linux 最常见的问题是机器正在运行，但你无法通过 SSH 或其他工具从远程机器登录。这可能有许多原因：网线故障；机器丢失了 IP 设置；系统没有正确启用网卡；网络配置问题（例如身份验证更改了机器设置，导致不再匹配）；`IPTables` 配置将你锁定在外面；或者其他许多问题。

![](img/c00dda504be4d70c6e7dd488ae0af42a_239_0.png)

![](img/c00dda504be4d70c6e7dd488ae0af42a_240_0.png)

答案是尝试从机器本身的控制台登录。如果你无法以普通用户登录，请点击登录屏幕上的“root”链接并尝试以 root 用户身份登录。

# 如果系统启动但未完成

更常见的情况是系统启动到一半就停止了。这通常是由于某些错误导致文件系统无法挂载，或者显示出“内核恐慌”（kernel panic）信息。这是由于磁盘损坏或强制关机导致的。在正常关机的情况下，Linux 比强行关机更健壮且具有恢复性。

如果发生这种情况，我们可以尝试进入单用户模式（single mode）启动。你可以通过以下方式操作：

- 在启动屏幕上按 `e` 来编辑命令。
- 找到包含 `linux` 的那行。
- 在行末尾添加 `single`。
- 按 `Ctrl+X` 启动。

进入单用户模式后，我们可以修复文件系统：

```
root@local]# fsck -y /dev/sda1
```

修复后，重启系统即可。

在某些情况下，Linux 是非常宽容的。例如，你可能会认为如果你使用 SSH 连接到机器并停止 SSH 服务进程，它将会将你踢出去，但事实并非如此：

```
[root@dc-linux ~]# systemctl stop sshd
[root@dc-linux ~]# ls
anaconda-ks.cfg Desktop Documents Downloads initial-setup-ks.cfg Music Pictures
```

在这里，我们杀掉了 SSH 服务器，但它允许我们的会话继续。不过，如果我们断开连接并尝试重新连接，它会如预期地拒绝我们的连接：

![](img/c00dda504be4d70c6e7dd488ae0af42a_245_0.png)

![](img/c00dda504be4d70c6e7dd488ae0af42a_246_0.png)

## 小贴士

如果你的 Linux 图形桌面冻结了，最好的办法是按下 `Ctrl + Alt + F2` 切换到控制台。这将允许你从控制台登录并找到导致桌面冻结的原因。

```
[root@dc-linux ~]# exit
[dsc-dc-linux ~]$ exit
Connection to 192.168.1.186 closed.
DCPro:~ davidcartwright$ ssh dsc@192.168.1.186
ssh: connect to host 192.168.1.186 port 22: Connection refused
DCPro:~ davidcartwright$
```

然而，对于其他配置项，你可能就不会那么幸运。因此，在远程重新配置系统时要务必极其小心。保持一个开启的连接以防万一，并且如果控制台位置较远，要有一个进入控制台的备用方案，因为我们职业生涯中的某个时刻都曾见过“锯掉自己正坐着的树枝”的情况。

# 术语表

**Apache**: 这是开源软件真正影响业务的地方。它是最广泛使用的 Web 服务器软件，占据了约 40% 的市场。它是开源开发的巅峰，由一群开发者维护，并由 Apache 软件基金会支持。

**Bloatware（臃肿软件）**: 不必要的程序和应用程序，或者内存和磁盘空间占用远超其需求的软件。特别指随操作系统一起交付的软件。

**BSD**: Berkeley Software Distribution（伯克利软件发行）的缩写。Linux 最早的实现之一，根源于 Unix。

**Bash**: 简单来说，它是将你的 CLI 命令转换并对其进行处理的程序之一。换句话说，它处理 Linux 命令，但它本身并不是 CLI。

**Compile（编译）**: 将源代码转换为可执行内容的艺术。程序员们经常使用这个词，但新手通常不会做很多编译。

**Copyleft（反向许可）**: 开源版的版权的等价物。它明确表示源代码可以自由地分发、修改和随意摆弄。

**CLI**: Command Line Interface（命令行界面）：你最初向计算机输入那些 Linux 指令的方式。曾经，所有的计算机都使用这种界面，后来我们发现了 GUI（图形用户界面）。

**CUPS**: Common Unix Printing System（通用 Unix 打印系统）。顾如名，这是一个打印实用，帮助 Linux 成为打印服务器并允许 Linux 与打印机通信。

![](img/c00dda504be4d70c6e7dd488ae0af42a_247_0.png)

**Daemon（守护进程）**: 与菲利普·普尔曼和《黑暗物质》无关，而是一种在后台运行以处理特定计算机请求的特殊程序。

**Debian**: 最早的 Linux 发行版之一。许多发行版都诞生于 Debian 的影子下。

**Distro（发行版）**: distribution 的缩写，赋予 Linux 不同变体的名称。市面上有很多发行版，几乎不可能列全。这是你在 Linux 世界中听到的最常用术语之一。

**Emacs**: 一个 Linux 编辑器。

**Fedora**: 由 Fedora 项目开发并由红帽支持的 Linux 发行版。Linus Torvalds 本人使用的 Linux 版本。

**Fork（分支）**: 这是开源开发中一个既定的部分，一种源自 Unix 的技术，通过复制并修改一个进程来创建一个完全不同的进程。有时分叉会产生如此显著的区别。

**FOSS**: Free and Open Source Software（自由开源软件）。它是“免费”与“软件”之间的一种折中，并且是开放修改的。

**Gimp**: 为想要 Photoshop 替代品的用户提供的照片处理程序。

**GitHub**: 一个用于软件的 Web 仓库。程序员在那里下载软件、进行修订并提供更改。

**Gnome**: 一个图形桌面环境；是你启动计算机时出现在屏幕上的图标、小部件、文件夹和工具栏集合。这两个产品根源非常不同（尽管都源自 Unix 世界）；Gnome 是作为一个项目开始的，而 KDE 设计的目标是尽可能高效。

**GPL Licence**: 代表 General Public Licence（通用公共许可证）。严格来说，GPL 许可证已成为被接受的术语（就像我们谈论 ATM 一样），指反向许可，任何修改都必须对其施加一套新的条件。

**GNU Project**: 非常自由软件项目之一，由理查德·斯托曼启动。Linux 是在 GNU 许可证下发布的（尽管该项目本身不是）。
