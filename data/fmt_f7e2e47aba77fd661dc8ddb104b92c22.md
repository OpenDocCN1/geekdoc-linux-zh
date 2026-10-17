
| `GtkColorSelectionDialog` | 一个对话框，向用户呈现颜色选择部件以及此类对话框中实用的按钮。 |

尽管 `GtkFontSelection` 和 `GtkColorSelection` 与 `GtkWindow` 无关，但它们在本章中被描述了。我在这里介绍它们是因为我觉得，理解它们的运行机制对于理解它们对应的 `GtkWindow` 派生类（分别为 `GtkFontSelectionDialog` 和 `GtkColorSelectionDialog`）至关重要，而且将它们全部写在一个章里比比散在整书中更有意义。

既然本章的议程已经设定好，让我们来看看 `GtkWindow` 部件层次结构的顶端，意不其料，就是 `GtkWindow` 部件本身。

# GtkWindow

## 类名

`GtkWindow`

## 父类名

`GtkBin`

## 宏

- 部件类型宏：`GTK_TYPE_WINDOW`
- 对象到部件强制转换宏：`GTK_WINDOW(obj)`
- 部件类型检查宏：`GTK_IS_WINDOW(obj)`

## 支持的信号

| 表 7.2 信号 |  |
|---|---|
| 信号名称 | 使用信号触发的条件 |
| `set_focus` | 窗口中的某个部件获得了焦点。 |

## 信号函数原型

```
void
set_focus(GtkWindow *window, GtkWidget *widget, gpointer user_data)
```

## 支持的参数

前缀：`GtkWindow::`

### 表 7.3 GtkWindow 参数

| 名称 | 类型 | 权限 |
|---|---|---|
| `type` | `GTK_WINDOW_TYPE` | `GTK_ARG_READWRITE` |
| `title` | `GTK_TYPE_STRING` | `GTK_ARG_READWRITE` |
| `auto_shrink` | `GTK_TYPE_BOOL` | `GTK_ARG_READWRITE` |
| `allow_shrink` | `GTK_TYPE_BOOL` | `GTK_ARG_READWRITE` |
| `allow_grow` | `GTK_TYPE_BOOL` | `GTK_ARG_READWRITE` |
| `modal` | `GTK_TYPE_BOOL` | `GTK_ARG_READWRITE` |
| `window_position` | `GTK_TYPE_WINDOW_POSITION` | `GTK_ARG_READWRITE` |

## 应用级 API 概述

在运行时检索窗口类型常量 `GTK_TYPE_WINDOW`：

```
GtkType
gtk_window_get_type(void);
```

创建一个指定类型的 `GtkWindow` 实例，`GTK_WINDOW_TOPLEVEL`、`GTK_WINDOW_DIALOG` 或 `GTK_WINDOW_POPUP`：

```
GtkWidget *
gtk_window_new(GtkWindowType type);
```

设置窗口管理器显示的窗口标题：

```
void
gtk_window_set_title(GtkWindow *window, const char *title);
```

设置窗口管理器类和类名：

```
void
gtk_window_set_wmclass(GtkWindow *window, const char *wmclass_name, const char *wmclass);
```

设置窗口策略提示：

```
void
gtk_window_set_policy(GtkWindow *window, int allow_shrink, int allow_grow, int auto_shrink);
```

设置窗口的 x 和 y 坐标：

```
void
gtk_window_set_position(GtkWindow *window, GtkWindowPosition position);
```

设置窗口的焦点部件：

```
void
gtk_window_set_focus(GtkWindow *window, GtkWidget *focus);
```

## 应用级 API 概述（续）

激活窗口的焦点部件：

```
gint
gtk_window_activate_focus(GtkWindow *window);
```

设置窗口的默认部件：

```
void
gtk_window_set_default(GtkWindow *window, GtkWidget *default_widget);
```

激活窗口的默认部件：

```
gint
gtk_window_activate_default(GtkWindow *window);
```

使窗口成为瞬态的：

```
void
gtk_window_set_transient_for(GtkWindow *window, GtkWindow *parent);
```

设置窗口管理器几何结构提示：

```
void
gtk_window_set_geometry_hints(GtkWindow *window, GtkWidget *geometry_widget, GdkGeometry *geometry, GdkWindowHints geom_mask);
```

设置窗口大小：

```
void
gtk_window_set_default_size(GtkWindow *window, gint width, gint height);
```

使指定的窗口成为模态：

```
void
gtk_window_set_modal(GtkWindow *window, boolean modal);
```

## 类描述

`GtkWindow` 类提供了应用程序创建和操作窗口所需的功能。

## 创建窗口部件

`Gtk+` 中的窗口创建是通过调用 `gtk_window_new()` 实现的。该程序接受一个参数，即要创建的窗口类型。`Gtk+` 中的窗口可以是顶层窗口（`GTK_WINDOW_TOPLEVEL`）、对话框（`GTK_WINDOW_DIALOG`）或弹出窗口（`GTK_WINDOW_POPUP`）。这些窗口类型将在后续节中分别讨论。首先，以下代码说明了顶层窗口的创建。

```
GtkWidget * window;
window = gtk_window_new(GTK_WINDOW_TOPLEVEL);

if (window != (GtkWidget *) NULL ) {
```

## GtkWindow

`gtk_window_new()` 的函数原型为：

```
GtkWidget *
gtk_window_new(GtkWindowType type);
```

前面的代码说明了两个值得注意的点。首先，正如我之前讨论的，无论类型如何，部件的惯是存储在类型为 `GtkWidget *` 的变量中。你会注意到下面的代码中我使用了 `GTK_WINDOW` 宏来根据需要将其转换为 `GtkWindow` API 中某些函数所需的 `GtkWindow *`。其次，特别是在开发期间，检查部件创建函数的返回值通常是一个好主意，无论实例化的是哪种 `Gtk` 类，以确保程序没有失败并且实际上创建了部件。如果发生故障，返回类型将为 `NULL`；这对于 `Gtk` 1.2 支持的所有部件创建函数都适用（在这种情况下，无效的类型参数将导致失败）。失败的另一个原因是某种内部故障，例如部件创建函数无法分配内存。

## 窗口类型

顶层窗口（`GTK_WINDOW_TOPLEVEL`）是一个没有父窗口的窗口（在实际上，父窗口将是服务器的根窗口）。换句话说，它是独立的，独立于用户桌面上的其他应用程序窗口。通常，这种窗口类型将用于创建应用程序的主窗口。`Gtk+` 顶层窗口参与窗口管理器协议；`GDK` 在创建顶层窗口时代表 `Gtk+` 请求这些协议的支持。顶层窗口支持的两种窗口管理器协议使用 `WM_DELETE_WINDOW` 和 `WM_TAKE_FOCUS`。对这些窗口管理器协议感兴趣感兴趣读者可以参考 O'Reilly & Associates 出版的《The Xlib Programming Manual, Volume One》。

对话框（`GTK_WINDOW_DIALOG`）与顶层窗口相似，因为它没有父窗口（父窗口是服务器根窗口）。而且像顶层窗口一样，对话框也参与 `WM_DELETE_WINDOW` 和 `WM_TAKE_FOCUS` 窗口管理器协议。它与顶层窗口的区别在于窗口是瞬态的。在 X 中，对话框几乎总是通过调用变为瞬态的
