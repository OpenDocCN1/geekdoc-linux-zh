
# Qt 4 C++ GUI 编程

## 第一部分：Qt 基础

## 第二部分：进阶 Qt

## 第三部分：高级 Qt

### 前言

为什么 Qt？为什么程序员喜欢它？当然，答案是显而易见的：单源兼容性、功能丰富性、C++ 性能、源码可用性、文档、技术支持以及所有提到的 Qt 营销材料。这些都很好，但它们忽略了最重要的一点：Qt 之成功是因为程序员喜欢它。

每一个字段。严格来说，你应该等待信用卡公司向你开具账单，上面会有他们实际使用的汇率。虽然这并不困难，但从不同的来源查找不同的信息，然后将相关项目以形式复制到几个地方，感觉非常不必要的别扭。

编程非常像填写差旅报销单，而且更糟。而这正是 Qt 大显身手的地方。Qt 与众不同。一方面，Qt 符合逻辑；另一方面，Qt 很有趣。Qt 让你能够专注于自己的任务。当 Qt 的原始架构师面临问题时，他们不仅仅是在寻找良好的解决方案或最简单的解决方案。他们寻找的是正确的解决方案，并将其记录下来。诚然，他们犯过错误，诚然，他们的某些设计决定没有通过时间的考验，但他们仍然取得了许多成就：一个最初设计为桥接 Windows 95、Mac OS X 和 GNU/Linux 而设计的系统，现在为嵌入式 Linux 的 Qtopia 应用平台奠定了基础。

你可以从这一事实中看到，一个最初是不正确的系统是可以并且能够被纠正的。

在 Qt 变得如此流行和被广泛使用之前，Qt 开发者对寻找正确解决方案的奉献就让 Qt 变得与众。这种奉献在今天同样强大，并影响着每一个开发和维护 Qt 的人。对我们来说，开发 Qt 是一份责任，也是一种荣幸。我们为帮助让你的专业和开源生活变得更加简单、愉快而感到自豪。

Matthias Ettrich

挪威，奥斯陆

2006年6月

### 前言

Qt 是一个全面的 C++ 框架，用于“编写一次，随处编译”的方法开发跨平台 GUI 应用程序。Qt 让程序员可以使用一套源码树，开发出运行在 Windows 98、Mac OS X、Linux、Solaris、HP-UX 以及其他许多带有 X11 的 Unix 版本上的应用程序。Qt 库和工具也是 Qtopia Core 的一部分，该产品在嵌入式 Linux 之上提供了自己的窗口系统。

本书的目的是教你如何使用 Qt 4 编写 GUI 程序。书从“Hello Qt”开始，迅速过渡到更高级的话题，例如创建自定义控件和提供拖放功能。文本由一张 CD 盘补充，其中包含了示例的源代码。CD 盘还包含了适用于所有支持平台的 Qt 4.1.1 开源版本，以及 MinGW——一组可以在 Windows 上构建 Qt 应用程序的免费可用开发工具。附录解释了如何安装软件。

本书分为三个部分。第一部分涵盖了使用 Qt 编写 GUI 应用程序所需的所有概念和技术。仅凭这部分的知识就足以编写 GUI 应用程序。第二部分更深入地探讨了 Qt 的主题，第三部分提供了更专业、更高级的材料。第二部分和第三部分的章节可以按顺序阅读，但它们假设读者已经熟悉第一部分的内容。

本书 Qt 3 版的读者会发现这个新版本在内容和风格上都很熟悉。本版已经过更新，以利用 Qt 4 的新功能（其中一些功能是在 Qt 4.1 中引入的），并展示了显示良好惯用 Qt 4 编程技巧的代码。在许多情况下，我们使用了与 Qt 3 版相似的示例。这不会影响新读​​，但将帮助那些读过旧版本的读者适应 Qt 4 更清晰、更具表现力的风格。

本版包含了新的章节，涵盖了 Qt 4/视图 架构、插件框架以及使用 Qtopia 进行嵌入式编程，还增加了一个附录。就像 Qt 3 版的书一样，重点在于解释 Qt 编程，而不是简单地重述或总结 Qt 详尽在线文档。

我们编写本书的假设是你已经具备了 C++、Java 或 C# 的基础知识。代码示例使用了 C++ 的子集，避免了许多在编写 Qt 时很少需要的 C++ 特性。在少数几个无法避免高级 C++ 结构的地方，我们解释了它们的使用场景。

如果你已经熟悉 Java 或 C# 但对 C++ 几乎没有或没有经验，我们建议你从附录 B 开始阅读，它提供了足够的 C++ 介绍以让你能够使用本书。为了更深入地介绍 C++ 面向对象编程，我们推荐 David Deitel 和 Paul Deitel 编写的《C++ How to Program》，以及由 Stanley B. Lippman、Josée Lajois 和 Barbara E. Moo 编写的《C++ Primer》。

Qt 以其跨平台框架而闻名，但由于其直观且强大的 API，许多组织使用 Qt 进行单平台开发。Adobe Photoshop 元素只是一个用 Qt 编写的大众市场应用示例。虚拟市场中的许多复杂软件系统，例如 3D 动画工具、数字胶片处理、电子设计自动化（用于芯片设计）、油气勘探、金融服务和医学影像，都是用 Qt 构建的。如果你正在使用一个用 Qt 编写的成功 Windows 产品，你只需重新编译就能在 Mac OS X 和 Linux 世界中创造新市场。

Qt 有多种许可协议可用。如果你想构建商业应用程序，必须购买商业 Qt 许可；如果你想构建开源程序，可以使用开源 (GPL) 版本。Qt 是 K 桌面环境 (KDE) 以及与其一同构建的许多开源应用程序的基础。

除了 Qt 的数百个类外，还有可以扩展 Qt 范围和能力的插件。其中一些产品，如用于应用程序的 Qt Script (QSA) 和 Qt Solutions 组件，可以从 Trolltech 获取，而另一些则由其他公司和开源社区提供。请访问 `http://www.trolltech.com/products/3party` 获取有关插件的信息。

### 致谢

我们的首要感谢的是 Trolltech 的总裁 Eirik。Eirik 不仅鼓励我们编写了 Qt 3 版书籍，还允许我们花费大量时间来编写。Eirik 和 Trolltech 首席官 Haavard 都阅读了手稿并提供了宝贵的反馈。

对于 Qt 3 版，我们邀请了两位 Qt 客户 Paul Curtis 和 Klaus Schmiding 担任我们的外部评审员。他们都是 Qt 专家，对技术细节非常关注，发现了我们手稿中的细微错误并提出了许多改进。在 Trolltech 内部，除了 Matthias 外，我们最得力的评审员是 Reginald Schauspieler。他的技术见解无价之，并教会了我们许多不知道的方法。

对于 Qt 4 版，我们继续受到 Eirik、Haavard 和 Matthias 的坚定帮助和支持。Klaus Schmiding 继续提供宝贵的反馈，在 Trolltech 内部，我们的关键评审员是 Andreas Hanssen、Henrik Hartz、Vivi Glückäck Karlsen、Trenton Schulz、Andy Shaw 和 Pavel Vibe。

除了上述评审员外，我们从 Harald Ferngenel（数据库）、Volker Hisheimer（ActiveX）、Bradley Huges（多线程）、Torn Kjærner（3D 图形和数据库）、Lars Knoll（2D图形和国际化）、Sam Magnususon（make）、Marius Bugge Mensen、Dimitri Papadopoulos（QtX11）、Paul Olav Tibet（自定义控件和嵌入式编程）、Rainer Schmidt（网络和 XML）、Amrit Paul Singh（C++ 介绍）以及 Gunnar Sletta（2D 图形和事件处理）那里获得了专家级的帮助。

特别感谢 Trolltech 的文档和支持团队，在书籍占据了我们大量时间时处理了文档相关问题，并感谢 Trolltech 的系统管理员在整个项目期间保持了我们的机器运行和网络通畅。如果你在书中发现错误，或者对下一版有建议，我们非常乐意听到你的反馈。你可以通过 `qt-book@trolltech.com` 联系我们。

在制作方面，Trenton Schulz 制作了随附的 CD，Trolltech 的 Cathrine Bore 代表我们处理了合同和法律事务。感谢 Nathan Clement 提供的 Troll 插画。最后，感谢 Pearsons 的 Lara Wysong，她很好地处理了制作方面的实际工作。

## Qt 简史

Qt 框架首次于 1995 年 5 月公开发布。它最初由 Haavard Nord（Trolltech 首席执行）和 Eirik Chambe-Eng（Troll 主席）开发。Haavard 和 Eirik 在特隆赫姆的挪威科技学院相识，他们都在那里获得了计算机科学的硕士学位。

Haavard 对 C++ GUI 开发的产生兴趣始于 1988 年，当时他受一家瑞典公司的委托，开发一个 C++ GUI 框架。几年后，即在 1990 年夏天，Haavard 和 Eirik 正在合作开发一个用于超声波图像的 C++ 数据库应用程序。该系统需要在 Unix、Macintosh 和 Windows 上带有 GUI 运行。那年夏天的某天，Haavard 和 Eirik 出去享受阳光，当他们坐在公园长椅上时，一人说：“我们需要一个面向对象的显示系统。”随后的讨论为他们很快开始构建的面向对象的跨平台 GUI 框架奠定了理论基础。

1991 年，Haavard 开始编写类，并与 Eirik 合作进行设计。次年，Eirik 提出了“信号与槽”（signals and slots）的想法，这简单而强大的编程范式，已被许多其他工具包所采用。Haavard 采取了这一想法并将其实现。到 1993 年，Haavard 和 Eirik 开发了 Qt 的第一个图形内核并实现了宽泛的部件（widgets）。在当年年底，Haavard 建议他们进入业务，构建“世界上最好的 C++ GUI 框架”。1994 年，Qt 无声无息地开始，两个程序员想要进入一个成熟的市场，但他们只有一个未完成的产品且没有资金。幸运的是，他们两个被雇佣了，因此 Eirik 和 Haavard 开发了产品并开始获得收入。“Q”字母被选为前缀，因为它看起来很漂亮。“t”字母代表“toolkit”（工具包）。1994 年 3 月 4 日，该公司成立，最初名为 Quasar Technologies，现在是 Trolltech。

1995 年 4 月，得益于一位挪威大学教授，他们获得了开发基于 Qt 的软件合同。这段时期，Trolltech 聘请了 Arnt Gulbrandsen，他在 Trolltech 工作六年期间设计并实现了一套精妙的文档系统并贡献了 Qt 的代码。1995 年 5 月 20 日，Qt 0.9 上传到 sunsite.edu。六天后，发布在 os.linux 上。这是 Qt 的首次发布。Qt 可用于 Windows 和 Unix 开发，在两个平台上都提供相同的 API。从第一天起，商业开发需要商业许可，而开源开发提供免费版本。这让 Trolltech 维持了运营。

1996 年 3 月，欧洲空间局成为 Qt 的第二个客户，购买了商业许可。随着不断的需求，Eirik 和 Haavard 聘请了另一个开发者。Qt 0.97 于 5 月底发布，1996 年 9 月 24 日，Qt 1.0 出问。到当年年底，Qt 达到了 1.1 版本；不同国家的客户购买了商业许可。这一年还见证了由 Matthias Ettrich 领导的 KDE 项目的成立。

1997 年 4 月发布了 Qt 1.2。Matthias Ettrich 使用 KDE 的决定成为 Linux 上 C++ GUI 开发的事实标准。1997 年 9 月发布了 Qt 1.3。

1998 年，Matthias 加入 Trolltech，同年 9 月制作了最后一个主要的 Qt 版本 1.4。1999 年 6 月发布了 Qt 2.0。Qt 2 有一个新的开源版本——Qt 公许可证（QPL），符合开源定义。此时，Trolltech Pty Ltd（澳大利亚）成立。1999 年 8 月，它获得了 LinuxWorld 最佳库/工具奖。2000 年，Trolltech 发布了 Qtopia（当时称为 QtEmbedded）。它被设计在嵌入式 Linux 设备上运行，并提供了自己的窗口系统作为 X11 的轻量级替代品。Qt1 和 Qt Core 现在都提供广泛使用的 GNU 通用许可证（GPL）以及商业许可。到 2000 年底，Trolltech 建立了 Trolltech Inc（美国），并发布了第一版本的 Qtopia，这是一个适用于手机和 PDA 的应用程序平台。Qtopia Core 在 2001 年和 2002 年获得了 LinuxWorld“最佳嵌入式 Linux 解决方案”，Qtopia 在 2004 年获得了同样的荣誉。

Qt 3.0 于 2001 年发布。Qt 现在可在 Windows、Mac OS X、Unix 和 Linux（桌面和嵌入式）上使用。Qt 3 提供了 42 个新类，其代码超过 500,000 行。Qt 3 是 Qt 2 的巨大进步，包括大大改进的本地化和 Unicode 支持、全新的查看和编辑界面，以及类 Perl 的正则表达式。Qt 3 在 2002 年赢得了《软件开发时代》的“Jolt 效率奖”。

2005 年夏天，发布了 Qt 4.0。拥有5500多个类和9000多个函数，Qt 4 比之前的任何版本都更大、更丰富，并被分成了几个库，以便开发者只需链接他们需要的 Qt 部分。Qt 4 是对以前版本的巨大跨越，改进包括了一套全新的易于使用的模板容器、高级的模型/视图功能、快速灵活的 2D 绘画框架以及强大的 Unicode 文本查看类。第一个版本在它支持的所有平台上均供商业和开源开发使用。

同样在 2005 年，Trolltech 在北京开设了办事处，为中国客户提供销售服务、培训和技术支持。

自 Trolltech 出生以来，Qt 的人气不断增长，并一直持续到今天。在过去的十年里，Qt 已从少数人使用的产品转变为全球数千名开源开发者每天使用的工具。

## 第一部分

### 基础 Qt

- Hello Qt
- 创建连接
- 布局

## 1. 开始

本章展示了如何将基础 C++ 与 Qt 提供的功能相结合创建图形界面（GUI）应用程序。本章还介绍了两个思想：“信号与槽”。在第 2 章中我们将深入研究，在第 3 章中我们将构建更真实的应用程序。

### Hello Qt

让我们从一个简单的 Qt 程序开始。我们将首先学习它，然后看看如何编译和运行。

```cpp
#include <QApplication>
#include <QLabel>

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    QLabel *label = new QLabel("Hello Qt!");
    label->show();
    return app.exec();
}
```

第 5 行创建一个 `QApplication` 对象来管理应用程序资源。`QApplication` 的构造函数需要 `argc` 和 `argv`，因为 Qt 支持一些命令行参数。第 6 行创建一个 `QLabel` 控件显示“Hello Qt!”。在 Qt 术语中，控件是用户界面中的视觉元素。大多数应用程序使用 `MainWindow` 或 `QDialog` 作为窗口，但 Qt 非常灵活，任何控件都可以是窗口。在这个示例中，`QLabel` 就是应用程序窗口。第 7 行使标签可见。控件总是隐藏创建，以便我们在显示之前对其进行自定义，避免闪烁。第 8 行将控制权交给应用程序。此时，程序进入循环。这是一种等待模式，等待用户操作。用户产生事件（也称为“消息”），程序可以通过执行一个或多个函数做出响应。例如，当用户点击控件时，会产生“鼠标按下”和“鼠标释放”。在这方面，GUI 程序与传统的批处理程序有很大区别，后者通常处理输入、产生结果并终止交互。

为了简单起见，我们没有在 `main()` 函数结束时删除 `QLabel` 对象。这种内存泄漏在这样的小程序中是无害的，因为操作系统会在程序终止时回收内存。

**图 1.1.** Linux 上的 Hello

### Hello Qt

输入命令来编译程序。在 Windows 上输入 `hello`，在 Unix 上输入 `./hello`，在 Mac OS X 上打开 `hello.app`。要终止程序，点击窗口标题栏上的关闭按钮。

如果你正在使用 Windows 并安装了 Qt 开源版和 MinGW 编译器，你将有一个 Dos 提示符快捷方式，它已经正确设置了所有 Qt 环境变量。如果你启动此窗口，可以如上所述使用 `qmake` 和 `make` 在其中编译 Qt 应用程序。可执行文件将生成在应用程序的 debug 或 release 文件夹中，例如 `c:\qt-book\release\hello.exe`。

如果你使用的是 Microsoft Visual C++，你需要运行 `nmake` 而不是 `make`。或者，你可以通过输入以下命令从 `hello.pro` 创建 Visual Studio 项目文件：

```
qmake -tp vc hello.pro
```

然后在 Visual Studio 中构建程序。如果你在 Mac OS X 上使用 Xcode，可以使用以下命令生成 Xcode 项目：

```
qmake -spec macx-xcode
```

![](img/34bd675de80edd220dc2d53b429caf78_22_0.png)

**图 1.2.** 带有基本 HTML 格式的标签

在继续下一个示例之前，我们来玩点什么：将该行

```
QLabel *label = new QLabel("Hello Qt!");
```

替换为

```cpp
QLabel *label = new QLabel("<h2><i>Hello!</i></h2>")
```

并重新构建应用程序。示例所示，使用一些简单的 HTML 样式格式就能美化 Qt 应用程序的用户界面。

# Making Connections
