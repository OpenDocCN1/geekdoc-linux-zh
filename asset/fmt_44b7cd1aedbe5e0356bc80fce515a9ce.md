
$ `/etc/yum.repos.d`

`fedora.repo` `fedora-updates.repo` `fedora-testing.repo`

```
```

在这些文件之一中设置的仓库将覆盖 `[main]` 部分（`yum.conf`）中的相同设置。这些文件中的每一个都包含一个文件头，例如 `[fedora]`，它为仓库提供了一个唯一的名称。文件名通常与仓库名称相似，增加了 `fedora-` 前缀和 `.repo` 扩展。常用的仓库包括 `fedora`（位于 `fedora.repo` 文件中），它包含安装 DVD 上的软件包（稳定包）；`updates`（位于 `updates-repo` 文件中），它包含稳定包的更新版本；以及 `updates-testing`（位于 `updates-testing.repo` 文件中），它包含尚未准备发布的更新。最后一个仓库未被启用；除非你正在测试不稳定的软件包，否则不要启用它。永远不要在生产系统上启用 `updates-testing` 仓库。

每个 `*.repo` 文件包含几个相关仓库的规范，这些仓库通常是禁用的。例如，`fedora.repo` 文件除了 `[fedora]` 之外还包含 `[fedora-debuginfo]` 和 `[fedora-source]`。你无法使用 `yum` 下载源文件。相反，请使用 `yumdownloader`（第 541 页）执行此任务。

## 544 第 13 章 查找、下载和安装软件

下一个示例显示了 `fedora.repo` 文件的部分，它指定了 fed 仓库的参数：

```
$ cat /etc/yum.repos.d/fedora.repo

[fedora]

name=Fedora $releasever=$basearch

failovermethod=priority

#baseurl=http://download.fedaproject.org/pub/fedora/linux/releases/$releasever/Everything/$basearch/

mirrorlist=https://mirrors.fedaproject.org/metalink?repo=fedora-$releasever&arch=$basearch

enabled=1

metadata_expire=7d

gpgcheck=1

gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-Fedora-$basearch
```

每个仓库规范文件包含在方括号 `[]` 中的仓库名称、一个名称、一个 `failovermethod`、一个 `baseurl` 和 `mirrorlist`。`mirrorlist` 为 `yum` 显示的仓库提供了一个正式名称。`failovermethod` 决定了当第一次失败时 `yum` 联系额外镜像站的顺序；`priority` 按照它们出现的顺序选择站点，而 `roundrobin` 则随机选择。`baseurl` 指明主仓库的位置；默认被注释掉。`mirrorlist` 指定了一个包含 `baseurls` 列表或主仓库镜像列表的文件的 URL。一次只能启用 `baseurl` 或 `mirrorlist` 之一。这些定义使用了两个变量：`yum` 选择 `$basearch` 代表系统架构（例如 `i686`），选择 `$release` 代表发行版本（例如 Fedora 15 的 `15`）。

如果 `enabled` 设置为 1，则文件描述的仓库被启用（`yum` 将使用它）；如果设置为 0，则被禁用。`metadata_expire` 指定了 `yum` 认为元数据有效的时间：在此时间之后，`yum` 会下载新的元数据。默认为六小时。如前所述，`gpgcheck` 决定了 `yum` 是否检查其下载的文件的 G 签名。`gpgkey` 指定了 GPG 密钥的位置。请参考 `yum.conf` 手册获取更多选项。

添加仓库：有很多软件软件包仓库。如需更多信息和仓库列表，请访问 `fedoraproject.org/wiki/Third_party_repositories`。你也可以在互联网上搜索 fed 仓库。这些网站中最有趣的之一是 `repos.fedorople.org`。这些站点提供了仓库规范文件。通过将规范文件放在 `/etc/yum.repos.d` 来向系统添加仓库——参见以下安全提示。

### 使用信任的仓库

对于你添加的仓库要谨慎：当你添加仓库时，你在信任该仓库不会发布恶意软件。此外，不支持 Fedora 的软件包可能与其他软件包冲突或升级失败。

## 597 BitTorrent

下载 BitTorrent 文件的最简单方法是在浏览器中点击种子文件；这会打开 GUI。本节描述了 BitTorrent 如何工作并解释了如何从命令行下载文件。

BitTorrent 协议实现了一种混合客户端/服务器和 P2P（第 1180 页）传输机制。BitTorrent 高效地分发大量数据，例如 Fedora/RHEL 安装镜像。它可以替代不需要客户端认证的匿名 FTP。每个下载文件的 BitTorrent 客户端都提供上传带宽，从而减轻初始源的负载。通常，BitTorrent 比 FTP 下载更快。

BitTorrent 像其他 P2P 系统一样不需要专用服务器。然而，服务器的功能由跟踪器（tracker）、节点（peers）和种子（seeds）执行。跟踪器允许客户端相互通信。每个客户端——下载 BitTorrent 文件时称为节点，下载整个 BitTorrent 文件后称为种子——都作为文件的额外源。节点和种子统称为集群（swarm）。在 P2P 网络中，集群的成员会上传它已经下载的 BitTorrent 文件部分。种子并没有特别之处；在种子可以从其他节点下载后，可以随时移除。

下载 BitTorrent 文件的第一步是定位或获取种子文件，即扩展名为 `.torrent` 的文件。种子包含有关要下载文件的某些信息（元数据），例如其大小和跟踪器的位置。你可以通过其 URI 获取种子，也可以通过电子邮件附件或其他方式获取。BitTorrent 客户端随后连接到跟踪器，学习集群中其他成员的位置以下载 BitTorrent 文件。

当你下载了种子（本地系统有了种子），良好的做法是允许本地 BitTorrent 客户端继续运行，这样节点（尚未下载完整 BitTorrent 文件的客户端）就可以上传至少和你所下载的内容。

# 使用 BitTorrent

`bittorrent` 工具是一个文本化的 BitTorrent 客户端，提供了一个伪图形界面。当你有一个 torrent（种子文件）时，输入类似下面的命令——将示例中的 Fedora torrent 替换为你想要下载的 torrent 名字：

```
$ bittorrent-curses Fedora-15-i386-DVD.torrent
```

一个 torrent 可以下载一个或多个文件；torrent 指定了下载文件的文件名，对于包含多个文件的 torrent，还会指定一个用于存放文件的目录。上述命令中的 torrent 将 BitTorrent 文件保存在工作目录下的 Fedora-15-i386-DVD 目录中。

下面的示例显示了 `bittorrent-curses` 的运行情况。根据网络连接速度和种子数量，下载一个大型 BitTorrent 文件可能需要几小时到几天时间不等。

| file: Fedora-15-i386-DVD |
| :--- |
| size: 3,634,920 (3 GiB) |
| dest: /home/sam/Fedora-15-i386-DVD |
| progress: #### |
| status: finishing in 05:57:25 (7.7%) |
| dl speed: 874.2 KB/s |
| ul speed: 0.0 KB/s |
| sharing: 0.000 (0.0 MB up / 25.1 MB down) |
| seeds: 17 seen now, plus 0 distributed copies (1.99%, 2.6%, 3.0%) |
| peers: 2 seen now |

你可以通过按下 `q` 或 `CONTROL-C` 来终止下载。当你再次将该 torrent 下载到相同位置时，下载将自动从上次的地方继续。

请确保你有足够的空间下载 torrent

注意 某些 torrent 是巨大的。请确保你正在操作的分区有足够的空间存放你正在下载的 BitTorrent 文件。

输入命令 `bittorrent-curses l` 查看选项列表（没有对应的帮助页）。最有用的选项之一是 `--max_upload_rate`，它限制了你在从本地系统下载 torrent 时可以使用的带宽（上行带宽），单位为千字节/秒。默认值为 20。后面的 0 (0) 表示对你可以使用的集群带宽没有限制。以下命令防止 BitTorrent 使用超过每秒 100 千字节的上行带宽：

```
