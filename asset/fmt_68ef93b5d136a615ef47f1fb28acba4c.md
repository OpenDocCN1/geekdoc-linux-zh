
| Key | Key_Escape, Key_Tab, Key_Backtab, Key_BackTab = Key_Backtab, Key_Backspace, Key_Return, Key_Enter, Key_Insert, Key_Delete, Key_Pause, Key_Print, Key_SysReq, Key_Home, Key_End, Key_Left, Key_Up, Key_Right, Key_Down, Key_Prior, Key_PageUp = Key_Prior, Key_Next, Key_PageDown = Key_Next, Key_Shift, Key_Control, Key_Meta, Key_Alt, Key_CapsLock, Key_NumLock, Key_ScrollLock, Key_F1, Key_F2, Key_F3, Key_F4, Key_F5, Key_F6, Key_F7, Key_F8, Key_F9, Key_F10, Key_F11, Key_F12, Key_F13, Key_F14, Key_F15, Key_F16, Key_F17, Key_F18, Key_F19, Key_F20, Key_F21, Key_F22, Key_F23, Key_F24, Key_F25, Key_F26, Key_F27, Key_F28, Key_F29, Key_F30, Key_F31, Key_F32, Key_F33, Key_F34, Key_F35, Key_Super_L, Key_Super_R, Key_Menu, Key_Hyper_L, Key_Hyper_R, Key_Space, Key_Any = Key_Space, Key_Exclam, Key_QuoteDbl, Key_NumberSign, Key_Dollar, Key_Percent, Key_Ampersand, Key_Apostrophe, Key_ParenLeft, Key_ParenRight, Key_Asterisk, Key_Plus, Key_Comma, Key_Minus, Key_Priod, Key_Slash, Key_0, Key_1, Key_2, Key_3, Key_4, Key_5, Key_6, Key_7, Key_8, Key_9, Key_Colon, Key_Semicolon, Key_Less, Key_Equal, Key_Greater, Key_Question, Key_At, Key_A, Key_B, Key_C, Key_D, Key_E, Key_F, Key_G, Key_H, Key_I, Key_J, Key_K, Key_L, Key_M, Key_N, Key_O, Key_P, Key_Q, Key_R, Key_S, Key_T, Key_U, Key_V, Key_W, Key_X, Key_Y, Key_Z, Key_BraceLeft, Key_Slash, Key_BraceRight, Key_AsciiCircum, Key_Underscore, Key_QuoteLeft, Key_BraceLeft, Key_Bar |

| ArrowType | UpArrow, DownArrow, LeftArrow, RightArrow |

| RasterOp | CopyROP, OrROP, XorROP, NotAndROP, EraseROP = NotAndROP, NotCopyROP, NotORROP, NotXorROP, AndROP, NotEraseROP=AndROP, NotClearROP, SetROP, NoROP, AndNotROP, OrNotROP, NanDroP, NoRoP, LastROP=NorROP |

| PenStyle | NoPen, SolidLine, DashLine, DotLine, DashDotLine, DashDotDotLine, MPenStyle |

### QT 扩展

Qt 扩展位于供应商支持的核心功能之外。这并不意味着如果你发现 bug，Troll 就不支持这些扩展，但 Troll 不会对其在特定平台上的可移植性或功能提供正式的保修。以下信息提供了扩展的概述以及使用它们的简要示例。

### OpenGL 扩展

OpenGL 是硅图形公司（Silicon Graphics, Inc.，简称 SGI）提供的一种 3D 渲染 API。Qt 可用的所有平台上都提供 OpenGL 或类似的 API，但 OpenGL 在提供 2D 用户界面支持方面的功能非常有限。从历史上看，OpenGL 应用程序通常会包含一些 Motif 或 MFC 代码来实现此目的。Qt 的 OpenGL 扩展起到了相同的作用，允许 Qt 程序员在其应用程序中添加 3D 渲染视图——或者允许 OpenGL 程序员在其渲染应用程序中添加良好的用户界面——具体取决于你当前是在 2D/3D 围墙的哪一边划定领地。

Qt 的 OpenGL 扩展可以与 OpenGL、Mesa、GLX 以及其他一些技术很好地协同工作，并提供了几个有用的示例。与所有扩展一样，你必须显式构建源代码，或者如果你使用该扩展，你将会有一个额外的库需要链接。

该扩展提供了以下类：

- `QGLWidget`——一个易于使用的 Qt 小部件，支持 OpenGL 渲染上下文。
- `QGLContext`——OpenGL 渲染上下文的封装。
- `QGLFormat`——指定渲染视口的显示格式和操作参数。

### 网络支持

虽然 Qt 工具包本身并未提供正式的network协议支持，但目前正在开发一个独立的 Qt 扩展。请查看 Trolltech 网站以了解其可用性。

## 摘要

本章涵盖的主题与先前或后续章节的内容无关，因此拥有独立的一章。

Qt 类定义了大量常量，传统上这些常量会被归类为全局变量或全局常量。由于大多数 Qt 类都继承自 Qt 类，这些类及其子类可以直接使用这些值。

尽管 Trolltech（Trolls）已经减少了工具包中可用的扩展数量，转而倾向于将扩展作为单独的库提供，但他们似乎希望继续维持这一传统一段时间。从 1.X 和 2.0 版本中保留下来的唯一扩展是 OpenGL 控件类。

# 第三部分

## 开发专业的 Qt 应用程序

# 第 7 章

## Qt 开发注意事项

应用程序开发不仅仅是将控件位置摆得恰到好处，或者优雅且富有风格地封装算法或编程概念类。大多数企业级开发项目（至少在客户端方面）是由列出了产品中必须出现的功能特性的市场规格驱动的。该规格通常用于创建原型。在市场人员对无数次的“狗和驴表演”（be thankful that programmers usually don’t have to attend these，谢天谢地程序员通常不需要参加这些）中对着原型发出“哦哦”和“啊啊”的惊叹后，会生成一份修订后的市场规格。

从循环的这个阶段通常有两条路径：要么将详细规格刻在石板上，要么刻在微软 PowerPoint 演示幻灯片集上（我讨厌这些），要么开始创建、测试、审查和修订的重复循环。后一种方法有时被称为“迭代方法”（因其项目经历的大量迭代而得名），通常是最具生产力的。无论如何，你将拥有一套针对最终产品的目标，很可能包括国际分销标准、目标平台限制、尺寸和性能目标，以及除了功能要求之外的所有其他内容。

以下主题试图以与 Qt 相关的方式讨论其中一些话题。

# 国际化

将国际化支持（I18N）添加到新或现有项目中有许多原因。项目可能书面要求支持美式英语和加拿大法语，或者你预见到未来在除本国以外的其他国家进行分销的需求。无论原因如何，Qt 工具包提供了一些国际化机制，其易用性使得无论规格是否要求，实现国际化应用程序都是有意义的，因为它扩大了应用程序的可使用受众。现有的 Qt 应用程序可以相对容易地改装以包含 I18N 支持。

你很可能已经看到过包含嵌入字符串的源代码示例。这些嵌入字符串可以采取几种不同的形式。例如，下面的代码片段演示了将硬编码字符串嵌入应用程序的两种非常常见的方法：

```cpp
/* I’ve actually seen this error message:
#define EMSG0001 "Bad treeout in do_rel_op"

    fprintf( stderr, "%s\n", EMSG0001 );

    QLabel *l = new QLabel( "Enter Password:", this );
```

在应用程序中嵌入字符串的这些方法非常常见。像这样对代码进行国际化的传统方法是繁琐且耗时的。程序员必须添加对（依赖于平台的！）翻译方法的调用，如下面的代码片段所示：
