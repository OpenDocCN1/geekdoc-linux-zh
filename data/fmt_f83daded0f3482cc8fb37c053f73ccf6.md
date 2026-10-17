
创建完成后，你可以使用`gnome_number_entry_get_number`获取输入到部件数字区域的数字。这与`GnomeCalculator`小部件的操作类似。

让我们在`numberentry.c`中查看此。

```c
/**
 * numberentry.c
 * 演示 GnomeNumberEntry
 * 小部件的使用
 */

#include <gnome.h>

void CloseTheApp ( GtkWidget * window, gpointer data )
{
    gtk_quit (0);
}

void NumberChanged ( GtkEditable * editable, gpointer data )
{
  /* 获取输入框持有的值并打印出来 */
  g_print ( "The value changed to %s\n", gtk_entry_get_text ( GTK_ENTRY ( editable ) ) );
}

int main ( int argc, gchar * argv[])
{
  GtkWidget * window;
  GtkWidget * numberentry;
  GtkWidget * entrybox;

  gnome_init ("numberentry", "1.0", argc, argv);

  window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );
  gtk_container_set_border_width ( GTK_CONTAINER ( window ), 10 );
  gtk_signal_connect ( GTK_OBJECT ( window ),
      "destroy",
      GTK_SIGNAL_FUNC ( CloseTheApp),
      NULL );

  /* 创建数字部件，无历史指针，
     但为其触发的弹出窗口提供有效的标题 */
  numberentry = gnome_number_entry_new ( NULL, "Enter your number ");
  gtk_container_add ( GTK_CONTAINER ( window ), numberentry );

  /* 获取输入框以对其连接信号处理函数 */
  entrybox = gnome_number_entry_gtk_entry ( GNOME_NUMBER_ENTRY ( numberentry ) );
  gtk_signal_connect ( GTK_OBJECT ( entrybox ),
      "changed",
      GTK_SIGNAL_FUNC ( NumberChanged),
      NULL );

  gtk_widget_show_all ( window );

  gtk_main ( );
  return 0;
}
```

## GNOME 控件

这实际上是 GNOME 和 GTK 都深受程序员喜爱的原因之一。这些库使用的面向对象模型设计得非常完美，从不会强迫你采用某一种解决方案路径。这些库足够灵活，允许你以选择的任何方式与它们交互。

## GnomeColorPicker

`GnomeColorPicker`控件是另一个 GNOME 控件，它简化了 GTK+ 拨盘的使用。在`GnomeColorPicker`中，你会得到一个显示颜色样本的按钮。点击按钮会弹出颜色选择对话框，允许用户选择新颜色。当对话框关闭时，新选择的颜色将显示在按钮的颜色区域。因此，`GnomeColorPicker`控件与我们在 GTK+ 中看到的颜色选择器不同。应用程序用户一眼看出当前选定的颜色，而无需让一个巨大的对话框占据屏幕。只有当用户显式通过点击`GnomeColorPicker`颜色样本按钮时，对话框才会显示。

![](img/aa3546013f120531cd191b770d85869c_350_0.png)

`GnomeColorPicker`在解释用户选择的颜色方面还为程序员提供了更大的灵活性。它没有强迫用户将颜色选择解释为 0 到 65535 之间的红、绿、蓝值，而是允许你根据需要将这些值指定为字节值（0–255）、浮点值（0.0–1.0）或标准的 0-65535 值。回想 GTK+ 的处理方式非常有用，因为你不需要编写代码将浮点颜色值转换为整数颜色值以便用于 GDK 的颜色函数。

创建控件非常简单。

```c
GtkWidget * gnome_color_picker_new () ;
```

这创建了一个样本按钮，供你将其安装到某种容器中。按钮的内置功能负责在被点击时弹出并响应颜色选择对话框。

获取用户选择的实际值通过这三个函数调用之一来实现。

```c
void gnome_color_picker_get_d ( GnomeColorPicker * cp,
double * red,
double * blue,
double * green,
double * alpha );
```

```c
void gnome_color_picker_get_i8 ( GnomeColorPicker * cp,
    guint8 * red,
    guint8 * blue,
    guint8 * green,
    guint8 * alpha );
void gnome_color_picker_get_i16 ( GnomeColorPicker * cp,
    gushort * red,
    gushort * blue,
    gushort * green,
    gushort * alpha );
```

在大多数情况下，你可以忽略`alpha`（透明度）值。这实际上用于复杂的图形应用程序，在这些程序中，不仅要指定组成颜色的值，还要指定颜色的透明度。这通常不是构建用户界面的人会关心的问题。

在所有情况下，你都需要传递指向要填充所选颜色值的变量的指针。在`get_i8`函数中，这些是双类型，返回的值在 0.0 到 1.0 之间。在`get_i16`函数中，这些是无符号字节，返回的值在 0 到 255 之间。`get_i16`函数返回传统的 0-65535 值。

你还可以通过这些代码设置颜色值，以便为`GnomeColorPicker`控件提供默认颜色。这通过`gnome_color_picker_set_routines`实现。

```c
void gnome_color_picker_set_d ( GnomeColorPicker * cp,
    double * red,
    double * blue,
    double * green,
    double * alpha );
void gnome_color_picker_set_i8 ( GnomeColorPicker * cp,
    guint8 * red,
    guint8 * blue,
    guint8 * green,
    guint8 * alpha );
void gnome_color_picker_set_i16 ( GnomeColorPicker * cp,
    gushort * red,
    gushort * blue,
    gushort * green,
    gushort * alpha );
```

这些函数的格式与`get`函数几乎完全相同，明显的区别在于传递的参数是值，而不是指向值的指针。

还记得我早些时候提到你可能想忽略 alpha 值吗？你实际上可以设置控件来实现。

```c
void gnome_color_picker_use_alpha ( GnomeColorPicker * cp,
    boolean use_alpha );
```

如果你想让颜色选择器与 alpha 值一起工作，请将`use_alpha`参数设置为 TRUE。否则，只需将其设置为 FALSE。对于我们大多数人来说，这段代码并非在高端图形程序运行，将参数设置为 FALSE 可能是最好的方法。

与`GnomeNumberEntry`控件一样，`GnomeColorPicker`也允许你为弹出对话框设置标题。与`GnomeNumberEntry`不同的是，这不是在创建控件时完成的，而是通过其函数处理的。

```c
void gnome_color_picker_set_title ( GnomeColorPicker * cp,
const gchar * title );
```

## GnomeFontPicker

从使用角度来看，`GnomePicker`控件的概念与`GnomeColorPicker`更为相似。它是一个点击时会调用对话框的按钮，在这种情况下是字体选择。

![](img/aa3546013f120531cd191b770d85869c_354_0.png)

当然，你也可以将这些信息回传给`GnomeFontPicker`组件。

```c
gboolean gnome_font_picker_set_font_name ( GnomeFontPicker * fp,
                   const gchar * fontname );
```

如果传递给函数的有效且可用的字体规格，则函数返回 TRUE；如果由于某些原因失败，则返回 FALSE。

你还可以控制出现在弹出字体选择对话框中的预览文本，以便让对话框的内容与应用程序本身结合得更紧密。

```c
void gnome_font_picker_set_preview_text ( GnomeFontPicker * fp,
                   const gchar * previewtext );
gchar * gnome_font_picker_get_preview_text ( GnomeFontPicker * fp );
```

查看`fontpicker.c`以了解`GnomeFontPicker`的用法。

```c
/**
 * fontpicker.c
 * 
 * 演示了 GnomeFontPicker 控件的使用
 */

#include <gnome.h>
```

```c
void CloseTheApp ( GtkWidget * window, gpointer data )
{
  gtk_main_quit();
}
```

```c
void FontChosen ( GnomeFontPicker * picker, gchar * argl, gpointer data )
{
  g_print ("You chose the %s font\n",
           gnome_font_picker_get_font_name ( picker ) );
}
```

```c
gint main ( int argc, gchar * argv[] )
{
  GtkWidget * window;
  GtkWidget * picker;

  gnome_init ( "FontPicker", "1.0", argc, argv );

  /* 首先，创建窗口 */
```
