

# GnomeFileEntry

GnomeFileEntry 小部件（在第 21 章中有描述）允许用户选择一个文件。

```c
static GtkWidget *makeWidget()
{
  GtkWidget *fileentry;

  fileentry = gnome_file_entry_new("fseekid","File Seeking");
  return(fileentry);
}
```

**字符串** `"fseekid"` **是用于保存之前选定的文件名列表的 ID。** 第二个字符串用于 `GtkFileSelection` 窗口的标题栏。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_695_0.png)

图 22-11：一个 GnomeFileEntry 小部件，带有四个记忆的文件名

## GnomeFontPicker

GnomeFontPicker 小部件是一个按钮，当被选中时，会弹出一个窗口，允许用户从众多可用字体中进行选择。

### 继承

`GnomeFontPicker->GtkButton->GtkBin->GtkContainer->GtkWidget->GtkObject`

### 函数

```c
GtkWidget *gnome_font_picker_create_inside(
   GnomeFontPicker *gfp)
void gnome_font_picker_dialog_destroy(GtkWidget *widget,
   gpointer data)
void gnome_font_picker_fi_set_show_size(GnomeFontPicker *gfp,
   gboolean show_size)
void gnome_font_picker_fi_set_use_font_in_label(
   GnomeFontPicker *gfp, gboolean use_font_in_label,
   gint size)
void gnome_font_picker_font_extract_attr(gchar *font_name,
   gchar *attr, gint i)
void gnome_font_picker_font_set_attr(gchar **font_name,
   const gchar *attr, gint i)
GdkFont *gnome_font_picker_get_font(GnomeFontPicker *gfp)
gchar *gnome_font_picker_get_font_name(GnomeFontPicker *gfp)
GnomeFontPickerMode gnome_font_picker_get_mode(
  GnomeFontPicker *gfp)
gchar *gnome_font_picker_get_preview_text(
  GnomeFontPicker *gfp)
GtkType gnome_font_picker_get_type(void)
void gnome_font_picker_label_use_font_in_label(
  GnomeFontPicker *gfp)
GtkWidget *gnome_font_picker_new(void)
gboolean gnome_font_picker_set_font_name(
  GnomeFontPicker *gfp, const gchar *fontname)
void gnome_font_picker_set_mode(GnomeFontPicker *gfp,
  GnomeFontPickerMode mode)
void gnome_font_picker_set_preview_text(GnomeFontPicker *gfp,
  const gchar *text)
void gnome_font_picker_set_title(GnomeFontPicker *gfp,
  const gchar *title)
void gnome_font_picker_update_font_info(GnomeFontPicker *gfp)
void gnome_font_picker_ww_set_widget(GnomeFontPicker *gfp,
  GtkWidget *widget)
```

### 枚举

```c
typedef enum {
  GNOME_FONT_PICKER_MODE_PIXMAP,
  GNOME_FONT_PICKER_MODE_FONT_INFO,
  GNOME_FONT_PICKER_MODE_USER_WIDGET,
  GNOME_FONT_PICKER_MODE_UNKNOWN
} GnomeFontPickerMode;
```

第 13 章提供了 GnomeFontPicker 的示例。

## GnomeFontSelector

GnomeFontSelector 小部件是一个对话框，它管理弹出、接受输入以及返回所选字体名称的所有细节。

### 继承

`GnomeFontSelector->GtkDialog->GtkWindow->GtkBin->GtkContainer->GtkWidget->GObject`

### 函数

```c
gchar *gnome_font_select(void)
gchar *gnome_font_select_with_default(
  const gchar *default_font)
gchar *gnome_font_selector_get_selected(
  GnomeFontSelector *text_tool)
GtkType gnome_font_selector_get_type(void)
GtkWidget *gnome_font_selector_new(void)
```

此示例展示了你的应用程序如何只需调用一次函数即可返回所选字体。你可以从程序中的任何地方调用 `gnome_font_select()` 或 `gnome_font_select_with_default()`，然后图 22-12 中所示的对话框将出现。函数调用包含自己的事件循环，因此只有当用户选择了一种字体或关闭对话框时，它才会返回。

```c
/** gnomefontpicker.c **/
#include <gnome.h>

int main(int argc, char *argv[])
{
    gchar *font;

    gnome_init("gnomefontpicker","1.0",argc,argv);

    font = gnome_font_select();
    if(font == NULL)
        g_print("No font selected\n");
    else
        g_print("Selected: %s\n",font);

    exit(0);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_697_0.png)

图 22-12：一个 GnomeFontSelector 对话框

## GnomeGuru

这是一个未完成的小部件。完成时，它将是一个构建向导（wizard）的工具（向导是一系列根据你采取哪个分支而变化的步骤）。

### 继承

`GnomeGuru->GtkVBox->GtkBox->GtkContainer->GtkWidget->GtkObject`

### 函数

```c
void gnome_guru_append_page(GnomeGuru *guru, const gchar *name, GtkWidget *graphic, GnomeDialog *dialog)
void gnome_guru_back_set_sensitive(GnomeGuru *guru, gboolean sensitivity)
void gnome_guru_construct(GnomeGuru *guru, const gchar *name, GtkWidget *graphic, GnomeDialog *dialog)
GtkWidget *gnome_guru_current_page(GnomeGuru *guru)
GtkType gnome_guru_get_type()
GtkWidget *gnome_guru_new(const gchar *name, GtkWidget *graphic, GnomeDialog *dialog)
void gnome_guru_next_set_sensitive(GnomeGuru *guru, gboolean sensitivity)
```

## GnomeHRef

GnomeHRef 小部件显示一个无边框按钮，当被选中时，它会发出命令让 Web 浏览器连接到某个 Web 站点。实际上，发给浏览器的命令全局定义为 GNOME 控制中心中 URL Handler 列表的默认成员。

### 继承

`GnomeHRef->GtkButton->GtkBin->GtkContainer->GtkWidget->GtkObject`

### 函数

```c
gchar *gnome_href_get_label(GnomeHRef *self)
GtkType gnome_href_get_type(void)
gchar *gnome_href_get_url(GnomeHRef *self)
GtkWidget *gnome_href_new(const gchar *url, const gchar *label)
void gnome_href_set_label(GnomeHRef *self, const gchar *label)
void gnome_href_set_url(GnomeHRef *self, const gchar *url)
```

此示例创建了一个标签为 *Gnome’s start page* 的小部件，并为其附加了一个 URL。该小部件显示为普通文本，如图 22-13 所示，它是蓝色且带下划线的。这样，你可以将它包含在其他小部件之间的文本正文中，它应该被识别为一个链接。此外，当鼠标经过它时，周围会出现一个边框。

```c
static GtkWidget *makeWidget()
{
    GtkWidget *href;

    href = gnome_href_new("http://www.gnome.org/start",
        "Gnome's start page");

    return(href);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_699_0.png)

图 22-13：GnomeHRef 小部件是一个指向 Web 站点的链接

## GnomeIconEntry

GnomeIconEntry 是一个按钮，点击后会弹出一个窗口，显示一组图标。用户可以选中 /usr/share/pixmaps 中找到的其中一个图标，或者浏览文件系统以在其他目录中找到图标。目录名的下拉列表维护了之前打开的目录的历史记录。

### 继承

`GnomeIconEntry->GtkVBox->GtkBox->GtkContainer->GtkWidget->GtkObject`

### 函数

```c
char *gnome_icon_entry_get_filename(GnomeIconEntry *ientry)
GtkType gnome_icon_entry_get_type(void)
GtkWidget *gnome_icon_entry_gnome_entry(GnomeIconEntry *ientry)
GtkWidget *gnome_icon_entry_gnome_file_entry(GnomeIconEntry *ientry)
GtkWidget *gnome_icon_entry_gtk_entry(GnomeIconEntry *ientry)
GtkWidget *gnome_icon_entry_new(char *history_id,
            char *browse_dialog_title)
void gnome_icon_entry_set_icon(GnomeIconEntry *ientry,
            const char *filename)
void gnome_icon_entry_set_pixmap_subdir(GnomeIconEntry *ientry, const char *subdir)
```

以下示例创建了一个按钮，点击后显示图 22-14 中所示的对话框。如果用户选择了某个图标，按钮将改变以显示该图标——如图 22-15 所示。

```c
static GtkWidget *makeWidget()
{
    GtkWidget *iconentry;
    GtkWidget *entry;

    iconentry = gnome_icon_entry_new("historyID",
                "Select an Icon");
    entry = gnome_icon_entry_gtk_entry(
                GNOME_ICON_ENTRY(iconentry));
    gtk_signal_connect(GTK_OBJECT(entry),"changed",
                GTK_SIGNAL_FUNC(eventIconChanged),iconentry);
    return(iconentry);
}

void eventIconChanged(GtkWidget *widget,
    GnomeIconEntry *iconentry)
{
    GtkWidget *dialog;

    dialog = GNOME_ICON_ENTRY(iconentry)->pick_dialog;
    if(dialog != NULL) {
        gtk_signal_handlers_destroy(GTK_OBJECT(dialog));
        gtk_signal_connect(GTK_OBJECT(dialog),"clicked",
            eventIconSelected,iconentry);
    }
}

void eventIconSelected(GtkWidget *widget, gint button,
    GnomeIconEntry *iconentry)
{
    gchar *iconfile;

    switch(button) {
    case 0:
        iconfile = gnome_icon_entry_get_filename(iconentry);
        g_print("Icon file name: %s\n",iconfile);
        break;
    case 1:
        g_print("No icon selection was made\n");
    }
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_700_0.png)

图 22-14：GnomeIconEntry 小部件的图标选择对话框

