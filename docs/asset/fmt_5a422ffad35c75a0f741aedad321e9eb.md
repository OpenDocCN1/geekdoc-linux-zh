
```
$
$ sudo apt upgrade
正在读取软件包列表... 完成
正在构建依赖树
正在读取软件包状态信息... 完成
正在计算升级... 完成
将要安装以下新软件包：
binutils binutils-common binutils-x86-64-linux-gnu build-
essential dpkg-dev
fakeroot g++ g++-9 gcc gcc-9 libalgorithm-diff-perl
libalgorithm-diff-xs-perl libalgorithm-merge-perl libasan5
libatomic1
libbinutils libc-dev-bin libc6-dev libcrypt-dev libcif-
nobfd0 libctf0
libfakeroot libgcc-9-dev libitm1 liblsan0 libquadmath0
libstdc++-9-dev
libtsan0 libubsan1 linux-libc-dev make manpages-dev
将升级以下软件包：
chromium-codecs-ffmpeg-extra eog file-roller fonts-
opensymbol gedit
gedit-common gir1.2-gnomedesktop-3.0 glib-networking glib-
networking-common
glib-networking-services gnome-control-center gnome-
control-center-data
gnome-control-center-faces gnome-desktop3-data gnome-
initial-setup
libgnome-desktop-3-19 libjuh-java libjurt-java libnautilus-
extension1a
libnetplan0 libreoffice-base-core libreoffice-calc
libreoffice-common
libreoffice-core libreoffice-draw libreoffice-gnome
libreoffice-gtk3
libreoffice-help-common libreoffice-help-en-us libreoffice-
impress
libreoffice-math libreoffice-ogltrans libreoffice-pdfimport
libreoffice-style-breeze libreoffice-style-colibre
libreoffice-style-elementary libreoffice-style-tango
libreoffice-writer
libridl-java libuno-cppu3 libuno-cppuhelpergcc3-3 libuno-
purpenvhelpergcc3-3
libuno-sal3 libuno-salhelpergcc3-3 libunoloader-java
nautilus nautilus-data
netplan.io python3-distupgrade python3-uno thermald ubuntu-
drivers-common
ubuntu-release-upgrader-core ubuntu-release-upgrader-gtk
ure
升级 56 个，新安装 32 个，移除 0 个，有 0 个未升级。
需要下载 133 MB 的归档文件。
此操作完成后，将额外使用 143 MB 磁盘空间。
你想要继续吗？ [Y/n]
```

在输出中，请注意 `apt` 列出了将要升级的软件包，但也列出了因升级而需要安装的新软件包。

`upgrade` 命令不会在升级过程中移除任何软件包。如果升级过程中需要移除某个软件包，请使用命令

```
apt full-upgrade
```

虽然这看起来可能有些奇怪，但有时为了在发行版升级之间保持同步，确实需要移除软件包。

> 注意
>
> 显然，运行 `apt` 的 `upgrade` 选项是定期更新系统以保持其最新状态时应执行的操作。然而，在新安装发行版之后运行该命令尤为重要。通常，自发行版最后一次完整发布以来，已经发布了大量的安全补丁和更新。

### 使用 apt 卸载软件

使用 `apt` 删除软件包与安装和升级软件包一样简单。你唯一真正需要做出的选择是之后是否保留该软件的数据和配置文件。

若要删除软件包但保留其数据和配置文件，请使用 `apt` 的 `remove` 命令。若要删除软件包及其相关的数据和配置文件，请使用 `purge` 选项：

```
$ sudo apt purge zsh
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following package was automatically installed and is no
longer required:
  zsh-common
Use 'sudo apt autoremove' to remove it.
The following packages will be REMOVED:
  zsh*
0 upgraded, 0 newly installed, 1 to remove and 56 not
upgraded.
After this operation, 2,390 kB disk space will be freed.
Do you want to continue? [Y/n] y
(Reading database ... 180985 files and directories currently
installed.)
Removing zsh (5.8-3ubuntu1) ...
Processing triggers for man-db (2.9.1-1) ...
(Reading database ... 180928 files and directories currently
installed.)
Purging configuration files for zsh (5.8-3ubuntu1) ...
```

不过请注意，作为 `purge` 输出的一部分，`apt` 警告我们，作为依赖项安装的 `zsh-common` 包并未被自动删除，以防它可能其他软件包所需要。如果你确定该依赖包不被其他任何包所需，你可以使用 `autoremove` 命令将其删除：

```
$ sudo apt autoremove
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following packages will be REMOVED:
 zsh-common
0 upgraded, 0 newly installed, 1 to remove and 56 not
upgraded.
After this operation, 15.6 MB of disk space will be freed.
Do you want to continue? [Y/n] y
(Reading database ... 180928 files and directories currently
installed.)
Removing zsh-common (5.8-3ubuntu1) ...
Processing triggers for man-db (2.9.1-1) ...
```

`autoremove` 命令将检查所有标记为依赖项且不再需要的软件包。

### apt 软件库

`apt` 的默认软件库位置是在你安装 Linux 发行版时为你配置好的。库的位置存储在 `/etc/apt/sources.list` 文件中。

在许多情况下，你永远不会需要添加/删除软件库，因此无需触碰此文件。然而，`apt` 只会从这些库中获取软件。此外，在搜索要安装或更新的软件时，`apt` 仅会检查这些库。如果你需要为包管理系统添加一些额外的软件库，这就是该进行配置的地方。

> 提示
>
> Linux 发行版开发者努力确保添加到库中的软件包版本互不冲突。通常，从库中升级或安装软件包是最安全的。即使其他地方有更新版本，你可能也要等到该版本在你的 Linux 发行版库中可用后再安装它。

以下是 Ubuntu 系统中 `sources.list` 文件的一个示例：
