
```c
gtk_signal_connect(GTK_OBJECT(button), "clicked",
    GTK_SIGNAL_FUNC(CancelClickedCallback), dialog_window);

label = gtk_label_new (message);
gtk_misc_set_padding(GTK_MISC(label), 10, 10);
gtk_box_pack_start(GTK_BOX(GTK_DIALOG(dialog_window))->content_area,
    label, TRUE, 0);
if (parent != NULL) {
    gtk_window_set_transient_for(GTK_WINDOW(dialog_window), GTK_WINDOW(parent));
}
gtk_widget_show_all(GTK_WINDOW(dialog_window));
gtk_main();
```

## GtkWindow

## 应用级 API 概述

在运行时获取常量 `GTK_TYPE_DIALOG`：
```c
GtkType
gtk_dialog_get_type (void);
```

创建一个 `GtkDialog` 的新实例：
```c
GtkWidget *
gtk_dialog_new(void);
```

### 类描述

对话框（在 Gtk+ 中）是一个包含两个区域的窗口：

- 一个内容区域，包含对话框展示的基本内容
- 一个操作区域，由一组按钮组成，点击这些按钮时，会对对话框的内容执行操作，并/或关闭对话框

对话框的内容区域和操作区域之间设有一个水平分隔线，用来帮助用户区分操作区域和内容区域。请见图 7.2。

![](img/b9af04aaed46302cb075052312fcd667_312_0.png)

图 7.2 对话框控件的区域

对话框可以是简单的（见图 7.3），在内容区域或操作区域中都只包含少许内容，也可以如图 7.4 所示具有任意复杂性。通常情况下，操作区域的内容通常只包含 `GtkButton` 实例，尽管 `Gtk-Dialog` 并不强制要求这一点。

![](img/b9af04aaed46302cb075052312fcd667_312_1.png)

图 7.3 简单对话框控件

## GtkDialog

![](img/b9af04aaed46302cb075052312fcd667_313_0.png)

**图 7.4** 复杂对话框控件

对话框的内容区域由一个垂直框控件（`GtkVBox`）组成。对话框控件的操作区域是一个水平框控件（`GtkHBox`）。使用垂直框用于内容区域，是因为通常情况下，应用程序倾向于从上到下（或从下到上）打包对话框内容。使用水平框控件用于操作区域，是因为通常该区域内的按钮会从左到右（或从右到左）排列。应用程序可以轻松地将一个水平框作为内容区域垂直框的子控件。控件的描述见第 10 章“容器和容器类”。在尝试在应用程序中使用对话框控件之前，你应该已经熟悉 `GtkHBox` 和 `GtkVBox` 控件。

## 创建对话框

要创建 `GtkDialog` 实例，请调用 `gtk_dialog_new()`：
```c
GtkWidget *
gtk_dialog_new(void);
```

使用以下示例代码创建了图 7.3 所示的对话框：

- **列表 7.1** 创建一个消息对话框
```c
001  #include <gtk/gtk.h>
002
003  main(int argc, char *argv[])
004  {
005      GtkWidget *dialog, *label, *button;
006      gtk_init( &argc, &argv);
007      dialog = gtk_dialog_new();
008
009
010  gtk_widget_set_size( dialog, 214, 117 );
011  gtk_window_set_policy( GTK_WINDOW( dialog ), FALSE, FALSE, FALSE);
012
013  gtk_window_set_title( GTK_WINDOW( dialog ), "Alert" );
014
015  label = gtk_label_new("You have new mail!");
016  gtk_box_pack_start( GTK_BOX (GTK_DIALOG(dialog))->vbox,
017  label, TRUE, 0);
018
019  button = gtk_button_new_with_label("OK");
020  GTK_WIDGET_SET_FLAGS(button, GTK_CAN_DEFAULT);
021  gtk_box_pack_start( GTK_BOX (GTK_DIALOG (dialog))->action_area,
022  button, FALSE, FALSE, 0);
023  gtk_widget_grab_default( button );
024
025  gtk_widget_show_all( dialog );
027  gtk_main();
028  }
```

## 对话框尺寸

前面的源代码让我想起了对话框尺寸的问题。图 7.3 所示类型的对话框在特定尺寸下看起来最好。为了确定我认为的最佳尺寸，我简单地运行了程序并调整窗口大小，直到其尺寸看起来我满意。然后我在程序中添加了第 010 行：
```c
010 gtk_widget_set_size( dialog, 214, 117 );
```

这设置了窗口的初始尺寸，结果正如实验所示，在这种情况下是一个宽度为 214、高度为 117 的控件。在后续行中，我添加了对 `gtk_window_set_policy()` 的调用：
```c
011 gtk_window_set_policy( GTK_WINDOW( dialog ),
FALSE, FALSE, FALSE);
```

前面的更改确保了用户无法调整对话框的尺寸，避免了如果允许用户调整对话框尺寸可能会出现的任何奇怪（且视觉上不可的）的布局。

![](img/b9af04aaed46302cb075052312fcd667_314_0)

图 7.5 边框

## GtkFileSelection

![](img/b9af04aaed46302cb075052312fcd667_319_0.png)

图 7.9 带有自定义内容的文件选择控件

图 7.9 展示了 GIMP 用于打开图像文件的文件选择控件。如你所示，对话框中图 7.7 或 7.8 中没有的额外内容（具体来说是标记为“打开选项”的文件）。我将在接下来的讨论中说明如何添加此类内容。

## 创建 GtkFileSelection 实例

创建一个文件选择控件非常简单。要此操作，你需要调用 `gtk_file_selection_new()`：
```c
GtkWidget *
gtk_file_selection_new(const gchar *title);
```

参数 `title` 将在应用程序显示文件选择对话框时，由窗口管理器在对话框的标题栏中显示。只需将返回值传递给 `gtk_widget_show()` 即可将其作为对话框窗口显示。你不需要像添加按钮或标签那样将文件选择控件作为容器控件的子控件。

## 修改文件选择控件

默认情况下，当前工作目录将显示在“目录”和“文件”列表中。“选择”文本编辑字段将为空。要在显示文件选择对话框之前更改要显示的目录，请调用 `gtk_file_selection_complete()`：
```c
void
gtk_file_selection_complete (GtkFileSelection *filesel,
const gchar *pattern);
```

- [费曼学习法](https://wiki.example.org/feynmans_learning_method)的灵感源于诺贝尔物理奖获得者**理查德·费曼**。

1. 运用费曼技巧，你只需花上`20 min`就能深入理解知识点，而且记忆深刻，*难以遗忘*。

```c
if (condVar > someVal) {console.log("xxx")}
```
