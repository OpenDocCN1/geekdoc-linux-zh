
![](img/1e024b9f135a8b3cebc6731238212d84_839_0.png)

图21-3 联系人，Evolution 窗口

在窗口右上角标记为搜索（Search）的文本框中输入每个条目并按回车键。Evolution 显示该条目。图 21-33 显示了遵循本章示例并在搜索文本框中输入 Zach 的结果。

# g: 一个 LDAP 客户端 (Fedora)

`gq` 工具（sourceforge.net/projects/gclient; `gq` 包）是一个图形化 (GTK+) LDAP 客户端，你可以用它显示和修改条目。在可以使用 `gq` 之前，你必须为管理员指定 DN。选择菜单栏：文件（File）首选项（Preferences），点击服务器（Servers）选项卡，突出服务器（示例中的 localhost），点击编辑（Edit），连接（Connections）选项卡，并将 Bind DN 设置为管理员的 DN（示例中 `cn=ldapadmin,dc=brillserve,dc=com`）。图 21-4 显示了 `gq` 显示来自 LDAP 目录的条目。

![](img/1e024b9f135a8b3cebc6731238212d84_839_1.png)

图 21-4 使用 `gq` 浏览 LDAP 目录

# 第 21 章 NIS 与 LDAP

![](img/1e024b9f135a8b3cebc6731238212d84_840_0.png)

图 21-5 架构（Schema）选项卡

你也可以使用 `qf` 浏览架构：点击架构（Schema）选项卡并从窗口左侧选择服务器（图 21-5 中的 localhost）。选择对象类（objectClasses），然后选择一个对象类以查看该对象类的信息，包括必需和可选属性的列表。

# 本总结

NIS（网络信息服务）通过将常用管理文件维护在中央数据库中并让客户端联系数据库服务器从数据库中检索信息，简化了管理文件的管理。NIS 服务的网络被称为 NIS 域。每个 NIS 域都有一个主服务器；较大的网络可能有从服务器。

NIS 的信息源自本地配置文件，例如 `/etc/passwd` 和 `/etc/hosts`。这些文件被称为源文件或主文件。在 NIS 能够存储源文件中包含的信息之前，必须将其转换为 dbm 格式的文件，称为映射（maps）。`yprint` 和 `ymatch` 工具显示来自 NIS 映射的信息。

当你使用 NIS 进行密码身份验证时，`ypasswd` 工具取代代了 `passwd` 客户端的功能。`/etc/ypserver.conf` 文件保存了 NIS 配置信息，指定了 NIS 服务器的选项和访问规则。为了增强系统安全性，你可以创建一个 `/var/yp/securenets` 文件，防止未经授权的系统检索 NIS 映射。

LDAP（轻量级目录访问协议）服务器持有针对搜索和读取化的数据库，称为目录。LDAP 客户端（如电子邮件客户端）查询并更新此目录。此外，身份验证服务器可以使用 LDAP 验证用户。

Fedora/RHEL 提供了 LDAP 的 OpenLDAP 实现。OpenLDAP 使用 Sleepycat Berkeley Database，支持分布式架构、复制和加密。

# 练习

1. `passwd` 和 `ypasswd` 工具有什么区别？

2. 你如何防止 NIS 将 root 用户和其他系统用户导出到客户端？

3. 你如何让 NIS 用户信息覆盖客户端系统上的本地用户信息？

4. 为什么 `/etc/passwd` 文件需要两个 NIS 映射？

5. LDAP 目录与关系型数据库系统有什么不同？

6. LDAP 目录中的基本信息单元是什么？属性的结构是什么？

# 进阶练习

7. 你如何使用 NIS 为小型网络镜像私有 DNS 服务器的功能？为什么在大型网络中不应这样使用 NIS？

8. 如何确定工作目录是否为 NIS 用户的家目录？

9. a. 当 NIS 与 NFS 使用时，它提供了什么优势？

   b. 建议一种实现 NIS 映射的方法，使其可以在多个字段上进行索引。

10. LDAP 设备对象类在哪里定义？它的哪些属性是强制的，哪些是可选的？

11. 你如何确定 I（小写字母“l”）LDAP 对象类的更长名称？

本页故意留白

# NFS：共享目录层次结构

## 本章内容

## 目标

- 运行 NFS 客户端 . . . . . . . . . . . . 795
- JumpStart I: 挂载远程目录层次结构 . . . . . . . . . . . . 796
- 提高性能 . . . . . . . . . . . . . 800
- 设置 NFS 服务器 . . . . . . . . . . . . . . . . . . 801
- JumpStart II: 使用 config-nfs (Fedora) 配置 NFS 服务器 . . . . . . 802
- 手动导出目录 . . . . . . . . . . . . 804
- 故障排除 . . . . . . . . . . . . . . . . . . . . . . 810
- NFS4: 挂载层次结构 . . . . . . . . 811
- NFS4: automount：按需挂载

读完本章后，你应该能够：

- 描述 NFS 的用途、历史和架构
- 挂载 NFS 客户端
- 配置 NFS 服务器
- 排除挂载故障
- 设置 automount 自动挂载目录

# 792 第 22 章 NFS：共享目录层次结构

![](img/1e024b9f135a8b3cebc6731238212d84_844_0.png)

**图 22-1** 典型 NFS 设置中的数据流

NFS（网络文件系统）协议是由 Sun Microsystems 开发的 UNIX 事实标准，允许服务器与客户端共享目录。客户端上的文件看起来就像于本地一样。NFS 服务器将客户端的命令翻译为服务器文件系统的操作。

在许多设施中，文件存储在配备大容量磁盘设备的中央文件服务器上，这些设备可以快速方便地制作数据的备份副本。无盘系统从文件服务器（网络启动——下文将讨论）或通过 CD/DVD 启动并从文件服务器加载系统软件。Linux 终端服务器项目（LTSP.org）网站说明了一切——Linux 是一个极

# 794 第 22 章 NFS：共享目录层次结构

从网络服务器启动的无盘工作站。LTSP 的核心在于在 Linux 环境中运行瘦客户端计算机。”由于无盘工作站确实大量的计算能力，你可以通过将它们作为无盘系统使用，让旧的、淘汰的计算机获得第二次生命。

Netboot/PXE 你可以对设置恰当的系统进行网络启动（第 1177 页）。Fedora/RHEL 包含 TFTP（简单文件传输协议；`tftp-server` 软件包），你可以使用它为 Intel 系统构建 PXE（预启动执行环境）启动服务器。非 Intel 架构在历史上包含了网络启动功能，你可以编译 Linux 内核，使其使用 NFS 挂载根目录（`/`）。RHEL 也支持。由于设置系统有多种方法，你可以根据你的需求进行选择。更多信息请参阅 Remote-Boot mini-HOWTO。

无数据系统另一种类型的 Linux 系统是无数据系统，在这种系统中，客户端拥有磁盘但不存储任何用户数据（磁盘上仅保留 Linux 和应用程序）。设置此类系统在于选择从远程挂载哪些目录层次结构。

df 显示目录层次结构的挂载位置 `df` 工具显示系统上可用的目录层次结构列表，以及每个目录的大小、已用空间和可用空间。`-h`（人类友好）选项使输出更具可读性。左列中的设备名称带有 `主机名:`，表示通过 NFS 可用的目录层次结构。

```
[zachguava~]$ cd pwd;
 /home/zach
[zachguava~]$ df -h
Filesystem Size Used Avail% Mounted on
/dev/mapper/vg_guava-lv_root 20G 2.4G 18G 13% /
plum:/home/zach 37M 2.3G 35G 7% /home/zach
/dev/sda1 485M 50M 410M 11% /boot
```

当 Zach 在 guava 上登录时，他的家目录 `/home/zach` 位于远程系统 plum 上。使用 NFS，plum 上的 `/home/zach` 目录层次被挂载到 guava 的 `/home`。当挂载 plum 上的 `zach` 目录时，任何文件都会隐藏；当卸载目录时，它们会重新出现。`/` 文件系统是 guava 的本地文件系统。

```
$ df -THT
Filesystem Type Size Used Avail% Mounted on
/dev/mapper/vg_guava-lv_root ext4 20G 2.4G 18G 13% /
plum:/home/zach nfs4 37M 2.3G 35G 7% /home/zach
/dev/sda1 ext4 485M 50M 410M 11% /boot
```

# 运行 NFS 客户端 795
