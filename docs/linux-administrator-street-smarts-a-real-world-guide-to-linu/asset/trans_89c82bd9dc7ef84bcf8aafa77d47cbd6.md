
## 任务范围

本任务涉及使用 `dpkg` 程序执行四种类型的操作：移除包、升级包、安装包以及查询包。第五个子任务，即更新系统，涉及使用 APT。

![](img/f430a19bdf014c43ad7c2d594afd5b21_146_0.png)

> Debian 包系统没有提供与 RPM 系统的 `verify` 操作完全等效的功能。

## 耗时

完成本任务大约需要一个小时。单个包的操作可能需要从几秒到几分钟不等，因此一旦你熟悉了 Debian 包管理，你就可以相当快速地管理包。

## 准备

要严格按照描述的方式完成任务，你必须拥有一个可用的 Debian 系统。如果你使用的是其他基于 Debian 的发行版，你仍然可以完成此任务，但你必须找到其他需要安装、升级和验证的包。这些包可能是此处描述的包的不同版本，或者你可以尝试操作完全不同于此的包。包管理需要超级用户访问权限，因此你应该以普通用户身份登录，然后获取 `root` 权限。

## 注意事项

作为 `root` 用户工作时的常规注意事项适用。此外，包管理存在使系统部分无法运行的风险。特别是，错误地移除你所需的软件是一个明显的风险。如果新软件包含新的 bug 或其操作方式发生了有害的变化，升级软件可能会引发问题。在极少数情况下，包未能正确标记配置文件，因此升级包可能会删除你的配置文件。如果你升级使用配置文件的包，请务必先对其进行备份。这些风险在全系统更新时都会被放大，仅仅因为此类更新可能在单次操作中升级许多不同的包。

## 步骤

本任务涉及演练 `dpkg` 程序的各种功能，最后以启用网络的 APT 结束。`dpkg` 程序接受一个操作（由单个破折号加一个字母代码或双破折号加一个较长的操作名称表示）、任意数量的选项（从零开始，以类似方式指定），以及一个包名、包文件名或磁盘上的文件名。通常，当你操作已安装的包时，你指定一个包名，例如 `zsh`。包文件名是未安装包所存储的文件名。它们可以是任何名称，但惯例上是在包名后跟版本号、架构信息和 `.deb` 文件扩展名，如 `zsh_4.3.2-13_powerpc.deb`。有时你可以使用磁盘上的文件名，通常借助 `--file`（或 `-f`）选项。如果你想查找某个文件属于哪个包，这可能很有用。

### 删除未使用的包

要删除一个包，你可以向 `dpkg` 使用 `--remove`、`--purge`、`-r` 或 `-P` 操作，该操作将包名作为选项接收：

```bash
# dpkg -r vsftpd

(Reading database ... 106705 files and directories currently installed.)

Removing vsftpd ...
Stopping FTP server: vsftpd.
```

如果操作成功完成，你将看到类似此示例中显示的消息。`--remove` 和 `-r` 选项移除整个包*除了*配置文件外，配置文件会保持原样；而 `--purge` 和 `-P` 选项则移除配置文件以及包的其他所有文件。如果你尝试删除一个未安装的包，`dpkg` 会告诉你。同样，如果你尝试删除被其他包依赖的包——例如，尝试删除程序包所依赖的库包——`dpkg` 也会抱怨。如果你看到此类消息，你有三个选择：

- 放弃删除该包的尝试。
- 删除依赖于你试图删除的包的那些包。你可以在命令行中添加它们的名称以同时删除多个包。你需要自己判断此操作是否合理。
- 使用 `--force-depends` 选项告诉 `dpkg` 忽略依赖性问题。由于这可能导致当你尝试使用依赖于你试图移除的包的那些包时发生失败，因此通常不建议使用此选项。

### 升级现有包

要升级一个包，你的硬盘上必须有一个包文件。你可以在各种镜像站点找到 Debian 包，并且 Debian 包数据库位于 [http://www.debian.org/distrib/packages](http://www.debian.org/distrib/packages)，这是一个用于查找包的非常有用的资源。

要升级 `apt` 包，你可以下载最新版本（编写本文时的 `apt_0.6.44.2-powerpc.deb`——注意这是一个 PowerPC 包；请根据你的 CPU 架构做相应修改！），然后直接从你的硬盘安装它：

```bash
# dpkg -i apt_0.6.44.2-powerpc.deb

(Reading database ... 106653 files and directories currently installed.)

Preparing to replace apt 0.5.28.6 (using apt_0.6.44.2-powerpc.deb) ...
Unpacking replacement apt ...
Setting up apt (0.6.44.2) ...
```

`--install` (-i) 操作指定安装新包或升级现有包。程序的输出总结了其操作，如此处所示。如果你愿意，可以在单个命令行上指定多个包文件，`dpkg` 将安装或升级它们全部。

无论你如何升级包，`dpkg` 都会执行依赖性检查。如果升级后的包包含额外的依赖项，或者依赖于比你所安装版本更新的包，`dpkg` 会抱怨并拒绝继续。虽然你可以使用 `--force-depends` 选项来解决这个问题，但这是在自找麻烦。相反，你应该取消升级计划或先升级依赖项。

### 安装新包

使用 `dpkg` 时，包的安装和升级是以完全相同的方式执行的，使用 `--install` (-i) 操作。当你安装一个新包时，输出略有不同：

```bash
# dpkg -i zsh_4.3.2-13_powerpc.deb
Selecting previously deselected package zsh.
(Reading database ... 106653 files and directories currently installed.)
Unpacking zsh (from zsh_4.3.2-13_powerpc.deb) ...
Setting up zsh (4.3.2-13) ...
```

请注意，与升级输出相比，安装输出省略了 `replace` 和 `replacing` 这两个词。除了这个细微的差别外，仅凭 `dpkg` 命令或输出，你很难区分是升级还是全新安装。

### 查询包

如果你不知道某个包的作用，可以使用 `--status` (-s) 操作，该操作将包名作为参数。此操作显示有关该包的一般信息：

```bash
# dpkg -s xpdf-reader
Package: xpdf-reader
Status: install ok installed
Priority: optional
Section: text
Installed-Size: 1792
Maintainer: Hamish Moffatt <hamish@debian.org>
Source: xpdf
Version: 3.00-12
Provides: pdf-viewer, postscript-preview
Depends: lesstif2, libc6 (>= 2.3.2.ds1-4), libfreetype6 (>= 2.1.5-1), libgcc1 (>= 1:3.4.1-3), libc6el | xlibs (>= 4.1.0), libpaper1, libsm6 | xlibs (>= 4.1.0), libstdc++5 (>= 1:3.3.4-1), libti1-5 (>= 5.0.2), libx11-6 | xlibs (>= 4.1.0), libxext6 | x11b6 (>= 4.1.0), libxp6 | xlibs (>= 4.1.0), libxpm4 | xlibs (>= 4.1.0), libxt6 | x11b6 (>= 4.1.0), zlib1g (>= 1:1.2.1), gsfonts (>= 6.0-1), xpdf-common (= 3.00-12)
Suggests: www-browser
Conflicts: xpdf-i (<= 0.90-8), xpdf (<= 0.93-6)
Description: Portable Document Format (PDF) suite -- viewer for X11

xpdf is a suite of tools for Portable Document Format (PDF) files. (These are sometimes called `Acrobat' files after the name of Adobe's PDF software.)

· This package contains xpdf itself, a PDF viewer for X11.

xpdf is designed to be small and efficient. xpdf supports encrypted PDF files. Standard X fonts, TrueType fonts and Type 1 fonts are supported.

· This package also contains pdftoppm, a utility for converting PDF files to PBM, PGM and PPM formats.

· See also the xpdf-utils package for conversion utilities and the other xpdf-* packages for additional language support.
```

此输出表明 xpdf-reader 是一个用于查看 PDF 文件的工具。它还包含有关依赖项、冲突等的信息。如果你想了解有关未安装包文件的类似信息，请使用 `--info` (-i) 选项并将包文件名传入。

另一个 Debian 包信息工具是 `--listfiles` (-L) 选项，它列出包中包含的文件。例如，输入 `dpkg -L xpdf-reader` 将显示从 xpdf-reader 包安装的文件。

如果你想了解拥有某个文件的包名，可以使用 `--search` (-S) 选项，该选项将文件名（或部分文件名）作为选项：

```bash
# dpkg -S /usr/bin/xpdf
xpdf-reader: /usr/bin/xpdf
```

### 执行系统更新

包更新的最终形式是使用 APT 更新系统上安装的每个包。基于 Debian 的系统包含一个文件 `/etc/apt/sources.list`，它指定了可以获取重要包的位置。如果你从 CD-ROM 驱动器安装了操作系统，该文件最初将列出安装 CD-ROM 上可以找到包的目录。顶部附近可能还有几行，用井号 (#) 注释掉，指示你可以从中获取更新包的 FTP 或网站上的目录。（如果你最初执行的是网络安装，这些行可能被取消注释。）

**警告** 除非你确信某个站点值得信赖，否则不要将其添加到 `/etc/apt/sources.list` 中。`apt-get` 实用程序执行自动和半自动升级，因此如果你将网络源添加到 `sources.list` 并且该源包含不可靠的程序或有安全漏洞的程序，你的系统将在通过 `apt-get` 升级后变得易受攻击。

