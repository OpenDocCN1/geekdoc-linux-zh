
## 参数

参数是 `GtkObject` 最有趣的特性之一。参数是一种用于发现对象拥有内容的机制。使用对象参数，可以发现对象支持的内容。这对于实现绑定的人非常有帮助。最后，参数在未来的 GTK 版本中将是可配置的，用户。

## 设置对象参数

参数通常用作设置控件属性的 API。然而，并不是所有的 GTK+ API 都通过对象导出，因此并非总是可能的。设置属性时最方便的接口是 `gtk_object_set()`。这是一个示例：

```c
gtk_object_set (GTK_OBJECT(hbox),
    "GtkContainer::border_width", (gulong) 10,
    NULL);
```

上述代码的效果等同于：

```c
gtk_container_set_border_width (GTK_CONTAINER(hbox), 10);
```

## 第 9 章. GTK+ 对象与类型系统

如果你没有在参数名中指定类名，GTK+ 将从对象的实际类型开始，在每个父类的参数表中查找名称，直到找到正确的类名（在本例中为 `GtkContainer`）。如果你指定了类名，GTK+ 将仅在指定类的参数表中查找该参数。

由于 `gtk_object_set()` 使用 C 语言的可变参数，它的类型安全性有限。这在你的代码中可能会引发严重问题。你可能已经在 `gtk_object_set()` 的示例调用注意了 `gulong`。参数 `GtkContainer::border_width` 的类型为 `GTK_TYPE_ULONG`，它将从参数中提取 `size(gulong)` 字节。如果你省略强制转换，C 可能会只向函数传递 `size(int)`。正如你所想象的，这会导致程序的内存损坏。这种问题也会出现在类型为 `GTK_TYPE_DOUBLE` 的参数上；如果你传递 `5` 而不是 `0`，C 将传递一个整数传递给 `gtk_object_set()`。一旦引入这些 Bug，非常难发现。

`gtk_object_set()` 是更具功能性的调用 `gtk_object_setv()` 的语法糖，后者在内部将其参数列表中的每个键值对转换为 `GtkArg`。

```c
GtkArg args[1];
args[0].name = "GtkContainer::border_width";
args[0].type = GTK_TYPE_ULONG;
GTR_VALUE_ULONG(args[0]) = 10;
gtk_object_setv(GTK_OBJECT(button),
  1,
args);
```

`gtk_object_setv()` 的第二个参数是 `GtkArg` 数组的长度。在手动编写代码时，`gtk_object_set()` 更容易使用，但 `gtk_object_setv()` 可以传递动态构建的参数数组——如果你正在将 GTK+ 导出到解释环境中，这非常方便。

在创建对象时设置对象也是可能的。你可以使用 `gtk_object_new()` 函数创建对象，使用 `gtk_widget_new()` 函数创建大多数小部件。这些程序接收 `GType` 作为第一个参数，并创建该类型的对象或小部件。然后它们接收一个参数值对列表，就像 `gtk_object_set()` 一样。还有 `gtk_object_new()` 和 `gtk_widget_new()` 的变体。

## 读取对象参数

为了获取一个或多个参数，你需要创建一个 `GtkArg` 数组，填充每个 `GtkArg` 的名称，`gtk_object_setv()` 会填充参数值字段。如果发生错误，该字段将设置为 `GTK_TYPE_INVALID`。如果返回值的基本类型是 `GTK_TYPE_STRING` 或 `GTK_TYPE_BOXED`，则你负责释放它。

这是一个简单的示例：

```c
GtkArg args[2];
args[0].name = "GtkContainer::border_width";
args[1].name = "GtkContainer::resize_mode";
```

```c
gtk_object_getv (GTK_OBJECT (button),
      args);
```

```c
g_assert(args[0].type == GTK_TYPE_ULONG);
g_assert(args[1].type == GTK_TYPE_RESIZE_MODE);
g_assert(GTK_FUNDAMENTAL_TYPE(args[1].type) == GTK_TYPE_ENUM);
```

```c
printf("*Border width: %lu Resize mode: %d\n",
       GTK_VALUE_ULONG(args[0]), GTK_VALUE_ENUM(args[1]));
```

## 在你的 GtkObject 子类中使用对象参数

如果你正在编写自定义的 `GtkObject` 或现有对象的自定义子类，你可以在类初始化函数中注册你的对象参数，同时注册对象的信号。要实现这一点，调用 `gtk_object_add_arg_type()`——这里有一个来自 `GtkContainer` 的示例：

```c
gtk_object_add_arg_type(*GtkContainer::border_width,
             GTK_TYPE_ULONG,
             GTK_ARG_READWRITE,
             GTK_ARG_BORDER_WIDTH);
```

第一个参数必须是静态字符串，因为 GTK+ 不复制它。它还必须与你的新类名结合，用冒号与参数隔开（联想到 C++ 的作用域运算符）。第二个参数应该是参数的类型；可以是任何 GTK+ 已知的 `GtkType`。
第三个参数包含一个或多个标志，定义在 `gtk/gtkobject.h` 中。标志如下：

- `GTK_ARG_READABLE` 意味着参数的值可以使用 `gtk_object_getv()` 读取。
- `GTK_ARG_WRITABLE` 意味着参数的值可以使用 `gtk_object_set_setv()` 或 `gtk_object_set_setv()` 写入。
- `GTK_ARG_CONSTRUCT` 意味着参数在构造时会被初始化。
- `GTK_ARG_CONSTRUCT_ONLY` 意味着参数仅在构造时使用，不能读取或写入。
- `GTK_ARG_CHILD` 是子参数的标志。

## 发现可选的对象参数

你可以使用 `gtk_object_query_args()` 轻松在运行时找出给定的 `GtkObject` 理解了哪些参数。这里有一段实用代码，可以打印出给定 `GtkObject` 整个类层级的所有参数：

```c
void
print_arguments(Gtkobject* object)
{
    GtkType type;
    type = GTK_OBJECT_TYPE(object);
    do {
        Gtkarg* args;
        guint32* flags;
        guint n_args;
        args = gtk_object_query_args(type,
                                    &flags,
                                    &n_args);
        printf("Displaying arguments for object type '%s\n",
               gtk_type_name(type));
        i = 0;
        while (i < n_args) {
            printf("- Argument %u is called '%s' and has type '%s\n",
                   i,
                   args[i].name,
                   gtk_type_name(args[i].type));
            ++i;
        }
        free(args);
        free(flags);
    } while (type != GTK_TYPE_INVALID);
```

注意，可以使用 `gtk_type_parent()` 函数获取类型的父类型，并使用 `GTK_OBJECT_TYPE()` 宏从 `GtkObject` 中提取 `GtkType` 句柄。`GTK_OBJECT_TYPE()` 的定义如下：

```c
#define GTK_OBJECT_TYPE(obj) ((GTK_OBJECT(obj))->class->type)
```
