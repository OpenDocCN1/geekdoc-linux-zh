

![](img/8bcc1ba72831c7d67cfc8b395deab95f_103_0.png)

**图 4-5：** 垂直方向调整大小会拉伸按钮。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_103_1.png)

**图 4-6：** 水平方向调整大小会分离按钮。

## 水平盒的选项

有三个选项设置控制控件在盒中的布局方式。（实际上有四个设置，但间距将在本章稍后讨论。）这三个设置均为布尔值，因此共有八种组合，如图 4-7 所示。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_103_2.png)

**图 4-7：** 使用水平盒布局控件

在水平盒中，如果所有控件都被分配相同宽度的显示区域，则这些控件是*同质的*。每个控件都显示在其分配区域的水平中心位置，控件可能也可能不会扩展以填满该区域。

可以指示控件*扩展*以使用整个盒子。这不会影响控件的显示大小。相反，它会在一个可能大于也可能小于控件自然宽度的区域中居中显示现有控件。每个控件的区域是按百分比分配的。如果一个控件的最小尺寸默认值是另一个控件的一半，那么在它们扩展以填满盒子后，这种尺寸比例保持不变。例如，如果一个盒子宽度为 800 像素，其中包含一个宽度为 100 像素的控件和另一个宽度为 300 像素的控件，那么为了填满盒子，这两个控件的大小都会加倍，分别变为 200 像素和 600 像素。

可以指示控件*填充*分配给它们的区域。默认情况下，分配给控件的区域也是其最小宽度；但如果控件已被命令*扩展*，并且分配了更大的区域，控件就会扩大以填满该区域。

图 4-7 展示了所有八种可能的组合，但存在一些重复。实际上只有六种不同的显示布局。编号 5 和 7 产生的显示效果相同，编号 6 和 8 产生的显示效果也相同。原因是如果盒子是*同质的*，*扩展*设置将不起作用。

图 4-7 中显示的窗口由以下程序生成。它创建一个包含主垂直盒的单窗口。进而，垂直盒中填充了所有水平盒。使用按钮控件来填充水平盒，因为它们是带有斜角边缘的简单控件，这使得很容易看出每个控件的开始和结束位置。

```c
/** horizboxes.c **/
#include <gnome.h>

GtkWidget *makeBoxes();
gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data);
void buttonFill(GtkWidget *box, gboolean expand, gboolean fill, guint spacing);

static gchar *buttonLabel[] = {
  "Purple",
  "Red",
  "LavenderBlue",
  "Yellow"
};

int main(int argc, char *argv[])
{
  GtkWidget *window;
  GtkWidget *box;

  gnome_init("horizboxes", "1.0", argc, argv);
  window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
  gtk_signal_connect(GTK_OBJECT(window),
                     "delete_event",
                     GTK_SIGNAL_FUNC(eventDelete),
                     NULL);
  gtk_signal_connect(GTK_OBJECT(window),
                     "destroy",
                     GTK_SIGNAL_FUNC(eventDestroy),
                     NULL);

  box = makeBoxes();
  gtk_container_set_border_width(GTK_CONTAINER(window), 25);
  gtk_container_add(GTK_CONTAINER(window), box);
  gtk_widget_show(box);

  gtk_widget_show(window);
  gtk_main();
  exit(0);
}

GtkWidget *makeBoxes()
{
  GtkWidget *vbox;
  GtkWidget *hbox;
  GtkWidget *label;

  gboolean homogeneous;
  gboolean expand;
  gboolean fill;
  gint hCount;
  gint eCount;
  gint fCount;
  gint count = 0;
  gchar labelString[80];

  vbox = gtk_vbox_new(FALSE, 0);

  for (hCount = 0; hCount <= 1; hCount++) {
    homogeneous = hCount ? TRUE : FALSE;
    for (eCount = 0; eCount <= 1; eCount++) {
      expand = eCount ? TRUE : FALSE;
      for (fCount = 0; fCount <= 1; fCount++) {
        fill = fCount ? TRUE : FALSE;
        if (count > 0) {
          label = gtk_label_new(" ");
          gtk_box_pack_start(GTK_BOX(vbox), label, FALSE, FALSE, 0);
          gtk_widget_show(label);
        }
        sprintf(labelString, "%d", ++count);
        if (homogeneous)
          strcat(labelString, " homogeneous, ");
        else
          strcat(labelString, "non-homogeneous, ");
        if (expand)
          strcat(labelString, "expand, ");
        else
          strcat(labelString, "no expand, ");
        if (fill)
          strcat(labelString, "fill: ");
        else
          strcat(labelString, "no fill: ");
        label = gtk_label_new(labelString);
        gtk_misc_set_alignment(GTK_MISC(label), 0.0);
        gtk_box_pack_start(GTK_BOX(vbox), label, FALSE, FALSE, 0);
        gtk_widget_show(label);
        hbox = gtk_hbox_new(homogeneous, 0);
        buttonFill(hbox, expand, fill);
        gtk_box_pack_start(GTK_BOX(vbox), hbox, FALSE, FALSE, 0);
        gtk_widget_show(hbox);
      }
    }
  }
  return(vbox);
}

void buttonFill(GtkWidget *box, gboolean expand, gboolean fill, guint spacing)
{
  GtkWidget *button;
  gint i;

  for (i = 0; i < 4; i++) {
    button = gtk_button_new_with_label(buttonLabel[i]);
    gtk_box_pack_start(GTK_BOX(box), button, expand, fill, spacing);
    gtk_widget_show(button);
  }
}

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data)
{
  return(FALSE);
}

gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data)
{
  gtk_main_quit();
  return(0);
}
```

第 35 行对 `makeBoxes()` 的调用返回包含所有水平盒的垂直盒。第 36 至 39 行定义了盒子周围的边框，将其添加到主窗口中，并显示出来。

从第 45 行开始的函数 `makeBoxes()` 为八种可能的配置设置各构建一个盒子。对于这个示例，显示效果有些重复，并且无需为按钮分配回调函数，因此所有盒子和按钮都是通过从第 61 行开始的循环构建的。实际上，这是一个嵌套循环，对于每个设置都有一个 for 语句。布尔值 `homogeneous`、`expand` 和 `fill` 在每个循环的顶部进行切换，所有可能的组合都被用来构建一个装满按钮的盒子。

每个水平盒之前都有一个空白标签（用于间距）和一个描述该盒子设置的标签。第 67 至 72 行插入空白标签。第 74 至 85 行使用配置设置创建描述性字符串，该字符串用于在第 86 行构建标签控件。第 88 行对 `gtk_misc_set_alignment()` 的调用使标签中的文本左对齐（默认是居中对齐）。

第 92 行对 `gtk_hbox_new()` 的调用创建水平盒，第 93 行对 `buttonFill()` 的调用用按钮填充它。这就是设置配置参数的地方。控件布局是否同质取决于盒子——而不是单独的控件，因此对 `gtk_box_new()`（此处实际代码为 `gtk_hbox_new`）的调用将其第一个参数设为布尔值 `homogeneous`。`expand` 和 `fill` 参数是逐个应用于控件的，因此传递给 `buttonFill()` 函数，以便应用于每个新按钮。

从第 102 行开始的函数 `buttonFill()` 使用传入的参数值，将四个按钮控件打包到一个盒子中。按钮标签由不同长度的字符串数组创建，以便位置差异更明显。从第 108 行开始的循环构建每个按钮并将其添加到盒子中。

## 垂直盒的选项

图 4-8 展示了将八种组合应用于一系列垂直盒的结果。将此图中的垂直盒与之前图 4-7 中显示的水平盒进行比较，你应该对布局机制有一个相当好的了解。相同的尺寸和位置规则适用于水平和垂直方向。

此示例与前一个示例非常相似。程序之间的唯一区别是，为了将盒子从水平变为垂直并使其正确显示所需的语句。

```c
/** vertboxes.c **/
#include <gnome.h>
```

