
`GnomeFontPicker` *gfp*, `gboolean` `use_font_in_label`,

`gint` `size`)

`void` `gnome_font_picker_font_extract_attr`(`gchar` *`font_name`*, `gchar` *`attr`*, `gint` `i`)

`void` `gnome_font_picker_font_set_attr`(`gchar` ** `font_name`*, `const gchar` *`attr`*, `gint` `i`)

`GdkFont` * `gnome_font_picker_get_font`(`GnomeFontPicker` *`gfp`)

`gchar` * `gnome_font_picker_get_font_name`(`GnomeFontPicker` *`gfp`)

`GnomeFontPickerMode` `gnome_font_picker_get_mode`(`GnomeFontPicker` *`gfp`)

`gchar` * `gnome_font_picker_get_preview_text`(`GnomeFontPicker` *`gfp`)

`GtkType` `gnome_font_picker_get_type`(void)

`void` `gnome_font_picker_label_use_font_in_label`(`GnomeFontPicker` *`gfp`)

`GtkWidget` * `gnome_font_picker_new`(void)

`gboolean` `gnome_font_picker_set_font_name`(`GnomeFontPicker` *`gfp`, `const gchar` *`fontname`)

`void` `gnome_font_picker_set_mode`(`GnomeFontPicker` *`gfp`, `GnomeFontPickerMode` `mode`)

`void` `gnome_font_picker_set_preview_text`(`GnomeFontPicker` *`gfp`, `const gchar` *`text`)

`void` `gnome_font_picker_set_title`(`GnomeFontPicker` *`gfp`, `const gchar` *`title`)

`void` `gnome_font_picker_update_font_info`(`GnomeFontPicker` *`gfp`)

`void` `gnome_font_picker_ww_set_widget`(`GnomeFontPicker` *`gfp`, `GtkWidget` *`widget`)

### 枚举

```c
typedef enum {
  GNOME_FONT_PICKER_MODE_PIXMAP,
  GNOME_FONT_PICKER_MODE_FONT_INFO,
  GNOME_FONT_PICKER_MODE_USER_WIDGET,
  GNOME_FONT_PICKER_MODE_UNKNOWN
} GnomeFontPickerMode;
```

第 13 章提供了 `GnomeFontPicker` 的示例。

## GnomeFontSelector

`GnomeFontSelector` 小部件是一个对话框，它管理弹出、接受输入以及返回所选字体名称的所有细节。

### 继承

`GnomeFontSelector->GtkDialog->GtkWindow->GtkBin->GtkContainer->GtkWidget->GObject`

### 函数

```c
gchar *gnome_font_select(void)
gchar *gnome_font_select_with_default(const gchar *default_font)
gchar *gnome_font_selector_get_selected(GnomeFontSelector *text_tool)
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

图 22-12：一个 `GnomeFontSelector` 对话框

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

`GnomeHRef` 小部件显示一个无边框按钮，当被选中时，它会发出命令让 Web 浏览器连接到某个 Web 站点。实际上，发给浏览器的命令全局定义为 GNOME 控制中心中 URL Handler 列表的默认成员。

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
    href = gnome_href_new("http://www.gnome.org/start", "Gnome's start page");
    return(href);
}
```
