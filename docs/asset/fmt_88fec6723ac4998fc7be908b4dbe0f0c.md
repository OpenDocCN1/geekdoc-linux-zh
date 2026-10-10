
```
gdk_draw_string(ev->event_window,
      widget->style->font,
      widget->style->black_gc,
      x,
      y,
      title);

gdk_set_clip_rectangle(widget->style->black_gc, NULL);
```

## 处理焦点

`GtkEv` 想要接收键事件，以便报告有关这些事件的信息。正如第 3 章中的“焦点”部分和第 10 章中的“键盘焦点”部分讨论的，顶层窗口从 GDK 接收键事件。`GtkWindow` 跟踪当前的焦点小部件并将键事件转发给它。

如果窗口接收到键事件，它必须：

- 设置其 `GTK_CAN_FOCUS` 标志，以便 `Gtk+` 将其视为一个可能的焦点小部件。
- 响应 "`focus_in`" 和 "`focus_out`" 信号，通过绘制和擦除视觉指示来表示它拥有焦点。

`GtkEv` 在 `gtk_ev_init()` 中设置了 `GTK_CAN_FOCUS` 标志；它如下所示实现了 `focus_in` 和 `focus_out` 方法：

```c
static void

ev_focus_in (GtkWidget *widget, GdkEvent *event) {

    // ... 实现略 ...

}

static void

ev_focus_out (GtkWidget *widget, GdkEvent *event) {

    // ... 实现略 ...

}
```
