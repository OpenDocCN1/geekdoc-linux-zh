
### 3.5 摘要

在本章中，你学习了 MXML 和 ActionScript。本章的目标并不是让你成为 ActionScript 专家，而是让你对这門卓越的语言有一个概览。

首先，你了解到 MXML 是为 Flex 应用程序创建的一种 XML 词汇。本章回顾了一些基本的 XML 概念，例如标签的结构和命名空间。

随后，本章介绍了 Flex 框架的构建模块——ActionScript。在这里，你学习了 ActionScript 语言的基础知识，以及如何将其与 MXML 有效结合使用。你还学习了事件处理的基础知识。

接下来的章节将更详细地介绍 Flex 组件及其事件。

### 3.6 复习问题

- 1. MXML 是在什么时候引入的？它有哪些优点？
- 2. ActionScript 中元数据标签的作用是什么？
- 3. 如何通过查看标签来识别 MXML 文件中的类和属性？
- 4. 为什么 MXML 中需要嵌套标签？
- 5. ActionScript 中 [Bindable] 元数据标签的作用是什么？
- 6. 指示仅对来自同一类的引用可见的修饰符是。
  - A. protected
  - B. private
  - C. public
  - D. internal
  - E. static
- 7. 向 MXML 文件添加 ActionScript 的不同方式包括
  - A. 内联 ActionScript
  - B. 使用 <mx:Script> 标签
  - C. 使用 <mx:Script source="file_name"> 导入 ActionScript 文件
  - D. 在 <mx:Script> 标签内使用 include 指令
  - E. 以上所有
- 8. 事件对象的属性包括
  - A. target
  - B. type
  - C. name
  - D. B & C
  - E. A & B
- 9. 以下哪一项不是 ActionScript 3.0 的数据类型
  - A. String
  - B. short
  - C. int
  - D. uint
  - E. Number
- 10. 以下哪些属性没有描述 ActionScript 访问器？
  - A. 方法与属性之间的结合
  - B. 也称为 getter/setter
  - C. 使其能够重写从父类继承的属性
  - D. 以上所有
  - E. 以上都不是

![](img/c4119654311ebf24679359ca130a5ee6_74_0.png)

## 第 4 章 - 使用 Flex 组件

Flex 是开发富用户界面的工具——视觉组件是其主要构建模块。用户几乎完全通过组件与任何 Flex 应用程序进行交互。Flex 组件大致分为两类：控件和容器。图表是 Flex 3.0 专业版中提供的另一组组件，但这些将在*第 8 章*中讨论。

在本章中，你将学习：

- Flex 组件类层次结构
- 使用容器
- 使用控件

### 4.1 使用 Flex 组件：全局视角

**Flex 组件**是构建 Flex 应用程序的构建模块。在幕后，它们基本上是在 Flex 中定义的类。Flex 拥有无数的组件——包括容器和单独的控件。*图 4.1* 展示了它们之间的关系。

![](img/c4119654311ebf24679359ca130a5ee6_74_1.png)

**图 4.1 - Flex 组件之间的关系：容器和控件**

*容器*定义 Adobe Flash Player 渲染表面的一个矩形区域。如上图中所示，容器可以包含控件和其他容器。定义在容器内的组件称为容器的子级。每个 Flex 应用程序都有一个名为 Application 容器的根容器，它代表整个 Flash Player 绘制表面。此 Application 容器持有应用程序内的所有其他容器和组件。这由上图中最大的灰色框表示。

控件是用户与之交互的 Flex 用户界面组件。例如，按钮或文本输入。控件始终放置在容器内部。

图 4.2 显示了一些 Flex 3 组件，包括 Flex Builder 中大纲视图和设计视图中的容器和控件。

![](img/c4119654311ebf24679359ca130a5ee6_75_0.png)

**图 4.2 – 设计视图和大纲视图中的示例 Flex 3 组件**

如图所示，每个控件，如 Label、TextArea 等，都包含在诸如 Canvas、Panel 等容器内。

下方的图 4.3 显示了 Flex 3 中可用的容器（左侧框）和控件（右侧框）列表。

![](img/c4119654311ebf24679359ca130a5ee6_76_0.png)

**图 4.3 – Flex 3 中的容器（左框）和控件（右框）列表**

从上图可以想象，Flex 为开发者提供了开发丰富且严肃应用程序的所有组件。如果发现默认功能不足，你始终可以通过 ActionScript 扩展现有组件来创建自定义组件。

### 4.2 组件

如前所述，组件是所有 Flex 应用程序的构建模块，它们对应于 ActionScript 类。图 4.4 显示了 Flex 组件的类层次结构，这些组件大多数通过继承 UIComponent 创建，有时从 Sprite 类继承。

![](img/c4119654311ebf24679359ca130a5ee6_77_0.png)

**图 4.4 – Flex 组件类层次结构**

注意：有关 ActionScript 类和层次结构的更多详细信息，请访问 [http://livedocs.adobe.com/flex/3/langref/index.html](http://livedocs.adobe.com/flex/3/langref/index.html)

