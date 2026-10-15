
```c
/*
 * expose_event
 * 使用 Gtkpixmap 重绘屏幕
 */
static int expose_event(GtkWidget *widget, GdkEventExpose *event)
{
    /* 直接覆盖。 -- */
    gdk_draw_pixmap(widget->window,
        widget->style->fg_gc[GTK_WIDGET_STATE (widget)],
        g->pixmap,
        event->area.x, event->area.y,
        event->area.width, event->area.height);

    return FALSE;
}

/*
 * quit
 * 退出应用程序
 */
void quit ()
{
    gtk_exit (0);
}

/* CreateDrawingArea
 * 创建绘图区域小部件并返回它。
 */
GtkWidget *CreateDrawingArea()
{
    /* 创建绘图区域 -- ... */
    drawing_area = gtk_drawing_area_new ();

    /* 给它一个良好的尺寸 -- ... */
    gtk_drawing_area_size(GTK_DRAWING_AREA (drawing_area), 200, 200);

    /* 让它可见 -- ... */
    gtk_widget_show (drawing_area);

    /* --- 我们需要 expose_event 和 configure_event --- */
    gdk_signal_connect(GTK_OBJECT (drawing_area), "expose_event",
      (GtkSignalFunc) expose_event, NULL);
    gtk_signal_connect(GTK_OBJECT(drawing_area), "configure_event",
      (GtkSignalFunc) configure_event, NULL);

    /* --- 每 2 秒调用一次函数。 --- */
    gdk_timeout_add (2000, UpdateAndRepaint, drawing_area);

    /* ---返回 widget 以置放在屏幕上。 --- */
    return (drawing_area);
}
```

## 总结

将 GDK 与绘图区域小部件结合可以让你创建涉及图形的复杂应用程序。GDK 提供了在绘图区域中绘制简单形状的程序。在绘图区域中使用双缓冲可以消除应用程序中的闪烁，但需要一些额外的工作。显示图形信息的应用程序应该始终使用双缓冲来尝试消除闪烁。

## 11 样式、颜色、字体、光标和引用

样式通过颜色和字体影响小部件的绘制方式。每个样式由若干种颜色和一个字体组成。样式是 GTK+ 的一部分，但颜色和字体属于图形绘制工具包（GDK）。虽然颜色也属于 SDK 的一部分，但 GTK+ 拥有一个颜色选择对话框，可以在应用程序中使用，允许用户选择颜色。同样，对于需要字体的应用程序，GTK+ 也有一个字体选择对话框。这些对话框小部件与文件选择对话框类似，为想要让用户选择颜色和字体的开发者提供了一个通用的用户界面。GDK 还提供了将鼠标光标更改为内置光标或自定义光标的能力。引用有助于 GTK+ 跟踪正在被使用的小部件。GTK+ 会释放它认为不再被使用的小部件，而在某些时刻，你可能希望阻止这一操作。

### 样式（颜色和字体）

GTK+ 中的每个小部件都有一个样式，决定了它在屏幕上的绘制方式。基本样式由颜色方案和字体组成。GTK+ 中的应用程序通常共享相同的样式，这就是为什么所有小部件都使用相同的颜色方案和相同的字体。小部件可以拥有自己独特的样式，但为每个小部件提供一个唯一的样式并不一定是个好主意。在页面上使用许多样式来显示小部件会分散对应用程序的注意力，特别是当小部件颜色不同时。最好是将样式限制在几个（或一个）上，并将时间花在应用程序的功能上。

### 第11 章 样式、字体、光标和引用

虽然样式中只定义了一种字体，但样式可以拥有许多种颜色。小部件可以处于几种模式：`NORMAL`、`ACTIVE`、`PRELIGHT`、`SELECTED` 和 `INSENSITIVE`。

- `NORMAL`：对象的正常绘制方式。
- `ACTIVE`：对象处于激活状态——对于按钮来说，`ACTIVE` 状态是按钮被按下的状态。
- `PRELIGHT`：通常意味着鼠标正移动到小部件上。这种颜色提示用户点击该项目。
- `SELECTED`：项目已被选择。
- `INSENSITIVE`：小部件处于不可用（不可选择）。这种模式在微软的术语中称为“禁用”（disabled）。

每种模式都定义了一组颜色来表示小部件所处的模式。你可以通过观察按钮小部件来看到此功能。按钮在 `NORMAL` 模式下是正常的。当鼠标移动到按钮小部件上时，小部件进入 `PRELIGHT` 模式，导致按钮以 `PRELIGHT` 颜色显示。如果按钮被按下，按钮将以小部件的 `ACTIVE` 颜色显示。并不是所有小部件都支持所有模式。

### 颜色

颜色定义为 `GdkColor`。颜色由红、绿、蓝（RGB）值组成，决定了它们对颜色的贡献。

```c
/* 定义红色为--大量的红色，绿色，无蓝色 */
GdkColor color = {0, 0xffff, 0x0000};
```

在创建 `Gdk` 结构后，应使用 `gdk_color_alloc` 函数从系统分配颜色。它尝试用硬件可以支持的颜色进行分配。该函数期望接收一个颜色表（colormap）或颜色，但如果你只使用少数颜色，可以通过传递 `gdk_colormap_get_system` 函数返回的值来使用系统颜色表。分配完成后，可以使用这些颜色创建具有更多（咳）有趣颜色的新样式。

### 使用样式

可以使用 `gtk_widget_get_default_style` 函数获取应用程序的默认样式。直接对该样式进行操作是不良的习惯，但你可以复制一份来进行操作。`gtk_style_copy` 函数会创建一个样式的副本以便进行修改。`GdkStyle` 结构包含一个前景颜色数组（`fg`）、一个背景颜色数组（`bg`）和一个文本颜色数组（`text`），这些共同定义了样式的颜色。要修改按钮使其在黑色背景上显示白色文字，你可以执行以下操作：

```c
/* --- 定义颜色 --- */
GdkColor white = {0, 0xffff, 0xffff, 0xffff};
GdkColor black = {0, 0x0000, 0x0000, 0x0000};
```

```c
/* --- 分配颜色 --- */
gdk_color_alloc (gdk_colormap_get_system (), &white);
gdk_color_alloc (gdk_colormap_get_system (), &black);
```

```c
/* --- 获取默认样式 --- */
defstyle = gtk_widget_get_default_style ();
```

```c
/* --- 为我们复制一份 --- */
style = gtk_style_copy (defstyle);
```

```c
/* --- 修改颜色 --- */
style->fg[NORMAL] = white;
style->text[NORMAL] = white;
style->bg[NORMAL] = black;
```

样式创建后，可以使用它更改任何现有小部件的样式。`gtk_widget_set_style_function` 设置现有小部件的样式。该函数设置传递给 `gtk_widget_set_style_function` 的小部件样式，但如果它是一个容器，则不会设置所有子小部件的样式。函数可以使用 `gtk_container_foreach` 如下所示更改小部件及其内部所有子部件的样式：

```c
void SetStyleRecursively (GtkWidget *widget, gpointer data)
{
	GtkStyle *style;

	/* 获取样式 --- */
	style = (GtkStyle *)data;

	/* 设置小部件的样式 --- */
	gtk_widget_set_style(widget, style);

	/* 如果它可能有子部件 --- */
	if (GTK_IS_CONTAINER(widget)) {
		/* 也设置所有子部件的样式 --- */
		gtk_container_foreach (GTK_CONTAINER(widget), 
			SetStyleRecursively);
	}
}
```

## 第11 章 样式、颜色、字体、光标和引用
