
例如，要为 64 位机器创建发行版，你会在 `pungi.conf` 中指定 `x86_64` 选项。确保 pungi 配置中的 `yum.conf` 选项被设置为 `yum.conf.x86_64` 文件。64 位架构使用 64 位 Yum 仓库，而 pcc 架构将使用 pcc 仓库。在你的 `pungi.conf` 文件中，确保 `arch` 选项设置为与 `yum.conf` 选项使用的相同架构。64 位架构的 `arch` 选项将使用 Yum 64 位仓库 `yum.conf.x86_64`。对于源代码，你会使用 source 架构以及你所需的架构相应的 Yum 配置文件。

默认的 Pungi 配置位于 `/etc/pungi/pungi.conf`。在这里你会找到创建发行版变体（spin）的选项。如果你想进行更改，可以还原原始文件或创建一个副本并进行编辑。通过 `--conf` 选项，你可以指定你的新 Pungi 配置。无论如何，请确保保留一份原始 `pungi.conf` 文件的备份供参考。Pungi 选项如表 2-1 所示。

默认 `pungi.conf` 所示：

```
pungi.conf
product_name = Fedora ; 安装期间使用的名称
product_path = Fedora ; RPM 存放的目录
iso_base = F ; ISO 文件名的第一部分
bugurl = http://bugzilla.redhat.com ; 用于错误报告
comps = /etc/pungi/comps ; 软件包组和默认安装
manifest = /etc/pungi/minimal-manifest ; 决定构建内容
yumconf = /etc/pungi/yum.conf.x86_64 ; 从哪里获取包
destdir = /srv/pungi/dest ; 顶层配置目录，必须保持清洁
cachedir = /srv/pungi/cache ; 重复运行的缓存
arch = x86_64 ; 要组合的架构（必须与系统架构相同）
version = 7 ; 用于安装并作为目标树的一部分
flavors = custom ; 针对特定包集合的补丁
discs = 1 ; 容纳所需的磁盘数量
cdsize = 4680.0 ; 如果磁盘数量为 1 则不使用
getsource = YES ; 用于确定是否需要源码包
```

要收集到发行版中的文件列在 `pungi.conf` 中 `manifest` 选项指定的 manifest 文件中。默认设置为 `/etc/pungi/minimal-manifest`，它包含了任何发行版所需的最小软件包集。然后你可以向其添加内容或更改某些设置。策略是复制 `minimal-manifest` 文件并对其进行修改。然后让生成的副本作为 Pungi 使用的 manifest 文件，并将 `manifest` 选项指向该文件。收集的包将列在你的目标目录中。你可以检查它们以查看你的发行版具体包含哪些。

| 选项 | 描述 |

|---|---|

| product_name | 安装期间使用的名称；默认为 Fedora。 |

| product_path | RPM 存放的目录；默认为 Fedora。 |

| iso_basename | ISO 文件名的第一部分；默认为 F。 |

| bugurl | 用于错误报告；默认是 http://bugzilla.redhat.com |

| comps | 用于定义软件包分组和默认安装；Fedora 7 默认是 /etc/pungi/comps-fc7.xml。 |

| manifest | 用于确定构建内容。支持 kickstart 语法；默认是 /etc/pungi/minimal-manifest，也位于 /etc/pungi 中。 |

| yumconf | 指定带有用于收集包的 Yum 仓库的 Yum 配置文件。确保区分架构：i386、x86_64、ppc。默认配置文件以 yum.conf 为前缀，带有发行版名称和架构，32 位系统为 yum.conf.fc7.i386 |

| destdir | 顶层目录，必须保持清洁；Pungi 命令选项默认为 /srv/pungi/destdir。 |

| cachedir | 重复运行的缓存；默认是 /srv/pungi/cache。 |

| arch | 要组合的内容（必须与系统架构一致），使用与当前相同的架构，64 位使用 x86_64，32 位使用 i386。 |

| version | 用于安装并作为目标树的一部分。Fedora 7 的默认值为 7。 |

| flavor | 进一步定义选定的包集合；默认为 Custom。 |

| discs | 容纳数据所需的磁盘数量；默认为 1 |

| cdsize | 如果磁盘数量为 1 则不使用，默认被注释掉；默认值为 4608.0。 |

| getsource | 用于确定是否需要源码包；默认是 YES。 |

表 2-1 Pungi 选项

`minimal-manifest` 文件的副本所示。软件包包括内核、Xorg Server 驱动和字体、SELinux 标记策略、GRUB 启动加载程序、Man 页面和 joe 编辑器。

`/etc/pungi/minimal-manifest`

```
kernel
xorg-x11-fonts-ISO88859-1-75dpi
busbox-xorg-anaconda
dejava-lgc-fonts
xorg-x11-fonts-base
memtest86+
xorg-x11-drivers
selinux-policy-targeted
anaconda-runtime
man
joe
grub
```

manifest 文件使用与 kickstart 相同的语法。在以下示例中使用的软件包组，**my-manifest** 文件将使用 GNOME 桌面环境和 Windows 文件服务器 (Samba) 组中的所有包。Editors 是 Applications 的一个子组。所有依赖软件（例如桌面所需的 X Windows 系统）都将自动包含，对于桌面来说，包含 X Windows 系统会有帮助。请务必使用与“添加/删除软件”中完全相同的名称，例如 `@GNOME Desktop Environment`，而不仅仅是 GNOME。你应该使用 KDE 桌面而不是 GNOME 桌面，即 `@K` (K Desktop Environment)。在 `comps` 文件中指定的组都将包含在磁盘中。这是一个 XML 文件，你可以修改它来添加自己的组。这里显示了一个使用组指定软件包的 manifest 文件。

```
+ /etc/pungi/my-manifest
kernel
busbox-anaconda
dejavu-lgc-fonts
memtest86+
selinux-policy-targeted
anaconda-runtime
man
@ Window System
@GNOME Desktop Environment
@Editors
@Windows File Server
grub
```

> **提示** 下载的包由 Pungi 保留在 `/etc/pungi/cache` 中。如果你通过添加新包来生成新版本，Pungi 将利用缓存目录中已有的的包，因此你不需要重新下载它们。

如果你想包含由 Livna 提供的供应商驱动程序，或带有 DVD 支持的 MPlayer 等多媒体软件，你将必须修改 pungi Yum 配置文件，以包含你想要的第三方仓库 Yum 配置。这只需编辑 Yum 配置文件并从 `/etc/yum.repos.d/` 目录中的第三方仓库文件进行复制粘贴即可。例如，要添加对 Livna 仓库的支持，你会编辑 `/etc/yum.repos.d/livna.repo` 文件，复制其内容并粘贴到你的 `/etc/pungi` Yum 配置文件的底部。然后你可以在你的 Pungi manifest 文件指定 Livna 包，例如用于 NVIDIA 供应商图形驱动的 `knvidia` 或用于 MPlayer 的 `mplayer`。你可以对 **freshrpm.repo** 文件执行相同的操作，以便访问 Freshrpm 仓库中的包。

# 54 第一部分：入门

Pungi 会通过不同的阶段来创建你的定制版本（spin）。你可以使用 `--all-stages` 选项让 Pungi 一次完成所有这些阶段，也可以逐阶段进行。每个阶段都有相应的选项：

- 收集 (Gather), `-G`：第一个 Pungi 将收集安装到你的版本所需的软件包。这些包将从 Fedora 存储库下载。

- 构建安装 (BuildInstall), `-B`：在构建阶段，收集到的包将与 Anaconda 同步以安装。

- 软件包排序 (Package Order), `-P`：将安装包组织成 Anaconda 可以安装的序列，确保按照需要优先安装包。

- 拆分树 (SplitTree), `-S`：如果包集合太大无法放入单张光盘，拆分树将精确地拆分集合。
