# GtkFontSelection

The `GtkFontSelection` widget can be used by your application to enable the user to select a font.

Using this widget, it is up to your application to determine when a selection is made and call the `gtk_font_selection_get_font()` function. The `GtkFontSelectionDialog` widget uses this widget and adds selection buttons and callbacks.

**Inheritance**

```
GtkFontSelection->GtkNotebook->GtkContainer->GtkWidget->GtkObject
```

**Functions**

```
GdkFont *gtk_font_selection_get_font(
GtkFontSelection *fontsel)
gchar *gtk_font_selection_get_font_name(
GtkFontSelection *fontsel)
gchar *gtk_font_selection_get_preview_text(
GtkFontSelection *fontsel)
GtkType gtk_font_selection_get_type()
GtkWidget *gtk_font_selection_new()
void gtk_font_selection_set_filter(GtkFontSelection *fontsel,
GtkFontFilterType filter_type, GtkFontType font_type,
gchar **foundries, gchar **weights, gchar **slants,
gchar **setwidths, gchar **spacings, gchar **charsets)
gboolean gtk_font_selection_set_font_name(
GtkFontSelection *fontsel, const gchar *fontname)
void gtk_font_selection_set_preview_text(
GtkFontSelection *fontsel, const gchar *text)
```

**Enums**

```
typedef enum {
GTK_FONT_FILTER_BASE,
GTK_FONT_FILTER_USER
} GtkFontFilterType;

typedef enum {
GTK_FONT_BITMAP,
GTK_FONT_SCALABLE,
GTK_FONT_SCALABLE_BITMAP,
GTK_FONT_ALL
} GtkFontFilterType;
```

The `GtkFontSelection` widget shown in Figure 21-19 following the example code is the default configuration (there is no filtering) that shows a selected font, along with its weight and size. The selected font is displayed in the window across the