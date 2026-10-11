

![](img/30dc0459712b32ede1a3814d456b41b6_69_0.png)

**由于它支持多点触控，Dizio 非常适合会议中的交互式桌面展示。**

# 物联网

**这个术语描述性并不强，但物联网几乎可以包含任何事物。**

**任何已经或可以连接到互联网或网络的产品，例如现代自动灯光，都可以连接到 Dizio 和 Raspberry Pi。**

- **Dizio 太空漫步**：体验一些预装项目，看看 Dizio 具体能做什么
- **Pizawg 创建**：创建一个自定义应用程序来监控 Raspberry Pi 的温度，然后更进一步
- **浏览器创建**：使用各种可以连接到并通过 Pi 传输的信息，创建一个完整的自定义显示界面

# 07 包文件

首先，使用 `sudo nano package.json` 创建 `package.json` 文件，然后输入以下内容：

```json
{
  "name": "serve-systeminfo",
  "version": "0.0.1",
  "dependencies": {"express": "4.x"}
}
```

![](img/30dc0459712b32ede1a3814d456b41b6_69_1.png)

# 08 应用程序节点

现在，创建一个名为 `app.js` 的文件，并输入以下内容：

```javascript
var express = require('express');
var app = express();
app.use(express.static(__dirname + '/public'));
app.listen(3000, function(){
    console.log('listening on *:3000');
});
```

# 09 启动 node.js

现在你可以通过输入以下命令来启动 node 服务器：

```bash
$ node app.js
```

它会提示正在监听 *:3000。打开一个新的终端，通过 `ssh` 登录，并使用 `mkdir /public` 创建 `/public` 文件夹，以将所有 CPU 数据保存在其中。

![](img/30dc0459712b32ede1a3814d456b41b6_69_2.png)

# 10 CPU 信息

我们将使用 `vcgencmd` 命令从 Raspberry Pi 获取 CPU 信息。我们将编写一个脚本来执行此操作，然后将信息写入 `sysinfo.json`。从 FileSilo 下载 `grabsysinfo.sh` 文件并将其放入 `/usr/local/bin/`。

# 11 创建定时任务

我们将设置每十分钟更新一次温度。如果你愿意，可以设置更快的更新频率，但请自行尝试。使用 `sudo crontab -e` 打开 `crontab`，并在末尾添加以下内容：

```sh
*/10 * * * * /usr/local/bin/grabsysinfo.sh
```

![](img/30dc0459712b32ede1a3814d456b41b6_70_0.png)

# 12 开始创建小部件

是时候开始构建小部件了。首先，在本地机器上创建一个名为 Gauge 的文件夹并进入该目录。现在你需要使用以下命令将第一个名为 info.plist 的文件下载到此目录：

```bash
$ wget x/info.plist
```

![](img/30dc0459712b32ede1a3814d456b41b6_70_1.png)

# 13 索引文件

Dismo 小部件基本上是一个 HTML 文件，将资源打包在一起以创建界面或图形。这里，我们有一个使用 jQuery 的主 HTML 文件，它有助于显示温度。仍在 Gauge 文件夹中，使用以下命令下载它：

```bash
$ wget x/index.html
```

![](img/30dc0459712b32ede1a3814d456b41b6_70_2.png)

# 14 样式指南

现在，我们将为 Dismo 小部件添加 CSS 样式表。通常，这用于美化将成为我们小部件的页面显示。使用以下命令下载它：

```bash
$ wget x/style.css
```

# 15 最终应用

最后一步是创建 application.js 文件，该文件将使用 Ajax 调用 Raspberry Pi 的温度。你可以使用以下命令下载：

```bash
$ wget x/application.js
```

将 IP 地址更改为你 Pi 的地址。
完成后，你可以测试小部件 – 将 Gauge 文件夹压缩为 .zip 文件，然后将 .zip 更改为 .dzm。启动 dizmoSpace 并将 dzm 文件拖入其中以启动它。

# 16 开始编程

利用这些构建模块，你现在可以开始进行更多有趣的物联网事情 – 控制 GPIO 端口，获取更多信息，以及连接其他对象来控制它们。有关你可以做的更多项目详情，请查看 Dismo 网站。

> “利用这些构建模块，你现在可以开始进行更多有趣的物联网事情 – 控制 GPIO 端口，获取更多信息”

**如上所示，我们选择了简单的 CPU 温度仪表盘，但可能性真的是无限的**

这是 TeX 项目的主网站，你可以在那里找到更多有用的信息

![](img/30dc0459712b32ede1a3814d456b41b6_71_0.png)

- 轻松创建自己的目录、图表列表或表格列表
- 以静默模式运行 latexmk Perl 脚本；Latextmk 是一个方便的自动化 LaTeX 文档生成例程，可以节省你的时间

# 使用 LaTeX 写一本书

学习如何使用 LaTeX 及其广泛的包来排版、美化和定制整本书

## 资源

- **LaTeX 项目**
  www.latex-project.org
- **综合 TeX 档案网络**
  www.ctan.org
- **Latextmk**
  http://users.phys.psu.edu/~rcollins/software/latexmk-perl
- **LaTeX 伴侣**
  第二版，Addison Wesley，2004

Donald Knuth 在 20 世纪 70 年代创造了 TeX，作为一种用于排版的计算机语言，当时他想撰写关于计算机算法的书籍，但发现没有现成的排版系统令他满意。其起源与 C 编程语言的故事相呼应，C 语言是为了编写 UNIX 操作系统而创建的 – TeX 有很多低级命令且难以使用，因此 Leslie Lamport 决定让它更容易消化。他编程了许多高级 TeX 命令，这就成了 LaTeX，如今被广泛使用。

许多人希望排版大量的作品或大约 350 页的书籍，但最大的顾虑可能是选择使用 LaTeX 还是 Adobe InDesign。LaTeX 往往证明是最好的选择，因此本教程将介绍整个过程以及可以对 LaTeX 风格的书籍进行的某些修改和添加。

虽然本文假设你已经熟悉 LaTeX，但如果你从未听说过它并想知道它为何如此流行，你应该知道它帮助了许多书籍和论文作者轻松构建他们的作品。

# 01 安装 LaTeX

首先你需要安装 LaTeX。外面有很多包含 LaTeX 名称的软件包，因此运行 `apt-cache search latex` 将返回大量输出。你可以通过简单执行以下命令获得更有用的输出：

```bash
$ apt-cache search latex | grep 'latex'
```

你使用 LaTeX 的旅程将从运行以下命令开始：

```bash
$ sudo apt-get install latex209-base latex209-bin
```

![](img/30dc0459712b32ede1a3814d456b41b6_72_0.png)

# 02 使用 LaTeX

安装基本 LaTeX 软件包后，你应该尝试编译随后的 LaTeX 代码，以确保一切工作正常：

```latex
\documentclass{article}
\title{The LaTeX version of the Hello World program}
\author{Mathias ToukaLos}
\date{January 2015}
\begin{document}
\maketitle
Hello world!
\end{document}
```

你可以使用以下命令编译文档：

```bash
$ latexmk helloworld.tex
```

上一个命令生成一个 DVI 文件，你可以按如下方式将其转换为 PDF 格式：

```bash
$ dvipdf helloworld.dvi
```

如果你查看生成的文件，你可以很容易地理解默认的 LaTeX 样式产生高质量的输出。问题在于，如果每个人都在使用默认样式，所有使用 LaTeX 制作的书籍看起来都将完全相同！

![](img/30dc0459712b32ede1a3814d456b41b6_72_1.png)

# 03 优点和缺点

LaTeX 有其优点。它带有很多默认样式，如果它们对你足够用，那么立即开始写作！它还使文本输入和编辑变得快速，因此你可以使用传统的 UNIX 工具对 LaTeX 代码进行修改。因此，你不需要一台非常快的计算机来运行 LaTeX。此外，LaTeX 文件在不同的平台之间很容易互换。它最大的优点之一是输出看起来非常专业，因为 LaTeX 是一个协议。然而，你必须编译 LaTeX 代码才能看到其输出，并且 LaTeX 需要时间和实验来设置和更改默认文档样式，这可能会令人烦恼。

# 04 安装 latexmk Perl 脚本

此命令安装了一个高度推荐的 Perl 脚本，以改进整个书籍构建过程：

```bash
$ sudo apt-get install latexmk
```

从现在开始，你可以使用以下命令将 LaTeX 代码转换为 PDF 格式：

```bash
$ latexmk -pdf book.tex
```

你所需的大多数软件包都是默认安装的。安装新的 LaTeX 软件包可能很棘手 – 最好的做法是在尝试安装之前阅读文档并遵循说明。对于这个教程，安装 texlive-full、texlive-math-extra、texlive-extra-utils、texlive-generic-extra 和 texlive-latex-extra 软件包也是值得的。

# 05 组织文件

是时候开始组织文件以简化流程了。核心 LaTeX 文件的名称将是 book.tex。与其使用一个大而不可管理的 LaTeX 文件，不如使用 `include` LaTeX 命令将书籍章节和附录放入单独的文件中，使其更易于观察：

```latex
\include{ch1}
\include{apa}
```

在这里，LaTeX 将查找名为 ch1.tex 和 apa.tex 的文件。核心 LaTeX 文件的名称将是 book.tex。这是整个过程中最重要的任务，因为它允许你编辑更小、更易于管理的文件。

我们将使用我们的示例和两个附录来制作我们的示例书籍，但你可以选择在未来的项目中使用更多或更少的页面。在为所有书籍章节和附录创建文件并在 book.tex 内部引用它们之后，你就完全准备好开始添加内容了。

# 04 安装 LaTeX Perl 脚本

