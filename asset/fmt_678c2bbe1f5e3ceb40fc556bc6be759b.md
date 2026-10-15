
## 加密

普通用户帮助执行安全的最常见方法之一是使用加密程序处理他们的电子邮件、USENET 帖子和数据文件。在这些加密程序中最流行的是 PGP（即 Pretty Good Privacy）。然而，PGP 在软件专利方面遇到了一些问题。我们建议你尝试 GNU Privacy Guard (GPG)；正如 GNU 项目发布的所有产品一样（见第 1 章，“为什么选择 Linux，以及为什么选择 Corel Linux？”），它是完全开源且不含专利限制的。GNU Privacy Guard 可以在 http://www.gnupgp.org 找到。

由于出口法，美国和加拿大以外的读者可能无法获得在美国开发的“强加密”软件。虽然我们认为限制使用和分发安全加密软件的法律是适得其反的，但事实这是美国的法律。不要通过撒谎获取加密软件，也不要违反任何法律去获取。如果你从另一个国家订购，请寻找本地的替代方案。

## 延伸阅读

如你所见，安全是一个巨大的课题，随着新技术的出现，许多方面不断演变。与大多数技术话题一样，Web 是获取最新消息以及你所用软件最新版本的最佳资源。我们特别建议你查看这些资源以学习更多安全知识：

- `The Linux Administrator’s Security Guide` 该文档不断修订以跟上变化，正迅速成为 Linux 安全问题的权威资源。在 http://www.securityportal.org/lasg 找到。
- `Linux Security HOWTO` 这个 HOWTO 没有 Security Guide 那么详尽，但它更短且充满了优秀信息。在 http://www.securityportal.org/lasg 找到。

## 第 29 章

## 使用 WordPerfect 8

## 第五部分

## 450 Corel Linux 启动套装：官方指南

WordPerfect 8 是一个强大且强大的文字处理器，免费提供给社区。如果你购买了 Corel Linux 的盒装零售版（标准版或豪华版），CD 中包含了 Corel WordPerfect 8。如果你是从官方网站下载的 Corel Linux，你也可以在那里下载 WordPerfect 8；但是，你必须进行一些预安装工作以确保它正常运行。请参阅“在 Linux 上安装 WordPerfect 8”章节获取更多信息。

由于空间限制，我们无法详细介绍 WordPerfect 8 的许多功能。我们推荐阅读《Word for for Bible》（IDG Books, 1999）以充分利用它。

WordPerfect 在 Linux 上的发布标志着社区的一个真正分水岭。当然，Linux 上还有其他文字处理器，但 Corel 将 WordPerfect 移植到 Linux 平台是第一次让在 Windows 上非常有用的办公应用程序提供了 Linux 版本。这意味着什么？这意味着 Linux 离完全可行的办公桌面解决方案进了一步。如果没有在 Windows 或 Mac 上使用相同的应用程序版本，Linux 将一直处于边缘。Linux 版本的 WordPerfect 8 是我们诚心推荐你尝试的。

为了完全透明，你应该知道我们还合著过《The WordPerfect 2000 for Linux: The Official Guide》——另一本由 Osborne/McGraw-Hill 出版的优秀书籍，而且我们还合著了多本关于 Star Office 的书——这是另一个适用于 Linux 和 Windows 平台的集成办公套件。我们建议你查看这两个套件以及文字套件，并做出自己的决定。我们同时使用 WordPerfect 2000 和 StarOffice 来满足办公需求。

用 WordPerfect 8 可以做什么？反过来的问题是，你需要做什么？你可以处理纯文本、创建表格或分栏、整合图形或声音、绘制新图像或插入复杂的数学方程。你可以使用内置工具检查拼写或语法、将文本转换为超链接，或处理同一个文件的多个版本。我们甚至专门设立了一个单独的章节（第 30 章，“使用 WordPerfect 8 创建网页”）来介绍 WordPerfect 8 附带的 HTML 发布工具。简而言之，你没有丢失任何功能。

## 第 29 章. 使用 WordPerfect 8

451

使用 Linux 版本的 WordPerfect；如果你从未用过 WordPerfect，那么你将会大开惊喜。

### 为 Linux 安装 Corel WordPerfect 8

如果你是在店面柜台购买了盒装版的 Corel Linux，那么在安装 Corel Linux 时，WordPerfect 8 应该已经默认安装好了。（哇——这太简单了，不是吗！）如果你是从 Corel Linux 官网下载的 Corel Linux 和 WordPerfect 8，那么在不进行一些初始工作的情况下，你无法安装 WordPerfect 8 并使其正常运行。

问题在于一组特定的库。Corel Linux 盒装版默认安装的 `xlib6` 软件包在下载版中并没有默认安装。然而，运行 WordPerfect 8 需要 `xlib6`。因此，你需要先安装 `xlib6`。

![](img/b608ba7a04add87643140fbc345d68f8_486_0.png)

以下是 Corel 官方提供的操作步骤：

- 1. 点击“应用程序启动器”(`Application Starter`)图标，并选择“应用程序 | 系统 | Corel 更新”。出现 Corel 更新屏幕。
- 2. 选择“选项”(`Options`) | 设置文件源(`Set File Sources`)。
- 3. 选择“发行站点”(`Distribution Site`)，并取消勾选“自定义路径”(`Custom Path(s)`)。
- 4. 点击确定。
- 5. 当文件管理器屏幕出现时，选择“可用软件”(`Available Software`)选项卡。
- 6. 选择“文件”(`File`) | 更新配置(`Update Profile`)。
- 7. 选择“编辑”(`Edit`) | 查找(`Find`)。
- 8. 在搜索框中输入 `lib6`（图 29-1）并点击确定。更新程序应定位到“`xlib6 3.3.5-1.0.1 shared libraries required by lib5 X clients.`”这一软件包。
- 9. 找到软件包后，点击 `lib6` 前方的 `X`，使其变为双向箭头。
- 10. 选择“文件”(`File`) | 升级/安装软件包(`Upgrade/Install Packages`)。

库将自动安装。

452 Corel Linux OS 启动器：官方指南

![](img/b608ba7a04add87643140fbc345d68f8_487_0.png)

**图 29-1** 使用更新工具安装所需的库

一旦安装好库，你就可以安装 WordPerfect 8。打开 Netscape 或文件管理器，访问 http://linux.corel.com/products/linuxproducts_wp8_download.htm。点击链接“Click Here To Continue With The Download Process”并按照步骤下载软件包。

> 你必须下载几个文件——如果你想使用非美国英语的语言文件，还需要下载可选模块。

当你下载好软件后（我们建议将所有 WordPerfect 文件下载到单独目录中），打开终端窗口，并对每个文件执行以下命令：

```
gunzip <filename>; tar -xvf <filename>
```

这将打开每个文件并为安装做好准备。

完成后，你只需要发出一个启动安装程序的命令即可。在系统提示符处，输入 `/Runme`。

如果你下载了语言模块，现在是安装它们的时候；模块安装的说明可以在 Corel 网站上找到。如果你不需要语言模块，WordPerfect 8 现在已准备好可以使用。

## 处理 WordPerfect 文档

一旦安装了 WordPerfect 8，你就可以开始处理文档了。WordPerfect 拥有相当直观的界面，这意味着你通常不需要太费力就能看出某个按钮的作用。（你也可以将鼠标指针悬停在任何按钮上片刻，以查看弹出标签。）如图 29-2 所示，WordPerfect 文档主屏幕有一个用于处理文档的大区域，并在菜单栏下方的工具栏配置了各种工具。

> 提示

> 如果你不喜欢 WordPerfect 显示选项的方式，请选择“工具 | 设置 | 自定义”，或“工具 | 设置 | 显示”。在“显示设置”中，你可以根据随心意愿地配置各种工具栏和图标。

![](img/b608ba7a04add87643140fbc345d68f8_488_0.png)

图 29-2 WordPerfect 的布局方式易于理解

### 打开 WordPerfect 文档
