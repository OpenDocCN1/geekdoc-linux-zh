
## 目录

### 集合
- QCollection 147
- QDict 147
- QDictIterator 148
- QIntCache 148
- QIntCacheIterator 148
- QIntDict 148
- QIntDictIterator 148
- QIntValidator 148
- QList 148
- QListIterator 149
- QMap 149
- QMapConstIterator 149
- QMapIterator 149
- QPtrDict 149
- QPtrDictIterator 149
- QQueue 149
- QSortedList 149
- QStack 149
- QString 和 QStrList 150
- QStringListIterator 150
- QStringList 150
- QValueList 150
- QValueListConstIterator 150
- QValueListIterator 150
- QValueStack 150
- QVector 150

### 文本处理
- QChar 151
- QClipboard 151
- QConstString 151
- QCString 151
- QDoubleValidator 151
- QRegExp 151
- QString 151
- QTextCodec 151
- QTextDecoder 151
- QTextEncoder 152
- QTranslator 152
- QValidator 152

### 日期与时间
- QDate 152
- QDateTime 152
- QTime 152

### 其他
- QRangeControl 153
- QGuardedPtr 153
- QMimeSource 154
- QMimeSourceFactory 154
- QPoint 154
- QPointArray 154
- QRect 154
- QSignal 154
- QSignalMapper 154
- QSize 154
- QTimer 154
- QVariant 156
- QWMatrix 156
- 摘要 156

## 6 QT 命名空间与 Qt 扩展 157
- Qt 类 157
- Qt 扩展 161
    - OpenGL 扩展 161
    - 网络支持 162
- 摘要 162

### 第三部分 开发专业的 Qt 应用程序 163

## 7 Qt 开发考量 165
- 国际化 166
    - 使用 QString 167
    - QObject::tr() 168
    - findtr 工具 169
    - msg2qm 工具 170
    - mergeqt 工具 171
    - 输入法 171
- 平台无关项目 172
    - Tmake 工具 173
- 对象重用考量 173
    - 保持简单且切中要点 173
    - 始终考虑性能…… 174
    - 了解你的编译器 174
    - 不要假设 174
    - 对暴露的返回 void 的方法使用槽 175
- 动态链接和静态链接 175
    - 大型程序 176
    - 兼容性 176
    - 可能的解决方案 176
    - 配置管理 177
    - 完全静态链接 177
    - 混合静态/动态链接 177
- 调试项目 178
    - 文档和培训错误 179
    - 用户感知缺陷 179
    - 软件缺陷 180
    - 缺陷事件捕获 180
    - 核心转储分析（仅限 Linux/Unix） 188
    - Dr. Watson（仅限 Windows） 189
    - 使用调试器 189
- 快速应用开发 190
    - Qt Architect 190
    - QteZ 190
    - KDevelopp 191
    - Ebuilder 191
- 摘要 192

## 8 Windows 2000 主题 193
- DDE 服务器类 193
- 多媒体支持 197
- 摘要 210

## 附录 A 212

## 附录 B 266

## 索引 269

## 前言

1991 年夏天，我和 Haavard Nord 一起坐在挪威特隆赫姆的一个公园长椅上。当时我们都在特隆赫姆地区医院同一个医疗数据库项目工作。我们正在讨论如何进行用户界面时，Haavard 说：“我们需要一个面向对象的显示系统。”

一年后，因为那句话，我制作了一个 C++ GUI 工具包。又过了一年，我制作该工具包的公司（也是我当时工作的公司）决定将其废弃以采用 Motif。我认为他们疯了。一天晚上，Haavard 给我打电话说：“让我们从头开始构建一个更新、更好的工具包。辞职，和我一起创办一家公司。”

Haavard 首先完成了他的论文，制作了第一个 Qt 内核。然后，在接下来的一年里，我们在一间小办公室里日夜编写代码，靠我们的妻子生活。我们有幸在无打扰的环境中工作。Qt 逐渐成形，我们打磨细节，设计并重新设计，直到感觉恰到好处（这是 Trolltech 至今仍遵循的设计准则）。随后我们获得了一个小型咨询合同，其中使用了我们当时仍相当原始的版本 0.60 的 Qt，以极其低廉的薪水雇用了 Arnt Gulbrandsen，雪球开始滚动起来。

我从未想象过有一天我会为 Prentice Hall 出版的一本关于 Qt 的书写前言。我们的许多梦想已经成真，这是其中之一。

我很荣幸遇到了本书的作者 Patric Ward。除了是一位出色的 Qt 黑客，他也是一个非常好的人，且有很好的幽默感。我认为这对于编写这样一本书来说是一个完美的组合。现在请坐下来，享受 Patric Ward 讲述的 Qt 的奇妙之处。帕特，舞台交给您了。

Eirik Eng，
Trolltech AS 总裁

## 序言

本书是一本指南，用于使用 Trolltech AS 的 Qt 软件工具包编写适用于 Linux、Microsoft NT 4.0、Windows 2000、Windows 95 和 Windows 98 的应用程序。正如任何一本尊重编程指南所应做的，它提供了对 Qt 软件发行版以及 Qt 工具包提供的对象、小部件和便利功能的工作知识。此外，它还探索了一些在企业应用开发中并不明显的 Qt 编程方面，这些内容在工具包供应商的文档中并不显而易见。

### 目标读者

本书面向希望使用 Qt 工具包编写有效应用程序的 C++ 程序员和学生。重点主要在于平台无关的软件，但不可避免地涵盖了一些平台特定的主题。

### 假设条件

本书不是 Qt 对象和小部件的参考手册——Trolltech 在提供 HTML 和 Adobe Postscript 格式的参考文档方面做得非常出色。他们的文档包含在 Qt-Free 版本和 Qt-Professional 版本的许可证中，并且可以从 Troll 网站获取。http://www/trolltech.com/

本书既面向经验丰富的 C++ 程序员，也面向知识渊博的初学者。假设读者熟悉标准 C++ 数据类型以及如何创建新的数据类型。读者应熟悉面向对象（OO）设计和实现的基本概念，特别是对象继承的概念。为了清晰起见，我在示例中避免使用多重继承，但鼓励读者进行实验。

虽然本书的标题暗示其重点是 Linux 和 Windows 2000，但实际范围要大得多。大多数示例以及 CD 上提供的代码，在 Qt 支持的几乎任何平台上都能正确编译和运行。

如果您是一位经验丰富的 Microsoft 开发人员，这里展示的一些编码风格可能会引起轻微困惑。请记住，除了少数例外，本书中展示的代码旨在用于跨平台使用。因此，您很少会看到对 DWORD、LPVOID 和 LPSTR 数据类型的引用，因为在 Microsoft 领域之外的平台上它们是未定义的，而且由于大多数标准 Unix 数据类型与 Windows 开发兼容，因此使用它们作为替代。两者的“正确性”完全是主观的。

Microsoft 平台特定的示例需要 Qt-Professional 许可证。可以直接从 Trolltech 获得许可证，并在第 1 章中详细讨论。虽然可以使用 Borland 编译器和工具进行 Qt 软件开发，但开发人员使用 Microsoft Visual C++ 更为常见。因此，假设 Windows 开发人员可以访问 Microsoft Visual Studio 6.0 和 VC98（Visual C++）。

从理论上讲，可以使用 Cygnus Win32 实现、ming32 编译器发行版、Win32 的 X11R6.3 开发工具包以及适当的 X 服务器，在 Windows 平台上编译和使用 Qt-Frame 版本的应用程序。由于这是一个极其罕见的环境，本书中的任何示例都没有涉及。但是，假设您成功使用 Cygnus 编译器发行版编译了 Qt-Frame 版本，任何 Linux 示例都应该可以工作——这是我尚未尝试的事情。

可以使用 Qt-Frame 版本进行 Linux 开发。您需要一个 C++ 编译器。本书假设使用来自自由软件基金会（FSF）的通用 gcc/g++ 发行版（示例中使用了 gcc-2.95），假设它是合理的最低公分母。

Troll 开箱即用地支持许多其他平台。我在 HP/UX 或 AIX 上使用 Qt 几乎没有遇到麻烦。

### 本书的组织结构

本书分为三个部分。第一部分是对 Qt 工具包的简介。它提供了一些初步的编程示例，并讨论了一些使 Qt 开发区别于其他工具包的独特功能。第二部分详细讨论工具包组件。第三部分讨论项目层面的考量和调试技术。

