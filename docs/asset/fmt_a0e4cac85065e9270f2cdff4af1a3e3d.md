
```
49

50    void packReceivingButton(GtkWidget *box, gchar *text) {

51

52        GtkWidget *button;

53        static GtkTargetEntry target = { "text/plain", 0, 0 };

54

55        button = gtk_button_new_with_label(text);

56        gtk_box_pack_start(GTK_BOX(box), button, TRUE, FALSE, 0);

57

58        gtk_signal_connect(GTK_OBJECT(button), "drag_data_received",

59            GTK_SIGNAL_FUNC(receiveCallback), NULL);
        gtk_drag_dest_set(button,
            GTK_DEST_DEFAULT_MOTION |
            GTK_DEST_DEFAULT_HIGHLIGHT |
            GTK_DEST_DEFAULT_DROP,
            &target, 1,
            GDK_ACTION_COPY);
    }

    void sendCallback(GtkWidget *widget,
        GdkDragContext *context,
        GtkSelectionData *selection, guint info, guint time)
    {

        gchar *ascii;
        GtkWidget *label;

        label = GTK_BUTTON(widget)->child;
        gtk_label_get(GTK_LABEL(label), &ascii);
        gtk_selection_data_set(selection, selection->target,
            8, ascii, strlen(ascii));
    }

    void receiveCallback(GtkWidget *widget,
        GdkDragContext *context,
        gint x, gint y, GtkSelectionData *selection,
        guint info, guint time)
    {

        GtkWidget *label;

        label = GTK_BUTTON(widget)->child;
        gtk_label_set_text(GTK_LABEL(label), selection->data);
    }

    gint eventDelete(GtkWidget *widget,
        GdkEvent *event, gpointer data) {
        return(FALSE);
    }

    gint eventDestroy(GtkWidget *widget,
        GdkEvent *event, gpointer data) {
        gtk_main_quit();
        return(0);
    }
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_478_0.png)

第 23 行至第 31 行初始化应用程序，创建一个水平框，并将该框插入应用程序窗口。第 33 行至第 35 行的函数调用创建按钮并将它们装入框中。其中两个按钮可以充当 ASCII 文本拖放的源，一个按钮可以充当目标。

第 42 行的 `packSendingButton()` 函数创建一个按钮，设置使其成为拖放源所需的回调，并将按钮装入框中。第 50 行的 `gtk_signal_connect()` 调用指定每当在按钮内部发起拖放操作时，应执行回调函数 `sendCallback()`。第 52 行的 `gtk_drag_source_set()` 调用指定关于拖放的信息（数据类型、使用的鼠标按钮以及完成拖放时应采取的操作）。

第 55 行的 `packReceivingButton()` 函数创建一个按钮，设置使其成为放置目标所需的回调，并将按钮装入框中。第 63 行的 `gtk_signal_connect()` 调用指定每当在窗口内部发生放置操作时执行回调函数。第 66 行的 `gtk_drag_dest_set()` 调用指定当此按钮检测到拖放操作时要采取的操作。

在第 73 行，调用 `sendCallback()` 函数以创建从拖放源传输的数据。第 80 行和第 81 行提取按钮标签的文本，`gtk_selection_data_set()` 调用将数据插入到 `GtkSelectionData` 结构体中。该结构体是发送给接收部件的那个。

第 85 行的 `receiveCallback()` 函数在接收按钮内发生放置操作时执行。`GtkSelectionData` 结构体包含一个指向 ASCII 字符串的指针，该字符串将成为新的标签。

只有当数据实际传输时，才会调用回调函数。例如，如果你使用鼠标开始拖放操作，但将数据放置在一个无法接收它的窗口上，则不会调用任何回调函数。也就是说，只有当选中接收窗口时，才会执行发送方的回调函数。在拖放操作之前，源调用 `gtk_drag_source_set()`，目标调用 `gtk_drag_dest_set()`，这些调用建立的设置用于确定拖放是否有效。如果拖放有效，则调用源回调，然后调用目标回调。这样，发送方的回调函数无需关心接收方是否已获取数据——这在 `GTK_ACTION_MOVE` 操作中尤为重要，因为在该操作中数据会从源中删除。

## 在应用程序之间移动图形数据

拖放操作可以支持多种数据类型。MIME（多用途互联网邮件扩展）规范决定了数据的类型。MIME 编码最初是作为识别和编码电子邮件附件的方法而设计的，但它已找到许多其他用途。每种数据类型由两个名称指定：类别以及类别内的具体数据类型。以下是一些 MIME 数据类型名称的示例：

```
text/plain
text/html
```

image/jpeg
video/mpeg

要查看 Linux 已知的 MIME 类型列表，请在 GNOME 控制中心窗口中选中 `Mime Types`。第一列包含双字 MIME 类型，第二列包含通常用于包含该数据类型的文件后缀（也称为文件扩展名）。只要发送方和接收方应用程序都理解相同的类型，你就可以在拖放操作中使用这些 MIME 类型中的任意一种。或者，如果你愿意，你也可以发明一种仅在你自己的应用程序之间使用的自定义类型。

你可以从同一位置拖放两个或更多 MIME 类型。数据的接收方将确定实际选中的类型。以下示例演示了拖放操作的来源是一个像素映射（pixmap）小部件，但接收方可以选择接收像素映射或纯文本。图 16-2 展示了当几个图片按钮被拖放到画布上后窗口的外观，并且底部的文本按钮上至少有一次放置（它显示的不是图片，而是放置的时间）。由于使用了标准的 MIME 类型名称，你可以将这些项目拖放至任何应用程序。例如，将此应用程序中的 logo 按钮拖放到 GNOME 终端，你会得到数据的纯文本形式（当前的日期和时间）。

```c
/** typend.c **/
#include <gnome.h>
#include "minilogo.xpm"
#define HEIGHT 300
#define WIDTH 200
#define TARGET_TYPE_TEXT 80
#define TARGET_TYPE_PIXMAP 81
typedef struct {
    GtkWidget *app;
    GnomeCanvasGroup *rootGroup;
} tdContext;
static GtkTargetEntry fromImage[] =
{   { "text/plain", 0, TARGET_TYPE_TEXT },
    { "image/x-xpixmap", 0, TARGET_TYPE_PIXMAP }
};
static GtkTargetEntry toButton =
{   { "text/plain", 0, TARGET_TYPE_TEXT } };
static GtkTargetEntry toCanvas =
```
