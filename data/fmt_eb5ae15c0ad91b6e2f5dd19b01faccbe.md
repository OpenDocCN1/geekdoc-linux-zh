
`root mkinitrd /boot/initrd2.0.36-0.7`

```
`mkinitrd` 会评估 `/etc/conf.modules` 中的信息。如果启动需要 SCSI 适配器，`conf.modules` 必须包含如下格式的行：
`alias scsi_hostadapter aic7xxx`

> 注意
> 在此启动过程中，Red-Hat 无法简单地将 `/boot/vmlinuz` 拷贝到磁盘并用其启动 SCSI 系统。相反，你必须使用 `initrd=/boot/initrd` 选项，或者编译一个直接集成你显卡 SCSI 支持的新内核。

# 语言设置

简要概述：在每次启动 shell 时，都会执行 `/etc/profile`。Red-Hat 的一个特点是，在该脚本文件中，`/etc/profile.d` 目录下的所有 `*.sh` 文件都会启动。在这些文件中，`lang.sh` 负责设置所需的语言（例如用于 GNOME 菜单文本）。

然而，躲猫游戏远不止此：`lang.sh` 随后返回到 `/etc/sysconfig/i18n`，它是“internationalization”（国际化）的缩写，在 Unix 世界中常用。对该文件的更改必须使用编辑器完成——目前控制面板工具或 `linuxconf` 都无法用于此目的。对于英语（美国/英国），`/etc/sysconfig/i18n` 中的以下设置很有用：

```
# /etc/sysconfig/i18n

LANG=C

LINGUAS=en

LC_ALL=en_US or LC_ALL=en_UK
```

> Note
> 更多信息可以在 GNU `gettext` 的信息文档以及互联网上找到：
`http://www.vlsivie.tuwien.ac.at/mike/i18n.html`

# SuSE 6.1

SuSE 提供德版和国际版（英语命令手册）。SuSE Linux 的主要优势包括：

## YaST (Another Setup Tool)

该程序现在是 SuSE 的中心安装、配置和管理程序。它现在达到了很高的成熟程度，大多数情况下你几乎不需要手动修改配置文件。

## 软件包

许多你原本需要搜索互联网或其它 Linux CD 才能获得的程序都是 SuSE 的组成部分，并可以随时安装。SuSE 完整版本目前包含一千多个预配置的软件软件包。

## 手册

这份极具实践性的手册显然受益于支持部门积累的经验——很少找到针对如此迥异的硬件和软件问题的提示和技巧。

## 互联网上的 SuSE

SuSE 的两个网站地址如下：

```
http://www.suse.de

http://www.suse.com
```

即使你不使用 SuSE，支持和硬件数据库也是非常有价值的机构，它们目前提供多种语言版本，但仅在德国 SuSE 服务器上提供。

# 738 SUSE 6.1

```
http://www.suse.de/Support/sdb_e/

http://cdb.suse.de
```
