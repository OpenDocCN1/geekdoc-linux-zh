
## 为类定义

类的`析构函数`（deconstructor function）是程序调用以析构类类型对象的函数。析构函数不接受参数且没有返回值。

**注意：** 在正常情况下，每当给定类的对象离开范围时，与对象相关的内存就会释放供重用。在这种情况下，你可以省略析构函数的定义。然而，在高级应用程序中，或者类赋值导致潜在指针冲突的情况下，可能需要显式地释放自由存储器内存。

除了构造函数和析构函数外，`Circle`类还包含一个名为`area`的公共函数。

程序可以调用此函数来计算圆对象的面积。

列表 6.18 中的主程序展示了如何声明对象。`mycircle`被声明为`Circle`类型，并赋予半径 2。

该程序的最后一条语句调用该函数计算`mycircle`的面积，并将其传递给输出函数进行显示。注意，面积计算函数是通过复合名称识别的，这与 C++ 类定义之外的数据结构的成员函数相同。这种使用下划线的方法强调了类型为`Circle`的对象`mycircle`被要求执行一个其自身的成员函数，并带有其自身的引用。你可以定义一个也包含`area`函数的`Rectangle`类，从而重载`area`函数名，并带有计算不同类型几何实体面积的相应算法。

## 继承与多态

面向对象语言（以及 C++）的另一个最终特征是对类继承和多态的支持。

你可以定义新的 C++ 类（以及相应的数据类型），使得它们自动`继承`与父类相关的属性和算法。每当新类使用任何一种标准 C 数据类型时，就会执行此操作。创建新类定义的类被称为`基类`（base class）。例如，一个包含整数成员的结构体也继承了所有与整数相关的数学函数。根据基类定义的新类被称为`派生类`（derived classes）。列表 6.18 中的`Circle`类就是一个派生类。

派生类可以基于多个基类，在这种情况下，派生类继承多个数据类型及其相关函数。这种类型被称为`多继承`（multiple inheritance）。

由于函数可以被重载，声明为派生类成员的对象的行为可能与基类类型的对象不同。例如，如果程序尝试给一个正整数类对象赋值负数，该类可能会返回错误，尽管对于基整数类型的对象来说，这种赋值是合法的。

这种同一类层次结构中的不同对象在相同情况下具有不同行为的能力被称为`多态性`（polymorphism），这是许多人难以理解的面向对象概念。

然而，它也是为面向对象设计和代码提供许多力量和优雅性的概念。如果你正在使用预定义的图形用户界面（GUI）类设计应用程序，例如，你可以自由地要求各种窗口对象适当地显示自己，而无需担心窗口的颜色、位置或其他显示特征在每种情况下是如何处理的。

类继承和多态是 C++ 中最强大的面向对象特征之一。与 C 的其他不那么剧烈的扩展相结合，这些特征使得如今 UNIX 中的许多最新应用程序和系统能力成为可能，包括用于用户终端的 GUI 以及许多先进的互联网和世界维网技术，其中一些将在本书的后续章节中讨论。

## 总结

UNIX 是基于 C 语言构建的。C 是一种平台无关的、编译的过程语言，基于函数以及推导出新的、程序员定义的数据结构的能力。

C++ 通过为面向对象设计和代码提供必要的特性扩展了 C 的能力。C++ 编译器可以正确编译 ANSI C 代码。C++ 还提供了一些特性，例如将函数与数据结构关联的能力，这些不需要使用完整的基于类的面向对象技术。由于这些原因，C++ 语言允许现有的 UNIX 程序随着时间的推移转向采用面向对象。

**UNIX Unleashed, Internet Edition**
**- 7 -**

### make 工具

*作者：Sean Drew*

本章旨在概述 UNIX `make` set。`make` 的大部分显著特征都已涵盖；然而，您应该查阅您的 `man` 页面以获取更多信息，因为不同 UNIX 供应商的 `make` 版本往往不同。以下是本章涵盖的主要主题列表。

- `Makefiles`。本节概述了 Makefile 的内容。
- `Target Lines`（目标行）。本节描述了如何告知 `make` 工具哪些项目是可以构建的。
- `Shell Command-Lines`（Shell 命令行）。本节解释了如何在 Makefile 中编码 Unix Shell 语句。
- `Macros`（宏）。本节讨论了在 Makefile 中如何以及何时定义宏。
- `make` 指令（Directives）。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Command-Line Arguments`（命令行参数）。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Makefiles`。本节概述了 Makefile 的内容。
- `Target Lines`。本节描述了如何告知 `make` 工具哪些项目是可以构建的。
- `Shell Command-Lines`。本节解释了如何在 Makefile 中编码 Unix Shell 语句。
- `Macros`。本节讨论了在 Makefile 中如何以及何时定义宏。
- `make` 指令。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Command-Line Arguments`。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Makefiles`。本节概述了 Makefile 的内容。
- `Target Lines`。本节描述了如何告知 `make` 工具哪些项目是可以构建的。
- `Shell Command-Lines`。本节解释了如何在 Makefile 中编码 Unix Shell 语句。
- `Macros`。本节讨论了在 Makefile 中如何以及何时定义宏。
- `make` 指令。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Command-Line Arguments`。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Makefiles`。本节概述了 Makefile 的内容。
- `Target Lines`。本节描述了如何告知 `make` 工具哪些项目是可以构建的。
- `Shell Command-Lines`。本节解释了如何在 Makefile 中编码 Unix Shell 语句。
- `Macros`。本节讨论了在 Makefile 中如何以及何时定义宏。
- `make` 指令。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Command-Line Arguments`。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Introduction to make`。本节概述了 `make` 工具。
- `Makefiles`。本节概述了 Makefile 的内容。
- `Target Lines`。本节描述了如何告知 `make` 工具哪些项目是可以构建的。
- `Shell Command-Lines`。本节解释了如何在 Makefile 中编码 Unix Shell 语句。
- `Macros`。本节讨论了在 Makefile 中如何以及何时定义宏。
- `make` 指令。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Command-Line Arguments`。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Introduction to make`。本节概述了 `make` 工具。
- `Makefiles`。本节概述了 Makefile 的内容。
- `Target Lines`。本节描述了如何告知 `make` 工具哪些项目是可以构建的。
- `Shell Command-Lines`。本节解释了如何在 Makefile 中编码 Unix Shell 语句。
- `Macros`。本节讨论了在 Makefile 中如何以及何时定义宏。
- `make` 指令。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Command-Line Arguments`。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Introduction to make`。本节概述了 `make` 工具。
- `Makefiles`。本节概述了 Makefile 的内容。
- `Target Lines`。本节描述了如何告知 `make` 工具哪些项目是可以构建的。
- `Shell Command-Lines`。本节解释了如何在 Makefile 中编码 Unix Shell 语句。
- `Macros`。本节讨论了在 Makefile 中如何以及何时定义宏。
- `make` 指令。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Command-Line Arguments`。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Introduction to make`。本节概述了 `make` 工具。
- `Makefiles`。本节概述了 Makefile 的内容。
- `Target Lines`。本节描述了如何告知 `make` 工具哪些项目是可以构建的。
- `Shell Command-Lines`。本节解释了如何在 Makefile 中编码 Unix Shell 语句。
- `Macros`。本节讨论了在 Makefile 中如何以及何时定义宏。
- `make` 指令。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Command-Line Arguments`。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Introduction to make`。本节概述了 `make` 工具。
- `Makefiles`。本节概述了 Makefile 的内容。
- `Target Lines`。本节描述了如何告知 `make` 工具哪些项目是可以构建的。
- `Shell Command-Lines`。本节解释了如何在 Makefile 中编码 Unix Shell 语句。
- `Macros`。本节讨论了在 Makefile 中如何以及何时定义宏。
- `make` 指令。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Command-Line Arguments`。本节描述了可以包含在 Makefile 中的特殊 `make` 命令。
- `Introduction to make`。本节概述了 `make` 工具。

`make` 工具的设计是为了自动化构建程序和其他项目的过程。它使用一个名为 `Makefile` 的文件来定义文件之间的依赖关系以及构建它们所需的命令。当你运行 `make` 时，它检查 `Makefile` 并根据修改日期和依赖关系确定哪些文件需要更新。

`Makefile` 的核心是规则。规则由一个目标、一个冒号以及依赖列表组成。目标和依赖项之后是一个或多个用于构建目标的命令。每条命令都必须缩进。
