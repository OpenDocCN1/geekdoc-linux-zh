```
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

The if statement on line 234 checks whether the cursor is inside the window (using the Boolean value set on lines 188 and 19) to select the color for the background. Then, the window is filled with the background color by the call to gdk_window_clear() on line 241.

The size and position of each bar is calculated in the loop beginning on line 246. If this is the first time a particular bar is displayed, a graphics context is constructed for it by a call to ag_bargraph_add_gc(). The graphics context is constructed at the last minute to make it simpler to add a new bar to the widget at any time. Once the size and position of the bar is determined, it is drawn onto the window by a call to gdk_draw_rectangle() on line 255. At the bottom of the loop, lines 259 through 261, the two x values marking the edges of the bar are saved as part of the bar information, and the bar_x value is incremented to the start position of the next bar. Finally, on line 263, a call is made to ag_bargraph_paint_text() so the selected bar’s text can be displayed.

If the show_text pointer for the widget is not NULL, it contains the address of a string of characters that are to be displayed. Whether or not the pointer is NULL is determined by the event processing on lines 193 through 199. Only text is present while a mouse button is held down.

```
265 static void ag_bargraph_paint_text (GtkWidget *widget)
266 {
267 AgBargraph *bargraph = AG_BARGRAPH (widget);
268 gint ibearing;
269 gint rbearing;
270 gint width;
271 gint ascent;
```