
```bash
$ su -c 'yum install tsclient'
Password:
Loaded plugins: refresh-packagekit
Setting up Install Process
Resolving Dependencies
--> Running transaction check
--> Package tsclient.i386 0:2.0.1-2.fc10 set to be updated
--> Processing Dependency: rdesktop >= 1.3.0 for package:tsclient-
2.0.1-2.fc10.i386
--> Processing Dependency: vnc >= 4.0 for package: tsclient-2.0.1-2.fc10.i386
--> Running transaction check
--> Package rdesktop.i386 0:1.6.0-2.fc10 set to be updated
--> Package vnc.i386 0:4.1.3-1.fc10 set to be updated
--> Processing Dependency: librfb.so.0 for package: vnc-4.1.3-1.fc10.i386
--> Running transaction check
--> Package vnc-libs.i386 0:4.1.3-1.fc10 set to be updated
--> Finished Dependency Resolution
Dependencies Resolved
====================================================================================================
 Package Arch Version Repository Size
====================================================================================================
Installing:
 tsclient i386 2.0.1-2.fc10 fedora 106 k
Installing for dependencies: rdesktop i386 1.6.0-2.fc10 fedora 147 k
 vnc i386 4.1.3-1.fc10 updates 90 k
 vnc-libs i386 4.1.3-1.fc10 updates 167 k
Transaction Summary
====================================================================================================
 Install 4 Package(s)
 Update 0 Package(s)
 Remove 0 Package(s)
Total download size: 509 k
Is this ok [y/N]: y
Downloading Packages:
(1/4): rdesktop-1.6.0-2.fc10.i386.rpm | 147 kB 00:00
(2/4): tsclient-2.0.1-2.fc10.i386.rpm     |  106 kB  00:00
(3/4): vnc-4.1.3-1.fc10.i386.rpm           |   90 kB  00:00
(4/4): vnc-libs-4.1.3-1.fc10.i386.rpm       |  167 kB  00:00
--------------------------------------------------------------------------------
Total                                           225 kB/s |  509 kB     00:02
Running rpm_check_debug
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction
    Installing     : vnc-libs-4.1.3-1.fc10.i386            1/4
    Installing     : vnc-4.1.3-1.fc10.i386                 2/4
    Installing     : rdesktop-1.6.0-2.fc10.i386            3/4
    Installing     : tsclient-2.0.1-2.fc10.i386            4/4

Installed:
  tsclient.i386 0:2.0.1-2.fc10

Dependency Installed:
  rdesktop.i386 0:1.6.0-2.fc10     vnc.i386 0:4.1.3-1.fc10
  vnc-libs.i386 0:4.1.3-1.fc10
Complete!
```

正如你所见，`tsclient` 的安装始于检查此次安装所需的软件包，或者更确切地说，是检查该软件的依赖项。这导致了两个依赖项：`VNC` 和 `rdesktop`，而后者又需要一个额外的库。依赖项检查需要是递归的，因此，必须安装的每个新软件包都会检查其依赖项，依此类推。对于一个大型且复杂的软件包（例如，安装 `KDE` 或 `GNOME` 环境），这可能会导致大量的依赖项。

> **考试警告**
>
> 当你安装一个服务时，`Linux` 系统不会启动它。你必须配置该服务以便在启动时运行，这可以通过使用 `chkconfig` 和 `service` 命令从命令行实现。

### 更新软件

要更新已安装的软件包，你可以使用 `yum` 中的更新选项。例如，要更新 `tsclient` 软件包，你会输入命令 `su -c 'yum update tsclient'`。如果软件未安装，系统会通知用户，如下所示：

```bash
$ su -c 'yum update tsclient'
Password:
Loaded plugins: refresh-packagekit
Setting up Update Process
Package(s) tsclient available, but not installed.
No Packages Marked for Update
```

如果正在更新的软件当前被系统使用，则需要在使更新生效之前重启应用程序或服务。

也可以使用 `yum` 更新内核，并且这些内核只有在系统重启后才会生效。当内核更新时，`yum` 会保留旧版本，以便在新内核出现错误时可以引导到旧内核。只保留当前版本和前一版本。

软件包组也可以更新，例如，使用命令 `su -c 'yum groupupdate "MySQL Database"'` 更新 `MySQL Database` 软件包组。

### 移除软件

使用 `remove` 选项可以实现软件的移除。同样，软件包和软件包组都可以被移除。当调用此命令时，`yum` 将检查软件包及其依赖项，并将两者都移除。

```bash
su -c 'yum remove firefox'
su -c 'yum groupremove "MySQL Database"'
```

当 `yum` 移除软件包时，它会保留任何用户数据，但配置文件可能会被移除。

## `deb`

`Debian` 衍生版本的 `Linux` 基于 `GNU` 项目，该项目始于 1984 年，旨在生产一个开源的类 `Unix` 操作系统。虽然它常被称为 `Linux`，但正确的名称是 `Debian GNU/Linux`，因为它结合了两者。当前版本的 `Debian` 包含超过 25,000 个软件包。`Debian` 软件包可以被视为类似于 `rpm` 软件包，因为它们是预编译的，便于在目标系统上安装。

`Debian` 软件包网站 [http://packages.debian.org] 提供三个主要的软件包库：

- **稳定库** 经过充分测试，并且仅出于安全或重大错误修复的目的进行更改。
- **测试库** 已经进行了大量测试，并预定在下一个发行版中发布。
- **不稳定库** 测试较少，很可能包含可能导致系统不稳定的错误。

`Debian` 软件包管理器的低级或基础工具是命令 `dpkg`。下面将讨论此命令及其主要选项。除了该工具外，还有许多更高级的工具，例如 `APT`，它们可以从许多位置获取软件包。此外，还有一个名为 `aptitude` 的工具，它具有更简单和友好的用户界面。

### 使用 `dpkg` 安装软件包

使用 `Debian` 软件包管理器安装基本软件包的过程与前面部分中使用的 `RPM` 非常相似。要安装软件包，请使用以下内容：

```bash
dpkg -i package_name
```

与上面的 `rpm` 一样，你需要拥有超级用户权限才能运行该命令。如果没有，将显示以下错误消息：

```bash
dpkg: requested operation requires superuser privilege
```

### 使用 `dpkg` 移除软件包

使用 `-r` 选项可以轻松移除软件包：

```bash
dpkg -r package_name
```

此选项将计算机上的配置文件保留，以便稍后更容易重新安装。如果你也想擦除配置文件，可以添加 `--purge` 选项。

## 高级打包工具

`Debian` 的另一个软件包管理工具是 `APT` 或高级打包工具，它旨在促进软件包的管理。`APT` 配置文件的默认位置是 `/etc/apt`。`APT` 维护着一个可以从中获取软件包的位置列表，该列表位于 `/etc/apt/sources.list`，部分内容如下所示：

```bash
#
###### deb cdrom:[Debian GNU/Linux 5.0.1 _Lenny_ - Official i386 DVD Binary-1 20090413-00:33]/ lenny contrib main

deb cdrom:[Debian GNU/Linux 5.0.1 _Lenny_ - Official i386 DVD Binary-1 20090413-00:33]/ lenny contrib main
deb http://security.debian.org/ lenny/updates main contrib
deb-src http://security.debian.org/ lenny/updates main contrib
deb http://volatile.debian.org/debian-volatile lenny/volatile main contrib
deb-src http://volatile.debian.org/debian-volatile lenny/volatile main contrib
```

`APT` 维护了一个内部数据库，用于跟踪当前已安装的软件包、未安装的软件包以及可安装的软件包。你可以使用 `apt-get` 命令来查询此数据库，安装和删除软件包，以及检查软件包中的依赖项。由于当添加新软件包和新依赖关系生效时，此列表会发生变化，因此需要更新该列表。可以使用以下命令来实现更新：

```bash
apt-get update
```

### 安装软件包

可以使用 `install` 选项安装软件包，其通用语法为：

```bash
apt-get install package_name(s)
```

当安装 `abiword` 软件包时，输出结果的第一部分示例如下：

```text
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following extra packages will be installed:
  abiword-common abiword-help abfonts abiword-plugin-grammar abiword-plugin-mathview
  aspell-en-doc-base latex-xft-fonts libaiksaurus-1.2-0c2a
  libaiksaurus-1.2-data libaiksauruskat-1.2-0c2a libfreetype-perl
  libfribidi0 libgdom2-0 libgdom2-cpp-smart0c2a libgoffice-0-4
  libgoffice-0-common libgsl-gnome-1-l14 libgtkmathview0c2a liblink-grammar4
  libloudmouth-1-0 libmdbm-perl libots0 libti-5 libuuid-perl libwww-1-2-3
  link-grammar-dictionaries-en
Suggested packages:
  abiword-plugin-goffice
The following NEW packages will be installed:
  abiword abiword-common abiword-help abiword-plugin-grammar
  abiword-plugin-mathview aspell-en-doc-base latex-xft-fonts
  libaiksaurus-1.2-0c2a libaiksaurus-1.2-data libaiksauruskat-1.2-0c2a
  libfreetype-perl libfribidi0 libgdom2-cpp-smart0c2a libgoffice-0-4
  libgoffice-0-common libgsl-gnome-1-l14 libgtkmathview0c2a
```

```text
liblink-grammar4 libloudmouth-1-0 libmdbm-perl libots0 libti-5 libuuid-perl
libwww-1-2-3 link-grammar-dictionaries-en
0 upgraded, 27 newly installed, 0 to remove and 0 not upgraded.
Need to get 0B/9858kB of archives.
After this operation, 31.3MB of additional disk space will be used.
Do you want to continue [Y/n]? y
Selecting previously deselected package libaiksaurus-1.2-data.
(Reading database ... 95088 files and directories currently installed.)
Unpacking libaiksaurus-1.2-data (from .../libaiksaurus-1.2-data-1.2.1+dev-0.12-
6_all.deb) ...
```

这将调用 `apt-get` 在数据库中搜索该软件包的最新版本，然后从 `/etc/apt/sources.list` 中指定的位置检索它，如果存在依赖项，则同时安装这些依赖软件包。在 `install` 选项中可以使用 `-y` 选项，自动对所有查询回答“是”，以减少用户交互。如果你希望确保文件是最新可用的版本，或者怀疑某些文件已损坏，你也可以重新安装软件包。

```bash
apt-get --reinstall install package_name(s)
```

你可以使用 `install` 选项中的 `-d` 选项下载软件包以便稍后安装。这些文件存储在 `/var/cache/apt/archives` 目录中。

```bash
apt-get -d install package_name(s)
```

### 移除软件包

使用 `remove` 选项从系统中移除软件包。

```bash
apt-get remove package_name(s)
```

该软件包将被移除，连同所有依赖于它的软件包一并移除。配置文件不会被移除，但添加 `--purge` 选项将移除与该软件包相关的所有文件。如果你确定将来不会使用该软件包，使用 `purge` 选项是很有价值的，因为它可以清理磁盘，不会在文件系统中留下大量不需要的文件。

### 高级安装和移除

你可以在同一命令行中安装和移除软件包。例如，要在安装软件包时移除某个 [或某些] 软件包，只需在软件包名称后加后缀“-”，该命令的语法看起来像这样：

```bash
apt-get install newpackage oldpackage-
```

因此，要安装 `python` 软件包并移除 `nano` 软件包，请使用：

```bash
apt-get install python nano-
```

### 安装、移除和更新程序

相反，要在安装软件包的同时移除一个软件包，需给要安装的软件包加后缀“+”

```bash
apt-get remove oldpackage newpackage+
```

在上述示例中，我们可以使用以下命令移除 `nano` 软件包并安装 `python`：

```bash
apt-get remove nano python+
```

### 升级软件包

在 `APT` 系统中，软件包的升级非常容易完成。当前发行版中的所有软件包都可以通过单条命令进行升级：

```bash
apt-get upgrade
```

要将软件包升级到新的发行版，最好使用以下命令，以确保软件包之间的所有关系都得到更新：

```bash
apt-get dist-upgrade
```
