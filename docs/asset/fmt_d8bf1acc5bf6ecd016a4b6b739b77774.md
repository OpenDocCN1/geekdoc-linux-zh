
# 列表 11.9 连接数字调节框到滚动条

```
#include <gtk/gtk.h>

#define ROWS 40
#define COLS 40

static GtkWidget *sw, *hspinner, *vspinner;

static void
HorizontalSpinChanged (GtkWidget *widget, gpointer data)
{
    GtkAdjustment *adj;
    int value;

    value = gtk_spin_button_get_value_as_int (GTK_SPIN_BUTTON(hspinner));
    adj = gtk_scrolled_window_get_adjustment (GTK_SCROLLED_WINDOW(sw));
    gtk_adjustment_set_value (adj, (float) value * (int) data);
}
static void
VerticalSpinChanged (GtkWidget *widget, gpointer data)
{
    GtkAdjustment *adj;
    int value;

    value = gtk_spin_button_get_value_as_int (GTK_SPIN_BUTTON(vspinner));
    adj = gtk_scrolled_window_get_vadjust (GTK_SCROLLED_WINDOW (sw));
    gtk_adjustment_set_value(adj, (float) value * (int) data);
}
void
CreateScrolledWindow() {
    GtkWidget *button, *vbox,*table;
    GtkAdjustment *adj1,adj2;
    guint width, height;
    int i, j;
    char buf[32];

    dialog = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_window_position(GTK_WINDOW(dialog), GTK_WIN_POS);
    gtk_widget_set_size(GTK_WIDGET(dialog), 200, 200);
    gtk_signal_connect(GTK_OBJECT(dialog), "destroy",
    GTK_SIGNAL_FUNC(gtk_main_quit), NULL);
    gtk_window_set_title(GTK_WINDOW(dialog),
    "GtkScrolledWindow Demo");
    gtk_container_border_width(GTK_CONTAINER(dialog), 0);

    vbox = gtk_box_new( FALSE, 0 );
    gtk_container_add(GTK_CONTAINER(dialog), vbox);

    sw = gtk_scrolled_window_new( NULL, NULL );
    gtk_box_pack_start(GTK_BOX (vbox), sw, TRUE, 0);

    table = gtk_table_new( ROWS, COLS, TRUE );
    gtk_scrolled_window_add_viewport( GTK_SCROLLED_WINDOW (sw),
    table );

    for ( i = 0; i < ROWS; i++) {
        for ( j = 0; j < COLS; j++) {
            sprintf( buf, "%d,%d", i, j);
            button = gtk_button_new_with_label( buf );
            gtk_table_add_defaults( GTK_TABLE ( table ),
            button, j, 1, i, 1);
        }
    }
    gtk_widget_show_all(dialog);

    width = button_allocation.width;
    height = button_allocation.height;

    hbox = gtk_box_new( FALSE, 0 );
    gtk_box_pack_end(GTK_BOX (vbox), hbox, FALSE, 0 );

    adj1 = (GtkAdjustment *) gtk_adjustment_new(0.0, 0.0, 0.0,
      (gfloat) COLS, 1.0, 1.0, 0.0);
    hspinner = gtk_spin_button_new(adj1, 0, 0);
    gtk_spin_button_set_wrap(GTK_SPIN_BUTTON (hspinner), TRUE);
    gtk_box_pack_start(GTK_BOX (hbox), hspinner, TRUE, 0);
    gtk_signal_connect(GTK_OBJECT (adj1), "value_changed",
      GTK_SIGNAL_FUNCTION(HorizontalSpinChanged), (gpointer) width);

    adj2 = (GtkAdjustment *) gtk_adjustment_new(0.0, 0.0, 0.0,
      (gfloat) ROWS - 1, 1.0, 0.0);
    vspinner = gtk_spin_button_new(adj2, 0, 0);
    gtk_spin_button_set_wrap(GTK_SPIN_BUTTON (vspinner), TRUE);
    gtk_box_pack_start(GTK_BOX (hbox), vspinner, TRUE, 0);
    gtk_signal_connect(GTK_OBJECT (adj2), "value_changed",
      GTK_SIGNAL_FUNCTION(VerticalSpinChanged), (gpointer) height);
    gtk_widget_show_all( hbox );
}
main( int argc, char *argv[]) {
    gtk_init(&argc, &argv);
    CreateScrolledWindow();
    gtk_main();
}
```

首先注意到的是，我们不再与滚动窗口和数字调节框共享调整对象。每对组件都有其自己的一对调整对象。在第 83 行（针对水平数字调节框），为每个数字调整对象都启了一个 `value_changed` 信号函数。水平数字调节框信号函数传递了由表格组件管理的按钮（表格子组件）的宽度，而垂直数字调节框的 `value_changed` 函数传递了由表格组件管理的按钮的高度。宽度和高度用于计算当数字值变化时，滚动条应该移动的距离。数字调节框的 `value_changed` 函数在第 019 行到 028 行被查询。数字调节框的值在第 025 行查询。接下来，获取垂直滚动条调整对象。通过调用 `gtk_adjustment_set_value()`。新的调整值通过乘以按钮的高度（作为信号函数的 `data` 参数传递）和垂直数字调节框的值来计算。

## 设置滚动策略

正如我之前提到的，你的应用程序可以为滚动组件的垂直和水平滚动条指定滚动策略。对于大多数应用程序，默认的 `GTK_POLICY_AUTOMATIC` 通常是正确的选择。要设置滚动

## 574 第 11 章 • 更多容器类

用于设置滚动窗口部件的水平或垂直滚动条策略的函数，请调用 `gtk_scrolled_window_set_policy()`：

```
void
gtk_scrolled_window_set_policy(GtkScrolledWindow *scrolled_window,
      GtkPolicyType hscrollbar_policy,
      GtkPolicyType vscrollbar_policy);
```

第一个参数是滚动窗口部件实例。参数 `hscrollbar_policy` 和 `vscrollbar_policy` 接受表 11.15 中列出的值之一。

### 表 11.15 滚动策略

| 值 | 含义 |
| :--- | :--- |
| `GTK_POLICY_ALWAYS` | 滚动条将始终显示。 |
| `GTK_POLICY_AUTOMATIC` | 当子部件大于视口（`viewport`）时，显示滚动条。 |
