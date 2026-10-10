

# 事件、信号与回调函数

本章探讨使用事件模型时产生的一些问题。如果程序一直阻塞等待事件队列的输入，就没有机会从文件或通信链路读取数据。另一个问题在于，当你的程序正在处理数据时，它忽略了事件队列，同时也忽略了任何鼠标和键盘输入。

事件通过事件队列进入，它们被转换为信号，信号进而触发回调函数的调用。但由于代码中在许多不同位置定义了大量的信号，对于试图跟踪这些信号的程序员来说，这可能会变得非常令人困惑。而且很难跟踪哪些参数被传递给了哪些回调函数。

## 读取事件队列

*事件队列*是每个应用的核心。事件队列不仅提供来自用户鼠标和键盘的信息，还可以用作计时器以及进程间通信的方法。

你的应用初始化自身，然后调用 `gtk_main()` 函数，该函数直到进程停止时才返回。你可以通过在 `gtk_main()` 调用周围添加两个打印语句来验证这一点，如下所示：

```
g_print("The call to gtk_main()\n");
gtk_main();
g_print("The return from gtk_main()\n");
```

当程序运行时，第一行会立即显示（好吧，一旦程序完成自身初始化并准备好打开窗口）。第二行只有在你退出程序时才会显示。当然，如果你的程序崩溃或以其他方式突然停止运行，第二行永远不会显示。

外部进程或设备使用事件队列向你的程序发送信息。队列是只读的，因此如果你的程序需要与其他程序或设备通信，它必须使用其他方法。

事件有几种不同的类型。其中一些对应用没有实际影响，因为底层的 GTK+ 事件处理器完成了大部分工作。例如，如果窗口不再被遮挡，会到达一个事件，指定该窗口必须完全或部分重绘。但通常应用程序无需操心此事，因为 GTK+ 会处理它。然而，在某些情况下，你可能希望获得关于传入事件的更多信息。例如，如果你的应用程序使用鼠标输入在屏幕上绘制线条，你需要知道鼠标的位置以及是否按住了某个按钮。这些信息都包含在事件中，并传递给你的回调函数。

### 事件分发序列

发生某个事件（例如按下键盘上的按键），你的程序做出反应。可能有几个程序同时在运行，因此进程需要决定哪个进程接收关于该事件的信息，并需要一种机制将信息送达那里。以下步骤是对该过程的高级概述。

- 步骤 1：鼠标指针在显示屏上移动并按下一个按钮。这会导致硬件中断。
- 步骤 2：鼠标的软件驱动捕获中断，并将信息打包为系统标准格式。信息包括鼠标点击的 x 和 y 位置以及按下了哪个按钮。然后驱动将这些信息传递给注册了它的进程——在 X 的情况下，它是窗口管理器。
- 步骤 3：窗口管理器的职责是定位显示屏上的所有窗口并确定堆叠顺序（哪些窗口被其他窗口遮挡）。利用这些地理信息，窗口管理器确定哪个窗口刚刚收到了鼠标点击。对于键盘，过程略有不同，因为没有屏幕位置信息。有一个窗口拥有焦点，该窗口接收所有击键。
- 步骤 4：每当应用程序打开一个窗口时，它都是通过将信息发送给窗口管理器来实现的。这样，窗口管理器就拥有了每个窗口的事件队列地址。窗口管理器将数据打包为 X 的标准格式，并将其写入与所选窗口相关联的事件队列。
- 步骤 5：应用程序的主循环使用底层 X 函数从队列中读取事件。然后软件通过查找随消息而来的窗口 ID 来确定哪个控件应接收信号。GTK+ 随后将信息传递给一个函数，如 `gtk_signal_emit()`，该函数将信息重新格式化为信号并将其传递给控件。
- 步骤 6：控件定义的一部分是用于接收所有传入信号的函数。信息包含在定义每个对象的 struct 中。
- 步骤 7：控件查看与此特定信号连接的一组回调函数列表，并调用它们全部。鼠标按钮被按下意味着它已到达最终目的地。

## 发出你自己的信号

有方法通过生成信号来模拟事件，而无需经过实际的事件队列。你可以使用 `gtk_signal_emit()` 函数来创建信号，但这样做需要你了解内部信号 ID 号。使用 `gtk_signal_emit_by_name()` 可能更容易，因为它只需要信号的文本书名和接收信号的对象的指针。此示例展示了如何发送你自己的信号：

```c
/* simsinal.c **/
#include <gnome.h>

GtkWidget *makeButtonBox();
gint eventDelete(GtkWidget *widget,
    GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget,
    GdkEvent *event, gpointer data);
void buttonFirstCallback(GtkWidget *widget,
    GdkEvent *event, gpointer data);
void buttonSecondCallback(GtkWidget *widget,
    GdkEvent *event, gpointer data);

GtkWidget *buttonFirst;
GtkWidget *buttonSecond;

int main(int argc, char *argv[])
{
    GtkWidget *window;
    GtkWidget *buttonbox;

    gnome_init("simsignal", "1.0", argc, argv);
    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_signal_connect(GTK_OBJECT(window), "delete_event",
            GTK_SIGNAL_FUNC(eventDelete), NULL);
    gtk_signal_connect(GTK_OBJECT(window), "destroy",
            GTK_SIGNAL_FUNC(eventDestroy), NULL);

    buttonbox = makeButtonBox();

    gtk_container_add(GTK_CONTAINER(window), buttonbox);
    gtk_widget_show_all(window);
    gtk_main();
    exit(0);
}

GtkWidget *makeButtonBox() {
    GtkWidget *buttonbox;

    buttonbox = gtk_hbutton_box_new();
    gtk_container_set_border_width(
            GTK_CONTAINER(buttonbox), 10);

    buttonFirst = gtk_button_new_with_label("First");
    gtk_container_add(GTK_CONTAINER(buttonbox),
            buttonFirst);
    gtk_signal_connect(GTK_OBJECT(buttonFirst),
            "clicked",
            GTK_SIGNAL_FUNC(buttonFirstCallback),
            NULL);

    buttonSecond = gtk_button_new_with_label("Second");
    gtk_container_add(GTK_CONTAINER(buttonbox),
            buttonSecond);
    gtk_signal_connect(GTK_OBJECT(buttonSecond),
            "clicked",
            GTK_SIGNAL_FUNC(buttonSecondCallback),
            NULL);

    return(buttonbox);
}

void buttonFirstCallback(GtkWidget *widget,
            GdkEvent *event, gpointer data) {
    g_print("Clicked: First\n");
}

void buttonSecondCallback(GtkWidget *widget,
            GdkEvent *event, gpointer data) {
    gtk_signal_emit_by_name(GTK_OBJECT(buttonFirst),
```

### 本章内容

- 接收并使用从鼠标和键盘发送到你的程序的事件
- 理解事件的起源及其到达你程序的路径
- 学习事件如何命名和编号，以便你知道你的程序应该期望什么
- 发出你自己的自定义事件消息，使它们出现在输入队列中
- 使用输入事件队列作为实现计时器和后台处理的一种方式

