```
gnome_font_picker_get_font (GnomeFontPicker *gfp)
```

```
gtk_font_selection_dialog_get_font
( GtkFontSelectionDialog *fse)
```

```
gtk_font_selection_get_font (GtkFontSelection *fonsel)
```

# GdkGC \*

```
gdk_gc_new (GdkWindow *window)
```

```
gdk_gc_new_with_values (GdkWindow *window, GdkGCValues *values,
GdkGCValuesMask values_mask)
```

```
gdk_gc_ref (GdkGC *gc)
```

```
gtk_gc_get (gint depth, GdkColormap *colormap,
GdkGCValues *values, GdkGCValuesMask values_mask)
```

# GdkIC \*

```
gdk_ic_new (GdkICAttr *attr, GdkICAttributesType mask)
```

# GdkICAttr \*

```
gdk_ic_attr_new (void)
```

# GdkICAttributesType

```
gdk_ic_get_attr (GdkIC *ic, GdkICAttr *attr,
GdkICAttributesType mask)
```

```
gdk_ic_set_attr (GdkIC *ic, GdkICAttr *attr,
GdkICAttributesType mask)
```

# GdkImage \*

```
gdk_image_get (GdkWindow *window, gint x, gint y, gint width,
gint height)
```

```
gdk_image_new (GdkImageType type, GdkVisual *visual, gint width,
```