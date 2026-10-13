
```
▼
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-10.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-2.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-3.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-4.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-5.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-6.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-7.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-8.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-9.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/new.gif
/usr/share/doc/FAQ/html/AfterStep-FAQ/next.gif
/usr/share/doc/FAQ/html/AfterStep-FAQ/prev.gif
▲
```

![](img/5ced0c78d748bd190e9027e5549a3622_183_0.png)

![](img/5ced0c78d748bd190e9027e5549a3622_183_1.png)

> > FAQ 包的前述示例是一个很好的起点，因为它没有依赖项。使用 RPM 工作时令人沮丧的一大原因是列出的依赖项存在不一致，因此尝试安装一个包时往往首先需要安装半打更新的库和支持包。这可能最令人沮丧！

能够快速轻松地从 Web 安装 RPM 包是使用 Linux 的真正奢侈之一。更新已安装的软件以匹配新下载的 RPM 也同样容易（例如使用 `rpm -Uvh package` 而不是 `-ivh`）。要删除包，请使用 `rpm -e packagename`。最有帮助的 `rpm` 标志总结在表 8.1 中。

##### 表 8.1 rpm 的有用的标志

| Flag | Meaning |
|------|---------|
| -e | 从系统中删除指定的 RPM 包。 |
| -h | 以井号 (#) 在屏幕上显示任何下载的进度。 |
| -i | 安装。（与 -v 一起使用以查看正在进行的操作。） |
| -p | 查询未安装的包。非常有帮助！ |
| -q | 查询 RPM 数据库：-qa 查询所有包，或可以按名称指定包。 |
| -U | 升级自上次安装以来指定的包中发生变化的部分。 |
| -v | 详细——RPM 通常只列出错误，这可能会令人困惑。使用 -v 查看它正在做什么。 |

#### Darwin 中的包管理

Darwin 中没有内置的默认包管理器，虽然 Mac OS X 拥有非常复杂的 Mac 应用安装系统，但它无法从命令行访问，也无助于特别扩展 Unix 部分。

好消息是开源社区已联合起来构建了一个非常复杂的替代包管理系统，名为 `fink`。

![](img/5ced0c78d748bd190e9027e5549a3622_184_0.png)

> > 想知道 fink 是什么意思吗？来自原始开发者：“Fink 是 Finch 的德语名称，一种鸟类。我在为项目寻找名称时，操作系统的名称 Darwin 让我想到查尔斯·达尔文、加拉帕戈斯群岛和进化。我记得在学校学过一篇关于所谓的达尔文雀及其喙的文章，就这样了....”你可以在 http://fink.sourceforge.net/faq/ 的优秀 fink FAQ 中阅读更多内容。

开始使用 fink，你需要下载初始的 fink 分发包，它被打包为标准的 Mac OS X 应用二进制文件。

##### 任务 8.3：安装和使用 fink

使用 fink 在你的 OS X Macintosh 上的第一步是确保已安装 Developer Tools，它包含在你的 Mac OS X 发行版中。如果没有，你可以随时从 Apple 的 http://developer.apple.com/tools/macosxtools.html 下载。

准备就绪后，访问 http://fink.sourceforge.net/ 并点击 Downloads 链接。然后你需要选择 Binary Installer，它的大小略小于 8MB。

下载完成后，点击 .pkg 打开的盒子图标来安装 fink 系统。请记住，如图 8.1 所示，你需要管理员密码才能成功安装。

完成之后，它会快速通过各种屏幕并无错误地完成。还有一个必要的步骤：当你在 OS X 中启动 Terminal 时，确保将 `/sw/bin` 和 `/sw/sbin` 添加到你的 `PATH` 中，以便可以找到命令。事实上，在编辑你的 `.cshrc`（或等效文件）时，你可能还想添加第二个环境变量：`MANPATH="/sw/share/man"`，以确保可以找到 fink 安装的应用的手册页。现在你可以开始了！

##### 图 8.1

管理员密码提示。

![](img/5ced0c78d748bd190e9027e5549a3622_185_0.png)

- 1. fink 应用安装在目录 `/sw/bin` 中，所以让我们从 list 命令开始，看看发行版中包含什么：

```
# fink list | head
```

```
Reading package info...
Information about 251 packages read.
a2ps 4.12-4 Any to PostScript filter.
anacron 2.3-3 A periodic command scheduler
ant 1.4.1-2 Java based build tool.
apache 1.3.20-2 Flexible and extensible web server
app-defaults 20010814-1 Creates an app-defaults directory for fink
i apt 0.5.4-1 Advanced front-end for dpkg
audiofile 0.2.1-2 Audio File Library
autoconf 2.13-3 System for generating configure scripts
```

`fink` 与 RPM 之间一个显著的区别是，`fink` 具有底层网络连接功能，可列出你可能安装的所有包，其中已安装的包在列表左侧用 i 标记（例如 `apt` 包）。

这意味着如果想查看已安装的包，只需将 `fink` 的输出传递给 `grep`：

```
# fink list | grep '^i '
```

```
i apt 0.5.4-1 Advanced front-end for dpkg
i base-files 1.3-1 Directory infrastructure
i bzip2 1.0.4-4 Block-sorting file compressor
i debianutils 1.15-4 Misc. utilities specific to Debian (and Fink)
i dpkg 1.9.17-2 The Debian package manager
i fink 0.9.4-1 The Fink package manager
i gettext 0.10.40-1 Message Localization support
i gzip 1.2.4a-5 The gzip file compressor
i libiconv 1.7-3 Character set conversion library
i ncurses 5.2-5 Full-screen ascii drawing library
i tar 1.13.19-1 GNU tar - tape archiver
```

状态可能为 (i) 的包已安装，但有更新版本可用。

- 2. 现在我们已安装 fink，可以解决 Darwin 发行版中的几个问题。是时候安装 `bash` 了，这是一种许多 Unix 系统管理员的首选命令 shell。
