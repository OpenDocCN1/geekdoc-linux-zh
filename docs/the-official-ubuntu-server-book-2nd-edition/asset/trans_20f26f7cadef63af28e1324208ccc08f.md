

```
keyboard us
#System mouse
mouse
#System timezone
timezone America/Los_Angeles
#Root password
rootpw --disabled
#Initial user
user ubuntu --fullname "ubuntu" --password insecure
#Reboot after installation
reboot
#Use text mode install
text
#Install OS instead of upgrade
install
#Use CDROM installation media
cdrom
#System bootloader configuration
bootloader --location=mbr
#Clear the Master Boot Record
zerombr yes
#Partition clearing information
clearpart --all --initlabel
#Disk partitioning information
part / --fstype ext3 --size 1 --grow --asprimary
part swap --recommended
#System authorization information
auth --useshadow --enablemd5
#Firewall configuration
firewall --disabled
#Do not configure the X Window System
skipx
# This section was added by hand
preseed base-installer/kernel/override-image string linux-server
preseed pkgsel/language-pack-patterns string
preseed pkgsel/install-language-support boolean false
%packages
@ standard
@ ubuntu-server
```

正如我对 preseed 文件所做的那样，我设置了一个单独的 / 分区，并使用 --grow 选项使其填满整个驱动器（实际上我只是在 GUI 中切换了该设置）。然后我将这个 ks.cfg 文件复制到我之前使用的同一个 Web 服务器上。使用这个 Kickstart 文件的另一个好处是，我不需要在启动时手动输入大量设置。事实上，我只需要将已有的 file preseed 选项替换为指向我的 Kickstart 文件的选项。启动 CD-ROM，然后按 F6 以

这些设置已经在 %packages 部分中的 Kickstart 文件中管理，但如果它们没有被管理，你可以使用以下方式设置此设置：

```
preseed --owner tasksel tasksel/first multiselect \
standard, ubuntu-server
```

## 账户选项

Kickstart 语法中另外两个重要的新增功能为账户管理提供了额外选项。由于 Ubuntu 默认禁用 root 用户，rootpw Kickstart 命令现在可以采用 --disabled 选项。这会禁用 root 密码，并赋予第一个用户通过 sudo 获得的 root 权限。

Ubuntu 的 Kickstart 文件还添加了一个 user 命令来为初始用户添加设置。该命令的语法如下：

```
user --disabled | username [--fullname "Firstname Lastname"] \
--password insecure [--iscrypted]
```

该命令要么采用 --disabled 选项来完全禁用初始用户，要么采用用户名、可选的全名以及最后的密码作为选项。默认情况下，密码是明文，但你也可以选择列出密码的 MD5 哈希；只需确保添加 --iscrypted 选项，以便 Kickstart 知道。

## 局限性

目前，Ubuntu 的 Kickstart 并未实现 Red Hat Kickstart 的全部功能。这些限制是提倡将 Kickstart 与 preseeding 结合使用的原因之一。Kickstart 文件可以处理基本配置，而在功能不可用的地方，可以通过 preseed 选项进行补充。以下列表列出了 Ubuntu Kickstart 尚未实现的主要功能：

- 不支持 LDAP、Kerberos 5、Hesios 或 Samba 认证。
- 没有针对 lilo 的 bootloader --linear、--nonlinear 或 --lba32 选项。
- 没有 lilocheck 命令。
- Ubuntu 在 Kickstart 文件之外处理系统升级。
- Ubuntu Kickstart 中的分区功能还不够完善。因此，如果你有更复杂的分区需求，我建议使用 preseed 选项进行补充。以下是当前分区的限制：
  - 只能对主磁盘进行分区
  - 不支持 LVM 配置
  - 不检查坏扇区
  - 不支持 RAID 分区
- 你不能将分区限制到特定磁盘，也不能指定起始或结束柱面。
- 安装期间不支持补充驱动程序盘。
- 不支持 device 命令。
- 不支持防火墙配置。
- 无法通过 DHCP 自动发现 Kickstart 源；你必须明确指定 Kickstart 源。
- 不支持将 NFS 和本地磁盘作为安装源。
- 不支持 xconfig --monitor 选项（选择特定的显示器名称）。
- Ubuntu 和 Red Hat 中的软件包组名称不同，在 Ubuntu 下，软件包组引用的是 Ubuntu 任务。
- 你不能在 %packages 部分排除软件包。
- 你只能在安装前和安装后部分使用 shell 脚本。

## 在安装期间运行自定义命令

与 preseeding 一样，Kickstart 支持在安装期间运行自定义命令。同样，与 preseeding 一样，这是通过安装前和安装后脚本完成的。在 Kickstart 文件中，这些分别在 %pre 和 %post 部分中定义。你放在这些部分中的任何 shell 命令将分别在安装过程之前或之后立即执行。Kickstart 中这些脚本的一个不错特性是，只要它们保持在 %pre 或 %post 部分内，就可以跨越多行。

