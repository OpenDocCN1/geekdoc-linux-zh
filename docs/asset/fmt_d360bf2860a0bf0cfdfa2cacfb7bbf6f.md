
- 一个 SUSE 安装服务器或软件包仓库
- 一个为安装提供配置信息的服务器

这三个服务器中的最后一个可以通过你选择的 HTTP、NFS 或 TFTP 提供配置文件。

在最基本的设置中，你为每台要安装的机器制作一个控制文件。AutoYaST 使用客户端的 IP 地址来确定使用哪个控制文件。如果要安装一系列略有不同的机器，这种方法并不特别高效。

你可以通过使用规则系统来创建更复杂的设置。不同的控制文件根据系统属性（如磁盘大小、主机 ID 或 PCMCIA 可用性）与目标系统匹配。所有选定控制文件的内容都会被合并，如果发生冲突，最后一个控制文件会覆盖之前的控制文件。（控制文件不必指定系统配置的所有方面，因此这种合并是有意义的。）

控制文件还可以根据主机名或 IP 地址范围定义机器的“类”，并且每个类可能还有另一个相关的子控制文件。机器可以属于零个、一个或多个类，其配置将合并所有适当的类控制文件的内容。

得益于整合多个控制文件内容的能力，AutoYaST 结构允许以最小的冗余定义复杂的设置。XML 控制文件对人类来说有点笨重，但文件很容易用任何常用的 XML 处理工具进行处理和编辑。

### 使用 Ubuntu 安装程序自动化安装

Ubuntu 依赖于底层的 Debian 安装程序（恰如其名，名为 `debian-installer`）进行“预设”，这是自动化安装的推荐方法。与 Kickstart 类似，预配置文件会回答安装程序提出的问题。预设安装不能使用现有分区；它们必须使用现有的空闲空间或重新分区整个磁盘。

Debian 安装程序的所有交互部分都使用 `debconf` 实用程序来决定要提出哪些问题以及使用什么默认答案。通过为 `debconf` 提供一组预先制定的答案数据库，你可以完全自动化安装程序。你可以手动生成数据库（它是一个文本文件），也可以在示例系统上执行交互式安装，然后使用以下命令导出你的 `debconf` 答案：

```
ubuntu$ sudo debconf-get-selections --installer > preseed.cfg
ubuntu$ sudo debconf-get-selections >> preseed.cfg
```

使配置文件在网络上可用，然后在安装时通过以下内核参数将其传递给内核：

```
preseed/url=http://host/path/to/preseed
```

`preseed` 文件的语法，通常称为 `preseed.cfg`，简单明了，让人想起 Red Hat 的 `ks.cfg`。下面的示例已为简单起见而缩短。

```
d-i debian-installer/locale string en_US
d-i console-setup/ask_detect boolean false
d-i console-setup/layoutcode string us
d-i netcfg/choose_interface select auto
d-i netcfg/get_hostname string unassigned-hostname
d-i netcfg/get_domain string unassigned-domain
d-i netcfg/wireless_wep string

d-i partman-auto/disk string /dev/sda
d-i partman-auto/method string lvm
d-i partman-auto/choose_recipe select atomic
...
d-i passwd/user-fullname string Daffy Duck
d-i passwd/username string dudck
d-i passwd/user-password-crypted password $1$mkq9$EG//i6tN.x6670.95IVSM/
d-i user-setup/encrypt-home boolean false
tasksel tasksel/first multiselect ubuntu-desktop
d-i grub-installer/only_debian boolean true
d-i grub-installer/with_other_os boolean true
d-i finish-install/reboot_in_progress note
xserver-xorg xserver-xorg/autodetect_monitor boolean true
...
```

此列表中的几个选项只是禁用了通常需要用户交互的对话框。例如，`ask_detect` 禁用了键盘映射选择。同样，`wireless_wep` 选项阻止了关于 WEP 密钥的问题。

此配置试图识别实际连接到网络的网络接口（`choose_interface select auto`）并通过 DHCP 获取网络信息。系统主机名和域名值被假定由 DHCP 提供，并且不会被覆盖。

提供了几种分区“配方”：

- `atomic` 将系统的所有文件放在一个分区中。
- `home` 为 `/home` 创建一个单独的分区。
- `multi` 为 `/home`、`/usr`、`/var` 和 `/tmp` 创建单独的分区。

你可以通过 `passwd` 系列指令创建用户。与 Kickstart 配置一样，我们强烈建议提供 MD5 哈希的密码值。`Preseed` 文件通常存储在 HTTP 服务器上，很容易被好奇的用户发现。（当然，MD5 密码仍然容易受到暴力破解攻击。）

任务选择（`tasksel`）选项用于选择要安装的 Ubuntu 系统类型。可用的值包括 `standard`、`ubuntu-desktop`、`dns-server`、`lamp-server`、`kubuntu-desktop`、`edubuntu-desktop` 和 `xubuntu-desktop`。

上面所示的示例 `preseed` 文件来自 help.ubuntu.com 上的 Ubuntu 安装文档。该指南包含 `preseed` 文件的语法和用法的完整文档。

尽管 Ubuntu 不源自 Red Hat 系，但它在其底层安装程序上嫁接了与 Kickstart 控制文件兼容的功能。Ubuntu 还包含 `system-config-kickstart` 工具用于创建这些文件。Ubuntu 安装程序中的 Kickstart 功能缺少 Red Hat Anaconda 支持的许多重要功能，例如 LVM 和防火墙配置。我们建议坚持使用 Debian 安装程序，除非你有充分的理由选择 Kickstart。

## 12.2 安装 SOLARIS

与大多数硬件厂商一样，Sun 会在新服务器上预装 Solaris。管理员只需回答几个简单问题并重新启动服务器，操作系统即可准备好进行本地化。我们多年来很欣赏这种预装功能，因为 Solaris 安装程序糟糕透顶。然而，OpenSolaris 团队已经幡然醒悟，新的安装程序（最初代号为“Caiman”）堪称一流。

Solaris 媒体现在是一个 live CD，提供类似 Ubuntu 的“试用后再购买”体验。安装过程非常简单，只需在安装到本地驱动器之前回答几个问题。

与 Linux 世界一样，Solaris 管理员需要一种通过网络实现大规模部署的方法。运行 Intel 处理器的 Solaris 系统可以使用 PXE 服务器进行网络启动辅助，就像他们的 Linux 同类一样。SPARC 处理器系统使用 OpenBoot PROM，即 `OBP`。`OBP` 通常通过 Sun 键盘上的 `STOP+A` 键组合访问。它识别并测试硬件，检测错误条件，并将启动过程交给更复杂的启动加载程序，类似于 Intel 系统上的 BIOS。然而 `OBP` 的功能比大多数 PC BIOS 更强大，包括内置的网络启动支持。

网络启动功能通过 DHCP 或 RARP 获取 IP 地址，然后通过 TFTP 下载内核。启动进行自动安装时，内核会连接到 HTTP 服务器或挂载 NFS 共享以下载适当的系统映像并开始安装。

Solaris 提供两种自动网络安装方法：

- `JumpStart`，由 Sun 开发的传统安装服务
- `Automated Installer`，由 OpenSolaris 使用的替代服务

`JumpStart` 是一款老牌安装工具，最早出现在 Solaris 2.6 中，可用于所有到 Solaris 10 的版本。与大多数自动安装方法一样，`JumpStart` 使用预定义的答案文件和基于规则的客户端选择来自动做出安装选择。

`JumpStart` 最大的缺点是其可扩展性差。每个客户端都必须通过 MAC 地址手动添加到安装服务器。配置文件按客户端指定安装类型、配置值和其他参数。这赋予管理员权力和灵活性，但在你拥有数百或数千台系统时就会变得繁琐。

`Automated Installer`（有时称为 AI）是新晋者。其主要开发目标是提高可扩展性和减少配置。AI 的根源在于 `JumpStart`，但部分通过使用新术语而与之区别。到本文撰写时，AI 仍在完善中，但或多或少已可用于生产环境。值得注意的是，AI 仅限于 OpenSolaris 的最新版本，目前完全不适用于传统 Solaris。

### 使用 JumpStart 进行网络安装
