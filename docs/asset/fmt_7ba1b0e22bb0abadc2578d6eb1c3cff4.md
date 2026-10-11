
我们完成了！还有比这更简单的吗？

## 配置 apt-get

配置 `apt-get` 非常简单，这是 Debian 文档有时还不错的领域之一；你几乎需要知道的一切信息可以在 APT HOWTO 中找到：

http://www.debian.org/doc/manuals/apt-howto

最重要的 `apt-get` 配置文件是 `/etc/apt/sources.list`，它列出了 `apt-get` 从何处获取软件包。每行定义了以下内容：软件包类型当前为 `deb` 或 `deb-src`；指向文件、CD-ROM、HTTP 服务器或 FTP 服务器的 URL，从那里获取软件包；一个“发行版”，允许你交付多个版本的软件包（Debian 使用它对发行版进行版本控制，你也可以将其用于内部版本）；以及潜在的组件列表——本质上是发行版内的软件包类别。

除非你想建立自己的 APT 仓库或缓存，否则默认配置通常运行良好。如果你有良好的网络连接，你可能想注释掉 Debian CD-ROM 的行。如果你想下载源代码，在编辑文件时取消指定 `deb-src` 的行的注释；你应该将 Debian 镜像的标识更改为离你较近的一个；可以在此处找到完整的镜像列表：

```bash
* http://www.debian.org/misc/README.mirrors
```

为了让这些事情变得极其简单，Debian 提供了一个名为 `netselect-apt` 的工具，它可以自动为你生成一个 `sources.list` 文件；它根据 ping 时间选择它能找到的最近镜像。`netselect-apt` 是 `netselect` 软件包的一部分，可以从最近的 Debian 镜像获取。

你还应该确保 `security.debian.org` 被列为源，这样你就可以访问最新的安全补丁了。

## 一个 /etc/apt/sources.list 文件示例

以下示例使用 `http.us.debian.org` 作为稳定版存档，但添加了 `non-us.debian.org` 作为非美国软件包的源（无法从美国出口的加密材料）。我们添加了安全补丁，以及我们的本地 APT 服务器 `debserver`。最后，我们开启了源代码下载。

```
deb http://us.debian.org/debian stable main contrib-free

deb http://non-us.debian.org/debian-non-US stable/non-US main contrib-free

deb http://security.debian.org/debian stable/updates main contrib-free

deb http://debserver.org/packages/

deb-src http://us.debian.org/debian stable main contrib-free

deb-src http://non-us.debian.org/debian-non-US stable/non-US main contrib-free

deb-src http://security.debian.org/debian stable/updates main contrib-free
```

此示例使用了稳定仓库。在实践中，稳定的 Debian 发行版的发布频率不如其他版本。如果你需要来自 `testing`（测试版）或 `unstable`（不稳定）发行版的软件包，只需复制稳定行并将其替换为 `unstable`（或 `testing`）即可。行是按顺序查询的，因此将 `unstable` 和 `testing` 的行放在文件末尾，以确保稳定版本具有优先级。

## 使用代理扩展 apt-get 规模

如果你在多台机器上使用 `apt-get`，你可能想在本地缓存软件包——为每台机器下载每个软件包的副本并不是带宽的合理利用。如果你的防火墙需要这种额外的保护，你可能还需要将 `apt-get` 指向代理。`apt-get` 使用原生的 HTTP 和 FTP，你可以使用任何你可能已经安装的代理。

作为 RPM 的替代方案，RPM 对于源码软件包有等效于 SRPM 的物，而 Debian 将源码软件包分发为三个部分：原生的 `.tar.gz` 文件、可选的 `.diff.gz` 文件（软件包维护者用它显示相对于原始代码分发所做的更改），以及一个包含软件包描述的 `dsc` 文件。`Packages.gz` 的源码等效物是 `Sources.gz`；它也由 `apt-ftarchive` 生成。

## 自动化 apt-get

你可以通过 `cron` 定期运行 `apt-get`。如果你不自动安装软件包，你可能想定期运行 `apt-get update` 以保持软件包摘要更新。

`apt-get dist-upgrade` 将下载并安装本地机器上已安装任何软件包的新版本。`dist-upgrade` 与 `upgrade` 类似，但具有稍微智能的依赖关系处理。如果你想玩火，可以让机器自动执行此升级——使用 `-yes` 参数进行无人值运行 operation；它会以热烈的“Yes！”回答 `apt-get` 可能会提出的确认问题。

直接从 Debian 镜像源进行自动化的升级可能不是一个好主意。然而，如果你有自己的 APT 服务器、软件包和发布控制系统，那么这就是保持客户端同步的完美方法。一个简单的 shell 脚本就可以让机器保持与你的 APT 服务器同步更新：

```bash
#!/bin/sh

apt-get update

apt-get -yes dist-upgrade
```
