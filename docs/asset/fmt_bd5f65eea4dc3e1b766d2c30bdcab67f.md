
```bash
$ dpkg -p samba
Package: samba
Priority: optional
Section: net
Installed-Size: 11157
Architecture: amd64
Version: 2.4.1+dfsg-1ubuntu2.14
Maintainer: Ubuntu Developers <ubuntu-developers@lists.com>
Depends: adduser, heindal-hdb-api, libpam-modules, libpam-runtime (>= 1.01), lsb-base (>= 4.1), procps, python (>= 2.7), python-dyninfo, python-nttdb, python-samba, samba-common (>= 2.1.6+dfsg-ubuntu2.14), samba-common-bin (>= 2.1.6+dfsg-ubuntu2.14), samba-dsdb-modules, tdb-tools, update-inetd, sysv-rc (>= 2.08dsf-24) | 
file-rc (>= 0.86), python (<< 2.8), python2.7:any, libas1n-8-heimdal (>= 1.4+git201102), libc6 (>= 2.14), libcommerr (>= 1.01), libhdb9-heimdal (>= 1.4+git201102), libkdc2-heimdal (>= 1.4+git201102), libkrb56-heimdal (>= 1.4+git201102), libldbi (>= 0.9.21), libpopt0 (>= 1.14), python2.7 (>= 2.7), libreken18-heimdal (>=)
1.4.0+git20101226), libtalloc2 (>= 2.0.4-git20101213), libdbti1 (>=)
1.2.7+git20101214, libtevent0 (>= 0.9.14), samba-libs (= 2:4.1+dfsg-ubuntu2.14.04.3)

Pre-Depends: dpkg (>= 1.15~), multiarch-support

Recommended: atrr, logrotrate, samba-vfs-modules

Suggestions: bind9 (>= 1:9.5.1), bind9utils, ldb-tools, ntp, smbldap-tools, winbind, ufw

Conflicts: libdb1 (<< 1:1.15), samba (<< 2:3.3.0-rc2-5), samba-ad-dc, samba-doc (<< 2:4.0.5-), samba4 (<< 4.0.0-alpha6-2)

Enhances: dpkg, ntp

Size: 838626
```

基于 Debian 的系统通常使用某种高级别的工具 `apt` 和 `dselect` 来处理软件包的安装和卸载。这些工具将在后文“使用 `apt-get`”以及“使用 `dselect`, `aptitude` 和 `Synaptic`”中进行描述。当你想要安装多个软件包时，这些工具的界面非常有用；但当你只操作一个或两个软件包时，`dpkg` 更好。由于 `dpkg` 可以接受文件名作为输入，因此它也是从非标准来源下载或自行创建的软件包的首选方法。

## 使用 `apt-cache`

APT 工具套包含一个名为 `apt-cache` 的程序，它专门用于提供有关 Debian 软件包数据库（在 Debian 术中称为软件包缓存）的信息。你可能对该工具的几个功能感兴趣：

### 显示软件包信息

使用 `showpkg` 子命令，例如 `apt-cache showpkg samba`，可以显示软件包的信息。显示的信息与 `dpkg` 的信息查询返回的内容不同。

### 显示软件包统计数据

通过在 `apt-cache stats` 中传递 `stats` 子命令，你可以了解你安装了多少软件包、记录了多少依赖项以及关于软件包数据库的各种其他统计数据。

### 查找未满足的依赖

如果某个程序报告缺少库或文件，输入 `apt-cache unmet` 可能会有所帮助；`apt-cache` 的此功能会返回有关未满足依赖的信息，这可能帮助你追踪缺失文件问题的来源。

## 显示依赖关系

使用 `depends` 子命令，例如 `apt-cache depends samba`，可以显示软件包的所有依赖项。这些信息对于追踪与依赖的问题非常有帮助。`rdepends` 用于查找反依赖——即依赖于你指定的软件包的包。

## 定位所有软件包

`pkgnames` 子命令显示系统上安装的所有软件包的名称。如果你包含第二个参数，例如 `apt-cache pkgnames sa`，程序将只返回以指定字符串开头的软件包。

虽然存在许多子命令和选项，但这些是你最可能使用的。几个 `apt-cache` 子命令是为软件包维护者调试严重的软件包数据库问题设计的，而不是用于日常系统管理。请参阅 `apt-cache` 的 man 页以获取更多信息。

## 使用 `apt-get`

APT 及其 `apt-get` 工具是 Debian 对应的某些基于 RPM 的发行版中的 `Yum`。这个元软件包工具允许你轻松地对软件包进行升级，特别是当你有快速互联网连接时。基于 Debian 的系统包含一个文件 `/etc/apt/sources.list`，该文件指定了可以获取重要软件包的位置。如果你是从 CD-ROM 驱动器安装的操作系统，该文件最初将列出安装 CD-ROM 上可以找到软件包的目录。顶部附近可能还有几行用井号（#）注释掉的行，表示从 FTP 站点或网站可以获取更新后的软件包的目录。（如果你最初是进行网络安装的，这些行可能已经被取消注释。）

![](img/f74c2c51e1985d4d3a6804ba2887d2f4_174_0.png)

除非你确定它是受信任的，否则不要向 `/etc/apt/sources.list` 添加新站点。`apt-get` 工具执行自动和半自动升级，因此如果你向 `/etc/apt/sources.list` 添加了网络源，而该源包含不可靠的程序或带有安全漏洞的程序，那么你的系统在通过 `apt-get` 升级后将变得脆弱。

尽管 APT 与 Debian 系统关联最紧密，但也提供了基于 RPM 系统的移植版本。访问 [http://apt4rpm.sourceforge.net](http://apt4rpm.sourceforge.net) 获取有关该移植的信息。

`apt-get` 工具的工作原理是从 `/etc/apt/sources.list` 中列出的源获取可用软件包的信息，并使用这些信息升级或安装软件包。其语法与 `dpkg` 类似：

```bash
apt-get [options] [command] [package-names]
```

表 2.6 列出了 `apt-get` 命令，表 2.7 列出了最常用的选项。在大多数情况下，你不会对 `apt-get` 使用任何选项——只需一个命令以及可能的一个或多个软件包名称。该工具的一个特别常见的用途是让你的系统通过任何新软件包保持更新。如果 `/etc/apt/sources.list` 包含了指向最新文件存档点的指针，以下两个命令将实现这一目标：

```bash
apt-get update
apt-get dist-upgrade
```

如果某个程序报告缺少库或文件，输入 `apt-cache unmet` 可能会有所帮助；`apt-cache` 的此功能会返回有关未满足依赖的信息，这可能帮助你追踪缺失文件问题的来源。

### 表 2.6 `apt-get` 命令

| 选项 | 配合命令 | 描述 |
|---|---|---|
| `-b`, `--compile`, or `--build` | `source` | 获取源包后对其编译。 |
| `--no-upgrade` | `install` | 如果已安装了旧版本，则导致 `apt-get` 不升级软件包。 |
| `update` | | 从 `/etc/apt/sources.list` 中列出的安装源获取有关可用软件包的更新信息。 |
| `upgrade` | | 根据本地存储的可用软件包信息，将所有已安装软件包升级到最新的可用版本。 |
| `dselect-upgrade` | | 在运行 `dselect` 后对软件包状态（安装、删除等）执行任何更改。 |
| `dist-upgrade` | | 与 `upgrade` 类似，但通过避免在破坏依赖关系的情况下执行“智能”冲突解决。 |
| `install` | | 通过名称（而非文件名）安装软件包，从包含最新版本的源获取软件包。 |
| `remove` | | 通过包名称删除指定的软件包。 |
| `source` | | 使用 `/etc/apt/sources.list` 中列出的可用软件包和安装存档，通过文件名检索最新的可用源包文件。 |
| `check` | | 软件包数据库的一致性和损坏的安装。 |
