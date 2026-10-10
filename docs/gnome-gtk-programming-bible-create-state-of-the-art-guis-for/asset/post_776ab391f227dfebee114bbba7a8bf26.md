
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

The mainline of the program, on lines 37 through 58, sets up a GNOME application that has just one window. The call to `createPositionWidget()` on line 52 creates a widget that is inserted in the main window on line 54 with a call to `gnome_app_set_contents()`.

The application window is shown in Figure 13-6. The row of buttons across the top repositions the string vertically, and the row of buttons toward the bottom repositions it horizontally. The button at the bottom is a font selector that you can use to change the font of the string being positioned.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_438_0.png)

The function `createPositionWidget()` on line 59 creates all the widgets for the display and assigns callback functions to them. A `Context` struct, defined on line 14, is used to pass information to this function, and to all the callback functions, instead of using global data. All of the widgets are contained in the vertical box created by the call to `gtk_vbox_new()` on line 67. Lines 69 through 86 create a horizontal box and fill it with buttons. Then the horizontal box is inserted at the top of the vertical box. Each button is assigned its own callback function with the context pointer as the data passed to it.

Lines 88 through 93 create the drawing area that is used to display the text. The call to `gtk_drawing_area_size()` sets the size of the drawing area to the `WIDTH` and `HEIGHT` values defined on lines 4 and 5. The callback function `eventDraw()` is connected to the drawing area, so whenever there is an exposure event, the function is called to paint the window.

Lines 95 through 118 create the buttons toward the bottom that control the horizontal position of the displayed text. Each button is assigned its own callback function.

A `GnomeFontPicker` widget is created by the call to `gnome_font_picker_new()` on lines 120 through 124. Its callback function is `eventFontSet()`, and it is packed as the last member of the vertical box.

The callback function `eventFontSet()` on line 128 is called by the font picker whenever a new font is selected. If there is a font already included in the context, the call to `gdk_font_unref()` on line 132 releases the font allocation both locally and in the X server (unless the same font is in use by some other process). The call to `gdk_font_load()` on line 133 creates a new font based on the string returned from the font picker. The call to `gdk_window_clear_area_e()` on line 134 is necessary for the display to be updated. The call does two things—it erases the previously drawn string by filling the drawing area with the background color, and it issues an expose event. The expose event causes the callback function `eventDraw()` to draw the text using the new font.

The callback function `eventDraw()` on line 137 is called whenever the string needs to be drawn into the drawing area. Line 148 tests whether a font is loaded already and, if not, loads the default font. The text of the string is determined by its location in the window, so the `switch` statements on lines 153 and 164 are used to build the string from the two names describing its position. Because both the font and the string are known, a call to `gdk_text_extents()` on line 176 returns the metrics of the string as it will appear on the display. These values can be used to position the text in the window.

The vertical positioning is set in the `switch` statement beginning on line 185. If the string is to be at the top of the window, the `y` value is set to the ascent—that is, the height of the tallest character above the base line. If the string is to be placed at the bottom of the window, the `y` value is set to the height of the window minus the descent—this puts the bottom of the character with the longest descender directly on the bottom of the window. There is a little bit more involved to calculate
