
如果你打算使用 Kerberos 进行登录身份验证，如上一节所述，测试 `krb-telnet` 等 Kerberos 客户端是确保你的 Kerberos 服务器运行正常且客户端能够成功与其通信的极佳方法。当你确定一切运行正常后，将 Kerberos 集成到用于系统登录过程的 PAM 中是逻辑上的下一步。

# 872 第 34 章

RHEL 和 Fedora 发行版提供的 `authconfig` 应用通过对 `/etc/pam.d/system-auth` PAM 文件进行所有必要的修改，简化了新身份验证机制的集成。要在系统中启用 Kerberos 认证，请执行以下操作：

1. 运行 `/usr/bin/authconfig` 命令，并在身份配置界面的“Authentication”部分中使用 Kerberos。图 34-7 显示了选中正确选项的此界面。
2. 选择 Next（下一步）并按回车进入下一个屏幕，输入你的域（realm）名称以及 KDC 管理服务器的 IP 地址或主机名（这些与本章示例使用的相同）。图 34-8 显示了选择了适用于本示例选项的此界面。选择 OK 并按回车退出 `authconfig` 应用。

> 注意：使用 DNS 定位主机和相关的 Kerberos 域需要在你的 DNS 服务器配置文件中添加特殊条目。有关有关此过程的更多信息，请参阅 `/usr/share/doc/krb5-server-version` 中的文档。

3. 退出 `authconfig` 后，注销并重新登录。登录后，使用 `klist` 命令验证你是否拥有 Kerberos 令牌，这将显示与上一节末尾显示相同的信息。

图 34-7 在 authconfig 中选择 Kerberos 认证。

## 实现网络安全 873

在使用 `authconfig` 后，你的 `/etc/pam.d/system-auth` 文件将如下：

```text
auth required               /lib/security/$ISA/pam_env.so

auth sufficient            /lib/security/$ISA/pam_unix.so alike

nullock

auth sufficient           /lib/security/$ISA/pam_krb5.so

use_first_pass

auth required               /lib/security/$ISA/pam_deny.so

account required            /lib/security/$ISA/pam_unix.so

broken_shadow

account sufficient         /lib/security/$ISA/pam_succeed_if.so uid < 100 quiet

account                   [default= success=ok user_unknown=ignore]

lib/security/$ISA/pam_krb5.so

account required            /lib/security/$ISA/pam_permit.so

password requisite          /lib/security/$ISA/pam_cracklib.so retry=3

password sufficient        /lib/security/$ISA/pam_unix.so nullock

use_authok md5 shadow

password sufficient        /lib/security/$ISA/pam_unix.so

auth required               /lib/security/$ISA/pam_deny.so

account required            /lib/security/$ISA/pam_permit.so

account sufficient           /lib/security/$ISA/pam_krb5.so
```

# 故障排除与问题解决

让他他（或她）重现问题。很多时候，用户会立即来电报告无法完成某些任务，但他们甚至不知道在问题发生时自己具体在做什么。要求用户再次尝试执行该任务，并写下问题发生时他们具体在执行的操作。询问他们是否收到了任何错误信息，如果有，以及信息内容是什么。通过这种方式，你将获得更多信息，用于帮助找出问题及其产生的原因。如果可能，尝试在用户执行任务时观察他们，以确定他们的操作方法是否正确。

## 第 3 步：寻找变化

在很多情况下，系统完美运行了几个月后突然停止工作。某个过去运行过无数次的服务现在无法工作了。为什么？你需要确定在一切正常到问题报告之间发生了什么变化。你可以提出一些可能引导你找到解决方案的问题。你可能会问的问题包括：

- 你能执行该任务吗？这听起来可能像个愚蠢的问题，用户通常会尝试执行系统并未设置支持的操作。也许他们可以在家里完成该任务，然后决定在公司尝试。你可能需要向用户解释，他们可能无法执行该任务，这并不是他们系统的问题。
- 如果某个服务之前可用，它是什么时候变得不可用的？知道这个答案可能会引导你发现问题发生前立即发生的变化。问题的原因可能与该变化直接相关。这个问题也引出了下一个问题。
- 自服务可用以来发生了什么变化？用户是否在系统上安装了任何软件？很多时候，发生的变化就是问题所在。
- 有其他用户也受该问题影响吗？如果问题只影响一个用户，你通常可以将问题隔离到该用户的系统上。

这些只是你可以向自己或用户提问的几个问题之一。在这一步以及故障排除过程的其他步骤中，你还可以提出许多探测性问题。你掌握的信息越多，你的故障排除工作就越容易。

## 第 4 步：确定最可能的原因

到此时，你已经完成了了故障排除中的三个步骤，应该能够缩小问题范围。接下来，你需要决定问题可能的原因。

如果继续之前的例子，即用户报告无法检查邮件，我们到目前为止的提问已经排除了许多可能的原因。我们知道物理网络连接是正常的，我们的 DNS 和路由器配置也是好的。如果问题只影响一个用户，我们可以推断问题与该特定用户的系统有关。显然，该用户的系统配置发生了某些变化，我们可以通过检查该特定系统（特别是邮件配置设置）来继续解决问题。

## 第 5 步：实施解决方案

在确定了问题最可能的原因后，你需要提出并实施解决方案。继续以无法发送邮件的例子，你已经确定问题出在单个用户的系统上。你需要检查该用户的系统配置，并进行必要的更改以恢复系统。在部署解决方案后，你需要测试系统以确保该方案已解决了问题。接下来，你应该确保实施解决方案没有导致任何额外的问题。有时，解决一个问题可能会引发其他问题，你需要确保你的解决方案不会出现这种情况。

## 第 6 步：保留文档记录

每当你遇到问题时，无论是你自己发现的，还是由用户报告给你的，你都应该对其进行记录。你应该完整地描述问题、你采取的调查步骤，以及所实施的解决方案。通过对系统问题保持良好的记录，你可以大幅缩短未来遇到类似问题的故障排除时间。

## 故障排除资源

每当你需要进行故障排除时，你通常不会单兵作战。有很多信息来源可以用来找到解决问题的办法。本节将按照我们认为最有用的顺序列出你可以使用的一些资源。

## 互联网

互联网是一个极好的信息源。很多时候当我的系统出现问题时，我会使用我最喜欢的搜索引擎搜索我正在遇到的问题。你的 Fedora Core 或 Red Hat Enterprise Linux 系统上出现的问题，很可能已经在其他某个系统上出现过。为什么不搜索一下这个问题，看看别人是如何确定原因及其解决方案的呢？正如老话所说：“为什么要重新发明轮子？”如果其他人有相同或类似的问题，为什么不看看他们是如何解决的呢？在大多数情况下，你的答案只需搜索即可找到。

## 系统日志文件

有时你可能在互联网上找不到问题的解决方案。也许问题太新，或者对于你的系统配置来说太特殊。在这种情况下，你可以使用系统日志文件获取更多关于问题的信息。

Fedora Core 和 Enterprise Linux 中的所有日志都位于 `/var/log` 目录。图 35-1 显示了典型 Fedora Core 系统的 `/var/log` 目录。

日志文件是文本文件，可以使用 `cat` 命令或任何文本编辑器查看。你必须以 root 身份登录才能查看日志文件的内容。一个非常有用的日志文件是内核启动文件，它显示了系统启动时上的所有设备及其配置状态。如果你的系统硬件出现问题，这是你开始故障排除的好地方。另一个值得查看的日志文件是 `/var/log/messages`，它包含了许多启动信息和最新的系统日志信息。列表 35-1 显示了内核启动日志内容的简略版本，可以通过执行命令 `dmesg` 查看。

```
[root@terry ~] dmesg

Linux version 2.6.0-77 (build@root.com) gcc version 3.4.20 #1 Feb 24 14:05

Kernel command line: root=/devGroup0/Logical1 quiet

Initializing CPU#0

CPU 0 interrupts tasks:

PID hash table entries: 2048 (order: 11, 32768 bytes)

Detected 598.26 MHz processor.

Using ptmgr for high-res timesource

Console: colour VGA

Dentry cache entries: 131072 (order: 7, 524288 bytes)

Inode cache entries: 65536 (order: 6, 262144 bytes)

Memory: 514364k/524096 available (2048 kernel node, 9128 reserved, 655k, 655k) 160k it, out 06

---snip---

ee1394: Initialized config entry 'ipv4'

hci1394: rev123 Ben collins@debian.org

ACPI: PCI interrupt 0000:02:00.00[1:4] -> GSI 10 (level, low) -> IRQ 10

hci1394: fw-host0: OHCI-1394.1.0 (PCI) IRQ:[10] MMIO:[90200000-902007ff] MaxPacket+[1024]

dim: Detecting RAID arrays.

md: autorun ...

md: ... adjacent DONE.

ieee1394: Host added: ID:BUS[0-00:1023] GUID[00023f4c4a405266]

SELinux: initialized (dev ramfs, type ramfs), uses genfs_configs

NET: Registered protocol family 10
```

列表 35-1 内核启动日志 dmesg 的内容。 (继续)

# 故障排除与问题解决 881

在设备 c03697c0(lo) 上禁用隐私扩展
IPv6 over IPv4 隧道驱动
divert: 为非以太网设备 sit0 分配 divert_blk
ACPI: 适配器槽 [C134] (在线)
ACPI: 电池槽 [C11f] (存在电池)
ACPI: 电源按钮 (FP) [PWRF]
ACPI: 盖开关 [C134]
ibm_acpi: 未找到对象
ACPI: 视频设备 [C000] (多头: yes rom: no post: no)
dm-0 上的 EXT3 FS，内部日志
日志启动: 提交间隔 5 秒
hda2 上的 EXT3 fs，内部日志
ext3-fs: 挂载了使用顺序数据模式的文件系统
selinux: 初始化: (dev hda2, type ext3), 使用 xattr
selinux: 初始化 (dev tmpfs, type tmpfs), 使用转换 SID
在 /dev/VolGroup0/Vol01 上添加 104856k swap。优先级:1 -extents:1
selinux: 初始化 (dev binfmint, type binfmint), 使用 genfs_contexts

**列表 35-1（继续）**

Fedora 和企业级 Linux 都提供了日志查看器，你可以用它查看日志。你需要运行 X 窗口系统才能使用日志查看器。在企业级 Linux 中，从桌面菜单选择“应用程序”->“系统工具”->“系统日志”。在 Fedora 中，选择“桌面”->“系统工具”->“系统日志”。如果你尚未登录，系统会提示你输入 root 密码。你将看到图 35-2 所示的“系统日志”窗口。图 35-2 中显示了内核启动日志 (dmesg)。

![](img/b5ebc2d43ffbc3488ca0205212f962cb_917_0.png)

**图 35-2** 系统日志窗口允许你选择查看哪个日志文件。

要了解日志文件的用途并查看其内容，请点击文件名。系统日志窗口的右上角会出现简短描述。所选日志文件的内容将出现在日志文件描述下方的文本框中。可以通过以下步骤向日志查看器添加其他日志文件：

- 1. 点击“编辑偏好”，打开图 35-3 所示的“偏好”对话框。
- 2. 点击“添加”，然后输入你想在日志列表中显示的名称、描述以及日志文件的路径。例如，要将 Samba 日志文件添加到日志列表，名称输入 `Samba Log`，位置输入 `/var/log/samba/smbd.log`。
- 3. 点击“确定”。Samba 日志条目将出现在日志文件列表中。

你系统中安装的许多程序会在 `/var/log` 中创建一个目录来存放它们的日志文件。例如，samba 服务器将其日志文件存放在 `/var/log/samba` 中。要查看任何与程序相关的日志文件，请进入相应的目录，并使用说明的某种方法查看文件。

# README 文件

README 文件通常包含关于软件硬件非常重要的信息，但由于某种原因，这些信息未包含在文档中。很多时候，README 中的信息旨在涵盖你可能遇到的具体问题。

![](img/b5ebc2d43ffbc3488ca0205212f962cb_918_0.png)

图 35-3 系统日志偏好对话框。

你可以找到安装和配置说明、默认设置和其他实用提示。每当你在系统上安装软件或硬件时，都应该阅读这些文件，而不仅仅是在遇到问题时。在尝试安装或配置其所指的软件或硬件之前阅读 README，你通常可以从源上避免问题。许多系统 README 文件位于 `/usr/share/doc` 目录下的以程序命名的子目录中。

# 解决常见问题

本节讨论的情况包括新用户遇到的常见问题。涵盖的主题包括无法登录系统以及处理忘记密码的问题。我们还查看了常见的硬件相关陷阱以及无效的命令。

# 无法登录

对于许多用户来说，一个常见的问题是无法登录。这个问题可能由许多问题引起，但最常见的原因是用户忘记了密码。另一个用户可能无法登录的原因是她在尝试使用的系统中没有账户。在任何情况下，你都可以以 root 用户身份登录并重置用户密码，或者为没有账户的用户创建一个账户。

# 重置用户密码

要重置用户密码，你必须将其更改不同的密码。按以下步骤操作：

- 1. 以 root 用户身份登录，打开终端窗口并输入以下命令：
  `passwd <用户名>`
- 2. 为用户输入新密码并按回车。
- 3. 再次输入相同的密码并按回车。
- 4. 注销 root 并以该用户身份登录，以确保登录正常。

# 创建用户账户

另一个用户可能无法登录的原因是她在尝试使用的系统中没有账户。在任何情况下，你都可以以 root 用户身份登录并重置用户密码，或者为没有账户的用户创建一个账户。（注：此处原文存在大量重复和 OCR 错误，翻译已根据逻辑进行清理）

## 第 35 章

尝试再次运行配置程序 —— 有时以 root 登录后运行它可以解决问题。选择“应用程序-系统设置-声卡检测”。如果检测到你的声卡，你将获得测试配置的选项。如果声音在测试期间正常，说明你已经完成了。

编辑 `/etc/modprobe.conf` 文件 — 如果声音无法工作或未检测到声卡，你可以通过编辑 `/etc/modprobe.conf` 文件来手动设置某些参数。列表 35-2 显示了我系统中的 `/etc/modprobe.conf` 文件。

```bash
[terry@terry ~]$ cat /etc/modprobe.conf

alias parport_lowlevel carport_pc

alias eth0 el10

alias usb-controller usb-uhci

alias sound-slot-0 snd-cs4232

options sound dmabuf=1

alias synth oplj3

options opljio=0x388

options cs4232 isapnp=1
```
