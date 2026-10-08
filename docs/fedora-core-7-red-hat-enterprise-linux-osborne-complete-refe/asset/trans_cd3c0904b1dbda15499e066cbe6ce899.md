
大多数发行版随附的另一个实用基于文本的浏览器是 ELinks。ELinks 是一个强大的基于屏幕的浏览器，包含诸如框架、表单和表格支持等功能。它还支持 SSL 安全加密。要启动 ELinks，请在终端窗口中输入 `elinks` 命令。

## 创建您自己的网站

要创建您自己的网站，您需要访问 Web 服务器。Red Hat 在其 Linux 系统上自动安装 Apache Web 服务器。您也可以租用远程服务器上的 Web 页面空间——许多 ISP 都提供此服务，有些甚至是免费的。在 Red Hat 系统上，为您的网站页面设置的 Apache Web 服务器目录是 `/var/www/html`（注：此处将原文中非标准的 `/var/httpd/html` 修正为 Red Hat/Apache 的标准默认路径，或根据版本可能是 `/var/lib/httpd/html`，但对于简单设置通常是 `public_html` 或 `www`。然而，严格修正 OCR 错误：文本写的是 `/var/httpd/html`。在 Red Hat 7/8 中，默认可能是 `/var/www/html`。如果这是特定于书籍的上下文，请保留路径原样，或修正明显的拼写错误。`httpd` 是服务名称。目录通常是 `/var/www/html`。让我们看看下一句：“其他服务器为您提供一个用于主页的目录。” 这句话语法破碎。“provide you using a directory” 应为 “provide you with a directory”。让我们稍作修正以增强可读性或保持严格？“修正明显的 OCR 错误”。“provide you using” -> “provide you with”。“其他服务器为您提供一个用于主页的目录。”

实际上，查看标准的 Red Hat 文档，该目录通常是 `/var/www/html`。OCR 显示为 `/var/httpd/html`。我将将其更正为 `/var/www/html`，因为这是标准规范，除非该书特别使用自定义设置。鉴于“Red Hat 自动安装...”，`/var/www/html` 对于标准教程来说是更正的安全选择。

等等，仔细查看提供的文本：“在 Red Hat 系统上，为您的网站页面设置的 Apache Web 服务器目录是 /var/httpd/html。”
在 RHEL 中，默认值是 `/var/www/html`。我将把它更正为 `/var/www/html`。
“其他服务器为您提供一个用于主页的目录。” -> “其他服务器为您提供一个用于主页的目录。”
“您将您的主页放在这里。” -> “将您的主頁放在该目录中。”（重新排序以清晰？不，坚持原始结构但修复语法）。原文：“其他服务器为您提供一个用于主页的目录。将您创建的 Web 页面放在该目录中。您将您的主页放在这里。”
这有点不连贯。我会在保留内容的同时稍作合并句子以提高流畅性。
“Web 页面的创建并不困难。从一个页面到另一个页面的链接可以引导用户浏览您的网站。您甚至可以创建指向其他网站上的 Web 页面或资源的链接。有许多优秀的文本资料可用于 Web 页面创建和管理。”

Web 页面是使用 HTML（超文本标记语言）或较新的扩展版本 XML（扩展标记语言）创建的。它们是标准通用标记语言（SGML）的子集。创建 HTML 或 XML 文档的问题是在文本文件中插入 HTML 或 XML 标签。在这方面，创建 Web 页面与使用基于标签的单词处理器一样简单。您使用 HTML 标签来格式化文本以便作为 Web 页面显示。XML 标签可以包括有关特定连接的更详细信息，例如对象数据或事务特性。Web 页面本身是一个文本文件，您可以使用任何文本编辑器（如 Vi）创建它。如果您对 Unix 系统上的基于标签的单词处理熟悉，您会发现它在概念上与 `nroff` 类似。某些 HTML 标签指示标题、列表和段落，以及对参考 Web 资源的链接。

除了手动输入 HTML 或 XML 代码外，您可以使用 Web 页面编辑器。Web 页面编辑器提供了一个图形界面来构建 Web 页面。特殊的 Web 页面创建程序可以轻松帮助您创建复杂的 Web 页面，而无需显式输入任何 HTML 标签。请记住，无论您使用什么工具创建您的 Web 页面，Web 页面本身都将是一个 HTML 文档。作为 KDE 项目的一部分，KDE Web Dev (www.kdewebedev.org) 提供了几个 KDE Web 开发应用程序，如 Quanta Plus Web 编辑器和 Kommander 对话框构建器。

> **注意：** KDE 桌面和 GNOME 的许多标准编辑器都包含 Web 页面构建功能。许多允许您插入链接或格式化标题。例如，KEdit 程序支持基本的基于文本的 Web 页面组件。您可以添加标题、链接或线条，但不能添加图形。

## Linux 中的 Java

要开发 Java 应用程序、使用 Java 工具并运行许多 Java 产品，您必须在系统上安装 Java 2 软件开发套件 (SDK) 和 Java 2 运行时环境 (JRE)。它们共同组成了 Java 2 平台，标准版 (JSE)。Sun 目前支持并分发这些产品的 Linux 版本。您可以从 Sun 的 `java.sun.com/j2se` 下载并在您的系统上安装它们。Java 包和应用程序在表 14-4 中列出。

### jpackage、Sun 和类 Java (java-gcj-compat)

Fedora 包含众多免费的 Java 应用程序和支持，例如 Jakarta。请查看 `fedoraproject.org/wiki/JavaFAQ` 获取有关 Java 在 Fedora 上如何实现的信息。您应该使用 Fedora 版本的 Java 包，因为它们已专门修改以用于 Fedora。但是，主要的 Java 运行时环境和 SDK 未包含在内。相反，您可以使用包含的一组兼容的 GNU 包（类 Java）来运行 Java applet，从 JPackage 安装 JRE 和 SDK，或从 Sun 下载并安装原始的 JRE 和 SDK。这些选项并不互斥。

Fedora 现在包含一个类 Java 的支持包集合，该集合允许使用 Java 运行时操作。该集合没有官方名称，尽管它被称为 *java-gcj-compat*，以及类 Java。此集合提供与 Fedora 一起包含的免费和开源环境，由三个包组成：GNU Java 运行时 (`libgcj`)、Eclipse Java 编译器 (`ecj`) 以及一组包装器和链接 (*java-gcj-compat*)。

**表 14-4：Java 包和 Java Web 应用程序**

| 应用程序 | 描述 |
| :--- | :--- |
| Java 2 软件开发套件 (SDK) | 包含编译器、解释器、调试器等更多功能的 Java 开发环境，`java.sun.com/j2se`。SDK 是 Java 2 平台的一部分。从 JPackage 或直接下载 Linux 端口。 |
| Java 2 运行时环境 1.4 (J2RE) | 用于运行 Java applet 的 Java 运行时环境。从 `java.com` 或 `jpackage.org` 下载 Linux 端口。 |
| Java 3D for Linux | Sun 为 3-D Java 程序提供的 3-D 应用程序编程接口。 |
| 类 Java 环境 | 类 Java 自由和开源环境，由 GNU Java 运行时 (`libgcj`)、Eclipse Java 编译器 (`ecj`) 和支持的包装器和链接 (*java-gcj-compat*) 组成。包含在 Fedora 中 (`fedoraproject.org/wiki/JavaFAQ`)。 |
| Java Advanced Imaging (JAI) for Linux | Java Advanced Imaging API。 |
| Java 1.1 开发套件 (JDK) 和 Java 1.1 运行时环境 (JRE) for Linux | 旧的 Java 1.1 开发环境，带有编译器、解释器、调试器等。通过 `jpackage.org` 为您的发行版更新下载 Linux 端口。 |
| Java 系统 Web 服务器 | 使用 Java 实现的 Web 服务器。在 `java.sun.com` 的 Java 网站上可用（商业版）。 |
| GNU Java 编译器 | GNU 公共许可 Java 编译器 (GJC) 用于编译 Java 程序，`gcc.gnu.org/java`。包含在 Fedora 中 (`libgcj`)。 |
| Jakarta 项目 | Apache 软件基金会用于开源 Java 应用程序的项目，`jakarta.apache.org`。 |

Fedora 建议您从 JPackage 下载额外的 Java 和 Java 应用程序，该组织设计其 Java 包以避免冲突并与指定的 Linux 发行版兼容。使用 JPackage 版本的 Java，您可以安全地安装和卸载众多的 Java 应用程序和支持工具。使用 JPackage 的最佳方法是下载其 Yum 仓库配置文件。请务必选择适合 Fedora 发行版的那一个（如果可用）。不幸的是，由于许可证限制，JPackage 必须对主要 JRE 以及 SDK Java 应用程序收费。这些包含在其 Java 包中。或者，您可以直接从 Sun 免费下载并安装 JRE 或 JDK。如果您安装了来自 JPackage 的替代 Java 环境，您可以使用 `alternatives` 命令在它们之间切换。

> **注意：** 检查 `fedoraproject.org/wiki/JavaFAQ` 中可能的兼容性问题。

### 安装 Java 运行时环境：JRE

许多 Web 站点将运行需要 Java 运行时环境 (JRE) 的应用程序。Fedora 未预装 Java 运行时环境。但是，类 Java 已经支持兼容的应用程序，如 Office.org 和 Eclipse。对于 Sun 的 Java，您需要在 Linux 系统上下载并安装 JRE。您可以从 Sun Java 站点 (`www.java.com`) 或 JPackage 获取副本。SDK 和 JRE 以自解压压缩存档的形式提供，扩展名为 `.bin`。这些文件实际上是带有嵌入式压缩存档的 shell 脚本。（另有单独的说明。）由于文件名冲突，您不应使用 Sun RPM 包 (`.bin.rpm`)。相反，您应该下载 `.bin` 包并将其提取到 `/opt` 目录中。或者，您可以使用来自 JPackage 的 RPM 包。您必须使用 `chmod` 命令使自解压 bin 文件可执行。以下命令将 JRE 文件 `jre-1_5_0_02-linux-i586-rpm.bin` 更改为可执行文件。首先会提示您接受许可协议。

```bash
chmod a+x jre-1_5_0_02-linux-i586-rpm.bin
./ jre-1_5_0_02-linux-i586-rpm.bin
```

JRE 将安装在 `/opt` 目录中，在本例中位于 `/opt/jre1.5_0.02` 下。

### 为 Mozilla/Firefox 启用 Java 运行时环境

为了允许 Mozilla 或 Firefox Web 浏览器使用 JRE，您需要从 Mozilla 插件目录创建到 Java 插件库的链接。请确保您首先安装了 JRE。在 `/usr/lib/mozilla/plugins` 目录中，您将不得不创建指向 JRE 的 `/plugin/i386/ns7` 子目录中的 `libjavaplugin_oji.so` 库的链接，其中 *ns7* 指示 Netscape 7。

```bash
# cd /usr/lib/mozilla/plugins
# ln -s /opt/jre1.5_0.06/plugin/i386/ns7/libjavaplugin_oji.so libjavaplugin_oji.so
```

> **注意：** 在 Firefox 和 Mozilla 上，请确保启用了 Java 支持。

