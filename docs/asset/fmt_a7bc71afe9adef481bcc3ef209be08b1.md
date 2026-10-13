
与 FEDORA AND LINUX 相关的命令

你可以使用这些命令在 Fedora 中创建和配置 X Window 系统：
- `xorg`--由 The X.Org Foundation 提供的 X Window System 发行版中的 X 服务器
- `mouseconfig`--Fedora 的基于文本的 GUI 指针设备配置程序
- `kcontrol`--KDE 控制中心客户端
- `system-config-display`--Fedora 的图形化 X11R7 配置工具
- `system-config-mouse`—Fedora 的图形化鼠标配置工具
- `gdmsetup`—GNOME 显示管理器配置客户端
- `startx`—一个用于从 shell 命令行启动一个或多个 X 会话的 shell脚本
- `xsri`—显示管理器根桌面装饰客户端

![](img/c4a0ea5ab3561ff33a8da88887702720_226_0.png)

图 6.12 你可以使用 KDE 控制中心管理 KDE 桌面会话的每一个方面。

## 参考

- http://www.x.org/—X Window 系统的维护者。
- http://www.x.org/Downloads_mirror.html—想下载 X 的最新修订源码吗？从这个镜像站点列表开始。
- http://www.xfree86.org/—The XFree86 Project, Inc. 的主页，近 10 年来为 Linux 提供了图形界面。
- http://www.kde.org/—学习 KDE 及其最新进展的地方。
- http://www.gnome.org/—获取更多 GNOME 信息的启动点、新客户端链接以及 GNOME 开发项目链接。
- http://people.redhat.com/~-hp/metacity/—Havoc Pennington 的 metacity 下载页面，你可以在这里获取此窗口管理器的最新全源码版本。
- http://sawmill.sourceforge.net/—sawfish 窗口管理器（以前称为 sawmill）的主页。
- http://www.icewm.org/—最新版本 Window Maker 的源码。
- http://www.icewm.org/—IceWM 主页。
- http://www.lesstif.org/—LessTif 项目的主页，其目的是提供 OS/Motif 兼容库的 GNU GPL 版本。
- http://scwm.sourceforge.net/—scwm 主页。
- http://www.icewm.org/—FVWM 的主页。
- http://www.novell.com/products/desktop/—GNOME 软件包。

# 第 7 章 管理软件包

在 2003 年 8 月，Ximian 被 Novell, Inc. 收购。Ximian GNOME 发行版（现名为 Ximian Desktop 2）未包含在 Red Hat 的 Enterprise Linux 发行版或 Fedora 中，但你可能可以通过 CD-ROM 安装它，或者如果你有宽带，可以在互联网上花费一小时或更短的时间完成。该版本适用于许多不同的 Linux 发行版（即使是非 Intel 平台的版本也是如此）。

已安装软件的主数据库数据库包含在命名的软件包中。正如从前面的示例可以看出，如果你执行了完整安装（超过 4GB 软件），此数据库可能会增长到 37MB（甚至更大）。安装 Fedora 后，`rpm` 和相关命令将在软件管理操作期间使用此目录。

## 命令行系统管理员，RPM 客户端

作为 Fedora 用户，你将使用 `rpm` 命令或 Fedora Core 图形化客户端来执行五项基本任务之一。这些操作必须由 root（根）操作员执行，包括以下内容：

- 安装新软件
- 删除或移除过时或不需要的软件包
- 升级已安装的软件包
- 查询以获取有关软件包的信息
- 验证软件包安装的正确性或完整性

`rpm` 命令有超过 60 种命令行选项，但其管理功能可以根据上述五类操作进行分组。图形化 RPM 客户端为这些操作提供了易于使用的界面。作为系统管理员，你可以在使用图形界面和使用 `rpm` 的各种命令行选项之间进行选择。`rpm` 命令的一般格式为：

```
# rpm option packageName
```

基本选项如下：

- `-i`—安装所选的包或包
- `-e`—删除（移除）所选的包或包
- `-u`—移除当前安装的包，然后使用所选包或包的内容安装软件，同时保留现有的配置文件
- `-q`—查询系统或所选的包或包
- `-V`—验证已安装或所选的包或包

## 实用的选项

通过在任何选项后添加 `v`，你可以获得：

- `v` 某些状态反馈
- `h` 随着工作进行显示哈希标记（hash marks）

还可以向这些选项添加或结合使用许多附加选项。这些总结在下表中：

| 选项 | 用途 |
| --- | --- |
| `rpm -i` | 安装软件包。<br>`-i` 的有用选项：<br>`- --excludedocs`: 不安装文档以节省空间。<br>`- --replacepkgs`: 用包的新副本替换该包。<br>`- --force`: “大铁锤”——忽略所有警告并强制安装。<br>`- --noscript`: 不执行任何安装前或安装后脚本。<br>`- --nodepends`: 忽略依赖关系。<br>`- --root path`: 设置备用根目录为路径。 |
| `rpm -e` | 擦除（删除）软件包。<br>`-e` 的有用选项：<br>`- --nodepends`: 忽略依赖关系。 |
| `rpm -U` | 升级软件包，移除旧版本但保留修改过的文件（如配置）。<br>`-U` 的有用选项：<br>`- --oldpackage`: 允许降级到旧版本。<br>其他选项与 `rpm -i` 相同。 |
| `rpm -q` | 查询软件包信息<br>`-q` 的有用选项：<br>`- -file`: 显示关于软件包文件的所有信息。<br>`- -f`: 哪个包拥有该文件？<br>`- --whatprovides x`: 确定哪些包提供了 x。<br>`- --whatrequires x`: 确定哪些包需要 x。<br>`- -i`: 汇总软件包信息。<br>`- -l`: 列出包文件。<br>`- --scripts`: 显示任何安装、卸载或验证脚本的内容。<br>`- --provides`: 显示包提供的能力。<br>`- --requires`: 显示包需要的能力。 |
| `rpm -V` | 根据 RPM 数据库验证软件包<br>`-V` 的有用选项：<br>`- -a`: 验证所有安装的包。 |
| `rpm -K` | 使用 GPG 验证下载的包。<br>`-k` 的有用选项：<br>`- --nosignature`: 如果你缺少 GPG 公密密钥，或者没有安装 GPG，或者被法律禁止使用 GPG，此仍将使用大小和 MDS 校验和来验证包。 |

关于获取 Fedora 公用 GPG 加密密钥及其使用方法的详情可见 http://rpm.org/max-rpm/s1-rpm-checking-rpm-k.html。

## RPM 也也适用于程序员！

请记住，RPM 的创建不仅是为了提供一个易于使用的管理工具，还作为开发人员工具用于多平台源码包管理。使用 `rpm` 进行开发和分发将使用其 `rpmbuild` 命令，带有许多额外的命令行标记。RPM 可用于构建二进制文件、执行程序、测试安装、验证并签名包、构建源码包、跟踪版本以及针对特定架构的构建。详情可以在 RPM 主页找到（列在本章的“参考”部分）。

## 在命令行使用 rpm

由于新的 RPM 客户端目前只能安装和卸载 RPM 包（目前——承诺会有更多功能），你仍然需要从命令行管理 RPM 软件包。你可以通过命令行使用 `rpm` 命令执行所有五个基本 rpm 操作。本节将介绍如何执行这些操作。它还提供了如何安装、查询、移除和升级软件包的示例。

最常用的操作是软件安装。使用 `rpm` 是跟踪已安装软件的简单方法，并可快速移除不需要的包。使用 `-i` 选项，配合软件包的完整或部分名称（使用正则表达式），通过 `rpm` 安装软件。例如，安装 unace 归档包，可以使用如下 `rpm` 命令：

```
# rpm -ivh http://mirrors.zoreil.plf.zarb.org/mandrake/10.0/
1586/unace-2.2-2plif.1586.rpm

Retrieving http://mirrors.zoreil.plf.zarb.org/mandrake/10.0/
1586/unace-2.2-2plif.1586.rpm

warning: ...
```

此示例使用了 `v` 和 `h` 选项，它们提供了更详细的输出和显示进度的哈希标记。它还证明了 `rpm` 可以使用 GPG 密钥来验证文件。如果安装一切正确，系统对 `-V` 将没有响应。例如，要验证 unace 归档包，可以使用如下 `rpm` 命令：

```
# rpm -V unace
```
