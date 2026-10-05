

## deb 文件

dpkg 管理系统处理 `.deb` 格式的文件，这些文件通常被称为 deb 文件。dpkg 无法从仓库下载 deb 文件，aptitude（第 526 页）通常会执行此任务。默认情况下，aptitude 下载的 deb 文件存储在 `/var/cache/apt/archives` 中。dpkg 管理系统将可用的软件包信息存储在 `/var/lib/dpkg/available` 中，将安装状态信息存储在 `/var/lib/dpkg/status` 中。

你可以管理、下载和安装 deb 文件。然而，这样做可能会非常繁琐，尤其是当你发现一个包依赖于几个其他包，而其中某些包又依赖于其他包时。

在构建内核时，你可以创建 deb 文件。第 579 页提供了一个构建内核 deb 文件的示例：第 536 页和 582 页显示了如何使用 dpkg 安装 deb 文件。

### 二进制文件
一个 deb 文件可以包含以下组件，这些组件使用 `ar`（归档）工具进行打包和解包。所有包都包含一个可执行文件；其他组件是可选的。

- binary—二进制可执行文件
- control—软件包信息，包括依赖、推荐和建议包的列表
- configfiles—软件包配置文件
- preinst—安装前脚本
- postinst—安装后脚本
- prerm—移除前脚本
- postrm—移除后脚本

要解包 deb 文件，首先使用命令 `aptitude download package` 将其下载到 `/var/cache/apt/archives`。将该文件复制到一个不包含其他文件的目录中，并使用 `ar -xv` 解压 deb 文件。然后你可以使用 `tar`（第 176 页）来解压 tar 文件。示例显示了如何从 `nfs-common` deb 文件中提取 `control` 文件。

```
$ ls nfs-common*deb
nfs-common_1~31.2.0~ubuntu2_i386.deb
$ sudo ar -xv nfs-common*deb
x - debian-binary
x - control.tar.gz
x - data.tar.gz
$ sudo tar -xvf control.tar.gz /
./.postinst
./.preinst
./.prerm
./.postrm
./.configfiles
./.md5
./.control
```

### 源文件
源文件包包含一个描述文件、源代码文件和一个包含针对 Ubuntu 的源文件更改的 diff 文件。请参见第 532 页关于如何使用 `apt-get` 下载和解包源文件的说明。

### 安装 deb
当 dpkg 安装二进制包（第 536 页）时，它会执行以下步骤：

1. 提取控制文件。
2. 如果系统中已安装相同包的其他版本，则执行旧包的 `prerm` 脚本。
3. 运行 `preinst` 脚本。
4. 备份旧的二进制文件并解压新的二进制文件，以便 dpkg 在安装失败时恢复到现有设置。
5. 如果系统中已安装相同包的其他版本，则执行旧包的 `postrm` 脚本。
6. 备份旧的配置文件并解压新的配置文件，以便 dpkg 在安装失败时恢复到现有设置。
7. 运行 `postinst` 脚本。

### 移除 deb
当 dpkg 移除二进制包（第 536 页）时，它会运行 `prerm` 脚本，移除文件并运行 `postrm` 脚本。

## dpkg: DEBIAN 软件包管理系统的基础

dpkg（debian package）工具用于安装（解包和配置）、查询和移除软件包。在查询软件包数据库之前，运行 `update-avail` 命令（下文将讨论）来更新可用软件包列表。

## dpkg 命令和选项均以连字符开头

> 提示：虽然以一个或两个连字符开头的命令行参数通常称为选项，但 dpkg 文档将它们分为命令和选项。例如，`--purge` 是一个命令，而 `--simulate` 是一个选项。

通常你将使用其中一个工具（由于你提供的原始文本在多处中断，此处根据上下文结束了已有部分的翻译）。
