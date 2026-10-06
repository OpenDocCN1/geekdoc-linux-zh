
```c001 #include <gtk/gtk.h>
002 #include <stdlib.h>
003
004 #define SQUARE_X 0
005 #define SQUARE_O 1
006 #define SQUARE_BLANK 2
007
008 static GtkWidget *table, *dialog, *entryrow, *entrycolor;
009
010 typedef struct _square {
011     unsigned char type;
012     GtkWidget *child;
013 };
014
015 static square board[9] = {
016 {SQUARE_BLANK, NULL, NULL}, {SQUARE_BLANK, NULL, NULL},
017 {SQUARE_BLANK, NULL, NULL}, {SQUARE_BLANK, NULL, NULL},
018 {SQUARE_BLANK, NULL, NULL}, {SQUARE_BLANK, NULL, NULL},
019 {SQUARE_BLANK, NULL, NULL}};
020
021 static GtkWidget *
022 MakeXSquare ( GtkWidget *window)
023 {
024
025     GdkPixmap *pixmap;
026     GdkBitmap *mask;
027     GtkWidget *wpmap;
028
029     pixmap = gdk_pixmap_create_from_xpm(window, &mask,
030     &window->style_bg[GTK_STATE_NORMAL], "x.xpm");
031     wpmap = gtk_pixmap_new(pixmap, mask);
031   return( wpmap );
032  }
033 
034   static int
035   TryMoveTo( int row, int col)
036   {
037     GtkWidget *widget;
038     if ( board[ row * 3 + col ].type == SQUARE_BLANK ) {
039         widget = MakeSquare(dialog);
040         gtk_table_attach_defaults( GTK_TABLE ( table ,
041             widget, col + 1, row, row + 1 );
042         gtk_widget_destroy(board[ row * 3 + col ].child );
043         gtk_widget_show( widget );
044         board[ row * 3 + col ].type = SQUARE_O;
045         board[ row * 3 + col ].child = widget;
046         return( 1 );
047     }
048     return( 0 );
049 }
051   static void
052   InitializeBoard( void )
053   {
054     GtkWidget *blank, button;
055     int i, j;
056 
057     for ( i = 0; i < 3; i++) {
058         for ( j = 0; j < 3; j++) {
059             blank = MakeBlankSquare( dialog );
060             gtk_widget_show( blank );
061             if ( board[ j * 3 + i ].child != NULL ) {
062                 gtk_widget_destroy(
063                 board[ j * 3 + i ].child );
064                 gtk_table_attach_defaults( GTK_TABLE ( table ,
065                     blank, i + 1, j, j + 1 );
066                 board[ j * 3 + i ].type = SQUARE_BLANK;
067                 board[ j * 3 + i ].child = blank;
068             }
069         }
070   static void
071   MakeMove( gpointer ignored )
072   {
073     char *text;
074     int row, col;
075     GtkWidget *widget;
076     text = gtk_entry_get_text( GTK_ENTRY( entryrow ) );
077     row = atoi( text );
078     text = gtk_entry_get_text( GTK_ENTRY( entrycol ) );
079     col = atoi( text );
080     if ( row < 1 || row > 3 || col < 1 || col > 3 )
081       return;
082     col--;
083     if ( board[row * 3 + col ].type == SQUARE_BLANK ) {
084       widget = MakeSquare( dialog );
085       gtk_table_attach_defaults( GTK_TABLE( table ),
086             widget, col + 1, row, row + 1 );
087       gtk_widget_destroy(board[row * 3 + col ].child);
088       gtk_widget_show(widget);
089       board[row * 3 + col ].type = SQUARE_X;
090       board[row * 3 + col ].child = widget;
091     if (CheckForWin())
092       NewGame( NULL );
093     else
094       ComputerMove();
095 } static GtkWidget *
096 GtkTTDialog( void ) {
097   GtkWidget *mouse, *quit, *newgame, *label, *rlabel,
098   dialog_window, *outerbox, *hbox;
099   dialog_window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
100  gtk_window_position(GTK_WINDOW(dialog_window), GTK_WINDOW_POS_MOUSE);
101  gtk_signal_connect(GTK_OBJECT(dialog_window), "destroy",
102  GTK_SIGNAL_FUNC(gtk_quit), dialog_window);
103  gtk_window_set_title(GTK_WINDOW(dialog_window), "Gtk-Toe");
104  gtk_window_set_policy(GTK_WINDOW(dialog_window), FALSE, FALSE);
105  gtk_container_border_width(GTK_CONTAINER(dialog_window), 0);
106  outerbox = gtk_box_new(FALSE, 0);
107  gtk_box_spacing(GTK_BOX(outerbox), 10);
108  gtk_container_add(GTK_CONTAINER(dialog_window), outerbox);
109  table = gtk_table_new(3, 3, TRUE);
110  gtk_box_pack_start(GTK_BOX(outerbox), table, FALSE, 0);
111  rule = gtk_separator_new();
112  gtk_box_pack_start(GTK_BOX(outerbox), rule, FALSE, 0);
113  hbox = gtk_box_new(FALSE, 0);
114  gtk_box_pack_start(GTK_BOX(outerbox), hbox, FALSE, 0);
115  gtk_box_spacing(GTK_BOX(hbox), 10);
116  gtk_box_pack_start(GTK_BOX(outerbox), hbox, TRUE, 0);
117  rlabel = gtk_label_new("Row");
118  gtk_box_pack_start(GTK_BOX(hbox), rlabel, TRUE, 0);
119  entryrow = gtk_entry_new();
120  gtk_widget_set_size(entryrow, 30, -1);
121  gtk_box_pack_start(GTK_BOX(hbox), entryrow, TRUE, 0);
122  rlabel = gtk_label_new("Column");
123  gtk_box_pack_start(GTK_BOX(hbox), rlabel, TRUE, 0);
124  entrycol = gtk_entry_new();
125  gtk_widget_set_size(entrycol, 30, -1);
126  gtk_box_pack_start(GTK_BOX(hbox), entrycol, TRUE, 0);
127  move = gtk_button_new_label("Move");
128  gtk_box_pack_start(GTK_BOX(hbox), move, TRUE, 10);
129  gtk_signal_connect(GTK_OBJECT(move), "clicked",
130  GTK_SIGNAL_FUNC(MakeMove), NULL);
131  rule = gtk_separator_new();
132  gtk_box_pack_start(GTK_BOX(outervbox), rule, FALSE, FALSE, 0);
133  bbox = gtk_button_new_label();
134  gtk_box_pack_start(GTK_BOX(outervbox), bbox, TRUE, TRUE, 0);
135  newgame = gtk_button_new_label("New Game");
136  gtk_box_pack_start(GTK_BOX(hbox), newgame, FALSE, FALSE, 10);
137  gtk_signal_connect(GTK_OBJECT(newgame), "clicked",
138  GTK_SIGNAL_FUNC(NewGame));
139  quit = gtk_button_new_label("Quit");
140  gtk_box_pack_start(GTK_BOX(hbox), quit, TRUE, 10);
141  gtk_signal_connect(GTK_OBJECT(quit), "clicked",
142  GTK_SIGNAL_FUNC(gtk_main), dialog_window);
143  gtk_widget_show_all(dialog_window);
144  gtk_main(argc, argv);
145 }
```

*(注：原文提供的代码块中存在行号重复和逻辑错乱的情况，翻译时严格遵循“代码块不需要翻译”的原则，保持了原样结构。)*

# Chapter 11 • More Container Classes

## GtkApplication 级 API 概览（续）

在工具栏的前面插入一个指定类型的元素：

```c
GtkWidget *
gtk_toolbar_prepend_element (GtkToolbar *toolbar,
GtkToolbarChildType type, GtkWidget *widget,
const char *text, const char *tooltip_text,
const char *tooltip_private_text, GtkWidget *icon,
const GtkSignalFunc callback, gpointer user_data);
```

在工具栏指定位置插入一个指定类型的元素：

```c
GtkWidget *
gtk_toolbar_insert_element (GtkToolbar *toolbar,
GtkToolbarChildType type, GtkWidget *widget,
const char *text, const char *tooltip_text,
const char *tooltip_private_text, GtkWidget *icon,
const GtkSignalFunc callback, gpointer user_data, gint position);
```

在工具栏末尾添加一个类型为 `GTK_TOOLBAR_CHILD_WIDGET` 的项目：

```c
void
gtk_toolbar_append_widget (GtkToolbar *toolbar, GtkWidget *widget,
const char *tooltip_text, const char *tooltip_private_text);
```

在工具栏的前面添加一个类型为 `GTK_TOOLBAR_CHILD_WIDGET` 的项目：

```c
void
gtk_toolbar_prepend_widget (GtkToolbar *toolbar, GtkWidget *widget,
const char *tooltip_text, const char *tooltip_private_text);
```

在工具栏指定位置插入一个类型为 `GTK_TOOLBAR_CHILD_WIDGET` 的项目：

```c
void
gtk_toolbar_insert_widget (GtkToolbar *toolbar, GtkWidget *widget,
const char *tooltip_text, const char *tooltip_private_text,
gint position);
```

将工具栏的方向更改为垂直或水平：

```c
void
gtk_toolbar_set_orientation (GtkToolbar *toolbar,
GtkOrientation orientation);
```

设置工具栏样式：

```c
void
gtk_toolbar_set_style (GtkToolbar *toolbar, GtkToolbarStyle style);
```

设置工具栏中间距的大小（以像素为单位）：

```c
void
gtk_toolbar_set_space_size (GtkToolbar *toolbar, gint space_size);
```

设置工具栏中间距的样式：

```c
void
gtk_toolbar_set_space_style (GtkToolbar *toolbar,
GtkToolbarSpaceStyle space_style);
```

## 级 API 概览（续）

启用或禁用菜单栏的工具提示：

```c
void
gtk_toolbar_set_tooltips(GtkToolbar *toolbar, gint enable);
```

设置按钮样式：

```c
void
gtk_toolbar_set_button_relief(GtkToolbar *toolbar,
GtkReliefStyle relief);
```

获取按钮样式：

```c
GtkReliefStyle
gtk_toolbar_get_button_relief(GtkToolbar *toolbar);
```

## GtkToolbar 描述

`GtkToolbar` 类专门为需要实现如图 11.29 所示工具栏的应用程序设计。工具栏管理一组按钮，用户可以通过点击这些按钮来激活应用程序任务或弹出应用程序对话框。对于许多用户来说，相比从菜单中选择项目等替代方案，工具栏提供了一种更简单、更直观的方式来访问应用程序的功能。因为工具栏对用户是始终可见的，应用程序选项以工具栏按钮的形式呈现，这对于用户来说比菜单项中的选项更容易发现。

| Bluefish 0.3.6 HTML 编辑器 | | |

| :--- | :--- | :--- |

| 文件 编辑 查看 项目 标签 对话框 外部 | | |

| X X | | 帮助 |

| 快速 字体 表格 框架 表单 列表 CSS 其他 | | |

| types need body B I T U s <br> <br> obst <br> | | |

| chapter11 | | |
