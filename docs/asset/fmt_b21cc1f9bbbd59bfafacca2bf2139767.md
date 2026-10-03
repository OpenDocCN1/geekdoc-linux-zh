
# 图 8-5：Epiphany Web 浏览器

## Lynx 和 eLinks：命令行模式浏览器

Lynx 是一种你可以在不使用 X 窗口系统的情况下使用的命令行浏览器。网页将仅以文本形式显示。文本页面可以包含指向互联网资源的链接，但不会显示任何图形、视频或声音。除了显示上的局限性外，Lynx 是一个功能完备的 Web 浏览器。你还可以使用 Lynx 下载文件或访问本地页面。网络上的所有信息仍然可以访问。因为它不需要图形浏览器所需的大量开销，Lynx 的运行速度快得多，可以快速显示网页文本。

另一个与大多数发行版一起附带的实用文本浏览器是 ELinks。ELinks 是一个强大的屏幕浏览器，具有框架、表单和表格支持等功能。它还支持 SSL 安全加密。要启动 ELinks，请在终端窗口输入 `elinks` 命令。

## 创建你自己的网站

要创建你自己的网站，你需要访问 Web 服务器。如果你在安装期间选择 Web 服务器，将安装 Apache Web 服务器。你也可以在远程服务器上租用页面空间——许多 ISP 供应商都提供这项服务，其中一些是免费的。在 Fedora 上，Apache Web 服务器为你的网页设置的目录是 `/var/httpd/html`。其他服务器会为你提供一个主页目录。将你创建的网页放置在该目录中。你可以创建带有自己网页的其他子目录，这些子目录之间可以相互链接。创建网页并不困难。从一个页面到另一个页面的链接引导用户在你的网站中移动。你甚至可以创建指向其他网站网页或资源的链接。网上有很多关于网页创建和管理的优秀教程。

网页是使用 HTML（超文本标记语言）或较新的扩展版本 XML（扩展标记语言，基于 SGML）创建的。创建一个 HTML 或 XML 文档只需在文本文件中插入 HTML 或 XML 标签。在这方面，创建网页就像使用基于标签的文字处理器一样简单。你使用 HTML 标签对文本进行格式化，以作为网页显示。XML 标签可以包含关于特定连接的更详细信息，作为对象数据或事务特征。网页本身是一个文本文件，你可以使用任何编辑器（如 Vi）来创建它。如果你熟悉 Unix 系统上的基于标签的文字处理，你会发现它在概念上与 `stoff` 相似。某些 HTML 标签表示标题、列表和段落，以及指向参考 Web 资源的链接。

与其手动输入 HTML 或 XML 代码，不如使用网页制作工具。这些工具帮助你创建复杂的网页，而无需显式地输入任何 HTML 标签。无论你使用什么工具来创建网页，网页本身都将是一个 HTML 文档。作为 KDE 项目的一部分，KDE Web Dev (www.kdewebdev.org) 提供了几个 Web 开发应用程序。

> **注意**：K Desktop 和 GNOME 的许多标准编辑器都包含网页构建功能。许多编辑器允许你插入链接或格式化标题。

## Linux 版 Java

要开发 Java 应用、使用 Java 工具并运行许多 Java 产品，你必须在系统上安装 Java 2 软件开发包 (SDK) 和 Java 2 运行时环境 (JRE)。它们共同组成 Java 2 平台标准版 (J2SE)。Sun 目前支持并分发这些产品的 Linux 版本。你可以从 Sun 网站 `java.sun.com/j2se` 下载它们并安装到你的系统中。Java 程序包和应用程序列在表 4-8 中。

| 应用程序 | 描述 |
|---|---|
| Iced Tea (OpenJDK) | 一个开源 Java 开发环境，带有编译器、解释器、调试器等，openjdk.java.net。作为 Fedora 8 发行版的一部分包含。 |
| Java 2 软件开发包 (SDK) | 一个带有编译器、解释器、调试器等的开发环境，java.sun.com/j2se。Java 2 平台的一部分。可以从 JPackage 或直接从 Sun 下载 Linux 端口。 |
| Java 2 运行时环境 1.4 (J2RE) | 用于运行 Java Applet 的 Java 运行时环境。从 www.java.com 或 jpackage.org 下载 Linux 端口。 |
| Java 类环境 | 类 Java 的自由开源环境，由 GNU Java 运行时 (libgcj)、Eclipse Java 编译器 (ecj) 以及支持的封装和链接 (java-gcj-compat) 组成。包含在 Fedora 中。 |
| Java 系统 Web 服务器 | 用 Java 实现的 Web 服务器。可以在 Java 网站 java.sun.com 获取（商用）。 |
| GNU Java 编译器 | 符合 GNU 公共许可协议的 Java 编译器 (GJC)，用于编译 Java 程序，gcc.gnu.org/java。包含在 Fedora 中，libgcj。 |
| Jakarta 项目 | Apache 软件基金会的开源 Java 应用程序项目，jakarta.apache.org。 |

**表 4-8：Java 程序包和 Java Web 应用程序**

## jpackage, Sun 和 Java 类 (java-gcj-compat)

Fedora 包含了许多免费的 Java 应用程序和支持，例如 Jakarta。关于 Java 的信息请访问 `fedoraproject.org/wiki/JavaFAQ`。

你可以从 JPackage 或直接从 Sun 下载 Linux 端口。

其设计的 Java 包不会产生冲突，并且与指定的 Linux 版本兼容。通过 JPackage 的 Java 版本，你可以安全地安装和卸载许多应用程序和支持工具。使用 JPackage 的最佳方法是下载你的 Yum 仓库配置文件。请确保选择适用于 Fedora 发行版的版本（可用）。遗憾的是，由于许可限制，JPackage 必须对主 JRE 以及 SDK 收费。这些包含在你的 Java 包中。

或者，你可以直接从 Sun 免费下载并安装 JRE 或 JDK。如果你从 JPackage 安装了备用 Java 环境，可以使用 `alternatives` 命令来切换它们。

## 安装 Java 运行时环境：JRE

许多网站将运行需要已安装原始 Java 运行时环境 (JRE) 的应用程序。Fedora 并不自带 Sun Java 运行时环境。但 Java 类环境已经支持 Office.org 和 Eclipse 等兼容应用程序。对于 Sun 的 Java，你需要在你的 Linux 系统上下载并安装 JRE。你可以从 Sun Java 网站 (`www.java.com`) 或 JPackage 获取副本。Java 程序包以自解压压缩包 .bin 的形式提供。这些文件实际上是带有嵌入压缩文件的脚本（有单独的安装说明）。由于文件名冲突，你不应该使用 Sun RPM 包 (.bin.rpm)。相反，你应该下载 RPM 包并将其解压到 `/opt` 目录中。你必须使自解压二进制文件具有可执行权限，使用 `chmod a+x jre-6u3-linux-amd64-rpm.bin` 变为可执行。以下命令将 JRE 文件 `jre-6u3-linux-amd64-rpm.bin` 变为可执行，首先会提示接受许可协议。

```bash
chmod a+x jre-6u3-linux-amd64-rpm.bin
./jre-6u3-linux-amd64-rpm.bin
```

## 为 Mozilla/Firefox 配置 Java 运行时环境

为了允许 Mozilla 或 Firefox 浏览器使用 JRE，你需要创建一个从 Mozilla 插件到 Java 插件库的链接。请确保你已经安装了 JRE。在 `/usr/lib/mozilla/plugins` 目录下，你必须在 JRE 的 `/plugin/i386/ns7/` 子目录下为 `libjavaplugin_oji.so` 库创建一个链接，其中“ns7”表示 Netscape 7。

```bash
# cd /usr/lib/mozilla/plugins
# ln -s /opt/jre.63/plugin/i386/ns7/libjavaplugin_oji.so libjavaplugin_oji.so
```

> **注意**：在 Firefox 和 Mozilla 上，请确保已启用 Java 支持。

## Java 产品与工具

目前有许多基于 Java 的产品和工具适用于 Linux。这些工具包括 Java 3D、Java 媒体框架 (JMF) 和 Java 高级映像 (JAI)。部分由 Sun 公司提供的直接运行在 Web 服务器上的产品。你可以直接从 Sun Java 网站 (`java.sun.com`) 下载其中几个。Apache 软件基金会的 Jakarta 项目 (`jakarta.apache.org`) 提供了开源工具和应用程序，包括库、服务器应用程序和引擎。Jakarta 以及其他软件包被包含在 Fedora 中。这些源自 package.org 的 JPackage 项目，该项目还包含一些 Fedora 中不具备的包，你可以下载并安装。JPackage 是一个 Fedora Yum 支持的仓库。

## Java 开发包与 Iced Tea

Sun 现在提供了一个名为 Iced Tea 的开源开发环境，旨在开发完全开源的 Java 应用 (OpenJDK)。Iced Tea 包含在 Fedora 8 中。OpenJDK 为完全开源的 Java 应用提供了 Java 开发平台。

此外，你也可以下载并安装 Java 软件开发包 (SDK)。该包提供了创建和调试自定义 Java Applet 的工具，并为 Java 应用提供支持。你可以从 Sun 网站 (`java.sun.com`) 获取有关 SDK 的详细文档。目前 SDK 有四个主要发行版本——1.2、1.3、1.4.x 和 1.5（也称为第 5 版），以及对应 Java 2 运行时环境 (J2RE) 的 1.2、1.3、1.4 版本和企业版。SDK 特性的详细描述可以在 SDK 文档 `java.sun.com/docs` 中找到。

## 第 8 章：Web、FTP、Java 和网络信息

你可以像使用标准编程语言创建程序一样创建 Java Applet。你首先使用文本编辑器创建源代码，并将其保存为 `.java` 扩展的文件。然后，你可以使用 `javac` 编译器编译源文件，生成 Java Applet。有许多集成开发环境 (IDE) 应用程序用于编写 Java Applet 和应用程序。尽管大多数是商业软件，但某些提供免费版本。IDE 提供了一个用于构建 Java Applet 的 GUI 界面。包含在 Fedora 中的 Eclipse 可以作为 Java Applet 的开发平台运行。

## FTP 客户端

通过 FTP 客户端，你可以连接到相应的 FTP 站点并从中下载文件。FTP 客户端通常用于从作为软件仓库的公共 FTP 站点下载软件。大多数 Linux 软件应用程序都可以从此类站点下载到你的 Linux 系统。这些站点提供匿名登录功能，允许任何用户访问其文件。`ftp.redhat.com` 这样的发行站点就是此类 FTP 站点示例，它拥有大量的打包 Linux 应用，你可以使用 FTP 客户端下载并安装到你的系统中。基础 FTP 客户端功能已集成到 Konqueror (KDE) 和 Nautilus 文件管理器中。你可以使用文件管理器访问 FTP 站点，并将文件拖到本地目录进行下载。有效的 FTP 客户端现在也集成到大多数 Web 浏览器中，使 Web 浏览器成为主要的下载工具。特别是 Firefox 具有强大的 FTP 下载能力。

| FTP 客户端 | 说明 |
|---|---|
| Firefox | Mozilla Web 和 FTP 浏览器 |
| Konqueror | K 桌面文件管理器 |
| Nautilus | GNOME 文件管理器 |
| gFTP | GNOME FTP 客户端 |
| ftp | 命令行 FTP 客户端 |
| lftp | 支持多连接的命令行 FTP 客户端 |
| NcFTP | 基于屏幕的 FTP 客户端 |
| curl | 网络传输客户端 (FTP 和 HTTP) |

**表 8-5：Linux FTP 客户端**

尽管文件管理器和 Web 浏览器提供了访问公共（匿名登录）站点的有效方法，但要访问私有站点，你可能需要独立的 FTP 客户端，如 curl、wget、gFTP 或 ftp。这些客户端允许你输入用户名和密码，以访问私有 FTP 站点。独立客户端对于从公共 FTP 站点下载大文件也非常有用，特别是那些支持有限或不支持 Web 显示的站点。流行的 Linux FTP 客户端如表 8-5 所示。

## 网络文件传输：FTP

通过文件传输协议 (FTP) 客户端，你可以直接从一个站点传输极大的文件。FTP 可以同时处理文本和二进制文件。它是 TCP/IP 协议之一，运行在连接到互联网的网络系统上。FTP 对网络上连接到你的另一个系统上的账户进行远程登录。一旦登录该系统，你就可以从中传输文件。要进行登录，你需要知道远程系统中账户的登录名和密码。例如，如果你在互联网上的两个不同站点都有账户，可以使用 FTP 将文件从一个传输到另一个。互联网上的许多站点允许通过匿名登录公共访问。

## 第二部分：应用程序

（此处原文重复了 FTP 客户端介绍内容，已按逻辑省略）

## 基于浏览器的 FTP

（此处原文重复了网络文件传输 FTP 介绍内容，已按逻辑省略）

## K 桌面文件管理器：Konqueror

（此处原文重复了 FTP 客户端介绍内容，已按逻辑省略）

## GNOME 桌面 FTP：Nautilus

（此处原文重复了 FTP 客户端介绍内容，已按逻辑省略）
