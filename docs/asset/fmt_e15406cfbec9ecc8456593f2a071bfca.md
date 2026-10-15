
# 第 7 章 内核风格与通用性

注意在正常编译期间，这些“错误”不会产生任何干扰，且 `__user_attribute` 被完全忽略；例如，`sparse` 是一个语法检查器，而不是编译器。`sparse` 的官方页面为 http://kernel.org/pub/linux/kernel/sparse/。可以在这里获取最新版本。如果你想尝试最新的，可以从 http://codemonkey.org/projects/git-nsnapshots/sparse/ 获取最新的开发。

在解包和解压后，可以使用以下命令编译并安装：

```
make PREFIX=/usr/local install
```

这会将二进制文件存放在 `/usr/local/bin` 中；你可以根据需要调整 `PREFIX` 的值。调用 `sparse` 非常简单。你只需要执行：在编译模块或内核时；`C=1` 值只处理特定模块；`C=2` 值处理所有文件。

## 7.6 使用 `likely(1)` 和 `unlikely(1)`

起初，列表的效率相当低且难以追踪；它们看起来像是：

```
if (test1) {

    ... 正在执行操作...

}

if (test2) {

    ... 正在执行...

}
```

第二个代码示例可能效率较低。因为编译器与处理器协同进行分支预测，如果第一个例子并不是那种最可能发生的情况总是失败，那么运行速度会更快，因为源码中更后的代码被假设为可能是错误的。

由于列表可能会让新手感到非常困惑，这些方法在代码频繁执行时变得非常有用，而且节省几个周期是非常重要的；它曾经会导致运行时结构中的调度。

从 2.96 版本开始，Linux 在 `likely()` 和 `unlikely()` 宏中添加了此类预测，这些宏在 `/usr/include/linux/linux/compiler.h` 中根据 `gcc` 宏 `build_...` 定义。当代码执行这些操作时，我们的示例将变为：

```
if (unlikely(test1)) {

    ... 正在执行操作...

}

if (unlikely(test2)) {

    ... 正在执行...

}
```

使用 `unlikely()` 宏非常相当。代码现在更容易理解，并受益于分支预测。

## 7.7 链接表

内核有大量 `goto` 语句的历史。这经常让新手感到头疼。例如，数据结构的链表在 Linux 内核以及主要的软件项目中非常常见。它们可能是双向链或单链，也可能是有头的或循环的。

例如，你可能会有类似这样的：

```
if (test1)
    goto flunk_test1;

test1_continue:

if (test2)
    goto flunk_test2;

test2_continue:
```

```
flunk_test:
    ... 正在执行操作 1
goto test1_continue

flunk_test2:
    ... 正在执行操作 2
goto test2_continue
```

在从原则上考虑直接实现此类链表时，新的方法很可能会让你的代码被拒绝。Linux 开发者标准化了一种巧妙的实现，并且它被采用到新中。

使用传统列表的一种有利方法是提供一组用于插入、移除、删除和操作链表的函数。由于数据结构性质的差异，每个函数都是不一样的。Linux 标准化的实现，无论函数是什么，链表结构都由以下部分组成：

双向链表的实现会定义一个嵌入了 `next` 和 `prev` 指针的数据结构，如下所示：

```
struct my_struct {
    struct my_struct *next, *prev;
    int val;
    char *my_data;
}
```

如果列表不是循环的，它在某一端 `next` 为 `NULL`，另一端 `prev` 为 `NULL`。如果它是自循环的，通过步进遍历列表你会回到起始元素。

各种函数和结构在 `/usr/src/include/linux/list.h` 中详细列出。基础数据结构是

```
struct list_head {
    list_head *next, *prev;
}
```

并且链表中的每个方法都可以用于开始遍历；因此有了 `list_head` 这个不寻的名字。要使用此功能，你需要将 `list_head` 结构放置在你正在编写的结构内部。例如：

```
struct my_struct {
    list_head list_head;
    int val;
    char *my_data;
}
```

```
struct my_struct *me = kmalloc(sizeof(struct my_struct), GFP_KERNEL);
me->val = 0;
me->my_data = NULL;
INIT_LIST_HEAD(&me->list_head);
```

```
struct list_head my_list;
INIT_LIST_HEAD(&my_list);
```

涉及双向链表的主要函数（宏）包括：

```
void list_add(struct list_head *new, struct list_head *head)
void list_add_tail(struct list_head *new, struct list_head *head)
void list_del(struct list_head *entry)
void list_splice(struct list_head *list, struct list_head *head, struct list_head *next);
```

`list_add()` 将元素插入到第二个参数所指向的第一个参数之后：  
`list_add_tail()` 将元素插入到第一个参数所在的链表末尾：  
`list_del()` 从链表中移除元素。必须释放与该数据结构相关的任何内存。  
`list_empty()` 检查列表是否为空。  
`list_splice()` 将两个列表合并，其中第一个参数指向新列表，第二个列表指向另一个列表。

使用以下宏来处理链表：

`list_entry()` 返回指向第二个参数中指示类型的结构指针，该结构来自第一个参数指向的 `list_head` 所在的列表，以及我们在结构中定义的该结构中的哪个成员。  
`list_for_each()` 通过其第二个参数遍历列表，性能。  
`list_for_each_prev()` 反向遍历列表。  
`list_for_each_safe()` 处理在删除元素时的情况。  
`list_entry()` 宏非常方便。

## 7.8 编写可移植代码

一个优势是使用了经过良好测试、安全的函数，这些函数通用并适用于所有架构，并在其基础上进行了精炼、增强和改进。
