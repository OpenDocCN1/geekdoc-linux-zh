
| | 第 1 列 | 第 2 列 | 第 3 列 | 第 4 列 | 第 5 列 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| fg_gc: | 0x8075fb0 | 0x8075fb0 | 0x8075fb0 | 0x8076490 | 0x8076758 |
| bg_gc: | 0x8076520 | 0x80766d0 | 0x80767f0 | 0x8076910 | 0x8076520 |
| light_gc: | 0x8076490 | 0x8076490 | 0x8076490 | 0x8076490 | 0x8076490 |
| dark_gc: | 0x80765b0 | 0x8076760 | 0x8076880 | 0x8076b38 | 0x80765b0 |
| mid_gc: | 0x8076640 | 0x8076640 | 0x8076520 | 0x8076ec3 | 0x8076640 |
| text_gc: | 0x8075fb0 | 0x8075fb0 | 0x8075fb0 | 0x8076490 | 0x8076520 |
| base_gc: | 0x8076490 | 0x8076490 | 0x8076490 | 0x8076490 | 0x8076490 |
| | | | | | 0x8076758 |
| | | | | | 0x8076520 |
| | | | | | 0x8076490 |
| | | | | | 0x80765b0 |
| | | | | | 0x8076640 |
| | | | | | 0x8076520 |
| | | | | | 0x8076490 |
| bgPixmap: | 0x0000000 | 0x0000000 | 0x0000000 | 0x0000000 | 0x0000000 |

```
20    GtkStyle *current;
21    GtkStyle *new;
22    GdkBitmap *mask;
23
24    gnome_init("stylemod", "1.0", argc, argv);
25    app = gnome_app_new("stylemod", "GtkStyle");
26    gtk_container_set_border_width(GTK_CONTAINER(app), 40);
27    gtk_signal_connect(GTK_OBJECT(app), "delete_event",
28    GTK_SIGNAL_FUNC(eventDelete), NULL);
29    gtk_signal_connect(GTK_OBJECT(app), "destroy",
30    GTK_SIGNAL_FUNC(eventDestroy), NULL);
31
32    gtk_widget_show(app);
33
34    button = gtk_button_new_with_label("Button");
35    gtk_widget_set_usize(button, 100, 100);
36
37    current = gtk_widget_get_default_style();
38    new = gtk_style_copy(current);
39
40    new->bg[GTK_STATE_ACTIVE] = green;
41    new->bg[GTK_STATE_PRELIGHT] = red;
42    new->bg[GTK_STATE_NORMAL] = cyan;
43    new->bg_pixmap[GTK_STATE_NORMAL] =
44    gdk_pixmap_create_from_xpm_d(app->window,
45    &mask, &new->bg[GTK_STATE_NORMAL],
46    (gchar **)module);
47    gtk_widget_set_style(button, new);
48
49    gnome_app_set_contents(GNOME_APP(app), button);
50    gtk_widget_show_all(app);
51
52    gtk_main();
53    exit(0);
54    }
55    gint eventDelete(GtkWidget *widget,
56    GdkEvent *event, gpointer data) {
57    return(FALSE);
58    }
59    gint eventDestroy(GtkWidget *widget,
60    GdkEvent *event, gpointer data) {
61    gtk_main_quit();
62    return(0);
63    }
```

在第 24 到 30 行 `GN0ME` 环境初始化完成后，立即在第 32 行通过 `gtk_widget_show()` 调用顶层应用程序窗口。这种初始化是必要的，因为它创建了一个颜色映射（color map），并使设置小部件样式所需的信息可用。样式可以稍后设置——在所有小部件显示之后——但初始化允许我们在小部件显示之前对其进行配置。

第 34 行和第 35 行调用 `gtk_button_new_with_label()` 和 `gtk_widget_set_usize()` 来创建一个大型按钮。

第 37 行获取当前的默认 `GtkStyle`。这是应用于所有未拥有自身样式的小部件的样式。虽然可以创建一个全新的样式，但这意味着需要填充 `GtkStyle` 结构体的每个成员——更常规的做法是从默认样式开始并简单地进行修改。现在，由于 `gtk_widget_get_default_style()` 返回的是一个指针，且该指针被程序中的所有小部件共用，直接修改默认样式会改变应用程序中所有小部件的样式。我们需要修改它的副本，因此在第 38 行调用 `gtk_style_copy()` 来创建默认 `GtkStyle` 的精确副本。

在复制的 `GtkStyle` 结构体中，第 40 行到第 42 行分配用于指示激活（active）、预亮（prelight）和正常（normal）状态的颜色。这些颜色在第 12 行到第 14 行定义，无需显式分配这些颜色——每当 `GtkStyle` 添加到一个小部件时，它们会被自动分配。

第 43 行创建一个像素图（pixmap），并将其安装用于按钮处于正常状态时。`gdk_pixmap_create_from_xpm_d()` 的调用使用主应用程序小部件的窗口和颜色映射信息，以及包含在第 4 行中的像素图定义。像素图是为活动状态设置的，因此该状态的背景颜色在第 45 行提供给像素图创建函数。最终生成的按钮如图 14-3 所示。像素图远小于按钮，但它会被重复平铺并填充整个按钮区域。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_462_0.png)

### 图 14-3：显示像素图样式的按钮

新的样式信息通过在第 47 行调用 `gtk_widget_set_style()` 设置到小部件中。第 49 行和第 50 行将按钮添加到主窗口，并且对 `gtk_widget_show_all()` 的调用导致包含按钮的窗口得以显示。

前面的示例展示了如何为单个小部件分配样式。要对多个小部件应用特殊样式，你可以为每一个调用 `gtk_widget_set_style()`——或者你可以暂时设置默认样式。例如，以下代码使用一个新创建的 `GtkStyle` 对象来创建多个小部件：

```
current = gtk_widget_get_default_style();

new = gtk_style_copy(current);

/* Make modification to new style */

gtk_widget_push_style(new);

/* Create new widgets */

gtk_widget_pop_style();
```

调用 `gtk_widget_push_style()` 会用新样式替换默认样式，并保存现有样式；调用 `gtk_widget_pop_style()` 则恢复原样式。你可以使用此方法对一组小部件的外观进行特殊调整。并且，由于这是一个压入-弹出（push-pop）的情况，调整组内的小部件可以进行各自的调整。

如果你有一个已经修改过样式的小部件，并且需要创建另一个具有相同修改的小部件，请这样做：

```
style = gtk_widget_get_style(existingWidget);

gtk_widget_set_style(newWidget, style);
```
