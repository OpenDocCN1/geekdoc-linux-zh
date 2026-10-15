
```
/*值 */
typedef struct {
    int x, y;
    int width, height;
    int border_width;
    Window sibling;
    int stack_mode;
} XWindowChanges;
```

`x` 和 `y` 成员用于设置窗口的 `x` 和 `y` 坐标，相对于父原点，表示窗口左上角的位置。`width` 和 `height` 成员用于设置窗口内部大小，不包括边框，且必须非零，否则将返回 `BadValue` 错误。配置根窗口的操作无效。

`border_width` 成员用于以像素设置边框宽度。注意，设置边框宽度会保持窗口左上角的固定，但会移动窗口原点的绝对位置。如果你尝试设置输入窗口（`InputWindow`）的边框属性，会导致 `BadMatch` 错误。

`sibling` 成员用于设置堆叠操作的兄弟窗口。`stack_mode` 成员用于设置如何重新堆叠窗口，可以设置为 `Above`、`Below`、`TopLeft`、`BottomLeft` 或 `Opposite`。

如果窗口的 `override-redirect` 标志为 `False` 且其他客户端在父窗口上选择了 `SubstructureRedirectMask`，则 X 服务器会生成 `ConfigureRequest`，且不进行后续处理。如果其他客户端在窗口上选择了 `ResizeRedirectMask` 且正在更改窗口内部宽度或高度，则会生成 `Resize` 事件，并使用当前的内部宽度和高度。注意窗口的覆盖重定向标志对 `ResizeRedirectMask` 无效，且父窗口上的 `SubstructureRedirectMask` 优先于窗口上的 `ResizeRedirectMask`。

当窗口几何形状按指定更改时，窗口将在兄弟窗口之间重新堆叠，如果窗口状态发生变化，则会生成 `ConfigureNotify` 事件。

## 窗口函数

实际上发生了变化。`GravityNotify` 事件在 `ConfigureNotify` 事件之后生成。如果窗口的内部宽度或高度实际上发生了变化，窗口的子窗口将按照规定受到影响。

如果窗口的大小实际上发生了变化，窗口的子窗口将根据它们的重力（gravity）移动。根据窗口的位重力（bit gravity），窗口的内容也可能被[第3.2.3节]移动。

如果窗口的区域之前被遮挡但现在不再被遮挡，则会对这些以前被遮挡的窗口进行暴露处理，包括窗口本身及其下级（inferiors）。由于宽度或高度增加，将对窗口的任何新区域以及窗口内容丢失的区域进行暴露处理。

重堆叠检查（具体而言，`Bottom`、`Top` 和 `Opposite` 的计算）是相对于窗口最终尺寸和位置（由区域的其他参数控制）进行的，而不是相对于其初始位置。如果在未指定栈模式（stack mode）的情况下指定兄弟窗口（`sibling`），将导致 `BadMatch` 错误。

如果指定了兄弟窗口和栈模式，窗口将按如下方式进行重堆叠：

- `Above`（上方）：窗口置于兄弟窗口之上。
- `Below`（下方）：窗口置于兄弟窗口正下方。
- `Top`（顶部）：如果兄弟窗口遮挡了窗口，则窗口置于栈顶部。
- `Bottom`（底部）：如果窗口遮挡了兄弟窗口，则窗口置于栈底部。
- `Opposite`（对侧）：如果兄弟窗口遮挡了窗口，则窗口置于栈顶部。如果窗口遮挡了兄弟窗口，则窗口置于栈底部。

如果指定了 `stack_mode` 但未指定兄弟窗口，窗口将按如下方式进行重堆叠：

- `Above`（上方）：窗口置于栈顶部。
- `Below`（下方）：窗口置于栈底部。
- `Top`（顶部）：如果任何兄弟窗口遮挡了窗口，则窗口置于栈顶部。
- `Bottom`（底部）：如果窗口遮挡了任何兄弟窗口，则窗口置于栈底部。
- `Opposite`（对侧）：如果任何兄弟窗口遮挡了窗口，则窗口置于栈顶部。如果窗口遮挡了任何兄弟窗口，则窗口置于栈底部。

尝试配置根窗口（root window）没有任何效果。

要配置窗口的大小、位置、堆叠顺序或边框，请使用 `ConfigureWindow(display, w, value_mask, values)`：

- `display`：指定与 X 服务器的连接。
- `w`：指定要重新配置的窗口。
- `value_mask`：指定要使用 `values` 结构体中的信息设置的值。此掩码是有效配置窗口位的按位包含或结果。
- `values`：指定 `XWindowChanges` 结构体。

`XConfigureWindow` 函数使用 `XWindowChanges` 结构体中指定的值来重新配置窗口的大小、位置、边框以及堆叠顺序。未指定的值将取自窗口现有的几何结构。

如果在未指定栈模式的情况下指定兄弟窗口，或者窗口本身就是兄弟窗口，将发生 `BadMatch` 错误。注意，`Bottom`、`Top` 和 `Opposite` 的计算是相对于窗口的最终几何结构（由传递给 `XConfigureWindow` 的其他参数控制），而不是其初始几何结构。窗口的任何存储内容、其下级以及其他新可见区域都将被丢弃或更改以反映当前屏幕内容（取决于实现方式）。

`XConfigureWindow` 可能产生 `BadMatch`、`BadValue` 和 `BadWindow` 错误。

要在不改变窗口大小的情况下移动窗口，请使用 `XMoveWindow`。

```
XMoveWindow(display, w, x, y);
```

- `display`：指定与 X 服务器的连接。
- `w`：指定要移动的窗口。
- `x`：指定 `x` 和 `y` 坐标，定义窗口边框左上角像素（或无边框时的窗口本身）的位置。

`XMoveWindow` 函数将指定的窗口移动到指定的 `x` 和 `y` 坐标，但不会改变窗口的大小、提升（raise）窗口或改变窗口的映射（mapping）状态。移动已映射的窗口可能会或可能不会丢失窗口内容，这取决于窗口是否被子窗口遮挡以及是否存在备份存储（backing store）。如果窗口内容丢失，X 服务器将生成遮挡事件。已映射的窗口会在任何被强制遮挡的窗口上生成 `Expose` 事件。

如果窗口的 `override-redirect` 标志为 `False`，且另一个客户端在父窗口上选择了 `SubstructureMask`，则 X 服务器将生成一个 `ConfigureRequest` 事件，且不进行任何进一步处理。否则，将移动窗口。

`XMoveWindow` 可能产生 `BadWindow` 错误。

要在不改变左上角坐标的情况下更改窗口大小，请使用 `XResizeWindow`。

```
XResizeWindow(display, w, width, height);
```

- `display`：指定与 X 服务器的连接。
- `w`：指定窗口。
- `width`：指定宽度和高度，它们是调用完成后窗口的内部尺寸。

`XResizeWindow` 函数更改指定窗口的内部尺寸，不包括边框。此函数不会更改窗口的左上角坐标，也不会重堆叠窗口。更改已映射窗口的大小可能会丢失其内容并生成 `Expose` 事件。如果已映射的窗口较小，更改其大小会在该映射窗口以前被遮挡的窗口上生成 `Expose`。

如果窗口的 `override-redirect` 标志为 `False`，且另一个客户端在父窗口上选择了 `SubstructureMask`，则 X 服务器将生成一个 `ConfigureRequest` 事件，且不进行任何进一步处理。如果宽度或高度任为零，将发生 `BadValue` 错误。

`XResizeWindow` 可能产生 `BadValue` 和 `BadWindow` 错误。

要更改大小和位置，请使用 `XMoveWindow`。

```
XMoveWindow(display, w, x, y, width, height);
```

- `display`：指定与 X 服务器的连接。
- `w`：指定窗口。
- `x`：指定 `x` 和 `y` 坐标，定义窗口边框左上角像素（或无边框时的窗口本身）的位置。
- `width`、`height`：指定宽度和高度，即调用完成后窗口的内部尺寸。

`XMoveWindow` 函数将指定的窗口移动到指定的 `x` 和 `y` 坐标，但不会更改窗口的大小、提升窗口或改变窗口的映射状态。移动已映射的窗口可能会或可能不会丢失窗口内容，取决于窗口是否被子窗口遮挡以及是否存在备份存储。如果窗口内容丢失，X 服务器将生成遮挡事件。已映射的窗口会在任何被强制遮挡的窗口上生成 `Expose` 事件。

如果窗口的 `override-redirect` 标志为 `False`，且另一个客户端在父窗口上选择了 `SubstructureMask`，则 X 服务器将生成一个 `ConfigureRequest` 事件，且不进行任何进一步处理。否则，将移动窗口。

`XMoveWindow` 可能产生 `BadWindow` 错误。

要在不改变左上角坐标的情况下更改窗口大小，请使用 `XResizeWindow`。

```
XResizeWindow(display, w, width, height);
```

- `display`：指定与 X 服务器的连接。
- `w`：指定窗口。
- `width`、`height`：指定宽度和高度，它们是调用完成后窗口的内部尺寸。
