
`dh_make` 命令创建了一个包含许多文件的 `debian` 子目录。其中某些文件是必须的，特别是 `rules`、`control`、`changelog` 和 `copyright`。以 `.ext` 结尾的文件是示例文件，可以通过修改它们并删除扩展名来使用。当不需要这些文件时，我们建议将它们删除。`compat` 文件应该保留，因为它是软件包构建过程中各个阶段所使用的 `debhelper` 程序套件（所有以 `dh_` 开头的程序）正常运行所需的。

`copyright` 文件必须包含包内包含文档的作者信息以及许可协议。如果 `dh` 选择的默认许可不符合你的需求，你必须编辑此文件。以下是修改后的 `copyright` 文件：

```
Format: https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/
Upstream-Name: offsec-defs

Files: *

Copyright: 2016 Offensive Security
License: GPL-3.0+

License: GPL-3.0+
本程序是自由软件：你可以根据自由软件基金发布的《GNU 通用许可协议》条款对其进行分发和/或修改，该协议可以是协议的第 3 版本，或（根据你的选择）任何后继版本。

本包的发行是希望它有用处，但`不提供任何保证`：即使没有对商品性或特定用途适用性的隐性保证。更多信息请参阅《GNU 通用许可协议》。

你应该在收到此程序的同时收到一份《GNU 通用许可协议》的副本。如果没有，请参阅 <https://www.gnu.org/licenses/>。

在 Debian 系统上，可以在 "/usr/share/common-licenses/GPL-3" 找到第 3 版《GNU 通用许可协议》的全文。
```

默认的 `changelog` 文件通常是合适的，将 "Initial release" 替换为更详细的解释应该足够：

```
offsec-defaults (1.0) unstable; urgency=medium

+   * 添加 salt minion 的配置文件。
* 添加 APT 的 sources.list 条目和 APT 的信任 GPG 密钥。
* 覆盖定义背景图片的 gsetting 架构。

-- Raphaël Herzog <bubxy@kali.org> 2016年6月16日 星期四 18:04:21 +0200
```

在示例示例中，我们将对 `control` 文件进行修改。我们将 `Section` 字段更改为 `misc` 并移除 `Vcs-Git` 和 `Vcs-Browser` 字段。最后，我们将填充 `Description` 字段：

```
Source: offsec-defaults

Section: misc

Priority: optional

Maintainer: Raphaël Herzog <bubxy@kali.org>

Build-Depends: debhelper (>= 9)

Standards-Version: 3.9.8

Package: offsec-defaults

Architecture: all

Depends: $(misc:Depends)

Description: Default settings for Offensive Security

This package contains multiple files to configure owned by Offensive Security.
```

+   * 它特别修改了：
* APT 的配置
* salt-minion 的配置
* 默认桌面设置

`rules` 文件通常包含一组规则，用于在专用子目录（以生成的二进制包命名）中配置、构建和安装软件。然后，该子目录的内容将在 Debian 软件包中进行归档（前提是它是文件系统的根目录）。在这种情况下，文件将安装在 `debian/offsec-defaults/` 子目录下。例如，为了生成一个安装了 `/etc/apt/sources.list.d/offsec.list` 的包，请将文件安装在 `debian/offsec-defaults/etc/apt/sources.list.d/offsec.list`。`rules` 文件被用作 `Makefile`，包含几个标准目标（分别包括 `clean` 和 `binary` 用于清理源码目录和生成二进制包）。

### 什么是 Makefile 文件？

你可能注意到了 `dh_make` 输出最后关于缺少 `Makefile` 的信息以及对它与 `rules` 文件相似性的提到。`Makefile` 是程序使用的脚本文件，它描述了如何在依赖树中从一组文件构建出其他文件的规则。例如，一个程序可以从一组源文件构建。`Makefile` 文件以以下格式描述这些规则：

```
target: source2 ...

    command1

    command2
```

对此类规则的解释是：如果其中一个 `source*` 文件比 `target` 文件新，则需要使用 `command1` 和 `command2` 生成 `target`。

请注意，命令行必须以制表符（tab）开头；另外请注意，当命令行以连杠（`-`）开头时，命令的失败不会中断整个过程。

尽管此文件是过程的核心，但它只包含了运行 `debhelper` 工具提供的标准命令集所需的极少内容。`dh_make` 生成的文件正是如此。为了安装你所有的文件，我们建议通过创建以下 `debian/offsec-defaults.install` 文件来配置 `dh_install` 命令的行为：

```
apt/offsec.list etc/apt/sources.list.d/

apt/offsec.gpg etc/apt/trusted.gpg/

salt/offsec.conf salt/minion.d/
```

更改 (N)名字、(E)邮箱或(O)确定/(Q)退出？ o

我们需要生成大量的随机字节。在生成质数期间，执行一些其他操作（在键盘上输入、移动鼠标、利用磁盘）是一个好主意；这让数字生成器有更好的机会获取熵。
[...]

```
gpg: /home/kgrepo/.gnupg/trustdb created

gpg: key B4EF2F0DD marked as ultimately trusted

gpg: directory '/home/kgrepo/.gnupg/openpgp-revocs.d' created

gpg: revocation certificate stored as '/home/kgrepo/.gnupg/openpgp-revocs.rev'

- F8EE22F7F4F1B71AE38DA61B2B7F7F4B4EF2F0D-public and secret key and signed.
```

```
gpg: checking the trustdb

gpg: marginals needed: 3 completed: 1 trust model: PGP

gpg: depth: 0 valid: 1 signed: 0 trust-: 0q, 0n, 0m, 0u

rsa2048/B4EF2F0DD 2016-06-17 (-S)

Key fingerprint = F8EE 22F7 F4F1 71AE 38DA 61B2 B7F7 F4B4EF 2F0D

[ultimate] Offensive Security Repository Key <repoadmin@offsec.com>

rsa2048/3B0355F3 2016-06-17 (uid connected as that)
```

当提示输入密码时，你应该输入一个空值（确认不想保护你的私钥），因为你希望能够交互式地签名仓库。注意，`gpg` 需要访问终端才能安全地提示或输入密码：这就是为什么在启动 `kgrepo` shell 之前，你更改了虚拟终端的所有者（由于你最初是以 root 身份连接的，它属于 root）。

现在你可以开始设置仓库了。`repropro` 需要一个专用目录，在该目录内你必须创建一个 `conf/distributions` 文件，记录软件包仓库中提供哪些发行版：

```
$ mkdir -p repropro/conf
$ cd repropro
$ cat >conf/distributions <<END
Codename: offsec-internal

AlsoAcceptFor: unstable

Origin: Offensive Security

Description: Offsec's Internal packages

Architectures: source amd64 i386

Components: main

SignWith: F8EE22F7F4F1B71AE38DA61B2B7F7F4B4EF2F02F0D
END
```
