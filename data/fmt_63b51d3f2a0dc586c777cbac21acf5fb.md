
```
[root@server1 conky-1.9.0]# make install
Making install in src
make[1]: Entering directory '/root/conky-1.9.0/src'
install-am
make[2]: Entering directory '/root/conky-1.9.0/src'
make[3]: Entering directory '/root/conky-1.9.0/src'
/usr/bin/mkdir -p '/usr/local/bin'
/bin/sh --mode=install /usr/bin/install -c conky /usr/local/bin
libtool: install:/usr/bin/install -c conky /usr/local/lib/conky
make[3]: Nothing to done for 'install-data'
make[3]: Leaving directory '/root/conky-1.9.0/src'
make[2]: Leaving directory '/root/conky-1.9.0/src'
Making install in doc
make[1]: Entering directory '/root/conky-1.9.0/doc'
make[2]: Entering directory '/root/conky-1.9.0/doc'
make[2]: Nothing to done for 'install-exec'
/usr/bin/mkdir -p '/usr/local/share/man1'
/usr/bin/install -c -m 644 conky.1 '/usr/local/share/man1'
make[2]: Leaving directory '/root/conky-1.9.0/doc'
make[1]: Leaving directory '/root/conky-1.9.0/doc'
```

<此处省略了内容>

```
[root@server1 conky-1.9.0]# cd ..
```

程序文件复制到相应的目录后，你可以删除源码目录和压缩包以找到程序的二进制文件，如下例所示：

```
[root@server1 conky-1.9.0]# rm -rf conky-1.9.0
[root@server1 conky-1.9.0]# rm -f conky-1.9.0.bz2
[root@server1 conky-1.9.0]# /usr/local/bin/conky
```

最后，你可以查看 conky 手页并切换到桌面环境执行程序，如图 11-3 所示。

图 11-3 conky 程序

## 使用红帽软件包管理器 (RPM)

红帽软件包管理器 (RPM) 是通过互联网分发或源自红帽的 Linux 软件最常用的格式。RPM 包文件名标识了软件编译的架构，并以 `.rpm` 扩展结尾。以下输出表示 RPM 包（pager）版本 2.2.12-6 是为 Fedora 36 (fc36) 的 Intel x86_64 平台编译的：

```
[root@server ~]# ls -F
Desktop/
bluefish-2.2.12-6.fc36.rpm
```

安装 RPM 时可以使用 `-i` 选项查看版本信息，并在安装期间分别使用 `-v` 和 `-h` 查看进度。某些 RPM 需要安装其他软件包或共享库，这种关系被称为包依赖。如果你尝试安装具有依赖关系的 RPM，会收到需要安装包和共享库的错误消息。安装这些前提条件后，你可以成功安装所需的 RPM。例如，下载了 Bluefish 编辑器的 RPM 包并运行以下命令进行安装：

```
[root@server ~]# rpm -iv bluefish-2.2.12-6.fc36.x86_64.rpm
Error: Failed dependencies
bluefish-shared is needed by bluefish-2.2.12-6.fc36.x86_64
libglib-2.90.so.7) (64bit) is needed by bluefish-2.2.12-6.fc36.x86_64
```

```
上述输出中的错误表明 Bluefish RPM 包有两个包依赖项，分别为 bluefish-shared 和 libgithub。因此，你必须下载适用于你架构的 bluefish-shared-data 包和 libgithub 共享库（gumarch 包的一部分）。然后你可以运行以下命令安装三个包：
```

```
[root@server1]# rpm -ivh bluefish-2.2.12-6.fc36.x86_64 bluefish-shared-data-2.2.12-6.fc36.noarch gumarch-libs-14.0.3-1.fc36.x86_64

Verifying...

########################### [100%]

Preparing...

########################### [100%]

Installing...

########################### [33%]

1:gumarch-libs-14.0.3-1.fc36

2:bluefish-shared-data-2.2.12-6.fc36 [67%]

3:bluefish-2.2.12-6.fc36

########################### [100%]

[root@server1]#
```

安装 RPM 后，RPM 数据库（存储在 `/var/lib/rpm` 中）会更新，包含有关该包及其包含文件的信息。要查询包名，可以通过以下名称使用 `rpm` 命令的 `-q` (query) 选项：

```
[root@server1]# rpm -q bluefish
bluefish-2.2.12-6.fc36.x86_64
[root@server1]#
```

此外，你可以向查询命令添加 `-i` (info) 选项来显示 bluefish 的详细包信息：

```
[root@server1]# rpm -qi bluefish
Name : bluefish
Version : 2.2.12
Release : 6.fc36
Architecture : x86_64
Install Date : Mon 26 Sep 2023 01:24:29 PM EDT
Group : Unspecified
Size : 1739019
License : GPLv+
Signature : RSA/SHA256, Wed 02 Feb 2023 10:23:18 AM EST, Key ID 999f7cbf38ab71f4
Source RPM : bluefish-2.2.12-6.fc36.src.rpm
Build Date : Wed 02 Feb 2022 10:19:27 AM EST
Build Host : build-x86_15.fedaproject.org
Packager : Fedora Project
Vendor : Fedora Project
URL : http://bluefish.fedaproject.org/bluefish
Bug URL : https://bugs.fedaproject.org/
Summary : web development application for experienced developers
Description :
Bluefish 是一个为 Web 设计师和程序员设计的强大编辑器。Bluefish 支持许多编程语言和标记语言，但它专注于编辑动态和交互式网站。
[root@server1 ~]#
```

# 第11章 压缩、系统备份与软件安装

由于红帽软件包管理器（Red Hat Package Manager）会跟踪所有已安装的文件，你可以使用 RPM 包管理器提供的 `-q` 和 `-l` 来列出软件包包含的所有文件，并找到程序的可执行文件。以下命令列出了 bluefish 包中的前10个文件：

```
[root@server1]# rpm -ql bluefish
/usr/bin/bluefish
/usr/lib64/bluefish
/usr/lib64/bluefish/about.so
/usr/lib64/bluefish/charmap.so
/usr/lib64/bluefish/entities.so
/usr/lib64/bluefish/htmlbrowser.so
/usr/lib64/bluefish/infbrowser.so
/usr/lib64/bluefish/snippets.so
/usr/lib64/bluefish/encoding.so
/usr/share/licenses/bluefish
/usr/share/licenses/bluefish/COPYING
[root@server1]# _
```

从上述输出中，你可以看到程序是 `/usr/bin/bluefish`，它位于 `PATH` 变量中的目录内。在桌面环境中执行时，你会看到图11-4所示的场景。

## 图 11-4 Bluefish 程序

![](img/0065b92b6d2dfbf8ba2a41373880797d_476_0.png)

相反，你可以使用 `-q` 和 `-f`（file）选项后跟文件名来查找哪个 RPM 包包含特定文件：

```
[root@server1]# rpm -qf /usr/bin/bluefish
bluefish-2.12-6.fc36.x86_64
[root@server1]# _
```

## CompTIA Linux+ 和 LPIC-1：Linux 认证指南

要从系统中删除软件包，可以使用 `rpm` 命令的 `-e` 选项；属于该软件包的文件也将将被删除。要删除 bluefish 和 bluefish-shared-data 包并验证删除情况，可以使用以下命令：

```
[root@server1 ~]# rpm -e bluefish bluefish-shared-data
[root@server1 ~]# rpm -q bluefish bluefish-shared-data
```

package bluefish is not installed
package bluefish-shared-data is not installed
[root@server1 ~]#

表 11-8 显示了与 `rpm` 命令一起使用的常用选项列表。

## 表 11-8 `rpm` 命令的常用选项

| 选项 | 描述 |
| --- | --- |
| -a --all | 显示系统中安装的所有软件包名称（与 `-q` 选项配合使用时）。 |
| -c --configfiles | 显示系统中已安装软件包的配置文件的位置（与 `-q` 选项配合使用时）。 |
| -d --dump | 显示有关已安装软件包配置文件的详细信息（在跟随 `-q` 和 `-c` 选项后使用时）。 |
| -e --erase | 从系统中删除指定的软件包。 |
| -F | 仅在存在旧版本时才升级指定的软件包。 |
| --freshen |  |
| -f --file | 显示指定文件所属的软件包（与 `-q` 选项配合使用时）。 |
| -h --hash | 在屏幕上打印标记以指示安装进度（与 `-i` 选项配合使用时）。 |
| -i --install | 安装指定的软件包（前提是不使用 `-q` 选项）。 |
| -i --info | 显示关于软件包的完整信息（与 `-q` 选项配合使用时）。 |
| -K | 在文件名参数之前使用时，会验证 RPM 文件中列出的校验和。 |
| -l --list | 列出指定软件包的文件名（与 `-q` 选项配合使用时）。 |
| --nodeps | 强制 RPM 在安装软件包前避免检查依赖关系（与 `-i` 选项配合使用时）。 |
| -q --query | 查询系统中软件包的软件包信息。 |
| --test | 执行测试安装（与 `-i` 选项配合使用时）。 |
| -U --upgrade | 升级指定的软件包；即使系统中没有旧版本，也会安装该软件包。 |
| -V --verify | 验证所有属于指定软件包的文件的位置。 |
| -v | 在安装或操作软件包时打印详细的输出信息。 |

# 第11章 压缩、系统备份与软件安装

# 注意事项 30

RPM 软件包还可以使用 `rpmcpio command` 转换为 cpio 归档。这允许你在不在系统中安装软件包的情况下，轻松地检查或从 RPM 包中提取文件。

互联网上被称为软件仓库的数千个不同的免费下载的 RPM 软件包。此外，软件仓库中的每个 RPM 可能都有多个软件包依赖关系。幸运的是，你可以使用 Yum Updater Modified 命令在互联网上搜索与你的架构匹配的软件包，并自动在你的系统上安装或升级软件包。在安装所需的 RPM 软件包之前，`yum` 还会下载并安装任何依赖项。`/etc/yum.conf` 和 `/etc/yum.repos.d/` 文件用于指定软件仓库的位置。

虽然许多 Linux 发行版仍使用 `yum` 命令，但许多其他 Linux 发行版使用 `dnf` 命令以及存储在 `/etc/dnf/conf` 和 `/etc/dnf/repos.d/` 文件中的仓库信息。

# 注意事项 31

`dnf` 命令是 `yum` 命令的简化版本，提供了相同的选项。

# 注意事项 32

SUSE 发行版使用 `zypper` 命令。

# 注意事项 33

安装特定的 RPM 软件包并可以使用 `dnf`。

# 注意事项 34

由于新版本的 RPM 软件包经常添加到软件仓库，为了升级软件包到最新版本可以使用 `dnf`。

## 第11章 压缩、系统备份与软件安装

465

### 备注 36

如果软件包升级包含新版本的配置文件

从之前的输出可以看出，`dnf` 命令升级了相关的内核模块（因为内核模块特定于内核版本）以及 `kernel-core` 软件包的依赖项。你可能还会发现 `dnf` 命令会尝试多个不同的软件仓库来查找软件（例如`软件镜像`），找到一个允许你的并发下载连接的镜像以进行下载。当某个软件仓库达到其连接限制时，它会向 `dnf` 命令返回负响应，然后 `dnf` 命令将在仓库配置文件中列出的下一个镜像中搜索 RPM 软件包。

在某些情况下，你可能找不到用于 `dnf` 命令的确切包名。幸运的是，你可以使用 `dnf search keyword` 来通过关键词搜索软件仓库，或者使用可用的 `dnf list` 列出可用的 RPM 软件包。可选 `dnf grouplist` 将显示可安装的组名称列表。软件包组是一组相关的软件包，它们通常会被一起安装以提供核心功能。例如，要在 Fedora Linux 上安装 Tools 软件包组（包含一组开发库和工具），你可以使用 `dnf groupinstall`。

你可以使用 `dnf` 命令查看在 `/etc/dnf/dnf.conf` 和 `/etc/yum.repos/` 文件中配置的软件仓库。许多软件作者将其 RPM 软件包放在私有仓库中，并提供指导你完成将私有软件仓库添加到你的仓库配置文件的指令（通常是安装一个特殊的 RPM 软件包）。例如，某个软件包的网站可能会指示你运行 `dnf install https://website/fedora.noarch` 命令，将适当的文件安装到 `/etc/yum.repo.d` 目录，该目录列出了包含 Fedora Linux 软件包仓库的位置。接下来，你可以运行 `dnf install packageName` 来安装该软件包。

### 备注 37

dnf 缓存目录缓存了仓库信息。你可以运行 `dnf clean` 命令来清除这些缓存，这通常用于解决与 dnf 相关的问题。

`dnf` 命令也可用于管理和安装 RPM 软件包。`dnf list installed` 将列出已安装的 RPM 软件包，`dnf grouplist installed` 将列出已安装的组，`dnf info packageName` 将显示安装 RPM 软件包的详细信息，`dnf groupinfo` 命令将显示软件包组的内容。你还可以使用 `dnf remove` 命令删除已安装的 RPM 软件包，并使用 `dnf groupremove packagegroup` 命令删除特定软件包组中的所有 RPM 软件包。

每个 Linux 发行版都包含一个软件包，为桌面用户提供了一种管理软件系统以及从网上可用软件仓库安装更新软件包的方法。同样，下载到桌面环境的任何软件包都由此图形应用程序生成，它会在安装之前自动下载并安装依赖项。在 Fedora Linux 上，图 11-5 所示的图形化软件（Software）工具用于在桌面环境中查看、管理和安装软件。要在 GNOME 中启动软件工具，请导航到活动 (Activities)”、“显示应用程序 (Show Applications)”、“软件 (Software)。

### 图 11-5 工具

![](img/0065b92b6d2dfbf8ba2a41373880797d_481_0.png)

## 使用 Debian 软件包管理器 (DPM)
