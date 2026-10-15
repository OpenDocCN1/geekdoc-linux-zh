
```c
GtkWidget *display;

gnome_init("timing", "1.0", argc, argv);

window = gtk_window_new(GTK_WINDOW_TOPLEVEL);

gtk_container_set_border_width(GTK_CONTAINER(window), 20);

gtk_signal_connect(GTK_OBJECT(window), "delete_event", GTK_SIGNAL_FUNC(eventDelete), NULL);
gtk_signal_connect(GTK_OBJECT(window),"destroy", GTK_SIGNAL_FUNC(eventDestroy),NULL);

display = makeDisplay();
gtk_container_add(GTK_CONTAINER(window),display);
gtk_widget_show_all(window);
gtk_main();
exit(0);
}

GtkWidget *makeDisplay() {
    GtkWidget *box;
    box = gtk_vbox_new(FALSE,0);
    oneSecondLabel = gtk_label_new("One Second Timer");
    gtk_box_pack_start(GTK_BOX(box),oneSecondLabel, FALSE,FALSE,0);
    tenSecondLabel = gtk_label_new("Ten Second Timer");
    gtk_box_pack_start(GTK_BOX(box),tenSecondLabel, FALSE,FALSE,0);
    tenSecondTag = gtk_timeout_add(10000, (GtkFunction)tenSecondCallback,NULL);
    return(box);
}

gchar *getTimeString()
{
    struct tm *t;
    time_t tt;
    gchar *string;
    tt = time(NULL);
    t = localtime(&tt);
    string = asctime(t);
    string[strlen(string)-1] = '\0';
    return(string);
}

gint oneSecondCallback(gpointer data)
{
    gtk_label_set_text(GTK_LABEL(oneSecondLabel), getTimeString());
    return(TRUE);
}

gint tenSecondCallback(gpointer data)
{
    gtk_label_set_text(GTK_LABEL(tenSecondLabel), getTimeString());
    if(oneSecondRunning) {
        gtk_timeout_remove(oneSecondTag);
        oneSecondRunning = FALSE;
    } else {
        oneSecondTag = gtk_timeout_add(1000, (GtkFunction)oneSecondCallback,NULL);
        oneSecondRunning = TRUE;
    }
    return(TRUE);
}

gint eventDelete(GtkWidget *widget, GdkEvent *event,gpointer data) {
    return(FALSE);
}

gint eventDestroy(GtkWidget *widget, GdkEvent *event,gpointer data) {
    gtk_main_quit();
    return(0);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_195_0.png)

由第 39 行函数 `makeDisplay()` 构建的窗口，由一个垂直框中的两个标签组成。第 51 行对 `gtk_timeout_add()` 的调用设置了一个每 10,000 毫秒（10 秒）触发一次的计时器。当它触发时，会调用名为 `tenSecondCallback()` 的回调函数。最后一个参数（`NULL` 值）是所有回调函数标准的可选数据指针。

第 56 行的函数 `getTimeString()` 仅仅是一个便捷函数，用于创建一个包含当前日期和时间的字符串，且末尾没有传统的 `'\n'`。

第 68 行的回调函数 `oneSecondCallback()` 通过调用 `gtk_label_set_text()` 使用日期和时间字符串来更新其标签的文本。返回 `TRUE` 告诉系统，调用了此函数的计时器应该重新开始计时，并在另一个时间间隔过期后再次调用该函数。此处如果返回 `FALSE`，计时器将停止，除非专门安排执行，否则回调不会再次被执行。

第 74 行的回调函数 `tenSecondCallback()` 执行了 `oneSecondCallback()` 函数所做的所有事情，但它还启动和停止秒级计时器。如果秒级计时器正在运行（由布尔变量 `oneSecondRunning` 指示），则将其停止；如果它没有运行，则将其启动。第 79 行通过对 `gtk_timeout_remove()` 的调用停止了计时器，使用的是第 82 行启动计时器运行时调用 `gtk_timeout_add()` 返回的标签。

### 从文件或套接字读取输入

有几种方法可以将数据从其他位置获取到 Linux 程序中。Linux 程序从一个文件读取数据，而另一个进程正在写入该文件，这种情况并不少见。还可以创建套接字并使用它建立 TCP/IP 链接，以便通过互联网链路进行通信。还有 FIFO（先进先出）文件和管道。为了让你的程序从这些来源之一读取输入，你的程序必须阻止自身并持续读取输入，或者时不时地检查输入状态以查看是否有数据到达。

使用事件队列的一个问题是，你的进程不能阻塞并等待来自其他位置的输入。如果你需要在数据可用时从套接字或文件中读取数据，你不能简单地阻塞并等待输入，因为程序无法处理事件。因此，它将表现为死机，因为它不再响应鼠标或键盘。你可以使用如前一节中所述的计时回调，但这有双重缺点。首先，它通过不断调用函数增加了进程开销。其次，直到计时器过期，你的进程才能检测到新的输入。

GDK 库中有一个功能，可用于在套接字或文件中有输入可用时生成回调。文件和套接字的机制是相同的——它们都使用 `int` 值作为文件描述符进行工作。

下面的程序展示了如何使用这一功能。为了简化示例代码，使用的是已经打开的标准输入。该程序显示一个带有单个按钮的窗口。它还设置为响应按钮点击，同时从标准输入读取输入。

```c
/** inputadd.c **/
#include <fcntl.h>
#include <gnome.h>

gint eventDelete(GtkWidget *widget, GdkEvent *event,gpointer data);
gint eventDestroy(GtkWidget *widget, GdkEvent *event,gpointer data);
void inputSetup();
void inputCallback(gpointer data,gint fd, GdkInputCondition in);

GtkWidget *button;
int main(int argc,char *argv[])
{
    GtkWidget *window;
    gnome_init("inputadd", "1.0", argc, argv);
    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
```
