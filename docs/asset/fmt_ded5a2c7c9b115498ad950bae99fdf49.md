
网页是使用 HTML，即超文本标记语言，或更新的扩展版本 XML，即扩展标记语言 创建的。它们是标准通用标记语言 SGML 的子集。创建 HTML 或 XML 文档只是在文本文件中插入 HTML 或 XML 标签。在这方面，创建网页就像使用基于标签的文字处理器一样简单。您使用 HTML 标签来格式化文本以显示为网页。XML 标签可以包含有关特定连接的更详细信息，例如对象数据或事务特征。网页本身是一个文本文件，您可以使用任何文本编辑器创建，例如 `vi`。如果您熟悉 Unix 系统上的基于标签的文字处理，您会发现它在概念上与 `nroff` 相似。一些 HTML 标签表示标题、列表和段落，以及指向参考网络资源的链接。

您可以不手动输入 HTML 或 XML 代码，而是使用网页编辑器。网页编辑器提供图形界面来构建网页。特殊的网页创建程序可以轻松帮助您创建复杂的网页，而无需明确输入任何 HTML 标签。请记住，无论您使用什么工具创建网页，网页本身都将是 HTML 文档。

> 注意 K 桌面和 GNOME 的许多标准编辑器都包含网页构建功能。许多编辑器使您能够插入链接或格式化标题。例如，`KEdit` 程序支持基本的基于文本的网页组件。您可以添加标题、链接或线条，但不能添加图形。

## Java for Linux: Blackdown

要开发 Java 应用程序、使用 Java 工具以及运行许多 Java 产品，您必须在系统上安装 Java 2 软件开发工具包（SDK）和 Java 2 运行时环境（JRE）。两者合在一起构成了 Java 2 平台标准版（J2SE）。Sun 目前支持并分发这些产品的 Linux 版本。您可以从 Sun 的 `java.sun.com/j2se` 下载它们并安装到您的系统上。您甚至可以为 Red Hat 选择 RPM 包版本以便轻松安装。J2SE 的当前版本被称为 Java 版本 1.4。较早的 1.2 版本无法在 Red Hat 7.0 上运行，尽管 1.3 版本可在 7.1 及更高版本上运行。

尽管 Sun 支持 Java 的 Linux 版本，但更全面、更有效的 Java Linux移植可以从 Blackdown 项目 `www.blackdown.org` 获得。Blackdown 项目已移植了 J2SE，包括 SDK 和 JRE 的 1.4 版本。他们还移植了以前的 Java 版本，包括 1.1、1.2 和 1.3。更多信息和文档也可在该 Blackdown 网站上获得。SDK 和 JRE 1.4 通常以压缩归档的形式提供，`.tar.bz2`。您使用 `bunzip2` 命令解压缩文件，并使用 `tar xvf` 命令提取它。提取应在 `/usr/local` 文件中进行。按照 `INSTALL` 文件中的说明安装软件。

目前有大量额外的基于 Java 的产品和工具可用于 Linux。工具包括 Java 3D、Java 媒体框架（JMF）和 Java 高级成像（JAI），均为 Blackdown 项目（见表 14-3）。其中许多产品可直接按 Sun 提供的形式运行。这些包括 HotJava Web 浏览器和 Java Web 服务器。您可以直接从 Sun Java 网站 `java.sun.com` 下载其中几个。

### TABLE 14-3 Blackdown Java Packages and Java Web Applications (continued)

| Application | Description |
| --- | --- |
| Java 2 Software Development Kit (SDK) 1.4 | 一个 Java 开发环境，包含编译器、解释器、调试器等。Java 2 平台的一部分。从 `www.blackdown.org` 下载 Linux 移植版。 |
| Java 2 Runtime Environment 1.4 (J2RE) | 用于运行 Java 小程序的 Java 运行时环境。Java 2 平台的一部分。从 `www.blackdown.org` 下载 Linux 移植版。 |
| Java 2 Platform SE (J2SE) for Linux 1.4 | Java 2 平台标准版，其中包括 Java 2 SDK 和 RE。从 `www.blackdown.org` 下载 Linux 移植版。 |
| Java 3D for Linux | Sun 的 3D 应用程序编程接口，用于 3D Java 程序。从 `www.blackdown.org` 下载 Linux 移植版。 |
| Java Media Framework (JMF) for Linux | 使音频和视频能够添加到 Java 中。从 `www.blackdown.org` 下载 Linux 移植版。 |
| Java Advanced Imaging (JAI) for Linux | Java 高级成像 API。从 `www.blackdown.org` 下载 Linux 移植版。 |
| Java 1.1 Development Kit (JDK) and Java 1.1 Runtime Environment (JRE) | 较旧的 Java 1.1 开发环境，包含编译器、解释器、调试器等。通过 `www.blackdown.org` 下载适用于您发行版的更新的 Linux 移植版。 |
| HotJava browser | Sun 的符合 HTML 3.2 和 JDK 1.1 的 Web 浏览器。从 `java.sun.com` 下载 Linux 版本。 |
| Java Web Server | 一个用 Java 实现的 Web 服务器。可在 Java 网站 `java.sun.com` 上获得。 |
| GNU Java Compiler | GNU 公共许可的 Java 编译器（GJC）用于编译 Java 程序，`gcc.gnu.org/java`。 |

> NOTE 请参阅 `java.sun.com/products` 获取 Java 应用程序的详细列表。

## The Java 2 Software Development Kit: SDK

Java 软件开发工具包（SDK）提供了创建和调试您自己的 Java 小程序的工具，并为 Java 应用程序（如 HotJava 浏览器）提供支持。该工具包包含带有源代码的演示小程序。您可以从 Sun 网站 `java.sun.com` 获得有关 SDK 的详细文档。目前有三个主要版本的 SDK 可用——1.2、1.3、1.4.x——对应于 Java 2 运行时环境（J2RE）的 1.2、1.3 和 1.4 版本。Java SDK 增加了安全性、GUI 支持（使用 JFC，也称为 Swing）以及运行 Java 增强功能（如 Java 3D 和 Java Sound）的能力。

SDK 包括 JDK 中常见的标准功能，用于国际化、签名小程序、JAR 文件格式、AWT（窗口工具包）增强、JavaBeans 组件模型、网络增强、大数数学包、数据库连接（JDBC）、对象序列化以及内部类。Java 应用程序包括 Java 编译器（`javac`）、Java 调试器（`jdb`）和小程序查看器（`appletviewer`）。此外，SDK 还提供 Java 命名和目录接口（JNDI）、集成 Swing、Java 2D、网络和安全增强以及 CORBA。使用 SDK，您可以运行 Blackdown 移植的 Java 3D、Java 高级成像、Java 媒体框架和 Java Sound。这些功能的详细描述可在 SDK 文档中找到。

您创建 Java 小程序的方式与使用标准编程语言创建程序的方式类似。您首先使用文本编辑器创建源代码，并将其保存在扩展名为 `.java` 的文件中。然后您可以使用 `javac` 编译器编译源代码文件，生成 Java 小程序。有许多集成开发环境（IDE）应用程序可用于编写 Java 小程序和应用程序。虽然大多数是商业产品，但其中一些提供免费的共享软件版本。IDE 提供用于构建 Java 小程序的 GUI 界面。您可以通过 Blackdown 网页链接并下载多个 IDE 应用程序。

## FTP 客户端

互联网是一个由遍布全球的计算机组成的网络，你可以通过互联网地址和一组互联网工具访问它。互联网上的许多计算机被配置为服务器，向任何请求信息的人提供信息。这些信息包含在你可以访问和复制的文件中。每个服务器（通常称为站点）都有自己可通过其定位的互联网地址。Linux 提供了一组互联网工具，你可以用来访问互联网上的站点，然后定位并下载其中的信息。这些工具被称为客户端。客户端应用程序（如 FTP 客户端或 Web 客户端）可以与远程系统上运行的相应服务器应用程序通信。FTP 客户端可以与另一个系统上的 FTP 服务器程序通信。服务器允许客户端访问其系统上的某些指定资源，并允许 FTP 客户端传输某些文件。表 14-4 显示了几种流行的 FTP 客户端。
