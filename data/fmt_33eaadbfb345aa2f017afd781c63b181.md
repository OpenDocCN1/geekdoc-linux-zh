
```
Source: offsec-defaults
Section: misc
Priority: optional
Maintainer: Raphaël Hertzog <bxy@kali.org>
Build-Depends: debhelper(>= 9)
Standards-Version: 3.9.8

Package: offsec-defaults
Architecture: all
Depends: $(misc:Depends)
Description: Default settings for Offensive Security
This package contains multiple files to configure
owned by Offensive Security.
```

它显著地修改了：

* APT 配置
* salt-minion 配置
* 默认桌面设置

`rules` 文件通常包含一组规则，用于在指定的子目录（以二进制包命名）中配置、构建和安装软件。如果该子目录是文件系统的根目录，则其内容将被归档 Debian 软件包中。在这种情况下，文件将安装在 `debian/offsec-defaults/` 子目录下。例如，为了生成一个安装了 `/etc/apt/sources.list.d/offsec.list` 的包，请将文件安装在 `debian/offsec-defaults/etc/apt/sources.list.d/offsec.list`。`rules` 文件作为 Makefile 使用，包含几个标准目标（包括 `clean` 和 `binary`，分别用于清理源码目录和生成二进制包）。

# 什么是 Makefile 文件？

你可能已经注意到 `dh_make` 输出最后关于缺少 Makefile 的信息，以及提到它与 `rules` 文件的相似之处。Makefile 是程序使用的脚本文件；它描述了如何在一个依赖树中从一组文件构建出其他文件的规则。例如，一个程序可以从一组源文件构建。Makefile 文件以以下格式描述这些规则：

```
target: source source2 ...-n  command1
  command2
```

此类规则的解释如下：如果其中一个源文件比目标文件新，则需要使用 `command1` 和 `command2` 生成目标文件。

请注意，命令行必须以制表符（tab）字符开头；同时请注意，当命令行以破折号（-`）开头时，命令的执行失败不会中断整个过程。

尽管该文件是过程的核心，但它只包含了运行 `debhelper` 工具提供的标准命令集所需的极少内容。`dh_make` 生成的文件就是如此。为了安装你所有的文件，我们建议通过创建以下 `debian/offsec-defaults.install` 文件来配置 `dh_install` 命令的行为：

```
apt/offsec.list etc/apt/sources.list.d/
apt/offsec.gpg etc/apt/trusted.gpg.d/
salt/offsec.conf salt/minion.d/
images/background.png usr/share/images/offsec/
```

你也可以用此来获取 getsettings 覆盖文件，`debhelper` 为此提供了专用工具（`dh_installsettings`），因此你可以依赖它。首先，将你的设置放在 `debian/offsec-defaults.settings-override` 中：

```
[org.gnome.desktop.background]
picture-options='zoom'
picture-uri='file:///usr/share/images/offsec/background.png'
```

接下来，在 `debian/rules` 中覆盖 `dh_installsettings`，以将优先级提高到组织覆盖预期的水平（根据手册页，该级别为 90）：

```bash
#!/usr/bin/make -f
```

```
%:
override_dh_installsettings:
  dh_installsettings --priority=90
```

此时，源包已准备就绪。剩下的工作是使用与之前重新构建包的相同方法生成二进制包：从 `offsec-defaults-1.0` 目录中运行 `dpkg-buildpackage -us -uc` 命令：

```
$ dpkg-buildpackage -us -uc
depkg-buildpackage: info: source package offsec-defaults
depkg-buildpackage: info: source version 1.0
depkg-buildpackage: info: source distribution unstable
depkg-buildpackage: info: source changed by Raphael Hertog <buxy@kali.org>
depkg-buildpackage: info: host architecture amd64
depkg-source --before-build offsec-defaults-1.0
fakeroot debian/rules clean
dh clean
dh_testdir
dh_auto_clean
dh clean
depkg-source -b offsec-defaults-1.0: info: using source format '3.0 (native)'
depkg-source: info: building offsec-defaults in offsec-defaults_1.0.tar.xz
depkg-source: info: building offsec-defaults in offsec-defaults_1.0.dsc
debian/rules build
dh build
dh_testdir
dh_auto_config
dh_auto configure
dh_auto build
dh_auto_test
fakeroot debian/rules binary
dh binary
dh_testroot
dh prep
dh_auto_install
dh_install
debian/rules override dh_installsettings
make[1]: Entering directory '/home/rhertzog/kali-book/samples/offsec-defaults-1.0'
dh_installsettings --priority=90
make[1]: Leaving directory '/home/rhertzog/kali-book/samples/offsec-defaults-1.0'
dh_perl
dh_link
dh_strip
dh_fixperms
dh_genchanges
dh_mdsums
dhbuild
dpkg-deb: building package 'offsec-defaults' in '../offsec-defaults_1.0_all.deb'.
dpkg-deb-genchanges >../offsec-defaults_1.0.amd64.changes
dpkg-deb-genchanges: info: including source code
depkg-source --after-build offsec-defaults-1.0
depkg-buildpackage: info: native package (full source included)
```

# 创建包仓库

现在你有了一个自定义包，就可以分发它了。你可以通过 APT 仓库分发它。首先，我们需要创建一个本地目录来存放二进制包：

```bash
mkdir -p ~/deb-repo
cp ../offsec-defaults_1.0_all.deb ~/deb-repo/
```

然后，进入该目录并生成索引：

```bash
cd ~/deb-repo
dpkg-scanpackages . .
```

将该仓库添加到系统的 `/etc/apt/sources.list.d/offsec.list` 中：

```bash
echo "deb [trusted=yes] file:/home/$USER/deb-repo/" | sudo tee /etc/apt/sources.list.d/offsec.list
```

最后，更新软件包列表：

```bash
sudo apt update
```

现在你就可以安装你的自定义包了：

```bash
sudo apt install offsec-defaults
```
