

28	GDK_SIGNAL_FUNC(eventDelete), NULL);
29	gdk_signal_connect(GTK_OBJECT(topLevel), "destroy",
30		GDK_SIGNAL_FUNC(eventDestroy), NULL);
31	
32	gdk_widget_show_all(topLevel);
33	
34	bitmap = gdk_bitmap_create_from_data(NULL, xbitmap_bits,
35		xbitmap_width, xbitmap_height);
36	mask = gdk_bitmap_create_from_data(NULL, xmask_bits,
37		xmask_width, xmask_height);
38	cursor = gdk_cursor_new_from_pixmap(
39		bitmap, mask,
40		&oneColor, &zeroColor,
41		xbitmap_x_hot, xbitmap_y_hot);
42	gdk_window_set_cursor(topLevel->window, cursor);
43	
44	gtk_main();
45	exit(0);
46	}
47	gint eventDelete(GtkWidget *widget,
48	GdkEvent *event, gpointer data) {
49	return(FALSE);
50	}
51	gint eventDestroy(GtkWidget *widget,
52	GdkEvent *event, gpointer data) {
53	gtk_main_quit();
54	return(0);
55	}

为了在程序中使用这两个位图，必须将它们转换为 `GdkBitmap` 对象。我们通过调用 `gdk_bitmap_create_from_data()` 来实现这一点（见第 34 至 37 行）。该函数的第一个参数可以是 `GdkWindow` 对象，但在本例中并非必需，因为默认值是根窗口。其余三个参数是定义位图布局的值。

`GdkCursor` 对象通过第 38 行的 `gdk_cursor_new_from_pixmap()` 调用创建。前两个参数是由驻留内存的位图创建的两个 `GdkBitmap` 对象。第二个和第三个参数是用于绘制光标的两种颜色。示例中的颜色定义在第 12 和 13 行，分别为红色和黑色。`oneColor` 定义为红色，`zeroColor` 为黑色。当掩码为 1 且位图像素为 0 时，像素为黑色。当掩码为 1 且位图为 1 时，颜色为红色。最后两个参数是热点的 x 和 y 坐标。

第 42 行的 `gdk_window_set_cursor()` 调用使得新建的光标成为每当鼠标指针位于窗口内时显示的光标。

## 从 XPM 创建光标

也可以从 XPM 数据创建光标，但必须省略颜色信息。以下示例通过选择 XPM 中的一个字母来表示“黑色”颜色，另一个字母表示“白色”颜色来实现这一点。光标通常绘制为黑白，但正如本例所示，您可以选择任意两种喜欢的颜色。所有既不是黑色也不是白色的像素都是透明的。

文件 `sancha.xpm` 的内容如下所示：

```text
/* XPM */
/* sancha.xpm **/
static char *sancha[] = {
"24 24 5 1",
" c none",
"B c Black",
"W c White",
"r c Red",
"y c Yellow",
"rWrrWWWWWW WWWWWWWWrn",
"rrWBBB BB rWWWBBBBBWrn",
"rrrWBBBBBB WWWBBBWrn",
"rrrWWWBBBBWWW WWWBBBWrn",
"rrrWBBBBBB WWWBBBWrn",
"rrrrWWWWWWWW WWWWWWWWWW",
"rrrWWWWW WWWWWWWWrn",
"rrrWBBBBBBBBBBBBBBWrn",
"rrrrWBBB BBBB BBBBWWrrr",
"rrrrrrWBBBBB BBBB WWrrrr",
"rrrrrrrrWWBBBBBBBBWWrrrrrr",
"rrrrrrrrrrWWBBBBWWrrrrrrrr",
"rrrrrrrrrrrrWWBBWWrrrrrrrrrr",
"rrrrrrrrrrrrrWWBBWWrrrrrrrrrrrr",
"rrrrrrrrrrrrrrWWBBWWrrrrrrrrrrrrrr",
"yyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
"yyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
"yyyyyyyyyyyyWWBBWWyyyyyyyyyyyyyyyy",
"yyyyyyyyyyyyWBBBBBWWyyyyyyyyyyyyyyyy",
"yyyyyyyyyyyyWWBBWWyyyyyyyyyyyyyyyy",
"yyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
"yyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
"yyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
"WWWWWWWWWWWWWWWWWWWWWWWWWW",
"WB WBBBBBBBBBBBBBBBBBBBBBWWW",
"WWWWWWWWWWWWWWWWWWWWWWWWWW"
};
```

此 XPM 定义包含五种颜色。它由一个中心黑色区域组成，周围用白色描边；两侧的红色和黄色为背景。顶部有一个透明区域。它显示在图 7-8 中。

### 图 7-8：待转换为光标的 XPM 图形

在以下示例中，XPM 中的两种颜色（B 和 W）被选中以表示可见像素位置。其他颜色（r、y 和空白）都变为透明。带有其光标的窗口显示在图 7-9 中。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_220_0.png)

```c
1 /** xpmcursor.c **/
2 #include <gnome.h>
3
4 gint eventDelete(GtkWidget *widget,
5                 GdkEvent *event, gpointer data);
6 gint eventDestroy(GtkWidget *widget,
7                 GdkEvent *event, gpointer data);
8 GdkCursor *newCursorFromXPM(char *xpm[],
9                             char blackLetter, GdkColor *blackColor,
10                            char whiteLetter, GdkColor *whiteColor,
11                            gint xHot, gint yHot);
12
13 #include "sancha.xpm"
14
15 GdkColor green = {0, 0x0000, 0xFF, 0x0000};
16 GdkColor black = {0, 0x0000, 0x0000, 0x0000};
17
18 int main(int argc, char *argv[])
19 {
20     GtkWidget *topLevel;
21     GdkCursor *cursor;
22
23     gnome_init("xpmcursor", "1.0", argc, argv);
24     topLevel = gtk_window_new (GTK_WINDOW_TOPLEVEL);
25     gtk_window_set_default_size (GTK_WINDOW (topLevel), 150, 150);
26
27     gtk_signal_connect (GTK_OBJECT (topLevel), "delete_event",
28                         GTK_SIGNAL_FUNC (eventDelete), NULL);
29     gtk_signal_connect (GTK_OBJECT (topLevel), "destroy",
30                         GTK_SIGNAL_FUNC (eventDestroy), NULL);
31
32     gtk_widget_show_all (topLevel);
```

34

35

36 cursor = newCursorFromXPM(sancha,
37	"8",&black,'W',&green,
38	12,13);
39
40	gdk_window_set_cursor(topLevel->window,cursor);
41
42	gtk_main();
43	exit(0);
44	}
45 GdkCursor *newCursorFromXPM(gchar *xpm[],
46	gchar blackLetter,GdkColor *blackColor,
47	gchar whiteLetter,GdkColor *whiteColor,
48	gint xHot,gint yHot)
49 {
50	gint height;
51	gint width;
52	gint colors;
53	gint pchars;
54	gint x;
55	gint y;
56	GdkBitmap *bitmap;
57	GdkBitmap *mask;
58	GdkCursor *cursor;
59
60	guchar *bitmapData;
61	guchar *maskData;
62	gint byteIndex = 0;
63	gint bitCount = 0;
64
65	sscanf(xpm[0],"%d %d %d %d",
66	&height,&width,&colors,&pchars);
67	g_assert(pchars == 1);
68
69	bitmapData = (guchar *)g_malloc((width * height) / 8);
70	maskData = (guchar *)g_malloc((width * height) / 8);
71
72	for(y=(colors+4); y < (height+4); y++) {
73	for(x=0; x<width; x++) {
74	if (xpm[y][x] == whiteLetter) {
75	maskData[byteIndex] |= 0x80;
76	bitmapData[byteIndex] |= 0x80;
77	} else if(xpm[y][x] == blackLetter) {
78	maskData[byteIndex] |= 0x80;
79	}
80	if(++bitCount == 8) {
81	byteIndex++;
82	bitCount = 0;
83	} else {
84	maskData[byteIndex] >>= 1;
85	bitmapData[byteIndex] >>= 1;
86	}
87	}
88	}
89	bitmap = gdk_bitmap_create_from_data(NULL,bitmapData,
90	width,height);
91	mask = gdk_bitmap_create_from_data(NULL,maskData,
92	width,height);
93	cursor = gdk_cursor_new_from_pixmap(bitmap,mask,
94	whiteColor,blackColor,
95	xHot,yHot);
96	g_free(bitmapData);
97	g_free(maskData);
98	return(cursor);
99	}
100
101	gint eventDelete(GtkWidget *widget,
102	GdkEvent *event,gpointer data) {
103	return(FALSE);
104	}
105	gint eventDestroy(GtkWidget *widget,
106	GdkEvent *event,gpointer data) {
107	gtk_main_quit();
108	return(0);
109	}

XPM 数据在第 13 行包含。用于光标的两种颜色在第 15 和 16 行定义。在本例中，光标是绿色，外轮廓为黑色。光标对象通过第 35 行的函数调用创建。该函数的第一个参数是 XPM 数据。接下来的两个参数指定成为“黑色”的字母和实际颜色。再接下来的两个参数指定成为“白色”的字母和实际颜色。最后两个参数是光标热点的 x 和 y 坐标。

从 XPM 到 `GtkCursor` 的转换由第 43 行开始的函数 `newCursorFromXPM()` 完成。XPM 数组中的第一个字符串包含描述随后数据的一组数字，并在第 65 行读取。第 66 行确保每种颜色由单个字符表示，因为此函数无法处理每种颜色多于一个字符的情况。第 67 和 68 行分配了用于存放位图的空间。函数 `g_malloc()` 调用 `calloc()` 来实际分配内存，因此返回的数据初始化为零。

第 70 行开始的循环使用 `y` 的值作为输入数组中每个字符串的索引。内层循环从第 71 行开始，对字符串中的每个字符迭代一次。在第 72 行，如果像素要用“白色”绘制，则位图和掩码的高位位都被置位。在第 75 行，如果像素要用“黑色”绘制，则掩码的高位位被置位。第 78 至 84 行使用位计数器来确定当前字节是否已满。如果字节已满，索引递增到下一个字节——否则，字节内的位会被移位以为下一个位腾出空间。

位图在第 87 和 89 行创建。这些位图在第 91 行用于创建光标。第 94 至 96 行释放已分配的内存并将 `GdkCursor` 返回给调用者。

