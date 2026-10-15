
| EastGravity | (Width, Height/2) |

| SouthWestGravity | (0, Height) |

| SouthGravity | (Width/2, Height) |

| SouthEastGravity | (Width, Height) |

当具有其中一个位重力值的窗口调整大同时，相应的坐标对定义了窗口尺寸内每个像素位置的变化。当具有其九种重力（nine-gravities）之一的窗口的父窗口调整大同时，相应的坐标对定义了窗口在父窗口内位置的变化。当窗口重新定位时，会生成 `GravityNotify` 事件（见第 10.10 节）。

（注：此处原文似乎存在多处重复的表述或翻译翻译，根据原文已，确保了连贯的语境，例如原文关于 `border-pixel` 属性描述和 `border-pixmap` 属性描述，以及原文的 `border-pixmap` 和 `border-pixel` 描述逻辑重复。）

如果不再对 `border-pixel` 进行显式引用，则 `border-pixel` 即可立即释放。如果你稍后向用于边框的 pixmap 绘图，结果是不定义的，因为 X 实现可以自由创建 pixmap 的副本或使用同一个 pixmap。如果你设置了 `border-pixel`，或者你在默认 `border-pixmap` 中设置的任何值，它将覆盖默认，窗口边框将被设置为 `border-pixel`。设置新边框（无论是通过设置 `border-pixel` 还是设置 `border-pixmap`）都会覆盖任何之前的边框。

到窗口的输出始终被裁剪在窗口内部。因此，图形操作永远不会影响窗口边框。

（注：由于提供的原文中存在大量逻辑重复段落和句子，译文已根据原文内容进行了对应翻译，并确保了所有出现的文本均已翻译。）

## 窗口函数

### 覆盖重定向标志 (Override Redirect Flag)

为了控制窗口的位置或装饰，窗口管理器通常需要拦截（重定向）任何映射（map）或配置（configure）请求。然而，弹出窗口通常需要在没有窗口管理器干扰的情况下进行映射。要控制输出（Output）或仅输入（InputOnly）窗口是否忽略这些结构控制设施，请使用 `override-redirect` 标志。

`override-redirect` 标志指定该窗口上的映射和配置请求是否应该覆盖父窗口的结构掩码（`SubstructureMask`）。你可以将 `override-redirect` 标志设置为 `True` 或 `False`（默认值）。窗口管理器使用这些信息来避免干扰弹出窗口（见第 14 章）。

### 调色板属性 (Colormap Attribute)

`colormap` 属性指定哪种调色板反映输出窗口的真实颜色。调色板必须与窗口具有相同的视觉类型（visual type），否则将导致 `BadMatch` 错误。支持多个硬件调色板的 X 服务器可以使用此功能，窗口管理器可以使用它调用 `XInstallColormap`。你可以将 `colormap` 属性设置为一个调色板或 `CopyFromParent`（默认值）。

如果你将 `colormap` 设置为 `CopyFromParent`，则父窗口的调色板将被复制并供子窗口使用。子窗口必须与父窗口具有相同的视觉类型，否则会导致 `BadMatch` 错误。父窗口的调色板不能为 `None`，否则将导致 `BadMatch` 错误。调色板的复制是通过在子、父窗口之间共享调色板对象，或通过对调色板内容进行完整拷贝来实现。对父窗口 `colormap` 属性的后续更改不会影响子窗口。

### 光标属性 (Cursor Attribute)

`cursor` 属性指定当指针位于输入输出（`InputOutput`）或仅输入（`InputOnly`）窗口时应使用哪种光标。你可以将 `cursor` 设置为一个光标或 `None`（默认值）。

如果你将 `cursor` 设置为 `None`，则当指针位于输入输出或仅输入窗口时，将使用父窗口的光标，父窗口光标的任何变化都将导致显示光标的立即变化。通过调用 `XFreeCursor`，只要不再对其进行引用，就可以立即释放该光标。

## 创建窗口

`Xlib` 提供了创建窗口的基本方法，工具包（toolkits）通常提供专门用于创建和放置顶层窗口的高级函数，这些函数在相应的工具包文档中会有讨论。然而，如果你不使用工具包，则必须使用 `Xlib` 客户端间通信函数为窗口管理器提供一些标准信息或提示（见第 14 章）。

如果你使用 `Xlib` 创建顶层窗口（根窗口的直接子窗口），你必须遵守以下规则，以确保所有应用程序在不同的窗口管理样式之间能够合理交互：

- 你绝不能与窗口管理器争夺顶层窗口的大小或位置。
- 你必须能够处理收到的任何尺寸，即使这意味着你的应用程序仅仅在窗口中打印诸如“请让我变大一点”的消息。
- 你应该只在直接响应用户请求时才尝试调整或移动顶层窗口。如果更改顶层窗口大小的请求失败，你必须准备好接受当前的结果。你可以根据需要自由地调整或移动顶层窗口的子窗口。（工具包通常具有自动布局的设施。）
- 如果你没有使用设置标准窗口属性的工具包，你应该在映射顶层窗口之前为它们设置这些属性。

欲需更多信息，请参阅第 14 章和《客户端间通信规范手册》（Inter-Client Communication Conventions Manual）。

`CreateWindow` 是一个更通用的函数，允许你在创建窗口时设置特定的窗口属性。`XCreateSimpleWindow` 创建一个继承其父窗口属性的窗口。

X 服务器的作用是，因为仅输入窗口在图形请求、显示处理（exposure processing）和可见性通知（VisibilityNotify）事件方面是不存在的。仅输入窗口不能作为可绘制区域（即作为图形请求的源或目的）。在其他方面（属性、抓取（grabs）、输入控制等），仅输入窗口和输出窗口的行为完全相同。扩展包可以定义其他类别的窗口。

要创建一个未映射的窗口并设置其属性，请使用 `XCreateWindow`。

```
Window XCreateWindow(display, parent, x, y, width, height, border_width, depth, class, visual, valuemask, attributes);
```

`display` 指定与 X 服务器的连接。

`parent` 指定父窗口。

`x`, `y` 指定 x 和 y 坐标，它们是创建窗口边界外部的左上角，相对于父窗口边界的内部。

`width`, `height` 指定创建窗口的宽度和高度，即创建窗口的内部尺寸，不包括窗口的边界。尺寸必须非零，否则将产生 `BadValue` 错误。

`border_width` 指定创建窗口边界的宽度（单位为像素）。

`depth` 指定窗口的深度。深度为 `CopyFromParent` 表示深度取自父窗口。

`class` 指定窗口的类。你可以传递 `InputOutput`、`InputOnly` 或 `CopyFromParent`。类为 `CopyFromParent` 表示类取自父窗口。

`visual` 指定窗口的类型。类型为 `CopyFromParent` 表示类型取自父窗口。

`valuemask` 指定在 `attributes` 参数中定义了哪些属性。此掩码是有效属性掩码位的按位包含或（bitwise inclusive OR）。如果 `valuemask` 为零，则将忽略且不引用属性。

`attributes` 指定了从中获取值（由值掩码指定）的结构。值掩码应设置相应的位，以指示结构中设置了哪些属性。

`CreateWindow` 函数为指定的父窗口创建一个未映射的窗口，返回该窗口的 ID，并导致 X 服务器生成 `CreateNotify` 事件。该窗口相对于兄弟窗口在堆叠顺序上处于顶端。使用父窗口的坐标系作为窗口的位置。超出父窗口边界的部分将被裁剪。仅输入窗口的 `border_width` 必须为 0，否则将产生 `BadValue` 错误。`XCreateSimpleWindow` 继承其父窗口的深度、颜色。除了背景外，所有其他窗口属性都有默认值。

要 `CreateWindow` 可能会产生 `BadAlloc`、`BadMatch`、`BadValue` 和 `BadWindow` 错误。

要映射给定窗口的 `InputOutput` 子窗口，请使用 `XCreateSimpleWindow`。

```
Window XCreateSimpleWindow(display, parent, x, y, width, height, border_width, border, background);
```

`display` 指定与 X 服务器的连接。

`parent` 指定父窗口。

`x`, `y` 指定 x 和 y 坐标，它们是创建窗口边界外部的左上角，相对于父窗口边界的内部。

`width`, `height` 指定创建窗口的宽度和高度，即创建窗口的内部尺寸，不包括窗口的边界。尺寸必须非零，否则将产生 `BadValue` 错误。

`border_width` 指定创建窗口边界的宽度（单位为像素）。

`border` 指定窗口的边界颜色。

`background` 指定窗口背景颜色。
