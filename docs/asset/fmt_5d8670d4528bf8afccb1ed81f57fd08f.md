
```c
gtk_signal_connect( GTK_OBJECT (drawing), "motion_notify_event",
    GTK_SIGNAL_FUNC(motion_notify_callback1), "Hello World1");
gtk_signal_connect( GTK_OBJECT (drawing), "motion_notify_event",
    GTK_SIGNAL_FUNC(motion_notify_callback2), "Hello World2");
gtk_signal_connect( GTK_OBJECT (drawing), "motion_notify_event",
    GTK_SIGNAL_FUNC(motion_notify_callback3), "Hello World3");
gtk_signal_connect( GTK_OBJECT (drawing), "motion_notify_event",
    GTK_SIGNAL_FUNC(motion_notify_callback4), "Hello World4");
gtk_signal_connect( GTK_OBJECT (drawing), "motion_notify_event",
    GTK_SIGNAL_FUNC(motion_notify_callback5), "Hello World5");
```

每个信号回调函数（`motion_notify_callback1()` 等）将在 `AlarmFunc()` 调用 `gtk_signal_emit()` 后由 `GtkDrawingArea` 部件调用。然后我修改了每个回调函数，使其在 [0,100] 范围内生成一个随机数。如果随机数小于 50，那么信号回调函数将调用 `gtk_signal_stop_by_name()` 来停止信号的发射。

## 信号查找

```c
012 #define RAND( value ) ( ((float) random() / RAND_MAX ) * value )
...
```

```c
027 static void
028 motion_notify_callback1(GtkWidget *widget, GdkEventMotion *event, char
029     *arg)
030 {
031     static int count = 1;
033     fprintf(stderr, "In motion_notify_callback1 %s %03d\n", arg, count++);
034     fflush(stderr);
035     if (RAND (100) < 50)
036         gtk_signal_stop_by_name (GTK_OBJECT (drawing),
037             "motion_notify_event");
038 }
```

该更改的效果是：其中一个信号回调函数生成一个低于 50 的随机数；剩余的信号回调函数将不会被调用，因为信号发射将停止。在测试此函数时，`motion_notify_callback2()` 被调用的频率大约是 `motion_notify_callback1(1)` 的一半，`motion_notify_callback3()` 被调用的频率大约是 `motion_notify_callback2(2)` 的一半，依此类推。至少这证明了我们的随机数宏执行得大致符合预期。

请注意，在发射停止后，我们需要重新连接信号回调函数。当下一次产生信号时，所有函数将再次获得调用资格。此外，对于未发射的信号调用 `gtk_signal_stop(*)` 是一个空操作（no-op）。

我提到过使用 `gtk_signal_connect()` 连接信号会导致注册的信号函数在之前为该控件注册的该信号的所有信号函数以及该控件实现的默认类信号函数之后被调用。然而，应用程序可以通过 `gtk_signal_connect_after()` 注册回调，安排信号回调函数在信号回调函数之后被调用：

```c
gint
gtk_signal_connect_after(GObject *object, gchar *name,
    GtkSignalFunc func, gpointer func_data)
```

连接信号到信号回调函数的另一种稍有不同的方法是调用 `gtk_signal_connect_object()`，其原型如下：

```c
gint
gtk_signal_connect_object(GObject *object, gchar *name,
    GtkSignalFunc func, GObject *slot_object)
```

`gtk_signal_connect_object()` 和 `gtk_signal_connect_after()` 之间的主要区别体现在 `gtk_signal_connect*` 函数的原型以及被调用的回调函数中。

## 第 3 章 • 信号、事件、对象和类型

`gtk_signal_connect()` 和 `gtk_signal_connect_after()` 的最后一个参数是应用程序私有数据。使用 `gtk_signal_connect()` 和 `gtk_signal_connect_after()` 注册的回调函数的第一个参数是注册该信号回调函数的控件或对象。相比之下，`gtk_signal_connect_object()` 的最后一个参数是一个 `GObject` 指针，该指针是信号或事件被触发时传递给信号回调函数的第一个（也是唯一的）参数。其效果是：在注册了信号回调函数的控件中发生的事件将调用一个回调函数，就好像该事件发生在另一个对象中一样。

函数 `gtk_signal_connect_object_after()` 类似于 `gtk_signal_connect_after()`，因为信号回调函数将在控件的默认类信号函数调用之后被调用。

```c
gint
gtk_signal_connect_object_after(GtkObject *object, gchar *name,
GtkSignalFunc func, GtkObject *slot_object)
```

`gtk_signal_connect_object()` 的经典示例是将显示按钮的对话框或窗口的析构结合。以下来自 `testgttk.c` 的代码片段（它是 Gtk+ 分中的一个示例应用程序）说明了如何实现这一点：

```c
GtkWidget button, *box2;
```

```c
button = gtk_button_new_label("Close");
gtk_button_pack_start(GTK_BOX (box2), button, TRUE, TRUE, 0);
gtk_signal_connect_object(GTK_OBJECT (button), "clicked",
GTK_SIGNAL_FUNC(gtk_widget_destroy), GTK_OBJECT (window));
```

在这里，由 `GtkButton` 对象的点击信号注册到由 `button` 定义的实例中。当 "clicked" 信号触发时，将调用 `gtk_widget_destroy()` 函数。`gtk_widget_destroy()` 的函数原型如下：

```c
void
gtk_widget_destroy(GtkWidget*widget);
```

请注意，`gtk_widget_destroy()` 只接受一个参数，在这种情况下是一个待销毁的控件。传递给 `gtk_widget_destroy()` 的控件参数与作为最后一个参数传递给 `gtk_signal_connect_object()` 的对象是同一个对象。

你使用这种技术的唯一可能是在处理简单对话框的析构时，例如向用户显示错误或消息。通常不需要应用程序信号回调函数来处理此类对话框的取消或关闭，因此前面的技术效果良好。然而，如果你有一个允许用户进行更改的对话框，你可能希望为“取消”或“关闭”按钮的“clicked”信号注册一个应用程序特定的信号回调函数，以便你的...

## 信号查找

我提到过使用 `gtk_signal_connect()` 连接信号会导致注册的信号函数在之前为该控件注册的该信号的所有函数以及该控件实现的默认类信号函数之后被调用。然而，应用程序可以通过 `gtk_signal_connect_after()` 注册回调，安排信号回调函数在信号回调函数之后被调用：

```c
gint
gtk_signal_connect_after(GObject *object, gchar *name,
    GtkSignalFunc func, gpointer func_data)
```

连接信号到信号回调函数的另一种稍有不同的方法是调用 `gtk_signal_connect_object()`，其原型如下：
