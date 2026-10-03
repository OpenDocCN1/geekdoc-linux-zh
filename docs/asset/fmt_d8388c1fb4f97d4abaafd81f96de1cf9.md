
# GtkMisc 与标签对齐

`GtkMisc` 是 `GtkLabel` 的父类之一，是你用来控制 `GtkLabel` 内文本对齐方式的机制。对齐参数范围从 0 到 1，在这种情况下意味着靠左对齐（0.0）和垂直居中（0.5）。默认值是水平和垂直居中（0.5），这在窗口中看起来并不好看。

`gtk_box_pack_start()` 指示 `GtkVBox` 将 `title_label` 装箱在盒子的开始（即顶部），尽管它是在之前使用 `pack_start` 装箱的任何小部件之后装箱。`gtk_box_pack_end()`（本章未使用）以相反的方向装箱，如果你希望在内容扩展时让小部件位于容器的中间某个位置，可以使用它。

`gtk_box_pack_start()` 以及 `gtk_box_pack_end()` 的最后三个参数指示小部件应如何分配空间。这三个参数中的第一个称为 `expand`（扩展），它影响小部件间距；如果应该为放置小部件的盒子分配额外空间，`expand` 决定了该小部件所在的容器分段是否包含该空间。额外空间将平均分配给所有 `expand` 为 `TRUE` 的分段。第二个值称为 `fill`（填充），在已为小部件分段分配额外空间的情况下，指示小部件是否应该增长以填充该空间，或者该空间应该用于内边距（padding）。第三个参数给出在该部件分段与其相邻部分之间应保持的像素填充数。

## 艺术家标签创建

艺术家标签以类似的方式创建：

```c
artist_label = gtk_label_new("Artist");

gtk_misc_set_alignment(GTK_MISC(artist_label), 0.0, 0.5);

gtk_box_pack_start(GTK_BOX(main_vbox), artist_label, FALSE, FALSE);
```

还有两个标签：一个显示播放器的尺寸，一个显示当前曲目的已用时间。这是因为它们在 `GtkImageBox` 中并排排列。

```c
status_hbox = gtk_hbox_new(TRUE, 0);
```

注意，为了让这些小部件的大小相等，因此你向构造函数传递了 `TRUE`。在这种情况下不需要额外的间距。

```c
gtk_box_pack_start(GTK_BOX(main_vbox), status_hbox, FALSE, 0);

status_label = gtk_label_new("<b>Stopped</b>");

gtk_label_set_use_markup(GTK_LABEL(status_label), TRUE);

gtk_misc_set_alignment(GTK_MISC(status_label), 0.0, 0.5);

gtk_box_pack_start(GTK_BOX(status_hbox), status_label, FALSE, 0);
```

# 第 11 章：GNOME 开发者平台

到目前，代码中唯一的新点是 `time_label` 被设置为右对齐，而不是我们之前所做的左对齐。这是因为标签将出现在窗口的右侧。

## 滑块控制

GUI 的下一个小部件是用于搜索和跟踪进度的滑块。它由 `GtkScale` 小部件提供（正如你预期的，`GtkScale` 也是可用的）。这些小部件是 `GtkScale` 的子类，可以在那里找到特定于刻度的方法，而它又是 `GtkRange` 的子类，包含了维护具有最小值、最大值和当前位置范围的其他功能。

`HScale` 和它的兄弟类 `VScale` 有多个构造函数。第一个使用默认范围，第三个是可用的，可以将小部件与现有的 `GtkRange` 对象关联。这里使用了从 0 到 100 的范围，这将允许将曲目的进度以百分比表示，消除了在启用不同长度的曲目时更改范围参数的需要。第三个参数指示范围的粒度——这里 1 非常合适。

使用 `gtk_scale_set_draw_value()` 不绘制当前位置的数值表示。最后的设置修改了小部件的更新策略，指示刻度在用户通过拖动更改值后何时发出值已更改的信号。`GTK_UPDATE_DISCONTINUOUS` 表示在用户完成拖动后才会发出信号。其他选项包括在用户拖动期间持续发出信号，这对于颜色选择器中的滑块要合适得多。

```c
seek_scale = gtk_scale_new_with_range(NULL, 0, 100, 1);

gtk_scale_set_draw_value(GTK_SCALE(seek_scale), FALSE);

gtk_range_set_update_policy(GTK_RANGE(seek_scale), GTK_UPDATE_DISCONTINUOUS);

gtk_box_pack_start(GTK_BOX(main_vbox), seek_scale, FALSE, 0);
```

## 播放控制按钮

GUI 的最后一部分是包含播放控制按钮的 `HBox`。

```c
controls_hbox = gtk_hbox_new(TRUE, 6);

gtk_box_pack_start_defaults(GTK_BOX(main_vbox), controls_hbox);
```

`gtk_box_pack_start_defaults()` 简单地让程序员无需提供三个尺寸和间距参数（如果他们使用的是默认值的话），而在这种情况下，默认值是完全完美的。

```c
play_button = gtk_button_new_from_stock(GTK_STOCK_MEDIA_PLAY);

gtk_widget_set_sensitive(play_button, FALSE);

gtk_box_pack_start_defaults(GTK_BOX(controls_hbox), play_button);
```

在这里，你创建了第一个按钮。由于 GTK+ 2.8 引入了用于播放、暂停和停止等常用媒体播放功能的库存项目，因此可以使用它们来构建具有正确图标、标题和工具提示的按钮。更好的是，只要安装了相关的翻译文件，库存项目将自动采用用户的语言设置，这意味着如果你想让应用程序本地化，你只需要翻译应用程序中的自定义函数。对于任何大型应用程序，这可能是大量的翻译工作，但通过使用库存项目，你可以确保常用功能至少是翻译一致的。库存项目还会适应用户的图标偏好，让你与周围环境融合。

在这里，按钮的“敏感”属性被设置为 `FALSE`。这会导致它显示为“灰色”，并且对点击或键盘事件没有响应。这是程序启动时按钮处于的一个良好状态，否则在用户选择文件之前，将没有可用文件。

其余按钮也以类似的方式创建，尽管由于按钮在暂停时处于按下状态，`GtkToggleButton` 让程序员需要多费一番功夫。在 GTK+ 2.8 中，没有 `gtk_toggle_button_new_from_stock()`，因此必须通过将标签设置为所需的库存 ID 来构建按钮，然后使用 `gtk_button_set_use_stock()`（继承自 `GtkButton`）将其设为库存按钮。`GtkButton` 的 `new_from_stock()` 构造函数也使用此过程，而它实际上只是一个方便的封装器。

```c
pause_button = gtk_toggle_button_new_with_label(GTK_STOCK_MEDIA_PAUSE);

gtk_button_set_use_stock(GTK_BUTTON(pause_button), TRUE);

gtk_widget_set_sensitive(pause_button, FALSE);

gtk_box_pack_start_defaults(GTK_BOX(controls_hbox), pause_button);
```

```c
stop_button = gtk_button_new_from_stock(GTK_STOCK_MEDIA_STOP);

gtk_widget_set_sensitive(stop_button, FALSE);

g_signal_connect(G_OBJECT(stop_button),
                 "clicked",
                 G_CALLBACK(stop_clicked),
                 NULL);

gtk_box_pack_start_defaults(GTK_BOX(controls_hbox), stop_button);
```

该函数通过返回 `GtkBox` 完成。GTK+ 部件像所有 `GObject` 一样是引用计数的，由于使用了指针来访问它们，在引用计数归零之前，对象本身不会被销毁。大多数情况下，引用计数的精确减少并不重要，因为大多数部件在应用程序关闭时会被销毁。如果在运行时创建和销毁部件，则需要注意，错误的引用计数可能会导致内存泄漏和段错误。

```c
return main_vbox;
}
```

在 `main()` 函数中，调用 `gtk_widget_show_all()` 之前添加一行：

```c
gtk_container_add(GTK_CONTAINER(main_window), build_gui());
```

这把包含窗口布局的 `VBox` 放入窗口本身。现有的 `gtk_widget_show_all()` 调用将使其可见，编译并运行程序后，你就应该拥有大部分的用户界面了。

## 菜单

仍然缺少一些东西：菜单栏。传统的 UI 设计认为，在像这样的小型程序中，菜单栏是没用的，但演示 GTK+ 构建菜单的方法是非常重要的。

构建菜单有多种方法，但在最近版本的 GTK+ 中，使用 `GtkAction` 对象的基于动作的菜单和工具栏已成为首选。`GtkUIManager` 在某种程度上类似于 `libglade`，但范围更小，它从程序员提供的 XML 生成菜单结构。每个菜单项都与一个 `GtkAction` 对象关联，该对象描述了它的标题、图标、工具提示以及点击它时的操作。`GtkAction` 对象也可以用于生成工具栏按钮，这提供了极大的便利：当菜单和工具栏项的启用/禁用状态改变时，`GtkAction` 对象的状态会自动更新相应的菜单和工具栏项的状态。

首要任务是描述我们将为创建菜单的动作。在 `build_gui()` 函数定义之前添加一个 `GtkActionEntry` 结构数组：

```c
static GtkActionEntry main_window_action_entries[] = {
    {"File", "NULL", "_File" },
    {
        "OpenFile",
        GTK_STOCK_OPEN,
        "_Open",
        "control>0",
        "Open a file for playback",
        G_CALLBACK(file_open)
    },
    {
        "Quit",
        GTK_STOCK_QUIT,
        "_Quit",
        "Exit the application",
        G_CALLBACK(app_quit)
    },
    {
        "Help",
        GTK_STOCK_HELP,
        "_Help",
        "Show help",
        G_CALLBACK(show_help)
    }
};
```

# 回调函数实现

```c
static void file_open(GtkAction *action) {
    /* We will write this function later */
}

static void file_quit(GtkAction *action) {
    gtk_main_quit();
}

static void help_about(GtkAction *action) {
    GtkWidget *about_dialog = gtk_dialog_new();

    gtk_dialog_set_name(GTK_ABOUT_DIALOG(about_dialog), "Music Player");
    gtk_dialog_set_version(GTK_ABOUT_DIALOG(about_dialog), "0.1*");
    gtk_dialog_set_copyright(GTK_ABOUT_DIALOG(about_dialog), "Copyright 2006, The Author");
    gtk_dialog_run(GTK_DIALOG(about_dialog));
}
```

在 `help_about` 中，你将遇到第一个 `GtkDialog`。`GtkAbout` 提供了一个适用于“关于应用程序”功能的理想对话框。应用程序的名称、版本和版权都可以通过简单的方法设置，然后由 `gtk_dialog_run()` 显示。你将在实现 `file_open()` 回调时再次遇到 `gtk_dialog_run()`。

```c
static void play_clicked(GtkWidget *widget, gpointer data) {
}

static void pause_clicked(GtkWidget *widget, gpointer data) {
}

static void stop_clicked(GtkWidget *widget, gpointer data) {
}
```

这些回调函数为播放、暂停和停止按钮提供了功能，因此回到 `build_gui()` 并将它们连接到按钮的“clicked”信号上。

```c
g_signal_connect(G_OBJECT(play_button), "clicked",
    G_CALLBACK(play_clicked), NULL);

g_signal_connect(G_OBJECT(pause_button), "clicked",
    G_CALLBACK(pause_clicked), NULL);

g_signal_connect(G_OBJECT(stop_button), "clicked",
    G_CALLBACK(stop_clicked), NULL);
```

程序现在可以编译了，如果你运行它，“关于”菜单项应该会显示“退出”。

# 介绍 GStreamer

现在大部分 GUI 已经就绪，可以添加实际播放音乐的能力。此功能将由 GStreamer 多媒体框架提供。

GStreamer 的工作原理要求应用程序开发者创建流水线。每个流水线由多个元素组成，每个元素执行特定的功能。通常，流水线从某种源元素开始。这可以是从磁盘读取并提供内容的 `filesrc` 元素，也可以是通过网络传输缓冲数据的元素，或者是从视频捕获设备获取数据的元素。随后会有许多元素，它们可能是解码器（用于将音频文件转换为处理的标准格式）、解复用器（用于从音频文件中分离多个音频通道）或其他处理器。流水线以输出元素结束，它可以是任何从文件到高级 Linux 音频架构（ALSA）音频输出或基于 OpenGL 的视频播放。这些输出元素被称为“汇点”。

因此，一个使用 ALSA 从磁盘播放 Ogg Vorbis 文件的典型流水线可能包含一个 `filesrc` 元素，一个 `vorbisdecoder` 元素，然后是一个 `alsasink`。

元素通过使用“衬垫”连接来连接。每个衬垫编辑一组能力，这些能力指示了衬垫的作用。某些衬垫提供特定类型的数据——例如来自文件的原始数据或来自解码器的解码音频。另一些衬垫接受特定类型或多种类型的数据，而另一些提供元数据或同步信息。

为了简化我们必须编写的代码，你将所有的 GStreamer 代码放在另一个文件中。如下所示创建 `playback.h`：

```c
#ifndef PLAYBACK_H
#define PLAYBACK_H

#include <gst/gst.h>

gboolean load_file(const gchar *uri);
gboolean play_file();
void stop_playback(void);
void seek_to(gdouble percentage);

#endif
```

该头文件为 `main.c` 调用所有它需要的函数提供了接口。修改 `main.c` 以包含 `playback.h`；创建 `playback.c`，它应该包含 `playback.h` 和 `main.h`。同时更新 `Makefile` 将 `playback.o` 链接到可执行文件中。然后搭建 `playback.c` 的基础。

```c
#include "main.h"
#include "playback.h"

static GstElement *play = NULL;
static guint timeout_source = 0;

gboolean load_file(const gchar *uri) {
  if (build_gstreamer_pipeline(uri)) return TRUE;
  return FALSE;
}
```

`build_gstreamer_pipeline()` 函数接收一个 URI 并构造一个 `playbin` 元素，其指针将存储在变量中供以后使用。

```c
static gboolean build_gstreamer_pipeline(const gchar *uri) {
  /* 如果已经有一个流水线，销毁它 */
  if (play) {
    gst_element_set_state(play, GST_STATE_NULL);
    gst_object_unref(GST_OBJECT(play));
    play = NULL;
  }
```
