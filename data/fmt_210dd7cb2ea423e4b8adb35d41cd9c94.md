
## 高级控件

```c
GtkObject * gtk_adjustment_new ( gfloat value,
    gfloat min, gfloat max,
    gfloat step_increment,
    gfloat page_increment,
    gfloat page_size );
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
  gfloat percent = gtk_progress_get_percentage_from_value ( GTK_PROGRESS ( progress )
  value + 10 );

  /* 使用新百分比更新进度条 */
  gtk_progress_bar_update ( GTK_PROGRESS_BAR ( progress ), percent );
}

GtkWidget * SetupVBox ()
{
  GtkWidget * vbox;
  GtkWidget * progress;
  GtkWidget * button;

  /* 设置一个 vbox 来包含进度条和按钮 */
  vbox = gtk_vbox_new ( FALSE, 5 );

  /* 在 vbox 中添加一个进度条 */
  progress = gtk_progress_bar_new_with_adjustment
    ( GTK_ADJUSTMENT ( gtk_adjustment_new ( 0.0, 0.0, 3000.0, 0.0, 0.0, 0.0 ) ) );
  gtk_box_pack_start ( GTK_BOX ( vbox ), progress, FALSE, 0 );

  /* 在 vbox 中添加一个按钮 */
  button = gtk_button_new_with_label ( "Update" );
  gtk_box_pack_start ( GTK_BOX ( vbox ), button, FALSE, 0 );

  /* 连接按钮信号 */
  gtk_signal_connect ( button, "clicked", G_CALLBACK ( ButtonClicked ), progress );

  return vbox;
}

int main ( int argc, gchar * argv )
{
  GtkWidget * window;

  gtk_init ( &argc,argv);

  /* 创建窗口 */
  window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );
  gtk_window_set_title ( GTK_WINDOW ( window ), "Progress widgets" );

  /* 添加 vbox 到窗口 */
  gtk_container_add ( GTK_CONTAINER ( window ), SetupVBox() );

  /* 连接销毁信号 */
  gtk_signal_connect ( window, "destroy", G_CALLBACK ( CloseApp ), NULL );

  /* 显示所有控件 */
  gtk_widget_show_all ( window );
  gtk_main();

  return 0;
}
```

## 第 9 章

让我们来看看旋钮按钮（spin button）是如何运作的。

```c
/**
 * spin1.c
 *
 * 一个用于显示旋钮按钮运行的简单应用程序
 */
#include <gtk/gtk.h>

void CloseTheApp ( GtkWidget * window, gpointer data ) {
  gtk_main_quit();
}

int main ( int argc, gchar * argv[]) {
  GtkWidget * window;
  GtkWidget * spinbutton;
  GtkAdjustment * initvals;

  gtk_init ( &argc, &argv);

  /* 按照通常方法构建窗口 */
  window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );
  gtk_window_set_title ( GTK_WINDOW ( window ), "Spin buttons" );
  gtk_container_set_border_width ( GTK_CONTAINER ( window ), 10 );
  gtk_window_set_default_size ( GTK_WINDOW ( window ), 320, 50 );

  /* 设置调整值，准备创建旋钮按钮 */
  initvals = GTK_ADJUSTMENT (gtk_adjustment_new ( 2000.0, 1900.0, 2050.0, 1.0, 1.0 ));

  /* 使用调整值创建旋钮按钮，然后将其添加到窗口 */
  spinbutton = gtk_spin_button_new ( initvals, 1.0, 0.0 );
  gtk_container_add ( GTK_CONTAINER ( window ), spinbutton );

  gtk_signal_connect ( GTK_OBJECT ( window ),
                      "destroy",
                      GTK_SIGNAL_FUNC ( CloseTheApp ),
                      NULL );

  gtk_window_show_all ( window );
  gtk_main ( );

  return 0;
}
```

编译源码并运行编译后的程序，你将得到一个与所示相似的窗口。

![](img/aa3546013f120531cd191b770d85869c_248_0.png)

尽管旋钮按钮功能强大，但它们的设置起来并不比任何其他 `GtkWidget` 困难。这显然是一个非常简单的示例，它没有捕获连接到旋钮按钮的输入框的信号（旋钮按钮会产生自己的信号）。在下一节中，当我们查看日历时，将在一个更强大的示例中重新回顾旋钮按钮。

## 日历

GTK+ 提供了一个日历控件，使用户可以快速、方便地选择单个日期。

![](img/aa3546013f120531cd191b770d85869c_248_1.png)

在屏幕图中，日历是占据窗口底部三分之二的矩形控件。旋钮按钮是我们将处理的下一个示例的一部分。

在使用时，日历控件非常简单。用户点击月份名称和年份的任一即可更改日期。选择日期只需在周显示器中点击日期即可。

从代码的角度来看，日历也同样容易处理。创建日历涉及调用此函数。

```c
GtkWidget * gtk_calendar_new ();
```

这会创建一个带有当前日期的日历小部件。要更改该日期，你需要调用以下一个或两个函数。

```c
void gtk_calendar_select_month ( GtkCalendar * calendar, guint month, guint year );
void gtk_calendar_select_day ( GtkCalendar * calendar, guint day );
```

尽管名字如此，`gtk_calendar_select_month` 是用于通过编程方式更改月份或月份和年份的。还需要注意的是，日历控件中的月份是从 0 开始的。1 月是月份 0，12 月是月份 11。如果你以前没有遇到这种情况，这可能看起来奇怪，但它与 Unix 日期和时间处理结构的布局是一致的。

从日历控件中提取日期（用户选择并高亮显示的日期）涉及调用名副其实的 `gtk_calendar_get_date` 函数。

```c
void gtk_calendar_get_date ( GtkCalendar * calendar,
guint *year, guint * month, guint * day );
```

你需要传递整数的指针，函数调用将通过这些指针填充当前选择的日期、月份和年份。

最后，你还可以标记月份中的某些日期。这与选择日期不同，因为它仅仅是在日历控件上画一个标记。如果你正在开发某种个人组织应用程序，并有某种突出重要日期的方法，这将是理想的。处理日历小部件中的标记有三个调用。

```c
