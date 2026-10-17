
```
aptitude show package_name
```

# 第一部分：Linux 命令行

以下是显示 `mysql-client` 软件包详情示例：

```
$ aptitude show mysql-client
Package: mysql-client
State: not installed
Version: 5.5.38-ubuntu0.14.04.1
Priority: optional
Section: database
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Architecture: all
Uncompressed Size: 129 k
Depends: mysql-client-5.5
Provided: mysql-client-5.5
Description: MySQL database client (metapackaging on the latest version)
这是一个空软件包，依赖于由 MySQL 维护者确定的当前“最佳”版本的 mysql-client（当前为 mysql-client-5.5）。如果你不确定想要哪种版本的 MySQL，请安装此软件包，因为这是维护者认为状态最完备的版本。
Homepage: http://dev.mysql.com/
$
```

> 注意

`aptitude` 命令中的状态标识表示该软件包未安装在系统上。它还显示了来自软件仓库的详细软件包信息。

你无法通过 `aptitude` 获取与特定软件包相关的所有文件列表。要获取此列表，必须使用 `dpkg` 工具本身：

```
$ dpkg -L package_name
```

以下是使用 `dpkg` 列出作为 `vim-common` 软件包一部分安装的所有文件的示例：

```
$
$ dpkg -L vim-common
/
usr
usr/bin
usr/bin/xxxd
usr/bin/helptags
usr/lib
usr/lib/mime
usr/lib/mime/packages
usr/lib/mime/packages/vim-common
usr/share
usr/share/man
usr/share/man/ru
```

```
/usr/share/man/ru/man1/man1.1.gz
/usr/share/man/ru/man1/vimdiff.gz
/usr/share/man/ru/man1/xxd.gz
/usr/share/man/it
/usr/share/man/it/manl
[...]
$
```

```
dpkg --search absolute_file_name
```

注意，此项工作需要使用绝对引用：

```
$ dpkg --search /usr/bin/xxd
vim-common: /usr/bin/xxd
```

输出显示 `/usr/bin/xxd` 是作为 `vim-common` 软件包的一部分安装的。

## 使用 aptitude 安装软件包

现在你已经更了解系统上软件包的列表，本节将介绍如何安装软件包。首先，你需要确定特定的软件包。使用带有 `search` 选项的 `aptitude` 命令：

```
aptitude search package_name
```

`search` 的妙处在于你不需要在 `package_name` 处输入通配符，通配符是隐含的。这是一个使用 `aptitude` 查找 `wine` 软件的示例：

```
$ aptitude search wine
p gnome-wine-icon-theme variation of GNOME
p libwineeffects - library used by effects...
libwineeffects - Qt4 GUI for wine (extra)
p shiki-wine-theme variation of Shiki
p wine - Compatibility ...
p wine-dev - Compatibility ...
p wine-gecko - Compatibility ...
p wine1.0 - Compatibility ...
p wine1.0-dev - Compatibility
+   p wine1.0--- - Compatibility...
- p wine1.2 - Compatibility...
- p wine1.2-dbg - Compatibility...
- p wine1.2-dev - Compatibility...
- p winefish - on Bluefish
```

注意每个软件包名称前面的符号。如果你看到 `i` 或 `u`，则该软件包已安装在你的系统上。如果你看到 `p` 或 `v`，则该软件包可用但尚未安装。但从列表可以看出，系统没有安装 `wine`，但仓库中有该软件包。

使用 `aptitude` 从仓库安装软件包非常简单：

当你从 `search` 选项找到软件包名称后，将其输入带有 `install` 选项的 `aptitude` 命令：

```
sudo aptitude install wine
The following NEW packages will be installed:
cabextract(a)
common(a)
gnome-exe-thumbnail(a)
icoutils(a)
imagemick(a)
libcodec2(a)
libaudiofile(a)
libcodec4(a)
libgraph4(a)
libsvg5(a)
libilmbase(a)
libmagickcore-extralibpng13-0
nett(a)
libopenali(a)
libopenexr(a)
libpathplane(a)
libtiff(a)
netmap(a)
tff-mscore-installer(a)
ttf-font-replacement(a)
wishbind(a)
wine1.2(a)
wine1.2-gecko(a)
0 packages upgraded, 27 installed, 0 to remove and 0 not upgraded.
Need to get 27.6 MB of archives. After installing 121MB will be used.
Do you want to continue? (Y/n) Y
Preconfiguring packages
[...]
All done, no errors.
All fonts downloaded and installed.
Updating fontconfig for /usr/share/fonts/truetype/mstcorefonts
Setting up winbind (2.3.5.4-ubuntu7)
* Starting the Wine daemon winbind
[ OK]
Setting up wine (1.2-ubuntu5)
Setting up gnome-exe-thumbnail (0.6-ubuntu5)
Processing triggers for libc-bin ...
ldconfig deferred now taking place

## 第9章：安装软件

### 注意

在前面的 `aptitude` 命令之前使用了 `sudo` 命令。`sudo` 命令允许你以 root 用户身份运行命令。你可以使用 `sudo` 命令执行管理任务，例如安装软件。

![](img/3d824df0fbf2e68950f7ddee680ca359_252_0.png)

要检查安装是否处理正常，只需再次使用 `search` 选项。这次你应该看到 `wine` 软件包前面有一个 `i`，表示它已安装。

你可能还会注意到额外的软件包前面也有 `i`。这是因为 `aptitude` 自动为我们解决了任何必要的软件包依赖，并安装了所需的额外库和软件包。这是许多软件包系统中包含的一个优秀功能。

## 使用 aptitude 更新软件

虽然 `aptitude` 帮助你避免安装软件时的问题，但协调软件包更新与依赖关系可能会变得复杂。要安全地更新具有许多新版本的系统上的所有软件软件包，请使用 `safe-upgrade` 选项：

```
aptitude safe-upgrade
```

注意，此命令不接受软件包名称作为参数。这是因为 `safe-upgrade` 选项会将所有已安装的软件包升级到仓库中的最新版本，这对于系统的稳定性更安全。

这是运行 `aptitude safe-upgrade` 命令的示例输出：

```
$ sudo aptitude safe-upgrade

The following packages will be upgraded:

evolution-common-evolution-plugins gsfonts libevolution
```
