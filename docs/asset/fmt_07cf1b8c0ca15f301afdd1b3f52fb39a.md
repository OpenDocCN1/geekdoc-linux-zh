
# v:4.33

作为数字取证平台的 Linux 全方位入门指南

```
连接到 pink-mist.github.io (pink-mist.github.io)|151.101.20.133|:80...

已连接。

发送 HTTP 请求，等待响应... 200 OK

Length: 43885 (43K) [application/octet-stream]

保存到：'sbotools-2.3.tar.gz'

sbotools-2.3.tar.gz 100%====================> 42.86KB --KB/s in

0.03s

2017-04-17 22:11:16 (1.39 MB/s) - 'sbotools-2.3.tar.gz' 保存 [43885/43885]
```

```
rootforensic1:-/sbotools$ ls
README
sbotools-2.3.tar.gz sbotools.info
sbotools.SlackBuild* slack-desc
rootforensic1:-/sbotools md5sum sbotools-2.3.tar.gz
9b7525e9f93717e3f7ff7a2e02da8 sbotools-2.3.tar.gz
```

对下载的源文件执行 `md5sum` 命令的输出结果与 `sbotools.info` 文件中的 MD5SUM 字段匹配，因此我们知道下载是正确的。

现在，如果我们还没有这样做的话，我们需要读取 `README` 文件（使用 `cat` 或 `less`）……了解注意事项并安装可选依赖项……然后编译我们的源代码并制作我们的 Slackware .tgz 包。后两个步骤只需通过通过 `./sbotools.SlackBuild` 调用 SlackBuild 文件本身即可完成：

```
rootforensic1:-/sbotools# ./sbotools.SlackBuild
sbotools-2.3/
sbotools-2.3/sbotlean
sbotools-2.3/man5/
sbotools-2.3/man5/sbotools.conf.5

正在检查您的工具包是否完整...

看起来不错

....

正在创建 Slackware 包：/tmp/sbotools-2.3-noarch-1_SBo.tgz

...usr/man/man1/sbosnap.1.gz

usr/man/man5/

usr/man/man5/sbotools.conf.5

Slackware 包 /tmp/sbotools-2.3-noarch-1_SBo.tgz 已创建。
```

查看输出行，我们看到已经在 `/tmp` 中为我们创建了一个可用的 .tgz Slack 包。我们只需要使用来自 `pkgtools` 的 `installpkg` 安装该包即可：

```
root@forensic1:~/sbtools# installpkg /tmp/sbtools-2.3-noarch-1_Sbo.tgz
gz
正在验证包 sbtools-2.3-noarch-1_Sbo.tgz。
正在安装包 sbtools-2.3-noarch-1_Sbo.tgz:
软件包描述:
### sbtools (类似于 ports 的 SlackBuild 接口)
#
# sbtools 是一组 perl 脚本，为 SlackBuilds.org 提供了类似于 ports 的自动化
# 接口。它的功能包括需求处理
# 以及在多库 x86_64 系统上处理 32 位和 compat32 构建的能力。
#
# https://pink-mist.github.io/sbtools/
#
包 sbtools-2.3-noarch-1_Sbo.tgz 已安装。
```

### 使用自动化工具包 sbtools

现在，我们已经安装了 `sbtools`，我们将使用它来代替所有的下载、md5 检查、提取和构建。非常重要的一点是，我们要留意每个包的 `README`，并确保不要让自动化让我们产生掉心理。阅读你正在安装的每个包的文档，熟悉它对你的系统做了什么以及你可能想要启用或禁用的选项。

第一次调用 `sbtools` 时，我们需要初始化 SlackBuild 仓库。默认情况下，`sbtools`（通过 `snobnap`）将拉取整个 SlackBuild 树（从 SlackBuilds [sbo]）并放入 `/usr/sbo/repo`。

```
root@forensic1:~/sbtools$ snobnap fetch
正在拉取 SlackBuild 树...
87,402,684 100%    3.73MB/s    00:00:22 (xfr#458434, to-chk=0/52275)
```

```
root@forensic1:~/sbtools$ ls /usr/sbo/repo
CHECKSUMS.md5 TAGS.txt          desktop/ ham/      office/
CHECKSUMS.md5.asc TAGS.txt.gz development/ haskell/ perl/
ChangeLog.txt academic/ doit.sh libraries/ python/
README accessibility/ games/     misc/       ruby/
SlackBuilds.TXT audio/      gis/        multimedia/ system/
SlackBuilds.TXT.gz business/  graphics/  network/
```

一旦完成，你可以使用以下命令通过单条命令搜索、安装和升级包及其初始依赖项：

- `sbtfind`：根据名称和关键词搜索包
- `sbocheck`：更新仓库并识别需要升级的包
- `sboinstall`：安装包（及其依赖项）
- `sbouprade`：升级已安装的包

在本文的剩余部分，我们将使用 `sbtools` 安装软件。

但让我们从一个简单的防病毒/恶意软件检测软件的快速安装示例开始，我们稍后会介绍。

我有一个干净的 Slack 系统，只安装了一个外部软件包 `sbtools`。现在我想安装更多软件。让我们从 ClamAV (`clamav`) 开始，这是一个病毒/恶意软件扫描器。我们使用 `sbfind` 搜索 `clamav`。然后我们缩小范围并查看 `README` 文件。接着我们只需运行 `sboinstall` 即可为你下载、检查、构建并安装该包。这一切的快捷方法只需输入 `sboinstall clamav` 就完成了。但我更倾向于使用更谨慎的方法。

首先，让我们搜索匹配 `clamav` 的可用包：

```
root@forensic1:~# sbfind clamav
SBo: thunar-sendto-clamkt
Path: /usr/sb/repo/desktop/thunar-sendto-clamkt

SBo: clamav-unofficial-sigs
Path: /usr/sb/repo/network/clamav-unofficial-sigs

SBo: clamav
Path: /usr/sb/repo/system/clamav

SBo: clamsmtp
Path: /usr/sb/repo/system/clamsmtp

SBo: clamkt
Path: /usr/sb/repo/system/clamkt
```

（注：由于原始文本中存在大量由于“再次运行 `sbfind`，但将输出限制为精确匹配 `clamav` (-e) 且无标签 (-t) 并查看包的 `README` (-r)”以及类似的 OCR 错误导致的重复，译文已根据逻辑流进行了清理和去重。）
