
## 在 Eclipse 中导入项目

![](img/e88880e40d650bfe19d5b6927bd86568_560_0.png)
![](img/e88880e40d650bfe19d5b6927bd86568_560_1.png)

如果你是从 tar 包导入，选择 Archive（归档）并点击 Next（下一步）。图 18.20 所示的对话框显示 tar 包的展开视图，允许你验证你需要的所有内容都在那里并且 Eclipse 可以成功打开它。点击 Finish 开始导入。一旦导入完成，导入的 tar 包的内容就会添加到所选项目中。

将项目导入 Eclipse，验证 `Makefile` 使用 Eclipse 预期的构建目标是一个好主意，你可以通过右键点击 `Makefile` 并选择 Create Make target 来告诉 Eclipse 其他构建目标，但我发现最简单的方法是在 Navigator（导航）视图中双击它的名称，这会在图 18.22 的编辑器中显示 `Makefile`。

![](img/e88880e40d650bfe19d5b6927bd86568_561_0.png)

### 对于 Eclipse 中的标准 make 项目

![](img/e88880e40d650bfe19d5b6927bd86568_562_0.png)
![](img/e88880e40d650bfe19d5b6927bd8658_562_1.png)

### 在 Eclipse 中构建

默认目标是 `pop3check`，你会将其改为 `all` 以简化操作。在按下 ➪Save（保存）保存更改后，你可以通过选择 Build All（全部构建）以标准方式构建项目。胜利！在这种情况下，你新导入的项目正确且成功地构建了，如图 18.23 所示。

### Eclipse 中导入项目的构建

在 Eclipse 中导入现有源项目时，你的情况可能会有所不同，但可以做到这一事实让你能够轻松迁移现有的应用程序开发工作，从而利用它的许多功能并利用像 Eclipse 这样提供的易用 IDE。

## 关于 Eclipse 的更多信息

强大的、功能齐全 IDE，这意味着前两个节中的示例仅触及其功能和额外功能的冰山。关于 Eclipse 的更多详细信息，请参阅许多关于使用 Eclipse 的书籍之一，或访问网络上的以下链接：

* <http://www.eclipse.org>：Eclipse 母机主页
* <http://www.eclipse.org/documentation/main.html>：eclipse 文档站点
* <http://planeteclipse.org/planet/>：Planet Eclipse，Eclipse 开发者、贡献者、黑客和用户经常出没
* <http://www.eclipseplugincentral.com>：Eclipse Plug-in Central，从那里你可以下载任何免费的 Eclipse 插件

![](img/e88880e40d650bfe19d5b6927bd86568_563_0.png)

该节讨论了源码控制软件，突出了 Subversion SCCS。作为 Eclipse 可用广泛免费插件的示例，以下是两个免费的 Subversion 插件：

* 位于 [www.polarion.org](http://www.polarion.org) 的 Subversive 插件
* 位于 <http://subclipse.tigris.org> 的 Subclipse 插件

这两个插件都为 Eclipse 中使用 Subversion 仓库提供了方便的方法，但它们是这种开源素材如何良好结合的极佳示例。而且你绝对不花钱！

## 源码控制软件

如果你曾经不小心删除了正在工作的文件，在系统崩溃时丢失了整个软件版本，或者在一个合作项目中工作时，有人足够周地覆盖了你所有的新代码，你可能希望早早地开始使用源码控制系统。源码控制系统，俗称为 *SCCS*，是一个管理源码仓库的软件包，跟踪其更改，管理代码的不同版本（通常被称为 *分支*），并提供在任何时间恢复仓库中任何版本的机制。

### 并发版本控制系统 (CVS)

前节对 CVS 的这些评论仅仅是如此，不应被视为事实。CVS 不是一个经过时间检验的稳定的 SCCS。CVS 已经使用并开发多年，通常用于为互联网上的开源软件项目提供访问。我所知的传统上依赖 CVS 的项目正在转向 Subversion，我相信这一趋势将继续，甚至加速。由于基础 Ubuntu 安装中没有安装 CVS 或 Subversion，我强烈建议你安装 Subversion 而不是 CVS。

如果你是 CVS 的狂热粉丝，或者你现在的项目已经在使用 CVS，你可以使用 Synaptic Manager 安装 CVS，然后可以查看以下网站获取有关设置和使用 CVS 存储库的信息：

* [www.faqs.org/docs/ldev/0130091154_198.htm](http://www.faqs.org/docs/ldev/0130091154_198.htm)：Linux 开发 FAQ 中关于 CVS 的章节。
* [www.freeos.com/articles/4608](http://www.freeos.com/articles/4608)：Mahantesh M. Vanturi 编写的一篇关于设置、配置 CVS 以及 CVS 存储库同步副本的精彩（而且很短！）的文章。虽然这篇文章是几年前的了，但并没有太大变化——毕竟我们谈论的是 CVS。
* [www.flexwiki.com/default.aspx/FlexWiki/ConfiguringCVS.html](http://www.flexwiki.com/default.aspx/FlexWiki/ConfiguringCVS.html)：一个非常好的 Wiki，提供了许多关于理解和使用 CVS 的有用信息。

该系统，我已经在许多公司广泛使用过它。然而，我觉得如果你打算在 Ubuntu 系统上从头开始 CCS，不如使用更现代、更强大的 SCCS。

## 安装和使用 Subversion

（<http://subversion.tigris.org/>）是一个相对较但极其流行的源代码管理器 (SCCS)。除了它的强大和丰富的命令集外，Subversion 的流行在很大程度上是因为它基于 WebDAV（Web 分布式授权与版本控制），这种基于 Web 的协议允许你在任何 Web 浏览器中查看和访问 subversion 存储库。这包括从你的 Web 浏览器将文件复制到桌面进行检出（checkout），反之则进行提交（checkin）。你将在接下来的几节中看到，设置 Subversion 存储库并将其集成到系统中是非常简单的，就像 subversion 在桌面或命令行中使用一样易用。

### Subversion

要安装 `subversion` 及其相关包，请从“系统 ➪”菜单启动 Synaptic 软件包管理器，选择“搜索”，在显示的搜索框中输入 `subversion`，确保搜索类型选择为“查找位置（Look in）”，并点击“搜索”。搜索完成后，在新的 subversion 类别下的软件包列表中向下滚动，并选择以下每一项。并非所有项都是强制的，但它们都是建议安装的——我对此列表中每个包的理由如下：

- `libapache2-svn`：（可选）只有当你想要提供一个用户可以通过你的 Web 服务器访问的 Subversion 存储库时，此包才是必要的。选择此项将导致 Apache2 Web 服务器和相关文件安装到你的系统中。我总是觉得通过 Web 访问我的存储库非常方便，可以一次性配置所有内容，而且 Apache2 消耗的额外磁盘空间对我来说总是值得的。不过，你以后可以随时添加。请参阅第 26 节“设置 Web 服务器”获取有关手动安装不同版本 Apache Web 服务器的信息。

- `rapidsvn`、`esvn` 或 `kdesvn`：（可选）Subversion 的图形界面客户端。只有在你想要使用图形客户端时才必要。rapidsvn 客户端非常受欢迎，是一个 GNOME 客户端。esvn 客户端使用 Qt 图形界面，因此在 GNOME 或 KDE 桌面中都没有太大负担。kdesvn 客户端是一个 KDE 客户端，因此要求你的系统中安装 KDE 库，但它是唯一接受命令行参数的 Subversion 客户端。因此，如果你想将图形化 subversion 客户端集成到 Firefox 中处理 `svn:` URLs，kdesvn 客户端会非常好用。请参阅本章稍后标题为“在 Firefox 中处理 `svn:` URLs”的侧边栏获取更多关于此类操作的信息。

- `subversion`：（强制）这是 Subversion 的核心包，提供了在本地系统通过命令行使用 Subversion 所需的所有内容。

- `subversion-helper-scripts`：（可选）这是一组简化与 subversion 存储库操作的脚本。这是一个小但实用的包，非常值得它占用的磁盘空间（小于 200KB）。
