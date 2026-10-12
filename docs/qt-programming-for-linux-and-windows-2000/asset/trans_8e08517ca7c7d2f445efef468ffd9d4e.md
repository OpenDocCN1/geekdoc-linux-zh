
## 第 6 章

### Qt 命名空间与 Qt 扩展

有几个话题值得讨论，但并不足以占用一整章的篇幅。第一个话题是 `Qt` 类，它提供了一些常用的枚举常量值。第二个话题讨论的是 Trolltech 对 Qt 工具包的扩展，这些扩展已经发展到一定程度，以至于 Trolls 将这些扩展从工具包的第二版中移除了。

### QT 类

提供全局值是一种糟糕的做法，几乎每一个面向对象（OO）程序员都对此不屑一顾。有很多很好的理由支持这一观点。避免使用全局定义的最有说服力的理由是为了避免污染开发命名空间。微软的开发环境就是一个命名空间被污染的典型例子——随着 VC++ 每个新版本的发布，创建一个不与其所包含头文件中某个宏发生冲突的唯一标识符名称变得越来越困难。例如，考虑以下宏定义：

```c
...
#define AlignLeft      0x01
#define AlignRight     0x02
...
```

这些宏定义乍看之下似乎无害，但在编译几乎任何图形工具包（不仅仅是 Qt）的代码时，都会导致有趣的事情发生。创建全局变量、宏和常量值会带来麻烦。即使你分配了不太可能重名的名称，将来仍有可能与他人的代码产生冲突。

解决“全局”常量需求的更好方法是在类中声明它们，然后简单地继承该类。这就是 `Qt` 类所服务的目的。

许多 Qt 小部件和类接受在几乎所有小部件和许多便捷类中通用的常量标志、修饰符和数据值。为了不再进一步污染命名空间，Qt 工具包定义了一个名为 `Qt` 的类，该类的目的是将这些通用值暴露给其派生类对象。由于 `QObject`（以及许多不基于 `QObject` 的类）都继承了 `Qt` 类，因此这些枚举常量可以直接从任何从这些 `Qt` 子类派生的类中访问。当然，显式访问其中一个值并没有错；例如：

```cpp
QColor r( Qt::red );
```

对于 `QObject` 的任何子类或 Qt 的其他子类，直接访问这些值要简单得多，如下所示：

```cpp
QColor r( red );
```

类 `QBrush`、`QCustomMenuItem`、`QEvent`、`QIconViewItem`、`QListViewItem`、`QObject`、`QPalette`、`QPen`、`QPixmap`、`QStyleSheet`、`QToolTip` 和 `QWhatsThis` 都继承了 `Qt` 类，因此这些常量可以直接被这些子类及其后续子类的方法访问。

表 6.1 列出了数据类型和常量名对。

**表 6.1 数据类型和常量名对**

| 值类型 | 常量 |
| :--- | :--- |
| ButtonState | NoButton, LeftButton, RightButton, MidButton, MouseButtonMask, ShiftButton, ControlButton, AltButton, KeyButtonMask |
| Orientation | Horizontal, Vertical |
| AlignementFlags | AlignLeft, AlignRight, AlignHCenter, AlignTop, AlignBottom, AlignVCenter, AlignCenter = AlignHCenter \| AlignVCenter, SingleLine, DontClip, ExpandTabs, ShowPrefix, WordBreak, DontPrint |
| WidgetState | WState_Created, WState_Disabled, WState_Visible, WState_ForcedHide, WState_OwnCursor, WState_MouseTracking, WState_CompressKeys, WState_BlockUpdates, WState_InPaintEvent, WState_Reparented, WState_Configuring, WState_Resizable, WState_AutoMask, WState_Polished, WState_IND, WState_Modal, WState_Reserved, WState_Reserved2, WState_Reserved3, WState_Reserved4, WState_TranslateBackground, WState_ForceDisabled, WState_Exposed |
| WidgetFlags | WType_TopLevel, WType_Modal, WType_Popup, WType_Desktop, WType_Mask, WType_Customize, WStyle_NormalBorder, WStyle_DialogBorder, WStyle_NoBorder, WStyle_Title, WStyle_SystemMenu, WStyle_Minimize, WStyle_Maximize, WStyle_MinMax = WStyle_Minimize \| WStyle_Maximize, WStyle_Tool, WStyle_StayOnTop, WStyle_Dialog, WStyle_ContextHelp, WStyle_NoBorderEx, WStyle_Mask, WDesktopIgnoreClose, WPaintDesktop, WPaintUnclipped, WPaintCliver, WResizeNoErase, WMouseEventMask, WMonitorTweaks, WRepaintNoErase, WM_X11ByPassWM |
| ImageConversionFlags | ColorMode_Mask, AutoColor, ColorOnly, MonoOnly, AlphaDither_Mask, ThresholdAlphaDither, OrderedAlphaDither, DitherMode_Mask, NoAlpha, Dither_Mask, ThresholdAlphaDither, OrderedAlphaDither, NoAlpha |
| BMode | TransparentMode, OpaqueMode |
| PaintUnit | PixelUnit, LoMetricUnit, HiMetricUnit, LogNishUnit, HiEngNishUnit, TwipUnit |
| GUIStyle | MacStyle, WindowsStyle, Win32Style, PMStyle, MotifStyle |
| Modifier | SHIFT_CTRL_ALT, MODIFIER_MASK, UNICODE_ACCEL, ASCII_ACCEL = UNICODE_ACCEL |
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

- **QGLWidget**——一个易于使用的 Qt 小部件，支持 OpenGL 渲染上下文。
- **QGLContext**——OpenGL 渲染上下文的封装。
- **QGLFormat**——指定渲染视口的显示格式和操作参数。

