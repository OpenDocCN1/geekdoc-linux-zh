
`void gtk_button_box_get_child_size(GtkButtonBox *widget, gint *width, gint *height)`

`void gtk_button_box_get_child_size_default(gint *width, gint *height)`

`GtkButtonBoxStyle gtk_button_box_get_layout(GtkButtonBox *widget)`

`gint gtk_button_box_get_spacing(GtkButtonBox *widget)`

`GtkType gtk_button_box_get_type(void)`

`void gtk_button_box_set_child_padding(GtkButtonBox *widget, gint ipad_x, gint ipad_y)`

`void gtk_button_box_set_child_padding_default(gint ipad_x, gint ipad_y)`

`void gtk_button_box_set_child_size(GtkButtonBox *widget, gint width, gint height)`

`void gtk_button_box_set_child_size_default(gint width, gint height)`

`void gtk_button_box_set_layout(GtkButtonBox *widget, GtkButtonBoxStyle layout_style)`

`void gtk_button_box_set_spacing(GtkButtonBox *widget, gint spacing)`

### 枚举

```c

typedef enum {

    GTK_BUTTONBOX_DEFAULT_STYLE,

    GTK_BUTTONBOX_SPREAD,

    GTK_BUTTONBOX_EDGE,

    GTK_BUTTONBOX_START,

    GTK_BUTTONBOX_END

} GtkButtonBoxStyle;

```

## `GtkCalendar`

`GtkCalendar` 组件显示一个月。用户可以选择月份和年份，然后选择该月的具体日期。

### 继承

`GtkCalendar` -> `GtkWidget` -> `GtkObject`

### 函数

```c

void gtk_calendar_clear_marks(GtkCalendar *calendar)

void gtk_calendar_display_options(GtkCalendar *calendar, GtkCalendarDisplayOptions flags)

```

## GtkCalendar

```c

void gtk_calendar_freeze(GtkCalendar *calendar)

void gtk_calendar_get_date(GtkCalendar *calendar, guint *year,

guint *month, guint *day)

GtkType gtk_calendar_get_type(void)

gint gtk_calendar_mark_day(GtkCalendar *calendar, guint day)

GtkWidget *gtk_calendar_new(void)

void gtk_calendar_select_day(GtkCalendar *calendar, guint day)

gint gtk_calendar_select_month(GtkCalendar *calendar,

guint month, guint year)

void gtk_calendar_thaw(GtkCalendar *calendar)

gint gtk_calendar_unmark_day(GtkCalendar *calendar, guint day)

```

### 枚举

```c

typedef enum {

GTK_CALENDAR_SHOW_HEADING,

GTK_CALENDAR_SHOW_DAY_NAMES,

GTK_CALENDAR_NO_MONTH_CHANGE,

GTK_CALENDAR_SHOW_WEEK_NUMBERS,

GTK_CALENDAR_WEEK_START_MONDAY

} GtkCalendarDisplayOptions;

```

每当创建一个新的日历小部件时，它默认显示当前的日期和时间，其显示效果如图 21-5 所示。

```c

static GtkWidget *makeWidget()

{

GtkWidget *widget;

widget = gtk_calendar_new();

return(widget);

}

```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_569_0.png)

图 21-5: 显示的 GtkCalendar 小部件

## GtkCheckButton

GtkCheckButton 小部件显示一个带有标签的小按钮。可以通过鼠标切换该按钮的开/关状态，并且它会保持该状态，直到再次被切换。

### 继承

GtkCheckButton -> GtkToggleButton -> GtkButton -> GtkBin -> GtkContainer -> GtkWidget -> GtkObject

### 函数

```c

GtkType gtk_check_button_get_type(void)

GtkWidget *gtk_check_button_new(void)

GtkWidget *gtk_check_button_new_with_label(

const gchar *label)

```

以下示例显示了图 21-6 中展示的窗口。

```c

static GtkWidget *makeWidget()

{

GtkWidget *widget;

widget = gtk_check_button_new_with_label(

"Check Button Label");

return(widget);

}

```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_570_0.png)

## GtkCheckMenuItem

此小部件显示一个切换按钮和一个标签。由于它继承自 GtkMenuItem，因此旨在用作菜单中的切换按钮。

### 继承

GtkCheckMenuItem -> GtkMenuItem -> GtkItem -> GtkBin -> GtkContainer -> GtkWidget -> GtkObject

### 函数

```c

GtkType gtk_check_menu_item_get_type(void)

GtkWidget *gtk_check_menu_item_new(void)

GtkWidget *gtk_check_menu_item_new_with_label(

const gchar *label)

void gtk_check_menu_item_set_active(

GtkCheckMenuItem *check_menu_item, Gboolean is_active)

void gtk_check_menu_item_set_show_toggle(

GtkCheckMenuItem *menu_item, Gboolean always)

void gtk_check_menu_item_toggled(

GtkCheckMenuItem *check_menu_item)

```

### 信号

- "toggled" void cb(GtkWidget *, gpointer)

以下示例显示了图 21-7 中展示的窗口。

```c

static GtkWidget *makeWidget()

{

    GtkWidget *widget;

    widget = gtk_check_menu_item_new_with_label(

             " Check Label");

    gtk_check_menu_item_set_show_toggle(

             GTK_CHECK_MENU_ITEM(widget), TRUE);

    return(widget);

}
