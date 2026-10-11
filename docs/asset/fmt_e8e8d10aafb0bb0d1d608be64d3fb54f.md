
## 10.3. 扩展和定制 Kali Linux

有时你需要修改 Kali Linux 以满足本地需求。实现这一点的最佳方法是维护一个你自己的软件包仓库，托管那些你需要分叉（fork）的 Kali 软件包的修改版本，以及提供自定义配置和额外软件（Kali Linux 未提供）的补充软件包。

### 10.3.1. 分叉 Kali 软件包

关于此主题的详细说明，请参阅第 9.1 节，“修改 Kali 软件包”[第 222 页]。如果你有充分的理由，可以分叉任何软件包，但必须意识到分叉软件包是有成本的，因为每次 Kali 发布更新时，你都必须对其进行更新。以下是一些你之所以想要分叉软件包的原因：

- 添加补丁以修复 bug 或添加新功能。尽管在大多数情况下，你最好将该补丁提交给上游开发者，以便在源头修复 bug 或添加功能。
- 使用不同的选项进行编译（假设 Kali 未使用这些选项编译有正当理由；否则最好与 Kali 开发者讨论，看他们是否能启用所需的选项）。

相反，以下是一些分叉软件包的不良理由，以及处理问题的建议：

- 修改配置文件。你有多个更好的选项，例如使用配置管理自动安装修改后的配置文件，或安装一个配置包，该包会将文件放入配置目录（如果可用），或者将原始配置文件重定向。
- 更新到新的上游版本。同样，最好与开发者合作，直接在 Debian 或 Kali 中更新软件包。在滚动发布模式下，更新能够相当快速地到达最终用户。

在所有可用的软件包中，有一些是 Kali Linux 的构建模块，在某些情况下可能值得分叉：

- `kali-meta`：此源码包构建所有的 `kali-linux-*` 元软件包，特别是 `kali-linux-full`，它定义了默认 Kali Linux ISO 镜像中安装的软件包。
- `desktop-base`：此源码包包含桌面安装中默认使用的各种杂项文件。如果你希望在默认背景中展示你组织的品牌，或更改桌面主题，可以考虑分叉此软件包。
- `kali-menu`：此软件包定义 Kali 菜单的结构，并为应在 Kali 菜单中列出的所有应用程序提供 `.desktop` 文件。

### 10.3.2. 创建配置软件包

既然我们已经讨论了 PXE 引导以及使用 SaltStack 进行配置管理，还讨论了软件包分叉，现在是时候将这些流程整合到一个实用示例中，并通过创建一个自定义配置软件包来部署自定义配置到多台机器，从而扩展该场景。

在本例中，你将创建一个自定义软件包，该软件包设置并利用你自己的软件包仓库和 GnuPG 签名密钥，分发 SaltStack 配置，推送自定义背景，并以统一的方式为所有 Kali 安装提供默认桌面设置。

这看起来可能是一项艰巨的任务（特别是如果你浏览一下 Debian 新维护者指南[1]），但幸运的是，配置软件包主要是一个高级的文件归档，将其转换为软件包相对容易。

**查看示例软件包**

如果你想查看一个基本上作为配置软件包的真实软件包，可以考虑 `kali-defaults` 软件包。它没有本节的示例那么简单，但具备所有相关特性，甚至使用了一些高级技术（如 `dpkg-divert`）来替换其他软件包已提供的文件。

> [1] https://www.debian.org/doc/manuals/maint-guide/

`offsec-defaults` 软件包将包含几个文件：

- `/etc/apt/sources.list.d/offsec.list`: APT 的 sources.list 条目，启用公司内部软件包仓库
- `/etc/apt/trusted.gpg.d/offsec.gpg`: 用于签署公司内部软件包仓库的 GnuPG 密钥
- `/etc/salt/minion.d/offsec.conf`: SaltStack 配置文件，用于指示在哪里找到 Salt 主节点
- `/usr/share/images/offsec/background.png`: 一张带有 Offensive Security 徽标的精美背景图片
- `/usr/share/glib-2.0/schemas/90_offsec-defaults.gschema.override`: 提供 GNOME 桌面备用默认设置的文件

首先，创建一个 `offsec-defaults-1.0` 目录并将所有文件放入该目录。然后运行 `dh_make --native`（来自 `dh-make` 软件包）以添加 Debian 打包指令，这些指令将存储在 `debian` 子目录中：

```bash
$ mkdir offsec-defaults-1.0; cd offsec-defaults-1.0

$ dh_make --native

Type of package: (single, indep, library, python)

[s/i/l/L/p]? i

Email-Address   : buxy@kali.org

License         : gpl3

Package Name    : offsec-defaults

Maintainer Name : Raphaël Hertzog

Version         : 1.0

Package Type    : indep

Date            : Thu, 16 Jun 2016 18:04:21 +0200

Are the details correct? [Y/n/q] y

Currently there is not top level Makefile. This may require additional tuning

Done. Please edit the files in the debian/ subdirectory now.
```

首先，你会被提示输入软件包类型。在示例中，我们选择了 `indep`，这表示该源码包将生成一个可以在所有架构之间共享的单一二进制软件包（Architecture: all）。`single` 作为对应项，生成一个依赖于目标架构的单一二进制软件包（Architecture: any）。在这种情况下，`indep` 更为相关，因为软件包仅包含文本文件，没有二进制程序，因此可以在所有架构的计算机上类似地使用。`library` 类型对于共享库很有用，因为它们需要遵循严格的打包规则。类似地，`python` 应限制用于 Python 模块。

**维护者姓名和电子邮件地址**

参与软件包维护的大多数程序会在 `DEBFULLNAME` 和 `DEBEMAIL` 或 `EMAIL` 环境变量中查找你的姓名和电子邮件地址。一旦定义了这些变量，就可以避免多次重复输入。如果你的常用 shell 是 Bash，只需在 `~/.bashrc` 文件中添加以下两行即可。例如：

```bash
export EMAIL="buxy@kali.org"
export DEBFULLNAME="Raphael Hertzog"
```

`dh_make` 命令创建了一个包含许多文件的 `debian` 子目录。有些是必需的，特别是 `rules`、`control`、`changelog` 和 `copyright`。带有 `.ex` 扩展名的文件是示例文件，可以通过修改并移除扩展名来使用。如果不需要它们，我们建议删除。应保留 `compat` 文件，因为它对于 `debhelper` 程序套件（均以 `dh_` 前缀开头）的正确功能是必需的，这些程序在软件包构建过程的各个阶段使用。

`copyright` 文件必须包含关于软件包中包括文档的作者的详细信息以及相关的许可证。如果 `dh_make` 选择的默认许可证不适合你，则必须编辑此文件。以下是修改后的 copyright 文件：

```
Format: https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/
Upstream-Name: offsec-defaults
Files: *
Copyright: 2016 Offensive Security
License: GPL-3.0+
License: GPL-3.0+
 This program is free software: you can redistribute it and/or modify
 it under the terms of the GNU General Public License as published by
 the Free Software Foundation, either version 3 of the License, or
 (at your option) any later version.

 .
 This package is distributed in the hope that it will be useful,
 but WITHOUT ANY WARRANTY; without even the implied warranty of
```
