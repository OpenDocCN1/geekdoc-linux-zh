
# GNOME 2 官方开发者指南

- `history-id` (`gchararray`): 选择器的历史记录标识符。
- `browse-dialog-title` (`gchar`): 图标选择对话框标题。
- `pick-dialog` (`GtkDialog *`, read-only): 对话框控件（用于更改其属性）。

当用户选择图标时，GNOME 会发出一个 `changed` 信号。处理函数的原型如下：

```c
void handler(GnomeIconEntry *entry, gpointer data);
```

### 4.3.9 图像选择器

为了允许用户选择任意图像而不是图标，你可以在应用程序中放入一个 `GnomePixmapEntry` (`GNOME_PIXMAP_ENTRY`) 控件。这个 `GnomeFileEntry` 的子类会将选定的图像显示为一个文件名。

要创建一个 `GnomePixmapEntry` 控件，请使用此函数：

```c
*image_entry;
```
