

## 表 3-2 帮助工具

| 资源 | 描述 |
| :--- | :--- |
| KDE 帮助中心 | KDE 帮助工具；用于访问 KDE 桌面和应用文档、Man 页面以及 info 文档的图形用户界面。 |
| GNOME 帮助浏览器 | GNOME 帮助工具；用于访问 GNOME 桌面和应用文档、Man 页面以及 info 文档的图形用户界面。 |
| `/usr/share/doc` | 应用程序文档的存放位置。 |
| man 命令 | Linux Man 页面；提供关于 Linux 命令的详细信息，包括语法和选项。 |
| info 应用程序 | GNU info 页面，GNU 应用程序的文档。 |
| www.redhat.com | Red Hat 企业版文档、指南、HOWTO 和常见问题解答；位于“支持和文档”下；许多 Red Hat Linux 文档可能非常有帮助。 |
| doc.fedoraproject.org | Fedora 在线文档，安装和桌面指南。 |
| fedorafaq.org | 包含快速帮助主题的官方常见问题解答。 |
| fedorasolved.org | 常见问题的解决方案。 |
| fedoraproject.org | Fedora 项目网站，包含大量文档、FAQ 和帮助资源，以及指向论坛、新闻组和社区网站的链接。 |
| fcp.homelinux.org | Fedora 社区门户；Fedora 论坛、FAQ、问答和新闻。 |

### Man 页面

你也可以访问 Man 页面，它们是通过命令行界面可用的 Linux 命令手册，使用 `man` 命令进行访问。在输入 `man` 后，跟上你想要了解信息的命令。以下示例请求有关 `ls` 命令的信息：

```
$ man ls
```

按空格键可以翻到下一页。按 b 键可以回退一页。当你完成后，按 q 键退出 Man 实用程序并返回命令行。通过按斜杠 (/) 或问号 (?) 键来激活搜索。/ 向前搜索；? 向后搜索。当你按 / 时，屏幕底部会打开一行，然后你输入要搜索的单词。按 ENTER 键激活搜索。你可以通过按 n 键重复相同的搜索。你无需重新输入模式。

> **提示** 你也可以使用 GNOME 或 KDE 帮助系统来显示 Man 和 info 页面。

### Info 页面

GNU 应用程序的在线文档，如 gcc 编译器和 Emacs 编辑器，也以 info 页面的形式存在，可以从 GNOME 和 KDE 帮助中心访问。你还可以通过输入命令 `info` 来访问这些文档。这会打开一个列出不同 GNU 应用程序的特殊屏幕。info 接口有自己的一组命令。你可以通过输入 `info info` 来了解更多关于它的信息。输入 `m` 会在屏幕底部打开一行，你可以在那里输入应用程序的前几个字母。按 ENTER 键会打开该应用程序的 info 文件。

### 网络资源

你可以在 Fedora 和 Red Hat 网站上获取 Fedora 的文档。部分 Red Hat 文档仍然适用于 Fedora。大多数 Linux 应用程序由 Linux 文档项目覆盖。GNOME 和 KDE 网站也包含大量文档，教你如何使用桌面并详细介绍 Linux 应用程序。还可以使用几个专门针对 Fedora 的支持网站。

-   **fedoraforum.org**：提供特定的最终用户支持；你可以查看支持论坛。
-   **www.fedorafaq.org**：列出一些常见问题的快速答案，例如启用 MP3 支持。
-   **fedoranews.org**：提供最新新闻、近期文章合集以及你可以查看的博客资源。
-   **fcp.homelinux.org**：这是 Fedora 社区门户，一个 Fedora 在线支持社区。
-   **fedorasolved.org**：提供常见问题的解决方案。

## 使用 Fedora 软件仓库

Fedora 软件已经变得非常庞大，且更新非常频繁，因此不再适合使用光盘作为主要的分发手段。相反，分发工作是通过在线 Fedora 软件仓库实现的。该仓库包含大量符合 Fedora 标准的软件，将以前版本中使用的 Fedora Core 和 Fedora Extras 合并到一个大型仓库中。

对于 Fedora，你可以通过访问任何支持 Yum（Yellowdog Updater, Modified）的软件仓库来向系统添加软件。许多软件应用程序，特别是多媒体应用，可能存在潜在的许可冲突。可以在第三方仓库中找到此类软件，从而让 Fedora 避免可能的法律问题。你可以使用与 Fedora 赞助软件相同的简单 Yum 命令从第三方仓库获取许多流行的多媒体应用程序，例如视频和数字音乐支持。Fedora 安装的一个令人沮丧的特点是缺乏流行的多媒体和驱动程序支持。使用 Yum，通过几个简单的步骤，你就可以轻松地将此类软件添加到系统中。

这种整体方法标志着一种观念的转变：不再将大多数 Linux 软件视为包含在几张光盘上的东西，而是将光盘视为一个核心，你可以从在线仓库中随心所欲地扩展已安装的软件。大多数软件现在都位于连接互联网的软件仓库中。随着 Yum 集成到 Fedora 系统中，你现在可以将该软件视为当前软件集合中易于安装的扩展。从某种意义上说，依赖光盘介质获取软件已经过时。你可以通过阅读位于 Fedora 文档页面 doc.fedoraproject.org/yum/en/ 的《使用 Yum 管理软件》来了解更多关于 Yum 在 Fedora 中如何使用的信息。

### 使用仓库完成安装

少数仓库提供了你通常需要的许多软件。主要的 Fedora 软件仓库很可能包含你想要的软件。在尝试第三方仓库之前，请始终先检查此仓库。一些专门的应用程序，如供应商提供的图形驱动程序，可以在 rpm.livna.org/fedora 找到。更完整的多媒体支持软件包集合可以在 freshrpms.net 找到。Java 应用程序位于 jpackage.org，尽管其中一些已经包含在 Fedora 仓库中。这些仓库共同组成了你可以用来提供用户期望的桌面系统大部分功能的一组软件站点。所有这些都符合 Yum，并带有针对 Fedora 的 Yum 配置文件。你可以使用 Yum 从这些仓库安装和更新软件。每个仓库都会有自己的 Yum 配置文件。这些站点及其仓库文件如下所示。

| 仓库站点 | 描述 / 配置文件 |
| :--- | :--- |
| download.fedora.redhat.com/pub/fedora/linux/ | Fedora 仓库：符合 Fedora 标准的软件。 `fedora.repo` |
| freshrpms.net | Freshrpms：以多媒体应用为特色的定制 RPM 软件包。 `freshrpms.repo` |
| rpm.livna.org/fedora | Livna：驱动程序、多媒体和其他 RPM 软件包的仓库。 `lvn.livna.repo` |
| jpackage.org | Java 应用程序。 `jpackage.repo` |

要查看有哪些可用软件包，你可以使用 Web 浏览器访问这些站点。Fedora 提供 repodata 目录用于详细列表。Livna 提供简单的目录文件列表，而 Freshrpms 使用详细的 Web 界面。Livna 软件包在其名称中通过术语 lvn 进一步标识。

所有这些站点都支持 Yum，允许你使用简单的 `yum` 命令同时下载和安装软件包以及任何支持库。这使得安装过程非常简便。

要在软件仓库上使用 Yum，必须配置 Yum 以访问它们。这只需要列出站点的 URL、其 Web 地址和目录位置即可。仓库的配置放置在 Linux 系统上 `/etc/yum.repos.d` 目录中的 repo 文件中。在使用 Yum 访问 Livna 和 Freshrpms 之前，你必须添加它们的配置。然而，Livna 和 Freshrpms 都在其网站上提供 RPM 软件包，安装这些软件包会自动设置所需的 Yum 配置文件。对于 Livna，这是 `livna-release` 软件包；对于 Freshrpms，这是 `freshrpms-release`。

要安装软件包，可以使用 Pirut、yumex 或 `yum` 命令。所有这些都会自动使用 repo 文件来检查你启用的仓库。

或者，你可以使用浏览器直接下载软件包。你的 Fedora Web 浏览器可以让你通过一个简单操作同时执行下载和安装。

