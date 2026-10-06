
```c
#include <stdio.h>
#include <time.h>
#include <gtk/gtk.h>
#include <unistd.h>
#include <signal.h>

static GtkWidget *drawing;
static int count = 1;

void AlarmFunc(int foo)
{
  GdkEvent event;
  gint retval;

  gtk_signal_emit ( GTK_OBJECT (drawing),
  gtk_signal_lookup ("motion_notify_event",
  GTK_OBJECT_TYPE (drawing) ), &event, &retval );
  alarm(1);
}

void motion_notify_callback(GtkWidget *w, GdkEvent *event, char *arg)
{
  fprintf("motion_notify_callback %s%d\n", arg, count++);
  fflush( stderr );
}

void Exit(GtkWidget *widget, gpointer arg)
{
  gtk_main_quit();
}

int main(int argc, char *argv[])
{
  GtkWidget *window, *box;
  struct sigaction old, act;

  gtk_set_locale();
  gtk_init(&argc, &argv);
  window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
  gtk_signal_connect(GTK_OBJECT(window), "destroy",
  GTK_SIGNAL_FUNC(Exit), NULL);
  gtk_window_set_title(GTK_WINDOW (window), "Events");
  gtk_container_border_width (GTK_CONTAINER (window), 0);
  box = gtk_vbox_new(FALSE, 0);
  gtk_container_add (GTK_CONTAINER (window), box);
  gtk_widget_set_events (drawing, GDK_POINTER_MASK);
  gtk_signal_connect (GTK_OBJECT(drawing), "motion_notify_event",
  GTK_SIGNAL_FUNC (motion_notify_callback), "Hello World" );
  gtk_pack_start (GTK_BOX (box), drawing, TRUE, 0);
  gtk_widget_show_all (window);

  act.sa_handler = AlarmFunc;
  act.sa_flags = 0;
  sigaction ( SIGALRM, &act, &old);
  alarm( 1 );
  gtk_main ();
  sigaction ( SIGALRM, &old, NULL );
  return ( 0 );
}
```

## 示例分析

在第 58 行，创建一个 `GtkDrawingArea` 小部件，然后在第 59 行和 70 行将 `GtkDrawingArea` 小部件的事件掩码设置为 `GTK_POINTER_MASK`，启用了该小部件的运动事件通知。在第 61 行和 62 行，在第 23 行到 29 行实现的信号回调函数 `motion_notify_callback()` 被注册到 Gtk+，以便在接收到 `GtkDrawingArea` 小部件的运动事件时调用。

```c
58 drawing = gtk_drawing_area_new();
59 gtk_widget_set_events (drawing, GTK_POINTER_MASK);
61 gtk_signal_connect (GTK_OBJECT (drawing), "motion_notify_event",
62 GT_SIGNAL_FUNC (motion_notify_callback), "Hello World" );
```

在第 70 行，我们使用 POSIX 信号函数 `signal(2)` 注册一个 `SIGALRM` 信号处理器 `AlarmFunc()`，它实现在第 009 行到 020 行。然后，在第 70 行，我们调用 `alarm(2)` 使 `SIGALRM` 信号在一秒后触发。当 `SIGALRM` 被触发时，进入 `AlarmFunc`。

```c
009 void
010 AlarmFunc( int foo );
011 {
012 GdkEvent event;
013 gint retval;

015
016 gtk_signal_emit ( GTK_OBJECT (drawing),
017 gtk_signal_lookup ("motion_notify_event",
018 GTK_OBJECT_TYPE (drawing) ), &event, &retval );
019 alarm(1 );
020 }
```

在 `AlarmFunc()` 中，我们调用 `gtk_signal_emit()` 在名为 `drawing` 的 `GtkDrawingArea` 小部件关联窗口上生成一个 `motion_notify_event`。这将 Gtk+ 调用我们的信号回调函数 `motion_notify_callback()`。`motion_notify_callback()` 仅仅打印一条包含序列号和与信号回调函数注册的应用程序相关数据（字符串 `"Hello World"`）的消息。

我在示例中使用 `alarm(2)` 有两个原因。第一个是 `alarm(2)` 提供了一种生成异步事件的方便方法

一个固定间隔，这给了我生成 `motion_notify_events` 的机会，以说明本示例的中心思想。使用 `alarm()` 的第二个原因是指出一个术语上的混淆点。需要注意的是，Gtk+/GTK 中的信号（signals）与 `signal(7)` 中描述的 UNIX 信号不同，后者是由 UNIX 函数 `signal(2)` 和 `kill(2)` 处理的。

确实存在某些时候向自己发送信号是合适的。。在本书稍后的部分讨论 `GtkDrawingArea` 时，我会给出一个例子。

## 控制信号

Gtk+ 提供了几个函数，允许应用程序以多种方式控制信号。其中第一个函数是 `gtk_signal_emit_stop()`：

```c
void
gtk_signal_emit_stop(GObject *object, gint signal_type)
```

`gtk_signal_emit_stop()` 函数停止信号的发射。信号发射定义为调用所有针对给定信号类型在小部件上注册的信号回调函数。例如，如果应用程序为某个事件注册了数十个回调函数，那么当事件发生时，该信号的发射将开始，并持续直到应用程序注册的每个回调函数都被调用。参数 `signal_type` 的获取方式与传递给 `gtk_signal_emit()` 的同名参数相同。如果你愿意通过名称而不是 `signal_type` 来标识信号，请调用 `gtk_signal_emit_stop_by_name()`：

```c
void
gtk_signal_emit_stop_by_name(GObject *object, char *name)
```

示例应该能解释得很清楚。我稍微修改了之前的示例，使得 `GtkDrawingArea` 小部件上注册了五个不同的信号回调函数：

```c
gtk_signal_connect( GTK_OBJECT(drawing), "motion_notify_event",
GTK_SIGNAL_FUNC(motion_notify_callback1), "Hello World");
gtk_signal_connect( GTK_OBJECT(drawing), "motion_notify_event",
GTK_SIGNAL_FUNC(motion_notify_callback2), "Hello World");
gtk_signal_connect( GTK_OBJECT(drawing), "motion_notify_event",
GTK_SIGNAL_FUNC(motion_notify_callback3), "Hello World");
gtk_signal_connect( GTK_OBJECT(drawing), "motion_notify_event",
GTK_SIGNAL_FUNC(motion_notify_callback4), "Hello World");
gtk_signal_connect( GTK_OBJECT(drawing), "motion_notify_event",
GTK_SIGNAL_FUNC(motion_notify_callback5), "Hello World5");
```

每个回调函数（`motion_notify_callback1()` 等）都会在 `AlarmFunc()` 调用 `gtk_signal_emit(1)` 后由 `GtkDrawingArea` 小部件调用。如果我修改每个回调函数，在 [0,100] 范围内生成一个随机数。如果随机数小于 50，那么信号回调函数将调用 `gtk_signal_emit_stop_by_name()` 来停止信号的发射。例如：

## 信号查找

```c
012 #define RAND( value ) ( ((float) random() / RAND_MAX) * value )
```

```c
...
```

```c
027 static void
028 motion_notify_callback1(GtkWidget *widget, GdkEventMotion *event, char
029   *arg)
030 {
031   static int count = 1;
032
033   printf(stderr, "In motion_notify_callback1 %s %03d\n", arg, count++);
034   fflush(stderr);
035   if (RAND (100) < 50)
036     gtk_signal_stop_by_name(GTK_OBJECT (drawing),
037     "motion_notify_event");
038 }
```

这种更改的效果是，其中一个信号回调函数生成了小于 50 的随机数，剩余的信号回调函数将不会被用于信号发射，因为信号发射已停止。在测试此函数时，`motion_notify_callback2()` 被调用的次数大约是 `motion_notify_callback1()` 的一半，`motion_notify_callback3()` 的次数大约是 `motion_notify_callback2()` 的一半，以此类推。至少这证明我的随机数宏执行得大致符合预期。

请注意，我们在信号发射停止后不会重新连接信号回调函数。下一次生成信号时，所有函数将再次具备空操作（no-op）的资格。此外，对一个未发射的信号调用 `gtk_signal_stop()` 是一个空操作。

我提到过使用 `gtk_signal_connect()` 连接信号会导致信号函数在之前为该小部件注册的所有信号函数以及为该小部件实现的默认类函数之后被调用。然而，应用程序可以通过通过 `gtk_signal_connect_after()` 注册回调，安排信号回调函数在另一个信号回调函数之后被调用：

```c
gint
gtk_signal_connect_after(GObject *object, gchar *name,
GtkSignalFunc func, gpointer func_data)
```

将信号连接到信号回调的稍有不同的方法是调用 `gtk_signal_connect_object()`，其原型如下：

```c
gint
gtk_signal_connect_object(GObject *object, gchar *name,
GtkSignalFunc func, GObject *slot_object)
```

`gtk_signal_connect_object()` 和 `gtk_signal_connect()` 之间的主要区别在于 `gtk_signal_connect_object()` 允许关联一个 `slot_object`。

## 信号、事件与类型

使用 `gtk_signal_connect()` 连接信号会导致信号函数在之前为该小部件注册的所有信号函数以及为该小部件实现的默认类函数之后被调用。然而，应用程序可以通过 `gtk_signal_connect_after()` 注册回调，安排信号回调函数在另一个信号回调函数之后被调用。

## 信号查找

Gtk+ 提供了两个函数，允许应用程序断开已注册的信号回调函数。第一个是 `gtk_signal_disconnect()`：

```c
void
gtk_signal_disconnect(GObject *object, gint id)
```

参数是注册信号的对象，对应于传递给 `signal_connect*` 族函数的第一个参数。正如我所指出的，一个信号可以注册多个信号回调函数，因此 `gtk_signal_disconnect()` 需要 `id` 来标识要断开哪一个信号回调函数。`id` 是用于连接信号回调函数的 `signal_connect*` 函数的返回值。在以下示例中，信号回调函数连接到一个点击信号，然后立即被断开，以说明所涉及的技术：

```c
GtkWidget *button;
gint id;

button = gtk_button_new_with_label("Close");
id = gtk_signal_connect_object(GTK_OBJECT(button), "clicked",
GTK_SIGNAL_FUNC(gtk_widget_destroy), GTK_OBJECT(window));
gtk_signal_disconnect(GTK_OBJECT(button), id);
```

`gtk_signal_disconnect_by_data()` 执行的操作与 `gtk_signal_disconnect()` 相同，但它不是通过 `id` 标识信号回调函数，而是通过作为 `gtk_signal_connect()` 或 `gtk_signal_connect_after()` 的 `func_data` 参数的应用数据，或者通过传递给 `gtk_signal_connect_object()` 或 `gtk_signal_connect_object_after()` 的 `slot_object` 参数来标识。这里是该函数原型：

```c
void
gtk_signal_disconnect_by_data(GObject *object, gpointer data)
```

通过调用一次 `gtk_signal_disconnect_by_data(data)` 可以断开多个信号回调函数，因为注册在该对象或应用程序数据上的所有信号回调函数都将被此函数断开。

相似的函数 `gtk_signal_handler_block_by_data()` 执行与 `gtk_signal_handler_block()` 相同的任务，但该参数被用于识别要阻塞的信号回调函数（函数）。这类似于 `gtk_signal_disconnect_by_data()` 使用 `data` 参数来识别要断开连接的信号回调函数的方式。以下是 `gtk_signal_handler_block_by_data()` 的函数原型：

```
void
gtk_signal_handler_block_by_data (GObject *object, gint data);
```

阻塞信号处理器的参数与调用 `gtk_signal_emit_stop()` 停止信号发射不是一回事。当信号发射被停止时，仅针对触发单个事件时相应的发射。下一次该事件或信号被触发时，每个信号回调都将再次可以被调用。当一个信号回调被阻塞时，在它被取消阻塞之前，不会被调用，无论信号或事件被触发了多少次。

注册到对象上的每个信号回调都维护一个“阻塞”计数，该计数从 0 开始，每次通过调用 `gtk_signal_handler_*` 函数阻塞信号时，计数就会加 1。

被阻塞的信号回调函数可以随时通过调用 `gtk_signal_handler_unblock` 来取消阻塞：

```
void
gtk_signal_handler_unblock (GObject *object, gint data);
```

这将对象的阻塞计数减 1。当计数变为零时，由 id 标识的对象的信号回调在下一次信号或事件触发时将变得可以被调用。

```
void
gtk_signal_handler_unblock_by_data (GObject *object, gint data);
```

与 `gtk_signal_disconnect_by_data()` 类似，它有能力取消多个信号回调函数的阻塞。

在本节中，我将讨论的操作信号的最后一个函数是 `gtk_signal_handlers_destroy()`：

```
void
gtk_signal_handlers_destroy (GObject *object);
```

`gtk_signal_handlers_destroy(object)` 会破坏所有注册到指定对象上的信号回调。然而，这不会销毁由对象或控件实现的类信号和事件函数。

## 对象
