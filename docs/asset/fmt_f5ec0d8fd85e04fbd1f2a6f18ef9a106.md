
### list_add

- `new`: 要添加的新条目
- `head`: 在之后添加的链表头部

#### 描述

在指定的 `head` 之后插入新条目。这有助于实现栈。

### list_add_tail

#### 名称

`list_add_tail` — 添加新条目

#### 概要

```
void list_add_tail (struct list_head * new, struct list_head * head);
```

#### 参数

- `new`: 要添加的新条目
- `head`: 在其之前添加的链表头部

#### 描述

在指定的 `head` 之前插入新条目。这有助于实现队列。

### list_del

#### 名称

`list_del` — 从链表中删除条目。

#### 概要

```
void list_del (struct list_head * entry);
```

#### 参数

- `entry`: 要从链表中删除的元素。

#### 注意

在此之后对 `entry` 执行 `list_empty` 不返回 true，该条目处于未定义状态。

### list_del_init

#### 名称

`list_del_init` — 从链表中删除条目并重新初始化。

#### 概要

```
void list_del_init (struct list_head * entry);
```

#### 参数

- `entry`: 要从链表中删除的元素。

### list_empty

#### 名称

`list_empty` — 测试链表是否为空

#### 概要

```
int list_empty (struct list_head * head);
```

#### 参数

- `head`: 要测试的链表。

### list_splice

#### 名称

`list_splice` — 合并两个链表

#### 概要

```
void list_splice (struct list_head * list, struct list_head * head);
```

#### 参数

- `list`: 要添加的新链表。
- `head`: 在第一个链表中添加它的位置。

### list_entry

#### 名称

`list_entry` — 获取该条目的结构体

#### 概要

```
list_entry ( ptr, type, member);
```

#### 参数

- `ptr`: `&struct list_head` 指针。
- `type`: 嵌入其中的结构体类型。
- `member`: 结构体内链表结构体的成员名称。

### list_for_each

#### 名称

`list_for_each` — 遍历链表

#### 概要

```
list_for_each ( pos, head);
```

#### 参数

- `pos`: 用作循环计数器的 `&struct list_head`。
- `head`: 链表的头部。

### list_for_each_safe

#### 名称

`list_for_each_safe` — 遍历链表，防止删除链表条目安全

#### 概要

```
list_for_each_safe ( pos, n, head);
```

#### 参数

- `pos`: 用作循环计数器的 `&struct list_head`。
- `n`: 另一个用于临时存储的 `&struct list_head`
- `head`: 链表的头部。

# 第 3 章基础 C 库函数

在编写驱动程序时，通常无法使用来自 C 库的例程。某些函数被证明是通用的，列如下。这些函数的行为可能与 ANSI 定义的略有不同，这些偏差在文中会有。

## 3.1. 字符串转换

### simple_strtol

#### 名称

`simple_strtol` — 将字符串转换为带符号的长型 `long`

#### 概要

```
long simple_strtol (const char * cp, char ** endp, unsigned int base);
```

#### 参数

- `cp`: 字符串起始
- `endp`: 将存储解析后字符串结束处的指针
- `base`: 使用的数字进制

### simple_strtoll

#### 名称

`simple_strtoll` — 将字符串转换为带符号的长型 `long long`

#### 概要

```
long long simple_strtoll (const char * cp, char ** endp, unsigned int base);
```

#### 参数

- `cp`: 字符串起始
- `endp`: 将存储解析后字符串结束处的指针
- `base`: 使用的数字进制

### simple_strtoul

#### 名称

`simple_strtoul` — 将字符串转换为无符号的长型 `unsigned long`

#### 概要

```
unsigned long simple_strtoul (const char * cp, char ** endp, unsigned int base);
```

#### 参数

- `cp`: 字符串起始
- `endp`: 将存储解析后字符串结束处的指针
- `base`: 使用的数字进制

### simple_strtoull

#### 名称

`simple_strtoull` — 将字符串转换为无符号的长型 `unsigned long long`

#### 概要

```
unsigned long long simple_strtoull(const char * cp, char ** endp, unsigned int base);
```

#### 参数

- `cp`: 字符串起始
- `endp`: 将存储解析后字符串结束处的指针
- `base`: 使用的数字进制

### vsnprintf

#### 名称

`vsnprintf` — 格式化字符串并放入缓冲区

#### 概要

```
int vsnprintf(char * buf, size_t size, const char * fmt, va_list args);
```

#### 参数

- `buf`: 缓冲区
- `size`: 大小
- `fmt`: 格式字符串
- `args`: 参数列表

#### 描述

- `buf`: 结果所在的缓冲区
- `size`: 缓冲区的大小
- `fmt`: 格式字符串
- `args`: 参数列表

### snprintf

#### 名称

`snprintf` — 格式化字符串并放入缓冲区

#### 概要

```
int snprintf(char * buf, size_t size, const char * fmt, ...);
```

#### 参数

- `buf`: 结果所在的缓冲区
- `size`: 缓冲区的大小
- `fmt`: 格式字符串
- `...`: 参数

### vsprintf

#### 名称

`vsprintf` — 格式化字符串并放入缓冲区

#### 概要

```
int vsprintf(char * buf, const char * fmt, va_list args);
```

#### 参数

- `buf`: 结果所在的缓冲区
- `fmt`: 格式字符串
- `args`: 参数列表

### sprintf

#### 名称

`sprintf` — 格式化字符串并放入缓冲区

#### 概要

```
int sprintf(char * buf, const char * fmt, ...);
```

#### 参数

- `buf`: 结果所在的缓冲区
- `fmt`: 格式字符串
- `...`: 参数

## 3.2. 字符串操作

### strcpy

#### 名称

`strcpy` — 复制终止字符串

#### 概要

```
char * strcpy (char * dest, const char * src);
```

#### 参数

- `dest`: 复制的目标位置
- `src`: 源字符串

### strncpy

#### 名称

`strncpy` — 复制长度限制的终止字符串

#### 概要

```
char * strncpy(char * dest, char * src, size_t count);
```

#### 参数

- `dest`: 复制的目标位置
- `src`: 源字符串
- `count`: 最大复制字节数

#### 描述

注意，与用户态的 `strncpy` 不同，这不会对缓冲区进行空填充。然而，如果源超过 `count` 字节，则结果是不终止的。

### strcat

#### 名称

`strcat` — 将一个终止字符串附加到另一个

#### 概要

```
char * strcat (char * dest, const char * src);
```

#### 参数

- `dest`: 要追加的字符串
- `src`: 要追加的字符串

### strncat

#### 名称
