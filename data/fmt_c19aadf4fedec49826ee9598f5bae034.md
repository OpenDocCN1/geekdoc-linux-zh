
## 下载/编译源码和二进制 Debian
`deget` 通过名称下载源码包和二进制包。它不需要本地 `Packages` 文件的副本，而是列出 FTP 站点上的目录以查找哪些可用内容。Debian 可以选择性挑选并编译源码包，然后安装生成的二进制包。如果你打算使用这些功能，你应该安装 `devscripts` 软件包以获取描述脚本。来自 Debian 3.0r0 APT http://www.tld.org/LDP/Linux-Dictionary/html/index.html

## debhelper
用于 `debian/rules` 的辅助程序。一组可以在 `debian rules` 文件中使用的程序，用于自动化与构建 debian 软件包相关的常见任务。包含的程序包括将各种文件安装到你的软件包中、压缩文件、文件权限、将你的软件包与 debian 菜单系统、系统管理、doc-base 等集成。大多数 debian 软件包都将 `debhelper` 作为其构建过程的一部分。来自 Debian 3.0r0 APT http://www.tld.org/LDP/Linux-Dictionary/html/index.html

## DEBI
Debian GNU/Linux
Debian 项目是最大的志愿者发行提供者。Debian 有一个稳定版本 2.2 (`potato`)，一个较新的稳定版本 3.0r1 (`woody`)，以及不不稳定但更新的分支。来自 LWN 分发列表 http://www.tld.org/LDP/Linux-Dictionary/html/index.html

## debian-cd
构建（官方）Debian CD 的工具。`debian CD` 是自 `potato` 发布以来构建 Debian CD 的 `is-cd` 工具。它以前被称为 YACS（另一组 CD 集）。它的目标是方便定制 Debian CD 的创建。来自 Debian 3.0r0 APT http://www.tld.org/LDP/Linux-Dictionary/html/index.html

## debian-guide
文本自：《Debian GNU/Linux: 安装与使用指南》。此软件包将安装由 Debian 开发者 John Goerzen 和 Ossama Oman 编写的《Debian GNU/Linux: 安装与使用指南》一书的完整 HTML 和 PostScript 版本（ISBN 0–7357–0914–9）。你可以使用 `/usr/doc/debian-guide` 找到已安装的项目。来自 Debian 3.0r0 APT http://www.tld.org/LDP/Linux-Dictionary/html/index.html

## Debian-Ham
Debian-Ham 是一个专门用于竞赛和记录的软盘发行版。它基于 uClique、busbox 和 it。目前的方案使用带有 minix 根软盘的 LILO 软盘。包含了 DX 集群的网络支持。Initialfresh 发布了 0.3 版本，于2002 年 7 月 21 日发布。0.5 版本于 2003 年 4 月 24 日发布。一种基于软盘的发行版。来自 LWN 分发列表 http://www.tldp.org/LDP-Linux-Dictionary/html/index.html

## Debian-Jr.
这是一个内部项目，旨在让所有年龄的儿童都想要使用的 Debian 系统。我们的重点是为8 岁以下的儿童制作东西。我们已经实现了，下一个目标范围是 12 岁。当孩子们进入青少年时期时，他们将可以在没有任何特殊修改的情况下熟练使用 Debian。来自 LWN 分发列表 http://www.tldp.org/LDP-Linux-Dictionary/html/index.html

## debian-keyring
Debian 开发者的 GnuPG（以及已过时的 PGP）密钥。Debian 项目希望开发者使用 GnuPG 对其软件包的公告进行数字签名以防止伪造。此软件包包含了开发者的 GnuPG 密钥和（弃用的）PGP 密钥。来自 Debian 3.0r0 APT http://www.tldp.org/LDP-Linux-Dictionary/html/index.html

## Debian-Med
Debian-Med 是一个支持医疗护理人员任务的内部项目。Debian-Med 的目标是仅使用自由软件构建一个完整的医疗护理系统。一种“特殊用途/小型”发行版。来自 LWN 分发列表 http://www.tldp.org/LDP-Linux-Dictionary/html/index.html

## debian-policy
Debian 策略手册及相关文档。此软件包包含：Debian 策略手册 – Linux 文件层次结构 (`FHS`) – 虚拟软件包权威列表 – 关于 `libc6` 的论文 – Debian 策略。它还包含了用于软件包迁移的检查列表。来自 Debian 3.0r0 APT http://www.tldp.org/LDP-Linux-Dictionary/html/index.html

## debian-test
测试已安装 Debian 系统的脚本。`debian-test` 包含了供其他软件包运行的测试框架，它在安装时运行这些测试以确保系统正常工作。来自 Debian 3.0r0 http://www.tldp.org/LDP-Linux-Dictionary/html/index.html

## debiadoc-sgml
Debian SGML 格式工具。这是一个基于 SGML 的程序，用于格式化软件包。它可以生成 DVI（通过 `tex`）、HTML（通过 `tex`）、PostScript（通过 `tex`）以及 Info（通过 `texinfo`）。它使用 `texinfo` 软件包。来自 Debian 3.0r0 http://www.tld.org/LDP-Linux-Dictionary/html/index.html

## debianutils
针对 Debian 的杂用工具。Debian 包含了一些用于帮助用户和开发者的微型实用程序。来自 Debian 3.0r0 http://www.tldp.org/LDP-Linux-Dictionary/html/index.html

## debmake
Debian 软件包生成工具。`debmake` 是一个从源码生成 Debian 软件包的工具。在以下情况下非常有用：
- 创建 DVD/CD Debian（使用 `debs`）
- 仅镜像软件包（使用 `debspt`）
- 维护软件包（使用 `debst`）
- 具有以下能力：
  - 在 `deb` 软件包中生成维护脚本。
  - 在 `deb` 软件包中执行维护脚本。
  - 字体 帮助开发者在配置 文件中进行修改。
  - 支持 GPG 签名的维护脚本。
  - 带有 GPG 签名的 `deb` 软件包。
  - 检查符号链接以确保文件已压缩。
来自 Debian 3.0r0 APT http://www.tld.org/LDP-Linux-Dictionary/html/index.html

## debootstrap
从零启动 Debian 系统。`debootstrap` 在不需要 `dpkg` 或 `apt` 的情况下，从零创建一个 Debian 系统。它通过从镜像下载文件并将其解压到目录来实现。来自 Debian 3.0r0 http://www.tld.org/LDP-Linux-Dictionary/html/index.html

## deorphan
查找系统中没有其他软件包依赖的孤立软件包。它在安装期间确定哪些软件包，在查找库时非常有用。来自 Debian 3.0r0 APT http://www.tld.org/LDP-Linux-Dictionary/html/index.html

## departial
Debian 软件包/源码分区工具。这是一个根据软件包大小准备 `Package.gz` 和 `Sources.gz` 的程序。它可以用于以下情况：
- 创建 DVD/CD Debian（使用 `debs`）
来自 Debian 3.0r0 APT http://www.tld.org/LDP-Linux-Dictionary/html/index.html

## deroster
一个用于使用的软件包。`deroster` 会启动一个以 Debian Logo 为背景的环境，屏幕上随机滚动当前开发者列表。可以使用它查看有多少人贡献了 Debian 项目以及我们这样做 :) 来自 Debian 3.0r0 APT http://www.tld.org/LDP-Linux-Dictionary/html/index.html

## debsig-verify
Debian 软件包签名验证工具。它根据预定义的策略检查并验证软件包签名。来自 Debian 3.0r0 APT http://www.tld.org/LDP-Linux-Dictionary/html/index.html

## debsigs
