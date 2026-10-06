

相关的标记 `-F` 允许你仅在包存在时对其进行更新。例如，命令

```
rpm -Fvh gnorpm-0.9-10.i386.rpm
```

只有在该包已安装时，该命令才会更新 `gnorpm` 包。`-F` 标记可以帮助保持系统处于最新状态。Red Hat 在 www.redhat.com/support/errata 维护了一份更新包列表。你应该监控该列表，并使用 `-F` 标记应用任何你认为对系统运行至重要的修复程序。现在，完成练习 12.3，该练习要求你更新一个 RPM 包。

## 练习 12.3

更新包
如所述，一个勤奋的系统管理员会监控 Red Hat Errata（错误列表）页面并及时应用用的修复。为了检查你执行此操作的能力，请使用 `rpm` 命令使用从 Red Hat Errata 页面下载的修复程序更新包。在练习过程中，你可以查阅本章寻求帮助，但请记住，在 RHCE 考试中你没有这个机会。

## 识别已安装的包

你可以使用 RPM 来查询已安装包的版本号和构建号。要为此，请执行格式如下的命令

```
rpm -q package_name
```

其中 `package_name` 是已安装包的名称。输出由单行组成，提供包名、版本号和构建号——示例：
gnorpm-0.9-10

要学习每个已安装包的版本和构建号，请执行命令

```
rpm -qa
```

为了验证你对 `rpm` 命令的 `-q` 和 `-qa` 标记的理解，请完成练习 12.4。

## 练习 12.4

## 识别包

通常情况下，能够确定系统上安装了哪些包是非常方便的。为了检查你执行此操作的能力，请使用 `rpm` 命令列出你系统中安装的包的版本号和构建号。如果必要，请回看本章，但请准备好在参加 RHCE 考试时在没有帮助的情况下执行此操作。

## 确定文件所有者

你可以使用 RPM 来了解哪个包（如果有的话）拥有特定文件。要为此，请执行格式如下的命令

```
rpm -qf filename
```

其中 `filename` 是文件名，必须包含完整路径。例如，要求 RPM 报告文件 `/etc/inittab` 的所有权将产生如下输出：

```
# rpm -qf /etc/inittab
inscripts-4.16-1
```

现在，完成练习 12.5，该练习要求你使用 `rpm` 命令的 `-qf` 标记。

## 练习 12.5

## 确定文件所有者

为了检查你对 `rpm` 命令的 `-qf` 标记的理解，请使用 `rpm` 命令确定哪个包拥有 `/etc/inetd.conf` 文件。执行此练习时你可以参考本章，但请准备好在 RHCE 考试期间没有书籍或笔记的情况下使用 `-qf` 标记。

## 查询和验证包内容

`rpm` 命令允许你查询和验证包内容。例如，你可以执行以下操作：

- 打印包的描述
- 列出包包含的文件
- 打印安装或卸载包时执行的脚本
- 验证包内容的完整性和真实性

接下来的小节将解释这些操作。

## 打印包的描述

要打印已安装包的描述，请执行格式如下的命令

```
rpm -qi package_name
```

其中 `package_name` 是已安装包的名称。例如，打印已安装包 `gnorpm` 的描述将产生类似于下面的输出：

```
# rpm -qip gnorpm-0.9-10.i386.rpm
Name : gnorpm Relocations: (not
-relocatable)
Version : 0.9 Vendor: Red Hat Software
Release : 10 Build Date: Sep 25
-13:51:53 1999
Install date: (not installed) Build Host:
-porky.devel.redhat.com
Group : Applications/System Source RPM:
-gnorpm-0.9-10.src.rpm
Size : 434375 License: GPL
Packager : Red Hat Software
<http://developer.redhat.com/bugzilla/
Summary : A graphical front-end to the RPM for GNOME.
Description :
GnorPM 是 Red Hat Package Manager (RPM) 的图形界面。GnorPM 类似于 Glint，但是使用 GTK 控件和 GNOME 库编写的。GnorPM 目前正在开发中，因此缺少某些功能，
```

但你目前可以使用 GUI 界面查询、安装、升级、卸载和验证包。

要为包文件打印此信息，请执行格式如下的命令

```
rpm -qip package_file_name
```

其中 `package_file_name` 是包文件的名称。

## 列出包含的文件

要列出已安装包包含的文件，请执行格式如下的命令

```
rpm -ql package_name
```

其中 `package_name` 是已安装包的名称。例如，列出 `gnorpm` 包的文件会产生这样的输出：

```
# rpm -ql gnorpm-auth
/etc/pam.d/gnorpm-auth
/etc/security/console.apps/gnorpm-auth
/usr/bin/gnorpm-auth
/usr/bin/gnorpm
/usr/share/gnorpm
/usr/share/gnorpm/README
/usr/share/gnorpm/NEWS
/usr/share/gnorpm/LICENSE
/usr/share/gnorpm/CHANGELOG
/usr/share/gnorpm/AUTHORS
/usr/share/gnorpm/COPYRIGHT
/usr/share/gnorpm/SUPPORT
/usr/share/gnorpm/HITS
/usr/share/gnorpm/CONTRIBUTING
/usr/share/gnorpm/bugreports
/usr/share/gnorpm/devel
/usr/share/gnorpm/perl
/usr/share/gnorpm/python
/usr/share/gnorpm/gnome-icons/
/usr/share/gnorpm/gnome-themes/
/usr/share/gnorpm/gnome-settings/
/usr/share/gnorpm/gnome-extensions/
/usr/share/gnorpm/gnome-shell/
/usr/share/gnorpm/gnome-session/
/usr/share/gnorpm/gnome-share/
/usr/share/gnorpm/gnome-plugins-common/
/usr/share/gnorpm/gnome-shell-extensions/
/usr/share/gnorpm/gnome-session-data/
/usr/share/gnorpm/gnome-share-data/
/usr/share/gnorpm/gnome-extensions-data/
/usr/share/gnorpm/gnome-settings-data/
/usr/share/gnorpm/gnome-themes-data/
/usr/share/gnorpm/gnome-icons-data/
```

## 打印脚本

要打印与包文件相关的安装前安装后脚本，请执行格式如下的命令

```
rpm -qp package_file_name
```

其中 `package_file_name` 是 `gnorpm-0.9-10.i386.rpm`

## 验证包内容

RPM 对已安装包中的每个文件都有记录。记录包含每个文件的大小、所有者、权限和 MD5 校验和。如果文件是符号链接，记录将附加链接的路径；如果文件是设备文件，记录将包含主从设备号。

通过这些记录，你可以通过格式如下的命令来确定自包安装以来哪些文件被修改过：

```
rpm -V package_name
```

其中 `package_name` 是已安装包的名称。输出每个每个文件一行。每行有三个字段：

- `*` 表示文件的状态。
- 配置，如果文件是配置文件，则包含 `c`，否则包含空格。
- 文件名，给出文件的路径和名称。

### 表 12.1 包验证标记

| 代码 | 含义 |
|---|---|
| | 无更改。 |
| S | MD5 校验和已更改。 |
| D | 设备主或从号已更改。 |
| G | 组已更改。 |
| L | 链接路径已更改。 |
| M | 文件模式已更改。 |
| S | 文件大小已更改。 |
| T | 修改时间已更改。 |
| U | 所有用户已更改。 |

这是一个显示 setup 包内容状态的示例：

```
# rpm -V setup
S.5....T c /etc/exports
S.5....T c /etc/hosts.allow
S.5....T c /etc/hosts.deny
S.5....T c /etc/printcap
S.5....T c /etc/profile
S.5....T c /etc/services
```

如果你愿意，也可以与包文件而不是数据库进行比较。这种选项在你怀疑数据库可能损坏时非常有用。如果是这样，执行格式如下的命令

```
rpm -Vp package_file_name
```

其中 `package_file_name` 是包文件的名称。

