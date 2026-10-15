
## GtkRange

```
void gtk_range_default_hslider_update(GtkRange *range)

gint gtk_range_default_through_click(GtkRange *range, gint x, gint y, gfloat *jump_perc)

void gtk_range_default_vmotion(GtkRange *range, gint xdelta, gint ydelta)

void gtk_range_default_vslider_update(GtkRange *range)

gint gtk_range_default_vthrough_click(GtkRange *range, gint x, gint y, gfloat *jump_perc)

void gtk_range_draw_background(GtkRange *range)

void gtk_range_draw_slider(GtkRange *range)

void gtk_range_draw_step_back(GtkRange *range)

void gtk_range_draw_step_fortw(GtkRange *range)

void gtk_range_draw_trough(GtkRange *range)

GtkAdjustment *gtk_range_get_adjustment(GtkRange *range)

GtkType gtk_range_get_type(void)

void gtk_range_set_adjustment(GtkRange *range, GtkAdjustment *adjustment)

void gtk_range_set_update_policy(GtkRange *range, GtkUpdateType policy)

void gtk_range_slider_update(GtkRange *range)

gint gtk_range_trough_click(GtkRange *range, gint x, gint y, gfloat *jump_perc)
```

## GtkRuler

此部件是 `GtkHRuler` 和 `GtkVRuler` 的基础类。它包含配置和计算软件，但无法显示结果。

### 继承

`GtkRuler`->`GtkWidget`->`GtkObject`

### 函数

```c
void gtk_ruler_draw_pos(GtkRuler *ruler)

void gtk_ruler_draw_ticks(GtkRuler *ruler)

guint gtk_ruler_get_type(void)

void gtk_ruler_set_metric(GtkRuler *ruler, GtkMetricType metric)

void gtk_ruler_set_range(GtkRuler *ruler, gfloat lower,
                         gfloat upper, gfloat position, gfloat max_size)
```

### 枚举

```c
typedef enum {
    GTK_PIXELS,
    GTK_INCHES,
    GTK_CENTIMETERS
} GtkMetricType;
```

## GtkScale

这是 `GtkHScale` 和 `GtkVScale` 的基础类。

### 继承

`GtkScale`->`GtkRange`->`GtkWidget`->`GtkObject`

### 函数

```c
void gtk_scale_draw_value(GtkScale *scale)

GtkType gtk_scale_get_type(void)

void gtk_scale_get_value_width(GtkScale *scale)

void gtk_scale_set_digits(GtkScale *scale, gint digits)

void gtk_scale_set_draw_value(GtkScale *scale, gboolean draw_value)

void gtk_scale_set_value_pos(GtkScale *scale, GtkPositionType pos)
```

### 枚举

```c
typedef enum
{
    GTK_POS_LEFT,
    GTK_POS_RIGHT,
    GTK_POS_TOP,
    GTK_POS_BOTTOM
} GtkPositionType;
```

## GtkScrollbar

`GtkScrollbar` 类是 `GtkHScrollbar` 和 `GtkVScrollbar` 的`基础类`。

### 继承

`GtkScrollbar`->`GtkRange`->`GtkWidget`->`GtkObject`

### 函数

```c
GtkType gtk_scrollbar_get_type(void)
```

## GtkScrolledWindow

`GtkScrolledWindow` 是一个容器，它不会调整大小以适应分配给它的空间。相反，它会根据需要添加滚动条，以便你可以查看窗口的任何部分。

### 继承

`GtkScrolledWindow`->`GtkBin`->`GtkContainer`->`GtkWidget`->`GtkObject`

### 函数

```c
void gtk_scrolled_window_add_with_viewport(GtkScrolledWindow *scrolled_window,
                                           GtkWidget *child)

GtkAdjustment *gtk_scrolled_window_get_hadjustment(GtkScrolledWindow *scrolled_window)

GtkType gtk_scrolled_window_get_type(void)
```

```c
GtkAdjustment *gtk_scrolled_window_get_vadjustment(
   GtkScrolledWindow *scrolled_window)

GtkWidget *gtk_scrolled_window_new(
   GtkAdjustment *hadjustment, GtkAdjustment *vadjustment)

void gtk_scrolled_window_set_hadjustment(
   GtkScrolledWindow *scrolled_window,
   GtkAdjustment *hadjustment)

void gtk_scrolled_window_set_placement(
   GtkScrolledWindow *scrolled_window,
   GtkCornerType window_placement)

void gtk_scrolled_window_set_policy(
   GtkScrolledWindow *scrolled_window,
   GtkPolicyType hscrollbar_policy,
   GtkPolicyType vscrollbar_policy)

void gtk_scrolled_window_set_vadjustment(
   GtkScrolledWindow *scrolled_window,
   GtkAdjustment *vadjustment)
```

### 枚举

```c
typedef enum {
   GTK_POLICY_ALWAYS,
   GTK_POLICY_AUTOMATIC,
   GTK_POLICY_NEVER
} GtkPolicyType;

typedef enum {
   GTK_CORNER_TOP_LEFT,
   GTK_CORNER_BOTTOM_LEFT,
   GTK_CORNER_TOP_RIGHT,
   GTK_CORNER_BOTTOM_RIGHT
} GtkCornerType;
```

关于 `GtkScrolledWindow` 的示例，请参见第 5 章。

## GtkSeparator

`GtkSeparator` 类是 `GtkHSeparator` 和 `GtkVSeparator` 的基类。

### 继承

`GtkSeparator -> GtkWidget -> GtkObject`

### 函数

```c
GtkType gtk_separator_get_type(void)
```
