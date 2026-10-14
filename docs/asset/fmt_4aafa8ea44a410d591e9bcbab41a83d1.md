
# GNOME 2 官方开发者指南

```c
void colorpicker_changed(GnomeColorPicker *picker,
    guint red, guint green, guint blue, guint alpha,
    gpointer data)
{
    g_print("颜色选择器发生变化；新颜色: R=%d; G=%d; B=%d; A=%d\n", red, green, blue, alpha);
}

/* GnomeIconEntry::changed 的处理器 */
void iconpicker_changed(GnomeIconEntry *picker, gpointer data)
{
    gchar *path;
    g_object_get(picker, "filename", &path, NULL);
    g_print("*图标选择器发生变化；新图标: %s\n", path);
    g_free(path);
}

/* GnomePixmapEntry::activate 的处理器 */
void pixmap_changed(GnomePixmapEntry *picker, gpointer data)
{
    gchar *path;
    g_print("*像素图发生变化；%s",
```

```c
/* 标准处理器 */
int delete_event(GtkWidget *widget, GdkEvent event, gpointer event)
{
    return FALSE;
}

void program(GtkWidget *widget, gpointer event)
{
    gtk_main_quit();
}

int main(int argc, char **argv)
{
  GnomeProgram *program;
  GtkWindow *window;
  GtkTable *table;
  GtkWidget *widgets[NUM_WIDGETS];
  int i;

  gnome_init(&argc, &argv, NULL);
  program = gnome_program_new("GNOME 选择器 Demo", NULL);
  window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
  gtk_window_set_title(GTK_WINDOW(window), "GNOME 选择器");
  gtk_window_set_default_size(GTK_WINDOW(window), 400, 300);
  gtk_container_add(GTK_CONTAINER(program), window);
  table = gtk_table_new(9, 2);
  gtk_container_add(GTK_CONTAINER(window), table);
  for (i = 0; i < NUM_WIDGETS; i++) {
    GtkWidget *label = gtk_label_new(widget_label[i]);
    gtk_table_attach(GTK_TABLE(table), label, 0, i, 1, 1);
  }
  widgets[0] = gnome_entry_new();
  g_signal_connect(widgets[0], "activate", G_CALLBACK(text_activate), NULL);
  gtk_table_attach(GTK_TABLE(table), widgets[0], 1, 0, 1, 1);
  widgets[1] = gnome_file_entry_new();
  g_signal_connect(widgets[1], "activate", G_CALLBACK(file_activate), NULL);
  gtk_table_attach(GTK_TABLE(table), widgets[1], 1, 1, 1, 1);
  widgets[2] = gnome_font_picker_new_with_accelgroup(NULL, NULL);
  g_object_set(widgets[2], "icon-name", "font-font-general", NULL);
  gtk_table_attach(GTK_TABLE(table), widgets[2], 2, 2, 1, 1);
  widgets[3] = gnome_font_picker_new_with_accelgroup(NULL, NULL);
  g_object_set(widgets[3], "show_font", TRUE, NULL);
  gtk_table_attach(GTK_TABLE(table), widgets[3], 1, 3, 1, 1);
  widgets[4] = gnome_font_picker_new_with_accelgroup(NULL, NULL);
  g_object_set(widgets[4], "label", "自定义字体", NULL);
  gtk_table_attach(GTK_TABLE(table), widgets[4], 1, 4, 1, 1);
  widgets[5] = gnome_color_picker_new();
  g_signal_connect(widgets[5], "color-set", G_CALLBACK(colorpicker_changed), NULL);
  gtk_table_attach(GTK_TABLE(table), widgets[5], 1, 5, 1, 1);
  widgets[6] = gnome_icon_entry_new();
  g_signal_connect(widgets[6], "changed", G_CALLBACK(iconpicker_changed), NULL);
  gtk_table_attach(GTK_TABLE(table), widgets[6], 1, 6, 1, 1);
  widgets[7] = gnome_pixmap_entry_new();
  g_signal_connect(widgets[7], "activate", G_CALLBACK(pixmap_changed), NULL);
  gtk_table_attach(GTK_TABLE(table), widgets[7], 1, 7, 1, 1);
  widgets[8] = gnome_date_entry_new();
  gtk_table_attach(GTK_TABLE(table), widgets[8], 1, 8, 1, 1);
  g_signal_connect(window, "destroy", G_CALLBACK(program), NULL);
  gtk_widget_show_all(window);
  gtk_main();
  return 0;
}
```

```c
"n-columns", 2,
"column-spacing", 6,
"row-spacing", 6,
NULL);
```

```c
/* 在每一行中将控件及其标签封装在一起 */
for (i = 0; i < NUM_WIDGETS; i++)
{
    gtk_table_attach(table, g_object_new(GTK_TYPE_LABEL,
        "label", widget_label[i],
        "use-underline", TRUE,
        "mnemonic-widget", widgets[i],
        "xalign", 1.0,
        "justify", GTK_JUSTIFY_RIGHT,
        NULL),
        0, 1, i+1, GTK_EXPAND|GTK_FILL, 0, 0, 0);
    gtk_table_attach(table, g_object_new(GTK_ALIGNMENT,
        "xalign", 0.0,
        "child", widgets[i],
        NULL),
        1, 2, i+1, GTK_EXPAND|GTK_FILL, 0, 0, 0));
```

```c
/* 封装、显示所有控件并启动 GTK+ 主事件循环 */
gtk_container_add(GTK_CONTAINER(window), GTK_WIDGET(table));
gtk_widget_show_all(GTK_WIDGET(window));
```
