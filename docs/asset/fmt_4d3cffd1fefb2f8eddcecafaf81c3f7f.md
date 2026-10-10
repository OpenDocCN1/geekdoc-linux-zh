
```c
#include <gtk/gtk.h>

// 预约
typedef struct {
    int day;                // 日期
    char *timestr;           // 时间
    char *title;            // 标题
    char *location;         // 地点
} CalEntry;

// 预约数据（硬编码）
static CalEntry entries[] = {
    {3, "9:30 AM", "Lunch with Bob"},
    {6, "12:00 PM", "Pick up dry-cleaning at airport"},
    {7, "3:00 PM", "Dentist"},
    {12, "6:00 PM", "Dinner with team"},
    {15, "9:00 AM", "Golf"},
    {17, "1:00 PM", "Flight"},
    {18, "4:30 PM", "Phone"},
    {19, "8:00 PM", "Course"}
};

// 显示消息
void DisplayMessage(char *title, char *location, char *timestr) {
    char buf[124];
    GtkWidget *dialog, *label;

    sprintf(buf, "Appointment: %s\nLocation: %s\nTime: %s", title, location, timestr);

    dialog = gtk_dialog_new_with_tags("Appointment",
        GTK_WINDOW(goplevel()), GTK_DIALOG_MODAL,
        "OK", GTK_RESPONSE_OK, NULL);

    label = gtk_label_new(buf);
    gtk_container_add(GTK_CONTAINER(dialog), label);

    gtk_widget_show_all(dialog);
    gtk_dialog_run(GTK_DIALOG(dialog));
    gtk_widget_destroy(dialog);
}

// day_selected信号
void SelectDay(GtkWidget *widget, gpointer data) {
    guint year, month, day;
    int i;

    // 获取选定的日期
    gtk_calendar_get_date(GTK_CALENDAR(widget), &year, &month, &day);

    // 查看是否在预约簿中有条目
    for (i = 0; i < sizeof(entries) / sizeof(CalEntry); i++)
        if (entries[i].day == day)
            DisplayMessage(entries[i].title, entries[i].location, entries[i].timestr);
}

int main(int argc, char *argv[]) {
    GtkWidget *button, *calendar, *window;
    GtkCalendarDisplayOptions flags;
    int i;

    gtk_init(&argc, &argv);

    // 创建窗口
    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_window_set_title(GTK_WINDOW(window), "Calendar Example");
    g_signal_connect(window, "destroy", G_CALLBACK(gtk_main_quit), NULL);

    // 创建日历
    calendar = gtk_calendar_new();
    gtk_container_add(GTK_CONTAINER(window), calendar);

    // 设置显示选项
    gtk_calendar_display_options(GTK_CALENDAR(calendar),
        GTK_CALENDAR_SHOW_HEADING | GTK_CALENDAR_NO_MONTH_CHANGE |
        GTK_CALENDAR_WEEK_START_MONDAY);

    // 处理日期选择信号
    g_signal_connect(calendar, "day-activated", G_CALLBACK(SelectDay), NULL);

    gtk_widget_show_all(window);
    gtk_main();

    return 0;
}
```

Figure 15.11 日历 截图

## 总结

此示例应用程序中的预约数据被硬编码在数组中，并适用于当前月份。该程序创建了一个日历控件并将其放置在对话框中。由于仅针对当前月份，我禁用了用户更改月份或年份的能力。对于预约簿数组中的每个条目，我标记了月中与预约日期相对应的日期（为了简单起见，每天只存储一个事件）。一个 `day_selected` 函数 `SelectDay()` 被注册到日历控件中，并在用户将指针悬停在某一天并点击鼠标 1 键时被调用。回调函数使用 `Gtk_calendar_get_date()` 从日历中获取选定的日期，并搜索预约簿查看当天是否有条目。如果有，`SelectDay()` 将调用一个函数来格式化预约簿数据并显示在对话框中。

## 总结

在本章中，我们通过查看一些杂类完成了对 Gtk+ 类的介绍。尺子控件（`GtkRuler`、`GtkVRuler` 和 `GtkHRuler`）在其所在容器中显示垂直（`GtkVRuler`）或水平（`GtkHRuler`）刻度。预览查询控件（`GtkPreview`）能够显示彩色或灰度图像。本章介绍的示例说明了如何结合 `GtkPreview` 和 `libtiff` 来显示 TIFF 图像数据。

进度控件（`GtkProgress` 和 `GtkProgressBar`）通过在耗时任务期间为用户提供视觉反馈，增强了应用程序的可用性。进度条支持两种模式。第一种我称之为“从开始到结束”模式，可以用于传达已知时长或工作量的的任务完成百分比状态，例如下载已知固定大小的文件。第二种模式可以指示任何持续时间的活动，例如将日志记录到服务器。

工具提示（`GtkTooltip`）支持在用户将鼠标移动到选定的控件上时，在弹出的小窗口中显示上下文相关的帮助信息。提示查询控件（`GtkTipsQuery`）是一个较少使用的控件，它提供了在应用程序中显示上下文相关帮助的替代方法。

组合控件（`GtkCombo`）是一种允许用户在输入字段中输入数据或从附加到容器的弹出菜单中进行内容的控件。状态栏（`GtkStatus`）本质上是一个框架控件，显示由应用程序提供的状态消息。状态消息存储在栈中；栈顶定义了状态栏显示的消息。加速器标签控件主要用于为控件提供兴趣，并支持按照我们的意图在这些控件中显示加速器文本。

图形应用程序可以使用绘制区域控件（`GtkDrawingArea`）作为绘图和图像的容器。在本章中，我展示了一个示例程序，说明了通过绘图区域高效处理暴露事件（expose events）的一种可能技术。最后的 `GtkCalendar` 对于需要显示日历或让用户选择日期的应用程序有用。我展示了一个短程序，说明了应用程序如何在日历控件中标记特定日期，以及响应用户在日历显示的特定日期上进行的按钮点击。

# GTK+ 1.2 控件层次结构

以下展示了 Gtk+ 1.2 控件层次结构。类名右侧的数字指定书中描述对应控件类的章节。书中未涵盖的控件类使用*斜体*。

- `GtkObject` 3

- `GtkWidget` 4

  - `GtkMisc`

    - `GtkLabel` 5

      - `GtkAccelLabel` 15

      - `GtkTipsQuery` 15

      - `GtkArrow` 8

    - `GtkImage` 8

    - `GtkPixmap` 8

  - `GtkContainer` 10

    - `GtkBin`

    - `GtkAlignment`

      - `GtkFrame` 11

      - `GtkAspectFrame` 11

      - `GtkButton` 5

        - `GtkToggleButton` 5

        - `GtkRadioButton` 5

        - `GtkOptionMenu` 9

  - `GtkItem`

    - `GtkMenuItem` 9
