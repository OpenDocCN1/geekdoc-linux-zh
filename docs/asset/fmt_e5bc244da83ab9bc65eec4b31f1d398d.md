
参数 `clist` 指定了感兴趣的 `clist`。将 `use_icons` 设置为 `TRUE` 可启用该 `clist` 的拖拽图标，而将其设置为 `FALSE` 则禁用。

你的应用程序可以通过调用 `gtk_clist_row_move()` 将行从一个位置移动到另一个位置：

# 第 6 章 • 列表

```c
void
gtk_clist_row_move(GtkClist *clist, gint source_row, gint dest_row);
```

参数 `source_row` 和 `dest_row` 分别指定要移动行在列表中的位置以及该行数据在移动后的位置。`source_row` 和 `dest_row` 都必须在 `[0, m - 1]` 范围内。

`GtkClist` 提供了对应用程序非常有用的功能。默认情况下，`GtkClist` 禁用了排序；要启用它，你可以调用 `gtk_clist_set_auto_sort()`。

```c
void
gtk_clist_set_auto_sort(GtkClist *clist, gboolean auto_sort);
```

将 `auto_sort` 设置为 `TRUE` 可启用排序，设置为 `FALSE` 则禁用。当向 `clist` 添加新项目时会进行排序。每当调用 `gtk_clist_set_auto_sort()` 将自动排序从禁用切换为启用时，`clist` 就会执行一次排序。由于每次添加项时都会执行排序，你可能会发现在应用程序向列表添加大量项时禁用排序，并在列表构建完成后重新启用排序，这样会更有效。例如：

```c
gtk_clist_set_auto_sort( clist, FALSE );
// 在此处添加项
```

```c
gtk_clist_set_auto_sort( clist, TRUE );
```

`clist` 的默认顺序被设置为 `GTK_SORT_ASCENDING`（可以通过调用 `gtk_clist_set_sort_type()` 来更改，如本章后文所示）。默认情况下对 `clist` 的第 0 列进行排序；其他列不是排序结果的因素。`GtkClist` 使用的排序（归并排序）使用一个比较函数，其结果是正在排序列中的数据基于 ASCII 值进行的。虽然这适用于字符串和字符的排序，但并不适用于数值数据。例如，按升序排序字符串 "1", "2", "13" 和 "1234" 会得到 "1", "1234", "13" 和 "2"，这可能不是预想要的结果。为了解决这个问题，你需要创建自己的函数来替换 `GtkClist` 使用的默认排序。这可以使用函数 `gtk_clist_set_compare_func()` 实现。

```c
void
gtk_clist_set_compare_func(GtkClist *clist,
GtkClistCompareFunc cmp_func);
```

参数 `clist` 是 `GtkClist` 实例，`cmp_func` 是指向用于在排序期间比较列表项的指针。该函数的原型必须匹配以下内容：

```c
int MyCompareFunc(GtkClist *clist);
```

将 `NULL` 传递 `gtk_clist_set_compare_func()` 的第二个参数会将比较函数恢复为 `GtkClist` 提供的默认值。值得看一眼 `Gtk+` 提供的默认比较函数，你应该将其作为开发自己的函数的依据：

## 列表 6.1 Gtk+ 默认比较函数

```c
static gint
default_compare (GtkClist *clist, gpointer p1, gpointer p2)
{
char *text1 = NULL;
char *text2 = NULL;

GtkListRow *row1 = (GtkListRow *) p1;
GtkListRow *row2 = (GtkListRow *) p2;

switch (row2->cell[clist->sort_column].type)
{
    case GTK_CELL_TEXT:
    text1 = GTK_CELL_TEXT(row1->cell[clist->sort_column])->text;
    break;
    case GTK_CELL_PIXTEXT:
    text1 = GTK_CELL_PIXTEXT(row1->cell[clist->sort_column])->text;
    break;
    default:
    break;
}
switch (row2->cell[clist->sort_column].type)
{
    case GTK_CELL_TEXT:
    text2 = GTK_CELL_TEXT(row2->cell[clist->sort_column])->text;
    break;
    case GTK_CELL_PIXTEXT:
    text2 = GTK_CELL_PIXTEXT(row2->cell[clist->sort_column])->text;
    break;
    default:
    break;
}
if (text2)
    return (text1 != NULL);

if (!text1)
    return -1;

return strcmp(text1, text2);
}
```

上述函数非常直接。在 007 和 008 行，传入函数的通用指针被赋值给 `GtkListRow` 变量。这允许我们轻松地访问每行中正在排序列的内容。010 到 020 行提取行 1 要比较的数据，022 到 032 行对行 2 执行相同的操作。在 010 行，我们访问正在排序列的单元格类型；该类型决定从单元格获取要比较的文本。注意此检查仅适用于行 1，有两个 `switch` 语句是因为行 1 的数据类型可能与行 2 不同。012 到 17 行的 `switch` 语句说明了如何从行中提取 `GTK_CELL_TEXT` 和 `GTK_CELL_PIXTEXT`。022 到 032 行执行相同的提取。`clist->sort_column` 是进行排序的列。034 到 040 行确保提取的文本有效，最后在 040 行调用 `strcmp()` 进行字符串的实际比较。

有几种方法可以扩展此函数。首先，之前的默认函数引入了仅对单列数据排序的限制。注意我们只选择了 `clist->sort_column` 指定的单元格。如果需要，此此函数转换为对行中的所有单元格进行排序。以下是 `default_compare()` 的修改版本，说明了如何实现：

## 列表 6.2 对行所有单元格排序

```c
static gint
CompareEntireRow(GtkCellList *clist, gpointer ptr1, gpointer ptr2)
{
    char *text1 = NULL;
    char *text2 = NULL;
    int i, ret;
    GtkListRow *row1 = (GtkListRow *) ptr1;
    GtkListRow *row2 = (GtkListRow *) ptr2;
    for (i = 0; i < clist->columns; i++) {
        switch (row1->cell[i].type)
        {
            case GTK_CELL_TEXT:
                text1 = GTK_CELL_TEXT(row1->cell[i])->text;
                break;
            case GTK_CELL_PIXTEXT:
                text1 = GTK_CELL_PIXTEXT(row1->cell[i])->text;
                break;
            default:
                break;
        }
        switch (row2->cell[i].type)
        {
            case GTK_CELL_TEXT:
                text2 = GTK_CELL_TEXT(row2->cell[i])->text;
                break;
            case GTK_CELL_PIXTEXT:
                text2 = GTK_CELL_PIXTEXT(row2->cell[i])->text;
                break;
            default:
                break;
        }
    }
}
```

# GtkClist

```c
break;
}

if (!text2)
    return (text1 != NULL);

if (!text1)
    return -1;

ret = strcmp(text1, text2);
if (ret != 0)
    return( ret );
}
return( 0 );
}
```

此例程的主要区别在于我们添加了一个循环，并且不再是比较每行中的单列，而是从左到右比较行中的每一列。一行的列数由我们传递的 `GtkClist` 指针的 `columns` 字段指定。在第 042 行到 044 行中，我们获取了 `strcmp()` 的返回值。如果该值为 0，则表示正在比较的列在两行中具有相同的值，我们继续从循环顶部处理下一列。如果返回非零，则说明两行不同，我们可以停止搜索。如果我们遍历了某行中的所有列且它们都包含相同的值，我们将到达第 046 行，在该处返回 0 表示这些行具有相同的数据。

要使预测排序函数成为 `clist` 的默认排序函数，你只需要调用以下代码并向 `clist` 中添加内容：

```c
gtk_clist_set_compare_func (GTK_CLIST(clist), CompareEntireRow);
```

关于函数的其余讨论主题涉及要排序的数据。比较函数都假设数据是 ASCII 格式的。然而，假设你的数据是数值、基于日历日期或与基于 ASCII 的比较函数不兼容的特殊格式。解决该问题的方案是将 `strcmp()` 的调用（如前述列表中的第 041、042 行所示）替换为适用于所比较数据类型的函数调用。以下是可以执行特定内容比较的函数示例。第一个函数 `CompareInt()` 根据字符串代表的整数值对两个字符串进行比较，而不是组成字符串的字符的 ASCII 值：

## 列表 6.3 比较整数

```c
// 如果 text1 在整数意义上小于、等于或大于 text2，
// 分别返回 -1、0 或 1，而不是 ASCII 字符串。
CompareInt(char *text1, char *text2)
{
    int val1, val2;
    val1 = atoi( text1 );
    val2 = atoi( text2 );
    if ( val1 < val2 )
        return( -1 );
    else if ( val1 > val2 )
        return( 1 );
    else
        return( 0 );
}
```

第二个函数 `CompareDate()` 可用于比较 `MM/DD/YYYY` 格式的日期字符串。

# 列表 6.4 比较日期

```c
// 如果 text1 在日期意义上小于、等于或大于 text2，
// 分别返回 -1、0 或 1，而不是 ASCII 字符串。日期必须符合
// m(m)/d(d)/y(y) 格式，其中 m、d 和 y 均在 [0,9] 范围内
int
CompareDate(char *text1, char *text2)
{
    char *m1, *m2, *d1, *d2, *y1, *y2; // 日期字符串部分
    int im1, im2, id1, id2, iy1, iy2;     // 整数对应项
    char delim[2];                         // strtok 需要 char *
    char tbuf[NAME_MAX]; // 用于存放 strtok 的拷贝
    /* 复制到字符串，否则 strtok 会破坏它们 */
    strncpy(tbuf, text1, NAME_MAX);
    //（注意：原文中有重复的 strncpy，此处已修正逻辑）
    /* 解析第一个日期 */
    delim = '/';
    m1 = strtok(tbuf, &delim);
    d1 = strtok(NULL, &delim);
    y1 = strtok(NULL, &delim);
    /* 解析第二个日期 */
    //（注意：逻辑意味着 text2 将以类似的方式处理）
    /* 确保每个组件都有内容 */
    if ( m1 || m2 || id1 || id2 || y1 || y2 )
        return( 0 );
    /* 将组件转换为整数以便进行比较 */
    im1 = atoi(m1); id1 = atoi(d1); iy1 = atoi(y1 );
    im2 = atoi( m2 ); id2 = atoi( d2 ); iy2 = atoi( y2 );
    /* 年的优先级高于月，月的优先级高于日 */
    if ( iy1 < iy2 )
        return( -1 );
    else if ( iy1 > iy2 )
        return( 1 );
    else {
        // 年相同的情况
        if ( im1 < im2 )
            return( -1 );
        else if ( im1 > im2 )
            return( 1 );
        else {
            // 日和月相同
            if ( id1 < id2 )
                return( -1 );
            else if ( id1 > id2 )
                return( 1 );
            // 日均相等，继续向下执行
        }
    }
    return( 0 );
}
```

如前所述，应用程序可以指定用于比较函数计算相等性时的排序列。默认列为 0。但是，你可以通过调用 `gtk_clist_set_sort_column()` 设置任何想要的列：

```c
void gtk_clist_set_sort_column(GtkClist *clist, int column);
```

参数值范围在 `[0, n-1]`，其中 `n` 是列数。应用程序更改默认排序列的常见示例：`clist` 可用于显示文件夹的内容，列表中的每行是消息、发送者、日期或其他列显示的信息。用户通常希望按日期或其他字段进行排序。为了实现这一点，程序将注册一个回调函数（前文已讨论）。在回调中，`clist` 对应的列将作为排序列，并通过调用 `gtk_clist_sort()` 进行排序：

```c
void gtk_clist_sort(GtkClist *clist);
```

`gtk_clist_sort()` 函数接收一个参数，即 `GtkClist` 实例。如果客户端未指定，调用此函数将根据排序列和比较函数进行排序。该函数的实现可能如下：

```c
void clist_column(GtkList *clist, int column, gpointer data) {
    gtk_clist_set_sort_column( clist, column);
    gtk_clist_sort( clist );
}
```

这里讨论的最终排序函数允许应用程序指定 `clist` 中排序后的项顺序。有两种选择，如表 6.11 所示。

## 表 6.11 排序值

| 排序顺序 | 含义 |
| :--- | :--- |
| `GTK_SORT_ASCENDING` | 行 0 值最小并随行号增加。 |
| `GTK_SORT_DESCENDING` | 行 0 值最大并随行号减小。 |

这两个值都由 `GtkSortType` 枚举定义。要指定排序后的项顺序，使用 `gtk_clist_set_sort_type()`：

```c
void gtk_clist_set_sort_type(GtkClist *clist, GtkSortType sort_type);
```
