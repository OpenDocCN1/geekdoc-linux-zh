
- **注意**：有关关于 BitTorrent 的更多信息，请阅读官方 BT 主页 `http://bitconjur.org/BitTorrent/`、Wikipedia 上的 BT 文章 `http://en.wikipedia.org/wiki/BitTorrent`，或 Brian 的 BitTorrent 常见问题解答与指南 `www.desnent.net/btfaq/`。

通过下载最新版本的 Knoppix 来尝试 BitTorrent。使用你的网络浏览器访问 `http://torrent.unix.au-kl.de`（BitTorrent 追踪器），并找到你语言的 Knoppix 最新版本（英语选 EN，德国选 DE）。点击你想保存的 Knoppix 旁边的 DL（下载），将 torrent 文件（高达 55KB）保存到你的桌面。现在……发生了什么？要查找其他文件，请使用 Google。你可以找到音乐（尤其是“带”的东西）、软件、电影以及更多。

- **提示**：记住，Knoppix 默认不包含任何文件共享应用，包括 BitTorrent。要对你下载的 torrent 文件进行任何操作，你需要安装 BT。幸运的是，你可以使用 APT（第 1 章讨论过）Knoppix 持久磁盘镜像，这样你重启 Knoppix 就可以继续使用该软件。不同的 BT 软件包由 BT 的发明者 Bram Cohen 提供。它们很好，还有一个名为 BT 的客户端 ![](img/2fb32174ccf4cfbddb3c8b1d8e3e3b4c)

# 54 第一部分 — 导航神奇的 Knoppix 工具箱

BitTorrent 功能齐全，所以用它代替。要这样做，在命令行输入：

```
# apt-get update && apt-get install btorrent
```

一旦 BitTorrent 打开，它会将你带到菜单并选择 Internet → BitTorrent。一个对话框要求你选择下载的 torrent 文件——它应该在你的桌面上，然后点击 OK。你被要求在何处保存它——Knoppix 镜像大约 700MB，除非你至少有 1GB 内存。相反，你应该挂载开启写入的硬盘分区（右键点击桌面上的分区，选择属性，选择 Device 选项卡，勾选 Read Only），然后点击图标来存储下载。一旦你选择了硬盘上的目录，点击 OK，BitTorrent 就会开始运行，下载并上传——Knoppix ISO。图 2-3 显示了程序运行状态（主页连接）。

![](img/2fb32174ccf4cfbddb3c8b1d8e3e3b4c)

图 2-3：BitTorrent 下载 Knoppix

屏幕显示已下载 31MB，速度为 196 Kbps，这非常棒。注意，几乎 1MB 的相同 ISO 已共享，只要 BT 窗口开着，这个数字就会增加（这就是为什么下载完成后保持 BT 窗口被认为是良好的做法，这样其他人也可以继续受益）。

点击窗口右上角的 Details 和 Advanced 链接获取更多关于你的下载的信息。玩玩那些链接，以及 Preferences。你对 BitTorrent 了解越多，就越能有效地使用这个强大的软件。估计 BT 承担了互联网上 35% 的所有流量——凭借其强大的功能，这种软件以及使用它的人都有非常光明的未来。

# 第 2 章 — 最大化 Knoppix 工具

如果你想安装并使用原始 BT 客户端，使用 `apt-get install btorrent-gui`。另一个优秀的 BT 客户端是 Azure，你可以通过 `apt-get install azure` 下载并安装。

## 使用 Mozilla Firefox 浏览

Knoppix 曾经包含完整的 Mozilla 套件（网络浏览器、电子邮件程序和网页编辑器），但在 3.8 版本中放弃了该套件，转而包含了 Firefox，它只是网络浏览器。这是一个伟大的举措。Firefox 拥有扩展和其他惊喜，而且它是一个更快、更流畅的程序。

如果你正在阅读这些，你可能以前用过 Firefox，并且可能知道如何使用网络浏览器。我在这里不会进行网页浏览 101；相反，让我们看看用 Firefox 可以做的三件非常酷的事。

## 改进你的主页

当我以前启动 Firefox 时，我发现每次都会打开三个标签：Gmail、Bloglines 和 Open Source Weblog。我终于意识到我所做的是低效的。于是我进入 Edit -> Preferences，选择 General，并在 Home Page 处了以下内容，完成后点击 OK：

`gmail.google.com | www.bloglines.com/myblogs | opens.weblogsinc.com`

现在我打开 Firefox，它会自动在标签页打开这三个网站供我查看。如果我点击 Home 按钮，这些网站就会出现。你自己尝试。确定你想要反复访问的网站，并将 URL 输入到 Home Page 框中，用大多数键盘上 Enter 键上面的管道符号 (`|`) 分隔。将你的主页改为关键页面让事情变得更高效实用，因为这些这些是你完成大部分工作所需的网站。

## 安装扩展

Firefox 最酷的事情之一是数百个免费扩展，它们以无限方式扩展浏览器。你可以通过选择 Tools -> Extensions 并点击 Get More 来安装新扩展，这会打开一个新的 Firefox 窗口指向 `https://addons.mozilla.org/extensions/`。从那里，找到你想要的扩展并点击 Install Now。下载安装后，重启 Firefox 以加载扩展。

Mozilla Update 网站拥有每一个扩展——你可以在那里找到很多很棒，其他网站也有必不可少的扩展。你只需要意识到你不能从任何旧网站安装 Firefox。为了安全起见，Firefox 启动时带有一个可以从中安装软件的站点白名单；当你尝试从不在白名单的站点安装扩展时，Firefox 在窗口顶部打开一个警告，警告该站点已被阻止。将其添加到白名单，点击警告栏右侧的 Edit Options 按钮，当 Allowed Sites 窗口打开时，点击 Allow 然后 OK。再次点击链接安装扩展，这次 Firefox 就不再抱怨了。

## 推荐扩展

我会在我的网站（`http://granneman.com/go/extensions/`）上维护一份已安装的 Firefox 扩展更新列表，如果你想看看我目前正在使用哪些扩展，可以去看看。目前，我推荐以下扩展是必不可少的：

- Adblock：在 Mozilla Update 的“杂项”（Miscellaneous）部分查找此扩展。被网站上的广告困扰了吗？只需右键点击广告，选择“Adblock Image”，就可以和那个烦人的广告说拜拜。你还可以使用正则表达式来阻止特定域的所有广告，或匹配特定模式的广告。你可以导入其他人创建的 Adblock 列表；在 Google 上搜索“adblock import filter list”并尝试你找到的列表。
- Jybe：`http://jybe.com/download/register.aspx`。Jybe 让你以及其他安装了 Jybe 的人（适用于 Windows、Linux、Mac OS 或 Windows 的 IE）协作查看网页，并对你们所看到的内容进行聊天。这对于演示、工作会议、故障排除或远程支持非常完美。
- miniT：在 Mozilla Update 的“标签页浏览”（Tabbed Browsing）部分查找此扩展。有了此扩展，你可以拖动标签页以你喜欢的任何顺序重新排列它们。当你拖动标签页时，会出现一个小箭头，清晰地显示你的标签页将去到哪里。
- SessionSaver：在 Mozilla Update 的“标签页浏览”部分查找此扩展。如果你曾经遭遇过 Firefox 崩溃导致标签页中所有的网站都丢失，那么你需要 SessionSaver。加载这个扩展，然后就可以不用管它了。Firefox 崩溃了？重启 Firefox，一切都会恢复：标签页、历史记录、Cookie，所有内容。在打开系列标签页的情况下关闭了 Firefox？重启 Firefox，它们就会再次出现。

当然，还有更多扩展——你可以在我的网站上查看完整列表，并在 Mozilla Update 及其他地方逛逛。Firefox 扩展领域正在发生惊人的创新，你一定能找到精彩的东西。

## 聚焦你的搜索

Firefox 内置了许多实用的搜索工具，既有显而易见的（右上角的搜索框），也有不显而易见的（按 `Ctrl+F` 打开窗口底部的搜索栏，或高亮一个单词或短语并右键点击以使用选择的内容搜索网络）。只需稍微努力，你就能优化 Firefox，变成一台精悍、强大的机器。
