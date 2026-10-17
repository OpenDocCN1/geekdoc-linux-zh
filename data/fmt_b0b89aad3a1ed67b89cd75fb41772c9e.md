
| 下载 | 你可以在这里下载预发布包。 |
| Slackbuilds | |
| 文档 | |
| 管理器 | |

```
slackrepo
Introduction
New version!
slack repo
https://github.com/slackbuild/slackrepo.index
```

## 它是什么？

`Slackrepo` 是一个用于 `Slackware` 用户管理其自己的包仓库的高度自动化工具。它帮助你将一组包集合管理为一个仓库。

**图 2：** `Slackrepo` 的原始主页（如所示），但该程序由 `Andrew Clemens` 维护。

`LINUX-MAGAZINE.COM` `ISSUE 272` `JULY 2023` `37`

## 深度解析

### 自定义仓库

依赖关系。通过编译可能加载的任何包都可能导致你破坏它们使用的应用程序。当你可以使用二进制发行版中的隔离组件进行升级时，过程可能会变得复杂。

当你使用基于源码的软件供应时，你获得了一种开箱即用的解决冲突的方法。如果你需要应用补丁或将其升级到新版本，你只需要在你的系统构建中放入一个配置文件。你可以专门为你的环境进行构建并部署（通常）没有冲突。

要了解更多关于其他使用软件方法的发行版信息，请参见“基于端口的系统——编译可能加载的任何包以分发到你的系统。你可以通过这种方式将包加载到 Web 服务器，该服务器可以作为正式仓库。”

本文提供了如何使用 `slackrepo` 创建自定义仓库并使用你的 `Slack` 计算机进行的说明。`slackrepo` 服务器位于我们的局域网内，地址为 `192.168.3.24`，而其他 `Slack` 链在网络中具有硬件地址。

为了开始，你需要在你的服务器上安装完整的 `Slacksetup`。`Slackrepo` 连接到安装了所有官方软件的全新安装系统上。列表 1 总结了如何使用来自 `SlackBuild` 的脚本构建构建仓库。来自 `SlackBuilds` 的 `SlackBuild` 脚本是大多数管理员将使用的。每当使用且距离上次更新超过一天时，`slackrepo` 就会更新本地 `Slack`。

为了创建一个正式仓库，你必须创建 `GPG` 密钥来签名包。客户端需要包签名来验证下载的完整性。列表 2 显示了如何在 `slackrepo` 服务器上创建密钥并输出分发给客户端的文件。客户端将使用此文件验证包。你必须配置 `slackrepo` 使用此密钥。编辑 `/etc/slackrepo.conf` 文件并按照列表 3 所示的操作。为了确保你的文件正确，使用命令生成有效的校验和。你现在准备好部署你的包了。作为一个演示，由 `David Spencer` 和 `Andrew Clemens` 创建的 `Slackrepo` 提供了创建 `Slack` 仓库的最佳方法。`Slackrepo` 用于跟踪的工具。

## 列表 1：在 Slack 服务器上安装 Slackrepo

```
01 # 下载 slackrepo 构建脚本，解压并下载
02 # 使用脚本构建。
04 cd /tmp
05 wget https://slackbuilds.org/slackbuilds/15.0/system/slackrepo.tar.gz
06 - xf slackrepo.tar.gz
07 cd slackrepo
08 wget http://slackbuilds.org/slackbuilds/sources/repo/slackrepo-1.tar.gz
09 bash /tmp/SlackBuild
10 installpkg /tmp/slackrepo*/
12 # 下载 slackrepo 构建脚本，解压
13 # 使用脚本构建。
14 cd /tmp
16 wget https://slackbuilds.org/slackbuilds/15.0/system/slackrepo.tar.gz
17 - xf slackrepo.tar.gz
18 cd slackrepo
19 wget https://github.com/alex/slackrepo/archive/v202317-slackrepo-202317.tar.gz
20 bash /slackrepo
21 installpkg /tmp/slackrepo*/
23 # 下载 hintsfiles 构建脚本，解压，下载 hintsfiles 并
24 # 使用脚本构建。
25
26 cd /tmp
27 wget https://slackbuilds.org/slackbuilds/15.0/system/slackrepo-hints.tar.gz
28 - xf slackrepo-hints.tar.gz
29 cd slackrepo
30 wget https://github.com/alex/slackrepo/archive/v202318-slackrepo-hints-202318.tar.gz
31 bash /slackrepo-hints.SlackBuild
32 installpkg /tmp/slackrepo-hints.gz
```

## 列表 2：包签名密钥

```
01 gpg --batch --passphrase="--quick-generate-key" "Repomaster@example.com"
02 gpg --export Repomaster > GPG-KEY
```

### 客户端设置

你有一个包仓库，但如何利用它？

仓库中的包更新可以手动下载和安装，但 `slackrepo` 支持许多自动化任务的工具。之前提到的 `slackpkg` 是一个流行的选择，但在示例中，我使用的是 `slackrepo`，它是标准 `Slack` 仓库的操作客户端！

虽然 `slackrepo` 仅用于官方 `Slack` 仓库，但请构建带有依赖关系的 `hedgesedges` 包：

```
# slackrepo build hedgesedges
```

一个最小仓库将位于 `/var/lib/slackrepo/packages/`。你可以根据需要编译尽可能多的包，所有包将放在这里。你之后可以将所有内容移动到 Web 服务器：

```
# rm -rf /var/lib/slackrepo/packages/
/var/www/htdocs/
# cp GPG-KEY /var/www/htdocs/keys.asc/x86_64
```

现在，你只需要启用并启动包含 `Slack` 完整仓库的 Web 服务器：

```
# chmod x /etc/rc.d/httpd
# /etc/rc.d/httpd start
```

你可以在网上找到 `http://192.168.1.34` 仓库（如图 3 所示）。

`slackpkg+` 插件与 `slack` 仓库配合。你可以按照以下方法在客户端机器上安装 `slackpkg+`：

```
# wget http://slackinfra.org/slackpkg/
# slackpkg+-1.8.0-nonarch.no7.rpm
# yum install slackpkg+-1.8.0-nonarch.no7.rpm
```

接下来，你需要配置 `slackpkg+`。简单的方法是在每台客户端机器上编辑 `/etc/slackpkg/pkg.conf` 并设置列表 4 中的变量。

## 列表 3：slackrepo.conf 变量

```
01 USE_GENERIC_REPO=1
02 REPOSER=Repomaster repomaster@example.com
03 DL_URL=http://192.168.1.34/slackrepo/SLACKREPO/SLACKERS/ARCHIVE/
04 RSS_UPDATE=EXAMPLE_URL
05 GPG_BIN=/usr/bin/gpg2
06 FOR_SLACKPATH="1"
```

## 列表 4：在 slackpkg conf 中设置变量

```
01 REPOLIST-( custom)
02 MIRRORLIST['custom']=http://192.168.1.34/15/x86_64/
```

### 自定义 Slackware 仓库

终于，你不再需要担心 `/etc/slackpkg/rors` 中的任何官方 `Slack` 镜像源了。该仓库可用于安装你需要的任何包：

- `slackpkg-gpp-update`
- `slackpkg-update`
- `slackpkg-physs gcc ghc lua fpc-headers`

请记住，`slackpkg` 不进行依赖跟踪；当你执行常规 `Slackware` 更新时，自定义仓库中安装的任何包都会被 `slackpkg` 提取：

- `slackpkg-update`
- `slackpkg-upgrade-all`

### 自定义包

在某些时刻，你可能需要构建一个自定义包。如果你发现它没有包含在 `SlackBuild` 数据库中，最好的方法是创建自己的 `SlackBuild` 脚本并将其提交到 `SlackBuilds`。这样社区以及你都可以从高可用服务器获取该构建脚本。

如果你需要使用一组特定的配置选项来构建包，

（此处为图片）
