

| 部分 | 描述 |
| :--- | :--- |
| vertical dpi | 每英寸分辨率的垂直像素数。 |
| spacing | 这可以是 m（等宽）、p（比例）或 c（字符单元）。等宽字体是指所有字符宽度相同的字体。比例字体的字符宽度各异（例如，字母 *w* 比字母 *i* 宽）。字符单元字体是一种基于打字机字体间距方式的固定宽度字体。 |
| pixel width | 字体中所有字符的平均宽度，以十分之一像素为单位。 |
| character set | 这是用于定义字符集的标准版本。ISO（国际标准化组织）已制定了标准，规定了各种语言字母表中包含的字符集。 |

长字体名称不仅具有描述性，而且其格式允许你在搜索字体时使用通配符。这样，你只需指定你关心的部分，其余部分则使用默认值。例如，在调用 `gtk_font_load()` 时，可以使用以下内容作为字体名称：

```
-* bookman-light-r-normal--14-*-*-*-*-iso8859-1
```

名称中指定的部分必须与实际字体完全匹配，而星号可以匹配任意值。当然，可能会有多个字体匹配，但遇到第一个匹配的字体将被返回。上述示例可能会选择此字体：

```
-adobe-bookman-light-r-normal--14-135-75-p-82-iso8859-1
```

在指定字体名称时，你只需要对你需要的部分进行具体指定。这样你有更大的机会匹配到实际的字体名称。如果你的指定条件不匹配任何字体名称，将使用名为 `fixed` 的默认字体，而这几乎不是你想要的字体。

## 字体选择器小部件

有一个 GNOME 小部件可以让你选择和显示字体。该小部件在你的应用程序中作为一个按钮放置在对话框或菜单中。以下程序展示了如何使用该小部件选择字体，以及如何将该字体应用于其他小部件的文本。

```c
/* fontpicker.c */
#include <gnome.h>

gint eventDelete(GtkWidget *widget,
                 GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget,
                 GdkEvent *event, gpointer data);
void eventFontSet(GtkWidget *widget,
                 gchar *string, GtkWidget *label);

int main(int argc, char *argv[]) {
    GtkWidget *app;
    GtkWidget *fontpicker;
    GtkWidget *label;
    GtkWidget *box;

    gnome_init("fontpicker","1.0",argc, argv);
    app = gnome_app_new("fontpicker","Font Picker");
    gtk_container_set_border_width(GTK_CONTAINER(app),30);
    gtk_signal_connect(GTK_OBJECT(app),"delete_event",
            GTK_SIGNAL_FUNC(eventDelete),NULL);
    gtk_signal_connect(GTK_OBJECT(app),"destroy",
            GTK_SIGNAL_FUNC(eventDestroy), NULL);

    box = gtk_vbox_new(FALSE,0);

    label = gtk_label_new(
            "Select the button below and the font picker\n"
            "window will appear.\n"
            "The font you select will be used to\n"
            "rewrite this text.");
    gtk_box_pack_start(GTK_BOX(box), label,
            FALSE,FALSE,0);

    fontpicker = gnome_font_picker_new();
    gtk_signal_connect(GTK_OBJECT(fontpicker),"font-set",
            GTK_SIGNAL_FUNC(eventFontSet),label);
    gtk_box_pack_start(GTK_BOX(box),fontpicker,
            FALSE,FALSE,0);

    gnome_app_set_contents(GNOME_APP(app),box);
    gtk_widget_show_all(app);
    gtk_main();
    exit(0);
}

void eventFontSet(GtkWidget *widget,
                 gchar *string, GtkWidget *label) {
    GtkStyle *oldStyle;
    GtkStyle *newStyle;
    GdkFont *font;

    font = gdk_font_load(string);
    oldStyle = gtk_widget_get_style(label);
    newStyle = gtk_style_copy(oldStyle);
    newStyle->font = font;
    gtk_widget_set_style(label,newStyle);
    gtk_style_unref(oldStyle);
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

在第 26 行，创建了一个垂直盒以包含文本标签和 GtkFontPicker 按钮。第 28 到 34 行创建带有文本的标签，并将其打包到盒子的顶部。第 36 行创建字体选择器。在第 37 行，将回调函数 eventFontSet() 附加到字体选择器上，并将字体选择器打包在标签下方的盒子中。

回调函数 eventFontSet()（在第 47 行定义）在字体选择器对话框中按下确定按钮时调用。第 53 行对 gdk_font_load() 的调用使用所选字体的名称创建一个 GdkFont 对象。这种创建过程被称为“加载”，因为该过程的一部分是通知 X 服务器加载该字体。返回的 GdkFont 对象持有字体 ID 信息，每当需要使用该字体时都会将这些信息传递给服务器。根据当前选择的字体，窗口看起来像图 13-4 中所示的那样。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_432_0.png)

小部件包含一个指向 GtkStyle 对象的指针，该对象包含颜色和字体信息（以及一些其他内容）。第 54 行对 gtk_widget_get_style() 的调用返回指向该 GtkStyle 对象的指针。同一个 GtkStyle 对象可以被许多小部件共享，因此应用程序不应直接修改它。相反，会调用 gtk_style_copy() 来创建 GtkStyle 的副本，然后，在第 56 行，将新字体赋值给该副本。第 57 行对 gtk_widget_set_style() 的调用用该副本替换原始的 GtkStyle。最后，在第 58 行，调用 gtk_style_unref() 来丢弃对旧 GtkStyle 对象的引用。如果没有其他引用，则 GtkStyle 使用的内存将返回给系统——否则，引用计数器将减少一。

图 13-5 显示了字体选择器对话框显示的三个面板之一。你可以从这个窗口中选择三个最基本的字体特性——字体名称、粗细和斜体以及字体大小。其他两个面板可用于指定字体名称的其他部分以细化搜索。底部的预览窗口会在选择更改时更新。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_433_0.png)

## 度量与字体放置

以下程序在绘图区域上定位文本。它使用特定字符串的字体度量信息来确定包含该字体的矩形区域的上、下、中、右和左边缘。然后，这些尺寸用于居中放置文本并将其对齐到边缘。

```c
/* fontposition.c */
#include <gnome.h>

#define HEIGHT 100
#define WIDTH 300

#define STRING_LEFT 1
#define STRING_CENTER 2
#define STRING_RIGHT 3
#define STRING_TOP 1
#define STRING_MIDDLE 2
#define STRING_BOTTOM 3

typedef struct {
    GdkFont *font;
    GtkWidget *drawingArea;
    gint horizontal;
    gint vertical;
} Context;

gint eventDelete(GtkWidget *widget,
                 GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget,
                 GdkEvent *event, gpointer data);
void eventFontSet(GtkWidget *widget,
                 gchar *string, Context *context);
gboolean eventDraw(GtkWidget *widget,
                 GdkEvent *event, Context *context);
void topButton(GtkWidget *widget, Context *context);
void middleButton(GtkWidget *widget, Context *context);
void bottomButton(GtkWidget *widget, Context *context);
void leftButton(GtkWidget *widget, Context *context);
void centerButton(GtkWidget *widget, Context *context);
void rightButton(GtkWidget *widget, Context *context);
static GtkWidget *createPositionWidget(Context *context);

int main(int argc, char *argv[])
{
    GtkWidget *app;
    GtkWidget *position;
    Context context =
            ( NULL, NULL, STRING_RIGHT, STRING_MIDDLE );

    gnome_init("fontposition","1.0",argc,argv);
    app = gnome_app_new("fontposition","Font Position");
    gtk_container_set_border_width(GTK_CONTAINER(app),30);
    gtk_signal_connect(GTK_OBJECT(app),"delete_event",
            GTK_SIGNAL_FUNC(eventDelete),NULL);
    gtk_signal_connect(GTK_OBJECT(app),"destroy",
            GTK_SIGNAL_FUNC(eventDestroy),NULL);

    position = createPositionWidget(&context);

    gnome_app_set_contents(GNOME_APP(app),position);
    gtk_widget_show_all(app);
    gtk_main();
    exit(0);
}

static GtkWidget *createPositionWidget(Context *context)
{
    GtkWidget *position;
    GtkWidget *box;
    GtkWidget *button;
    GtkWidget *frame;
    GtkWidget *fontpicker;

    position = gtk_vbox_new(FALSE,0);

    box = gtk_hbox_new(TRUE,10);
    button = gtk_button_new_with_label("Top");
    gtk_signal_connect(GTK_OBJECT(button),"clicked",
```

