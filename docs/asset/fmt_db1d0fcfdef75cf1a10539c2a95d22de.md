
```
label Linux
menu label ^Install RHEL
menu default
kernel vmlinuz
append initrd-initrd.img \
ks=http://account.example.com/anaconda-ks.cfg
```

在该文件中，请确保 `menu label` 的标题以 `^` 开头，这将其标识为菜单标签标题。同时确保 `append` 行是一行以 `append` 开头并以 Kickstart 文件的 URL 结尾的内容。

在使用虚拟机管理器（Virtual Machine Manager）安装虚拟机时，也可以使用 Kickstart 文件。在练习 20.3 中，你将学习如何在不使用 PXE 启动的情况下进行网络安装，并配置此安装使用 `anaconda-ks.cfg` 文件。

# 练习 20.3 使用 Kickstart 文件进行虚拟机网络安装

在此练习中，你对一个使用 Kickstart 文件的虚拟机进行网络安装。你使用了练习 20.1 中创建的网络安装服务器。该网络服务器用于访问安装文件，同时也提供对 Kickstart 文件的访问。

> 在练习中，你使用的是安装服务器的 DNS 名称。如果安装失败并显示消息“unable to retrieve http://account.example.com/images/install.img”，那是因为无法通过 DNS 解析 `account.example.com`。请使用安装服务器的 IP 地址。

- 1. 在安装服务器上，将 `/root` 目录下的 `anaconda-ks.cfg` 文件复制到 `/www/docs/account.example.com` 目录。你可以直接将其复制到根目录。复制文件后，将权限设置为模式 644；否则 Apache 用户将无法读取它。
- 2. 启动虚拟机管理器并点击“创建虚拟机”按钮。为虚拟机输入名称，并选择“网络安装”。
- 3. 在“创建新虚拟机”向导的第二个屏幕，输入 Web 服务器安装目录的 URL：`http://account.example/`。打开“URL 选项”并输入以下 Kickstart：`http://account.example/anaconda-ks.cfg`（见图 20.1）。
- 4. 接受创建新虚拟机向导中剩余窗口中的所有默认选项，这将启动安装。在过程开始，你将看到“Retrieving anaconda-ks.cfg”的消息。如果该消息消失且你没有看到错误，说明 Kickstart 文件加载成功。
- 5. 在 Kickstart 文件加载后停止安装。由于 Kickstart 文件是为虚拟机设计的，它仍然会询问很多问题。（此练习的目的是证明 Kickstart 文件是有效的。）停止安装后，从虚拟机管理器中移除配置。

464 红帽 RHCSA/RHCE 7 指南

![](img/5a30005f195700270765e15ffa2b199b_520_0.png)

图 20.1 指定使用 Kickstart 文件的选项。

# 使用 system-configstart 修改 Kickstart 文件

在在上一个练习中，你根据安装完成后创建的 Kickstart 文件启动了安装。你可能注意到仍然询问了很多问题，那是因为你的 Kickstart 文件不符合你尝试安装的虚拟机。在许多情况下，你需要微调 Kickstart 配置。为了实现这一点，你可以使用 `system-configstart` 界面（见图 20.2）。

使用 `system-configstart`，你可以创建新的 Kickstart 文件，也可以读取现有的 Kickstart 文件并进行所有修改，而无需担心导致 Kickstart 文件失败的语法错误。

## 第 20 章：使用 Kickstart 465

![](img/5a30005f195700270765e15ffa2b199b_521_0.png)

使用 `system-configstart` 创建或调整 Kickstart 文件。

> 注意：早期的 RHEL 版本中，有很多 `system-config` 工具可以方便配置 RHEL。在 RHEL 7 中，操作系统本身经历了重大修订，大多数 `system-config` 工具已被取代。`system-configstart` 工具是剩余的工具之一。如果你用过以前版本的 RHEL，你会发现它的界面与 RHEL 6 安装界面非常相似，且某些项目发生了变化。你还会发现许多 RHEL 7 的功能在该界面中并不支持。例如，你无法通过 `system-configstart` 创建 `firewalld` 配置；无法通过该工具配置 LVM 或安装单个 RPM 包。

在“基本配置”选项下，你可以找到安装服务器的基本选项，如键盘和时区。在这里，你还会找到设置 root 密码的界面。在“安装方法”下，你会找到安装源。你需要选择网络安装服务器的类型以及该服务器上使用的目录。在图 20.3 中，你可以看到你在练习 20.1 中创建的安装服务器的样式。

## 466 红帽 RHCSA/RHCE 7 认证指南

![](img/5a30005f195700270765e15ffa2b199b_522_0.png)

**图 20.3** 指定网络安装源。

在引导加载选项（Boot Loader Options）下，你可以指定想要安装新的引导加载程序以及想要安装它的的位置。如果在启动时需要内核参数，你也可以在这里指定它们。一个重要的选项是分区信息（Partition Information，见图 20.4）。在这里，你可以告诉 Kickstart 你想在服务器上创建哪些分区。遗憾的是，该界面不允许你创建逻辑卷。如果你需要这些逻辑卷，需要手动添加，这将在下一节中进行解释。

![](img/5a30005f195700270765e15ffa2b199b_522_1.png)

**图 20.4** 创建分区。

网络配置（Network Configuration）选项默认是空的。如果你想在服务器上使用网络，需要使用添加网络设备（Add Network Device）选项来指定设备名称以及你希望设备如何获取网络配置。身份验证（Authentication）选项提供了标签页，用于指定外部身份验证服务，例如 NIS、LDAP、Kerberos 等。如果你不指定其中任何项，只需使用通过 `/etc/passwd` 的本地身份验证机制，这对于许多服务器来说是可以的。

如果你不喜欢 SELinux 和防火墙，可以激活防火墙配置（Firewall Configuration）选项。SELinux 默认开启（这在大多数情况下是好事），而防火墙默认是的。如果你的服务器直接连接到互联网，请开启它并选择你想要允许的所有信任服务。在显示配置（Display Configuration）选项上，你可以告诉安装程序你的服务器是否应该安装图形环境。

一个有趣的选项是软件包选择（Package Selection）。该选项允许你选择类别而不是单个软件包。如果你需要单个软件包，你需要创建一个手动配置。最后，还有安装前脚本（Pre-Installation Script）和安装后脚本（Post-Installation Script）选项，允许你在安装服务器时向安装过程添加脚本。

# 对 Kickstart 文件进行手动修改

有些修改是无法通过图形界面对 Kickstart 文件完成的。幸运的是，Kickstart 文件是一个 ASCII 文本文件，可以很容易手动编辑。通过手动修改，你可以配置如 LVM 逻辑卷或单个软件包等功能，这些功能是 `system-config-kickstart` 界面无法实现的。在列表 20.4 中，你可以看到安装服务器时生成的 `anaconda-ks.cfg` 文件内容。研究这个文件很有趣，因为它展示了所有无法通过图形界面完成的操作示例。

**列表 20.4** `anaconda-ks.cfg` 的内容

```
[root@server1 ~]# cat anaconda-ks.cfg
#version=RHEL7
# 系统授权信息
auth --enableshadow --passalgo=sha512

# 使用 CDROM 安装介质
cdrom
# 在首次启动时运行 Setup Agent
firstboot --enable
```

```
ignoredisk --only-use=sda
## 键盘布局
keyboard --vckeymap=us --xlayouts='us'
# 系统语言
lang en_US.UTF-8
```
