
# 10. 容器小部件

```c
GtkWidget *list_item;

int i;

char buffer[16];

/* 创建一个滚动窗口，仅在需要时显示滚动条 */

scrolled_window = gtk_scrolled_window_new(NULL, NULL);

gtk_scrolled_window_set_policy(GTK_SCROLLED_WINDOW(scrolled_window),

                               GTK_POLICY_AUTOMATIC,

                               GTK_POLICY_AUTOMATIC);

/* 创建新列表并将其放入滚动窗口 */

list = gtk_list_new();

gtk_container_add(GTK_CONTAINER(scrolled_window), list);

gtk_widget_show(list);

/* 向窗口添加一些消息 */

for (i=0; i<10; i++) {
    sprintf(buffer, "Message %d", i);
    list_item = gtk_list_new_with_label(buffer);
    gtk_container_add(GTK_CONTAINER(list), list_item);
    gtk_widget_show(list_item);
}

return scrolled_window;
```

/* 当窗口被初始化时，向我们的文本控件添加文本的回调。
   我们也可以通过 gtk_widget_realize 强制窗口，但它必须先是层级的一部分 */
void realize_text (GtkWidget *text, gpointer data) {
    gtk_widget_freeze(GTK_TEXT(text));
    gtk_text_insert(GTK_TEXT(text), NULL,
"From: path.gov\n"
"To: mom@nasa.gov\n"
"Subject: Made it!\n"
"We got this morning. The weather has been great, and there are lots of sights.\n"
"Sojner says hi. See you soon.\n");
    gtk_widget_thaw(GTK_TEXT(text));
}

/* 创建显示“消息”的滚动区域 */
GtkWidget *create_text (void)
{
    GtkWidget *table;
    GtkWidget *text;
    GtkWidget *hscrollbar;
    GtkWidget *vscrollbar;
    /* 创建持有控件和滚动条的表格 */
    table = gtk_table_new(2, 2, FALSE);
    /* 在左上放置控件。注意在 y 方向使用了 GTK_SHRINK */
    text = gtk_text_new(NULL, NULL);
    gtk_table_attach(GTK_TABLE(table), text, 0, 0, 1, 1,
    GTK_FILL | GTK_EXPAND, GTK_FILL | GTK_EXPAND | GTK_SHRINK);
    gtk_widget_show(text);
    /* 在左下放置水平滚动条 */
    hscrollbar = gtk_hscrollbar_new(GTK_TEXT(text)->get_adjustment());
    gtk_table_attach(GTK_TABLE(table), hscrollbar, 0, 1, 1, 2,
    GTK_EXPAND | GTK_FILL, GTK_FILL, 0, 0);
    gtk_widget_show(hscrollbar);
    /* 在右上放置垂直滚动条 */
    vscrollbar = gtk_vscrollbar_new(GTK_TEXT(text)->get_adjustment());
    gtk_table_attach(GTK_TABLE(table), vscrollbar, 1, 2, 0, 1,
    GTK_FILL | GTK_EXPAND | GTK_FILL | GTK_SHRINK, 0, 0);
    gtk_widget_show(vscrollbar);
    /* 当文本控件被初始化时添加一个处理器以放入消息 */
    gtk_signal_connect(GTK_OBJECT(text), "realize",
    G_CALLBACK_FUNC(realize_text), NULL);
    return table;
}

int
main (int argc, char *argv[])
{
  GtkWidget *window;
  GtkWidget *vpaned;
  GtkWidget *list;
  GtkWidget *text;
  gtk_init (argc, &argv);
  window = gtk_window_new (GTK_WINDOW_TOPLEVEL);
  gtk_window_set_title(GTK_WINDOW (window), "Paned Windows");
  gtk_signal_connect(GTK_OBJECT (window), "destroy",
      G_CALLBACK_FUNC (gtk_main_quit), NULL);
  gtk_container_set_border_width(GTK_CONTAINER (window), 10);
  gtk_widget_set_size(GTK_WIDGET (window), 450, 400);
  /* 创建一个 vpan 控件并添加到我们的顶层窗口 */
  vpaned = gtk_vpaned_new ();
  gtk_container_add (GTK_CONTAINER(window), vpaned);
  gtk_paned_set_handle_size (GTK_PANED(vpaned),
      10);
  gtk_paned_set_gutter_size (GTK_PANED(vpaned),
      15);
  gtk_widget_show (vpaned);
  /* 现在创建窗口的两个部分的内容 */
  list = create_list ();
  gtk_paned_add (GTK_PANED(vpaned), list);
  gtk_widget_show (list);
  text = create_text ();
  gtk_paned_add2 (GTK_PANED(vpaned), text);
  gtk_widget_show (text);
  gtk_widget_show (window);
  gtk_main();
  return 0;
}

/* example-end */
```

## 10.9 滚动窗口

滚动窗口用于在实际窗口内创建一个可滚动区域。你可以将任何类型的小部件插入到滚动窗口中，无论尺寸如何，都可以通过滚动条进行访问。

使用以下函数可以创建一个新的滚动窗口：

```c
GtkWidget *gtk_scrolled_window_new( GtkAdjustment *adjustment,
GtkAdjustment *vadjustment );
```

其中第一个参数是水平方向的调整项，第二个是垂直方向的调整项。这些参数通常被设置为 `NULL`。

另一个视口函数用于更改其外观：

```c
void gtk_viewport_set_shadow_type( GtkViewport *viewport,
GtkShadowType type );
```

`type` 参数的可能值：

- `GTK_SHADOW_NONE`
- `GTK_SHADOW_IN`
- `GTK_SHADOW_OUT`
- `GTK_SHADOW_ETCHED_IN`
- `GTK_SHADOW_ETCHED_OUT`

另一个视口函数用于更改其外观：

```c
void gtk_viewport_set_vadjustment( GtkViewport *viewport,
GtkAdjustment *adjustment );
```
