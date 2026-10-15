
```c
void mawa_dosomethingnested(GError **error)
{
    int i;
    boolean it_worked;
    GError *simple_error = NULL;

    << 执行某些操作 >>

    if (!it_worked)
    {
        g_set_error(error,
            MAWA_DOSOMETHING_ERROR,
            MAWA_DOSOMETHING_ERROR_PANIC,
            "Panic in do_something_nested(), i = %d", i);

        return;
    }

    do_something_simple(&simple_error);
    if (simple_error != NULL)
    {
        << 额外的错误处理 >>

        g_propagate_error(error, simple_error);
    }
}
```

在 `do_something_nested()` 中，如果函数的第一部分失败，会发生类似的错误初始化。然而，如果第一部分成功，该函数将继续执行 `do_something_simple()`。函数可以设置错误代码，并将该条件传回给原始调用者是有意义的。通过这样做，函数在 `simple_error` 中收集 `do_something_simple()` 的条件；然后使用 `g_propagate_error()` 将 GError 结构体从 `simple_error` 传输到 `error`。

**警告**：永远不要释放你传递给任何其他函数的 GError **指针**。如果它恰好是 NULL，当你尝试解引用（访问）它的任何内容时，你的程序将会崩溃。

要将从函数获取错误发送到其他地方，请使用：

```c
g_propagate_error(error_dest, error_src)
```

在这里，`error_dest` 是作为 `GError **` 的错误目标，`error_src` 是作为 `GError *` 的源。如果目标为 NULL，此函数只需将源复制到目标。然而，如果目标不为 NULL，该函数将释放源错误。

### 1.4.8 带有错误报告的异常处理

# GNOME 2 官方开发者指南

你现在可能已经注意到 GError 努力实现关于 NULL 的透明性，这样当你不在乎错误的性质时，就不需要担心内存泄漏或额外的 GError 指针。此外，如果你的某个函数遇到 NULL 错误条件，你可以将其视为提示，说明用户不希望任何特殊的错误处理并可能希望修复它。

你应该始终记住，只要使用正确，GError 是处理异常的工具。

## 1.5 数据结构

GLib 拥有许多结构，包括列表、树和哈希表。对于字符串，GLib 提供了 `GString` 结构。

### 1.5.1 字符串

`GString` 是一个根据需要增长的动态字符串。它内部不是空结尾的，但它存储了长度，这使得查找字符串长度非常快。

要创建一个 `GString`，使用 `g_string_new` 函数：

```c
GString *s = g_string_new("initial string");
```

如果你对存储在 `GString` 中的文本量大致了解，使用 `g_string_sized(size)` 预留 `size` 字节。正如前面提到的，`GString` 可以包含二进制数据，包括 NULL 字节。当然，当你初始化这些字符串时需要指定数据的长度，因为没有通用的终止符。分配此类字符串使用：

```
g_string_new_len(initial_data, length)
```

#### 添加字符

所有函数都返回 `GString *`：

- `g_string_append(GString *gstring, const gchar *str)`

  将 `str` 值添加到 `gstring` 的末尾。

- `g_string_append_c(GString *gstring, gchar c)`

  将 `c` 添加到 `gstring`。

- `g_string_append_unchar(GString *gstring, gunichar c)`

  将 Unicode 字符 `c` 添加到 `gstring`。

如果你想在字符串的开头插入内容，请使用 `g_string_prepend` 函数；它们的名称在前面的列表中描述。

`g_string_insert` 函数相同，只是它们多了一个参数（在字符串中插入的索引；第一个索引为 0）：

- `g_string_insert(GString *gstring, gssize pos, const gchar *str)`

- `g_string_insert_c(GString *gstring, gssize pos, gchar c)`

- `g_string_insert_unchar(GString *gstring, gssize pos, gunichar c)`

以下代码在名为 `sl` 的字符串上演示了其中五个函数。

```c
sl = g_string_assign(sl, "ar*");
sl = g_string_append(sl, "gh*");
sl = g_string_prepend(sl, "aa*");
sl = g_string_prepend_c(sl, 'H');
```

```c
sl = g_string_insert(sl, 4, "rr");
g_print("%s\n", sl->str);/* 输出 "Aaaarrrgh" */
```

要向 `GString` 插入数据，请使用这些函数：

- `g_string_append_len(GString *gstring, gsize pos, const gchar *str)`

- `g_string_prepend_len(GString *gstring, gsize pos, const gchar *str, gsize length)`

- `g_string_insert_len(GString *gstring, gsize pos, const gchar *str, gsize length)`

#### 删除字符

你可以可以使用函数从 `GString` 的任意位置提取字符：

```
g_string_erase(string, index, num_to_remove)
```

要将字符串截断到特定长度，请使用：

```
g_string_truncate(desired_length)
```

其中 `desired_length` 是字符串的最终长度。如果你尝试将字符串截断为比实际长度更大的尺寸，什么都不会发生。如果你还想让字符串的分配大小也增长到该长度，此函数可以实现截断并扩展：

```
g_string_set_size(desired_length)
```

```c
sl = g_string_assign(sl, "Anyway");
sl = g_string_erase(sl, 4, 1);
/* sl 现在应该是 "Anywy" */
sl = g_string_truncate(sl, 3);
g_print("%s\n", sl->str);/* 输出 "Any" */
```

注意，新扩展字符串末尾的新数据是未定义的。在实践中，这种结果通常没有影响，GLib 会用 NULL 字节终止字符串。以下是这些函数的示例：

#### 杂字符串函数

以下是杂杂字符串函数：

- `g_string_equal(string1, string2)`

- `g_string_hash(string)`

比较 `string1` 和 `string2`，如果它们匹配则返回 TRUE。注意，此函数不像 `strcmp()`。

- 返回字符串的 31 位键值。有关哈希键值的更多信息，请参见第 1.5.5 节。

- `g_string_printf(string, format, ...)`

类似于 `sprintf()`，它将输出存储在 `GString` 字符串中。返回值为 `GString` 字符串以及其他的字符串处理函数。

### 1.5.1 字符串

- `g_string_append_printf(string, format, ...)`

与前面的函数相同，它将结果追加到 `*string*` 中，而不是替换原来的值。

#### 释放字符串

使用 `free(string, free_orig)` 释放 `GString`：

```
g_string_free(string, free_orig)
```
