

```c
    72    GTK_SIGNAL_FUNC(topButton),context);
    73    gtk_box_pack_start(GTK_BOX(box),button,
    74        FALSE,TRUE,0);
    75    button = gtk_button_new_with_label("Middle");
    76    gtk_signal_connect(GTK_OBJECT(button),"clicked",
    77        GTK_SIGNAL_FUNC(middleButton),context);
    78    gtk_box_pack_start(GTK_BOX(box),button,
    79        FALSE,TRUE,0);
    80    button = gtk_button_new_with_label("Bottom");
    81    gtk_signal_connect(GTK_OBJECT(button),"clicked",
    82        GTK_SIGNAL_FUNC(bottomButton),context);
    83    gtk_box_pack_start(GTK_BOX(box),button,
    84        FALSE,TRUE,0);
    85    gtk_box_pack_start(GTK_BOX(position),box,
    86        FALSE,FALSE,0);
    87    
    88    context->drawingArea = gtk_drawing_area_new();
    89    gtk_drawing_area_size(
    90        GTK_DRAWING_AREA(context->drawingArea),
    91        WIDTH,HEIGHT);
    92    gtk_signal_connect(GTK_OBJECT(context->drawingArea),
    93        "event",GTK_SIGNAL_FUNC(eventDraw),context);
    94    
    95    frame = gtk_frame_new(NULL);
    96    gtk_container_add(GTK_CONTAINER(frame),
    97        context->drawingArea);
    98    gtk_box_pack_start(GTK_BOX(position),frame,
    99        FALSE,FALSE,0);
   100    
   101    box = gtk_hbox_new(TRUE,10);
   102    button = gtk_button_new_with_label("Left");
   103    gtk_signal_connect(GTK_OBJECT(button),"clicked",
   104        GTK_SIGNAL_FUNC(leftButton),context);
   105    gtk_box_pack_start(GTK_BOX(box),button,
   106        FALSE,TRUE,0);
   107    button = gtk_button_new_with_label("Center");
   108    gtk_signal_connect(GTK_OBJECT(button),"clicked",
   109        GTK_SIGNAL_FUNC(centerButton),context);
   110    gtk_box_pack_start(GTK_BOX(box),button,
   111        FALSE,TRUE,0);
   112    button = gtk_button_new_with_label("Right");
   113    gtk_signal_connect(GTK_OBJECT(button),"clicked",
   114        GTK_SIGNAL_FUNC(rightButton),context);
   115    gtk_box_pack_start(GTK_BOX(box),button,
   116        FALSE,TRUE,0);
   117    gtk_box_pack_start(GTK_BOX(position),box,
   118        FALSE,FALSE,0);
   119    
   120    fontpicker = gnome_font_picker_new();
   121    gtk_signal_connect(GTK_OBJECT(fontpicker),"font-set",
   122        GTK_SIGNAL_FUNC(eventFontSet),context);
   123    gtk_box_pack_start(GTK_BOX(position),fontpicker,
   124        FALSE,FALSE,0);
   125    
   126    return(position);
   127  }
   128  void eventFontSet(GtkWidget *widget,
   129        gchar *string, Context *context) {
   130  
   131      if(context->font != NULL)
   132          gdk_font_unref(context->font);
   133      context->font = gdk_font_load(string);
   134      gdk_window_clear_area_e(context->drawingArea->window,
   135                  0,0,WIDTH,HEIGHT);
   136  }
   137  gboolean eventDraw(GtkWidget *widget,
   138      GdkEvent *event,Context *context) {
   139      gchar outstring[40];
   140      gint lbearing;
   141      gint rbearing;
   142      gint width;
   143      gint ascent;
   144      gint descent;
   145      gint x;
   146      gint y;
   147  
   148      if(context->font == NULL) {
   149          context->font = gdk_font_load(
   150          "-x-bookman-light-r-normal--14-*--*--p-1-iso8859-1");
   151      }
   152  
   153      switch(context->vertical) {
   154      case STRING_TOP:
   155          strcpy(outstring,"Top");
   156          break;
   157      case STRING_MIDDLE:
   158          strcpy(outstring,"Middle");
   159          break;
   160      case STRING_BOTTOM:
   161          strcpy(outstring,"Bottom");
   162          break;
   163      }
   164      switch(context->horizontal) {
   165      case STRING_LEFT:
   166          strcat(outstring," Left");
   167  
   168      case STRING_CENTER:
   169          strcat(outstring," Center");
   170          break;
   171      case STRING_RIGHT:
   172          strcat(outstring," Right");
   173          break;
   174      }
   175  
   176      gdk_text_extents(context->font,    outstring,
   177                  strlen(outstring),
   178                  &lbearing,
   179                  &rbearing,
   180                  &width,
   181                  &ascent,
   182                  &descent);
   183    
   184    
   185      switch(context->vertical) {
   186      case STRING_TOP:
   187          y = ascent;
   188          break;
   189      case STRING_MIDDLE:
   190          y = HEIGHT / 2;
   191          y += (ascent - descent) / 2;
   192          break;
   193      case STRING_BOTTOM:
   194          y = HEIGHT - descent;
   195          break;
   196      }
   197      switch(context->horizontal) {
   198      case STRING_LEFT:
   199          x = 0;
   200          break;
   201      case STRING_CENTER:
   202          x = (WIDTH / 2) - (width / 2);
   203          break;
   204      case STRING_RIGHT:
   205          x = WIDTH - width;
   206          break;
   207      }
   208    
   209      gdk_draw_string(widget->window,
   210                  context->font,
   211                  context->drawingArea->style->black_gc,
   212                  x,y,
   213                  outstring);
   214    
   215      return(TRUE);
   216  }
   217  void topButton(GtkWidget *widget,Context *context) {
   218      context->vertical = STRING_TOP;
   219      gdk_window_clear_area_e(context->drawingArea->window,
   220          0,0,WIDTH,HEIGHT);
   221  }
   222  void middleButton(GtkWidget *widget,Context *context) {
   223      context->vertical = STRING_MIDDLE;
   224      gdk_window_clear_area_e(context->drawingArea->window,
   225          0,0,WIDTH,HEIGHT);
   226  }
   227  void bottomButton(GtkWidget *widget,Context *context) {
   228      context->vertical = STRING_BOTTOM;
   229      gdk_window_clear_area_e(context->drawingArea->window,
   230          0,0,WIDTH,HEIGHT);
   231  }
   232  void leftButton(GtkWidget *widget,Context *context) {
   233      context->horizontal = STRING_LEFT;
   234      gdk_window_clear_area_e(context->drawingArea->window,
   235          0,0,WIDTH,HEIGHT);
   236  }
   237  void centerButton(GtkWidget *widget,Context *context) {
   238      context->horizontal = STRING_CENTER;
   239      gdk_window_clear_area_e(context->drawingArea->window,
   240          0,0,WIDTH,HEIGHT);
   241  }
   242  void rightButton(GtkWidget *widget,Context *context) {
   243      context->horizontal = STRING_RIGHT;
   244      gdk_window_clear_area_e(context->drawingArea->window,
   245          0,0,WIDTH,HEIGHT);
   246  }
   247  gint eventDelete(GtkWidget *widget,
   248                   GdkEvent *event,gpointer data) {
   249      return(FALSE);
   250  }
   251  gint eventDestroy(GtkWidget *widget,
   252                   GdkEvent *event,gpointer data) {
   253      gtk_main_quit();
   254      return(0);
   255  }
```

程序的主线位于第 37 行至 58 行，它设置了一个仅包含一个窗口的 GNOME 应用程序。第 52 行调用 `createPositionWidget()` 创建一个控件，该控件随后在第 54 行通过调用 `gnome_app_set_contents()` 插入主窗口中。

应用程序窗口如图 13-6 所示。顶部一排按钮在垂直方向上重新定位字符串，而底部附近的一排按钮则在水平方向上重新定位。底部的按钮是一个字体选择器，可用于更改被定位字符串的字体。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_438_0.png)

第 59 行的函数 `createPositionWidget()` 创建了显示所需的所有控件，并为它们分配回调函数。在第 14 行定义的 `Context` 结构体用于向此函数以及所有回调函数传递信息，而不是使用全局数据。所有控件都包含在第 67 行调用 `gtk_vbox_new()` 创建的垂直框中。第 69 行至 86 行创建一个水平框并填入按钮。然后，该水平框被插入到垂直框的顶部。每个按钮都分配了自己的回调函数，并将 context 指针作为数据传递给它。

第 88 行至 93 行创建了用于显示文本的绘图区域。调用 `gtk_drawing_area_size()` 将绘图区域的大小设置为在第 4 行和第 5 行定义的 `WIDTH` 和 `HEIGHT` 值。回调函数 `eventDraw()` 连接到绘图区域，因此每当发生暴露事件时，都会调用该函数来绘制窗口。

第 95 行至 118 行创建底部附近控制显示文本水平位置的按钮。每个按钮都分配了自己的回调函数。

第 120 行至 124 行通过调用 `gnome_font_picker_new()` 创建了一个 `GnomeFontPicker` 控件。其回调函数是 `eventFontSet()`，它被作为垂直框的最后一个成员进行打包。

第 128 行的回调函数 `eventFontSet()` 在字体选择器选择新字体时由字体选择器调用。如果 context 中已经包含字体，则第 132 行调用 `gdk_font_unref()` 释放该字体的分配，无论是在本地还是在 X 服务器中（除非其他进程正在使用相同的字体）。第 133 行调用 `gdk_font_load()` 基于字体选择器返回的字符串创建新字体。第 134 行调用 `gdk_window_clear_area_e()` 是为了更新显示所必需的。该调用执行两项操作——通过用背景色填充绘图区域来擦除之前绘制的字符串，并发出一个 expose 事件。expose 事件导致回调函数 `eventDraw()` 使用新字体绘制文本。

第 137 行的回调函数 `eventDraw()` 在需要将字符串绘制到绘图区域时调用。第 148 行测试是否已加载字体，如果没有，则加载默认字体。字符串的内容由其窗口中的位置决定，因此第 153 行和第 164 行的 `switch` 语句用于由两个描述其位置的名称构建该字符串。由于字体和字符串都是已知的，第 176 行调用 `gdk_text_extents()` 返回字符串在显示上将呈现的度量值。这些值可用于定位窗口中的文本。

垂直定位由始于第 185 行的 `switch` 语句设置。如果字符串应位于窗口顶部，则 `y` 值被设置为上升高度（ascent）——即最高字符在基线上的高度。如果字符串应放置在窗口底部，则 `y` 值被设置为窗口高度减去下降高度（descent）——这将使具有最长下延部分的字符底部直接置于窗口底部。计算过程还涉及一点

