
使用

```c
g_create_hash_table_new(hash_func, equal_func)
```

来创建一个新的哈希表，返回结果为 `GHashTable`。这两个参数是函数。第一个是哈希函数，类型为 `GHashFunc`。紧接着是一个相等性测试函数（类型为 `GEqualFunc`），用于判断两个键是否相等。虽然你可能可以使用内置函数，但了解以下类型也无益处：

```c
typedef guint (*GHashFunc)(gpointer key);
typedef gboolean (*GEqualFunc)(gpointer a, gpointer b);
```

*(注：原文后续部分似乎存在大量重复或乱码文本，此处已根据要求对可读的逻辑部分进行了翻译。)*

# GNOME 开发者官方指南

GLib 函数接受两个指针地址作为第三和第四参数：一个用于键 `key`，另一个用于值 `value`。如果给定的键 `key` 在哈希表中，该函数将设置哈希表内部指向键和值的指针。成功后返回 `TRUE`。

当你需要手动分配键和值时，此函数非常有用。

警告：`g_hash_table_lookup_extended()` 让你能够直接访问表条目中的键，这意味着你也有能力更改它们。这是一个非常糟糕的主意；你可能会冒风险导致条目无法访问或出现重复。

### 删除条目

要删除哈希表中的条目，请使用：

```c
g_hash_table_remove(table, key)
```

其中 `table` 是哈希表，`key` 是条目的键。执行成功后，该函数返回 `TRUE`；如果你在创建哈希表时使用了自动释放键和值的函数，它将释放键和值的内存。此过程不会尝试释放 `deallocate` 你作为参数传递的键，因此你可以编写带有常量的语句，例如：

```c
g_hash_table_remove(hash2, *this);
```

你可以通过以下方式防止 GLib 哈希表释放键和值：

```c
g_hash_table_steal(table, key)
```

### 遍历哈希表

你可以对哈希表中的每一个条目调用函数，就像对列表、数组和树操作一样。有三种遍历方式：

- `g_hash_table_foreach(GHashTable *table, GHFunc func, gpointer user_data)`

    - 在表中的每个条目上运行 `func`。该函数将 `user_data` 作为第三参数传递给 `func`。

- `g_hash_table_foreach_remove(GHashTable *table, GHFunc func, gpointer user_data)`

    - 与前面的函数相同，但如果 `func` 返回 `TRUE`，则删除该条目。这种方法包括在你创建哈希表时指定的在键和值上运行任何释放函数。当你需要过滤哈希表时，此函数非常有用。

- `g_hash_table_foreach_steal(GHashTable *table, GHFunc func, gpointer user_data)`

    - 与前面的函数相同，但在删除条目时，该函数不会尝试释放键和数据。此函数适用于将条目移动到其他哈希表或数据结构。

以下是 `GHFunc` 的类型定义：

```c
typedef void (*GHFunc)(gpointer key, gpointer value, gpointer user_data);
```

下面是一个短示例。如果你需要查看涉及 `user_data` 参数的内容，请查看 1.5.4 节中的示例。

### 1.5.6 创建哈希表

```c
void print_entry(gpointer data, gpointer user_data)
{ /* user_data not used */
    g_print("key: %10s value: %10s\n",
           (gchar *)key, (gchar *)data);
}

g_print("*Hash table entries:\n");
gash_table_foreach(hash2, print_entry, NULL);
```

删除哈希表

要完全移除一个 `GHashTable`，

```c
g_hash_table_destroy(hash_table);
```

如果在创建哈希表时提供了释放函数，则此方法包含了键和值数据。否则，你必须自己处理每个条目中的键值；`gash_table_foreach(hash2)` 是实现此操作的方法。

> [13] 这使得 GLib 哈希表与许多解释型语言的哈希表（或字典）区别开；后者通常只允许字符串作为键。

## 1.6 其他主题

GLib 有许多功能在这里没有涵盖，因为空间不足。这些包括：

- **动态模块加载器**：`GModule` 是一个将共享对象加载到运行进程中的系统。如果你想让程序支持插件，请查看此内容。

如你所见，GLib 是一个强大的工具，无法在这样的书中进行完全记录。然而，经验丰富的程序员可以通过翻阅 GLib 附带的详尽 API 参考文档，轻松掌握如何使用其他所有功能。

# 第 2 章：GObject

## 概述

与你听到的传言相反，GNOME 与其他现代 GUI 平台一样面向对象。GNOME 与其“竞争对手”之间的主要区别在于 GNOME 库源码使用纯 C 语言编写，因此你也可以用 C 语言编程。`GTK+` 和 GNOME 等库建立在 `GObject` 对象系统之上。相比之下，其他系统依赖于编程语言的面向对象特性，例如 KDE 的 C++ 实现。

注意：本章内容枯燥且密集；在较小的空间内涵盖了几个复杂主题。本章是书中的第二部分，因为它反映了整个 GNOME API 的各个方面。你不需要理解这些内容就可以进入后续章节，特别是因为许多技术贯穿全书。至少要学习如何创建对象、操纵属性以及安装处理器（第 2.5 节、2.5.1 节和 2.6.5 节）。你不需要知道如何创建自己的类。

## 2.1 面向对象编程

由于对象属于一个类，它有一个类型。这有时被称为成员关系；一个对象可能属于 `Flipper` 类，因为你用 `Flipper` 构造函数创建了它，因此类和对象之间存在成员关系。

# GNOME 2 开发者官方指南

`CDROM` 是 `CD` 的子类。它们从其父类（或超类）继承属性，并添加一些自身的属性。整个系统被称为继承。

子类也从其父类继承方法。`CD` 类中的所有方法适用于 `AudioCD` 和 `CDROM` 对象；`CD` 方法无法关心对象的具体子类成员身份。

你可以创建子类的子类。例如，`CDROM` 可以有一个包含程序的 `SoftwareCD` 子类（`CD` 的子类），以及一个用于归档文档的 `RecordsCD` 子类。这些子类将从 `CDROM` 继承其继承的属性和方法，并添加自己的属性。如果你有一个名为 `my_disc` 的 `RecordsCD` 对象，它的成员关系将如下：

- `my_disc` 是一个 `RecordsCD` 对象。
- `my_disc` 是一个 `CDROM` 对象。
- `my_disc` 是一个 `CD` 对象。

图 2.1 显示了整个类层次结构（树状图）。

![](img/ae44ff3edd9313fce71c50baa18b0c66_67_0.png)

图 2.1: `CD` 类层次结构。

- `my_disc` 是一个 `RecordsCD` 对象。

如果你在 `GObject` 中实现 `RecordsCD`，那么图 2.1 并不是全部。`GObject` 系统有一个基类叫做 `GObject`。因此，你拥有以下成员关系：

- `my_disc` 是一个 `CDROM` 对象。
- `my_disc` 是一个 `CD` 对象。
- `my_disc` 是一个 `GObject` 对象。

整个树状图请参见图 2.2。

### 2.1.2 继承

# GNOME 开发者官方指南

![](img/ae44ff3edd9313fce71c50baa18b0c66_68_0.png)

图 2.2: `CD` 类层次结构

如果你的集合不包含任何奇特的 `CD` 格式，那么每个 `CD` 就是 `CD-ROM`（`CDROM` 的子类）或音频 `CD`（`AudioCD`）。`CD` 类仅用于派生子类；你不会实例化 `CD` 对象。这种类被称为抽象类。抽象类的一些现实中的例子是“建筑”、“车辆”和“艺术品”。没有任何东西仅仅是艺术品，而是绘画、装置、雕塑或任何其他。

### 接口

假设你已经完成了你的 `CD` 目录管理程序。现在你决定 `CD` 太小了，于是增加了一些磁带和唱片。作为一个有组织能力的人，你决定扩展库存系统以包含一些新类：`Media` 是一个新的抽象类，你旧的 `CD` 是它的子类，以及两个新子类：`Tape` 和 `Vinyl`。此外，这些还有它们自己的子类：`EightTrack`、`TapeStore`、`EP` 和 `LP`（具体位置请参见图 2.3）。

![](img/ae44ff3edd9313fce71c50baa18b0c66_68_1.png)

图 2.3: `Media` 层次结构。
