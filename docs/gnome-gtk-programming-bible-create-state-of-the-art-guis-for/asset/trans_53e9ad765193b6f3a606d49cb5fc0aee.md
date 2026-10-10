

```c
25  = GTK_CONTAINER(topLevelWindow), 20);
26  box = gtk_vbox_new(FALSE, 0);
27
28  popupButton = gtk_button_new_with_label("Popup");
29  gtk_signal_connect(GTK_OBJECT(popupButton),
30      "clicked",
31      GTK_SIGNAL_FUNC(showPopup),
32      NULL);
33  gtk_box_pack_start(GTK_BOX(box), popupButton,
34      FALSE, FALSE, 0);
35  gtk_widget_show(popupButton);
36
37  dialogButton = gtk_button_new_with_label("Dialog");
38  gtk_signal_connect(GTK_OBJECT(dialogButton),
39      "clicked",
40      GTK_SIGNAL_FUNC(showDialog),
41      NULL);
42  gtk_box_pack_start(GTK_BOX(box), dialogButton,
43      FALSE, FALSE, 0);
44  gtk_widget_show(dialogButton);
45
46  gtk_container_add(GTK_CONTAINER(topLevelWindow), box);
47  gtk_widget_show(box);
48  gtk_widget_show(topLevelWindow);
49
50  gtk_main();
51  exit(0);
52 }
53 gint eventDestroy(GtkWidget *widget,
54     GdkEvent *event, gpointer data) {
55     gtk_main_quit();
56     return(0);
57 }
58 void showPopup(GtkWidget *widget, gpointer data) {
59     GtkWidget *popup;
60     GtkWidget *button;
61
62     popup = gtk_window_new(GTK_WINDOW_POPUP);
63     button = gtk_button_new_with_label("Close Popup");
64     gtk_container_set_border_width
65         (GTK_CONTAINER(popup), 20);
66     gtk_container_add(GTK_CONTAINER(popup), button);
67     gtk_signal_connect(GTK_OBJECT(button),
68         "clicked",
69         GTK_SIGNAL_FUNC(destroyPopup),
70         popup);
71     gtk_widget_show(button);
72     gtk_widget_show(popup);
73 }
74 void showDialog(GtkWidget *widget, gpointer data) {
75
76     GtkWidget *dialog;
77     GtkWidget *button;
78
79     dialog = gtk_window_new(GTK_WINDOW_DIALOG);
80     button = gtk_button_new_with_label("Close Dialog");
81     gtk_container_set_border_width(
82         GTK_CONTAINER(dialog), 20);
83     gtk_container_add(GTK_CONTAINER(dialog), button);
84     gtk_signal_connect(GTK_OBJECT(button),
85         "clicked",
86         GTK_SIGNAL_FUNC(destroyDialog),
87         dialog);
88
89     gtk_widget_show(button);
90     gtk_widget_show(dialog);
91 }
92
93 void destroyPopup(GtkWidget *widget, gpointer data)
94 {
95     gtk_widget_destroy(GTK_WIDGET(data));
96 }
97 void destroyDialog(GtkWidget *widget, gpointer data)
98 {
99     gtk_widget_destroy(GTK_WIDGET(data));
100 }
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_88_0.png)

**图 3-16：带有两个按钮的主窗口**

![](img/8bcc1ba72831c7d67cfc8b395deab95f_88_1.png)

**图 3-17：带有“关闭”按钮的弹出窗口**

![](img/8bcc1ba72831c7d67cfc8b395deab95f_88_2.png)

**图 3-18：带有“关闭”按钮的对话框窗口**

第 18 到 25 行初始化 GNOME，设置销毁回调，创建一个顶级窗口，并指定窗口周围的边距为 20 像素宽。

第 26 行创建一个框（box）组件，这是一种被称为容器的特殊组件。容器组件能够同时组织和显示多个组件。由于主窗口需要显示一个以上的组件，因此这是必要的。

并非将按钮直接插入到主窗口中，而是将它们插入到第 33 行和第 42 行中的框中。随后，该框在第 47 行被插入到主窗口中。框有两种基本类型（水平和垂直），并且将组件填充到其中的方式各不相同，我将在第 4 章中详细讨论。在这个示例中，第 26 行上的函数调用 `gtk_vbox_new()` 创建一个垂直组织按钮的框，而第 33 行和第 42 行对 `gtk_box_pack_start()` 的调用将按钮从顶部插入到垂直框中。框会自动调整大小以紧紧包裹按钮，而主窗口则在框周围添加了一个 20 像素的边框。

主窗口的回调函数从第 58 行和第 74 行开始，各自创建一个临时窗口。函数 `showDialog()` 创建并显示如图 3-18 所示的对话框窗口，而函数 `showPopup()` 创建并显示如图 3-17 所示的弹出窗口。除了第 62 行和第 78 行指定的窗口类型不同外，这两个函数几乎完全相同。

弹出窗口和对话框都有删除自身的回调。第 83 行对 `gtk_signal_connect()` 的调用指定 `destroyDialog()` 作为对话框的回调函数。传递给该函数的最后一个参数（在第 86 行）是一个指向对话框窗口的指针。这个指针在第 95 行作为数据指针传递给回调函数。在第 97 行调用 `gtk_widget_destroy()`，导致对话框消失并将任何分配的内存归还给系统。

这个程序可以运行，但它有一两个怪癖可能需要更改（取决于您的应用程序）。照原样，每次按下主窗口中的一个按钮时，您都会得到一个 新的对话框或弹出窗口——您可以获得任意数量的它们。每个窗口使用相同的回调，并且可以按任意顺序单独关闭，因此有时这可能很方便。然而，对于大多数程序来说，允许只出现一个对话框副本更有意义。

防止出现多个对话框的一种方法是设置您的对话框为模态。本示例中的对话框可以通过在第 78 行和第 87 行之间的某处添加这行代码使其变为模态：

```c
gtk_window_set_modal(GTK_WINDOW(dialog), TRUE);
```

同样，通过在插入第 62 行和第 71 行之间插入这行代码，也可以将弹出窗口设为模态：

```c
gtk_window_set_modal(GTK_WINDOW(popup), TRUE);
```

函数 `gtk_window_set_modal()` 可以通过使用 TRUE 作为第二个参数来将任何窗口从非模态更改为模态。相反，也可以使用 FALSE 作为第二个参数来将任何窗口从模态更改为非模态。

## 通过隐藏来放下

在前面的示例中，每次显示时都会构建一个新的对话框；当它被关闭时，它会被销毁。如果对话框在每次显示时稍有不同，这是一种有效且特别有用的方法。然而，如果对话框将经常被使用，您可能希望构建一次，然后在需要时随时将其显示和隐藏。本示例隐藏并重新显示一个对话框：

```c
1 /** hiding.c **/
2 #include <gnome.h>
3 
4 void closeDialog(GtkWidget *widget,gpointer data);
5 void showDialog(GtkWidget *widget,gpointer data);
6 gint eventShutdown(GtkWidget *widget,gpointer data);
7
8 typedef struct {
9   GtkWidget *dialog;
10 } hidingContext;
11
12 int main(int argc,char *argv[])
13 {
14   GtkWidget *topLevelWindow;
15   GtkWidget *dialogButton;
16   hidingContext context;
17
18   context.dialog = NULL;
19
20   gnome_init("hiding", "1.0",argc,argv);
21   topLevelWindow = gtk_window_new(GTK_WINDOW_TOPLEVEL);
22   gtk_signal_connect(GTK_OBJECT(topLevelWindow),
23                     "destroy",
24                     GTK_SIGNAL_FUNC(eventShutdown),
25                     &context);
26   gtk_container_set_border_width(
27                     GTK_CONTAINER(topLevelWindow),20);
28
29   dialogButton = gtk_button_new_with_label("Dialog");
30   gtk_signal_connect(GTK_OBJECT(dialogButton),
31                     "clicked",
32                     GTK_SIGNAL_FUNC(showDialog),
33                     &context);
34   gtk_container_add(GTK_CONTAINER(topLevelWindow),
35                     dialogButton);
36
37   gtk_widget_show(dialogButton);
38   gtk_widget_show(topLevelWindow);
39
40   gtk_main();
41   exit(0);
42 }
43 gint eventShutdown(GtkWidget *widget,gpointer data) {
44 hidingContext *context;
45 
46 context = (hidingContext *)data;
47 if((context->dialog != NULL))
48 gtk_widget_destroy(GTK_WIDGET(context->dialog));
49 gtk_main_quit();
50 return(0);
51 }
52 void showDialog(GtkWidget *widget,gpointer data) {
53 GtkWidget *button;
54 hidingContext *context;
55 
56 context = (hidingContext *)data;
57 
58 if((context->dialog == NULL)) {
59 context->dialog =
60 gtk_window_new(GTK_WINDOW_DIALOG);
61 button = gtk_button_new_with_label("Close Dialog");
62 gtk_container_set_border_width(
GTK_CONTAINER(context->dialog),20);
63 gtk_container_add(GTK_CONTAINER(context->dialog),
button);
64 
65 gtk_signal_connect(GTK_OBJECT(button),
"clicked",
66 GTK_SIGNAL_FUNC(closeDialog),
67 context->dialog);
68 
69 gtk_window_set_modal(GTK_WINDOW(context->dialog),
70 TRUE);
71 gtk_widget_show(button);
72 }
73 gtk_widget_show(context->dialog);
74 }
75 
76 
77 void closeDialog(GtkWidget *widget,gpointer data)
78 {
79 gtk_widget_hide(GTK_WIDGET(data));
80 }
```

顶级窗口包含在第 29 到 33 行中定义的按钮。该按钮的回调函数是定义在第 52 行的 `showDialog()`。传递给回调的数据是定义在第 8 行的 `hidingContext` 结构体。在更大的应用程序中，该结构体可以扩展以容纳更多信息；但在此示例中，它仅包含一个指向对话框组件的指针。对 `hidingContext()` 的第一次调用（第 58 行）确定对话框不存在，因此它创建对话框组件并将其地址存储在结构体中。一旦对话框被创建，它就一直存在，后续对 `hidingContext()` 的调用只需确保通过第 74 行对 `gtk_widget_show()` 的调用来显示它。

