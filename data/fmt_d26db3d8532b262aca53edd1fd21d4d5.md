
| `hscrollbar_policy` | 水平滚动条的策略。有效选项有 `GTK_POLICY_ALWAYS`（默认）、`GTK_POLICY_AUTOMATIC`（需要时显示）和 `GTK_POLICY_NEVER`。 |

| `vscrollbar_policy` | 垂直滚动条的策略。有效选项有 `GTK_POLICY_ALWAYS`（默认）、`GTK_POLICY_AUTOMATIC`（需要时显示）和 `GTK_POLICY_NEVER`。 |

![](img/7fa9959a9d28ad339fa75e44952feeb9_786_0)

```c
gtk_selection_add_target()
void gtk_selection_add_target( GtkWidget *widget, GdkAtom selection,
GdkAtom target, guint info )
```

| 参数 | 描述 |
|---|---|
| `widget` | 将注册的控件指针。 |
| `selection` | 对应的选择项。 |
| `target` | 你想要注册的目标名称原子。 |
| `info` | 稍后传递的应用程序特定整数。 |

```c
gtk_selection_add_targets()
void gtk_selection_add_targets( GtkWidget *widget, GdkAtom selection,
const GtkTargetEntry *targets, guint ntargets )
```

| 参数 | 描述 |
|---|---|
| `widget` | 将注册的控件指针。 |
| `selection` | 对应的选择项。 |
| `targets` | 填充好的 `GtkTargetEntry` 数组指针。 |
| `ntargets` | `targets` 中的项数。 |

```c
gtk_selection_convert()
gint gtk_selection_convert( GtkWidget *widget, GdkAtom selection,GdkAtom target,
guint time )
```

如果请求成功则返回 `TRUE`；如果请求无法处理，则返回 `FALSE`。

| 参数 | 描述 |
|---|---|
| `widget` | 作为请求者的控件。目标的数据将提供给此控件，并在数据准备绪时收到通知。 |

### 函数原型

- `selection`: 定义将处理哪个选择的原子。
- `target`: 定义将检索数据的原子。
- `time`: 请求发生的时间。

```c
gtk_selection_data_set()
void gtk_selection_data_set( GtkSelectionData *selection_data, GdkAtom type, int format, guchar *data, gint length )
```

| 参数 | 描述 |
|---|---|
| `selection_data` | 通过 `selection_get` 信号提供的 `GtkSelectionData` 结构指针。 |
| `type` | 定义提供的数据类型的原子。 |
| `format` | 存储一个类型元素所需的位数。这很重要，因为 X 服务器使用它来判断数据是否应该进行字节交换。 |
| `data` | 提供的数据指针。 |
| `length` | 提供的数据字节长度。 |

```c
gtk_selection_owner_set()
gint gtk_selection_owner_set( GtkWidget *widget, GdkAtom selection, guint time )
```

| 参数 | 描述 |
|---|---|
| `widget` | 将成为选择所有者的控件指针。 |
| `selection` | 需要更改所有者的选择原子。 |
| `time` | 定义所有权的时间戳。 |

```c
gtk_signal_connect()
guint gtk_signal_connect( GtkObject *object, const gchar *name, GtkSignalFunc func, gpointer func_data )
```

| 参数 | 描述 |
|---|---|
| `object` | 你附加回调函数的 `GtkObject`（或其子类）实例。 |

![](img/7fa9959a9d28ad339fa75e44952feeb9_788_0.png)

### 附录 D

| 参数 | 描述 |
|---|---|
| `name` | 你将 `func` 连接到的信号。 |
| `func` | 你注册的回调函数。 |
| `func_data` | 调用时传递给 `func` 的数据。 |

### `gtk_signal_connect_object()`

```c
guint gtk_signal_connect_object( GtkObject *object, const gchar *name, GtkSignalFunc func, GtkObject *slot_object )
```

| 参数 | 描述 |
|---|---|
| `object` | 你附加回调函数的 `GtkObject`（或其子类）实例。 |
| `name` | 你将 `func` 连接到的信号。 |
| `func` | 你注册的参数函数。 |
| `slot_object` | 调用时传递给 `func` 的参数。 |

### `gtk_target_list_add()`

```c
void gtk_target_list_add( GtkTargetList *list, GdkAtom target, guint flags, int info )
```

| 参数 | 描述 |
|---|---|
| `list` | 指向现有 `GtkTargetList` 的指针，新目标必须存储其中。 |
| `target` | 对应于你想要添加的目标名称原子。 |
| `flags` | 这些仅用于拖放放下上下文。 |
| `info` | 应用程序特定整数。 |

### `gtk_target_list_add_table()`

```c
void gtk_target_list_add_table( GtkTargetList *list, const GtkTargetEntry *targets, guint ntargets )
```

| 参数 | 描述 |
|---|---|
| `list` | 指向需要存储新目标项的 `GtkTargetList` 指针。该 `GtkTargetList` 应该通过 `gtk_target_list_new()` 创建。 |
| `targets` | 填充好的 `GtkTargetEntry` 数组指针。 |
| `ntargets` | `targets` 中的项数。 |

### 函数原型

```c
gtk_target_list_find()
```

```c
boolean gtk_target_list_find(GtkTargetList *list, GdkAtom target, guint *info )
```

如果找到目标则返回 `TRUE`，否则返回 `FALSE`。

| 参数 | 描述 |
| --- | --- |
| `list` | 指向 `GtkTargetList` 的指针，在该列表中查找目标。 |
| `target` | 与目标名称对应的原子值（atom），你想要获取该名称的 `info` 字段。 |
| `info` | 指向 `geist` 变量的指针，如果可以检索到，将用它存储 `info` 值。 |

```c
gtk_target_list_new()
```

```c
GtkTargetList* gtk_target_list_new(const GtkTargetEntry *targets, guint ntargets )
```

返回新创建的 `GtkTargetList` 指针。

| 参数 | 描述 |
| --- | --- |
| `targets` | 指向填充 `GtkTargetEntry` 结构体数组的指针。 |
| `ntargets` | `targets` 中的项数。如果将 `targets` 设置为 `NULL` 且 `ntargets` 设置为 `0`，则将创建一个空的 `GtkTargetList`。 |

```c
gtk_target_list_ref()
```

```c
void gtk_target_list_ref( GtkTargetList *list )
```

| 参数 | 描述 |
| --- | --- |
| `list` | 指向 `GtkTargetList` 的指针，应增加其引用计数。 |

```c
gtk_target_list_remove()
```

```c
void gtk_target_list_remove( GtkTargetList *list, GdkAtom target )
```

| 参数 | 描述 |
| --- | --- |
| `list` | 指向 `GtkTargetList` 的指针，新目标必须存储其中。 |
