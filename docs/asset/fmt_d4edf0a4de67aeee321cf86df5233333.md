
## GtkFixed

### 库
`GTK+`

### 头文件
`gtk/notebook.h`

### 描述
`GtkFixed` 是一个允许绝对坐标放置小部件的容器。如果你需要布局，应该考虑使用其他布局。`GtkFixed` 任何小部件都不是自动布局的。

## GtkNotebook

### 库
`GTK+`

### 头文件
`gtk/notebook.h`

### 描述
`GtkNotebook` 小部件呈现了多个页面；它包含标签。`GtkNotebook` 的标签位于左、右或底部。`GtkNotebook` 允许在顶部放置标签，这通常是高效的。

## GtkFontSelection

### 库
`GTK+`

### 头文件
`gtk/fontsel.h`

### 描述
`GtkFontSelection` 是一个复合小部件，允许用户从系统字体中选择字体。`GtkSelectionDialog` 包含一个 `GtkFontSelection` 实例。

## GtkPaned

### 库
`GTK+`

### 头文件
`gtk/gtkpaned.h`

### 描述
`GtkPaned` 将区域分为两个用户可缩放的部分。它具有水平和垂直变体。

![](img/f08b98c3d9ba764fd120a058661d79d5_335_0.png)

图 14-23. `GtkNotebook`

## GtkHPaned

### 库
`GTK+`

### 头文件
`gtk/gtkhpared.h`

### 描述
`GtkHPaned` 是 `GtkPaned` 的水平变体；它允许用户划分 `GtkHPaned` 两个子部件之间的水平空间。

## GtkVPaned

### 库
`GTK+`

### 头文件
`gtk/gtkvaned.h`

### 描述
`GtkVPaned` 是 `GtkPaned` 的垂直变体；它允许用户划分 `GtkVPaned` 两个子部件之间的垂直空间。

![](img/f08b98c3d9ba764fd120a058661d79d5_336_0.png)

图 14-24. 水平和垂直 `GtkPaned` 小部件

(注：由于原文存在部分重复和错乱，翻译已按逻辑进行对应翻译)

## GtkMenuShell

### 库
`GTK+`

### 头文件
`gtk/gtkmmenushell.h`

### 描述
`GtkMenuShell` 是用于包含 `GtkMenuItems` 控件的抽象基类。它的两个子类是 `GtkMenu` 和 `GtkMenuBar`。

## GtkMenuBar

### 库
`GTK+`

### 头文件
`gtk/gtkmubar.h`

### 描述
`GtkMenuBar` 是一个菜单栏。它包含一个或多个菜单项；通常，每个菜单项都会有一个子菜单（即包含更多菜单项的 `GtkMenu`）。例如，菜单栏可能有一个名为“文件”的菜单项，其子菜单包含“打开”和“退出”菜单项。

## GtkMenu

### 库
`GTK+`

### 头文件
`gtk/gtkmenu.h`

### 描述
`GtkMenu` 包含菜单项。`GtkMenu` 的独特之处在于，它不应该由程序员显示（通过 `gtk_widget_show()`）；菜单是在响应用户操作时被弹出的。

## GtkPacker

### 库
`GTK+`

### 头文件
`gtk/gtkpacker.h`

### 描述
`GtkPacker` 是受 Tk 工具包启发的布局容器。如果你熟悉该工具包，可能会发现它比标准的 `GTK+` 布局容器更容易使用。

## GtkSocket

### 库
`GTK+`

### 头文件
`gtk/gtksocket.h`

### 描述
`GtkSocket` 是一个应用程序中的“洞”，允许来自第二个应用程序的 `GtkPlug` 嵌入其中。

## GtkTable

### 库
`GTK+`

### 头文件
`gtk/gtktable.h`

### 描述
第 3 章中的 `GtkTable` 章节详细描述了 `GtkTable`。它是最重要的 `GTK+` 布局控件之一。

## GtkTed

### 库
`Gnome`

### 头文件
`libgnomeui/gtk-ted.h`

### 描述
`GtkTed` 是 `Gnome` 早期的遗留；“ted”代表“表格编辑器”。它是一种原始的 GUI 构建器。目前至少有两个先进的项目用于编写良好的 GUI 构建器（Glade 和 GLE），因此这个控件应该被忽略，并在 `libgnomeui` 的未来版本中消失。

## GtkToolbar

### 库
`GTK+`

### 头文件
`gtk/gtktoolbar.h`

### 描述
这里没什么意外：`GtkToolbar` 是一个工具栏控件。`Gnome` 应用通常会使用 `Gnome` 辅助函数而不是直接创建工具栏，正如第 6 节所述。

## GtkTree

### 库
`GTK+`

### 头文件
`gtk/gtktree.h`

### 描述
`GtkTree` 之于 `GtkTree` 之于 `GtkList`。也就是说，`GtkTree` 比 `GtkTree` 更灵活——树项可以包含任何控件——但它也比 `GtkTree` 慢一点，且只能持有有限数量的项目。最大项目数量取决于行的高度；总行高必须适应 `GdkWindow` 内部，即 32x768 像素。

![](img/f08b98c3d9ba764fd120a058661d79d5_341_0.png)

图 14-25. `GtkTree`

## GnomeAnimator

### 库
`Gnome`

### 头文件
`libgnomeui/gnome-animator.h`

### 描述
`GnomeAnimator` 显示一系列图像以创建动画。它有“循环模式”和“播放一次”模式。对于 `Gnome` 1.0，`GnomeAnimator` API 被标记为“不成熟”，并在未来版本中发生不兼容的更改；这是一个实验性控件。

## GnomePixmap

### 库
`Gnome`

### 头文件
`libgnomeui/gnome-pixmap.h`

### 描述
应该优先使用 `GnomePixmap` 而不是 `GtkPixmap`，尽管目的相同。`GnomePixmap` 在视觉处理上更智能。它还可以使用 Imlib 加载许多不同格式的图像，因此更方便。

## GnomeStock

### 库
`Gnome`

### 头文件
`libgnomeui/gnome-stock.h`

### 描述
`GnomeStock` 是封装 `GnomePixmap` 的容器；它会自动创建 pixmap 的“不敏感”和“聚焦”副本以反映控件状态。它可以被设置为 `GnomeStock` pixmap 宏之一，例如 `GNOME_STOCK_PIXMAP_CUT`（一个小剪刀图标）等。你还可以在运行时注册新的库存 pixmap 映射来指定你的应用程序。`Gnome` 在使用 `GnomeUIInfo` 模板创建菜单和工具栏时内部会使用此控件（详见第 6 节中带有 `GnomeUIInfo` 的菜单和工具栏章节）。

## GtkMisc

### 库
`GTK+`

### 头文件
`gtk+gtmisc.h`

### 描述
描述性命名（或填充）`GtkMisc` 抽象基类允许你设置其子类的“对齐”。对齐是一个 0.0 到 1.0 之间的浮点数，其中 0.0 是左对齐，0.5 是居中，1.0 是右对齐。只有当 `GtkMisc` 接收到的尺寸分配大于其请求时，对齐才重要；对齐使控件在实际边界框内的自然边界框匹配。填充是添加到控件尺寸请求的像素数。控件将留出这些像素为空白。

未派生自 `GtkMisc` 的控件可以通过放置在 `GtkMisc` 中以相同的方式变为“可对齐”。

## GtkLabel

### 库
`GTK+`

### 头文件
`gtk/gtklabel.h`

### 描述
`GtkLabel` 显示字符串。它可以处理换行符。对齐定义了文本的位置。左对齐意味着文本从左侧开始，右对齐意味着在右侧结束，居中意味着在中间。只有当标签接收到的尺寸分配大于其尺寸请求时，对齐才重要。

## GtkAccel

### 库
`GTK+`

### 头文件
`gtk/gtkacc.h`

### 描述
`GtkAccel` 用于处理键盘快捷键。它显示一个标签。

## GtkClock

### 库
`Gnome`

### 头文件
`libgnomeui/gtk-clock.h`

### 描述
`GtkClock` 显示时间。它可以定期更新。

## GtkTips

### 库
`GTK+`

### 头文件
`gtk/gtips.h`

### 描述
`GtkTips` 是一个管理工具提示的容器。它在鼠标移动到控件上时显示出一个弹窗。

## GtkArrow

### 库
`GTK+`

### 头文件
`gtk/gtkarrow.h`

### 描述
`GtkArrow` 显示箭头。它是一个简单的绘制区域扩展。

## GtkImage

### 库
`GTK+`

### 头文件
`gtk/gtkimage.h`

### 描述
`GtkImage` 显示图像。它可以用于显示静态图形。

## GtkPixmap

### 库
`GTK+`

### 头文件
`gtk/gtkpixmap.h`

### 描述
`GtkPixmap` 显示 `GdkPixmap`。如果你正在使用 `Gnome`，出于上述原因优先使用 `GnomePixmap`。

## GtkCalendar

### 库
`GTK+`

### 头文件
`gtk/calendar.h`

### 描述
`GtkCalendar` 显示日历页。它允许用户选择日期。`GnomeEdit` 在弹出菜单中使用 `GtkCalendar`。

## GtkDrawingArea

### 库
`GTK+`

### 头文件
`gtk/drawingarea.h`

### 描述
`Gtkdrawingarea` 是 `GdkWindow` 的一个更薄的封装；它为你提供了一个空白区域进行绘图。通常，你会连接到它的“configure_event”信号以捕获区域的变化，并在“expose_event”处理程序中进行绘制。为了消除闪烁，你可能会保持一个与绘制区域等大的 `GdkPixmap` 并向 pixmap 绘图；在你的“expose_event”处理程序中，只需将从 pixmap 暴露区域复制到绘制区域即可。

![](img/f08b98c3d9ba764fd120a058661d79d5_348_0.png)

图 14-27. `GtkDial` 控件

## GtkEditable

### 库
`GTK+`

### 头文件
```
