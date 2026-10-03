
> acpio: <PLITD RSDT> on motherboard
> acpibo: <ACPI Host-PCI bridge> port 0xcf8-0xcff on acpio
> acpcio: <ACPI PCI bus> on pcpibo
> acpio: <PLITD RSDT> on motherboard
> acpibo: <ACPI Host-PCI bridge> port 0xcf8-0xcff on acpio
> acpcio: <ACPI PCI bus> on pcpibo
> acpio: <PLITD RSDT> on motherboard
> acpibo: <ACPI Host-PCI bridge> port 0xcf8-0xcff on acpio
> acpcio: <ACPI PCI bus> on pcpibo
> acpio: <PLITD RSDT> on motherboard
> acpibo: <ACPI Host-PCI bridge> port 0xcf8-0xcff on acpio
> acpcio: <ACPI PCI bus> on pcpibo
> acpio: <PLITD RSDT> on motherboard
> acpibo: <ACPI Host-PCI bridge> port 0xcf8-0xcff on acpio
> acpcio: <ACPI PCI bus> on pcpibo
> acpio: <PLITD RSDT> on motherboard
> acpibo: <ACPI Host-PCI bridge> port 0xcf8-0xcff on acpio
> acpcio: <ACPI PCI bus> on pcpibo
> acpio: <PLITD RSDT> on motherboard
> acpibo: <ACPI Host-PCI bridge> port 0xcf8-0xcff on acpio
> acpcio: <ACPI PCI bus> on pcpibo
> acpio: <PLITD RSDT> on motherboard
> acpibo: <ACPI Host-PCI bridge> port 0xcf8-0xcff on acpio
> acpcio: <ACPI PCI bus> on pcpibo
> acpio: <PLITD RSDT> on motherboard
> acpibo: <ACPI Host-PCI bridge> port 0xcf8-0xcff on acpio
> acpcio: <ACPI PCI bus> on pcpibo
> acpio: <PLITD RSDT> on motherboard
> acpibo: <ACPI Host-PCI bridge> port 0xcf8-0xcff on acpio
> acpcio: <ACPI PCI bus> on pcpibo

在接下来的章节中，我们将检查 `/etc/rc.conf` 中的常见条目。这些条目都出现在 `/etc/defaults/rc.conf` 中，并且可以通过在 `/etc/rc.conf` 中放置覆盖项来编辑。每个变量都带有其默认设置出现。

## 启动选项

以下 `rc.conf` 选项控制 FreeBSD 如何配置和启动其他程序。这些深远的设置会影响所有其他系统程序和服务的运行方式。

如果您在启动脚本本身遇到问题，可以对 `/etc/rc` 及其子脚本启用调试功能。这可以提供关于脚本为何运行或未运行的额外信息。

```
rc_debug="NO"
```

如果您不需要完整的调试输出，但想获取关于 `/etc/rc` 过程的一些额外信息，可以通过 `rc_info` 启用信息性消息：

```
rc_info="NO"
```

内存较小的系统经常遇到的的一个问题之一是交换空间不足。我们将在第 19 章详细讨论交换空间的使用，但您可以在启动时立即配置一个文件作为额外的交换空间使用：

```
swapfile="NO"
```

## 文件系统选项

FreeBSD 可以将内存作为文件系统，正如我们在第 8 章中讨论的那样。该功能的一个常见用途是使用内存而非硬盘作为后端使 `/tmp` 变得非常快。一旦您实现了这一点，`rc.conf` 允许通过变量来启用内存支持的 `/tmp` 并透明且简便地设置其大小。您还可以选择 FreeBSD 用来完成文件系统所需的选项（你们中急躁的人可能在想 `-S` 是什么意思。它禁用了软更新 soft updates。如果您不知道这意味着什么，请等第 8 章。）如果您想使用内存文件系统 `/tmp`，请将 `tmpfs` 设置为 YES 并设置您所需的 `/tmp` 大小。

```
tmpfs="AUTO"
tmpsize="20m"
tmpfs_flags="-S"
```

FreeBSD 的另一个流行特性是其集成的加密分区。FreeBSD 出箱即支持两种不同的文件系统加密系统：GBDE 和 GELI。基于几何的磁盘加密 (GBDE) 是 FreeBSD 第一个为军事级用途设计的加密文件系统。GELI 则比 GBDE 更友好一点，并且符合不同的标准。（在启用其中任何一个之前，您绝对想要阅读第 18 章！）

```
gbde_autoattach_all="NO"
gbde_devices="NO"
gbde_attach_attempts="3"
gbde_lock="/etc"
geli_devices=""
geli_tries=""
geli_default_flags=""
geli_autodetect="YES"
geli_swap_flags="-aes -l 256 -s 4096 -d"
```

默认情况下，FreeBSD 在进入多用户模式后会将根分区挂载为读/写。如果您想以只读模式运行，可以将变量设置为 NO。许多人认为这样更安全，但可能会干扰某些软件的操作，并且它会阻止您编辑根分区上的任何文件！

```
root_rw_mount="YES"
```

当 FreeBSD 启动尝试挂载其文件系统时，它会检查初始的不一致性。如果内核发现严重的文件系统问题，它可以使用 `fsck -y` 自动修复。虽然这在某些情况下是必要的，但并不是完全安全的。（在启用此项之前，请务必仔细阅读第 8 章！）

```
fsck_y_enable="NO"
```

内核可能会发现细微的文件系统问题，并在系统运行于多用户模式时，通过后台 `fsck` 即时解决它们，正如第 8 章所述。在某些情况下，对该功能的安全性存在合法的担忧。您可以控制后台 `fsck` 的使用，并设置系统在开始后台 `fsck` 之前等待多久。

```
background_fsck="YES"
background_fsck_delay="60"
```

## 其他网络守护进程

FreeBSD 包含了许多在后台运行的较小程序（或守护进程），以提供特定的服务。我们将在整书中涵盖许多此类集成服务，但这里有几个对经验系统管理员感兴趣的特定服务。

`daemon` 是 `syslogd(8)`。日志是一件好事。日志是非常、非常好，以至于第 20 章的大部分内容都用于在 FreeBSD 上、使用 FreeBSD 以及关于 FreeBSD 的日志的主题。

```
syslog_enable="YES"
```

一旦您决定运行日志守护进程，您可以通过为它设置命令行标志来精确选择它的运行方式。FreeBSD 在启动守护进程时将使用这些标志。对于 `rc.conf` 中包含的所有可以接受命令行标志的程序，这些标志按格式给出。

```
syslogd_flags="-s"
```

另一个流行的守护进程是 `inetd(8)`，小型网络服务的服务器。（我们在第 15 章涵盖了 inetd。）

```
inetd_enable="NO"
```

FreeBSD 经常运行的一项工作是域名系统 (DNS)，使用行业标准的守护进程 `named(8)`。DNS 是互联网的路线图，让更多人类使用网络成为可能。由于 DNS 必须配置后可用，FreeBSD 默认禁用了它。我们在第 14 章涵盖了 DNS。

```
named_enable="NO"
```

大多数设施都使用 Secure Shell (SSH) 守护进程进行远程登录。如果您想通过网络远程连接到您的系统，您几乎需要 SSH 服务。

```
sshd_enable="NO"
```

虽然 SSH 守护进程可以通过命令行进行配置，但通常情况下使用 `/etc/ssh/` 中的配置文件会更好。见第 15 章。

```
sshd_enable="NO"
```

网络控制设备（如防火墙）必须在不同接口之间传递流量。虽然 FreeBSD 默认不会执行此操作，但开启它非常简单。只需告诉系统它是一个网关，它就会为你连接多个网络。

```
gateway_enable="NO"
```

如果你的系统需要运行路由信息协议（RIP），请使用 `router_enable` 旋钮在启动时开启它。我认为这个开关的命名有误导——许多路由器使用 RIP 以外的协议，但几十年来这个旋钮一直叫这个名字。如果你并不特别需要 RIP 协议，就不要动它这个开关！

```
router_enable="NO"
```

## 控制台选项

控制台选项控制显示器和键盘的行为。你可以更改键盘语言、显示器尺寸，或任何你喜欢的其他设置。例如，键盘映射默认为标准美国键盘（通常是 QWERTY 布局）。你可以在 `/usr/share/syscons/keymaps` 目录下找到所有的键映射。我更倾向于 Dvorak 键盘布局，它有一个 `us.dvorak` 条。通过将 `keymap` 旋钮改为 `us.dvorak`，我的系统在启动到多用户模式后将使用 Dvorak 键盘。

```
keymap="NO"
```

当键盘空闲时间达到 `blanktime` 旋钮指定的时间时，FreeBSD 会变暗。如果你将其设置为 `NO`，FreeBSD 将不会调暗屏幕。请注意，新硬件在一段时间后也会调暗显示器以节省电源。如果你将 `blanktime` 旋钮设置为 `NO` 但屏幕仍然变空，请检查你的 BIOS 和显示器说明书。

```
blanktime="300"
```

FreeBSD 还可以在控制台上使用多种字体。虽然默认字体是为服务器设计的，但你可能在桌面电脑或笔记本电脑上想要不同的字体。我的笔记本有一块为看电影设计的 17 英寸屏幕，默认字体在这种尺寸下看起来很滑稽。你可以从 `/usr/share/syscons/` 目录选择新字体。尝试几种，看看它们在你的系统上的效果。字体名称包含尺寸，因此你可以设置相应的变量。例如，字体 `swiss-8x8_font` 是瑞士字体，大小为 8 像素乘8 像素。要使用它，你需要设置 `font8x8` 旋钮。

```
font816="NO"
font814="NO"
fontx8="NO"
```

你可以在控制台上使用鼠标，即使没有 GUI。默认情况下，FreeBSD 会尝试自动检测你的鼠标类型。如果你有 PS/2 或 USB 鼠标，在启用守护进程后，它很可能直接工作，无需任何特殊配置。一些较旧和特殊类型的鼠标需要手动配置，如 `moused(8)` 文档中所示。

```
moused_enable="NO"
moused_type="AUTO"
```

你还可以更改显示器的显示以适应你的硬件。如果你有一个奇特尺寸的显示器，可以更改文本行数和长度以适应，更改文本颜色，更改光标及其行为，以及各种细微调整。你可以在 `man vidcontrol(8)` 中获取不同选项的完整列表。

```
allscreens_flags=""
```

其次，你几乎可以任意调整键盘行为。从按键重复到功能键的速度，一切都可以进行配置，如 `kbdcontrol(8)` 文档所示。

```
allscreens_kbdfflags=""
```

## 其他选项

这些关于旋钮的最后描述在任何环境中可能有用也可能无用，但它们出现的频率足以提及。例如，并非所有系统都能访问打印机，但有需要的系统会想要运行 `lpd(8)` 打印守护进程。我们将在第15 章介绍打印机配置。

```
ldp_enable="NO"
```

`sendmail(8)` 守护进程管理系统之间电子邮件的发送和接收。并非所有系统都需要传输电子邮件，但 FreeBSD 机器确实需要。

```
sendmail_enable="NO"
sendmail_outbound_enable="YES"
```

FreeBSD 最有趣的功能之一是它可以运行为其他操作系统设计的软件。最常见的兼容模式是 Linux 软件，但 FreeBSD 也支持 SVR4 软件。我们在第12章讨论这一功能。

```
linux_enable="NO"
```

对于任何 Unix 类操作系统，共享库都是至关部分。FreeBSD 有一个安全配置文件，允许管理员控制基本功能。虽然默认设置通常足够，但如果你发现需要设置 `LD_LIBRARY_PATH` 环境变量，应该考虑查看第12章以获取更多信息。

```
ldconfig_paths="/usr/lib /usr/local/lib"
```

FreeBSD 有一个安全级别系统，允许控制挂载磁盘、访问特定的 TCP/IP 端口。请查看第7章以了解如何使用这些。

```
kern_securelevel="NO"
kern_securelevel="-1"
```

既然你已经知道了 FreeBSD 开箱支持的配置开关，让我们看看它们是如何使用的。

## rc.d 启动系统

FreeBSD 通过脚本 `/etc/rc` 桥接单用户模式和多用户模式。该脚本读取 `/etc/defaults/rc.conf` 和 `/rc.conf`，并根据发现的内容运行一系列脚本。例如，如果你启用了 USB 守护进程，`/rc` 会运行专门为该守护进程编写的脚本。FreeBSD 包含了启动、挂载磁盘、配置网络和设置安全参数的脚本。你可以使用这些脚本停止服务。

### 什么是 rcNG?

曾经，FreeBSD 包含一些单体脚本。每个守护进程或服务都由这些脚本启动。这对于大多数系统效果良好，但并不灵活。FreeBSD 开发了目前的微型脚本系统，或称为 rcNG。该系统是目前唯一使用的，你看到的任何对旧 rc 的引用都是遗留。

一旦你在 `rc.conf` 中启用了某个功能，你就可以通过 rc.d 脚本控制它。例如，假设你需要在以前没有运行的系统中运行 SSH 守护进程。将 ssh 设置为 YES，并进入 `/etc/rc.d` 目录。你会发现一个名为 `sshd` 的脚本。

```
# .sshd start
starting sshd.
#
```

除非在 `rc.conf` 中启用，否则任何 rc.d 脚本都不会运行。这确保了重启前运行的所有内容在重启后仍然运行。

# 4

## 在弄坏其他东西之前请先读这个！

（备份与恢复）

![](img/b00144f770bf509a54e1d770bb05a101_120_0.png)

系统故障最常见的原因是那些讨厌的人类，但硬件和操作系统也会发生故障。黑客学习了新的破坏网络和渗透应用程序的方法，你不可避免地需要定期对系统升级并打补丁。（是否升级和打补丁完全是另一个问题。）每当你接触系统时，都有可能犯错、错误配置关键服务或以其他方式完全毁掉你的系统。想一想你有多少次给运行任何操作系统的电脑打过补丁，然后发现某些东西运行异常了！即使是微小的变化也可能导致损坏。因此，你应该假设最坏的情况即将发生。在我们这里，这意味着要么硬件或人类销毁了你硬盘上的数据，你必须能够恢复这些数据。

更糟糕的是，如果你正在读这本书，你正处于学习如何配置 FreeBSD 阶段，因此还没有为灾难做好充分准备。作为一个新用户，你将需要测试各种配置并回顾你所做过的历史。没有什么比说“但这上个月还好好好的，我到底改了什么？”更让人沮丧的。你真的能记得过去几周、几个月或几年所做的每一个更改吗？同事所做的更改呢？事实上，如果你实验得足够疯狂，甚至可能会完全摧毁系统，你需要一种方法来恢复重要数据。

本章从备份整台计算机的大规模方法开始。如果你只想备份单个文件，这种方法的效果并不理想，因此我们将单独处理它们。如果一个文件每天变化三次，而你每周备份一次，那么当文件消失时你将丢失价值信息。最后，如果你遭遇了部分或近乎全部的灾难，我们将考虑使用单用户模式和修复磁盘（fixit disk）进行恢复和重建。

## 系统备份
