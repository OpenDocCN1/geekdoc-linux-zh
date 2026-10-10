
`GtkrolledWindow` provides scrollbars for its child.

## GtkBox

### 库
`GTK+`

### 头文件
`gtk/box.h`

### 描述
`GtkBox` 是一个容器，允许按水平或垂直方向排列子部件。

## GtkHBox

### 库
`GTK+`

### 头文件
`gtk/hbox.h`

### 描述
`GtkHBox` 是一个 `GtkBox`，从左到右排列控件。

## GtkVBox

### 库
`GTK+`

### 头文件
`gtk/vbox.h`

### 描述
`GtkVBox` 是一个 `GtkBox`，从上到下排列控件。

## GnomeAppBar

### 库
`Gnome`

### 头文件
`libgnome/appbar.h`

### 描述
`GnomeAppBar` 是一个标题栏，它包含一个标题、一个图标和一个用于关闭窗口的按钮。

## GMenu

### 库
`GTK`

### 头文件
`gtk/gtkmenu.h`

## GtkCombo

### 库
`GTK+`

### 头文件
`gtk/combo.h`

### 描述
`GtkCombo` 是一个下拉列表，它允许用户从一组预定义的选项中选择。

## GnomeEntry

### 库
`Gnome`

### 头文件
`libgnome/entry.h`

### 描述
`GnomeEntry` 是一个文本框，允许用户输入文本。

## GnomeFileEntry

### 库
`Gnome`

### 头文件
`libgnome/fileentry.h`

### 描述
`GnomeFileEntry` 是一个带有浏览按钮的文本框，允许用户选择文件。

## GnomeNumberEntry

### 库
`Gnome`

### 头文件
`libgnome/nentry.h`

### 描述
`GnomeNumberEntry` 是一个文本框，允许用户输入数字。

## GnomeProcBar

### 库
`Gnome`

### 头文件
`libgnome/procbar.h`

### 描述
`GnomeProcBar` 是一个进度条，用于显示长时间任务的完成情况。

## GnomeDateEdit

### 库
`Gnome`

### 头文件
`libgnome/dateedit.h`

### 描述
`GnomeDateEdit` 是一个允许用户选择日期的控件。

# 头文件

## 头文件
`libgnomeui/gnome-icon-entry.h`

## 描述
`GnomeIconEntry` 类似于 `GnomeColorPicker` 和 `GnomeFontPicker`。它是一个显示当前选中图标的按钮；当点击该按钮时，会弹出一个图标浏览器对话框允许用户设置新图标。该小部件曾有一个用于输入图标文件名的文本输入框，因此它被称为 `GnomeIconEntry` 而不是 `GnomeIconPicker`。

## GnomeIconSelection

### 库
`Gnome`

### 头文件
`libgnomeui/gnome-icon-sel.h`

### 描述
`GnomeIconSelection` 用于浏览图标文件；它被 `GnomeIconEntry` 使用，但也可以直接使用。

# 第 14 章. GTK+/Gnome 对象层级结构

![](img/f08b98c3d9ba764fd120a058661d79d5_325_0.png)

图 14-17. `GnomeIconSelection`

## GnomeLess

### 库
`Gnome`

### 头文件
`libgnomeui/gnome-less.h`

### 描述
`GnomeLess` 是 `GtkText` 的一个简单扩展，可以从文件或文件描述符加载文本并显示。避免使用这个小部件可能是一个好主意；因为它并不实用，它可能会在 `Gnome` 未来的版本中消失。

## GnomePaperSelector

### 库
`Gnome`

### 头文件
`libgnome-ui/gnome-paper-selector.h`

### 描述
`GnomePaperSelector` 是另一个值得避免的小部件；在 1.0 版本中，它是严格的实验性。它允许用户选择打印时的纸张尺寸。

## GnomePixmapEntry

### 库
`Gnome`

### 头文件
`libgnome-ui/gnome-pixmap-entry.h`

### 描述
`GnomePixmapEntry` 的目的与 `GnomeIconEntry` 基本相同；它允许用户选择位图映射（pixmap）。你可能倾向于选择其中一个另一个的唯一理由是 `GnomeIconEntry` 会将图像缩放到标准的 `Gnome` 图标尺寸。

## GnomeSpell

### 库
`Gnome`

### 头文件
`libgnome-ui/gnome-spell.h`

### 描述
`GnomeSpell` 是一个拼写检查接口；它在内部使用了 `ispell` 程序。该小部件应该被认为是实验性的，并在生产代码中避免使用。

## GtkColorSelection

### 库
`GTK+`

### 头文件
`gtk/gtkcolorsel.h`

### 描述
`GtkColorSelection` 允许用户使用色轮或滑动条指定颜色。它构成了 `GtkColorSelectionDialog` 内容（图 14-1）。

## GtkGammaCurve

### 库
`GTK+`

### 头文件
`gtk/gtkgamma.h`

### 描述
`GtkGammaCurve` 允许用户编辑曲线；它是一个非常专门的小部件，用于 `Gimp` 中。很少有应用程序会用到它。

![](img/f08b98c3d9ba764fd120a058661d79d5_327_0.png)

图 14-18. `GtkGammaCurve`

## GtkButtonBox

### 库
`GTK+`

### 头文件
`gtk/gtkbbox.h`

### 描述
`GtkButtonBox` 是一种特殊的 `GtkBox`，设计用于存储对话框的按钮。它具有水平和垂直变体。`GnomeDialog` 会为你创建一个按钮框，在用 `Gnome` 编程时，无需直接使用这个小部件。

## GtkHButtonBox

### 库
`GTK+`

### 头文件
`gtk/gtkhbox.h`

### 描述
`GtkHButtonBox` 是 `GtkButtonBox` 的水平变体。

## GtkVButtonBox

### 库
`GTK+`

### 头文件
`gtk/gtk.h`

### 描述
`GtkVButtonBox` 是 `GtkButtonBox` 的垂直变体。

## GtkLayout

### 库
`GTK+`

### 头文件
`gtk/gtklayout.h`

### 描述
`GtkLayout` 创建了一个无限尺寸容器的幻象。因为 X 窗口的尺寸限制为 32,768 像素 (`2^15`)，大多数小部件也有 32,768 像素的尺寸限制（且子部件必须定位在父级 X 窗口内）。原始的小部件通过简单的移动其 `GdkWindow` 来滚动。`GtkLayout` 在这方面更为智能。

## GnomeCanvas

### 库
`Gnome`

### 头文件
`libgnomeui/gnome-canvas.h`

### 描述
`GnomeCanvas` 在第 12 章中被广泛讨论。它渲染无闪烁的结构化图形，是自定义显示的理想选择。

![](img/f08b98c3d9ba764fd120a058661d79d5_330_0.png)

图 14-19. `GnomeCanvas`

## GnomeIconList

### 库
`Gnome`

### 头文件
`libgnomeui/gnome-icon-list.h`

### 描述
`GnomeIconList` 用于 `Gnome` 文件管理器。它显示图标及其名称；用户可以通过橡形框框（rubberbanding）选择一组图标。

![](img/f08b98c3d9ba764fd120a058661d79d5_331_0.png)

图 14. `Gnome` 文件管理器，展示了 `GnomeIconList`

## GnomeBand

### 库
`Gnome`

### 头文件
`libgnomeui/gnome-band.h`

### 描述
`GnomeBand` 包含一个 `GnomeBands`。请参阅 `GnomeDock` 详情。

## GnomeDock

### 库
`Gnome`

### 头文件
`libgnomeui/gnome-dock.h`

### 描述
`GnomeDock` 允许使用 Dock 控件。请参阅 `GnomeDock` 详情。

## GtkList

### 库
`GTK+`

### 头文件
`gtk/gtklist.h`

### 描述
`GtkList` 是 `GtkTree` 的垂直变体。因为 X 窗口的尺寸限制为 32,768 像素，大多数小部件也有 32,768 像素的尺寸限制（且子部件必须定位在父级 X 窗口内）。`GtkList` 是水平的，Dock 控件。

![](img/f08b98c3d9ba764fd120a058661d79d5_333_0.png)

图 14-22. `GtkTree`

## Gtkree

### 库
`GTK+`

### 头文件
`gtk/gtctree.h`

### 描述
`Gtkree` 与 `GtkList` 类似，它包含 `DockBands`。`Gtkree` 允许 `DockItems`。

![](img/f08b98c3d9ba764fd120a058661d79d5_334_0.png)

## GtkFixed

### 库
`GTK+`

### 头文件
```
