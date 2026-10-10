
### GTK 主循环退出

```c
/* -- Do not return until gtk_main_quit is called -- */

gtk_main ();

/* -- Exit status code -- */

return 0;

}
```

注意，当窗口销毁时，启动应用程序的控制台会显示“Quitting...” 消息。该消息的显示是因为回调函数的执行。`gtk_main` 函数处于循环中，处理事件，直到你尝试关闭窗口。当你尝试关闭窗口时，会调用 `destroyapp` 函数来通知应用程序已通过 `gtk_signal_connect` 注册的 `delete_event` 信号。`destroyapp` 函数知道关闭主窗口应该结束 `gtk_main_quit` 函数，从而终止在应用程序中启动的 `gtk_main` 循环。该程序变成了一个简单且良好的 GTK+ 应用程序。在之前的程序中，生成了 `delete_event` 信号，但应用程序没有事件处理器来处理它。通过回调函数发出信号，应用程序干净地退出。

## 添加小部件

一个没有菜单或控件的空白窗口可能是一个应用程序，但它很难算是一个实用的应用程序。你可以通过为你之前创建的空白窗口添加功能来开始编写应用程序；在这种情况下，你可以向窗口添加一个小部件。由于创建的顶层窗口是一个容器，因此可以将小部件放置其中。你可以使用 `gtk_button_new_with_label` 函数创建按钮，并使用 `gtk_container_add` 函数将按钮放置在窗口中。注意，顶层窗口和按钮都必须通过 `gtk_widget_show` 函数设置为可见。按钮还需要经过添加到容器的额外步骤。尽管按钮已经被创建并设置为可见，但在它被添加到容器之前，它在屏幕上是不可见的。小部件需要是顶层窗口（无父级），或必须位于可见面板中才能被看到。`gtk_container_add` 函数设置了顶层窗口与按钮之间的父子关系，并将部件放置在窗口中。你还可以为按钮添加事件处理器来处理点击事件，这样每次按下按钮时，都会调用 `button_was_clicked` 函数向控制台显示消息。图 3.3 显示

![](img/0c25d93d8fa983d9a11557943feed9d0_48_0.png)

图 3.3 GTK+ 按钮中的简单事件。

```c
#include <gtk/gtk.h>

gint CloseAppWindow(GtkWidget *widget, gpointer data)
{
    g_print ("Quitting...\n");
    gtk_main_quit();
    /* --- Continue closing -- */
    return (FALSE);
}
```

```c
/*
* button_was_clicked
* 按钮被点击时调的回调函数。
 */
```

```c
void button_was_clicked (GtkWidget *widget, gpointer gdata)
{
    g_print ("Button was clicked.\n");
}
int main (int argc, char *argv[])
{
    GtkWidget *window;
    GtkWidget *button;
    /* --- Initialize gtk, handle command-line parameters --- */
    gtk_init (&argc, &argv);
    /* --- Create a window in gtk - note the window is NOT visible yet --- */
    window = gtk_window_new (GTK_WINDOW_TOPLEVEL);
    /* --- 应用程序退出时的清理代码 --- */
    gtk_signal_connect(GTK_OBJECT (window), "delete_event",
                      GTK_SIGNAL_FUNC (destroy), NULL);
    /* --- 在容器中的对象周围留出间距 --- */
    gtk_container_border_width (GTK_CONTAINER (window), 15);
    /* --- 创建一个按钮 --- */
    button = gtk_button_new_with_label ("Click me");
    /* 给按钮添加一个事件处理器 - 点击时将调用该函数 -- */
    /* 当按钮被点击时调用 button_was_clicked -- */
    gtk_signal_connect(GTK_OBJECT (button),
                      "clicked",
                      GTK_SIGNAL_FUNC (button_was_clicked),
                      NULL);
    /* --- 主窗口包含按钮 -- */
    gtk_container_add (GTK_CONTAINER (window), button);
    /* --- 让按钮可见 -- */
    gtk_widget_show (button);
    /* --- 现在，让窗口可见 -- */
    gtk_widget_show (window);
    gtk_main ();
    return 0;
}
```

## 多句处理器

在很多情况下，一个小部件需要多个事件处理器。本节扩展了之前的示例，并添加了当鼠标移动到按钮上触发的事件处理器。

```c
/*
* button_entered
* 当鼠标移动到部件上时调的回调函数。
 */
void button_entered (GtkWidget *widget, gpointer data)
{
  g_print("Welcome to fantasy!\n");
}
```

```c
/*
* button_leave
* 当鼠标移出部件时调的回调函数。
 */
void button_leave (GtkWidget *widget, gpointer data)
{
    g_print("Hey! Where are you going?\n");
}
```

在编写回调函数后，需要将它们注册到 GTK+，以便可以使用 `gtk_signal_connect` 函数将回调注册到信号上。`enter` 事件表示鼠标移动到了按钮上，`leave` 事件表示鼠标离开了按钮。通过将这两个事件分配给函数，你可以创建一个响应不同事件的按钮。

```c
/* 给按钮添加一个事件处理器 - 移动到按钮上将调用该函数 -- */
/* 当鼠标移动到按钮上调用 button_entered -- */
gtk_signal_connect(GTK_OBJECT (button),
    "enter",
    GTK_SIGNAL_FUNC (button_entered),
    NULL);
```

```c
/* 给按钮添加一个事件处理器 - 移出按钮时将调用该函数 -- */
/* 当鼠标离开按钮时调用 button_leave -- */
gtk_signal_connect(GTK_OBJECT (button),
    "leave",
    GTK_SIGNAL_FUNC (button_leave),
    NULL);
```
