
```c
GtkType gtk_button_get_type (void) {
  static GtkType button_type = 0;

  /* 尚未生成 ID */
  if (!button_type) {
    GtkTypeInfo button_info = {
      "GtkButton",
      sizeof (GtkButton),
      sizeof (GtkObjectClass),
      GtkClassInitFunc gtk_button_class_init,
      GtkObjectInitFunc gtk_button_init,
      GtkArgSetFunc gtk_button_set_arg,
      GtkArgGetFunc NULL,
    };

    button_type = gtk_type_unique (gtk_container_get_type(), &button_info);
  }
  return button_type;
}
```

下一步是定义 `gtk_button_class_init` 和 `gtk_button_init` 函数。

## 类初始化

在 `get_type` 函数中定义的 `class_init` 函数创建控件类结构。控件类定义了该类型所有控件的通用信息。信息包括定义新信号和重定义旧信号。通过定义的信号数组添加新按钮信号：

```c
static guint button_signals[LAST_SIGNAL] = {};
```

`LAST_SIGNAL` 是枚举的一部分。按钮的类初始化分为几部分。下面总结了更重要的代码。第一部分涉及从控件类获取信息。

```c
static void gtk_button_class_init (GtkButtonClass *class)
{
    GtkObjectClass *object_class;
    GtkWidgetClass *widget_class;
    GtkContainerClass *container_class;
    GtkButtonClass *parent_class;

    object_class = (GtkObjectClass*) class;
    widget_class = (GtkWidgetClass*) class;
    container_class = (GtkContainerClass*) class;
    parent_class = (GtkButtonClass*) class->parent_class;
```

下一步是创建新信号。`button_signals` 必须填充这些信号。每个信号都用 `gtk_signal_new` 创建并放入数组中。`gtk_signal_new` 函数定义为：

```c
gint gtk_signal_new (const gchar *name,
                     GtkSignalType run_type,
                     GtkType object_type,
                     gint function_offset,
                     GtkSignal marshaller,
                     GtkType return_val,
                     gint nparams,
                     GtkType types[]);
```

“pressed”和“clicked”信号仅不同名称和信号偏移。它们使用默认 marshaller 且没有参数。

### 第15章 创建你自己的控件

```c
button_signals[PRESSED] =
    gtk_signal_new ("pressed",
                    GTK_RUN_FIRST,
                    object_class->type,
                    GTK_SIGNAL_OFFSET (GtkButtonClass, pressed),
                    gtk_signal_default_marshaller,
                    GTK_TYPE_NONE, NULL);

button_signals[CLICKED] = 
    gtk_signal_new ("clicked",
    GTK_RUN_FIRST,
    object_class->type,
    GTK_SIGNAL_OFFSET (GtkButtonClass, clicked),
    gtk_signal_default_marshaller,
    GTK_TYPE_NONE, NULL);
```

然后信号需要添加到对象类。

```c
gtk_object_class_add_signals (object_class, button_signals, LAST_SIGNAL);
```

控件还可以选择覆盖任何父类中的任何信号。按钮选择覆盖许多信号和一些容器信号。

```c
widget_class->activate_signal = button_signals[CLICKED];
widget_class->map = gtk_button_map;
widget_class->unmap = gtk_button_unmap;
widget_class->realize = gtk_button_realize;
widget_class->draw = gtk_button_draw;
widget_class->focus = gtk_button_draw_focus;
widget_class->default = gtk_button_draw_focus;
widget_class->size_request = gtk_button_size_request;
widget_class->size_allocate = gtk_button_size_allocate;
widget_class->expose = gtk_button_expose;
widget_class->press_event = gtk_button_button_press;
widget_class->release_event = gtk_button_button_release;
widget_class->enter_notify_event = gtk_button_enter_notify;
widget_class->leave_notify_event = gtk_button_leave_notify;
widget_class->in_event = gtk_button_focus_in;
widget_class->out_event = gtk_button_focus_out;
container_class->add = gtk_button_add;
container_class->remove = gtk_button_remove;
container_class->foreach = gtk_button_foreach;
```

最后，填充信号。“clicked”信号被设置为 NULL，因为控件本身不关心该信号，但开发者在使用按钮进行编程时可能关心该信号。

```c
class->pressed = gtk_real_button_pressed;
class->released = gtk_real_button_released;
class->clicked = NULL;
class->enter = gtk_real_button_enter;
class->leave = gtk_real_button_leave;
}
```

## 发射信号

在 GTK+ 中，可以使用 `gtk_signal_emit` 函数或 `gtk_signal_emit_by_name` 函数来发射信号。通常，`gtk_signal_emit` 在小部件内部使用，因为它可以访问信号表并知道信号 ID。`gtk_signal_emit_by_name` 使用名称而不是信号 ID，主要在小部件外部使用。`GtkButton` 的代码包含一个 `gtk_button_clicked` 函数，可以通过调用它来发射"clicked"点击）信号。它所做的只是调用了 `gtk_signal_emit` 函数。

```c
void gtk_button_clicked (GtkButton *button)
{
  gtk_signal_emit (GTK_OBJECT (button), button_signals[CLICKED]);
}
```
