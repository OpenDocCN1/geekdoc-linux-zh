
# rpm option packageName

基本选项如下：

- `-i`—安装选定的软件包或包。
- `-e`—擦除（移除）选定的软件包或包。
- `-U`—移除当前安装的包，然后用选定软件包或包的内容安装软件，保留现有的配置文件。
- `-q`—查询系统或选定的软件包或包。
- `-V`—验证已安装或选定的软件包或包。

## 两个实用的选项

在任何选项后附加 `vh`，即可获得一些状态反馈。

`h` 在操作进行时显示哈希标记（hash marks）。

还可以向这些选项添加许多额外的选项或将它们结合使用。它们总结在下表中。

| 选项 | 用途 |
| --- | --- |
| `rpm -i` | 安装软件包 |
| `-i` 的有用选项： | |
| `--excludedocs` | 不安装文档以节省空间。 |
| `--replacekgs` | 用新副本替换该软件包。 |
| `--force` | “大力神锤”——忽略所有警告并强制安装。 |
| `--noscripts` | 不执行任何安装前或安装后置脚本。 |
| `--nodeps` | 忽略任何依赖关系。 |
| `--root path` | 将备根目录设置为 *path*。 |
| `rpm -e` | 擦除（删除）软件包 |
| `-e` 的有用选项： | |
| `--nodeps` | 忽略任何依赖关系。 |
| `rpm -U` | 升级软件包，移除旧版本但保留已修改的文件（如配置文件）。 |
| `-U` 的有用选项： | |
| `--oldpackage` | 允许降级到旧版本。 |
| 其他选项与 `rpm -i` 相同。 |
| `rpm -q` | 查询软件包信息 |
| `-q` 的有用选项： | |
| `-p file` | 显示关于软件包 *file* 的所有信息。 |
| `-f file` | 哪个软件包拥有该 *file*？ |
| `--whatprovides x` | 确定哪些软件包提供了 *x*。 |
| `--requires x` | 确定哪些软件包需要 *x*。 |
| `-i` | 总结软件包信息。 |
| `-l` | 列出软件包的文件。 |
| `--scripts` | 显示任何安装、卸载或验证脚本的内容。 |
| `--provides` | 显示软件包提供的能力。 |
| `--requires` | 显示软件包所需的能力。 |

## rpm -V 根据 RPM 数据库验证软件包

`-V` 的有用选项：

- `-a` 验证所有已安装的软件包。

## rpm -K 使用 GPG 验证下载的软件包。

`-K` 的有用选项：

- `--nosignature` 如果你缺少公共 GPG 加密密钥、未安装 GPG 或在法律上禁止使用 GPG，此仍然会验证软件包的大小和校验。

获取 Fedora Core GPG 加密密钥并使用它的详细信息请参阅 http://www.rpm.org/max-rpm/s1-rpm-checksig-using.rpm-k.html。

> RPM 同样适用于程序员！
> 请记住，RPM 的创建不仅是为了提供一个易于使用的管理工具，还作为开发者用于多平台源码包管理的工具。程序员使用 `rpm` 进行分发，并将使用其 `rpmbuild` 命令以及许多额外的命令行标志。RPM 可用于构建二进制文件、执行程序、测试安装、验证并签名软件包、构建源码包、跟踪版本以及针对特定架构的构建。详情可以在 RPM 主页找到（在本章末尾的“参考”部分）。

## 命令行上的 rpm

由于新的图形界面 RPM 客户端只能安装和卸载 RPM 软件包（目前承诺会有更多功能），你仍然需要从命令行管理 RPM 软件包。你可以通过命令行使用 `rpm` 命令执行所有五个基本操作。本节将介绍如何执行这些操作。它还提供了如何安装、验证、查询、删除和升级软件软件包的示例。

最常见的 `rpm` 操作是软件安装。RPM 是跟踪已安装软件的简单方法，并用于快速移除不需要的软件包。使用 `-i` 选项，配合软件包的完整或部分名称（使用正则表达式）来使用 `rpm` 安装软件。例如，要安装 unwise 归档包，可以使用如下的 `rpm` 命令：

```bash
# rpm -ivh http://mirrors.zoreil.plf.zarb.org/9/1586/unace-2-2plf.1586.rpm
Retrieving http://mirrors.zoreil.plf.zarb.org/9/1586/unace-2-2plf.1586.rpm
```

```bash
warning: /var/tmp/rpm-xfer.48amVs: V3 DSA signature: NOKEY, key ID 8df56d05
Preparing...
#################################### [100%]
1:unace
################################ [100%]
```

此示例使用了 `v` 和 `h` 选项，它们提供了更详细的输出并显示哈希标记以显示安装进度。该示例还演示了 `rpm` 使用 HTTP 或 FIP 服务器获取安装文件的能力。它显示了 `rpm` 可以使用 GPG 密钥来验证文件。（我们的示例中未安装密钥。）

你也可以在安装软件包后使用 `rpm` 查询其数据库以验证安装。使用 `-V` 选项配合软件包名称，在你的系统上验证安装。例如，要验证 unace 归档包，可以使用如下的 `rpm` 命令：

```bash
# rpm -V unace
```

> 注意
> 如果你的软件安装无误，在运行命令后系统对 `rpm -V` 不显示任何响应；只有问题会被显示。

从下面的程序输出可以看出，你可以通过添加额外的验证选项（例如两个验证选项）获取有关软件包的附加信息。要获取已安装软件包的更多信息，请使用 `-q` 选项配合软件包名称。例如，查询 unace 归档包，可以使用如下的 `rpm` 命令：

```bash
# rpm -qi unace
Name: unace
Version: 2.2
Release: 2plf.1586
Size: 401368
OS: linux
Build Date: Sat Mar 01 12:13:48 EST 2003
Install date: Tue Sep 02 14:46:28 EDT
Vendor:
Group: Archiving/Compression
Packager: Guillaume Rousseau <guillomitch@zarp.org>
URL: http://www.ace.com
Summary: Decompressor for .ace archives
Description: Unace 是一个用于用于提取、查看和测试 ACE 归档内容的工具。
```

# 第 8 章 管理软件和系统资源

> 注意
> `rpm` 命令的另一个基本功能是它的 `--rebuilddb` 选项。如果你的系统 RPM 数据库损坏了，这是你恢复软件管理服务的第一个（可能也是唯一的）选项。我们希望你永远不需要使用此选项；请通过始终备份你的数据来确保这一点！

## 使用 RPM 进行软件包组织

在你的 Fedora Core Linux 系统上，软件包被组织成各种组，正如你在本章稍后部分看到的。使用分组组织有助于 Fedora 按类别保持软件的组织，并在使用图形化 RPM 客户端时提供软件的层级列表。你不需要手动操作这些组，但理解软件包组织的概念可以帮助你熟悉 Fedora Core Linux 的工作原理。

## 从 RPM 文件中提取单个文件

有时，从 RPM 软件包中提取单个文件是有用的。你可以通过 Midnight Commander（即 `mc`）的命令行视图来实现这一点。在图 8.1 中，Midnight Commander 正在显示你的 `.rpm` 文件的内容。Midnight Commander 是著名的文件管理实用程序 Dos Norton Commander 的 UNIX 克隆版本。使用 `mc`，只需高亮 RPM 文件并按回车，即可显示 RPM 文件的内容。在列表中，你可以浏览 RPM 文件的文件结构并使用 `mc` 从中复制文件。

![](img/96ce0bc6bd65a9b4c721fc1cd7169438_255_0.png)

图 8.1 经典的双面板目录视图和下拉菜单透露了 Midnight Commander 的 DOS 灵感，但它是一个功能齐全 Linux 文件管理器。

你可能想在安装应用程序之前知道 `.rpm` 脚本将做什么。你可以使用 `mc` 中的 `F3` 键来查看脚本文件。如果你想不使用 `mc` 查看脚本，请使用此命令：

```bash
# rpm -q --scripts filename | scripts.txt
```

此命令将脚本管道到一个文件中，你可以使用文本编辑器对其进行检查。你也可以将其管道到 `less` 分页命令以便在显示器上查看脚本：

```bash
# rpm -q --scripts filename | less
```
