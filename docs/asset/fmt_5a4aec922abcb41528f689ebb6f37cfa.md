
# Debian 系统的安全性

警告：以下软件包无法通过验证！

`openssl` `ssl-cert` `apache2-common` `apache2-mpm-worker` `apache2`

是否在不验证的情况下安装这些软件包？[y/N]

此外，如果使用了 `--assume-yes` 选项，安装将中止。你必须明确强制 APT 安装未验证的软件包，即使在启用了 `--assume-yes` 的情况下也是如此：

```
# apt-get install apache2
[...
WARNING: 以下软件包无法通过验证！
openssl ssl-cert apache2-common apache2-mpm-worker apache2
E: There are problems and --yes was used without --force-yes
```

## 使用安全 APT

在编写本文时，APT 0.6 是一项实验性软件，仅从 Debian 镜像上的实验存档可用。虽然正在努力与 sarge 一起发布 APT 0.6，但软件包管理工具与 APT 之间的紧密依赖关系可能导致 APT 0.6 被推迟到 etch 进入开发阶段。尽管如此，已经可以使用 APT 0.6 了，下面将演示这一点。

你可以通过向 `/etc/apt/sources.list` 添加如下行来从实验存档获取 APT 0.6。请考虑使用更近的镜像而不是 ftp.debian.org¹16。

```
# cat <<EOF >> /etc/apt/sources.list
deb http://ftp.debian.org/debian experimental main
EOF
# apt-get update
[...]
# apt-get install --target-release experimental apt
[...]
```

遗憾的是，在编写此时，其他部署 APT 的软件尚未更新到 0.6 版本。因此，安装 APT 0.6 会与 `aptitude` 和 `tasksel` 等软件包冲突，并需要删除它们。显然，当安全 APT 正式发布后，这种限制将会消失。

安装后，建议删除或注释 `/etc/apt/sources.list` 中的实验行，并在安装新软件包之前更新 APT，以避免无意中将实验性软件安装到系统中。实验优先级（见第 8.2.1 节）其他发行版不可用的软件包将根据请求从实验源满足。

> 16参见第 5.4.1 节或 http://www.debian.org/mirror/list

## 问题与缺点

APT 0.6 支持的 APT 验证机制对现有基础设施的较小，并在标准使用场景下可靠工作。然而，它也存在主要的缺点。首先，它需要基础设施支持才能进行验证。存档必须发布并签名 Release 文件，而这些文件在验证时可能在本地可用。此外，该方法只能验证当前的软件包。当 1.0-2 版本的软件包已进入镜像并替换了池中的旧版本以及 Packages 索引时，无法验证例如版本 1.0-1 软件包的真实性或完整性。

另一个相关的缺点是 APT 的验证机制只允许检查存档中的软件包。当通过其他手段获取 DEB 文件时，没有办法验证其真实性或完整性。APT 的 MD5 和检查主要为 Debian 镜像基础设施提供安全性，防止其中一个镜像被破坏。因此，它是一个充分的工具。然而，它不能被视为软件包签名系统的完整实现。

## 7.5.3 debsigs 和 dpkg-sig

虽然 APT 0.6 使用索引来验证软件包完整性，因此在索引不可用时作用很小，但另外两个工具使用附加到 DEB 文件上的签名进行完整性验证：`dpkg-sig` 和 `debsigs`。`debsigs`（在 `debsigs` 软件包中）在 potato 发布后不久编写。在此，另一个程序 `dpkg-sig`（在 `dpkg-sig` 软件包中）被授权处理其缺点¹⁷。

软件包签名类似于电子邮件中使用的数字签名，由存档中所有文件的列表（见 5.2.3 节）、以及签名和 MD5 哈希值组成。该列表位于自己的文件中，只需插入存档中。这种方法允许每个软件包积累签名数量，由于签名位于 DEB 文件之前，发行介质包含了验证所需的所有内容。

APT 验证需要基础设施支持，任何人可以使用 `debsigs` 或 `dpkg-sig` 为 DEB 文件添加签名。`dpkg-sig` 直接源于 `debsigs`，在签名创建和验证方面应优于 `debsigs`。除了 `debsigs` 的功能外，它允许对软件包进行远程签名并保持策略合规，而 `debsigs` 创建的是不兼容 DEB 文件⁸。

> ¹⁷http://dpkg-sig.debian.net

¹⁸http://bugs.debian.org/16593

### Debian 系统的安全性

使用 `dpkg-sig` 非常简单，它假设存在 GnuPG 和一个私钥。`-k` 选项允许指定密钥进行签名，`dpkg-sig` 还尊重 `$DEBSIGN_KEYID`，该值可以通过 `$DPGSIG_KEYID` 覆盖。每个签名由名称标识，主要用于标识签名者的角色。对于实例软件包，软件应使用 "builder" 作为签名名称：

```
# dpkg-sig --sign builder postfix_2.1.5-1_i386.deb
Processing postfix_2.1.5-1_i386.deb..
```

你需要密码来解锁用户的私钥：'Martin F Kraft <madduck@madduck.net>' 1024 位 DSA 密钥，ID 330C4A75，创建于 2001-06-02

输入密码：

Signed deb postfix_2.1.5-1_i386.deb

使用 `dpkg-sig` 验证 DEB 文件同样简单：

```
# dpkg-sig --verify postfix_2.1.5-1_i386.deb
GOODSIG ACF49D3E1EID5EE2B2035E53220BC8330C4A75 109342208
```

DEB 文件的任何修改在验证时被 `dpkg-sig` 捕。签名认证存档中所有数据的 MD5 和，无论是对 `control.tar.gz` 中的控制文件、`data.tar.gz` 中的数据进行修改，还是通过向 DEB 文件插入新数据，都没有区别。例如，向 DEB 负载中间插入一个虚拟文件将使签名失效：

```
# echo dummy dummy
# ar rb data.tar.gz postfix_2.1.5-1_i386.deb dummy
# ar t postfix_2.1.5-1_i386.deb
debian-binary
control.tar.gz
dummy
data.tar.gz
_ppgbuilder
# dpkg-sig --verify postfix_2.1.5-1_i386.deb
Processing postfix_2.1.5-1_i386.deb...
BADSIG builder:
```

显然，`dpkg-sig` 仅检查软件包的签名，而不检查用于签名消息的密钥的真实性。在信任一个软件包之前，必须信任用于签署它的密钥的签名。

除了手动验证外，目前尚不存在针对软件包签名的集成验证机制。在 sarge 发布之后，将开始工作使软件包签名跟上时代水平。此外，一些开发者（包括我本人）已经在思考如何实现一种全方位基于策略的签名验证机制了。

## 高级概念

> 惊险的冒险！

跟随 J. Random 系统管理员的故事，看他如何与邪恶作斗，救出落落的少女，并打磨他的 Debian GNU/Linux 安装！

— Lars Wirzenius

到目前为止书中介绍的概念和技术对于大多数用途来说，已经足够成功管理 Debian 系统。尽管如此，仍然存在特殊需求，而 Debian 存档拥有工具来满足大多数此类需求。在本章中，你将学习如何为自定义且可能经过补丁的内核构建软件包、创建内核模块包、以合理的方式混合不同的 APT 仓库，并使用 Debian 安装程序的替代方案来安装 Debian 系统。

### 8.1 使用 make-kpg 构建内核包

`make-kpg` 是 Debian 的内核包工具。它提供了一个内核编译的一站式接口，创建 DEB 文件来封装内核、头文件、源码和文档，方法如第 5.12.2 章和 5.12.3 章所示。此外，`make-kpg` 允许为任何 Debian 内核轻松编译模块，并对 Debian 内核源码应用补丁。

`make-kpg` 工具位于 `kernel-package` 软件包中（一个真不巧的名字）。`kernel-package (5)` 为你管理了使用 `make-kpg` 为 Debian 系统构建内核的优缺点。此外，`make-kpg (5)` 包含了关于程序本身的大量信息，在 `/usr/share/doc/kernel-package` 下可以找到许多额外信息。

与 `make` 类似，`make-kpg` 通过目标（targets）工作。重要的目标如下：

- `kernel_image`

  - 构建内核镜像并将其转换为 DEB 文件。

- `kernel_headers`

  - 创建包含内核头文件的 DEB 文件，该头文件针对内核源码树所配置的架构和处理器类型。

- `kernel_source`
