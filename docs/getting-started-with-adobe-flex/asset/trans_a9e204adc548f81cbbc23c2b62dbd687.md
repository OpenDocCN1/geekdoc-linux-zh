

Adobe Flex 在客户端需要一个插件（Flash），该插件目前存在于几乎 99% 的计算机上。JSF 不需要任何客户端插件。JSF 开发起来非常复杂，因为其基本实现相当基础，对于复杂的 UI，我们需要额外的组件库。对于具有非常复杂 UI 的跨企业应用程序，Adobe Flex 会是更好的工具选择。

### 1.5.5 Adobe Flex 与 Microsoft Silverlight

Microsoft Silverlight 是一个通过编译 XAML（一种基于 XML 的界面描述语言）来提供富 Web 内容开发支持的框架。Silverlight 框架被编译并转换为 XAP 文件，由 Silverlight 插件执行。它还提供了跨平台兼容性。

Flex 应用程序使用 Flash 插件以类似的方式工作。然而，Adobe Flex 是一个开源框架，而 Silverlight 归 Microsoft 所有。这引发了关于使用专有软件与开源软件的相同争论。就 Adobe Flex 而言，来自开源社区贡献的第三方 Flex 组件数量正在迅速增加。

## 1.6 总结

在本章中，你了解了 Adobe Flex 的简短历史、使用 Adobe Flex 的优缺点以及 Adobe Flex 的不同版本和迭代。本章的目标是介绍这项新技术并提供简要概述。

在章节的后半部分，你还了解了市场上的竞争产品以及简短的对比。

## 1.7 复习题

- 什么是 RIA，它有什么用？

- 什么是 MVC，你如何将其与 Flex 应用程序联系起来？

- 使用 Adobe Flex 3 可以构建哪些类型的应用程序？

- Flex 和 Flash 之间有什么区别？

- Adobe Flex 3.0 中引入了哪些新的关键特性？

- 以下哪一项好处是 Adobe Flex 无法实现的？
  - A. 增强的用户体验
  - B. 完整的开发环境
  - C. 支持任何面向对象的编程语言用于客户端开发
  - D. 企业级功能
  - E. 跨浏览器兼容性

- Adobe Flex 的主要竞争产品是什么？
  - A. Google code
  - B. Microsoft SilverLight
  - C. Ajax
  - D. JSF
  - E. 以上都不是

- 以下哪项未包含在 Adobe Flex 3 SDK 的免费版本中？
  - A. Flex 框架
  - B. 编译器
  - C. 调试器
  - D. 设计视图
  - E. IDE

- 哪些特性仅在 Adobe Flex Builder 3.0 专业版中提供？
  - A. 高级 DataGrid
  - B. 图表组件
  - C. 交互式调试
  - D. 性能分析器
  - E. 设计视图

- 以下哪项是富互联网应用程序（RIA）的特征？
  - A. 它提供实时交互性
  - B. 它对最终用户隐藏客户端和服务器之间的通信
  - C. 它自动在客户端机器上安装应用程序的最新版本
  - D. 以上都是
  - E. 以上都不是

![](img/c4119654311ebf24679359ca130a5ee6_31_0.png)

## 第 2 章 – 安装 Flex

Flex® Builder™ 是一个用于开发 Flex 应用程序的高级 IDE。你可以下载并安装 Flex Builder 的 30 天试用版。试用期结束后，你可以从 Adobe 购买授权版本。虽然 Flex Builder 不是唯一可用于编写 MXML™ 和 ActionScript® 的软件，但 Flex Builder 可以加速整个开发过程。

在本章中，你将了解以下内容：

- Flex Builder 组件
- 如何在 Windows 上安装 Eclipse Flex Builder 插件

### 2.1 安装 Flex：总体视图

Flex Builder 由三个独立的组件组成：

- Flex SDK：一组用于构建、运行和部署 Flex 应用程序的库。
- Eclipse 插件：这提供了 IDE 支持，使开发更容易、更快。
- Flash Player：Flex 应用程序仅在 Flash Player 9 或更高版本上运行。

这体现在 *图 2.1* 中

![](img/c4119654311ebf24679359ca130a5ee6_31_1.png)

**图 2.1 – Flex Builder 组件总体视图**

如图所示，安装了 Flex Builder Eclipse 插件的 Eclipse 以及 Flex SDK 库，你可以开发编译为 .swf 文件的 RIA，并从 Flash Player 运行。

Flex Builder 可以以下列两种配置之一进行安装：

*独立 IDE*：如果你不是 Eclipse 用户，你可以安装此版本的 Flex Builder。它附带了一个兼容版本的 Eclipse。

*插件*：如果你正在使用 Eclipse，你可以安装 Flex Builder 的插件版本。在安装过程中，它会提示你输入 Eclipse 的位置。

> **注意：**
>
> 上述两种安装方法最终做的是同一件事，只有一个区别：如果你安装独立版本的 Flex Builder，默认透视图将是 Flex 开发；而如果你安装插件版本，默认透视图将是 Java 开发。
>
> 在这本书中，你将学习在 *Windows* 上安装 Flex Builder 的插件版本。本书当前范围不会讨论使用独立版本。

### 2.2 使用设置向导安装 Flex

安装 Flex Builder 插件是一个两步过程。第一步需要安装 Eclipse，第二步是安装 Flex Builder 插件。

#### 2.2.1 安装 Eclipse

请遵循以下步骤在 Windows 上安装 Eclipse：

1. 前往 http://archive.eclipse.org/eclipse/downloads/drops/R-3.3.2-200802211800/index.php 并下载与你计算机操作系统对应的 Eclipse RCP（富客户端平台）SDK 版本。
2. 将下载的文件解压到一个目录，例如你可以将其解压到 c:\eclipse。
3. 导航到解压/安装 Eclipse 的目录，并为 Eclipse 创建一个桌面快捷方式。

> **注意：**
>
> 有关 Eclipse 的更多信息，请参阅免费电子书 *Getting Started with Eclipse*，这也是本系列书籍的一部分。

#### 2.2.2 安装 Flex Builder

请遵循以下步骤安装 Flex Builder：

1. 你可以从安装 CD/DVD 安装 Flex Builder 插件，或者从 http://www.adobe.com/cfusion/entitlement/index.cfm?e=flexbuilder3 下载 60 天试用版。要安装 Flex Builder 插件，请通过执行 setup.exe 启动 InstallAnywhere 向导。
2. 向导将首先提示你选择安装语言，选择语言后点击确定。这体现在 *图 2.2* 中

![](img/c4119654311ebf24679359ca130a5ee6_33_0.png)

**图 2.2 – 语言选择器 - Flex Builder 安装向导**

3. 下一个屏幕将提示你关闭所有正在运行的应用程序，因为 Flex 将安装其自己的 Flash Player 版本。这体现在 *图 2.3* 中

![](img/c4119654311ebf24679359ca130a5ee6_33_1.png)

**图 2.3 – 关闭所有正在运行的应用程序 - Flex Builder 安装向导**

4. 下一个屏幕将提示你接受许可证。接受条款并点击下一步。这体现在 图 2.4 中

![](img/c4119654311ebf24679359ca130a5ee6_34_0.png)

5. 向导现在将提示你选择默认安装位置 - 选择位置并点击下一步。这体现在 图 2.5 中

![](img/c4119654311ebf24679359ca130a5ee6_34_1.png)

6. 下一个屏幕将询问你 Eclipse 安装目录的位置。选择你安装 Eclipse 的目录并点击下一步。这体现在 图 2.6 中

![](img/c4119654311ebf24679359ca130a5ee6_35_0.png)

**图 2.6 – Eclipse 目录屏幕 - Flex Builder 安装向导**

7. 向导现在将提示你安装 Flash Player，如果系统中已安装的浏览器中尚未安装 Flash Player。Flash Player 渲染你在应用程序中创建的 swf 文件。此屏幕还将询问你选择开发过程中可能需要的其他插件。进行适当的选择并点击下一步。这体现在 *图 2.7* 中

![](img/c4119654311ebf24679359ca130a5ee6_35_1.png)

**图 2.7 – 浏览器的 Flash Player 插件 - Flex Builder 安装向导**

8. 以下屏幕允许你查看安装参数。验证后，点击 *安装* 按钮。这体现在 *图 2.8* 中

