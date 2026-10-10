
```
244      bar_width = (float)widget->allocation.width /

245 (float)bargraph->bar_count;

246 for (i=0; i<bargraph->bar_count; i++) {

247 if (bargraph->bars[i].gc == NULL)

248 ag_bargraph_add_gc (widget,&bargraph->bars[i]);

249 bar_percent = (float)bargraph->bars[i].value /

250 (float)bargraph->maximum_value;

251 bar_height = bar_percent

252 * (float)widget->allocation.height;

253 bar_y = (float)widget->allocation.height

254 * (1.0 - bar_percent);

255 gdk_draw_rectangle (widget->window,

256 &bars[i].gc,(gint)bar_x,

257 (gint)bar_width + 1,(gint)bar_height + 1);

258 (gint)bar_width + 1,(gint)bar_height + 1);

259 bargraph->bars[i].x_left = (gint)bar_x;

260 bar_x += bar_width;

261 bargraph->bars[i].x_right = (gint)bar_x;

262 }

263 ag_bargraph_paint_text (widget);

264
```

第 234 行的 if 语句通过检查光标是否在窗口内部（使用在第 188 行和第 191 行设置的布尔值）来选择背景颜色。然后，第 241 行对 `gdk_window_clear()` 的调用会用背景颜色填充窗口。

每个条形的大小和位置是在从第 246 行开始的循环中计算的。如果是第一次显示某个特定的条形，则通过调用 `ag_bargraph_add_gc()` 为其构建一个图形上下文。图形上下文在最后一刻构建，以便随时向组件添加新条形更加简单。一旦确定了条形的大小和位置，就会在第 255 行调用 `gdk_draw_rectangle()` 将其绘制到窗口上。在循环底部，第 259 行至第 261 行，标记条形边缘的两个 x 值被保存为条形信息的一部分，并且 `bar_x` 值递增到下一个条形的起始位置。最后，在第 263 行，调用 `ag_bargraph_paint_text()`，以便可以显示所选条形的文本。

如果组件的 `show_text` 指针不为 NULL，则它包含要显示的字符字符串的地址。指针是否为 NULL 由第 193 行至第 199 行的事件处理决定。只有当按住鼠标按钮时，才会存在文本。

```c
265 static void ag_bargraph_paint_text (GtkWidget *widget)
266 {
267 AgBargraph *bargraph = AG_BARGRAPH (widget);
268 gint ibearing;
269 gint rbearing;
270 gint width;
271 gint ascent;
272     int descent;
273     int x;
274     int y;

276     if(bargraph->show_text == NULL)
277         return;

279     if(bargraph->text_font == NULL) {
280         bargraph->text_font = gdk_font_load(
281             "-*-bookman-light-r normal-18-*-*-*-*-p*-iso8859-1");
282     }
283     gdk_text_extents(bargraph->text_font,
284             bargraph->show_text,
285             strlen(bargraph->show_text),
286             &ibearing,
287             &rbearing,
288             &width,
289             &ascent,
290             &descent);
291     y = ascent;
292     x = (widget->allocation.width / 2) - (width / 2);

294     gdk_draw_string(widget->window,
295             bargraph->text_font,
296             widget->style->black_gc,
297             x, y,
298             bargraph->show_text);
299 }
```

如果是第一次显示文本，则字体由第 279 行至第 282 行对 `gdk_font_load()` 的调用定义。然后，在第 283 行进行对 `gdk_text_extents()` 的调用。从该调用中设置的 x 和 y 值（在第 291 行和第 292 行）用于将文本定位在窗口的顶部中央。字符串由第 294 行对 `gdk_draw_string()` 的调用绘制。

每个条形都有不同的颜色，颜色由第 300 行的函数 `ag_bargraph_add_gc()` 设置。在这个示例中，分配给每个条形的颜色是随机选择的。（实际上，它是伪随机的，因为每次运行程序时，颜色序列都是相同的。）

```c
300 static void ag_bargraph_add_gc(GtkWidget *widget,
        AgBargraphBar *bar)
301 {
302     GdkColor color;
303     GdkColormap *colormap;

305     bar->gc = gdk_gc_new(widget->window);
306     color.red += (((double)rand()*0xFFFF)/RAND_MAX);
307     color.green += (((double)rand()*0xFFFF)/RAND_MAX);
308     color.blue += (((double)rand()*0xFFFF)/RAND_MAX);

310     colormap = gtk_widget_get_colormap(widget);
311     gdk_color_alloc(colormap,&color);
312     gdk_gc_set_foreground(bar->gc,&color);
313 }
```

第 316 行的函数 `ag_bargraph_size_request()` 和第 325 行的 `ag_bargraph_size_allocate()` 协同工作以确定组件的大小和位置。这两个函数在第 67 行和第 68 行被设置为尺寸回调，并由任何负责容纳 AgBargraph 组件的容器组件调用。

```c
316 static void ag_bargraph_size_request(GtkWidget *widget,
                       GtkRequisition *requisition)
317 {
318   g_return_if_fail(widget != NULL);
319   g_return_if_fail(AG_IS_BARGRAPH(widget));

321   requisition->width = 200;
322   requisition->height = 100;
323 }
324 static void ag_bargraph_size_allocate(GtkWidget *widget,
                       GtkAllocation *allocation)
325 {
326   g_return_if_fail(widget != NULL);
327   g_return_if_fail(AG_IS_BARGRAPH(widget));
328   g_return_if_fail(allocation != NULL);

330   widget->allocation.x = allocation->x;
```
