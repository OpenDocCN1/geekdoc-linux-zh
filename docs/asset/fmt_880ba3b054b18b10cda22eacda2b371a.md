
```c
/** notebook.c **/
#include <gnome.h>

GtkWidget *makeNotebook();
GtkWidget *makeButtonPage(gchar *str);
GtkWidget *makeTextPage(gchar *str);

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data);

int main(int argc, char *argv[])
{
    GtkWidget *window;
    GtkWidget *notebook;

    gnome_init("notebook", "1.0", argc, argv);
    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_window_set_default_size(GTK_WINDOW(window), 200, 200);

    gtk_signal_connect(GTK_OBJECT(window),
                "delete_event",
                GTK_SIGNAL_FUNC(eventDelete),
                NULL);
    
    gtk_signal_connect(GTK_OBJECT(window),
                "destroy",
                GTK_SIGNAL_FUNC(eventDestroy),
                NULL);

    notebook = makeNotebook();

    gtk_container_add(GTK_CONTAINER(window), notebook);
    gtk_widget_show_all(window);
    gtk_main();
    exit(0);
}

GtkWidget *makeNotebook() {
    GtkWidget *notebook;
    GtkWidget *page;
```

```c
40	GtkWidget *label;
41
42	notebook = gtk_notebook_new();
43	gtk_notebook_set_tab_pos(GTK_NOTEBOOK(notebook),
44		GTK_POS_TOP);
45
46	page = makeButtonPage("First Button Page");
47	label = gtk_label_new("Front");
48	gtk_notebook_append_page(GTK_NOTEBOOK(notebook),
49		page,label);
50
51	page = makeTextPage("first");
52	label = gtk_label_new("Second");
53	gtk_notebook_append_page(GTK_NOTEBOOK(notebook),
54		page,label);
55
56	page = makeButtonPage("Second Button Page");
57	label = gtk_label_new("Third");
58	gtk_notebook_append_page(GTK_NOTEBOOK(notebook),
59		page,label);
60
61	page = makeTextPage("second");
62	label = gtk_label_new("Fourth");
63	gtk_notebook_append_page(GTK_NOTEBOOK(notebook),
64		page,label);
65
66	page = makeButtonPage("Third Button Page");
67	label = gtk_label_new("Back");
68	gtk_notebook_append_page(GTK_NOTEBOOK(notebook),
69		page,label);
70
71	return(notebook);
72 }
73 GtkWidget *makeButtonPage(gchar *str)
74 {
75	GtkWidget *alignment;
76	GtkWidget *button;
77
78	alignment = gtk_alignment_new(0.5,0.5,0.5,0.5);
79	button = gtk_button_new_with_label(str);
80	gtk_container_add(GTK_CONTAINER(alignment),button);
81
82	return(alignment);
83 }
84 GtkWidget *makeTextPage(gchar *str)
85 {
86	int i;
87	GtkWidget *text;
88	gchar string[80];
89
90	text = gtk_text_new(NULL,NULL);
91            sprintf(string,
92                "This is the text of the %s text page.. ",str);
93            for(i=0; i<80; i++) {
94                gtk_text_insert(GTK_TEXT(text),NULL,NULL,NULL,
95                    string,-1);
96            }
97        }
98        return(text);
99    }
100 gint eventDelete(GtkWidget *widget,
101                GdkEvent *event,gpointer data) {
102        return(FALSE);
103    }
104 gint eventDestroy(GtkWidget *widget,
105                GdkEvent *event,gpointer data) {
106        gtk_main_quit();
107        return(0);
108    }
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_165_0.png)

**图 5-22：** 一个包含五页的笔记本

从第 37 行开始的函数 `makeNotebook()` 创建笔记本并将若干页面存储其中。笔记本在第 42 至 44 行创建并配置。页面在第 46 至 69 行创建并插入到笔记本容器中。（实际的页面由从第 73 行和第 84 行开始的 `makeButtonPage()` 和 `makeTextPage()` 函数创建。）

笔记本容器可以将选项卡行定位在其四条边中的任意一边。调用 `gtk_notebook_set_tab_pos()` 用于设置选项卡的位置。值 `GTK_POS_TOP` 将选项卡置于顶部（如图 5-22 所示）。使用值 `GTK_POS_BOTTOM` 将选项卡置于底部，如图 5-23 所示。使用 `GTK_POS_LEFT` 将选项卡置于左侧，生成如图 5-24 所示的窗口。值 `GTK_POS_RIGHT` 将选项卡置于右侧。默认值，也是可能最常用的位置，是 `GTK_POS_TOP`。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_166_0.png)

**图 5-23：** 选项卡位于底部的笔记本

![](img/8bcc1ba72831c7d67cfc8b395deab95f_166_1.png)

**图 5-24：** 选项卡位于左侧的笔记本

每个页面控件都通过函数 `gtk_notebook_append_page()` 安装到笔记本中。此函数将新页面添加到笔记本中已存在的任何页面之后。换句话说，新添加的页面成为笔记本中的最后一个页面。以这种方式添加的页面，其选项卡会根据选项卡方向定位在底部或最右侧。

调用 `gtk_notebook_append_page()` 时有第三个参数。在向笔记本添加新页面时，需要指定一个控件用作选项卡上的标签。通常，在此示例中，使用标签控件在选项卡上显示文本。然而，并没有任何限制禁止使用图形控件；这种控件会使选项卡看起来并像图标一样工作。

还有一个名为 `gtk_notebook_prepend_page()` 的函数——具有与 `gtk_notebook_append_page()` 相同的参数集——它执行相同的功能，除了插入的页面成为第一页而不是最后一页。
