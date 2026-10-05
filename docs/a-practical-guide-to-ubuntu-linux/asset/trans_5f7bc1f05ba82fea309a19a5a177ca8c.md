
[content]

# APT：保持系统最新更新

以下软件包将被升级：
bash gnome-disk-utility media-player-info xscreensaver-data
4 个软件包已升级，0 个新安装，0 个待删除，0 个未升级。
需要下载 1,266kB 的归包。解压后将使用 28.7kB。
您确定要继续吗？(Y/n)?

...
aptitude 工具会列出它将执行的更改并询问您是否要
继续。输入 y 升级列出的软件包，或输入 n 退出。由于依赖未安装的软件包而未升级的软件包将列为“已保留（kept back）”。

使用 `full-upgrade` 命令可以升级所有软件包，包括依赖于未安装软件包的
full-upgrade 软件包。该命令会根据需要满足依赖关系安装新软件包。

# aptitude search：在仓库中搜索软件包

`search` 命令将命令行上的软件包列表解释为模式列表；其他所有 aptitude 通常将其解释为软件包名列表。该命令搜索 `/etc/apt/sources.list` 中列出的仓库中的所有软件包，包括尚未下载的软件包，并为每个名称匹配 `package-list` 中某个元素的软件包显示一行信息：

+ apt aptitude search vim
p firefox-vimperator - 使其具有 vim 效果的 Firefox 扩展
v gvim
p jvim-canna - 日语 VIM (Canna 版本)
p jvim-doc - jvim 的文档 (日语 VIM)
p vim libtext-vimcolor-perl - 使用 Vim 在 HTML 或 XML 中显示语法颜色文本
p vim - Vi Improved - 增强的 vi 编辑器
p vim-addon-manager - vim 编辑器的插件管理器
p vim-common - Vi Improved - 通用文件

第一列中的字母表示软件包在系统上的状态：i 表示已安装（installed），e 表示已删除（配置文件除外），p 表示已清除（软件包和配置文件均已删除），v 表示虚拟软件包（见第 526 页）。第一列中的字母表示将对软件包执行的存储操作。如果第三个字母为 A，则表示该软件包是自动安装的。

# aptitude show：显示软件包信息

`aptitude show` 命令显示仓库中软件包的信息，包括依赖信息。参见 `apt-cache show` 命令，它显示更多信息（见第 531 页），以及 `dpkg status` 命令（见第 537 页）。下一页是一个示例。

```
$ aptitude nfs-common
Package: nfs-common
State: not installed
Version: 1.1.2.0-ubuntu4
Priority: optional
Section: net
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Size: 602k
Depends: portmap (>= 6.0-10ubuntu1), adduser, ucf, lsb-base (>=
1.3-ubuntu3), netbase (>= 4.24), libproc6 (>= 2.4), libcommer2 (>= 1.01),
libweent-1.4-2 (>= 1.4-13), libgapi-krb5-2 (>=
1.6.dsfg2), libsqsgue1, libscrypt3 (>= 1.6.dsfg2),
libkrb5-3 (>= 1.6.dsfg2), libnfsidmap2, libprpcsecgss3,
libwrap0 (>= 7.6-4), upstart-job
```

Replaces: (mount >= 2.1.3)

Upstream: Sourceforge "nfs", CVS module nfs-utils.
Homepage: http://nfs.sourceforge.net/

# apt-cache：显示软件包信息

`apt-cache` 工具拥有多个命令——某些操作 APT 软件包缓存，另一些则显示缓存中软件包的信息。本节包含一些显示信息的简单命令示例。使用 `apt-file`（见第 521 页）显示系统上未安装的软件包信息。

显示软件包 `apt-cache depends` 命令显示某个软件包所依赖的软件包列表。这些是正向（普通）依赖。使用 `--recurse` 选项显示依赖项所依赖的软件包（依赖的依赖项）。

```
$ apt-cache depends nfs-common
nfs-common
Depends: portmap
Depends: adduser
Depends: ucf
```

```
Conflicts: <nfs-client>
Replaces: mount
Replaces: <nfs-client>
nfs-common
Replaces: nfs-kernel-server
```

`apt-cache rdepends` 命令显示依赖于指定软件包的软件包列表。这些是反向依赖。使用 `--recurse` 选项显示依赖依赖项的软件包。

```
$ apt-cache rdepends nfs-common
nfs-common
Reverse Depends:
rgmanager
nfs-kernel-server
mount
mountautofs5
```

显示软件包 `apt-cache show` 命令显示来自 APT 记录本地软件包索引的软件包记录。参见 `show` 命令，它显示的信息较少（见第 529 页），以及 `dpkg status` 命令（见第 537 页）。以下是一个示例：

```
$ apt-cache show nfs-common
Package: nfs-common
Priority: optional
Section: net
Installed-Size: 588
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Anibal Monsalve Salazar <anibal@debian.org>
Architecture: i386
Source: nfs-utils
Version: 1.2.0-ubuntu2
Replaces: << 2.13-), nfs-client, nfs-kernel-server (>= 1.10.7-5)
Provides: nfs-client
Deps: portmap (>= 6.0-ubuntu1), adduser, ucfd, lsb-base (>= 1.3-9-ubuntu
tu3), netbase (>= 4.24), inscripts (>= 2.86.ds31-3), lib1c6 (>= 2.4)
libcommer2 (>= 1.01), libbevent-4-2 (>= 1.13-stable), libgssapi-krb
5-2 (>= 1.6-dfgs2), libgssuelei, lib5crypto3 (>= 1.6.dfgs2), libkrbs
3-3 (>= 1.6.dfgs2), libnfsidmap2, libprsecss3, libwrap0 (>= 7.6-4)
```

# apt-get source：下载源码

`apt-get source` (dpkg) 命令从 `sources.list`（见第 523 页）中指定的仓库下载并解压源码到工作目录。APT 不像二进制文件那样索引缓存源码。使用 `--download-only` 选项，该命令不解压源码。使用 `--compile` 选项，它会解压并编译源码。不需要 root 权限运行；它只需要工作目录的写入权限。以下是一个示例：

```
$ apt-get source adduser

dpkg-info: extracting adduser-3.112ubuntu
dpkg-info: unpacking adduser_3.112ubuntu.tar.gz
$ ls -ld adduser*
drwxr-xr-- 7 sam 4096 2010-01-27 00:54 adduser_3.112ubuntu
-rw-r-- 1 sam 1141 2010-01-27 03:04 adduser_3.112ubuntu.dsc
-rw-r-- 1 sam 299038 2010-01-27 03:04 adduser_3.112ubuntu.tar.gz
```

# dpkg：DEBIAN软件包管理系统

Debian 软件包 (dpkg) 系统数据库跟踪系统中安装了哪些软件包、它们安装在何处、哪个版本以及软件包依赖关系。dpkg 管理系统包含许多工具。这些工具安装、升级、查询和验证软件包。原始主要的工具是 dpkg。虽然你可以使用 dpkg 管理系统完成大多数任务，但其他工具可以让你的工作更容易。这里描述了一些最常用的工具：

- apt-cache——显示并操作 APT 缓存的信息（见第 530 页）。
- apt-file——与 apt-cache 类似，但除了本地系统已安装的软件包外，它还可以处理未安装的软件包和未下载的软件包（见第 521 页）。
- aptitude——获取软件包并使用 dpkg 安装和删除它们（见第 519 页和 526 页）。
- apt-get——APT 的文本界面；与 aptitude 类似。
- dpkg——主要的 dpkg 管理系统工具（见第 534 页）。
- dselect——dpkg 的伪图形前端。
- Synaptic——APT 的图形界面（见第 133 页）。

[/content]
