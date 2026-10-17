
### 添加超时超时
`gtk_timeout_add()` 的第一个参数 `interval` 是一个无符号 32 位值，表示 Gtk+ 在计时器过期前必须等待的时间（毫秒）。一旦超时过期，就会调用 `gtk_timeout_add()` 函数参数指定的程序，并将 Gtk+ 通过 `data` 参数传递给该函数所指定的值作为其唯一参数传递给该函数。Gtk+ 中超时函数的原型如下：

```
guint
function( gpointer data )
```

如果超时函数返回非零值，Gtk+ 将重新启动计时器间隔，您的函数将在间隔过期后被调用一次。如果您的超时函数返回零，则超时将由 Gtk+ 注销且不再被触发。

### 移除超时
`gtk_timeout_add()` 返回一个类型为 `guint` 的唯一句柄。可以将此句柄传递给 `gtk_timeout_remove()`，以在超时被触发前将其取消注销。调用 `gtk_timeout_remove()` 等同于在超时函数被调用时返回零。使用超时的应用程序需要 `gtk_timeout_remove()` 来确保某些操作在指定的时间范围内完成。如果超时操作在超时触发之前已完成，则不再需要该超时，应用程序应通过调用 `gtk_timeout_remove()` 将其移除。

## 超时示例

让我们重新回顾邮件应用程序，看看如何应用 Gtk+ 超时。为了启用每隔 n 秒触发一次的邮件轮询功能，Gtk+ 邮件应用程序调用 `gtk_timeout_add()` 来指定轮询间隔，并向 Gtk+ 注册在每次间隔过期时将调用的函数。该程序将联系邮件服务器以确定是否有新邮件送达，并读取邮件头以确保在有新邮件送达时更新用户界面。超时应返回一个非零值；这将导致 Gtk+ 重置间隔，并在指定的间隔通过后再次调用超时函数。用户可能在任何时候想要禁用新邮件的轮询；这可以通过调用 `gtk_timeout_remove()` 轻松实现。用户也可能想更改间隔本身；这可以通过移除超时并调用 `gtk_timeout_add()` 重新注册来实现，调用时指定相同的函数和新的轮询间隔作为参数。

在超时函数内部，我们需要建立到邮件服务器的网络连接（假设它是从 POP 或 IMAP4 邮件服务器读取的），并发送请求请求远程邮箱状态的命令。在这两种情况下（即建立连接和发送状态请求时），我们都应该注册一个超时函数，以便在无法建立连接或服务器对我们发送的状态命令没有响应时不会被触发。如果在超时过期前发生了连接或我们收到了对状态更改的响应，则通过调用 `gtk_timeout_remove()` 移除超时。如果超时函数被触发，它可以对失败的连接和命令执行清理工作，并通过显示消息告知用户发生了失败。超时函数应该始终返回零，以确保不再被 Gtk+ 再次。

## 超时精度

需要意识到的一点是，这些超时是我所谓的“低精度的”，其意义在于 Gtk+ 在主循环的每次迭代中都会遍历一次注册的超时列表，将当前时间与超时应触发的时间进行比较，并触发那些自上一次检查列表以来间隔已过期的超时。因此，在触发超时时存在产生延迟的风险——Gtk 可能无法及时完成主循环的某次迭代来处理已过期的超时。例如，在时间 `$t_0$`，Gtk+ 可能会调用一个应用程序回调来响应某个事件。如果一个超时定于在时间 `$t_1$` ，而回调函数在 `$t_1$` 之后才返回主循环，那么 Gtk+ 就无法按预期在 `$t_1$` 时分发该超时。处理这个问题有两种方法。

第一种方法是确保分配给主循环操作的周期足够长，可能会可能会影响 Gtk+ 对超时的处理。这可以通过像之前描述的频繁调用 `gtk_main_iteration()` 来实现。每次调用将允许 Gtk+ 完成主循环的单通过，并处理任何可能触发的超时。

第二种方法是完全不使用 Gtk+ 超时，而是使用 UNIX `alarm(2)` 系统调用在应用程序中实现超时。虽然使用报警将消除任何延迟问题，但您的应用程序无法享受与 Gtk+ 超时相关的优势。

## 应用启动、终止与主循环函数

## 空闲函数

空闲函数与超时的不同在于，它们在每次通过主循环时被调用。因此，Gtk+ 无法保证空闲函数调用的频率。然而，与超时一样，这并不担心。

那么，在空闲函数中应该做什么呢？通回答是做任何需要长时间完成的任务。这类耗时任务可以可以是任何内容：渲染分形图像、从网络读取文件或计算质数。执行耗时任务不应阻碍用户与应用程序交互的能力，也不应阻碍应用程序响应系统事件的能力。像 Netscape 这样的程序如果不允许用户在长时间下载期间执行其他任务（如浏览网页或阅读新收到的消息），那将是非常不友。执行文件传输的程序通常会为用户提供取消操作的方法；在 GUI 中，这通常以“取消”按钮的形式出现。Gtk+ 必须在主循环中获得周期来处理与点击“取消”按钮关联的用户事件。Gtk+ 还需要周期来处理如窗口暴露之类的系统事件。编写良好的 GUI 应用程序会在暴露发生后重绘用户界面的暴露部分，而不是在文件传输完成后重绘。只有在应用程序执行的任务与 Gtk+ 主循环之间共享时间的情况下才能这一点。空闲函数是让这种情况发生的一种方法。

### 添加空闲函数

添加空闲函数与添加超时相似，但不需要指定间隔。向 Gtk+ 注册空闲函数的程序是 `gtk_idle_add()`：

```
guint
gtk_idle_add (GtkFunction function, gpointer data)
```

参数 `function` 是 Gtk+ 将调用的空闲函数，`data` 是传递给函数的类型为 `gpointer` 的参数。返回一个类型为 `guint` 的句柄；此句柄可用于移除空闲函数，正如我在本章稍后讨论的那样。返回零值的空闲函数将被 Gtk+ 销毁，除非重新注册，否则将不再被调用。非零返回值将确保空闲函数保留并在 gtk 主循环的下次迭代中等待被调用。

## 空闲函数优先级

空闲函数在调用 `gtk_idle_priority()` 注册时，可以由应用程序为其分配一个优先级值：

```c
guint
gtk_idle_add_priority(gint priority, GtkFunction function,
pointer data)
```

从功能上讲，`gtk_idle_add_priority()` 与 `gtk_idle_add()` 相同，只是多了一个参数。Gtk+ 和 Glib 头文件在表 2.4 中定义了优先级值。

### 表 2.4 优先级级别

| 优先级 | 值 |
|---|---|
| G_PRIORITY_HIGH | -100 |
| G_PRIORITY_DEFAULT | 0 |
| G_PRIORITY_HIGH_IDLE | 100 |
| G_PRIORITY_DEFAULT_IDLE | 200 |
| G_PRIORITY_LOW | 300 |
| GTK_PRIORITY_REDRAW | G_PRIORITY_HIGH_IDLE + 20 |
| GTK_PRIORITY_RESIZE | G_PRIORITY_HIGH_IDLE + 10 |
| GTK_PRIORITY_HIGH | G_PRIORITY_HIGH |
| GTK_PRIORITY_INTERNAL | GTK_PRIORITY_REDRAW |
| GTK_PRIORITY_DEFAULT | G_PRIORITY_DEFAULT |
| GTK_PRIORITY_LOW | G_PRIORITY_LOW |

Gtk+ 为通过 `gtk_idle_add()` 注册的空闲函数分配的默认优先级是 `GTK_PRIORITY_DEFAULT`。值越小优先级越高；越大优先级越低。如果应用程序需要，以 `GTK_PRIORITY_DEFAULT + 30` 注册空闲函数也是完全合理的。

相同优先级的空闲函数以轮询方式执行。Gtk+ 只执行所有已注册空闲函数中优先级最高的函数。优先级较低的空闲函数在较高优先级的空闲函数被销毁之前，将无法被调用。因此，应用程序在使用空闲函数时必须小心。如果应用程序注册了一个或多个更高级的空闲函数，且这些高优先级空闲函数从未被销毁，那么低优先级的空闲函数将会饥饿。Gtk+、Glib 或 GDK 可能会为了内部目的注册空闲函数；为了让这些空闲函数获得执行周期，应用程序必须确保不存在更高优先级的已注册空闲函数。

## 应用程序启动、终止、主循环函数

基本上，最安全的方法是使用 `gtk_idle_add()`，或使用带有 `GTK_PRIORITY_DEFAULT` 优先级的 `gtk_idle_add_priority()` 来注册空闲函数。如果你必须以 `GTK_PRIORITY_DEFAULT` 以外的优先级添加空闲函数，为了确保该函数不被高优先级空闲函数饥饿，且不会导致低优先级函数饥饿，最佳方法是从所有空闲函数中返回零，以确保它们在执行后后被销毁。需要调用多次的空闲函数应该赋予较低的优先级，或者以确保不会导致其他空闲函数饥饿的方式使用。

## 销毁空闲函数

如前所述，空闲函数在调用后，可以通过在函数内部返回 0 来取消注册或销毁。销毁空闲函数的另一种方法是调用 `gtk_idle_remove()`，并传递由 `gtk_idle_add_priority()` 或 `gtk_idle_add()` 返回的 `guint` 值：

```c
void
gtk_idle_remove(guint tag)
```

空闲函数也可以通过在创建时与其关联注册的用户数据来移除。这可以通过调用 `gtk_idle_remove_by_data()`，并将创建空闲函数时传递给 `gtk_idle_add()` 的 `gpointer` 参数作为参数来实现。`gtk_idle_remove_by_data()` 的函数原型如下：

```c
void
gtk_idle_remove_by_data(gpointer data)
```

## 监听按键

在本章中我想讨论的最后主循环例程包括 `gtk_key_snooper_install()` 和 `gtk_key_snooper_remove()`。这些例程序的函数原型如下：

```c
guint
gtk_key_snooper_install(GtkKeysSnoopFunc snooper, gpointer func_data)
```

```c
void
gtk_key_snooper_remove(guint snooper_id)
```

`gtk_key_snooper_install()` 接收的参数是一个监听函数的指针（在本章稍后描述）以及用户数据，这些数据会在每次被 Gtk+ 调用监听函数时传递给该函数。`gtk_key_snooper_install()` 返回一个唯一的 ID 或标签值。此 ID 可在调用 `gtk_key_snooper_remove()` 尝试移除时用于识别“按键监听器”。

监听函数的原型如下：

```c
gint
function(GtkWidget *widget, GdkKeyEvent *event, gpointer data)
```

参数 `widget` 是接收按键事件的控件。参数 `event` 是按键事件。`GdkKeyEvent` 定义如下：

```c
typedef struct _GdkKeyEvent {
  GdkEventType type;
  GdkWindow *window;
  gint send_event;
  guint2 time;
  guint state;
  guint keyval;
  gint length;
  gchar *string;
} GdkKeyEvent;
```

感兴趣的监听字段可能包括 `type`、`keyval` 和 `string`。`keyval` 是所按按键的 ASCII 码。`string` 是按键的字符串表示。`time` 是事件发生的时间。

# 44

# 第 2 章 • Hello Gtk+

```c
021 }
022
023 int
024 main(int argc, char *argv[])
025 {
026 GtktkWidget *window, *box, *entry;
027
028 gtk_set_locale();
029
030 gtk_init(&argc, &argv);
031
032 window = gtk_entry_new(GTK_WINDOW_TOPLEVEL);
033 gtk_window_title(GTK_WINDOW(window), "Enter Password");
034
035 box = gtk_box_new(FALSE, 0);
036 gtk_container_add(GTK_CONTAINER(window), box);
037
038 entry = gtk_entry_new();
039 gtk_entry_set_text(GTK_ENTRY(entry), "");
040 gtk_editable_select_region(GTK_EDITABLE(entry), 0, -1);
041 gtk_pack_start(GTK_BOX(box), entry, TRUE, 0);
042
043 gtk_key_snooper_install(foo, (gpointer) NULL);
044 gtk_widget_show_all(window);
045
046 gtk_main();
047
048 return (0);
050
```
