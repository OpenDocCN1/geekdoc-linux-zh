
一旦创建了配置文件，您有几种方法让 Kickstart 使用它。官方认可的方法是使用 DVD 启动并在初始启动提示符处指定 `linux ks` 来进行 Kickstart 安装。如果系统通过 DHCP 确定网络地址，它将获取 DHCP 启动服务器和启动文件选项，尝试通过 NFS 挂载启动服务器，并使用启动文件选项的值作为其 Kickstart 配置文件。如果没有指定启动文件，系统将寻找名为 `kickstart/host_ip_address-kickstart` 的文件。

或者，您可以通过为 `ks` 选项提供路径作为参数，告诉 Kickstart 以其他方式获取其配置文件。有几种可能性：

```
boot linux ks=http:server/path
```

告诉 Kickstart 使用 HTTP 下载文件而不是 NFS。`ks=floppy` 则告诉 Kickstart 在本地软盘上查找 `ks.cfg`。

要完全消除启动介质，您将需要升级到 PXE。有关该内容的更多信息请参阅第 363 页。

# 使用 YaAST：SUSE 的自动化安装工具

YaST2 是 SUSE 的全功能安装和配置工具。它带有一个美观的 GUI，在安装单个系统时使用起来很有趣。AutoYaAST 是其自动化版本，是本书所介绍的所有发行版中最强大的自动化安装软件。您可以从 `suse.com/~ug/autoyast_doc` 下载详细文档。

SUSE 将自动安装过程分为三个阶段：准备、安装和配置。初始准备通过 YaST2 AutoYaST 模块执行：

```
suse$ /bin/yast2 autoyast
```

该模块定义了您所需设置的细节。运行它的结果是一个 XML 控制文件，它告诉安装程序如何配置 SUSE

![](img/579efec8c67772f31ecf34844bbb71a2_415_0.png)

## 第 12 章 软件安装与管理

系统。文件的结构在上述的在线文档中描述。

几个快捷方法可以加快配置过程。AutoYaST 模块可以读取 Kickstart 配置文件来帮助您从“旧”系统升级。如果您想复制当前机器的配置，也可以启用此选项。

要执行实际安装，您需要三个网络服务：

- 与设置的同一子网的 DHCP 服务器
- SUSE 安装服务器或软件包仓库
- 提供配置信息的服务器

最后一种设置可以通过选择的 HTTP、NFS 或 TFTP 提供配置文件。

在基础设置中，您为要安装的每个机器创建一个配置文件。AutoYaST 使用客户端的 IP 地址来确定使用哪个配置文件。如果您需要安装一系列不同的机器，这种方法并不是特别高效。

您可以使用规则系统创建更复杂的设置。根据磁盘大小、主机 ID 或 PCMCIA 可用性等属性将不同的配置文件匹配到目标系统。所有选中的文件内容将合并，在冲突的情况下，最后一个文件将覆盖前面的文件。（配置文件不需要指定系统配置的所有方面，因此合并是有意义的。）

配置文件还可以根据主机名或 IP 地址范围定义机器的“类”，并且每个类都可能关联另一个子级配置文件。机器可以属于零、一个或多个类，它们的配置将整合所有相关类文件的内容。

得益于整合多个配置文件的能力，AutoYaST 结构允许以最少的冗余定义复杂的设置。XML 控制文件对于人类来说可能有些繁琐，但这些文件可以使用任何常用的 XML 工具进行简单的处理和编辑。

## 使用 Ubuntu 安装程序实现自动化

Ubuntu 依赖于底层的 Debian 安装程序（名之恰恰为 `debian-installer`）进行“预填充”，这是推荐的自动化安装方法。在 Kickstart 中，预配置文件回答安装程序提出的问题。预填充安装无法使用现有分区；它们必须使用空空间或对整个磁盘进行分区。

Debian 安装程序的所有交互部分都使用 `debconf` 工具来决定提问哪些问题以及使用哪些默认答案。通过提供 `debconf`

### 使用 Ubuntu 安装程序实现自动化安装

通过一个预设答案的数据库，你可以实现安装程序的完全自动化。你可以手动生成该数据库（这是一个文本文件），也可以在示例系统上进行交互式安装，并使用以下命令导出你的 debconf 答案：

```
ubuntu$ sudo debconf-get-selections --installer > preseed.cfg
ubuntu$ sudo debconf-get-selections >> preseed.cfg
```

将配置文件发布到网络上，然后通过以下内核参数将其传递给内核安装：

`preseed/url=http://host/path/to/preseed`

`preseed` 文件（通常称为 `preseed.cfg`）的语法非常简单，让人联起 Red Hat 的 `ks.cfg`。为了简单起见，示例经过简化。

```
-d debian-installer/locale string en_US
-d console-setup/ask_detect boolean false
-d console-setup/layoutconfigure string
-d netcfg/choose_interface select auto
-d netcfg/get_hostname string unassigned-hostname
-d netcfg/get_domain string unassigned-domain
-d netcfg/wireless_webp string
-d partman-auto/disk string /dev/sda
-d partman-auto/method string lvm
-d partman-auto/choose_recipe select atomic
...
-d password/user-filename string Duffy Duck
-d password/username string dduck
d$1$/mk9$G$/it6N.x6670.951VSM/
-d user-setup/enter-home boolean false
tasksel/first/multiselect ubuntu-desktop
d-d grub-installer/only_debian boolean true
d-d grub-installer/with_other_os boolean true
d-d finish-install/reboot_in_progress note
xserver-org xserver-org/autodetect_monitor boolean true
```

列表中的几个选项会显示简单的对话框，这些框通常需要用户交互。例如，`ask_detect` 禁用了键盘布局选择。同样，`wireless_webp` 会获取一个关于 WEP 密钥的问题。

此配置识别一个连接到网络的网络接口（`choose_interface select auto`）并通过 DHCP 获取网络信息。系统主机名和域名值假定由 DHCP 提供且不会被覆盖。

`partman*` 是使用 `partman-auto` 包进行磁盘分区的证据。除非系统只有一个磁盘，否则你必须指定一个安装磁盘。在这种情况下，使用了 `/dev/sda`。

提供了几种分区“配方”：

- `atomic` 将系统所有文件放在一个分区中。
- `home` 为 `/home` 创建一个独立的分区。
- `multi` 为 `/home`, `/usr`, `/var` 和 `/tmp` 创建独立的分区。

你可以通过密码系列指令创建用户。与 Kickstart 配置一样，我们强烈建议提供 MD5 哈希处理后的密码值。Preseed 文件通常存储在 HTTP 服务器上，很容易被好奇的用户发现。（当然，MD5 密码仍然面临受到暴力攻击的风险。）

任务选择（`tasksel`）选项用于选择安装的 Ubuntu 系统类型。可用值包括标准版（`standard`）、`ubuntu-desktop`、`dns-server`、`lamp-server`、`kubuntu-desktop`、`edubuntu-desktop` 和 `xubuntu-desktop`。

上述显示的示例预设文件来自 `help.ubuntu.com` 上的 Ubuntu 文档。该指南包含了关于 `preseed` 文件语法和用法的完整文档。

尽管 Ubuntu 并非源自 Red Hat 血统（后者在其底层首次引入了对 Kickstart 控制文件的兼容性），但 Ubuntu 也包含了 `system-config-kickstart` 工具来创建这些文件。Ubuntu 安装程序中的 Kickstart 功能缺少许多 Red Hat 的 Anaconda 支持的重要功能，例如 LVM 和 fiery 配置。除非你有选择 Kickstart 的充分理由，否则我们建议使用 Debian 安装程序。

## 第 12 章 软件安装与管理

### 12.2 安装 Solaris
