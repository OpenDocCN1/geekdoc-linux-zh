
如所示，在发射信号之前之后都需要特定的操作；因此它应该只通过 `gtk_widget_size_request()` 函数发射。

## 信号发射时发生了什么

由于在创建信号和连接回调时有很多选项，你可能对信号发射时发生的情况感到困惑。以下是事件序列的总结：

- 1. 如果通过信号名称发射，则会查找信号 ID。
- 2. 如果另一个相同的信号发射正在进行，并且该信号设置了 `GTK_RUN_NO_RECURSE` 标志，GTK+ 会信号发射重启，本次发射结束。
- 3. 如果信号是 `GTK_RUN_FIRST`，则使用信号的封送（marshall）调用默认处理器。如果从处理器处停止了发射（使用 `g_emit_stop_by_name(i)` 或其变体），则本次发射结束。如果在此处理器内部重新发射信号且为 `GTK_RUN_NO_RECURSE`，它将重新启动。
- 4. 如果为此信号安装了任何发射钩子（emission hooks），它们将被调起。GTK+ 在此点不会检查发射是否已停止或重新发射；它不会检查下一步。发射钩子不会重新发射它们正在监控的信号，也不会尝试停止它。
- 5. 正常连接的回调将使用信号的封进行调用。通过 `g_signal_connect_after()` 连接的回调在此点不会被调用。在每个回调之后，GTK+ 会检查它是否停止了信号，发射随之结束。GTK+ 还会检查信号是否重新发射，并为 `GTK_RUN_NO_RECURSE` 信号重启进程。
- 6. 如果信号是 `GTK_RUN_LAST`，则调用默认处理器。之后 GTK+ 再次检查发射是否已停止或是否应该重启。
- 7. 任何通过 `gtk_signal_connect_after()` 连接的回调都将被调用。在调用每个回调后，GTK+ 检查发射是否应该停止或重启。

在每个步骤内部，处理器都会被调用。步骤的顺序是固定的：`GTK_RUN_FIRST` 默认处理器、发射钩子、普通回调、`GTK_RUN_LAST` 默认处理器。

## 对象初始化

要编写自己的子类，你必须在 `GClass` 中实现以下方法：

```
void (* shutdown) (GObject *object);

void (* destroy) (GObject *object);

void (* finalize) (GObject *object);
```

`shutdown` 方法在对象被销毁之前调用。`finalize` 方法在引用计数归零时调用。`shutdown` 方法允许你执行不需要资源的操作。`finalize` 方法用于释放资源。

## 链式调用 (Chaining Up)

为了更具体一点，让我们看看用于销毁对象的函数。首先是 `gtk_object_destroy()`：

```
void

gtk_object_destroy(GObject *object)

  g_return_if_fail (object != NULL);

  g_return_if_fail (GTK_IS_OBJECT (object));

  g_return_if_fail (GTK_OBJECT_CONSTRUCTED (object));

  if (GTK_OBJECT_DESTROYED (object))

    gtk_object_ref (object);

    object->class->shutdown (object);

    gtk_object_unref (object);
```

注意，已销毁但未最终化的对象会被标记，可以使用 `GTK_OBJECT_DESTROYED()` 宏检查此标记。`gtk_object_destroy()` 通过忽略任何已销毁的对象来确保对象不会重复销毁。如果对象尚未被销毁，`gtk_object_destroy()` 会引用它以防止在销毁过程中执行 `finalize`，并调用 `shutdown` 方法，默认情况下该方法如下：

```
static void

gtk_object_shutdown (GObject *object)

{

  GTK_OBJECT_SET_FLAGS (object, GTK_DESTROYED | DESTROY);

  gtk_signal_emit (object, object_signals[DESTROY]);

}
```

# 第 9 节. GTK+ 对象的对象与类型系统

此方法设置了销毁标记，以确保任何递归的 `gtk_object_destroy()` 调用都不会产生影响；然后它会发出“destroy”信号。`gtk_object_shutdown()` 本身似乎毫无意义；然而，子类可能会重写此方法，以执行更实质的操作，并链式调用到 `GtkObject` 的默认方法（见“链式调用”章节）。

人们可能不清楚的是，`gtk_object_shutdown()` 是一个方法实现，而 `gtk_object_destroy()` 是一个公共函数。请注意，`gtk_object_shutdown()` 是 `GtkObject` 类实现 `shutdown` 方法的内部函数，而 `gtk_object_destroy()` 是公共 API 的一部分。`GtkObject` 对该方法的实现称为 `gtk_object_real_destroy()`：

```
static void

gtk_object_real_destroy (GtkObject *object)

{

    if (GTK_OBJECT_CONNECTED(object))

        gtk_signal_handlers_destroy(object);
```

这段代码只调用与对象相关的任何信号处理程序。`object_object_real_destroy()` 是在发出“destroy”信号时调用的默认处理器。`gtk_object_destroy()` 调用了（可能被重写的）类函数 `shutdown`；默认的 `shutdown` 发出“destroy”信号。

初始化由 `gtk_object_unref()` 完成，且仅当引用计数达到 0 时，用户才能直接调用 `gtk_object_unref()`，但通常是 `gtk_object_destroy()` 调用了它。代码如下：

```
void

gtk_object_unref (GtkObject *object)

{

    g_return_if_fail (object != NULL);

    g_return_if_fail (GTK_IS_OBJECT(object));

    g_return_if_fail (object->ref_count > 0);

    if (object->ref_count == 1)

    {

        gtk_object_destroy(object);

        g_return_if_fail (object->ref_count > 0);

    }

    if (object->ref_count == 0)

    {

        object->klass->finalize (object);

    }

}
```

如果一个对象的引用计数为 1，调用 `gtk_object_unref()` 将调用 `shutdown` 和 `destroy` 方法（通过 `gtk_object_destroy()`）并对对象析析（除非在 `shutdown`/`destroy` 过程中引用计数被增加；如果对象的引用计数在 `gtk_object_unref()` 开始时就大于 1，则引用计数只是简单地递减）。

再次注意，如果用户调用 `gtk_object_destroy`，一个对象在引用计数大于 1 时也可以被销毁；如果发生这种情况，在持有剩余引用的者调用 `gtk_object_unref` 之前，不会发生析构操作。在最常见的情况下，`gtk_object_destroy()` 的实现持有最后的引用计数——请记住这一点查看 `gtk_object_destroy()` 的代码。

为了完整起见，请参见 GObject 的默认 `finalize` 方法：

```
static void

gtk_object_finalize(GtkObject *object)

{

    gtk_object_notify_weaks (object);

    g_datalist_clear (&object->object_data);

    gtk_type_free (GTK_OBJECT_TYPE (object), object);

}
