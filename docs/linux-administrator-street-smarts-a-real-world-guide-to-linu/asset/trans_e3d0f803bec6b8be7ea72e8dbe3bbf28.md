

## 140

处理完全不同于的包。包管理需要超级用户权限，因此您应该以普通用户身份登录并获取 root 权限。

### 注意事项

关于以 root 身份操作的那些通常注意事项在此同样适用。此外，包管理还存在使系统部分组件无法运行的风险。特别是，错误地删除了您需要的软件是一个明显的风险。如果新软件包含新 bug，或者其运行方式发生了不利的变化，升级软件可能会引发问题。在极少数情况下，包未能正确标记配置文件，因此升级包可能会清除您的配置文件。如果您升级使用配置文件的包，请务必先对其进行备份。在进行整个系统更新时，这些风险会被放大，因为这通常涉及在单次操作中升级许多不同的包。

### 操作步骤

此任务涉及练习 rpm 程序的各种功能，最后介绍支持网络的 RPM 封装工具 Yum。rpm 程序接受一个操作（由一个短横线和单字母代码，或两个短横线和更长的操作名称表示），任意数量的选项（从零开始，以类似方式指定），以及一个包名、包文件名或磁盘上的文件名。通常来说，当您处理已安装的包时，您需要指定包名，例如 zsh。包文件名是存储未安装包的文件的名称。它们可以是任何内容，但惯例上是包名后跟版本号、架构信息以及 .rpm 文件扩展名，例如 zsh-4.2.5-1.2.2.i386.rpm。有时您可以使用磁盘上的文件名，通常需要借助 `-ffile`（或 `-f`）选项。如果您想查找拥有特定文件的包，这可能会非常方便。

#### 删除未使用的包

要删除一个包，您对 rpm 使用 `--erase`（或 `-e`）选项，该选项接受包名作为参数：

```
# rpm -e vsftpd
```

如果操作成功完成，您将不会看到其他消息。如果您尝试删除未安装的包，rpm 会告知您这一点。同样，如果您尝试删除被其他包依赖的包，rpm 也会报错——例如，如果您尝试删除程序包所依赖的库包。如果您看到此类消息，您有三种选择：

- 放弃删除该包的尝试。
- 删除依赖于您试图删除的那个包的包。您可以将它们的名称添加到命令行中以同时删除多个包。您需要自行判断此操作是否合理。
- 使用 `--nodeps` 选项告诉 rpm 忽略依赖性问题。通常不建议使用此选项，因为它可能导致在您尝试使用依赖于您试图删除的包的软件时发生失败。

### 升级现有包

要升级一个包，您必须在硬盘上拥有该包的文件，或者拥有服务器上该包文件的完整 URL。您可以在各种镜像站点上找到 Fedora Core 5 的 RPM；详情请查阅 http://fedora.redhat.com/Download/mirrors.html。x86 的基础操作系统 RPM 位于镜像页面上列出的目录下的 `5/i386/os/Fedora/RPMS` 目录中，而更新包则位于 `updates/i386/` 目录中。（如果您没有使用 x86 发行版，请将 i386 替换为您的平台 CPU 代码。）

要升级 yum 包，您可以下载最新版本（在撰写本文时是 yum-2.6.1-0.fc5.noarch.rpm）并从您的硬盘安装它：

```
# rpm -Uvh yum-2.6.1-0.fc5.noarch.rpm
```

`--upgrade`（`-U`）选项指定升级现有包，而 `-vh`（`--verbose --hash`）选项告诉 rpm 以一系列井号（#）的形式显示进度条。您可以不下载包，而是通过在 RPM 文件名前加上完整 URL 来告诉 rpm 直接从网络仓库安装，包括针对 Web 站点或 FTP 站点的 `http://` 或 `ftp://` 说明。这个选项可以是一个便捷的快捷方式，但额外的打字可能会很繁琐。

无论您如何升级包，rpm 都会执行依赖项检查。如果升级后的包包含额外的依赖项，或者依赖于比您已安装版本更新的其他包版本，rpm 会抱怨并拒绝继续。虽然您可以使用 `--nodeps` 选项来克服这个问题，但这其实是自找麻烦。相反，您应该取消升级计划或先升级依赖项。

与删除包一样，您可以在单个命令行中列出多个包以进行升级。这在升级一个包及其依赖项时特别方便；只需按任意顺序列出它们，rpm 将升级它们所有。

### 安装新包

您可以像升级现有包一样安装新包，但使用 `--install`（`-i`）操作而不是 `--upgrade`（`-U`）：

```
# rpm -ivh zsh-4.2.5-1.2.2.i386.rpm
```

与升级一样，您可以通过在 RPM 文件名前传递完整 URL 直接从 FTP 或 Web 站点安装。

许多管理员更喜欢使用 `--upgrade`（`-U`）操作来安装软件；如果该操作接收了一个尚未安装的包的包文件名，rpm 会将其安装，除了常规的依赖项检查外，不会有任何其他说明。这可能很方便，因为您不需要知道包是否已经安装，并且可以在单个命令行中混合升级和新安装。

### 查询包

如果您不知道某个包的作用，您可以使用 `--query`（`-q`）操作，该操作接受包名作为参数。为了使该操作有用，您可能会指定 `--info`（`-i`）或 `--list`（`-l`）选项，它们分别显示关于包的总体信息以及它包含的文件列表。要了解 xpdf 的作用，您将使用 `-i`：

```
# rpm -qi xpdf
Name : xpdf Relocations: (not relocatable)
Version : 3.01 Vendor: Red Hat, Inc.
Release : 12.1 Build Date: Sun 12 Feb 2006 13:32:24 PM EST
Install Date: Tue 27 Jun 2006 06:57:45 PM EDT Build Host:
bcl-13.build.redhat.com
Group : Applications/Publishing Source RPM: xpdf-3.01-12.1.src.rpm
Size : 7758073 License: GPL
Signature : DSA/SHA1, Mon 06 Mar 2006 04:21:30 PM EST, Key ID
4269d04f2a6fd2
Packager : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
URL : http://www.foolabs.com/xpdf/
Summary : A PDF file viewer for the X Window System.
Description :
Xpdf is an X Window System based viewer for Portable Document Format (PDF) files. Xpdf is a small and efficient program which uses standard X fonts.
```

此输出表明 xpdf 是一个用于查看 PDF 文件的工具。它还包含关于包安装时间、构建地点等信息。如果您传递了 `-l` 代替或除了 `-i` 之外，您将获得包中包含的文件列表。

除了传递包名，您还可以使用 `--package`（`-p`）选项传递包文件名，例如 `rpm -qpi xpdf-3.01-12.1-i386.rpm`，或者通过传递 `--file`（`-f`）选项来查询拥有计算机上特定文件的包，例如 `rpm -qfi /usr/bin/xpdf`。您还可以使用 `--all`（`-a`）选项查询系统中安装的所有包。在没有 `-i` 或 `-l` 选项的情况下执行此操作最有用，以便获取已安装包的简单列表。如果您将输出重定向到文件或通过 `less` 管道处理，然后就可以对您不熟悉的包执行进一步的查询，以跟踪那些可能导致系统臃肿的包。

### 验证包

RPM 维护了一个数据库，其中包含它从每个已安装包安装的所有文件，以及这些包的校验和 information。您可以使用 `--verify`（`-V`）操作来使用这些信息验证包的完整性：

```
# rpm -V samba
...T /usr/bin/smbcontrol
SMS...T /usr/bin/smbstatus
missing d /usr/share/doc/samba-3.0.22/html/docs/using_samba/figs/sam2_0811.gif
```

