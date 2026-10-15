
- `database`：指定要使用的数据库。
- `quark_name`：指定要检索的值的完全限定名（作为 quark）。
- `quark_class`：指定要检索的值的完全限定类（作为 quark）。
- `quark_type_return`：返回目的地的表示类型（作为 quark）。
- `value_return`：返回数据库中的值。

`XrmGetResource` 和 `XrmGetResource` 函数从指定的数据库中检索资源。两者都包含一个完全限定名/类对、一个目的资源表示以及一个(大小/地址)对的地址。该值和返回的类型指向数据库；因此，你不能修改数据。

数据库仅在执行 `XrmPutResource`、`XrmMergeDatabases` 时才会释放或覆盖条目。未使用返回给你的地址或未合并数据库的客户端必须在退出前保持安全。如果通过 `XrmGetResource` 和 `XrmGetResource` 找到了资源，则它们返回 True；否则，它们返回 False。

大多数应用程序和工具包不会对资源数据库进行随机探测以获取资源。资源数据库的 XML 访问模式是风格化的。从 1 到 20 次的探测中，每次探测仅在最后的名称/类上不同。`XrmGetResource` 函数在最坏的情况下是 2n 算法，其中 n 是名/类列表的长度。应用程序程序员可以通过预取一个可能匹配名/类列表第一部分的数据库级别列表来改进这一点。

要获取数据库级别列表，请使用 `XrmGetSearchList`。

```
Bool XrmGetSearchResource(database, names, classes, list_return, list_length);
```

- `database`：指定要使用的数据库。
- `names`：指定资源名列表。
- `classes`：指定资源类列表。
- `list_return`：返回进一步搜索的列表。调用者在调用 `XrmGetSearchList` 之前必须为列表分配足够的空间。
- `list_length`：指定为 `list_return` 分配的条目数量（不是字节大小）。

`XrmGetSearchList` 获取名称和类列表，并返回可能匹配的数据库级别列表。返回的列表按从优到劣排序，并使用与 `XrmGetResource` 相同的算法来确定优先级。如果列表足够大用于搜索列表，`XrmGetSearchList` 返回 True；否则返回 False。

调用者必须分配的搜索列表大小取决于存储在数据库中的资源级别和通配符数量。最坏情况长度为 3^n，其中 n 是 `names` 或 `classes` 中名称或类组件的数量。

当使用 `XrmQgGetSearchList` 随后对具有相同名称的资源进行多次探测时，公共前缀应在 `XrmGetSearchList` 中指定。

要为给定的资源搜索数据库级别，请使用 `XrmGetResource`。

```
Bool XrmGetSearchResource(database, str_name, str_class, str_type_return, value_return);
```

- `database`：指定要使用的数据库。
- `str_name`：指定要检索的值的完全限定名（字符串形式）。
- `str_class`：指定要检索的值的完全限定类（字符串形式）。
- `str_type_return`：返回目的地的表示类型（字符串形式）。
- `value_return`：返回数据库中的值。

`XrmGetResource` 和 `XrmGetResource` 函数从指定的数据库中检索资源。两者都包含一个完全限定名/类对、一个目的资源表示以及一个(大小/地址)对的地址。该值和返回的类型指向数据库；因此，你不能修改数据。

如果通过 `XrmGetResource` 和 `XrmGetResource` 找到了资源，则它们返回 True；否则，它们返回 False。

# 存储到资源数据库

要将资源存储到数据库，`XrmPutResource` 或 `XrmMergeDatabases` 执行部分资源规格、表示类型和值。

```
void XrmPutResource(database, specifier, type, value);
```

- `database`：指定资源数据库。
- `specifier`：指定资源的完整或部分规格。
- `type`：指定资源的类型。
- `value`：指定数据库中的值。

数据库仅在执行 `XrmPutResource`、`XrmMergeDatabases` 时才会释放或覆盖条目。未使用返回给你的地址或未合并数据库的客户端必须在退出前保持安全。

# 资源管理器函数

如果指定符和类型不在主机可移植编码（Host Portable Encoding）中，结果取决于实现。值在不经修改的情况下存储在数据库中。

```
void XrmQmPutResource(database, bindings, quarks, value);
```

- `database`：指定资源数据库。
- `bindings`：指定绑定列表。
- `quarks`：指定资源的完整或部分名称或类列表。
- `type`：指定资源的类型。
- `value`：指定资源的值，指定为字符串。

如果数据库包含 NULL，`XrmQmPutResource` 会创建一个新数据库并返回其指针。如果数据库中已存在相同绑定和 `quarks` 的资源条目，则之前的类型和值将被新指定的类型和值替换。值在不经修改的情况下存储在数据库中。

要添加指定为字符串的资源，请使用 `XrmPutStringResource`。

```
void XrmPutStringResource(database, specifier, value);
```

- `database`：指定资源数据库。
- `specifier`：指定资源的完整或部分规格。
- `value`：指定资源的值，指定为字符串。

如果数据库包含 NULL，`XrmPutStringResource` 会创建一个新数据库并返回其指针。`XrmPutStringResource` 向指定的数据库添加资源。`XrmPutStringResource` 是一个便利函数，它首先对指定符调用 `XrmStringToQuarkList`，然后调用 `XrmPutResource` 并使用 "String" 表示类型。如果指定符不在主机可移植编码中，结果取决于实现。值在不经修改的情况下存储在数据库中。

要使用 `quarks` 作为规格添加字符串资源，请使用 `XrmPutStringResource`。

如果 `database` 包含 NULL，`XrmPutStringResource` 将创建一个新的数据库并返回其指针。`XrmPutStringResource` 是一个便利例程，它返回一个对应字符串值的 `XrmValue`（通过使用 `strlen` 计算大小），然后调用 "String" 表示类型。该值将在不经过任何修改的情况下存储在数据库中。

要添加一个指定为包含名称和值的字符串的单个资源条目，请使用 `XrmPutLineResource`。

```
void XrmPutLineResource(database, line);
```

- 指定资源数据库。
- 将资源名称和值值对作为单行进行指定。

如果 `database` 包含 NULL，`XrmPutLineResource` 将创建一个新的数据库并返回其指针。`XrmPutLineResource` 会向指定的数据库添加一个单个资源条目。该行应采用 `valueLine` 格式（见第 15.1 节），并以换行符或空字符结束终止；使用具有错误语法的字符串导致的数据结果取决于实现。该字符串将在数据库的区域设置（locale）中进行解析。如果 `ResourceName` 不在主机可移植字符编码（Host Portable Character Encoding）中，结果取决于实现。请注意，注释行不会被存储。

## 枚举数据库条目

要枚举数据库的条目，请使用 `XrmEnumerateDatabase`。

```
#define XrmEnumAllLevels 0
#define XrmEnumOneLevel 0

Bool XrmEnumerateDatabase(database, name_prefix, class_prefix, mode, (*proc)(), arg);
```

- 指定资源数据库。
- 指定资源名称前缀。
- 指定资源类前缀。
- 指定要枚举的层数。
- 指定为每个匹配的条目调用的过程。
- 指定将传递给该过程的用户提供的参数。

`XrmEnumerateDatabase` 函数会为数据库中每个匹配给定的名称/类资源前缀补全的资源调用该过程。发现资源的顺序取决于实现。如果 `mode` 为 `XrmEnumOneLevel`，则资源必须通过分配的单个名称和类匹配给定的名称/类前缀。如果 `mode` 为 `XrmEnumAllLevels`，资源必须匹配类前缀，并附加一个或多个名称和类。如果过程返回 True，则枚举终止且函数返回 True。如果过程始终返回 False，则枚举所有匹配的资源并函数返回 False。

调用过程时带有以下参数：

```
(*proc)(database, bindings, quarks, type, value, arg)
```
