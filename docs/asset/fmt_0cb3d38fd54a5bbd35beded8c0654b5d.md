
`tooltips = gtk_tooltips_new ();`

/* 按通常方式构建窗口 */

`window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );`

`gtk_window_set_title ( GTK_WINDOW ( window ), "Global tooltip control" );`

`gtk_window_set_default_size ( GTK_WINDOW ( window ), 320, 200 );`

`gtk_signal_connect ( GTK_OBJECT ( window ), "destroy", G_SIGNAL_FUNC ( CloseTheApp ), NULL );`

/* 创建一个布局框来放置两个按钮，并将其窗口 */

`buttonbox = gtk_hbox_new ( TRUE, 5 );`

`gtk_container_add ( GTK_CONTAINER ( window ), button );`

/* 创建一个开启提示的按钮 */

`button = gtk_button_new_label ( "Turn tips on" );`

`gtk_box_pack_start ( GTK_BOX ( button ), button, TRUE, TRUE, 5 );`

`gtk_signal_connect ( GTK_OBJECT ( button ), "clicked", G_SIGNAL_FUNC ( TipsOnClicked ), tooltips );`

/* 为此按钮创建一个新提示 */

`gtk_tooltips_set_delay ( tooltips, 0 );` // 根据上下文重建

/* 创建一个关闭提示的按钮 */

`button = gtk_button_new_label ( "Turn tips off" );`

`gtk_box_pack_start ( GTK_BOX ( button ), button, TRUE, TRUE, 5 );`

`gtk_signal_connect ( GTK_OBJECT ( button ), "clicked", G_SIGNAL_FUNC ( TipsOffClicked ), tooltips );`

/* 为此按钮创建一个新提示 */

`gtk_tooltips_disable ( tooltips );`

`gtk_widget_show_all ( window );`

`gtk_main ();`

`return 0;`

## 状态栏

状态栏是一种向用户提供反馈而不中断其操作的方式。在 GTK+ 中，状态栏使用消息栈。你可以将消息推入栈，也可以将其弹出。

拥有上下文 ID 后，在状态栏中推送和弹出消息只需要两次调用。

```c
guint gtk_statusbar_push ( GtkStatusbar * statusbar,
guint context_id, const gchar * text );
void gtk_statusbar_pop ( GtkStatusbar * statusbar,
guint context_id );
```

第一个调用将新消息推入栈，使其显示在状态栏中。它返回一个唯一的消息 ID。第二个调用将从栈中移除匹配指定上下文的消息。

所以，回到我们的联系人示例，你可能会有类似如下的代码：

```c
maincontext = gtk_statusbar_get_context_id ( GTK_STATUSBAR ( status ), "main" );
updatecontext = gtk_statusbar_get_context_id ( GTK_STATUSBAR ( status ), "update" );
```

## 第 9 章

```c
void ButtonOff ( GtkButton button, gpointer data )
{
  /* 最后一次出现的消息是消息上的按钮。
  将其从状态栏堆栈中弹出 */
  gtk_statusbar_pop ( GTKSTATUSBAR ( status ), btncontext );
}
```

```c
GtkWidget * BuildUserInterface ()
{
  GtkWidget * vbox;
  GtkWidget * button;
  GtkTooltips * buttontip;
  guint context;

  /* 创建一个包含按钮和状态栏的 VBox */
  vbox = gtk_box_new ( FALSE, 5 );

  /* 创建按钮 */
  button = gtk_button_new_with_label ( "点我这里" );
  gtk_box_pack_start ( GTK_BOX ( vbox ), button, TRUE, 5 );

  /* 创建状态栏 */
  status = gtk_statusbar_new ( );
  gtk_box_pack_end ( GTK_BOX ( vbox ), status, FALSE, 5 );

  /* 获取主程序的上下文 ID */
  context = gtk_statusbar_get_context_id (
    GTKSTATUSBAR ( status ),
    "Main" );

  /* 设置就绪消息 */
  gtk_statusbar_push ( GTKSTATUSBAR ( status ),
    context, "就绪。" );

  /* 现在连接按钮处理程序 */
  gtk_signal_connect ( GTK_OBJECT ( button ),
    "enter",
    GTK_SIGNAL_FUNC ( ButtonOn ),
    NULL );
  gtk_signal_connect ( GTK_OBJECT ( button ),
    "leave",
    GTK_SIGNAL_FUNC ( ButtonOff ),
    NULL );

  /* 最后，为按钮连接工具提示 */
  buttontip = gtk_tooltips_new ( );
  gtk_tooltips_set_tip ( buttontip, button,
    "我什么都不做",
    "这个按钮还没有设置好能做什么" );

  return vbox ;
}
```

## 高级控件

```c
gint main ( gint argc, gchar * argv[] )
{
    GtkWidget * window;
    gtk_init ( &argc, &argv );
    window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );
    gtk_container_set_border_width ( GTK_CONTAINER ( window ), 2 );
    gtk_window_set_default_size ( GTK_WINDOW ( window ), 320, 200 );
    gtk_signal_connect ( GTK_OBJECT ( window ),
        "destroy",
        GTK_SIGNAL_FUNC ( CloseTheApp ),
        NULL );
    gtk_container_add ( GTK_CONTAINER ( window ),
        BuildUserInterface ( );
    gtk_widget_show_all ( window );
    gtk_main ();
    return 0;
}
```

编译并运行后，你将得到一个所示的窗口。

| 状态栏 |
| :--- |
| 点我这里 |
| 这个按钮还没有设置好能做什么 |

代码设置了一个包含单个按钮和状态栏的窗口。按钮上附有一个工具提示。一旦窗口被创建，一个 READY（就绪）消息就会推送到状态栏上。在这个例中，我使用的上下文仅被称为 "main"，表示这是一个通用的应用程序消息。你可以根据需要对其进行命名。

连接到按钮的信号处理程序用于在用户将鼠标移入或移出按钮运行时某些代码。此时，我们使用一点简单的工具代码来查找提示的私有文本，并使用不同的上下文将其推送到状态栏。这导致每当我们将鼠标移入按钮时，状态栏就会发生变化。鼠标移出后，消息就会弹出，显示最初推送到状态栏的 READY 消息。

## 工具栏

从头开始自己创建一个工具栏并不困难。你可以在窗口顶部的菜单下方放置一个框架（frame），然后在框架内部放置一个水平框（Hbox）。然后你将按钮以及你选择的任何控件放入 HBox 中，从而得到属于你自己的工具栏。

在对几个应用程序进行这样做之后，聪明的开发者会获取你的工具栏代码，并在其中编写一个实用函数，为你完成所有繁琐的工作，例如自动连接回调处理程序、动态创建按钮等。然而，GTK+ 的开发者们想到了这一点，并产生了一个完全自包含且功能极其多样的 `GtkToolbar` 对象，它可以实现你对工具栏的所有可能需求。

第一步是创建工具栏。

```c
GtkWidget * gtk_toolbar_new ( GtkOrientation orientation, GtkToolbarStyle style );
```

这两个参数决定了工具栏的外观和感受。`orientation` 参数可以是两个值之一：`GTK_ORIENTATION_VERTICAL` 或 `GTK_ORIENTATION_HORIZON`。而 `style` 参数规定了按钮的布局，可以是 `GTK_TOOLBAR_ICONS`、`GTK_TOOLBAR_TEXT` 或 `GTK_TOOLBAR_BOTH` 中的任意一个。

在创建工具栏并将其封装到窗口后，下一步是向其添加内容。通常情况下，你会添加按钮，因此工具栏带有一组预构建的函数，为你承担创建按钮的重复性工作。

```c
GtkWidget * gtk_toolbar_append_item ( GtkToolbar * toolbar,
const gchar * text,
const gchar * tooltip_text,
const gchar * tooltip_private_text,
GtkWidget * icon,
GtkSignalFunc callback,
gpointer data );
```

另一种方法是 `gtk_toolbar_prepend`。它与 `append_item` 类似，但它会将项目插入到工具栏开头。

连接到按钮的信号处理程序用于在用户将鼠标移入或移出按钮运行时某些代码。此时，我们使用一点简单的工具代码来查找提示的私有文本，并使用不同的上下文将其推送到状态栏。这导致每当我们将鼠标移入按钮时，状态栏就会发生变化。鼠标移出后，消息就会弹出，显示最初推送到状态栏的 READY 消息。

## 高级控件

```c
GtkObject * gtk_adjustment_new ( gfloat value,
    ...gfloat min, gfloat max,
    ...gfloat step_increment,
    ...gfloat page_increment,
    ...gfloat page_size );
```

对于该调用的前三个参数，从进度条的视图应该是显而易见的。它们允许你指定进度条的当前值，以及代表 0% 和 100% 的值。

想象滚动条中的最后三个参数。滚动条两端箭头的每次点击都会按 `step_increment` 步长增加或减少滚动条的位置。在滚动条本身上的每次点击（使滚动条跳转到鼠标指针下）会导致数值按 `page_increment` 步长增加或减少。`page_size` 参数用于显示多少个项目将代表单页信息，正如进度条被称的那的那样。

回到进度条，你如何使用 `GtkAdjustment` 对象来自动设置进度条而无需进行 `make` 调用呢？这在下面的代码中所示：

```c
GtkObject * adjustment = gtk_adjustment_new ( 0.0, 0.0, 3000.0,
0.0, 0.0, 0.0 );
GtkWidget * progress = gtk_progress_bar_new_with_adjustment
    ( GTK_ADJUSTMENT ( adjustment ) );
```

关于 `gtk_progress_bar_new_with_adjustment` 需要注意的重要点是，它期望一个指向 `GtkAdjustment` 指针，但 `gtk_adjustment_new` 的调用返回的是指向通用 `GtkObject` 的指针。这个问题可以通过合理使用 `GTK_ADJUSTMENT` 解决。

正如你根据 GTK+ 目前为止所预期的那样，有几个调用可以自定义进度条的外观和感觉。

默认情况下，进度条是水平的，条从左到右延伸。你可以通过调用以下函数来改变此行为：

```c
void gtk_progress_bar_set_orientation ( GtkProgressBar * pbar,
GtkProgressBarOrientation orientation );
```

`orientation` 参数可以是以下值之一：`GTK_PROGRESS_LEFT_TO_RIGHT`、`GTK_PROGRESS_RIGHT_TO_LEFT`、`GTK_PROGRESS_TOP_TO_BOTTOM` 或 `GTK_PROGRESS_BOTTOM_TO_TOP`。我相信你可以自己弄清楚这些不同的值。

让进度条随新值更新涉及调用 `gtk_progress_bar_update`。

```c
void gtk_progress_bar_update ( GtkProgressBar * pbar, gfloat percent );
```

只需传入指向控件本身的指针，后跟你想显示的作为 `gfloat` 的百分比。如果你将 `GtkProgressBar` 强制转换为基类 `GtkProgressBar`，你就不局限于处理百分比，而且也不局限于仅向进度条传递值。

```c
void gtk_progress_set_value ( GtkProgressBar * progress, gfloat value );
void gtk_progress_set_percentage ( GtkProgressBar * progress, gfloat percentage );
```

第一个调用将值设置到进度对象中，该对象反将其转换为百分比供进度条显示。考虑到 `gtk_progress_bar_update` 的调用，在处理进度条时，第二个调用 `gtk_progress_set_percentage` 是没有意义的。

从 `GtkProgressBar` 对象中获取信息同样简单。

```c
float gtk_progress_get_value ( GtkProgressBar * progress );
float gtk_progress_get_current_percentage ( GtkProgressBar * progress );
```

然而，`GtkProgressBar` 对象也可以告诉你某个值代表多大的百分比。

```c
float gtk_progress_get_percentage_from_value ( GtkProgressBar * progress, gfloat value );
```

将值作为第二个参数传递给此调用，将返回该值如果设置到进度对象中将代表的百分比。`GtkProgressBar` 确实如其其言，它显示的是进度条。如果你快速看一眼上方进度条的截图，你会注意到条上以数字显示了百分比。这得益于调用 `gtk_progress_show_text`。

```c
void gtk_progress_show_text ( GtkProgressBar * progress, gboolean show );
```

将 `TRUE` 传入第二个参数，条将显示以数字形式表示的百分比，传入 `FALSE` 则恢复默认行为。让我们来看看这些是如何运行的。

```c
/**
* progress.c
* 实现进度控件的代码
 */
#include <gtk/gtk.h>

void CloseApp ( GtkWidget * window, gpointer data )
{
  gtk_main_quit();
}
```

```c
void ButtonClicked ( GtkButton * button, gpointer progress )
{
  /* 第一，获取当前值 */
  gfloat value = gtk_progress_get_value ( GTK_PROGRESS ( progress ) );

  /* 将值加 10 并计算百分比 */
  gfloat percent = gtk_progress_get_percentage_from_value ( GTK_PROGRESS ( progress ),
  value + 10 );

  /* 使用新百分比更新进度条 */
  gtk_progress_bar_update ( GTK_PROGRESS_BAR ( progress ), percent );
}

GtkWidget * SetupVBox ()
{
  GtkWidget * vbox;
  GtkWidget * progress;
```
