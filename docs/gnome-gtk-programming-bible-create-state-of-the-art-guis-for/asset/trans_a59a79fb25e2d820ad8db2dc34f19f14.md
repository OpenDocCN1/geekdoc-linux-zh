

![](img/8bcc1ba72831c7d67cfc8b395deab95f_98_0.png)

## 在窗口中布局小部件

本章是两章关于在窗口上放置小部件章节中的第一章。在本章中，使用盒子和表格来实现定位。在表格或盒子中对小部件进行定位的过程被称为*打包小部件*。使用盒子和表格，您可以快速实现复杂的窗口。这只需要创建盒子或表格，然后将小部件填充进去即可。盒子本身也是一个小部件，可以打包到其他盒子中。表格也是如此。实际上，您可以将表格打包到盒子中，也可以将盒子打包到表格中。

## 打包盒子

有两种类型的盒子。小部件被打包到垂直盒子中时，会一个接一个地垂直堆叠显示；或者被打包到水平盒子中时，会并排显示。将一组小部件的盒子称为小部件列表可能更准确，因为小部件必须并排或一个在另一个之上排列。然而，通过嵌套盒子，这个过程变得非常灵活且易于管理。

盒子是一种设计用来容纳小部件的小部件。这意味着盒子可以包含其他盒子。例如，如果一个水平盒子包含一对垂直盒子，而每个垂直盒子包含四个小部件，这些小部件将显示为两列四行。此外，由于盒子中容纳的任何小部件都可以是包含小部件的另一个盒子，因此可以创建具有许多不同模式的小部件填充的窗口。

尺寸调整完全由盒子自动完成，盒子通过与其中包含的小部件“通信”来了解小部件能做什么和不能做什么。每个小部件都有自己的内部最小高度和宽度，盒子在计算布局和尺寸的位置时必须考虑这些因素。有时，盒子会要求小部件在垂直或水平方向上扩展到大于小部件所需尺寸的更大尺寸。

### 本章内容

- 在盒子中水平打包和垂直打包小部件
- 更改盒子的配置设置以改变其排列小部件的方式
- 在表格中水平打包和垂直打包小部件
- 更改配置设置和打包命令以改变表格排列小部件的方式
- 组合表格和盒子

## 垂直打包盒子

垂直盒子是一种能够容纳多个小部件并垂直显示它们的小部件，如图 4-1 中的那些小部件所示。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_99_0.png)

这是一个创建图 4-1 中所示盒子的示例程序，该盒子包含四个按钮：

```c
/** vertbox.c **/
#include <gnome.h>

GtkWidget *makeBox();
gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data);

int main(int argc, char *argv[])
{
  GtkWidget *window;
  GtkWidget *box;

  gnome_init("vertbox", "1.0", argc, argv);
  window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
  gtk_container_set_border_width(GTK_CONTAINER(window), 25);
  gtk_signal_connect(GTK_OBJECT(window), "delete_event",
            GTK_SIGNAL_FUNC(eventDelete), NULL);
  gtk_signal_connect(GTK_OBJECT(window), "destroy",
            GTK_SIGNAL_FUNC(eventDestroy), NULL);
  box = makeBox();
  gtk_container_add(GTK_CONTAINER(window), box);
  gtk_widget_show(window);
  gtk_main();
  exit(0);
}

GtkWidget *makeBox() {
  GtkWidget *box;
  GtkWidget *button;
  
  box = gtk_vbox_new(FALSE, 0);
  gtk_widget_show(box);
  
  button = gtk_button_new_with_label("Start 1");
  gtk_box_pack_start(GTK_BOX(box), button, FALSE, FALSE, 0);
  gtk_widget_show(button);
  
  button = gtk_button_new_with_label("End 1");
  gtk_box_pack_end(GTK_BOX(box), button, FALSE, FALSE, 0);
  gtk_widget_show(button);
  
  button = gtk_button_new_with_label("Start 2 button");
  gtk_box_pack_start(GTK_BOX(box), button, FALSE, FALSE, 0);
  gtk_widget_show(button);
  
  button = gtk_button_new_with_label("End 2 button");
  gtk_box_pack_end(GTK_BOX(box), button, FALSE, FALSE, 0);
  gtk_widget_show(button);
  
  return(box);
}

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data) {
  return(FALSE);
}

gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data) {
  gtk_main_quit();
  return(0);
}
```

程序的主线在第 16 行创建一个顶级窗口，并在第 17 和 18 行在其边缘放置 25 像素的边框。在关闭回调初始化后，小部件盒子在第 28 行通过调用 makeBox() 创建。第 29 行的函数 gtk_container_add() 将盒子小部件放入主窗口，第 30 行对 gtk_widget_show() 的调用使主窗口可见。

从第 34 行开始的 makeBox() 函数构造并返回一个包含四个按钮的垂直盒子。第 38 行对 gtk_vbox_new() 的调用构造了该盒子。按钮按照显示的顺序添加，但可以从顶部或底部添加。第 41 行构造的按钮在第 42 行添加到盒子的开始位置——这意味着它被插入到盒子的顶部。第 45 行构造的按钮在第 46 行添加到盒子的结束位置——这意味着它被插入到盒子的底部。任何添加到顶部的其他小部件都会位于已有小部件的下方，而任何添加到底部的其他小部件都会位于已有小部件的上方。

图 4-1 中显示的默认尺寸表明所有内容都合适。每个按钮都向盒子报告了其尺寸。盒子希望沿其边缘排列物品，因此它分析每个按钮的高度和宽度，以确定每个按钮的整体尺寸和位置。所有按钮的高度相同，因此不需要垂直调整。盒子确定最宽按钮（即 Start 2 按钮）的宽度，并使用该值设置所有按钮的宽度。除了宽度信息外，盒子还告诉每个按钮其在屏幕上的 x 和 y 坐标。每个按钮遵循其指令，居中对齐文本，并在请求的位置和请求的尺寸下显示自身。盒子也是一个子部件，因此当主窗口查询盒子的尺寸时，盒子返回显示所有四个按钮所需的总面积。主窗口使用此尺寸信息，在边缘添加 25 像素的边距，为盒子提供其 x 和 y 坐标。

默认尺寸和配置是最佳的。可以使用鼠标调整窗口大小，但在水平或垂直方向上都不能使其小于原始尺寸。然而，窗口可以变大。例如，如图 4-2 所示垂直拉长窗口会导致盒子通过拆分按钮列表将物品分开——打包在顶部的按钮保持在顶部，打包在底部的按钮保持在底部。如图 4-3 所示水平拉伸盒子也会调整按钮大小，它们被拉伸以填满盒子。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_101_0.png)

**图 4-2**：垂直调整大小使按钮分离。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_102_0.png)

**图 4-3**：水平调整大小拉伸按钮。

很明显，垂直盒子不能垂直扩展按钮，但可以水平扩展它们以填满空间。此外，盒子中包含的小部件的偏移量是根据顶部或底部计算的，具体取决于小部件如何被添加到盒子中。在实践中，这被证明是相当有用的。如果所有小部件都打包在盒子的一端，那么无论盒子本身如何变形拉伸，它们都会保持在该端。

## 水平打包盒子

水平盒子和垂直盒子的工作方式完全相同，区别在于将小部件打包到开始位置会将其放在左侧，而将小部件打包到结束位置会将其放在右侧。名为 vertbox.c 的前述程序可以通过更改程序名称和一行代码转换为 horibox.c。对于垂直盒子，第 38 行如下所示：

```c
box = gtk_vbox_new(FALSE, 0);
```

将其替换为以下行即可使其成为水平盒子：

```c
box = gtk_hbox_new(FALSE, 0);
```

就是这样。显示效果现在看起来像图 4-4 中的样子。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_102_1.png)

**图 4-4**：水平盒子中的四个按钮

对水平盒子尺寸所做的调整与对垂直盒子所做的调整具有相同的效果，只是沿着另一个维度进行。图 4-5 显示水平盒子变高，所有按钮也变高以适应。图 4-6 显示水平盒子变宽，按钮没有改变大小，而是定位以贴合其最初添加的末端。

