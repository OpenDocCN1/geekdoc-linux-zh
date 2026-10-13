
今天，只有两个模块必须编译到服务器中：`http_core.c`（它提供了服务器的核心功能）和 `mod_so.c`（支持动态共享对象 `DSO` 的模块）。

## 静态模块的优点

有时，将其他模块编译到服务器中可能是理想理想的，这样它们将始终可用，提供略快的响应速度并保证模块的特定版本。

## 静态模块的缺点

静态编译模块的缺点是它占用了空间。另一个缺点是升级模块需要重新编译服务器。

## DSO 的优点

在大多数情况下，可以在不重新编译服务器的情况下添加或删除功能是非常有用的。

## DSO 的缺点

使用 `DSO` 文件时，服务器启动比静态模块慢 20%，因为模块加载器必须找到所有模块、加载它们并解析符号。不过这不是严重的问题，因为启动是一个发生频率的事件。

在某些平台上，位置无关代码的地址比绝对地址更复杂。

## DSO 文件

自 `DSO` 文件出现以来，发行版通常会包含已安装的 Apache 服务器，并将源码安装变为可选。为了解决这个问题，作者们开发了 Apache 扩展（`APXS`）。这是一个安装时创建的 Perl 程序，提供了 Apache 头文件以及平台编译器和链接器标志。

## APXS 使用

以下代码提供了 `APXS` 使用的通用示例，构建可以动态加载到 Apache 的模块：

```
cd /path/to/the_module
$ apxs -c mod_new_module.c
$ apxs -i -a -n foo mod_new_module.so
```

## 浏览器

课程中你需要模拟客户端看到的内容。为了这种模拟，你需要 X Window 系统，以及一些额外的 Web 浏览器，即 Netscape 4.7x、Mozilla 和 Opera 的最新版。除了 X Window 系统外，建议安装这些浏览器。

Web 服务器极可能不需要图形界面或图形增强型浏览器，因为它们往往会占用大量的资源。然而，在整个课程中，它们将用于测试、示例和实验。此外，将建议甚至要求使用图形界面。

> 注意：整个课程中使用 Lynx 作为测试工具。我们推荐此程序而非 Netscape，因为 Netscape 给你的机器增加了资源开销。如果你更倾向于 GUI 工具，请使用 Netscape 代替 Lynx。

下载 Lynx 请访问 `www.slcc.edu/lynx/realease`。有关更多 Lynx 信息请访问：

+   `www.lynx-browser.org`

`www.trill-home.com/lynx.html`

`www.slcc.edu/lynx/release-8-2/lynx2-8-2/lynx_help/`

`lynx_help_main.html`

## 如何获取 Apache

首先，从 `http://httpd.apache.org/dist/` 获取最新的源码。

在发布时，最新的稳定版本是 tar 包 `apache_1.3.19.tar.gz`。当然，发行版提供的 rpm 或 deb 文件也可以使用，但本文未涵盖这些安装方法。我们建议在从源码安装之前，删除任何之前安装的包。例如，使用 `rpm -e | grep apache`（对于基于 Debian 的安装，使用 `apt-get --purge remove apache`）。务必同时删除依赖项。如果不从源码安装，请使用适用于发行版的包进行升级。本章的剩余部分将基于上述源码安装说明。此外，路径和文件位置将根据具体的安装情况进行调整。

从源码安装是任何发行版的一个选项，本文将讨论这种方法。在移除所有之前的安装后，解压 tar 包。不要担心剩余的配置文件；但是，它们可能需要移动，因为源码安装可能不会覆盖某些文件。我们使用 `/usr/src` 作为起点，但后续步骤可以使用任何目录。

## 内容协商概述 (Overview of Content Negotiation)

现代浏览器允许用户对其从 Web 服务器接收的文件指明任何偏好。这包括内容类型（例如，对于压缩文件，优先选择 tar.gz 而非 zip 文件）、首选图像格式以及首选语言。

为了处理这些偏好，每个文档都有其自己的变体（variants）。这些变体之间的差异被称为文档的维度（dimensions）。Apache 可以沿着类型、编码和语言的维度进行协商。

## 类型 (Type)

每个文档都有一种类型。示例类型是 `text/html`。如果 Web 浏览器告诉 Apache 它只能接受特定类型的文档，则 Apache 将仅向浏览器提供该类型的内容。

## 编码 (Encoding)

如果资源被压缩或不是以最终的可用格式存在，则经过了编码。Web 传输目前仅识别 `compress` 和 `gzip` 编码。标准现在还可以处理其他可选的实验性编码。它们的编码前缀为 `x-`，例如用于 Stuffit 存档的 `x-stiff`。

```
AddEncoding x-stiff
```

## 语言 (Language)

这一次，在计算机术语中提到语言时，我们指的是人类的口语和书面语言。文件的语言通过为文件添加扩展名并使用 Apache 的 `AddLanguage` 指令来指定：`AddLanguage MIME extension [extension]`。

使用语言扩展名的文件或文档名称示例如下：

```
index.html.fi
dummy.zip
```

`httpd.conf` 文件中由文件语法指定的类型类型如下所示：

```
AddLanguage en.en
AddLanguage fi.fi
```

这两个指令指定任何文件名末尾带有 `en` 或 `fi` 语言标签的文件将分别归类为英语或芬兰语。它们还显示标签可以位于文件名最后一段之前的一个点位处。

## 选择文档参数 (Choosing Document Parameters)

Web 服务器可以处理多个变量维度，任何给定的客户端也是如此。客户端偏好按质量列出。质量值从 `0.000`（从不显示给定维度）到 `1.000`（最受喜的维度）。

例如，浏览器可能会在头文件中发送以下内容：

```
Accept-Language: en; q=1.0, no; q=0.7
```

这意味着浏览器首先接受英语，其次是挪威语。

## 多视图 (MultiViews)

服务器还可以对多个变体设置质量值。当它必须在多个对客户端同样接受的变体之间做出决定时，服务器将使用它自己的质量偏好。

`MultiViews` 指令 Apache 寻找与客户端偏好最匹配的文档。例如，客户端请求 `http://www.linux.org/index` 但没有文件完全匹配该请求，Apache 会扫描相关目录中 `index` 的变体。Apache 会找到所有名称相似的文件，然后检查客户端的内容偏好（类型、编码和语言）以找到合适的匹配项。

> 注意：扫描会大幅增加磁盘 I/O 活动，减慢 Web 服务器。

由于 `MultiViews` 固有的高 I/O 带宽，当指定 `Options All` 时，MultiViews 是关闭的。要开启 MultiViews，必须针对给定范围指定：

```
Options +MultiViews
```

这会将 MultiViews 添加到现有选项中。有关内容协商的更多信息，请访问以下两个网站：

`http://httpd.apache.org/docs/content-negotiation.html`

`http://httpd.apache.org/docs/mod/mod_negotiation.html`

## 浏览器与 HTTP (Browsers and HTTP)

在整个教程中都会提到客户端和代理（agents）的使用，通常避免提到 Web 浏览器。这是因为有多种方法使用 HTTP 连接到 Web 站点。事实上，在 Web 浏览器中执行的任何操作都可以通过命令行完成。

访问“I sit in Siberia”获取更多关于如何结合 CLI 和 HTTP 访问 Web 点的信息（`http://www.pfuca.com/products/products.html`），或者从 Telnet 窗口输入以下内容：

## 第一章 (Chapter 1)

按下回车键，然后输入：

```
GET /products/products.html HTTP/1.0
```

或者，也可以输入以下内容：

```
GET /products/products.html HTTP/1.1
Host: studi.twien.ac.at
```

然后按两次回车并等待输出，输出将类似于所示：

```
Bash$ wget yahoo.com
--15:29:43-- http://yahoo.com:80/
    => 'index.html'
15:29:44 (143.9 KB/s) - 100% saved in 1.0s
```

## 样式表 (Style Sheets)

Web 开发人员使用样式表来控制网站的各个方面（如字体、背景颜色或表格属性）。

尽管从 1997 年起就有了标准，但样式表仍然很稀有。由于多个版本的浏览器支持程度不同，专门的开发人员使用变通方法（workarounds）让每个浏览器以类似的方式显示内容。
