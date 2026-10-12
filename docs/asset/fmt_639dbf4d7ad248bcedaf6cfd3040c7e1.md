
# LINUX 视图 LINKACE/FLINACUS

新手们大家好。我使用了 `Ubuntu 22.04` 作为基础。若要在你的机器上设置 `Docker` 及其相关组件，请按照列表 1 所示进行操作。如果你使用的是不同的 `Ubuntu` 版本，请将第 5 行中的 `james` 替换为你正在使用的 `Ubuntu` 版本。

你可以在 `https://github.com/docker/releases` 检查版本 `2.13.0`（第 12 行）是否为最新版本。第 14 行和第 15 行的内容可以让你确定当前安装的版本。

进一步的步骤在 `LinkAce` 文档（16）中有描述。首先，你需要在 `LinkAce` 的基础版和高级版之间进行选择。如果你只想在本地使用 `LinkAce`，那么在容器中交付应用和数据库的基础版就足够了。对于网络访问，你需要在独立的容器中安装 `Web`、服务器和数据库。另外，这增强了使用反向代理通过 `HTTPS` 进行安全保护，以便应用程序可以从外部访问。

在安装方面，两种变体是相同的，只是你需要下载不同的 `Compose` 文件。我在这里将使用基础方法。在扩展变体中使用反向代理或负载均衡器的步骤可以在文档（16）中找到。

首先，将 `linkace-docker-simple.zip` 或 `linkace-docker-advanced.zip` 下载到家目录下之前创建的文件夹中并解压 `zip` 包。该文件包含了多种变体的 `docker-compose.yml` 文件以及各种问题，此外还有许可证和 `README`。扩展变体还包含了 `nginx.conf` 和 `nginx.conf1` 文件。

## 设置密码

在继续之前，你需要更改 `.env` 文件中的 `POSTGRES_PASSWORD` 和 `REDIS_PASSWORD`。如果你使用的是 `MySQL` 以外的数据库，请更改名称以匹配。保存后，使用 `docker-compose up -d` 运行最终设置。之后可能需要几分钟时间，所有调用将按照 `compose` 文件中的规范运行。完成后，你将看到一个启动 `LinkAce` `Web` 服务器的 `URL`。

针对 `LinkAce` 的一些需要进一步采取的步骤（部分可选）总结在文档的 `Setup Tutorial` [17] 章节中。我将查看其中最重要的部分。首先，切换到右上角的书签。你可以将刚刚拖入的书签保存到你的书签栏中。就在下方，你将拥有创建 `API` 令牌的功能。

![](img/89cd889ee36b4c92cc520e4f74809806_77_0.png)

| 更新 | | |
| --- | --- | --- |
| 当前版本: `v1.11.0` | | |
| 发现更新：版本 `v1.11.1` 可用。 | 需要 `cron` 来运行 `cron` 服务以检查死链接或运行中的备份。 | `WPv4xm6n22Aq4vF1qKutsXLgtw` 生成令牌 |
| 注意：如果你已经有一个 `cron` 令牌，生成新令牌将破坏现有的 `cron` 令牌！ | 将你的 `cron` 指向以下 `URL`：`https://demo.linkace.com/cron/WPv4xm6n22Aq4vF1qKutsXLgtw` | |
| 系统设置 | 启用访客访问 | |
| 页面标题 | | |
| `LinkAce` `Demo` | 是 | 如果启用，访客将看到所有非私有的链接。 |
| 自定义页头内容 | | |

**图 11：** 除其他外，你可以根据需求生成令牌；你需要它让时间控制的 `cron` 任务能够正常工作。

使用密码和电子邮件地址创建用户。如果你想通过双重认证增加更多安全性，可以在设置文档（18）中找到相关说明。

你可以为 `Web` 界面选择语言、时区、隐私等偏好。在页面底部，决定你倾向于浅色模式还是深色模式，以及你是否想要下载桌面设置。至少要选择你想要分享链接的社交媒体平台（如果有的话）。

除了设置之外，还有系统设置，任何一方都可以加入。要做的第一件事是定期检查你的链接、进行备份，并在 `Wayback Machine` 中进行备份。为 `Linkage` 设置 `cron` 任务的步骤在“`Cron for Linkage`” 框中描述（图 11）。`Linkage` 在网页浏览器中搜索和分类时提供了更多书签管理选项。你可以随心意欲将单个链接从公共改为私有，反之亦然。描述链接将留在 `Linkage` 中，直到你清空它。此外，还有针对公共和私有链接的 `RSS` 馈（19）。可以通过命令行界面 (`CLI`) [20] 用于管理。`Linkage` 的更新也是可用的，正如文档 [21] 所示。

该应用程序的论坛 [22]。无论你选择什么，好的一点是数据不会属于 `Google`、`Mozilla` 或其他提供者。相反，一切都留在你的控制之下。

# Info

- [1] `Firefox Sync`: `https://www.mozilla.org/en/firefox/sync/`

- [2] `floccus`: `https://floccus.org`

- [3] `Linkage`: `https://www.linkage.org`

- [4] `Bookmark for Nextcloud`: `https://github.com/nextcloud/bookmarks`

- [5] `floccus Guide`: `https://flcus.org/guides`

- [6] `floccus FAQ`: `https://floccus.org/faq`

- [7] `Self-hosted Firefox server`: `https://mozilla.services.red`

- [8] `Linkage`: `https://linkage.org`

- [9] `Wayback Machine`: `https://en.wikipedia.org/Wayback_Machine`

- [10] `AWS`: `https://aws.amazon.com`

- [11] `S3`: `https://cloud.com`

- [12] `Linkage demo`: `https://demo.linkace.com`

- [13] `Docker`: `https://hub.docker.com`

- [14] `Docker`: `https://www.docker.com`

- [15] `Docker`: `https://www.docker.org`

- [16] `LinkAce documentation`: `https://docs.linkace.org`

- [17] `Setup Tutorial`: `https://docs.linkace.org/setup`

- [18] `Settings document`: `https://docs.linkace.org/settings`

- [19] `RSS feeds`: `https://linkace.org/rss`

- [20] `CLI`: `https://docs.linkace.org/cli`

- [21] `documentation`: `https://docs.linkace.org`

- [22] `forum`: `https://forum.linkace.org`
