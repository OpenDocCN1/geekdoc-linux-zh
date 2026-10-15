
编辑此文件最简单的方法是按 `Alt-F2`，这将弹出运行命令对话框。输入以下命令：

```
gksudo "edit /opt/ltsp/i386/etc/lts.conf"
```

点击确定将弹出一个编辑窗口。确保 `lts.conf` 文件中至少有一个 `[default]` 章节，你可以在其中添加以下行：

```
SOUND=True
```

Dapper 6.06 LTS 对 `SOUND=True` 语句非常严格。你必须完全按照所示所示输入，并特别注意大写字母等细节。

对于所有 6.10 版本的 Edubuntu，这些已经为你完成了，音频应该可以在客户端上开箱即用。

## 通过 LTSP 打印

在 LTSP 环境中实现打印有两种方法。第一种方法是将打印机直接连接到服务器。在这种情况下，按照通常的方式设置打印。你可以在第 4 章中找到更多详细信息。

允许打印的另一种方法是将一台工作站作为打印服务器。此功能在 Ubuntu Edgy 6.10 中引入。通过并行端口和 USB 端口，工作站最多连接三台打印机。LTSP 使用工作站上的 `jetpipe` 程序从服务器重定向到工作站。必须对工作站上的 `/opt/ltsp/i386/etc/lts.conf` 进行更改。该文件是某些配置选项的示例。

```
[00:4C:69:73:61:00]
PRINTER_0_DEVICE = /dev/lp0
PRINTER_1_DEVICE = /dev/usb1p0
```

这将导致 `jetpipe` 程序作为后台进程运行，并打开 9100 和 9101 端口，它将在那里监听来自服务器的打印流。该流随后将重定向到连接在计算机并行端口上的打印机。

在此示例中，我们使用客户端的 MAC 地址在网络上识别它。除非你知道计算机所连接的客户端的 MAC 地址，否则你需要运行以下命令来查找它。当客户端启动时，它会在登录屏幕右下角显示其 IP 地址。只需将以下代码中的 `<ip>` 替换为该 IP 地址即可找到客户端的 MAC 地址。

```
IP=<ip>; ping -c1 $IP | grep "NULL"; arp -a | grep $IP
```

这是一个示例：

```
pete@ubuntu:~$ IP=192.168.16.5; ping -c1 $IP | grep "NULL"
pete@ubuntu:~$ arp -a | grep $IP
? (192.168.16.5) at 00:12:50:30:5A:E5 [ether] on eth0
pete@ubuntu:~$
```

只需要在服务器上创建打印队列，以便客户端知道打印机的存在。这可以按照第 4 章所示的通常打印机的方式进行。`jetpipe` 程序允许工作站打印机被识别为 HP JetDirect 系统。要向服务器添加打印机，你需要输入工作站的 IP 地址以及 `jetpipe` 服务监听的端口。连接到工作站的第一台打印机将使用端口 9100，第二台使用 9101，第三台使用 9102。

## 在 Eduntu 中使用其他窗口管理器

在 Eduntu 中使用其他窗口管理器很容易。从 Edubuntu Edge 6.10 开始，添加窗口管理器将导致选择一个新的选项。

如果你知道有更新版本的内核可用并且知道包名，那么下一步就很简单了。如果你不知道是否有新内核并想检查一下，请按照以下步骤操作。

你首先需要找到当前安装了哪个内核镜像。执行以下命令将得到类似下方的输出。请记住，你必须在 chroot 环境中运行这些命令；否则你看到的将只是主服务器的内核版本，而不是客户端 chroot 环境中的版本。

```
root@ubuntu:~~$ dpkg -l | grep linux-image
  linux-image-2.6.24-12-generic      2.6.24-12.22
  Linux kernel image for version 2.6.24 on x86
  linux-image-generic               2.6.24.12
  Generic Linux kernel image
root@ubuntu:~-$
```

从这里我们可以看到 Linux 内核镜像的最新版本是 2.6.24-12.2。运行以下命令可以显示存储库中内核的最新版本是什么。再次提醒，在执行此命令时你应该处于 chroot 环境中。

```
root@ubuntu:~$ apt-cache show linux-image-2.6.24-12-generic \
| grep Version
Version: 2.6.24-12.22
root@ubuntu:~-$
```

注意上一个代码输出中的包名 `linux-image-2.6.24-12-generic` 现在再次用于第二个命令，以查找当前已安装内核的最新版本。在这个示例中，两个内核版本是相同的。但是，如果它们不同，使用以下命令将更新 chroot 环境中的内核版本。

```
apt-get install linux-image-2.6.24-12-generic
```

内核升级后，你必须运行运行 LTSP 脚本来用正确的信息更新 chroot，以便允许新内核优于旧内核使用。要执行此操作，首先像之前一样卸载 `proc`，然后按 `Ctrl-D` 退出 chroot。然后运行以下命令：

```
ltsp-update-kernels
```

## 控制和管理用户桌面

脚本完成后，你应该重启客户端机器，以便它们开始使用新内核。

在之前的示例中，在管理 LTSP chroot 时，注意不需要 `sudo` 命令。这是因为在使用 `sudo chroot` 命令时，我们会自动获得该环境内 root 用户的身份。所以请留心！

## Thin Client Manager

Thin Client Manager 起于 Dapper 6.06 版本中的 Student Control Panel（学生控制面板），由 Oliver Grawert 编写。它在 6.10 中进行了重构和功能增强，并在 7.04 中由 Pete Savage 和 Oliver Grawert 再次改进。Thin Client Manager 现在提供了许多你在商业网络管理包中可以找到的功能。它专门为管理和维护 LTSP 客户端环境而设计，提供了以下功能：

- 停止客户端机器上的进程。
- 注销用户会话。
- 向用户发送消息。
- 在客户端屏幕上运行应用程序。
- 清空或锁定用户屏幕。
- 使用 Pessulus 锁定客户端。
- 将用户添加到组以便于过滤。
- 使用插件框架执行简单任务。

### 使用 Thin Client Manager

首次加载 Thin Client Manager 时，你将看到一个与图 9-16 所示类似的屏幕。屏幕基本上分为两个部分。左侧是用户列表，显示所有登录到 LTSP 服务器用户的动态更新列表。右侧第二个部分包含进程视图（Process View）。

# LTSP 故障排除

旨在提供一些关于如何诊断和修复常见 LTSP 问题的有用提示。LTSP 官方网站 `www.ltsp.org` 拥有一个庞大的 wiki 和知识库，可以帮助您找到解决 LTSP 问题的答案。

## 计算机未获取 IP 地址

如果您的客户端没有接收到 IP 地址，很可能是 DHCP 服务器出了问题。为了检查这一点，您必须加载终端窗口并运行以下命令：

```
pidof dhcp3 2&> /dev/null && echo OK
```

如果显示结果为正常，那么问题出在其他地方。如果结果显示 DHCP 服务器未运行，那么是时候检查 DHCP 日志中的错误了。要做到这一点，您必须重启 DHCP 服务器并查看日志。使用以下命令重启服务器：

```
sudo /etc/init.d/dhcpd-server restart
```

如果在在此阶段您在启动 DHCP 服务器时看到 FAIL 消息，那么 `dhcpd` 配置一定存在问题。按照所示的方法检查日志将引导您找到问题。您可以通过运行以下命令查看 `dhcpd` 服务器最后的错误：

```
tail /var/log/daemon.log
```

使用此方法可以显示各种问题，在您对问题有了更好的了解后，您可能自己解决它。您也可以通过本章末提供的信息联系 Edubuntu 团队寻求帮助。

## NFS 服务器未响应

如果您的客户端显示类似于 `nfs warning: server not responding` 的错误，可能是内核对 NFS 数据包使用了过大的块大小。本质上，内核使用 32K 的块大小，这必须被分解为 1500 字节的数据报。由于这会导致发送大量小数据报，客户端在接收所有数据之前可能会超时。幸运的是，修复方法非常简单。

您必须加载文件 `/var/lib/tftpboot/ltsp/pxelin.cfg/default` 以进行编辑。要做到这一点，可以使用在本章之前描述的任何方法。打开文件后，有一行以 `APPEND;` 开头；您必须在该行的末尾添加以下内容之一：

```
NFSOPTS="- nolock,ro,wsize=2048,rsize=2048"
```
