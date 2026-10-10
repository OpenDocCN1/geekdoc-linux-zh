# **Table 11-4 (*continued*)**

| Function Call | GdkGCValues Field | GdkGCValues Mask |
| :--- | :--- | :--- |
| `gdk_gc_set_dashes`(`GdkGC *gc`, `gint dash_offset`, `gchar dash_list[ ]`, `gint list_length`) | | |
| `gdk_gc_set_exposures`(`GdkGC *gc`, `gint exposures`) | `Graphics_exposures` | `GDK_GC_EXPOSURES` |
| `gdk_gc_set_fill`(`GdkGC *gc`, `GdkFill fill`) | `Fill` | `GDK_GC_FILL` |
| `gdk_gc_set_font`(`GdkGC *gc`, `GdkFont *font`) | `Font` | `GDK_GC_FONT` |
| `gdk_gc_set_foreground`(`GdkGC *gc`, `GdkColor *color`) | `Foreground` | `GDK_GC_FOREGROUND` |
| `gdk_gc_set_function`(`GdkGC *gc`, `GdkFunction function`) | `Function` | `GDK_GC_FUNCTION` |
| `gdk_gc_set_line_attributes`(`GdkGC *gc`, `gint line_width`, `GdkLineStyle line_style`, `GdkCapStyle cap_style`, `GdkJoinStyle join_style`) | `Line_width`<br>`Line_style`<br>`Cap_style`<br>`Join_style` | `GDK_GC_LINE_WIDTH`<br>`GDK_GC_LINE_STYLE`<br>`GDK_GC_CAP_STYLE`<br>`GDK_GC_JOIN_STYLE` |
| `gdk_gc_set_stipple`(`GdkGC *gc`, `GdkPixmap *stipple`) | `Stipple` | `GDK_GC_STIPPLE` |
| `gdk_gc_set_subwindow`(`GdkGC *gc`, `GdkSubwindowMode mode`) | `Subwindow_mode` | `GDK_GC_SUBWINDOW` |
| `gdk_gc_set_title`(`GdkGC *gc`, `GdkPixmap *tile`) | `Tile` | `GDK_GC_TILE` |
| `gdk_gc_set_ts_origin`(`GdkGC *gc`, `gint x`, `gint y`) | `tx_x_origin`<br>`ts_y_origin` | `GDK_GC_TS_X_ORIGIN`<br>`GDK_GC_TS_Y_ORIGIN` |