# Linux Kernel API 入门指南





















































devfs_unregister_blkdev......................................................285













- z8530_channel_load................................................................................................339









## 第 1 章 驱动基础

### 1.1. 驱动入口与退出点

#### module_init

#### 名称
module_init — 驱动初始化入口点

#### 概要
```
module_init ( x );
```

#### 参数
x
在内核启动时或插入模块时运行的函数

#### 描述
如果驱动被检查为“y”或静态，module_init 将将驱动初始化例程序添加到“__initcall.int”段中；否则，它将驱动初始化例程序封装在 init_module 中，当驱动作为模块使用时，insmod 和 modprobe 会使用该函数。

#### module_exit

#### 名称
module_exit — 驱动退出入口点

#### 概要
```
module_exit ( x );
```

#### 参数
x
在驱动被移除时运行的函数

#### 描述
当驱动作为模块且配合 rmod 使用时，module_exit 将驱动清理代码封装在 cleanup_module 中。如果驱动被静态编译到内核中，module_exit 则不起任何作用。

### 1.2. 原子操作与指针操作

#### atomic_read

#### 名称
atomic_read — 读取原子变量

#### 概要
```
atomic_read ( v );
```

#### 参数
v
类型为 atomic_t 的指针

#### 描述
原子化地读取 v 的值。请注意，atomic_t 能够保证的有效范围仅为 24 位。

#### atomic_set

#### 名称
atomic_set — 设置原子变量

#### 概要
```
atomic_set ( v, i);
```

#### 参数
- * v
类型为 atomic_t 的指针
- i
所需的值

#### 描述
原子化地将 v 的设置为 i。请注意，atomic_t 能够保证的有效范围仅为 24 位。

#### atomic_add

#### 名称
atomic_add — 向原子变量相加整数

#### 概要
```
void atomic_add (int i, atomic_t * v);
```

#### 参数
- * i
要加的整数值
- * v
类型为 atomic_t 的指针

#### 描述
原子化地将 i 加到 v。请注意，atomic_t 能够保证的有效范围仅为 24 位。

#### atomic_sub

#### 名称
atomic_sub — 减去原子变量

#### 概要
```
void atomic_sub (int i, atomic_t * v);
```

#### 参数
- * i
要减的整数值
- * v
类型为 atomic_t 的指针

#### 描述
原子化地从 v 中减去 i。请注意，atomic_t 能够保证的有效范围仅为 24 位。

#### atomic_sub_and_test

#### 名称
atomic_sub_and_test — 从变量中减去值并测试结果

#### 概要
```
int atomic_sub_and_test (int i, atomic_t * v);
```

#### 参数
- * i
要减的整数值
- * v
类型为 atomic_t 的指针

#### 描述
原子化地从 v 中减去 i，如果结果为零则返回真，其他所有情况均返回假。请注意，atomic_t 能够保证的有效范围仅为 24 位。

#### atomic_inc

#### 名称
atomic_inc — 原子变量自增

#### 概要
```
void atomic_inc (atomic_t * v);
```

#### 参数
v
类型为 atomic_t 的指针

#### 描述
原子化地将 v 增 1。请注意，atomic_t 能够保证的有效范围仅为 24 位。

#### atomic_dec

#### 名称
atomic_dec — 原子变量自减

#### 概要
```
void atomic_dec (atomic_t * v);
```

#### 参数
- v
类型为 atomic_t 的指针

#### 描述
原子化地将 v 减 1。请注意，atomic_t 能够保证的有效范围仅为 24 位。

#### atomic_dec_and_test

#### 名称
atomic_dec_and_test — 从变量中减去值并测试结果

#### 概要
```
int atomic_dec_and_test (atomic_t * v);
```

#### 参数
v
类型为 atomic_t 的指针

#### 描述
原子化地将 v 减 1，如果结果为零则返回真（此处应为：如果结果为零则返回真，其他所有情况均返回假）。请注意，atomic_t 能够保证的有效范围仅为 24 位。

#### atomic_inc_and_test

#### 名称
atomic_inc_and_test — 原子变量自增并测试

#### 概要
```
int atomic_inc_and_test (atomic_t * v);
```

#### 参数
v
类型为 atomic_t 的指针

#### 描述
原子化地将 v 增 1，如果结果为零则返回真，其他所有情况均返回假。

#### atomic_add_negative

#### 名称
atomic_add_negative — 相加并测试为负

#### 概要
```
int atomic_add_negative (int i, atomic_t * v);
```

#### 参数
- * i
要加的整数值
- * v
类型为 atomic_t 的指针

#### 描述
原子化地将 i 加到 v，如果结果为负则返回真，结果大于等于零时返回假。请注意，atomic_t 能够保证的有效范围仅为 24 位。

#### get_unaligned

#### 名称
get_unaligned — 从未对齐位置获取值

#### 概要
```
get_unaligned ( ptr );
```

#### 参数
ptr
值指针

#### 描述
该宏应用于访问比字节大的未对齐值，例如从未按 u16 对齐的位置获取 u16 值。在某些架构上，未对齐访问的开销很大。

#### put_unaligned

#### 名称
put_unaligned — 将值放入可能未对齐的位置

#### 概要
```
put_unaligned ( val, ptr);
```

#### 参数
val
要存放的值
ptr
位置指针

#### 描述
该宏应用于将比字节大的值存放在预期的未对齐位置，例如向未按 u16 对齐的位置写入 u16 值。在某些架构上，未对齐访问的开销很大。

### 1.3. 延迟、调度和定时器例程

#### schedule_timeout

#### 名称
schedule_timeout — 等待超时

#### 概要
```
signed long schedule_timeout (signed long timeout);
```

#### 参数
超时以 jiffies 为单位的超时时间

#### 描述
让当前任务睡眠直到通过指定的 jiffies 时间。除非设置了当前任务状态（见 set_current_state），否则该函数将立即返回。

你可以如下设置任务状态：

- TASK_UNINTERRUPTIBLE 保证在函数返回之前至少经过了 timeout jiffies。函数返回 0。
- TASK_INTERRUPTIBLE 如果向当前任务递送信号，函数可能会提前返回。在这种情况下，返回剩余的 jiffies 时间，如果定时器到期则返回 0。

当该函数返回时，保证当前任务状态为 TASK_RUNNING。





指定 `timeout` 值为 `MAX_SCHEDULE_TIMEOUT` 将调度 CPU 离开且没有超时限制。在这种情况下，返回值将为 `MAX_SCHEDULE_TIMEOUT`。

在所有情况下，返回值保证为非负数。

## 第 2 章数据类型

### 2.1. 双向链表

#### list_add

#### 名称
list_add — 添加新条目

#### 概要
```
void list_add (struct list_head * new, struct list_head * head);
```

#### 参数
- * new: 要添加的新条目
- head: 在之后添加的链表头部

#### 描述
在指定的 head 之后插入新条目。这有助于实现栈。

#### list_add_tail

#### 名称
list_add_tail — 添加新条目

#### 概要
```
void list_add_tail (struct list_head * new, struct list_head * head);
```

#### 参数
- new: 要添加的新条目
- head: 在其之前添加的链表头部

#### 描述
在指定的 head 之前插入新条目。这有助于实现队列。

#### list_del

#### 名称
list_del — 从链表中删除条目。

#### 概要
```
void list_del (struct list_head * entry);
```

#### 参数
- entry: 要从链表中删除的元素。

#### 注意
在此之后对 entry 执行 `list_empty` 不返回 true，该条目处于未定义状态。

#### list_del_init

#### 名称
list_del_init — 从链表中删除条目并重新初始化。

#### 概要
```
void list_del_init (struct list_head * entry);
```

#### 参数
- entry: 要从链表中删除的元素。

#### list_empty

#### 名称
list_empty — 测试链表是否为空

#### 概要
```
int list_empty (struct list_head * head);
```

#### 参数
- head: 要测试的链表。

#### list_splice

#### 名称
list_splice — 合并两个链表

#### 概要
```
void list_splice (struct list_head * list, struct list_head * head);
```

#### 参数
- list: 要添加的新链表。
- head: 在第一个链表中添加它的位置。

#### list_entry

#### 名称
list_entry — 获取该条目的结构体

#### 概要
```
list_entry ( ptr, type, member);
```

#### 参数
- * ptr: &struct list_head 指针。
- type: 嵌入其中的结构体类型。
- member: 结构体内链表结构体的成员名称。

#### list_for_each

#### 名称
list_for_each — 遍历链表

#### 概要
```
list_for_each ( pos, head);
```

#### 参数
- pos: 用作循环计数器的 &struct list_head。
- head: 链表的头部。

#### list_for_each_safe

#### 名称
list_for_each_safe — 遍历链表，防止删除链表条目安全

#### 概要
```
list_for_each_safe ( pos, n, head);
```

#### 参数
- pos: 用作循环计数器的 &struct list_head。
- n: 另一个用于临时存储的 &struct list_head
- head: 链表的头部。

## 第 3 章基础 C 库函数

在编写驱动程序时，通常无法使用来自 C 库的例程。某些函数被证明是通用的，列如下。这些函数的行为可能与 ANSI 定义的略有不同，这些偏差在文中会有。

### 3.1. 字符串转换

#### simple_strtol

#### 名称
simple_strtol — 将字符串转换为带符号的长型 (long)

#### 概要
```
long simple_strtol (const char * cp, char ** endp, unsigned int base);
```

#### 参数
- cp: 字符串起始
- endp: 将存储解析后字符串结束处的指针
- base: 使用的数字进制

#### simple_strtoll

#### 名称
simple_strtoll — 将字符串转换为带符号的长型 (long long)

#### 概要
```
long long simple_strtoll (const char * cp, char ** endp, unsigned int base);
```

#### 参数
- cp: 字符串起始
- endp: 将存储解析后字符串结束处的指针
- base: 使用的数字进制

#### simple_strtoul

#### 名称
simple_strtoul — 将字符串转换为无符号的长型 (unsigned long)

#### 概要
```
unsigned long simple_strtoul (const char * cp, char ** endp, unsigned int base);
```

#### 参数
- cp: 字符串起始
- endp: 将存储解析后字符串结束处的指针
- base: 使用的数字进制

#### simple_strtoull

#### 名称
simple_strtoull — 将字符串转换为无符号的长型 (unsigned long long)

#### 概要
```
unsigned long long simple_strtoull(const char * cp, char ** endp, unsigned int base);
```

#### 参数
- cp: 字符串起始
- endp: 将存储解析后字符串结束处的指针
- base: 使用的数字进制

#### vsprintf

#### 名称
vsnprintf — 格式化字符串并放入缓冲区

#### 概要
```
int vsnprintf(char * buf, size_t size, const char * fmt, va_list args);
```

#### 参数
- buf: 缓冲区
- size: 大小
- fmt: 格式字符串
- args: 参数列表

#### 描述
- buf: 结果所在的缓冲区
- size: 缓冲区的大小
- fmt: 格式字符串
- args: 参数列表

#### snprintf

#### 名称
snprintf — 格式化字符串并放入缓冲区

#### 概要
```
int snprintf(char * buf, size_t size, const char * fmt, ...);
```

#### 参数
- buf: 结果所在的缓冲区
- size: 缓冲区的大小
- fmt: 格式字符串
- ...: 参数

#### vsprintf

#### 名称
vsprintf — 格式化字符串并放入缓冲区

#### 概要
```
int vsprintf(char * buf, const char * fmt, va_list args);
```

#### 参数
- buf: 结果所在的缓冲区
- fmt: 格式字符串
- args: 参数列表

#### sprintf

#### 名称
sprintf — 格式化字符串并放入缓冲区

#### 概要
```
int sprintf(char * buf, const char * fmt, ...);
```

#### 参数
- buf: 结果所在的缓冲区
- fmt: 格式字符串
- ...: 参数

### 3.2. 字符串操作

#### strcpy

#### 名称
strcpy — 复制终止字符串

#### 概要
```
char * strcpy (char * dest, const char * src);
```

#### 参数
- dest: 复制的目标位置
- src: 源字符串

#### strncpy

#### 名称
strncpy — 复制长度限制的终止字符串

#### 概要
```
char * strncpy(char * dest, char * src, size_t count);
```

#### 参数
- dest: 复制的目标位置
- src: 源字符串
- count: 最大复制字节数

#### 描述
注意，与用户态的 strncpy 不同，这不会对缓冲区进行空填充。然而，如果源超过 count 字节，则结果是不终止的。

#### strcat

#### 名称
strcat — 将一个终止字符串附加到另一个

#### 概要
```
char * strcat (char * dest, const char * src);
```

#### 参数
- dest: 要追加的字符串
- src: 要追加的字符串

#### strncat

#### 名称
strncat — 将长度限制的终止字符串附加到另一个

#### 概要
```
char * strncat (char * dest, char * src, size_t count);
```

#### 参数
- dest: 要追加的字符串
- src: 要追加的字符串
- count: 最大追加字节数

#### 描述
注意，与 strncpy 相比，strcat 确保结果是终止的。

#### strcmp

#### 名称
strcmp — 比较两个字符串

#### 概要
```
int strcmp (const char * cs, const char * ct);
```

#### 参数
- cs: 一个字符串
- ct: 另一个字符串

#### strncmp

#### 名称
strncmp — 比较两个长度限制的字符串

#### 概要
```
int strncmp (const char * cs, const char * ct, size_t count);
```

#### 参数
- cs: 一个字符串
- ct: 另一个字符串
- count: 最大比较字节数

#### strchr

#### 名称
strchr — 在字符串中查找第一次出现的字符

#### 概要
```
char * strchr (const char * s, int c);
```

#### 参数
- s: 要搜索的字符串
- c: 要查找的字符

#### strrchr

#### 名称
strrchr — 在字符串中查找最后一次字符




#### 概要

```
char * strrchr (const char * s, int c);
```

#### 参数

s

要查找的字符串

c

要查找的字符

#### strlen

#### 名称

strlen — 查找字符串的长度

#### 概要

```
size_t strlen (const char * s);
```

#### 参数

s

需要计算大小的字符串

#### strnlen

#### 名称

strnlen — 查找长度限制字符串的长度

#### 概要

```
size_t strnlen(const char * s, size_t count);
```

#### 参数

s

需要计算大小的字符串

count

要查找的最大字节数

#### strpbrk

#### 名称

strpbrk — 查找字符集中第一个字符出现的位置

#### 概要

```
char * strpbrk (const char * cs, const char * ct);
```

#### 参数

cs

要查找的字符串

ct

要查找的字符

#### strtok

#### 名称

strtok — 将字符串分割为标记

#### 概要

```
char * strtok (char * s, const char * ct);
```

#### 参数

s

要查找的字符串

ct

要查找的字符

## 警告

strtok 已废弃，请使用 strcat。

#### memset

#### 名称

memset — 用给定的值填充内存区域

#### 概要

```
void * memset(void * s, int c, size_t count);
```

#### 参数

s

区域起始位置的指针

c

填充区域的字节值

count

区域的大小

#### 描述

不要使用 memset 访问 IO 空间，请使用 memset_io。

#### bcopy

#### 名称

bcopy — 将一个内存区域复制到另一个内存区域

#### 概要

```
char * bcopy (const char * src, char * dest, int count);
```

#### 参数

src

复制源

dest

复制目标

count

区域的大小

#### 描述

注意，这与 memcpy 相同，但参数顺序反相反。memcpy 是标准函数，bcopy 是一个遗留的 BSD 函数。

你不应该使用此函数访问 IO 空间，请使用 memcpy_toio 或 memcpy_fromio。

#### memcpy

#### 名称

memcpy — 将一个内存区域复制到另一个内存区域

#### 概要

```
void * memcpy (void * dest, const void * src, size_t count);
```

#### 参数

dest

复制目标

src

复制源

count

区域的大小

#### 描述

你不应该使用此函数访问 IO 空间，请使用 memcpy_toio 或 memcpy_fromio。

与 memcpy 不同，memmove 可以处理重叠区域。

#### memcmp

#### 名称

memcmp — 比较两个内存区域

#### 概要

```
int memcmp (const void * cs, const void * ct, size_t count);
```

#### 参数

cs

一个内存区域

ct

另一个内存区域

count

区域的大小

#### memscan

#### 名称

memscan — 在内存区域中查找字符。

#### 概要

```
void * memscan (void * addr, int c, size_t size);
```

#### 参数

addr

内存区域

c

要查找的字节

size

区域的大小

#### 描述

返回 c 第一次出现的位置地址；如果未找到 c，则返回该区域后 1 字节处的地址。

#### strstr

#### 名称

strstr — 在 NUL 终止字符串中查找第一个子串

#### 概要

```
char * strstr (const char * s1, const char * s2);
```

#### 参数

s1

要查找的字符串

s2

要查找的字符串

#### memchr

#### 名称

memchr — 在内存区域中查找字符。

#### 概要

```
void * memchr (const void * s, int c, size_t n);
```

#### 参数

s

内存区域

c

要查找的字节

n

区域的大小

#### 描述

返回 c 第一次出现的位置地址；如果未找到 c，则返回 NULL。

### 3.3. 位操作

#### set_bit

#### 名称

set_bit — 原子性地设置内存中的一个位

#### 概要

```
void set_bit (int nr, volatile void * addr);
```

#### 参数

nr

要设置的位

addr

开始计数的地址

#### 描述

此函数是原子的，且可能不会被重排。如果你不需要原子保证，请参见 `__set_bit`。注意 nr 可以可以是任意大的；此函数不限制于操作单个字长度的量。

#### __set_bit

#### 名称

__set_bit — 设置内存中的一个位

#### 概要

```
void __set_bit(int nr, volatile void * addr);
```

#### 参数

- nr
要设置的位
- addr
开始计数的地址

#### 描述

与 set_bit 不同，此函数是非原子的，且可能被重排。如果同时在同一内存区域上调用它，结果可能只有一次操作成功。

#### clear_bit

#### 名称

clear_bit — 清除内存中的一个位

#### 概要

```
void clear_bit (int nr, volatile void * addr);
```

#### 参数

- nr
要设置的位（此处清除）
- addr
开始计数的地址

#### 描述

此函数是原子的，且可能被重排。如果你不需要原子保证，请参见 `__set_bit`。注意 nr 可以是任意大的；此函数不限制于操作单个字长度的量。

#### __clear_bit

#### 名称

__clear_bit — 清除内存中的一个位

#### 概要

```
void __clear_bit(int nr, volatile void * addr);
```

#### 参数

- nr
要设置的位（清除）
- addr
开始计数的地址

#### 描述

与 set_bit 不同，此函数是非原子的，且可能被重排。如果同时在同一内存区域上调用它，结果可能只有一次操作成功。

#### change_bit

#### 名称

change_bit — 翻转内存中的一个位

#### 概要

```
void change_bit (int nr, volatile void * addr);
```

#### 参数

- nr
要设置的位（翻转）
- addr
开始计数的地址

#### 描述

等等，文本写着：此函数是原子的，且可能不会被重排。如果你不需要原子保证，请参见 `__set_bit`。注意 nr 可以是任意大的；此函数不限制于操作单个字长度的量。实际上，此函数是非原子的，且可能被重排。如果同时在同一内存区域上调用它，结果可能只有一次操作成功。

（注：由于提供的 OCR 文本存在重复和乱码，已根据逻辑进行了清理和翻译。）




#### 概要

```c
int find_next_zero_bit (void * addr, int size, int offset);
```

#### 参数

addr
用于搜索的基地址

size
搜索的最大大小

offset
开始搜索的位偏移

#### ffz

#### 名称

ffz — 找到字中的第一个零位

#### 概要

```c
unsigned long ffz (unsigned long word);
```

#### 参数

word
要搜索的字

#### 描述

如果不存在零位则结果未定义，因此代码应先检查 `~UL`。

#### ffs

#### 名称

- ffs — 找到第一个置1位

#### 概要

```c
int ffs (int x);
```

#### 参数

x
要搜索的字

#### 描述

其定义方式与 libc 和编译器内置的 ffs 例程相同，因此在设计意图上与上述 ffz（man ffs）有所不同。

#### hweight32

#### 名称

hweight32 — 返回 N 位字的汉明重量（Hamming weight）

#### 概要

```c
hweight32 ( x );
```

#### 参数

x
要计算重量的字

#### 描述

一个数字的汉明重量是其中置1的位的总数。

## 第 4 章 Linux 内存管理

### 4.1. Slab 缓存

#### kmem_cache_create

名称

kmem_cache_create — 创建一个缓存

概要

参数

name
一个字符串，用于在 `/proc/slabinfo` 中标识此缓存。

size
在此缓存中创建的对象的大小。

offset
页内使用的偏移量。

flags
SLAB标志位

ctor
对象的构造函数。

dtor
对象的析构函数。

#### 描述

成功时返回缓存指针，失败时返回 NULL。该函数不能在原子上下文上下文中调用，但可以被中断。当缓存分配新页时运行 `ctor`，在页面归还之前运行 `dtor`。标志位如下：

- SLAB_POISON - 使用已知的测试模式（a5a5a5a5）对 slab 进行毒化，以捕获对未初始化内存的引用。
- SLAB_RED_ZONE - 在分配的内存周围插入“红色”区域以检查缓冲区溢出。
- SLAB_NO_REAP - 在内存压力下不收回此缓存。
- SLAB_HWCACHE_ALIGN - 将此缓存中的对象对齐到硬件缓存行。如果你需要像 dave 那样精确地计算周期，这将是有益的。

#### kmem_cache_shrink

#### 名称

kmem_cache_shrink — 收缩缓存

#### 概要

```c
int kmem_cache_shrink (kmem_cache_t * cachep);
```

#### 参数

cachep
要收缩的缓存。

#### 描述

为缓存尽可能释放 slab。为了方便调试，退出状态为0 表示所有 slab 都已释放。

#### kmem_cache_destroy

#### 名称

kmem_cache_destroy — 删除缓存

#### 概要

```c
int kmem_cache_destroy (kmem_cache_t * cachep);
```

#### 参数

cachep
要删除的缓存

#### 描述

从 slab 缓存中移除 `kmem_cache_t` 对象。成功时返回 0。

预计该函数会在模块卸载时由模块调用。这将完全移除缓存，并避免在模块加载和卸载时重复分配缓存（如果该模块在加载和卸载之间没有持久的内核态存储）。

调用者必须保证在 `kmem_cache_destroy` 执行期间没有从该缓存中分配内存。

#### kmem_cache_alloc

#### 名称

kmem_cache_alloc — 分配对象

#### 概要

```c
void * kmem_cache_alloc (kmem_cache_t * cachep, int flags);
```

#### 参数

cachep
从中分配内存的缓存。

flags
见 `kmalloc`。

#### 描述

从此缓存中分配一个对象。仅当缓存有可用对象时，`flags` 才有效。

#### kmalloc

#### 名称

kmalloc — 分配内存

#### 概要

```c
void * kmalloc (size_t size, int flags);
```

#### 参数

size
所需的字节数。

## 第 4 章 Linux 内存管理

flags
要分配的内存类型。

#### 描述

`kmalloc` 是内核中分配内存的标准方法。

`flags` 参数可能是之一：

- GFP_USER - 代表用户分配内存。可能会睡眠。
- GFP_KERNEL - 分配普通内核内存。可能会睡眠。
- GFP_ATOMIC - 分配不会睡眠。在中断处理程序内部使用。

此外，可能会设置 `GFP_DMA` 标志表示内存必须适合 DMA。这在不同平台上有不同的含义。例如，在 i386 上，这意味着内存必须来自前 16MB 区域。

#### kmem_cache_free

#### 名称

kmem_cache_free — 释放对象

#### 概要

```c
void kmem_cache_free (kmem_cache_t * cache, void * objp);
```

#### 参数

cache
分配所属的缓存。

objp
之前分配的对象。

#### 描述

从此缓存中释放一个对象。

#### kfree

#### 名称

kfree — 释放对象

#### 概要

```c
void kfree (void * objp);
```

#### 描述

释放之前由 `kmalloc` 分配的内存。

## 第 5 章 proc 文件系统

### 5.1. sysctl 接口

#### register_sysctl

名称

register_sysctl — 注册 sysctl

概要

```c
struct ctl_table_header * register_sysctl (ctl_table * table, int insert_head);
```

参数

table
sysctl 表

insert_head
是否应在头部插入

#### 描述

注册一个 sysctl 表。`ctl_table` 的成员用法如下：

- ctl_name: sysctl 的名称
- data: 数据指针
- maxlen: 最大大小
- mode: sysctl 的权限
- handler: proc 处理例程（见下文）
- strategy: 策略例程（见下文）

该程序在注册失败时返回 NULL，成功时返回表头。

#### unregister_sysctl_table

#### 名称

unregister_sysctl_table — 取消注册 sysctl 表

#### 概要

```c
void unregister_sysctl_table (struct ctl_table_header * header);
```

#### 参数

header
register_sysctl 返回的表头

#### 描述

取消注册 sysctl 表及其所有子项。proc 条目在不再被使用之前可能不会被实际移除。

#### proc_dostring

#### 名称

proc_dostring — 读取/写入字符串 sysctl

#### 概要

```c
int proc_dostring (ctl_table * table, int write, struct file * filp, void * buffer, size_t * lenp);
```

#### 参数

table
sysctl 表

write
如果是向 sysctl 文件写入为 TRUE

filp
文件结构体

buffer
用户缓冲区

lenp
用户缓冲区的大小

#### 描述

从用户缓冲区读取/写入字符串。如果提供的内核缓冲区不够大以容纳字符串，则字符串将被截断。复制的字符串以空字符结束。




以空字符终止。如果字符串由用户进程读取，则将进行复制并添加换行符 '\n'。如果缓冲区不够大，则会被截断。

成功时返回 0。

#### proc_dointvec

#### 名称

proc_dointvec — 读取一个整数向量

#### 概要

```
int proc_dointvec (ctl_table * table, int write, struct file * filp, void * buffer, size_t * lenp);
```

#### 参数

- table
  sysctl 表
- write
  如果这是对 sysctl 文件的写操作，则为 TRUE
- filp
  文件结构
- buffer
  用户缓冲区
- lenp
  用户缓冲区的大小

#### 描述

从/向用户缓冲区读取/写入最多 `table->maxlen/sizeof(unsigned int)` 个整数值，将其视为 ASCII 字符串。

成功时返回 0。

#### proc_dointvec_minmax

#### 名称

proc_dointvec_minmax — 读取带有最小/最大值的整数向量

#### 概要

```
int proc_dointvec_minmax (ctl_table * table, int write, struct file * filp, void * buffer, size_t * lenp);
```

#### 参数

- table
  sysctl 表
- write
  如果这是对 sysctl 文件的写操作，则为 TRUE
- filp
  文件结构
- buffer
  用户缓冲区
- lenp
  用户缓冲区的大小

#### 描述

从/向用户缓冲区读取/写入最多 `table->maxlen/sizeof(unsigned int)` 个整数值，将其视为 ASCII 字符串。

此例程将确保值位于 `table->extral`（最小）和 `table->extra2`（最大）指定的范围内。

成功时返回 0。

#### proc_doulongvec_minmax

#### 名称

proc_doulongvec_minmax — 读取带有最小/最大值的长整型向量

#### 概要

```
int proc_doulongvec_minmax (ctl_table * table, int write, struct file * filp, void * buffer, size_t * lenp);
```

#### 参数

- table
  sysctl 表
- write
  如果这是对 sysctl 文件的写操作，则为 TRUE
- filp
  文件结构
- buffer
  用户缓冲区
- lenp
  用户缓冲区的大小

# 描述 

从/向用户缓冲区读取/写入最多 `table->maxlen/sizeof(unsigned long)` 个无符号长 值，将其视为 ASCII 字符串。

此例程将确保值位于 `table->extra1`（最小）和 `table->extra2`（最大）指定的范围内。

成功时返回 0。

#### proc_doulongvec_ms_jiffies_minmax

#### 名称

proc_doulongvec_ms_jiffies_minmax — 读取带有最小/最大值的毫秒值向量

#### 概要

```
int proc_doulongvec_ms_jiffies_minmax (ctl_table * table, int write, struct file * filp, void * buffer, size_t * lenp);
```

#### 参数

- table
  sysctl 表
- write
  如果这是对 sysctl 文件的写操作，则为 TRUE
- filp
  文件结构
- buffer
  用户缓冲区
- lenp
  用户缓冲区的大小

# 描述 

从/向用户缓冲区读取/写入最多 `table->maxlen/sizeof(unsigned long)` 个无符号长 值，将其视为 ASCII 字符串。这些值被视为毫秒，并在存储时转换为 jiffies。

此例程将确保值位于 `table->extral`（最小）和 `table->extra2`（最大）指定的范围内。

成功时返回 0。

#### proc_dointvec_jiffies

#### 名称

proc_dointvec_jiffies — 以秒为单位读取整数向量

#### 概要

```
int proc_dointvec_jiffies (ctl_table * table, int write, struct file * filp, void * buffer, size_t * lenp);
```

#### 参数

- table
  sysctl 表
- write
  如果这是对 sysctl 文件的写操作，则为 TRUE
- filp
  文件结构
- buffer
  用户缓冲区
- lenp
  用户缓冲区的大小

# 描述 

从/向用户缓冲区读取/写入最多 `table->maxlen/sizeof(unsigned int)` 个整数值，将其视为 ASCII 字符串。读取的值假设为秒，并被转换为 jiffies。

成功时返回 0。

## 第 6 章. Linux VFS

### 6.1. 目录缓存

#### d_invalidate

**名称**

d_invalidate — 使一个 dentry（目录项）失效

**概要**

```
int d_invalidate (struct dentry * dentry);
```

**参数**

dentry

要使失效的 dentry

**描述**

如果可行，尝试使该 dentry 失效。如果可以通过该 dentry 访问其他 dentry，则我们无法删除它并返回 -EBUSY。成功时返回 0。

不使用 dcache 锁。

#### d_find_alias

#### 名称

d_find_alias — 获取 inode 的哈希别名（alias）

#### 概要

```
struct dentry * d_find_alias (struct inode * inode);
```

**参数**

inode

要查找的 inode

**描述**

获取 inode 的哈希别名。如果找到，返回该 dentry 并增加其引用计数。否则返回 NULL。

#### prune_dcache

#### 名称

prune_dcache — 剪枝 dcache

#### 概要

```
void prune_dcache (int count);
```

**参数**

count

要剪枝的项数

**描述**

当我们需要内存时收缩 dcache。

#### shrink_dcache_sb

#### 名称

shrink_dcache_sb — 为超级块缩小 dcache

#### 概要

```
void shrink_dcache_sb (struct super *);
```

**参数**

sb

超级块

**描述**

为指定的超级块缩小 dcache。

#### have_mounts

#### 名称

have_mounts — 检查 dentry 是否为挂载点

#### 概要

```
int have_mounts (struct dentry * parent);
```

**参数**

parent

要检查的 dentry

**描述**

如果 dentry 包含挂载点，则返回真。

#### shrink_dcache_parent

#### 名称

shrink_dcache_parent — 剪枝 dcache

#### 概要

```
void shrink_dcache_parent (struct dentry * parent);
```

**参数**

parent

父级 dentry

**描述**

剪枝父级 dentry 的未使用的子项。

#### d_alloc

#### 名称

d_alloc — 分配 dcache 项

#### 概要

```
struct dentry * d_alloc (struct dentry * parent, struct qstr * name);
```

**参数**

parent

父级 dentry
name

名称的 qstr

**描述**

分配 dentry。如果内存不足则返回 NULL。成功后，名称可以重用。

### d_instantiate

#### 名称

d_instantiate — 为 dentry 填充 inode 信息

#### 概要

```
void d_instantiate (struct dentry * entry, struct inode * inode);
```

**参数**

entry

要完成的 dentry
inode

附加到该 dentry 的 inode

**描述**

在 entry 中填充 inode 信息。这会将负项变为成员。注意 inode 计数已由调用者增加，以指示其被 dcache 使用。

#### d_alloc_root

#### 名称

d_alloc_root — 分配根 dentry

#### 概要

```
struct dentry * d_alloc_root (struct inode * root_inode);
```

**参数**

root_inode 要为分配根的 inode

**描述**

为 inode 分配根。inode 将被实例化并返回。内存不足时返回 NULL。

### d_lookup

#### 名称

d_lookup — 查找 dentry

#### 概要

```
struct dentry * d_lookup (struct d * parent, struct qstr * name);
```

**参数**

parent

父级 dentry
name

要查找的名称的 qstr

**描述**

在父级 dentry 中查找目标名称。如果找到了 dentry，则增加其引用计数并返回该 dentry。调用者在使用后必须使用 d_put 释放它。失败时返回 NULL。

### d_validate

#### 名称

d_validate — 验证从不安全源提供的 dentry

#### 概要

```
int d_validate (struct dentry dentry, struct dentry * dparent);
```

**参数**

dentry
据说是 dparent 的有效子 dentry
dparent
父级 dentry（已知有效）

**描述**

一个不安全源向我们发送了一个 dentry，在这里对其进行验证并执行 dget。这用于 ncpfs 的 readdir 实现。如果 dentry 无效，则返回零。

### d_delete

#### 名称

d_delete — 删除一个 dentry

#### 概要

```
void d_delete (struct dentry * dentry);
```




#### 参数

#### dentry
要删除的 dentry

#### 描述

如果可能，将 dentry 转换为负 dentry（negative dentry），否则将其从哈希队列中移除以便稍后删除

#### d_rehash

### 名字
d_rehash — 将条目加回哈希表

#### 概要

```
void d_rehash (struct dentry * entry);
```

#### 参数

entry
要添加到哈希表的 dentry

#### 描述
根据其名称将 dentry 添加到哈希表中。

## d_move

### 名字
d_move — 移动 dentry

#### 概要
```
void d_move (struct dentry * dentry, struct dentry * target);
```

#### 参数

dentry
要移动的 dentry

target
新的 dentry

#### 描述
更新 dcache 以反映文件名的移动。负 dcache 条目不应通过这种方式移动。

#### __d_path

### 名字
__d_path — 返回 dentry 的路径

#### 概要
```
char __d_path (struct dentry * dentry, struct vfsmount *
vfsmnt, struct dentry * root, struct vfsmount * rootmnt, char *
buffer, int buflen);
```

#### 参数

- dentry
要报告的 dentry
- vfsmnt
dentry 所属的 vfsmnt
- root
根 dentry
- rootmnt
根 dentry 所属的 vfsmnt
- buffer
用于返回值的缓冲区
- buflen
缓冲区 长度

#### 描述
将 dentry 转换为 ASCII 路径名。如果该条目已被删除，会在末尾附加字符串“(deleted)”。注意这是歧义的。返回缓冲区。

“buflen”应为 PAGE_SIZE 或更大。调用者持有 dcache_lock。

## is_subdir

### 名字
is_subdir — 检查 new_dentry 是否为 old_dentry 的子目录

#### 概要
```
int is_subdir (struct dentry * new_dentry, struct dentry * old_dentry);
```

#### 参数

- new_dentry
new_dentry

- old_dentry
old_dentry

#### 描述
如果 new_dentry 是父目录的子目录（任何深度），则返回 1。否则返回 0。

#### find_inode_number

### 名字
find_inode_number — 检查 dentry 名称

#### 概要
```
ino_t find_inode_number (struct dentry * dir, struct qstr * name);
```

#### 参数

dir
要检查的目录

name
要查找的名称

#### 描述
检查是否已存在给定名称的 dentry，如果它拥有 inode，则返回 inode 号。否则返回 0。

此例程用于对使用合成 inode 号的文件系统对目录列表进行后处理，并且对于保持 getcwd 正常工作是必须的。

#### d_drop

### 名字
d_drop — 丢弃 dentry

#### 概要
```
void d_drop (struct dentry * dentry);
```

#### 参数

dentry
要丢弃的 dentry

#### 描述
d_drop 从父 dentry 哈希表中取消该条目的哈希（unhashes），使其不再通过 VFS 查找找到它。注意这不同于删除 dentry —— d_delete 会尝试尽可能将 dentry 标记为负，从而产生成功的*负向查找*，而 d_drop 只是让缓存查找失败。

d_drop 主要用于因某些原因想要失效 dentry的情况（如 NFS 超时或 autofs 删除）。

#### d_add

### 名字
d_add — 将 dentry 添加到哈希队列

#### 概要
```
void d_add (struct dentry * entry, struct inode * inode);
```

#### 参数

- entry
要添加的 dentry
- inode
要附加到此 dentry 的 inode

#### 描述
这会将条目添加到哈希队列并初始化 inode。该条目实际上在早前的 d_alloc 期间已经填充了内容。

#### dget

### 名字
dget — 获取 dentry 的引用

#### 概要
```
struct dentry * dget (struct dentry * dentry);
```

#### 参数
dentry
要获取引用的 dentry

#### 描述
给定一个 dentry 或 NULL 指针，如果合适则增加引用计数并返回 dentry。当 dentry 拥有引用时，不会被销毁。不应对引用计数为 0 的 dentry 调用 dget。对于这些情况（最好没有，dcache.c 中的函数已足够满足正常需求且它们采取了必要的预防措施），你应该持有 dcache_lock 并调用 dget_locked 而非 dget。

#### d_unhashed

### 名字
d_unhashed — 检查 dentry 是否已哈希

#### 概要
```
int d_unhashed (struct dentry * dentry);
```

#### 参数
dentry
要检查的条目

#### 描述
如果 dentry 当前未被哈希，则返回 true。

### 6.2. Inode 处理

#### __mark_inode_dirty

### 名字
__mark_inode_dirty — 内部函数

#### 概要
```
void __mark_inode_dirty (struct inode * inode, int flags);
```

#### 参数

inode
要标记的 inode
flags
标记的类型（例如 I_DIRTY_SYNC 标记 inode 为脏）

#### write_inode_now

### 名字
write_inode_now — 写入 inode 到磁盘

#### 概要
```
void write_inode_now (struct inode * inode, int sync);
```

#### 参数

inode
要写入的 inode
sync
是否同步写入

#### 描述
如果 inode 是脏的，则将其写入磁盘。这是 knfs 需要的。

#### clear_inode

### 名字
clear_inode — 清理 inode

#### 概要
```
void clear_inode (struct inode * inode);
```

#### 参数

inode
要清理的 inode

#### 描述
由文件系统调用，用以 inode 不再使用。

#### get_empty_inode

### 名字
get_empty_inode — 获取空 inode

#### 概要
```
struct inode * get_empty_inode (void);
```

#### 描述
由文件系统调用，以获取一个空 inode。

## iunique

### 名字
iunique — 获取唯一的 inode

#### 概要
```
ino_t iunique (struct super_block * sb, ino_t max_reserved);
```

#### 参数

sb
superblock
max_reserved
保留数量

#### 描述
在 superblock 上获取唯一的 inode 号。这用于具有自然编号的文件系统。

## BUGS
当大量 inode 存在时，此函数变得相当慢。

#### insert_inode_hash

### 名字
insert_inode_hash — 将 inode 哈希

#### 概要
```
void insert_inode_hash (struct inode * inode);
```

#### 参数

inode
要哈希的 inode

#### 描述
将 inode 添加到该 superblock 的哈希表中。如果 inode 没有 superblock，则会被添加到单独的链。

#### remove_inode_hash

### 名字
remove_inode_hash — 从哈希表中移除 inode

#### 概要
```
void remove_inode_hash (struct inode * inode);
```

#### 参数

inode
要取消哈希的 inode

#### 描述
从 superblock 或匿名哈希中移除 inode。

#### iput

### 名字
iput — 释放 inode

#### 概要
```
void iput (struct inode * inode);
```

#### 参数

inode
要释放的 inode

#### 描述
释放 inode，减少其使用计数。如果 inode 使用计数归零，inode 也将被释放并可能被销毁。





#### 参数

inode

要测试的 inode

#### 描述

如果所说的 inode 被标记为坏块，则返回 true。

### 6.3. 注册与超级块

#### register_filesystem

register_filesystem

#### 名称

register_filesystem — 注册一个新的文件系统

#### 概要

```
int register_filesystem (struct file_system_type * fs);
```

#### 参数

fs

文件系统结构体

#### 描述

将传递的文件系统添加到内核感知的文件系统列表中，以便进行挂载。成功时返回 0，或出错时返回负的 errno 代码。

传递的 `struct file_system_type` 被链接到内核结构中，在文件系统被注销之前不能被释放。

#### unregister_filesystem

#### 名称

unregister_filesystem — 取消文件系统的注销

#### 概要

```
int unregister_filesystem (struct file_system_type * fs);
```

#### 参数

fs

要注销的文件系统

#### 描述

从内核中移除之前已成功注册的文件系统。如果未找到该文件系统，则返回错误。成功时返回 0。

一旦此函数返回，`struct file_system_type` 结构体可以被释放或重用。

#### get_super

#### 名称

get_super — 获取设备的超级块

#### 概要

```
struct super_block * get_super (kdev_t dev);
```

#### 参数

dev
要获取超级块的设备

#### 描述

扫描超级块列表并找到挂载在给定设备上的文件系统的超级块。如果没有找到匹配，则返回 NULL。

### 6.4. 文件锁

#### posix_lock_file

#### 名称

posix_lock_file —

#### 概要

```
int posix_lock_file (struct file * filp, struct file_lock * caller, unsigned int wait);
```

#### 参数

- filp: 要加锁的文件
- caller: 要应用的锁
- wait: 1 为自动重试，0 为返回 -EAGAIN

#### 描述

向文件添加一个 POSIX 风格的锁。我们尽可能地合并相邻的锁。POSIX 锁按所有者任务排序，然后按起始地址排序。

### Kai Petzke 撰写

为了让释放锁变得快得多，我们保留了实际锁之前的指针。但新代码的真正收益是，lock_it 和 unlock_it 变成了一个函数。

### 给所有纯主义者的话

是的，我使用了几个 goto。直接跳转到下一个函数即可。

#### __get_lease

#### 名称

__get_lease — 撤销文件上所有未决租约

#### 概要

```
int __get_lease (struct inode * inode, unsigned int mode);
```

#### 参数

inode

要返回的文件 inode

mode

打开模式（读或写）

#### 描述

get_lease（为了速度进行了内联）已检查该文件是否已存在租约。在调用 open 或 truncate 时，租约会被破坏。除非在 open 中指定了 O_NONBLOCK，否则此函数可能会睡眠。

#### lease_get_mtime

#### 名称

lease_get_mtime —

#### 概要

```
time_t lease_get_mtime (struct inode * inode);
```

#### 参数

inode
inode

#### 描述

这是为了强制 NFS 客户端刷新具有独占租约的文件缓存。理由是，如果有人拥有独占租约，那么他们可能正在修改它。

#### posix_block_lock

#### 名称

posix_block_lock — 阻塞等待文件锁

#### 概要

```
void posix_block_lock (struct file_lock * blocker, struct file_lock * waiter);
```

#### 参数

blocker

正在阻塞的锁

waiter

冲突并必须等待的锁

#### 描述

lockd 需要阻塞等待锁。

#### posix_unblock_lock

#### 名称

posix_unblock_lock — 停止等待文件锁

#### 概要

```
void posix_unblock_lock (struct file_lock * waiter);
```

#### 参数

- waiter:  正在等待的锁

#### 描述

lockd 需要阻塞等待锁。

#### lock_may_read

#### 名称

lock_may_read — 检查区域是否没有锁

#### 概要

```
int lock_may_read (struct inode * inode, loff_t start, unsigned long len);
```

#### 参数

inode
正在读取的 inode

start
要读取的第一个字节

len
要读取的字节数

#### 描述

模拟 Windows 锁定要求。全文件强制性锁（共享模式）可以禁止读取，而字节范围 POSIX 锁如果发生重叠则可以禁止读取。

注意，此函数仅从 knfsd 调用，且永远不会检查锁的所有权。

#### lock_may_write

#### 名称

lock_may_write — 检查区域是否没有锁

#### 概要

```
int lock_may_write (struct inode * inode, loff_t start, unsigned long len);
```

#### 参数

inode
正在写入的 inode

start
要写入的第一个字节

len
要写入的字节数

#### 描述

模拟 Windows 锁定要求。全文件强制性锁（共享模式）可以禁止写入，而字节范围 POSIX 锁如果发生重叠则可以禁止写入。

注意，此函数仅从 knfsd 调用，且永远不会检查锁的所有权。

## fcntl_getlease

#### 名称

fcntl_getlease — 询问当前活跃的租约

#### 概要

```
int fcntl_getlease (struct file * filp);
```

#### 参数

filp
文件

#### 描述

返回的值将是：F_RDLCK 表示读租约活跃，F_WRLCK 表示写租约活跃。

## fcntl_setlease

#### 名称

fcntl_setlease — 为文件设置租约

#### 概要

```
int fcntl_setlease (unsigned int fd, struct file * filp, long arg);
```

#### 参数

fd
文件描述符

filp
文件指针

arg
租约类型

#### 描述

调用此函数为文件建立租约。注意，如果租约已损坏，将返回 SIGIO。

#### sys_flock

#### 名称

sys_flock — 系统调用

#### 概要

```
long sys_flock (unsigned int fd, unsigned int cmd);
```

#### 参数

fd
要锁的文件描述符

cmd
锁类型

#### 描述

对文件应用 FLOCK 风格锁。cmd 可以是：LOCK_SH -- 共享锁。
LOCK_EX -- 独占锁。
LOCK_UN -- 移除现有锁。
LOCK_MAND -- 强制性锁。

#### get_locks

#### 名称

get_locks — 在 /proc/locks 中报告

#### 概要

```
int get_locks (char * buffer, char ** start, off_t offset, int length);
```

#### 参数

buffer
写入到用户空间的地址

start
我们处理缓冲区的位置

length
读取长度

## 7. 网络

### 7.1. 缓冲区函数

#### skb_queue_empty

#### 名称

skb_queue_empty — 检查队列是否为空

#### 概要

```
int skb_queue_empty (struct sk_buff_head * list);
```

#### 参数

list
队列头

#### 描述

如果队列为空则返回 true，否则返回 false。

#### skb_get

#### 名称

skb_get — 缓冲区

#### 概要

```
struct sk_buff * skb_get (struct sk_buff * skb);
```

#### 参数

- skb: 要引用的缓冲区

#### 描述

对缓冲区增加引用并返回缓冲区指针。

#### kfree_skb

#### 名称

kfree_skb — 释放 sk_buff

#### 概要

```
void kfree_skb (struct sk_buff * skb);
```

#### 参数

skb
要释放的缓冲区

#### 描述

放弃缓冲区引用，如果计数归零则释放它。

### skb_cloned

#### 名称

skb_cloned — 缓冲区是否为副本

#### 概要

```
int skb_cloned (struct sk_buff * skb);
```

#### 参数

skb
要检查的缓冲区

#### 描述

如果缓冲区是通过 skb_clone 生成的多个共享副本之一，则返回 true。副本缓冲区是共享数据，因此正常情况下不能写入。

#### skb_shared

#### 名称

skb_shared — 缓冲区是否共享

#### 概要

```
int skb_shared (struct sk_buff * skb);
```

#### 参数

skb
要检查的缓冲区





#### 描述

如果多于一个人引用此缓冲区，则返回 true。

#### skb_share_check

#### 名称

skb_share_check — 检查缓冲区是否被共享，如果是，则进行克隆

#### 概要

```
struct sk_buff * skb_share_check (struct sk_buff *skb, int pri);
```

#### 参数

- skb: 要检查的缓冲区
- pri: 内存分配的优先级

#### 描述

如果缓冲区被共享，则会进行克隆，旧副本会释放一个引用。返回一个具有单一引用的新克隆。如果缓冲区未被共享，则返回原始缓冲区。当在中断状态下或持有自旋锁的情况下调用时，pri 必须为 GFP_ATOMIC。

#### skb_unshare

#### 名称

skb_unshare — 为共享缓冲区创建副本

#### 概要

```
struct sk_buff * skb_unshare (struct sk_buff *skb, int pri);
```

#### 参数

- skb: 要检查的缓冲区
- pri: 内存分配的优先级

#### 描述

如果套接缓冲区是一个克隆体，此函数会创建数据的新副本，释放旧副本的引用计数，并返回引用计数为 1 的新副本。如果缓冲区不是克隆，则返回原始缓冲区。当在持有自旋锁或从中断状态调用时，pri 必须为 GFP_ATOMIC。

在内存分配失败时返回 NULL。

#### skb_peek

#### 名称

skb_peek —

#### 概要

```
struct sk_buff * skb_peek (struct sk_buff_head * list_);
```

#### 参数

- list_: 要查看的列表

#### 描述

查看（Peek）一个 &sk_buff。与大多数其他操作不同，你*必须*小心使用这一个。查看操作（peek）会将缓冲区保留在列表中，其他人可能会将其取走。你必须持有相应的锁或拥有该列表的私有队列。

对于空列表返回 NULL，或返回指向头元素的指针。引用计数不会增加，因此该引用是易变的。请谨慎使用。

#### skb_peek_tail

#### 名称

skb_peek_tail —

#### 概要

```
struct sk_buff * skb_peek_tail (struct sk_buff_head * list_);
```

#### 参数

- list_: 要查看的列表

#### 描述

查看（Peek）一个 &sk_buff。与其它操作不同，你*必须*小心使用这一个。查看操作（peek）会将缓冲区保留在列表中，其他人可能会将其取走。你必须持有相应的锁或拥有该列表的私有队列。

对于空列表返回 NULL，或返回指向尾元素的指针。引用计数不会增加，因此该引用是易变的。请谨慎使用。

#### skb_queue_len

#### 名称

skb_queue_len — 获取队列长度

#### 概要

```
__u32 skb_queue_len (struct sk_buff_head * list_);
```

#### 参数

- list_: 要测量的列表

#### 描述

返回 &sk_buff 队列的长度。

#### __skb_queue_head

#### 名称

__skb_queue_head — 在列表头部队列缓冲区

#### 概要

```
void __skb_queue_head (struct sk_buff_head * list, struct sk_buff *newsk);
```

#### 参数

- list: 要使用的列表
- newsk: 要队列的缓冲区

#### 描述

在列表开始处队列缓冲区。此函数不获取锁，因此在调用它之前必须持有所需的锁。

一个缓冲区不能同时放在两个列表中。

# skb_queue_head

#### 名称

skb_queue_head — 在列表头部队列缓冲区

#### 概要

```
void skb_queue_head (struct sk_buff_head * list, struct sk_buff * newsk);
```

#### 参数

- list: 要使用的列表
- newsk: 要队列的缓冲区

#### 描述

在列表开始处队列缓冲区。此函数会获取锁，可以安全地与其他加锁的 &sk_buff 函数一起使用。

一个缓冲区不能同时放在两个列表中。

#### __skb_queue_tail

#### 名称

__skb_queue_tail — 在列表尾部队列缓冲区

#### 概要

```
void __skb_queue_tail (struct sk_buff_head * list, struct sk_buff * newsk);
```

#### 参数

- list: 要使用的列表
- newsk: 要队列的缓冲区

#### 描述

在列表末尾队列缓冲区。此函数不获取锁，因此在调用它之前必须持有所需的锁。

一个缓冲区不能同时放在两个列表中。

# skb_queue_tail

#### 名称

skb_queue_tail — 在列表尾部队列缓冲区

#### 概要

```
void skb_queue_tail (struct sk_buff_head * list, struct sk_buff * newsk);
```

#### 参数

- list: 要使用的列表
- newsk: 要队列的缓冲区

# 描述 

在列表尾部队列缓冲区。此函数会获取列表锁，可以安全地与其他加锁的 &sk_buff 函数一起使用。

一个缓冲区不能同时放在两个列表中。

#### __skb_dequeue

#### 名称

__skb_dequeue — 从队列头部移除

#### 概要

```
struct sk_buff * __skb_dequeue (struct sk_buff_head * list);
```

#### 参数

- list: 要出队列的列表

# 描述 

移除列表头部。此函数不获取锁，因此必须在持有相应锁的情况下使用。对于空列表返回 NULL。

#### skb_dequeue

#### 名称

skb_dequeue — 从队列头部移除

#### 概要

```
struct sk_buff * skb_dequeue (struct sk_buff_head * list);
```

#### 参数

- list: 要出队列的列表

# 描述 

移除列表头部。此函数会获取锁，因此可以安全地与其他加锁的列表函数使用。对于空列表返回 NULL。

#### skb_insert

#### 名称

skb_insert — 插入缓冲区

#### 概要

```
void skb_insert (struct sk_buff_head * list, struct sk_buff * old, struct sk_buff * newsk);
```

#### 参数

- list: 要使用的列表
- old: 要插入的缓冲区
- newsk: 要队列的缓冲区

# 描述 

在列表开始处队列缓冲区。此函数不获取锁……等等。

#### skb_append

#### 名称

skb_append — 追加缓冲区

#### 概要

```
void skb_append (struct sk_buff_head * list, struct sk_buff * old, struct sk_buff * newsk);
```

#### 参数

- list: 要使用的列表
- old: 要插入的缓冲区
- newsk: 要队列的缓冲区

# 描述 

在列表末尾队列缓冲区。此函数会获取列表锁，可以安全地与其他加锁的 &sk_buff 函数一起使用。

#### skb_unlink

#### 名称

skb_unlink — 从列表中移除缓冲区

#### 概要

```
void skb_unlink (struct sk_buff * skb);
```

#### 参数

- skb: 要移除的缓冲区

# 描述 

在列表开始处队列缓冲区。等等……即使不知道它在哪个列表中也能工作，这在某些时候非常方便。这也意味着当你移除它时，*列表必须存在*。因此，在销毁列表之前，必须移除其内容。





要添加的数据量

#### 描述

此函数扩展缓冲区起始处的已用数据区域。如果这超过了缓冲区的总头部空间（headroom），内核将触发崩溃（panic）。返回指向额外数据第一个字节的指针。

#### skb_pull

#### 名称

skb_pull — 从缓冲区头部移除数据

# 签 supposed

```
unsigned char * skb_pull (struct sk_buff *skb, unsigned int len);
```

#### 参数

- skb: 要使用的缓冲区
- len: 要移除的数据量

#### 描述

此函数从缓冲区头部移除数据，并将内存归还给头部空间（headroom）。返回缓冲区中下一个数据的指针。一旦数据被拉取，未来的推送（push）将覆盖旧数据。

#### skb_headroom

#### 名称

skb_headroom — 缓冲区头部的字节数

# 签 supposed

```
int skb_headroom (const struct sk_buff *skb);
```

#### 参数

- skb: 要检查的缓冲区

#### 描述

返回 &skb_buff 头部可用空间的字节数。

#### skb_tailroom

#### 名称

skb_tailroom — 缓冲区尾部的字节数

# 签 supposed

```
int skb_tailroom (const struct sk_buff *skb);
```

#### 参数

- skb: 要检查的缓冲区

#### 描述

返回 skb_buff 尾部可用空间的字节数

#### skb_reserve

#### 名称

skb_reserve — 调整头部空间

# 签 supposed

```
void skb_reserve (struct sk_buff *skb, unsigned int len);
```

#### 参数

- skb: 要修改的缓冲区
- len: 要移动的字节数

#### 描述

通过减少尾部空间（tail room）来增加空 &sk_buff 的头部空间。这只允许空缓冲区。

#### skb_trim

#### 名称

skb_trim — 移除缓冲区的末部

# 签 supposed

```
void skb_trim (struct sk_buff *skb, unsigned int len);
```

#### 参数

- skb: 要修改的缓冲区
- len: 新长度

#### 描述

通过移除尾部数据来裁剪缓冲区长度。如果缓冲区长度已经小于指定的长度，则不进行修改。

#### skb_orphan

#### 名称

skb_orphan — 孤立缓冲区

# 签 supposed

```
void skb_orphan (struct sk_buff *skb);
```

#### 参数

- skb: 要孤立的缓冲区

#### 描述

如果缓冲区当前有所有者，则我们调用所有者的析构函数并使 skb 变为无所有。缓冲区继续存在，但不再由其原所有所有。

#### skb_queue_purge

#### 名称

skb_queue_purge — 清空列表

# 签 supposed

```
void skb_queue_purge (struct sk_buff_head * list);
```

#### 参数

- list: 要清空的列表

#### 描述

删除 &sk_buff 列表上的所有缓冲区。每个缓冲区都从列表中移除并释放一个引用。此函数会获取列表锁，并且对于其他列表锁函数来说是原子的。

#### __skb_queue_purge

#### 名称

__skb_queue_purge — 清空列表

# 签 supposed

```
void __skb_queue_purge (struct sk_buff_head * list);
```

#### 参数

- list: 要清空的列表

#### 描述

删除 &sk_buff 列表上的所有缓冲区。每个缓冲区都从列表中移除并释放一个引用。此函数不获取列表锁，调用者必须持有相关锁才能使用它。

#### __dev_alloc_skb

#### 名称

__dev_alloc_skb — 为发送分配一个 skbuff

# 签 supposed

```
struct sk_buff * __dev_alloc_skb (unsigned int length, int gfp_mask);
```

#### 参数

- length: 要分配的长度
- gfp_mask: 获取空页掩码，传递给 alloc_skb（等待，传递给内部分配器）

#### 描述

分配一个新的 &sk_buff 并将其使用计数设置为 1。该缓冲区内置了未指定的头部空间。用户应该分配他们认为需要的头部空间，而无需考虑已内置的空间。内置空间用于优化。

如果没有可用内存，则返回 NULL。

#### dev_alloc_skb

#### 名称

dev_alloc_skb — 为发送分配一个 skbuff

# 签 supposed

```
struct sk_buff * dev_alloc_skb (unsigned int length);
```

#### 参数

- length: 要分配的长度

#### 描述

分配一个新的 &sk_buff 并将其使用计数设置为 1。该缓冲区内置了未指定的头部空间。用户应该分配他们认为需要的头部空间，而无需考虑已内置的空间。内置空间用于优化。

如果没有可用内存，则返回 NULL。虽然此函数分配内存，但它可以在中断中调用。

#### skb_cow

#### 名称

skb_cow — 需要时拷贝 skb 的头部

# 签 supposed

```
int skb_cow (struct sk_buff *skb, unsigned int headroom);
```

#### 参数

- skb: 要拷贝的缓冲区
- headroom: 需要的头部空间

#### 描述

如果传递的 skb 提供了足够的头部空间或其数据部分是共享的，则重新分配数据。如果重新分配失败，返回错误且不改变原始 skb。

结果是具有可写区域 skb->head...skb->tail 且头部至少有 headroom 空间的 skb。

#### skb_over_panic

#### 名称

skb_over_panic — 私有函数

# 签 supposed

```
void skb_over_panic (struct sk_buff *skb, int sz, void *here);
```

#### 参数

- skb: 缓冲区
- sz: 大小
- here: 地址

#### 描述

用于 skb_put 的支持代码。用户不可调用。

#### skb_under_panic

#### 名称

skb_under_panic — 私有函数

# 签 supposed

```
void skb_under_panic (struct sk_buff *skb, int sz, void *here);
```

#### 参数

- skb: 缓冲区
- sz: 大小
- here: 地址

#### 描述

用于 skb_push 的支持代码。用户不可调用。

#### alloc_skb

#### 名称

alloc_skb — 分配一个 skbuff

# 签 supposed

```
struct sk_buff * alloc_skb (unsigned int size, int gfp_mask);
```

#### 参数

- size: 要分配的尺寸
- gfp_mask: 分配掩码

#### 描述

分配一个新的 &sk_buff。返回的缓冲区没有头部空间或尾部空间。引用计数为 1。如果分配失败，返回 NULL。此函数从中断调用，gfp_mask 必须是 GFP_ATOMIC。

#### __kfree_skb

#### 名称

__kfree_skb — 私有函数

# 签 supposed

```
void __kfree_skb (struct sk_buff *skb);
```

#### 参数

- skb: 缓冲区

#### 描述

释放 skbuff。释放附加到缓冲区上的任何内容。这是一个内部函数。

#### skb_clone

#### 名称

skb_clone — 复制一个 skbuff

# 签 supposed

```
struct sk_buff * skb_clone (struct sk_buff *skb, int gfp_mask);
```

#### 参数

- skb: 要复制的缓冲区
- gfp_mask: 分配优先级

#### 描述

复制一个 skbuff。新的缓冲区共享相同数据但不共享结构。如果分配失败，函数返回 NULL。

#### skb_copy

#### 名称

skb_copy — 创建 skbuff 的副本

# 签 supposed

```
struct sk_buff * skb_copy (const struct sk_buff *skb, int gfp_mask);
```

#### 参数

- skb: 要复制的缓冲区
- gfp_mask: 分配优先级

#### 描述

对 &sk_buff 及其数据进行复制。这用于调用者希望修改数据并需要数据私有副本的情况。失败时返回 NULL，成功时返回缓冲区指针。





gfp_mask

分配优先级

#### 描述

扩展（如果 `&nhead` 和 `&tail` 为零，则创建相同的副本）skb 头部。&sk_buff 本身不会改变。&sk_buff 的引用计数必须为 1。如果扩展成功则返回零，如果扩展失败则返回错误。在后一种情况下，&sk_buff 不会改变。

所有指向 skb 头部的指针都可能会发生，并在调用此函数后必须重新加载。

#### skb_copy_expand

#### 名称

skb_copy_expand — 复制并扩展 sk_buff

# 签名

```
struct sk_buff * skb_copy_expand (const struct sk_buff *skb, int newheadroom, int newtailroom, int gfp_mask);
```

#### 参数

- skb: 要复制的缓冲区
- newheadroom: 头部新的空字节数
- newtailroom: 尾部新的空字节数
- gfp_mask: 分配优先级

#### 描述

为 &sk_buff 及其数据创建一个副本，并在在此过程中分配额外的空间。

当调用者希望修改数据并需要数据的私有副本以为新字段分配尽可能空间时，使用此函数。失败时返回 NULL，成功时返回缓冲区指针。返回的缓冲区引用计数为 1。

如果从中断程序中调用此函数，必须将 GFP_ATOMIC 作为分配优先级。

#### __pskb_pull_tail

#### 名称

__pskb_pull_tail — 推进 skb 头部的尾部

# 签名

```
unsigned char * __pskb_pull_tail (struct sk_buff *skb, int delta);
```

#### 参数

- skb: 要重新分配的缓冲区
- delta: 向后推进尾部的字节数

#### 描述

该函数仅对分片的 &sk_buff 意义意义，它通过向前移动尾部来扩展头部，并从碎片部分复制必要的数据。
&sk_buff 的引用计数必须为 1。

如果拉取失败则返回 NULL（且 &sk_buff 不改变），成功则返回 skb 新尾部的值。

所有指向 skb 头部的指针都可能会发生，并在调用此函数后必须重新加载。

### 7.2. 套接字过滤器

#### sk_run_filter

#### 名称

sk_run_filter — 在套接字上运行过滤器

# 签名

```
int sk_run_filter (struct sk_buff *skb, struct sock_filter *filter, int flen);
```

#### 参数

- * skb: 在其运行过滤器的缓冲区
- filter: 要应用的过滤器
- flen: 过滤器的长度

#### 描述

解码并将过滤器指令应用到 skb->data。返回要保留的长度，0 表示无。skb 是我们正在过滤的数据，filter 是过滤器指令的数组，flen 是数组中过滤器块的数量。

#### sk_chk_filter

#### 名称

sk_chk_filter — 验证套接字过滤器代码

# 签名

```
int sk_chk_filter (struct sock_filter * filter, int flen);
```

#### 参数

- filter: 要验证的过滤器
- flen: 过滤器的长度

#### 描述

检查用户的过滤器代码。如果我们让糟糕的过滤器代码溜过去，就完蛋了！过滤器不能包含超出范围的引用或跳转、没有非法指令且没有向后跳转。它必须以 RET 指令结束。

如果规则集合法则返回 0，否则返回负的 errno 代码。

## 第 8 章 网络设备支持

### 8.1. 驱动支持

#### init_etherdev

#### 名称

init_etherdev — 注册以太网设备

# 签名

```
struct net_device * init_etherdev (struct net_device * dev, int sizeof_priv);
```

#### 参数

- dev: 要填充的以太网设备结构，或者如果应该分配新的 struct 则为 NULL。
- sizeof_priv: 分配额外的私有结构的大小

#### 描述

填充以太网设备结构的值。

如果传递了设备结构，则创建一个大小为 sizeof_priv 的私有区域。对于该私有区域执行 32 字节对齐（注：原文为 bit，可能为字节之误）。

#### 名称

alloc_etherdev — 分配以太网设备

# 签名

```
struct net_device * alloc_device (int sizeof_priv);
```

#### 参数

- sizeof_priv: 分配私有结构的大小

#### 描述

填充以太网设备结构的值。

除了注册设备外，该函数还完成了所有其他设置工作。

#### 名称

init_fddidev — 注册 FDDI 设备

# 签名

```
struct net_device * init_fddidev (struct net_device * dev, int sizeof_priv);
```

#### 参数

- dev: 要填充的 FDDI 设备结构，或者如果应该分配新的 struct 则为 NULL。
- sizeof_priv: 分配额外的私有结构的大小

# 描述 

填充以太网设备结构的值。

如果传递了设备结构，则创建一个大小为 sizeof_priv 的私有区域。对于该私有区域执行 32 字节对齐。

#### 名称

alloc_fddidev — 分配 FDDI 设备

# 签名

```
struct net_device * alloc_fddidev (int sizeof_priv);
```

#### 参数

- sizeof_priv: 分配私有结构的大小

# 描述 

填充以太网设备结构的值。

#### init_hippi_dev

#### 名称

init_hippi_dev — 注册 HIPPI 设备

# 签名

```
struct net_device * init_hippi_dev (struct net_device * dev, int sizeof_priv);
```

#### 参数

- dev: 要填充的 HIPPI 设备结构，或者如果应该分配新的 struct 则为 NULL。
- sizeof_priv: 分配额外的私有结构的大小

# 描述 

填充以太网设备结构的值。

如果传递了设备结构，则创建一个大小为 sizeof_priv 的私有区域。对于该私有区域执行 32 字节对齐。

#### 名称

alloc_hippi_dev — 分配并设置 HIPPI 设备

# 签名

```
struct net_device * alloc_hippi_dev (int sizeof_priv);
```

#### 参数

- sizeof_priv: 分配私有结构的大小

# 描述 

填充以太网设备结构的值。





## Arguments

dev
一个待填充的光纤通道设备结构，如果需要分配新结构体则为 NULL。

sizeof_priv
为此以太网设备分配的额外驱动私有结构的大小。

## Description

使用光纤通道通用值填充设备结构中的字段。
如果没有传递设备结构，则会构造一个新的结构体，并包含一个大小为 `sizeof_priv` 的私有数据区域。该私有数据区域强制执行 32 字节（而非位）对齐。
如果传递的 dev->name 为空字符串区域或创建了新结构，则将构造一个新的字符串。

#### alloc_fcdev

# Name

alloc_fcdev — 注册光纤通道设备

# Synopsis

```
struct net_device * alloc_fcdev (int sizeof_priv);
```

## Arguments

sizeof_priv
为此以光纤通道设备分配的额外驱动私有结构的大小。

## Description

使用光纤通道通用值填充设备结构中的字段。
构造一个新的网络设备，并包含一个大小为 `sizeof_priv` 的私有数据区域。该私有数据区域强制执行 32 字节（而非位）对齐。

#### dev_add_pack

# Name

dev_add_pack — 添加数据包处理器

# Synopsis

```
void dev_add_pack (struct packet_type * pt);
```

## Arguments

pt
数据包类型声明

## Description

向网络栈添加一个协议处理程序。传递的 `&packet_type` 被链接到内核列表中，在它从内核列表中移除之前可能被释放。

#### dev_remove_pack

# Name

dev_remove_pack — 移除数据包处理器

# Synopsis

```
void dev_remove_pack (struct packet_type * pt);
```

## Arguments

- pt
数据包类型声明

## Description

移除之前通过 `dev_add_pack` 添加到内核协议处理器的协议处理程序。传递的 `&packet_type` 将从内核列表中移除，并在此函数返回后可以释放或重用。

#### __dev_get_by_name

# Name

__dev_get_by_name — 通过名称查找设备

# Synopsis

```
struct net_device * __dev_get_by_name (const char * name);
```

## Arguments

name
要查找的内容

## Description

通过名称查找接口。必须在 RTNL 信号量或 `dev_base_lock` 下调用。如果找到名称，则返回设备指针。如果未找到，则返回 NULL。引用计数不会增加，因此调用者必须小心处理锁。

#### dev_get_by_name

# Name

dev_get_by_name — 通过名称查找设备

# Synopsis

```
struct net_device * dev_get_by_name (const char * name);
```

## Arguments

name
要查找的名称

## Description

通过名称查找接口。这可以在任何上下文中调用，并处理自己的锁。返回的句柄使用计数已增加，调用者在不再需要它时必须使用 `dev_put` 来释放它。如果没有找到匹配的设备，则返回 NULL。

#### dev_get

# Name

dev_get — 测试设备是否存在

# Synopsis

```
int dev_get (const char * name);
```

## Arguments

name
要测试的名称

## Description

测试名称是否存在。如果找到名称，则返回 true。为了确保名称在测试期间未被分配或移除，调用者必须持有 rtnl 信号量。
此函数主要存在是为了与旧驱动程序兼容。

#### __dev_get_by_index

# Name

__dev_get_by_index — 通过 ifindex 查找设备

# Synopsis

```
struct net_device * __dev_get_by_index(int ifindex);
```

## Arguments

ifindex
设备的索引

## Description

通过索引搜索接口。如果未找到设备，则返回 NULL 或返回设备指针。设备的引用计数未增加，因此调用者必须小心处理锁。调用者必须持有 RTNL 信号量或 `dev_base_lock`。

#### dev_get_by_index

# Name

`dev_get_by_index` — 通过 ifindex 查找设备

# Synopsis

```
struct net_device * dev_get_by_index (int ifindex);
```

## Arguments

ifindex
设备的索引

## Description

通过索引搜索接口。如果未找到设备，则返回 NULL 或返回设备指针。返回的设备已增加引用，在用户调用 `dev_put` 表明已完成操作之前，该指针是安全的。

#### dev_alloc_name

# Name

dev_alloc_name — 为设备分配名称

# Synopsis

```
int dev_alloc_name (struct net_device * dev, const char * name);
```

## Arguments

- dev
设备
- name
名称格式字符串

## Description

传递一个格式字符串——例如 "%s"——它将尝试寻找一个合适的 ID。对于许多设备来说效率不高，且调用并不频繁。调用者在分配名称和添加设备时必须持有 `dev_base` 或 `rtl` 锁，以避免重复。返回分配的单元号或负 errno 错误码。

#### dev_alloc

# Name

dev_alloc — 分配网络设备和名称

# Synopsis

```
struct net_device * dev_alloc (const char * name, int * err);
```

## Arguments

name
名称格式字符串

err
错误返回指针

## Description

传递格式字符串，例如 "ltd"，它将分配一个网络设备和名称空间。如果没有可用内存，则返回 NULL。如果分配成功，则会分配名称并返回设备指针。如果名称分配失败，则返回 NULL。错误原因将作为负 errno 错误码通过 `err` 指向的变量返回。

调用者在执行此操作时必须持有 `dev_base` 或 RTNL 锁，以避免重复分配名称。

#### netdev_state_change

# Name

netdev_state_change — 设备状态变更

# Synopsis

```
void netdev_state_change (struct net_device * dev);
```

## Arguments

dev
触发通知的设备

## Description

表示设备状态已更改。此函数调用 `netdev_chain` 通知链并向路由套字发送 NEWLINK 消息。

## dev_load

# Name

dev_load — 加载网络模块

# Synopsis

```
void dev_load (const char * name);
```

## Arguments

name
接口名称

## Description

如果不存在网络接口且进程具有相应权限，此函数将加载模块。如果内核中不支持模块加载，则它成为一个无操作操作（nop）。

#### dev_open

# Name

dev_open — 准备接口使用

# Synopsis

```
int dev_open (struct net_device * dev);
```

## Arguments

dev
要打开的设备

## Description

将设备从关闭状态切换到开启状态。调用设备的私有打开函数，然后加载组播列表。最后将设备移动到开启状态并向 netdev 通知链发送 NETDEV_UP 消息。

在激活接口上调用此函数为无操作。失败时返回负 errno。

#### dev_close

# Name

dev_close — 关闭接口

# Synopsis

```
int dev_close (struct net_device * dev);
```

## Arguments

dev
要关闭的设备

## Description

此函数将激活设备移动到关闭状态。向 netdev 通知链发送 NETDEV_GOING_DOWN。随后停用设备，最后向通知链发送 NETDEV_DOWN。

## register_netdevice_notifier

# Name

register_netdevice_notifier — 注册网络通知器

# Synopsis

```
int register_netdevice_notifier (struct notifier_block * nb);
```

## Arguments

nb
通知器

## Description

注册一个网络设备事件发生时调用的通知器。传递的通知器被链接到内核结构中，在注销之前不能重用。失败时返回负 errno 错误码。

## unregister_netdevice_notifier

# Name

unregister_netdevice_notifier — 注销网络通知器

# Synopsis

```
int unregister_netdevice_notifier (struct notifier_block * nb);
```

## Arguments

nb
通知器

注销之前通过 `register_netdevice_notifier` 注册的通知器。该通知器从内核结构中解除链接，之后可以重用。失败时返回负 errno 错误码。





#### 概要

```
int dev_queue_xmit (struct sk_buff * skb);
```

#### 参数

- skb
  要传输的缓冲区

#### 描述

将缓冲区加入队列以发送到网络设备。调用者在调用此函数之前必须设置设备和优先级并构建缓冲区。该函数可以从中断中调用。

失败时返回负的 errno 码。成功并不保证帧一定会被发送，因为它可能由于拥塞或流量整形而被丢弃。

# netif_rx

#### 名称

netif_rx — 将缓冲区提交到网络层代码

#### 概要

```
int netif_rx (struct sk_buff * skb);
```

#### 参数

skb

要提交的缓冲区

#### 描述

此函数从设备驱动程序接收一个数据包，并将其放入队列以供上层（协议层）处理。该函数总是执行执行的。在处理过程中，缓冲区可能会因为拥塞控制或协议层而被丢弃。

# 返回值

NET_RX_SUCCESS (无拥塞)
NET_RX_CN_LOW (低拥塞)
NET_RX_CN_MOD (中度拥塞)
NET_RX_CN_HIGH (高拥塞)
NET_RX_DROP (包被丢弃)

# net_call_rx_atomic

#### 名称

net_call_rx_atomic —

#### 概要

```
void net_call_rx_atomic (void (*fn) (void));
```

#### 参数

fn

要调用的函数

#### 描述

执行一个相对于协议层是原子的函数调用。

# register_gifconf

#### 名称

register_gifconf — 注册一个 SIOCGIF 处理程序

#### 概要

```
int register_gifconf (unsigned int family, gifconf_func_t * gifconf);
```

#### 参数

family

地址族

gifconf

函数处理程序

#### 描述

注册与协议相关的地址转储例程。传递的处理程序在被另一个处理程序替换之前，不能被释放或重用。

# netdev_set_set_master

#### 名称

netdev_set_master — 设置主从设备对

#### 概要

```
int netdev_set_master (struct net_device * slave, struct net_device * master);
```

#### 参数

- slave
  从设备

- master
  新的主设备

# 描述 

更改从设备的主设备。传递 NULL 以断开绑定（bonding）。调用者必须持有 RTNL 信号量。失败时返回负的 errno 码。成功时调整引用计数，向路由套接字发送 RTM_NEWLINK 信号，函数返回零。

# dev_set_promiscuity

#### 名称

dev_set_promiscuity — 更新设备上的混杂模式计数

#### 概要

```
void dev_set_promiscuity (struct net_device * dev, int inc);
```

#### 参数

- dev
  设备

- inc
  修改值

# 描述 

从设备上添加或移除混杂模式。只要设备中的计数保持为零，接口就会保持在混杂状态。一旦计数归零，设备将恢复到正常的过滤操作。负的 inc 值用于取消设备上的混杂模式。

# dev_set_allmulti

#### 名称

dev_set_allmulti — 更新设备上的全组播计数

#### 概要

```
void dev_set_allmulti (struct net_device * dev, int inc);
```

#### 参数

- dev
  设备

- inc
  修改值

# 描述 

在设备上添加或移除对所有组播帧的接收。只要设备中的计数保持为零，接口就会保持监听所有接口。一旦计数归零，设备将恢复到正常的过滤操作。负的 inc 值用于在释放需要所有组播的资源时递减计数器。

# dev_ioctl

#### 名称

dev_ioctl — 网络设备 ioctl

#### 概要

```
int dev_ioctl (unsigned int cmd, void * arg);
```

#### 参数

cmd
要执行的命令

arg
用户空间中 structreq 结构体的指针

# 描述 

向设备下发 ioctl 函数。这通常由用户空间接口调用，但有时对其他用途也有用。如果值为正，则返回系统调用的返回值；若出错则返回负的 errno。

# dev_new_index

#### 名称

dev_new_index — 分配 ifindex

#### 概要

```
int dev_new_index ( void );
```

#### 参数

void

无参数

# 描述 

为新的设备接口编号返回一个唯一的值。调用者必须持有 rtn 信号量或 dev_base_lock 以确保其唯一性。

# netdev_finish_unregister

#### 名称

netdev_finish_unregister — 完成取消注销

#### 概要

```
int netdev_finish_unregister (struct net_device * dev);
```

#### 参数

dev
设备

# 描述 

销毁并释放一个死亡的设备。成功时返回零。

# unregister_netdevice

#### 名称

unregister_netdevice — 从内核中移除设备

#### 概要

```
int unregister_netdevice (struct net_device * dev);
```

#### 参数

dev
设备

# 描述 

此函数关闭设备接口并将其从内核表中移除。成功时返回 0，失败时返回负的 errno。

调用者必须持有 rtn 信号量。关于锁的细节请参见 Space.c 末尾的注释。你可能想用 unregister_netdev 而不是这个。

# 8.2. 基于 8390 的网卡

#### ei_open

#### 名称

ei_open — 打开/初始化板卡

#### 概要

```
int ei_open (struct net_device * dev);
```

#### 参数

dev
网络设备

# 描述 

此例程在打开时重新设置，尽管许多设置只需要在启动时设置。

#### ei_close

#### 名称

ei_close — 关闭网络设备

#### 概要

```
int ei_close (struct net_device * dev);
```

#### 参数

dev
网络设备

# 描述 

ei_open 的相反操作。在执行 `ifconfig <dev> down` 时使用。

# ei_tx_timeout

#### 名称

ei_tx_timeout — 处理传输超时

#### 概要

```
void ei_tx_timeout (struct net_device * dev);
```

#### 参数

dev
网络设备

# 描述 

当传输完成（或失败）时由内核调用。

#### ei_interrupt

#### 名称

ei_interrupt — 处理来自 8390 的中断

#### 概要

```
void ei_interrupt (int irq, void * dev_id, struct pt_regs * regs);
```

#### 参数

- irq
  中断号

- dev_id
  指向 net_device 的指针

- regs
  未使用

# 描述 

处理接口中断。我们从 8390 卡中提取数据包并将其发送到协议栈。我们还处理完成情况、更新计数器并进行其他清理工作。

#### ethdev_init

#### 名称

ethdev_init — 初始化 8390 设备结构

#### 概要

```
int ethdev_init (struct net_device * dev);
```

#### 参数

dev
网络设备

# 描述 

初始化 8390 设备结构。不要对此使用 __init，因为它也被用于基于 8390 的模块化驱动程序。

# NS8390_init

#### 名称

NS8390_init — 初始化 8390 硬件

#### 概要

```
void NS8390_init (struct net_device * dev, int startp);
```

#### 参数

dev
网络设备

startp
布尔值。启动芯片处理。

#### 描述

必须在持有锁的情况下调用。

# 8.3. 同步 PPP

#### sppp_input

#### 名称

sppp_input — 接收并处理 WAN PPP 帧

#### 概要

```
void sppp_input (struct net_device * dev, struct sk_buff * skb);
```

#### 参数

dev
到达设备

skb
要处理的缓冲区

# 描述 

此函数可以由没有时间限制的卡调用，通常在中断处理后由网络层调用，以处理通过 netif_rx 的帧。

我们处理卡中的选项。如果帧的目标是协议栈，我们将其重新放入队列供上层协议处理。如果是控制帧，则在此处理并丢弃。

#### sppp_close

#### 名称

sppp_close — 关闭同步 PPP 或 Cisco HDLC 链路

#### 概要

```
int sppp_close (struct net_device * dev);
```

#### 参数

dev
要关闭链路的网络设备

# 描述 

关闭通道的逻辑接口。这不是优雅的操作，因为我们假设也将将掉 DTR。任何超时都会被杀死。

# sppp_open

#### 名称

sppp_open — 打开同步 PPP 或 Cisco HDLC 链路

#### 概要

```
int sppp_open (struct net_device * dev);
```

#### 参数

dev
要打开的网络设备





#### 参数

dev

要激活的网络设备

#### 描述

关闭任何同步会话并从头开始。在 PPP 情况下，这意味着与 LCP/IPCP 等等协议进行协商，而对于 Cisco HDLC，我们只需要开始发送心跳包（keepalives）。

#### sppp_reopen

#### 名称

sppp_reopen — 物理链路链路丢失的通知

#### 概要

```
int sppp_reopen (struct net_device *dev);
```

#### 参数

dev

丢失链路的设备

#### 描述

此函数通知同步协议代码底层链路已失效（例如 X.21 上的载波信号丢失）。

我们增加了魔术数字（magic numbers），以确保如果对方没有注意到我们的变化，我们将能够正确地启动新会话。由于电信电路的特性，你会在某一端不断地丢失载波信号。

执行此操作后，我们回到协商阶段。此函数可以在中断上下文中调用。

# sppp_change_mtu

#### 名称

sppp_change_mtu — 修改链路 MTU

#### 概要

```
int sppp_change_mtu (struct net_device *dev, int new_mtu);
```

#### 参数

- dev
要修改 MTU 的设备
- new_mtu
新的 MTU

#### 描述

修改链路的 MTU。这只能在链路处于关闭（down）状态时调用。如果链路已开启或 MTU 超出范围，将返回错误。

#### sppp_do_ioctl

#### 名称

sppp_do_ioctl — ppp/hdlc 的 ioctl 处理器

#### 概要

```
int sppp_do_ioctl (struct net_device *dev, struct ifreq *ifr, int cmd);
```

#### 参数

dev

执行 ioctl 的设备

ifr

来自用户的接口请求块

cmd

正在执行的命令

#### 描述

此函数处理用户可能为了控制 PPP/HDLC 链路设置而发出的 ioctl。它同时进行忙碌检查和安全检查。此函数旨在供想要添加自定义 ioctl 的调用者进行封装。

#### sppp_attach

#### 名称

sppp_attach — 将同步 PPP/HDLC 附加到设备

#### 概要

```
void sppp_attach (struct ppp_device *pd);
```

#### 参数

pd

要初始化的 PPP 设备

# 描述 

这在接口上初始化 PPP/HDLC 支持。在调用时，设备元素必须指向该接口所附加的网络设备。该接口尚未尚未注册。

#### sppp_detach

#### 名称

sppp_detach — 从设备中释放 PPP 资源

#### 概要

```
void sppp_detach (struct net_device *dev);
```

#### 参数

dev

要释放的网络设备

# 描述 

停止并释放此接口使用的任何 PPP/HDLC 资源。必须在设备释放之前调用此函数。

## 第 9 章 模块支持

## 9.1. 模块加载

### request_module

#### 名称

request_module — 尝试加载内核模块

#### 概要

```
int request_module (const char *module_name);
```

#### 参数

module_name

模块名称

#### 描述

使用用户态模块加载器加载模块。该函数成功时返回零，失败时返回负 errno 码。注意，模块加载成功并不意味着模块没有因为自身的错误而卸载并退出。调用者必须检查其请求的服务现在是否可用，而不是盲目调用。

如果禁用了模块自动加载支持，则此函数将变为无操作。

# call_usermodehelper

#### 名称

call_usermodehelper — 启动用户态应用程序

#### 概要

```
int call_usermodehelper (char *path, char **argv, char **envp);
```

#### 参数

path

应用程序的路径

argv

null 终止的参数列表

envp

null 终止的环境列表

#### 描述

运行用户空间应用程序。该应用程序异步启动。它作为 keventd 的子进程运行。以全 root 权限运行。keventd 在子进程退出时静默回收它。

必须在进程上下文中调用。成功时返回零，否则返回负错误码。

## 9.2. 模块间支持

# inter_module_register

#### 名称

inter_module_register — 注册一组新的模块间数据。

#### 概要

```
void inter_module_register (const char *im_name, struct module *owner, const void *userdata);
```

#### 参数

- im_name
用于标识数据的任意字符串，必须唯一
- owner
注册数据的模块，始终使用 THIS_MODULE
- userdata
指向要注册的任意用户数据的指针

# 描述 

检查 im_name 是否已经注册，如果是，则报错。对于新数据，将其添加到 inter_module_entry 列表中。

# inter_module_unregister

#### 名称

inter_module_unregister — 取消注册一组模块间数据。

#### 概要

```
void inter_module_unregister (const char *im_name);
```

#### 参数

im_name
用于标识数据的任意字符串，必须唯一

# 描述 

检查 im_name 是否已经注册，如果是，则报错。对于新数据（此处误），将其添加到 inter_module_entry 列表中。

# inter_module_get

#### 名称

inter_module_get — 从另一个模块获取数据

#### 概要

```
void *inter_module_get (const char *im_name);
```

#### 参数

im_name
用于标识数据的任意字符串，必须唯一

# 描述 

检查 im_name 是否已经注册，如果是，则报错。对于新数据（此处误），将其添加到 inter_module_entry 列表中。

# inter_module_get_request

#### 名称

inter_module_get_request — 请求并获取数据

#### 概要

```
void *inter_module_get_request (const char *im_name, const void *userdata);
```

#### 参数

im_name
用于标识数据的任意字符串，必须唯一
userdata
要注册的用户数据的指针

# 描述 

将数据添加到 inter_module_entry 列表中。如果成功，返回 userdata。

# inter_module_put

#### 名称

inter_module_put — 从另一个模块释放数据

#### 概要

```
void inter_module_put (const char *im_name);
```

#### 参数

im_name
用于标识数据的任意字符串，必须唯一

# 描述 

检查 im_name 是否已经注册，如果是，则报错。对于新数据，将其添加到 inter_module_entry 列表中。

## 第 10 章 硬件接口

## 10.1. 中断处理

### disable_irq_nosync

#### 名称

disable_irq_nosync — 无同步地禁用中断

#### 概要

```
void disable_irq_nosync (unsigned int irq);
```

#### 参数

irq
要禁用的中断

#### 描述

禁用选定的中断线。操作是嵌套的。与 disable_irq 不同，此函数不确保现有的中断处理程序实例在返回前完成。

此函数可以在中断上下文中调用。

### disable_irq

#### 名称

disable_irq — 禁用中断并等待完成

#### 概要

```
void disable_irq (unsigned int irq);
```

#### 参数

irq
要禁用的中断

#### 描述

禁用选定的中断线。操作是嵌套的。此函数会等待任何挂起的中断处理程序执行完成。如果你在持有资源时调用此函数，而中断处理程序需要该资源，会导致死锁。

此函数可以小心地从中断上下文中调用。

### enable_irq

#### 名称

enable_irq — 启用中断的处理

#### 概要

```
void enable_irq (unsigned int irq);
```

#### 参数

irq
要启用的中断

#### 描述

撤销调用 disable_irq 的影响。如果这匹配最后一次禁用操作，则重新启用该中断线的处理。

此函数可以在中断上下文中调用。

### probe_irq_mask

#### 名称

probe_irq_mask — 扫描位图的中断线

#### 概要

```
unsigned int probe_irq_mask (unsigned long val);
```

#### 参数

```
val
要考虑的中断掩码
```

#### 描述

扫描 ISA 总线中断线并返回活动中断的位图。然后中断探测逻辑状态恢复到之前的值。

## 10.2. MTRR 处理

# mtrr_add

#### 名称

mtrr_add — 添加一个内存类型区域

#### 概要

```
int mtrr_add (unsigned long base, unsigned long size, unsigned int type, char increment);
```





#### 参数

#### 参数

- base: 区域的物理基地址
- size: 区域的物理大小
- type: 所需的 MTRR 类型
- increment: 如果为真，则对该区域进行使用计数

#### 描述

内存类型区域寄存器（MTRR）控制较新的 Intel 和非 Intel 处理器上的缓存。此函数允许驱动程序请求添加一个 MTRR。每个处理器实现的细节和硬件特定之处对调用者隐藏，但尽管如此，调用者应预期提供一个 2 的幂大小并对齐到相应的 2 的幂边界。

如果无法添加区域（所有区域均在使用或 CPU 不支持），则返回负值。成功时，返回该条目的的寄存器编号，但应仅将其视为令牌（cookie）。

在多处理器机器上，更改将应用于所有处理器。在 x86 架构上，这是 Intel 处理器的要求。

可用类型有：

- MTRR_TYPE_UNCACHABLE - 不缓存
- MTRR_TYPE_WRBACK - 随时以突发写回数据
- MTRR_TYPE_WRCOMB - 尽快写回数据但允许突发
- MTRR_TYPE_WRTHROUGH - 缓存读取但不写入

# 缺陷

需要一个静默标志（quiet flag），用于驱动程序不在乎失败且不希望发送系统日志消息的情况。

# mtrr_del

#### 名称

mtrr_del — 删除内存类型区域

# 签 /

```
int mtrr_del (int reg, unsigned long base, unsigned long size);
```

#### 参数

- reg: mtrr_add 返回的寄存器
- base: 物理基地址
- size: 区域大小

#### 描述

如果提供了寄存器，则忽略 base 和 size。这是驱动程序应该调用它的方式。

释放一个 MTRR 区域。如果使用计数降为零，则寄存器被释放，区域恢复默认状态。成功时返回寄存器，失败时返回负错误代码。

# 10.3. PCI 支持库

# pci_find_slot

#### 名称

pci_find_slot — 从给定的 PCI 插槽定位 PCI 设备

# 签 /

```
struct pci_dev * pci_find_slot (unsigned int bus, unsigned int devfn);
```

#### 参数

- bus: 目标 PCI 设备所在的 PCI 总线编号
- devfn: 编码了目标 PCI 设备所在的 PCI 插槽号，以及在多功能设备情况下该插槽内的逻辑设备号。

#### 描述

给定的 PCI 总线和插槽/功能号，在系统全局 PCI 设备列表中定位目标 PCI 设备。如果找到设备，则返回其数据结构体的指针。如果没有找到设备，则返回 NULL。

# pci_find_subsys

#### 名称

pci_find_subsys — 通过厂商/子厂商/设备/子设备 ID 开始或继续搜索 PCI 设备

# 签 /

```
struct pci_dev * pci_find_subsys (unsigned int vendor, unsigned int device, unsigned int ss_vendor, unsigned int ss_device, const struct pci_dev * from);
```

#### 参数

- vendor: 要匹配的 PCI 厂商 ID，或使用 PCI_ANY_ID 匹配所有厂商 ID
- device: 要匹配的 PCI 设备 ID，或使用 PCI_ANY_ID 匹配所有设备 ID
- ss_vendor: 要匹配的 PCI 子系统厂商 ID，或使用 PCI_ANY_ID 匹配所有厂商 ID
- ss_device: 要匹配的 PCI 子系统设备 ID，或使用 PCI_ANY_ID 匹配所有设备 ID
- from: 搜索中找到的上一个 PCI 设备，或为 NULL 表示新搜索。

#### 描述

遍历已知 PCI 设备列表。如果找到匹配 vendor、device、ss_vendor 和 ss_device 的 PCI 设备，则返回其设备结构体的指针。否则，返回 NULL。通过向 from 参数传递 NULL 开始新搜索。否则，如果 from 不为 NULL，则从全局列表中的下一个设备继续搜索。

# pci_find_device

#### 名称

pci_find_device — 通过厂商/设备 ID 开始或继续搜索 PCI 设备

# 签 /

```
struct pci_dev * pci_find_device (unsigned int vendor, unsigned int device, const struct pci_dev * from);
```

#### 参数

- vendor: 要匹配的 PCI 厂商 ID，或使用 PCI_ANY_ID 匹配所有厂商 ID
- device: 要匹配的 PCI 设备 ID，或使用 PCI_ANY_ID 匹配所有设备 ID
- from: 搜索中找到的上一个 PCI 设备，或为 NULL 表示新搜索。

#### 描述

遍历已知 PCI 设备列表。如果找到匹配 vendor 和 device 的 PCI 设备，则返回其设备结构体的指针。否则，返回 NULL。通过向 from 参数传递 NULL 开始新搜索。否则，如果 from 不为 NULL，则从全局列表中的下一个设备继续搜索。

# pci_find_class

#### 名称

pci_find_class — 通过类开始或继续搜索 PCI 设备

# 签 /

```
struct pci_dev * pci_find_class (unsigned int class, const struct pci_dev * from);
```

#### 参数

- class: 搜索具有类指定的 PCI 设备
- from: 搜索中找到的上一个 PCI 设备，或为 NULL 表示新搜索。

#### 描述

遍历已知 PCI 设备列表。如果找到匹配 `class` 的 PCI 设备，则返回其设备结构体的指针。否则，返回 NULL。通过向 `from` 参数传递 NULL 开始新搜索。否则，如果 *from* 不为 NULL，则从全局列表中的下一个设备继续搜索。

# pci_find_capability

#### 名称

pci_find_capability — 查询设备的容量

# 签 /

```
int pci_find_capability (struct pci_dev * dev, int cap);
```

#### 参数

- dev: 查询的设备
- cap: 容量代码

#### 描述

告知设备是否支持指定的容量。返回设备配置空间内请求容量的地址，如果不支持则返回 0。可能的 cap 值：

- PCI_CAP_PM 电源管理
- PCI_CAP_AGP 加速图形
- PCI_CAP_VPD 关键数据
- PCI_CAP_SLOT 插槽标识
- PCI_CAP_MSI 消息信号中断
- PCI_CAP_CHSWP PCI 热插拔

# pci_find_parent_resource

#### 名称

pci_find_parent_resource — 返回区域所属的父总线区域

# 签 /

```
struct resource * pci_find_parent_resource (const struct pci_dev dev, struct resource * res);
```

#### 参数

- dev: 资源的设备结构
- res: 需要查找的子资源记录

#### 描述

对于给定的区域，返回其所属的父总线区域，或其应从何处分配。

# pci_set_power_state

#### 名称

pci_set_power_state — 设置 PCI 设备的电源状态

# 签 /

```
int pci_set_power_state (struct pci_dev * dev, int state);
```

#### 参数

- dev: 要挂起的设备
- state: 进入的状态

#### 描述

使用设备配置空间中的电源管理功能转换到新的电源状态。

# 返回值

尝试进入比当前低的状态返回 -EINVAL。如果已经是请求的状态返回 0。如果设备不支持 PCI PM 返回 -EIO。如果成功更改电源状态返回 0。

# pci_save_state

#### 名称

pci_save_state — 在挂起前保存设备的 PCI 配置空间

# 签 /

```
int pci_save_state (struct pci_dev * dev, u32 * buffer);
```

#### 参数

- dev: 我们正在处理的设备
- buffer: 用于存储配置空间的缓冲区

#### 描述

buffer 必须足够容整个 PCI 2.2 配置空间（>= 64 字节）。

# pci_restore_state

#### 名称

pci_restore_state — 恢复保存的设备状态

# 签 /

```
int pci_restore_state (struct pci_dev * dev, u32 * buffer);
```

#### 参数

- dev: 我们正在处理的设备

# pci_enable_device

#### 名称

pci_enable_device — 在驱动程序使用前初始化设备

# 签 /

```
int pci_enable_device (struct pci_dev * dev);
```

#### 参数

- dev: 要初始化的设备

#### 描述

在驱动程序使用前初始化设备。请求低层代码启用 I/O 和内存。如果设备处于挂起状态，则唤醒它。注意，此函数可能会失败。





## pci_disable_device

# Name
pci_disable_device — 使用后禁用 PCI 设备

# Synopsis
```
void pci_disable_device (struct pci_dev * dev);
```

# Arguments
dev
要禁用的 PCI 设备

# Description
向系统信号该 PCI 设备已不再被系统使用。这仅涉及禁用 PCI 总线主控（bus-mastering），如果的话。

## pci_enable_wake

# Name
pci_enable_wake — 允许设备在挂起时生成 PME#

# Synopsis
```
int pci_enable_wake (struct pci_dev * dev, u32 state, int enable);
```

# Arguments
- dev: 要操作的 PCI 设备
- state: 设备当前状态。
- enable: 启用或禁用生成的标志位

# Description
设置设备 PM 能力集中的位位，以便在系统挂起时生成 PME#。

如果设备没有 PM 能力，则返回 -EIO。如果设备支持但无法生成唤醒事件，则返回 -EINVAL。操作成功则返回 0。

## pci_release_regions

# Name
pci_release_regions —释放预留的 PCI I/O 和内存资源

# Synopsis
```
void pci_release_regions (struct pci_dev * pdev);
```

# Arguments
pdev
之前通过 pci_request_regions 预留资源的 PCI 设备

# Description
释放之前通过成功调用 pci_request_regions 预留的所有 PCI I/O 和内存资源。仅在所有对 PCI 区域的使用停止后调用此函数。

## pci_request_regions

# Name
pci_request_regions — 预留 PCI I/O 和内存资源

# Synopsis
```
int pci_request_regions (struct pci_dev * pdev, char * res_name);
```

# Arguments
pdev
要预留资源的 PCI 设备
res_name
与资源关联的名称。

# Description
将与 PCI 设备 pdev 相关的所有 PCI 区域标记为由所有者 res_name 预留。除非此调用成功返回，否则不要访问 PCI 区域内的任何地址。

成功时返回 0，错误时返回 EBUSY。失败时还会打印一条警告消息。

## pci_match_device

# Name
pci_match_device — 判断 PCI 设备结构是否有匹配的 PCI 设备 ID 结构

# Synopsis
```
const struct pci_device_id * pci_match_device (const struct pci_device_id * ids, const struct pci_dev * dev);
```

# Arguments
ids
要搜索的 PCI 设备 ID 结构数组
dev
要匹配的 PCI 设备结构

# Description
供驱动程序使用，检查系统中存在的 PCI 设备是否在其支持设备列表中。返回匹配的 pci_device_id 结构，如果没有匹配则返回 NULL。

## pci_register_driver

# Name
pci_register_driver — 注册一个新的 PCI 驱动

# Synopsis
```
int pci_register_driver (struct pci_driver * drv);
```

# Arguments
drv
要注册的驱动结构

# Description
将驱动结构添加到已注册的驱动列表中。返回在注册期间被该驱动程序占用的 PCI 设备数量。即使返回值为 0，驱动程序仍保持注册状态。

## pci_unregister_driver

# Name
pci_unregister_driver — 注销一个 PCI 驱动

# Synopsis
```
void pci_unregister_driver (struct pci_driver * drv);
```

# Arguments
drv
要注销的驱动结构

# Description
从已注册的 PCI 驱动列表中删除该驱动结构，通过调用其负责的每个设备的 remove 函数为其提供一个清理机会，并将这些设备标记为无驱动状态。

## pci_insert_device

# Name
pci_insert_device — 插入热插设备

# Synopsis
```
void pci_insert_device (struct pci_dev * dev, struct pci_bus * bus);
```

# Arguments
- dev
要插入的设备
- bus
插入位置

# Description
向设备列表添加新设备并通知用户态 (/sbin/hotplug)。

## pci_remove_device

# Name
pci_remove_device — 移除热插设备

# Synopsis
```
void pci_remove_device (struct pci_dev * dev);
```

# Arguments
dev
要移除的设备

# Description
从设备列表中删除设备结构并通知用户态 (/sbin/hotplug)。

## pci_dev_driver

# Name
pci_dev_driver — 获取设备的 pci_dev_driver

# Synopsis
```
struct pci_driver * pci_dev_driver (const struct pci_dev * dev);
```

# Arguments
dev
要查询的设备

# Description
返回相应的 pci_driver 结构，如果该设备没有注册的驱动则返回 NULL。

## pci_set_master

# Name
pci_set_master — 为设备 dev 总线主控

# Synopsis
```
void pci_set_master (struct pci_dev * dev);
```

# Arguments
dev
设备

# Description
为设备 dev 总线主控。

## pci_setup_device

# Name
pci_setup_device — 填充设备

# Synopsis
```
int pci_setup_device (struct pci_dev * dev);
```

# Arguments
dev
设备

# Description
初始化设备配置 空间。成功返回 0，未知时返回 -1。

## pci_pool_create

# Name
pci_pool_create — 创建 PCI 内存池

# Synopsis
```
struct pci_pool * pci_pool_create (const char * name, struct pci_dev * pdev, size_t size, size_t align, int flags);
```

# Arguments
name
池名称
pdev
将进行 DMA 的设备
size
块大小
align
必须是 2 的幂
flags（并非都支持）

# Description
返回设备及其驱动程序可以直接访问的一致性映射。无法创建时返回空。

## pci_pool_alloc

# Name
pci_pool_alloc — 获取一致性内存

# Synopsis
```
void * pci_pool_alloc (struct pci_pool * pool, int mem_flags, dma_addr_t * handle);
```

# Arguments
pool
产生块的池
mem_flags：SLAB_KERNEL 或 SLAB_ATOMIC
handle：DMA 地址指针

# Description
返回当前未使用块的内核虚拟地址，并通过 handle 报告其 DMA 地址。如果无法分配内存块，则返回空。

## pci_pool_free

# Name
pci_pool_free — 将块放回 PCI 池

# Synopsis
```
void pci_pool_free (struct pci_pool * pool, void * vaddr, dma_addr_t dma);
```

# Arguments
- pool：持有块的 PCI 池
- vaddr：块虚拟地址
- dma：DMA 地址

# Description
调用者承诺在重新分配之前，设备或驱动都不会再次接触此块。

## pci_pool_destroy

# Name
pci_pool_destroy — 销毁 PCI 内存池

# Synopsis
```
void pci_pool_destroy (struct pci_pool * pool);
```

# Arguments
pool
要销毁的 PCI 池

# Description
调用者保证池中没有更多内存正在使用，且在此调用后不会有人尝试使用该池。

## 10.4. MCA 架构

### 10.4.1. MCA 设备函数

#### mca_find_adapter

# Name
mca_find_adapter — 扫描适配器

# Synopsis
```
int mca_find_adapter (int id, int start);
```

# Arguments
id
要搜索的 MCA 标识
start
起始槽位





# Description

在 MCA 配置中搜索与给定 16bit ID 匹配的适配器。第一次调用时 `start` 应设为零，随后的调用应传递上一次调用的返回值，直到返回 `MCA_NOTFOUND` 为止。

已禁用的适配器不会被报告。

## mca_find_unused_adapter

#### 名称

mca_find_unused_adapter — 扫描未使用的适配器

#### 概要

```
int mca_find_unused_adapter(int id, int start);
```

#### 参数

- id
  要搜索的 MCA 标识符

- start
  起始槽位

# Description

在 MCA 配置中搜索与给定 16bit ID 匹配的适配器。第一次调用时 `start` 应设为零，随后的调用应传递上一次调用的回价值，直到返回 `MCA_NOTFOUND` 为止。

被驱动程序占用的适配器和禁用的适配器不会被报告。因此，此函数允许驱动程序在某些卡可能已被驱动的情况下扫描更多的显卡。

## mca_read_stored_pos

#### 名称

mca_read_stored_pos — 从启动数据读取 POS 寄存器

#### 概要

```
unsigned char mca_read_stored_pos (int slot, int reg);
```

#### 参数

- slot
  要读取的槽位

- reg
  要读取的寄存器

# Description

获取内核在扫描 MCA 空间时启动时存储的 POS 值。返回寄存器值。缺失或无效的寄存器报告 0。

## mca_read_pos

#### 名称

mca_read_pos — 从显卡读取 POS 寄存器

#### 概要

```
unsigned char mca_read_pos (int slot, int reg);
```

#### 参数

- slot
  要读取的槽位

- reg
  要读取的寄存器

# Description

直接从硬件获取 POS 值以获得当前值。这比 `mca_read_stored_pos` 慢得多，并且可能不在中断文中调用。它透明地处理了板载设备所需的底层魔法。

## mca_write_pos

#### 名称

mca_write_pos — 从显卡写入 POS 寄存器（注：此处原文为read，应为write）

#### 概要

```
void mca_write_pos (int slot, int reg, unsigned char byte);
```

#### 参数

- slot
  要写入的槽位

- reg
  要写入的寄存器

- byte
  要写入 POS 寄存器的字节

# Description

直接从硬件存储一个 POS 值。通常情况下你不应该使用此函数，并且在此之前你应该对 MCA 总线有非常深入的了解。操作不当可能会损坏硬件。

此函数可能在中断文中未使用。

请注意，这在技术上是一件“坏事”（Bad Thing），IBM 的技术人员表示你应该只通过他们的工具来设置 POS 值。然而，像 3c523 等某些设备建议你写回一些数据以确保配置的一致性。
我是说 IBM 是的，但我希望我的驱动程序能正常工作。

此函数无法检查多个设备是否最终导致了相同的资源，所以如果有人搞砸了，你可能会看到“魔法烟雾”。

## mca_set_adapter_name

#### 名称

mca_set_adapter_name — 设置卡的描述

#### 概要

```
void mca_set_adapter_name (int slot, char* name);
```

#### 参数

- slot
  要命名的槽位

- name
  名称的文本字符串

# Description

此函数设置通过 `/proc` 报告的此适配器槽位的名称。这仅供用户参考。设置名称将删除任何之前的名称。

## mca_set_adapter_procfn

#### 名称

mca_set_adapter_procfn — 设置 /proc 回调函数

#### 概要

```
void mca_set_adapter_procfn (int slot, MCA_ProcFn procfn, void* dev);
```

#### 参数

- slot
  要配置的槽位

- procfn
  /proc 调用的回调函数

- dev
  传递给回调的设备信息

# Description

这为 `/proc/mca/slot?` 设置了一个回调。调用该函数时会带有缓冲区、槽位和设备指针（或某些等量信息的上下文信息，如果你愿意，也可以不传任何），并预期在缓冲区中放入有用信息。尽管如此在调用此函数之前，适配器的名称、ID 和 POS 寄存器已经打印了，所以不要重复操作。

当模块注销时，应该带有 `NULL` procfn 调用此函数，以防止内核崩溃或其他类似的糟糕情况。

## mca_is_adapter_used

#### 名称

mca_is_adapter_used — 检查是否被驱动程序占用

#### 概要

```
int mca_is_adapter_used (int slot);
```

#### 参数

- slot
  要检查的槽位

# Description

如果槽位已被驱动程序占用，则返回 1

## mca_mark_as_used

#### 名称

mca_mark_as_used — 占用一个 MCA 设备

#### 概要

```
int mca_mark_as_used (int slot);
```

#### 参数

- slot
  要占用的槽位

# FIXME

我们是否应该让它是线程安全的
为设备驱动程序占用一个 MCA 槽位。如果槽位已被占用，函数返回 1；如果未被占用，则占用并返回 0。

## mca_mark_as_unused

#### 名称

mca_mark_as_unused — 释放 MCA 设备

#### 概要

```
void mca_mark_as_unused (int slot);
```

#### 参数

- slot
  槽位

# Description

释放槽位。

## mca_get_adapter_name

#### 名称

mca_get_adapter_name — 获取适配器名称

#### 概要

```
char * mca_get_adapter_name (int slot);
```

#### 参数

- slot
  槽位

# Description

适配器的名称。

## mca_isadapter

#### 名称

mca_isadapter — 检查适配器是否存在

#### 概要

```
int mca_isadapter (int slot);
```

#### 参数

- slot
  槽位

# Description

如果适配器存在，返回 1

## mca_isenabled

#### 名称

mca_isenabled — 检查槽位是否启用

#### 概要

```
int mca_isenabled (int slot);
```

#### 参数

- slot
  槽位

# Description

如果槽位已启用，返回 1

## mca_enable_dma

#### 名称

mca_enable_dma — 启用 DMA

#### 概要

```
void mca_enable_dma (unsigned int dmanr);
```

#### 参数

- dmanr
  DMA 通道

# Description

DMA 控制器。

## mca_disable_dma

#### 名称

mca_disable_dma — 禁用 DMA

#### 概要

```
void mca_disable_dma (unsigned int dmanr);
```

#### 参数

- dmanr
  DMA 通道

# Description

DMA 控制器。

## mca_set_dma_addr

#### 名称

mca_set_dma_addr — 设置 24bit DMA 地址

#### 概要

```
void mca_set_dma_addr (unsigned int dmanr, unsigned int a);
```

#### 参数

- dmanr
  DMA 通道

- a
  24bit 地址

# Description

设置 DMA 控制器中的寄存器。

## mca_get_dma_addr

#### 名称

mca_get_dma_addr — 获取 24bit DMA 地址

#### 概要

```
unsigned int mca_get_dma_addr (unsigned int dmanr);
```

#### 参数

- dmanr
  DMA 通道

# Description

读取 DMA 控制器中的寄存器。

## mca_set_dma_count

#### 名称

mca_set_dma_count — 设置 16bit 传输计数

#### 概要

```
void mca_set_dma_count (unsigned int dmanr, unsigned int count);
```

#### 参数

- dmanr
  DMA 通道

- count
  计数

# Description

设置该通道的 DMA 计数。最大为 64KB。将计数设置为 0 不符合你的预期。

## mca_get_dma_residue

#### 名称

mca_get_dma_residue — 获取剩余传输字节

#### 概要

```
unsigned int mca_get_dma_residue (unsigned int dmanr);
```

#### 参数

- dmanr
  DMA 通道

# Description

该 DMA 通道剩余传输的字节数。

## mca_set_dma_io

#### 名称

mca_set_dma_io — 设置 I/O 传输端口

#### 概要

```
void mca_set_dma_io (unsigned int dmanr, unsigned int io_addr);
```

#### 参数

- dmanr
  DMA 通道

- io_addr
  I/O 端口号

# Description 与 ISA 总线 DMA 控制器不同，MCA 的 DMA 可以与 I/O 端口进行传输。

## mca_set_dma_mode

#### 名称

mca_set_dma_mode — 设置 DMA 模式

#### 概要

```
void mca_set_dma_mode (unsigned int dmanr, unsigned int mode);
```





#### 参数

dmanr

DMA 通道

mode

设置模式

#### 描述

DMA 控制器支持多种模式。你可以设置的模式值包括：

- 当从 DMA 设备读取时使用 MCA_DMA_MODE_READ。

## 第 11 章 设备文件系统

## devfs_register

#### 名称
devfs_register — 注册一个设备条目。

#### 概要

```
devfs_handle_t devfs_register (devfs_handle_t dir, const char * name, unsigned int flags, unsigned int major, unsigned int minor, umode_t mode, * ops, void * info);
```

#### 参数

dir
父 devfs 目录条目的句柄。如果此为 NULL，则新名称相对于 devfs 的根目录。

name
条目的名称。

flags
一组按位或组合的标志 (DEVFS_FL_*)。

major
设备号。普通文件不需要。

minor
次设备号。普通文件不需要。

mode
默认文件模式。

ops
&file_operations 或 &block_device_operations 结构体。此不能在外部释放内存。

info
一个任意指针，将写入传递给设备驱动程序文件结构体的 private_data 字段中。你可以将其设置为任何想要的值，并在文件打开时对其进行更改（下一个打开的文件将不会看到此更改）。

#### 描述
返回一个句柄，该句柄后续可以用于调用 devfs_register。失败时返回 NULL。

## devfs_unregister

#### 名称
devfs_unregister — 取消注册一个设备条目。

#### 概要

```
void devfs_unregister (devfs_handle_t de);
```

#### 参数

de
之前由 devfs_register 创建或从 devfs_find_handle 返回的句柄。如果此为 NULL，则程序不执行任何操作。

## devfs_mk_symlink

#### 名称
devfs_mk_symlink —

#### 概要

```
int devfs_mk_symlink (devfs_handle_t dir, const char * name, unsigned int flags, const char * link, devfs_handle_t * handle, void * info);
```

#### 参数

dir
父 devfs 目录条目的句柄。如果此为 NULL，则新名称相对于 devfs 的根目录。

name
条目的名称。

flags
一组按位或组合的标志 (DEVFS_FL_*)。

link
目标名称。

handle
符号链接条目的句柄将写入此处。此处可能为 NULL。

info
一个将与条目关联的任意指针。

#### 描述
成功时返回 0，否则返回负错误代码。

## devfs_mk_dir

#### 名称
devfs_mk_dir — 在 devfs 命名空间中创建一个目录。

#### 概要

```
devfs_handle_t devfs_mk_dir (devfs_handle_t dir, const char * name, void * info);
```

#### 参数

dir
父 devfs 目录条目的句柄。如果此为 NULL，则新名称相对于 devfs 的根目录。

name
条目的名称。

info
一个将与条目关联的任意指针。

#### 描述
使用此函数是可选的。devfs_register 函数会根据需要自动创建中间目录。提供此函数是为了效率考虑，因为它提供了一个目录的句柄。返回一个句柄，该句柄后续可以用于调用 devfs_unregister。失败时返回 NULL。

## devfs_find_handle

#### 名称
devfs_find_handle — 查找 devfs 条目的句柄。

#### 概要

```
devfs_handle_t devfs_find_handle (devfs_handle_t dir, const char * name, unsigned int major, unsigned int minor, char type, int traverse_symlinks);
```

#### 参数

dir
父 devfs 目录条目的句柄。如果此为 NULL，则名称相对于 devfs 的根目录。

name
条目的名称。

major
设备号。如果 name 为 NULL 则使用此。

minor
次设备号。如果 name 为 NULL 则使用此。

type
要查找的特殊文件类型。可以是 DEVFS_SPECIAL_CHR 或 DEVFS_SPECIAL_BLK。

traverse_symlinks
如果为 TRUE，则遍历 devfs 命名空间中的符号链接条目。指向 devfs 命名空间的符号链接会导致失败。遍历符号链接会消耗栈空间。

#### 描述
返回一个句柄，该句柄后续可以用于调用 devfs_unregister、devfs_get_flags 或 devfs_set_flags。失败时返回 NULL。

## devfs_get_flags

#### 名称
devfs_get_flags — 获取 devfs 条目的标志。

#### 概要

```
int devfs_get_flags (devfs_handle_t de, unsigned int * flags);
```

#### 参数

de
设备条目的句柄。

flags
标志将写入此处。

#### 描述
成功时返回 0，否则返回负错误代码。

## devfs_get_maj_min

#### 名称
devfs_get_maj_min — 获取 devfs 条目的设备号和次设备号。

#### 概要

```
int devfs_get_maj_min (devfs_handle_t de, unsigned int * major, unsigned int * minor);
```

#### 参数

de
设备条目的句柄。

major
设备号将写入此处。可能为 NULL。

minor
次设备号将写入此处。可能为 NULL。

#### 描述
成功时返回 0，否则返回负错误代码。

## devfs_get_handle_from_inode

#### 名称
devfs_get_handle_from_inode — 获取 VFS inode 的 devfs 句柄。

#### 概要

```
devfs_handle_t devfs_get_handle_from_inode (struct inode * inode);
```

#### 参数

inode
VFS inode。

#### 描述
成功时返回 devfs 句柄，否则返回 NULL。

## devfs_generate_path

#### 名称
devfs_generate_path — 生成相对于 devfs 根目录的条目路径。

#### 概要

```
int devfs_generate_path (devfs_handle_t de, char * path, int buflen);
```

#### 参数

de
devfs 条目。

用于写入路径的缓冲区。缓冲区末尾将写入 '\0' 终止符。

buflen
缓冲区的长度。

#### 描述
成功时返回缓冲区中路径起始的偏移量，否则返回负错误代码。

## devfs_get_ops

#### 名称
devfs_get_ops — 获取 devfs 条目的操作集。

#### 概要

```
void * devfs_get_ops (devfs_handle_t de);
```

#### 参数

de
devfs 条目的句柄。

#### 描述
成功时返回操作指针，否则返回 NULL。

## devfs_set_file_size

#### 名称
devfs_set_file_size — 设置 devfs 文件的大小。

#### 概要

```
int devfs_set_file_size (devfs_handle_t de, unsigned long size);
```

#### 参数

de
devfs 条目的句柄。

size
文件大小。

#### 描述
成功时返回 0，否则返回负错误代码。

## devfs_get_info

#### 名称
devfs_get_info — 获取写入 private_data 的 info。

#### 概要

```
void * devfs_get_info (devfs_handle_t de);
```

#### 参数

de
devfs 条目的句柄。

#### 描述
返回 info 指针。

## devfs_set_info

#### 名称
devfs_set_info — 设置写入 private_data 的 info。

#### 概要

```
int devfs_set_info (devfs_handle_t de, void * info);
```

#### 参数

de
devfs 条目的句柄。

info
info 数据。

#### 描述
成功时返回 0，否则返回负错误代码。

## devfs_get_parent

#### 名称
devfs_get_parent — 获取父设备条目。

#### 概要

```
devfs_handle_t devfs_get_parent (devfs_handle_t de);
```

#### 参数

de
devfs 条目的句柄。

#### 描述
成功时返回父设备条目，否则返回 NULL。

## devfs_get_first_child

#### 名称
devfs_get_first_child — 获取目录中的第一个子节点。

#### 概要

```
devfs_handle_t devfs_get_first_child (devfs_handle_t de);
```

#### 参数

de
devfs 条目的句柄。

#### 描述
成功时返回子节点条目，否则返回 NULL。

## devfs_get_next_sibling

#### 名称
devfs_get_next_sibling — 获取设备条目的下一个兄弟节点。

#### 概要

```
devfs_handle_t devfs_get_next_sibling (devfs_handle_t de);
```

#### 参数

de
devfs 条目的句柄。

#### 描述
成功时返回兄弟节点条目，否则返回 NULL。

## devfs_auto_unregister

#### 名称
devfs_auto_unregister — 配置一个自动取消注册的 devfs 条目。

#### 概要

```
void devfs_auto_unregister (devfs_handle_t master, devfs_handle_t slave);
```

#### 参数

master
主 devfs 条目。只能注册一个从节点。

slave
当主条目取消注册时会自动取消注册的 devfs 条目。对该条目调用 devfs_unregister 是非法的。

## devfs_get_unregister_slave

#### 名称
devfs_get_unregister_slave — 获取将自动取消注册的从条目。

#### 概要

```
devfs_handle_t devfs_get_unregister_slave (devfs_handle_t master);
```

#### 参数

master
主 devfs 条目的句柄。





#### 参数

master

master devfs 条目。

#### 描述

返回在 master 被注销时将取消注销的从设备（slave）。

## devfs_get_name

### 名字

devfs_get_name — 获取设备条目在其父目录中的名称。

#### 概要

```
const char * devfs_get_name (devfs_handle_t de, unsigned int * namelen);
```

#### 参数

de

设备条目的句柄。

namelen

名称长度将写入此处。此值可能为 NULL。

#### 描述

成功时返回名称，否则返回 NULL。

## devfs_register_chrdev

### 名字

devfs_register_chrdev — 可选注册一个常规字符驱动程序。

#### 概要

```
int devfs_register_chrdev (unsigned int major, const char * name, struct file_operations * fops);
```

#### 参数

major

驱动的主设备号。

name

驱动的名称（在 /proc/devices 中可见）。

fops

&file_operations 结构体指针。

#### 描述

如果在启动时未提供“devfs=only”选项，此函数将注册一个字符驱动程序。成功返回 0，失败则返回负错误代码。

## devfs_register_blkdev

### 名字

devfs_register_blkdev — 可选注册一个常规块驱动程序。

#### 概要

```
int devfs_register_blkdev (unsigned int major, const char * name, struct block_device_operations * bdops);
```

#### 参数

major

驱动的主设备号。

name

驱动的名称（在 /proc/devices 中可见）。

bdops

&block_device_operations 结构体指针。

#### 描述

如果在启动时未提供 "devfs=only"选项，此函数将注册一个块驱动程序。成功返回 0，失败则返回负错误代码。

## devfs_unregister_chrdev

### 名字

devfs_unregister_chrdev — 可选注销一个常规字符驱动程序。

#### 概要

```
int devfs_unregister_chrdev (unsigned int major, const char * name);
```

#### 参数

major

驱动的主设备号。

name

驱动的名称（在 /proc/devices 中可见）。

#### 描述

如果在启动时未提供 "devfs=only"选项，此函数将注销一个字符驱动程序。成功返回 0，失败则返回负错误代码。

## devfs_unregister_blkdev

### 名字

devfs_unregister_blkdev — 可选注销一个常规块驱动程序。

#### 概要

```
int devfs_unregister_blkdev (unsigned int major, const char *
name);
```

#### 参数

major

驱动的主设备号。

name

驱动的名称（在 /proc/devices 中可见）。

#### 描述

如果在启动时未提供 "devfs=only"选项，此函数将注销一个块驱动程序。成功返回 0，失败则返回负错误代码。

## 第12章 电电源管理

## pm_register

### 名字

pm_register — 向电源管理注册一个设备

#### 概要

```
struct pm_dev * pm_register (pm_dev_t type, unsigned long id,
      pm_callback callback);
```

#### 参数

- type: 设备类型
- id: 设备 ID
- callback: 回调函数

#### 描述

将设备添加到希望接收电源管理事件通知的设备列表中。成功时返回 &pm_dev 结构体，失败时返回 NULL。

回调函数将在进程上下文中调用，并且它可能会睡眠。

## pm_unregister

### 名字

pm_unregister — 从电源管理中注销一个设备

#### 概要

```
void pm_unregister (struct pm_dev * dev);
```

#### 参数

dev
要注销的设备

#### 描述

从电源管理通知列表中移除设备。传递的 dev 必须是之前由 pm_register 返回的句柄。

## pm_unregister_all

### 名字

pm_unregister_all — 注销所有具有匹配回调的设备

#### 概要

```
void pm_unregister_all (pm_callback callback);
```

#### 参数

- callback: 回调函数指针

#### 描述

注销所有会调用所传回调的设备。这主要用于可加载模块提供一个辅助函数。它允许模块放弃其管理的所有设备，而无需保留自己的私有列表。

## pm_send

### 名字

pm_send — 向单个设备发送请求

#### 概要

```
int pm_send (struct pm_dev * dev, pm_request_t rqst, void * data);
```

#### 参数

- dev: 要发送到的设备
- rqst: 电源管理请求
- data: 回调函数的数据

#### 描述

向给定设备发布电源管理请求。PM_SUSPEND 和 PM_RESUME 事件会被特殊处理。data 字段必须持有预期的下一个状态。如果状态匹配，则不调用。

## BUG

什么能阻止两个电源管理请求并行发生并冲突。

## 警告

通常不建议直接调用 pm_send，特别是没有防止 pm_dev 消失的锁。调用者必须维护所有必要的锁，或者了解“lustre 内部”安全性。此外，请记住，此函数没有针对 pm_unregister 加锁。这意味着你必须处理回调执行时的 SMP 竞态并进行卸载自己。

## pm_send_all

### 名字

pm_send_all — 向所有管理的设备发送请求

#### 概要

```
int pm_send_all (pm_request_t rqst, void * data);
```

#### 参数

rqst

电源管理请求

data

回调函数的数据

#### 描述

向所有设备发布电源管理请求。PM_SUSPEND 事件会被特殊处理。任何设备都可以通过从回调返回非零（错误）值来阻止挂起。

## 警告

此函数持有 dev_lock，并在回调执行完成前不会释放。这防止了针对电源函数和模块卸载的竞态。

成功时返回零。如果挂起失败，则返回设备状态。

## pm_find

### 名字

pm_find — 查找设备

#### 概要

```
struct pm_dev * pm_find (pm_dev_t type, struct pm_dev * from);
```

#### 参数

type

设备类型

from

开始位置

#### 描述

扫描特定类型设备的电源管理列表。返回的设备可以传递给后续调用。NULL 表示列表结束。

要从开始搜索，请将 NULL 作为 from 值。

调用者在调用此函数时必须持有 pm_devs_lock。一旦释放锁，返回的所有指针可能会失效。

## 第13章 块设备

## blk_cleanup_queue

### 名字

blk_cleanup_queue — 在不再需要时释放 request_queue_t

#### 概要

```
void blk_cleanup_queue (request_queue_t * q);
```

#### 参数

q
要释放的请求队列

#### 描述

blk_cleanup_queue 与 blk_init_queue 配对。它在请求队列被释放时调用；通常在块设备被注销时。目前，它的主要任务是释放分配给队列的所有 struct request 结构。

#### 注意

希望底层驱动程序已完成任何请求...

## blk_queue_headactive

### 名字

blk_queue_headactive — 指示请求队列头部可以是活跃的

#### 概要

```
void blk_queue_headactive (request_queue_t * q, int active);
```

#### 参数

q

应用于此的队列。

active

队列头部活跃的标志指示。

#### 描述

块设备的驱动程序可能选择将当前活跃的请求留在请求队列中，直到它完成后才移除。队列处理程序出于安全考虑默认假设这一点，并在队列拔出（因此可能正在处理此特定请求）时，将请求队列头部包含在任何请求的合并或重排序中。

如果驱动程序在处理之前从请求队列中移除请求，那么它可能指示队列头部参与合并和重排序。这是通过调用 blk_queue_headactive 且活跃标志为 0 实现的。





## 第13章 块设备

当队列被插入（plugged）时，头部将被假设为非活动状态。

### blk_queue_make_request

#### 名称
blk_queue_make_request — 为设备定义备选的 make_request 函数

#### 概要
```
void blk_queue_make_request (request_queue_t * q, make_request_fn * mfn);
```

#### 参数
- q: 受影响的设备请求队列
- mfn: 备选的 make_request 函数

#### 描述
将 &buffer_heads 传递给设备驱动程序的常规方法是将它们收集到请求队列中，并允许设备驱动程序在准备就绪时从该队列中选择请求。这对于许多块设备都是有效的。然而，某些块设备（通常是如 md 或 lvm 等虚拟设备）并不能从请求队列的处理中获益，通过直接将请求传递给它们来提供服务效果更好。这可以通过向 blk_queue_make_request 提供一个函数来实现。

# 注意事项
执行此操作的驱动程序*必须*能够适当地处理“高内存”（highmemory）中的缓冲区，方法可以是调用 bh_kmap 获取内核映射，或者通过调用 create_bounce 在普通内存中创建缓冲区。

### blk_init_queue

#### 名称
blk_init_queue — 为块设备准备使用的请求队列

#### 概要
```
void blk_init_queue (request_queue_t * q, request_fn_proc * rfn);
```

#### 参数
- q: 需要初始化的 &request_queue_t
- rfn: 调用以处理已放入队列的请求的函数。

#### 描述
如果块设备希望使用标准的请求处理程序（该程序会对请求排序并合并相邻请求），则它必须调用 `blk_init_queue`。当队列上有需要处理的请求时，将调用函数 `rfn`。如果设备支持插入（plugging），当队列中有可用请求时，`rfn` 可能不会立即调用，而可能在稍后的某个时间被调用。当需要队列中某个请求的缓冲区，或由于内存压力时，已插入的设备通常会被拔出（unplugged）。

`rfn` 并不要求也不被期望移除队列上的所有请求，而只需移除它一次能处理的请求。如果它在队列中留下了请求，则它负责安排这些请求最终被处理。

在操作队列上的请求时，必须持有全局自旋锁 `io_request_lock`。

队列头部请求默认被假设为可能活跃，每当通用队列被拔出时，它都不会被考虑重新排序或合并。这种行为可以通过 `blk_queue_headactive` 进行更改。

#### 注意
当块设备被禁用时（例如在模块卸载时），`blk_init_queue` 必须与 `blk_cleanup_queue` 调用配对。

### generic_make_request

#### 名称
generic_make_request —

#### 概要
```
void generic_make_request (int rw, struct buffer_head * bh);
```

#### 参数
- rw: READ, WRITE 或 READA - 所需的 I/O 类型。
- bh: 描述内存和设备上位置的缓冲区头（buffer head）。

#### 描述
generic_make_request 用于向块设备发出 I/O 请求。它接收一个 &struct buffer_head 和一个 &rw 值。READ 和 WRITE 选项的含义（很显然）是易懂的。READ 值意味着需要读取，但如果驱动程序无法立即获取资源，可以自由地让请求失败。generic_make_request 不返回任何状态。请求的成功/失败状态以及完成通知将通过在（别处）描述的 bh->b_end_io 函数异步交付。

调用 generic_make_request 的调用者必须确保 b_page、b_addr、b_size 已设置以描述内存缓冲区，b_dev 和 b_rsector 已设置以描述设备地址，并且 b_end_io 和可选的 b_private 已描述如何发出完成通知。还应该设置 BH_Mapped（以确认 b_dev 和 b_blocknr 请求）。

generic_make_request 及其调用的驱动程序使用 b_reqnext，并可能会更改 b_dev 和 b_rsector。在调用 generic_make_request 之后，**不应**依赖这些字段的值。由于此原因，调用者应该在调用 generic_make_request 之前在 b_dev 和 b_blocknr 中记录设备地址信息，而不应记录其他字段，特别是 generic_make_request 或任何低层驱动程序都不会更改其他标志位。

除了上述字段外，generic_make_request 或任何低层驱动程序都不会更改其他字段，特别是其他其他标志位。

### submit_bh

#### 名称
submit_bh —

#### 概要
```
void submit_bh (int rw, struct buffer_head * bh);
```

#### 参数
- rw: 是否 READ 还是 WRITE，或者可能是 READA（预读）
- bh: 描述 I/O 的 &struct buffer_head

#### 描述
submit_bh 的目的与 generic_make_request 非常相似，并使用该函数来完成大部分工作。

submit_bh 提供的额外功能是根据 b_blocknr 和 b_size 确定 b_rsector，并从 b_dev 设置 b_rdev。这对于来自缓冲区缓存和页缓存的 I/O 请求是合适的，因为这些请求（目前）始终使用对齐的块。

### ll_rw_block

#### 名称
ll_rw_block — 块设备的访问

#### 概要
```
void ll_rw_block (int rw, int nr, struct buffer_head * bhs);
```

#### 参数
- rw: 是否 READ 还是 WRITE，或者可能是 READA（预读）
- nr: &struct buffer_head 的数量
- bhs: &struct buffer_head 指针数组

#### 描述
ll_rw_block 接收 &struct buffer_head 指针数组并执行 I/O 操作。这对于来自缓冲区缓存和页缓存的 I/O 请求是合适的，因为这些请求（目前）始终使用对齐的块。

该函数提供了 generic_make_request 不具备的额外功能。它标记 b_end_io 为有效（如果适用），解锁缓冲区并唤醒等待者。需要更感兴趣例的客户端应直接调用 submit_bh（或 generic_make_request）。

### end_request_first

#### 名称
end_request_first — 完成缓冲区的 I/O

#### 概要
```
int end_request_first (struct request * req, int uptate, char * name);
```

#### 参数
- req: 正在处理的请求
- uptate: 0 表示 I/O 错误

#### 描述
完成 `req` 上的第一个缓冲区的 I/O，并为簇中的下一个缓冲区做好准备。

# 返回
0 - 我们已完成此请求，调用 `end_request_last`
1 - 此请求仍有挂起的缓冲区

# 注意事项
用于 I/O 错误的名称

## 第14章 杂项设备

### misc_register

#### 名称
misc_register — 注册杂项设备

#### 概要
```
int misc_register (struct miscdevice * misc);
```

#### 参数
- misc: 设备结构

#### 描述
向内核注册杂项设备。如果设备号设置为 MISC_DYNAMIC_MINOR，将分配一个设备号并放入结构的 minor 字段中。其他情况下使用请求的设备号。

传递的结构被链接到内核，在注销之前不会销毁。

成功返回零，失败时返回负错误码。

### misc_deregister

#### 名称
misc_deregister — 取消注册杂项设备

#### 概要
```
int misc_deregister (struct miscdevice * misc);
```

#### 参数
- misc: 要注销的设备

#### 描述
注销之前通过 misc_register 注册的杂项设备。成功由零表示，负错误码表示错误。

## 第15章 Video4Linux

### video_unregister_device

#### 名称
video_unregister_device — 取销 video4linux 设备

#### 概要
```
void video_unregister_device (struct video_device * vfd);
```

#### 参数
- vfd: 要注销的设备

#### 描述
此函数注销传递的设备并取消分配的设备号。未来的打开调用将遇到错误。





## 第16章. 音频设备

### register_sound_special

#### 名称
register_sound_special — 注册一个特殊的音频节点

#### 概要
```
int register_sound_special (struct file_operations * fops, int unit);
```

#### 参数
- * fops
  驱动程序的文件操作
- * unit
  要分配的单元号

#### 描述
从音频子系统通过设备号分配一个特殊的音频设备。成功时返回分配的编号。失败时返回负数错误代码。

## register_sound_mixer

#### 名称
register_sound_mixer — 注册一个混音器设备

#### 概要
```
int register_sound_mixer (struct file_operations * fops, int dev);
```

#### 参数
- * fops
驱动程序的文件操作
- * dev
要分配的单元号

#### 描述
分配一个混音器。Unit 是请求的混音器编号。传递 -1 请求下一个空闲混音器单元。成功时返回分配的编号，失败时返回负数错误代码。

## register_sound_midi

#### 名称
register_sound_midi — 注册一个 midi 设备

#### 概要
```
int register_sound_midi (struct file_operations * fops, int dev);
```

#### 参数
- * fops
驱动程序的文件操作
- * dev
要分配的单元号

#### 描述
分配一个 midi 设备。Unit 是请求的 midi 设备编号。传递 -1 请求下一个空闲的 midi 单元。成功时返回分配的编号，失败时返回负数错误代码。

## register_sound_dsp

#### 名称
register_sound_dsp — 注册一个 DSP 设备

#### 概要
```
int register_sound_dsp (struct file_operations * fops, int dev);
```

#### 参数
- fops
驱动程序的文件操作
- dev
要分配的单元号

#### 描述
分配一个 DSP 设备。Unit 是请求的 DSP 编号。传递 -1 请求下一个空闲的 DSP 单元。成功时返回分配的编号，失败时返回负数错误代码。

此函数同时分配音频和 dsp 设备条目，并始终将它们作为配对分配 -例如 dsp3/audio3

## register_sound_synth

#### 名称
register_sound_synth — 注册一个合成器设备

#### 概要
```
int register_sound_synth (struct file_operations * fops, int dev);
```

#### 参数
- fops
驱动程序的文件操作
- dev
要分配的单元号

#### 描述
分配一个合成器设备。Unit 是请求的合成器设备编号。传递 -1 请求下一个空闲的合成器单元。成功时返回分配的编号，失败时返回负数错误代码。

## unregister_sound_special

#### 名称
unregister_sound_special — 取注销一个特殊的音频设备

#### 概要
```
void unregister_sound_special (int unit);
```

#### 参数
- unit
要释放的单元号

#### 描述
释放通过 `register_sound_special` 分配的音频设备。传递的 unit 是注册函数的返回值。

## unregister_sound_mixer

#### 名称
unregister_sound_mixer — 取注销一个混音器

#### 概要
```
void unregister_sound_mixer (int unit);
```

#### 参数
- unit
要释放的单元号

#### 描述
释放通过 `register_sound_mixer` 分配的音频设备。传递的 unit 是注册函数的返回值。

## unregister_sound_midi

#### 名称
unregister_sound_midi — 取注销一个 midi 设备

#### 概要
```
void unregister_sound_midi (int unit);
```

#### 参数
- unit
要释放的单元号

#### 描述
释放通过 `register_sound_midi` 分配的音频设备。传递的 unit 是注册函数的返回值。

## unregister_sound_dsp

#### 名称
unregister_sound_dsp — 取注销一个 DSP 设备

#### 概要
```
void unregister_sound_dsp (int unit);
```

#### 参数
- unit
要释放的单元号

#### 描述
释放通过 `register_sound_dsp` 分配的音频设备。传递的 unit 是注册函数的返回值。

两个分配的单元会被自动同时释放。

## unregister_sound_synth

#### 名称
unregister_sound_synth — 取注销一个合成器设备

#### 概要
```
void unregister_sound_synth (int unit);
```

#### 参数
- unit
要释放的单元号

#### 描述
释放通过 `register_sound_synth` 分配的音频设备。传递的 unit 是注册函数的返回值。

## 第17章. USB 设备

### usb_register

#### 名称
usb_register — 注册一个 USB 驱动

#### 概要
```
int usb_register (struct usb_driver * new_driver);
```

#### 参数
- new_driver
驱动程序的 USB 操作

#### 描述
向 USB 核心注册 USB 驱动程序。每当添加新驱动程序时，未连接的接口列表将重新扫描，允许新驱动程序绑定到任何识别出的设备。失败时返回负错误代码，成功时返回 0。

## usb_scan_devices

#### 名称
usb_scan_devices — 扫描所有未声明的接口

#### 概要
```
void usb_scan_devices (void);
```

#### 参数
- void

#### 描述
遍历所有未声明的接口，通过 USB 核心将其提供所有已注册的驱动程序。这由其中一个子驱动程序在 `usb_register` 之后调用。

## usb_deregister

#### 名称
usb_deregister — 取注销一个驱动程序

#### 概要
```
void usb_deregister (struct usb_driver * driver);
```

#### 参数
- driver
驱动程序的 USB 操作

#### 描述
从内部驱动列表中解除与指定驱动程序的链接。

## usb_alloc_bus

#### 名称
usb_alloc_bus — 创建一个新的主机控制器结构

#### 概要
```
struct usb_bus * usb_alloc_bus (struct usb_operations * op);
```

#### 参数
- op
该总线结构应使用的 `usb_operations` 指针

#### 描述
创建一个具有指定 `usb_operations` 的主机控制器总线并初始化所有必要的对象。（仅供 USB 控制器驱动程序使用。）如果没有可用内存，返回 NULL。调用者在完成对结构的使用后应调用 `usb_free_bus`。

## usb_free_bus

#### 名称
usb_free_bus — 释放总线使用的内存

#### 概要
```
void usb_free_bus (struct usb_bus * bus);
```

#### 参数
- bus
要释放的总线指针

#### 描述
（仅供 USB 控制器驱动程序使用。）

## usb_register_bus

#### 名称
usb_register_bus — 向 USB 核心注册 USB 主机控制器

#### 概要
```
void usb_register_bus (struct usb_bus * bus);
```

#### 参数
- * bus
要注册的总线指针

#### 描述
（仅供 USB 控制器驱动程序使用。）

## usb_deregister_bus

#### 名称
usb_deregister_bus — 取注销 USB 主机控制器

#### 概要
```
void usb_deregister_bus (struct usb_bus * bus);
```

#### 参数
- bus
要注销的总线指针

#### 描述
（仅供 USB 控制器驱动程序使用。）

## usb_match_id

#### 名称
usb_match_id — 匹配设备或接口的 usb_device_id

#### 概要

#### 参数
- dev
  匹配时考虑的设备描述
- interface
  感兴趣的接口
- id
  usb_device_id 结构数组，以零项结束

#### 描述
usb_match_id 搜索 `usb_device_id` 数组并返回第一个匹配设备或接口的项，或返回空。这用于将驱动绑定（重新绑定）到接口。大多数 USB 设备驱动程序通过 USB 核心间接使用此函数，但某些驱动框架直接使用。这些设备表通过 `MODULE_DEVICE_TABLE`、`modutils` 和 `modules.usbmap` 导出，以支持 USB 热插的驱动加载功能。

# 匹配规则

`usb_device_id` 中的 `match_flags` 元素控制使用哪些成员。如果相应的位被设置，则 `device_id` 中的值必须与设备或接口描述中对应的成员匹配，否则 `device_id` 不匹配。`driver_info` 通常仅供设备驱动程序使用，但如果你提供，可以为驱动程序的 `modules.usbmap` 条目创建一个通配符“匹配任何内容”的 `usb_device_id`。





一个仅包含非零“driver_info”字段的 id。如果你这样做，USB 设备驱动的探测程序（probe routine）应该使用额外的智能逻辑来决定是否绑定到指定的接口。

## 什么是良好的 usb_device_id 表

匹配算法非常简单，因此驱动程序选择的智能性必须来自智能的驱动 id 记录。除非你有充分理由使用其他选择策略，否则请仅在相关的组中提供匹配元素，并按照从特定到一般的顺序排列指定符。如果可以，请使用为此目的提供的宏。

最特定的指定符使用设备描述符数据。这些通常用于特定特定的匹配；`USB_DEVICE` 宏允许你提供厂商和 ID，你也可以针对产品修订版本的范围进行匹配。这些被广泛用于具有特定应用程序或厂商特定 `bDeviceClass` 值的设备。

基于设备类/子类/协议规范的匹配稍微通用一些；使用 `USB_DEVICE_INFO` 宏或其同类宏。这些用于单功能设备，在这些设备中 `bDeviceClass` 不会指定每个接口都有自己的类。

基于接口类/子类/协议的匹配是最通用的；它们允许驱动程序绑定到多功能设备上的任何接口。使用 `USB_INTERFACE_INFO` 宏或其同类宏来匹配按接口分类的设备（如在 `bDeviceClass` 中记录的）。

在这些组中，请记住并非所有组合都有意义。例如，不要在没有厂商和产品 ID 的情况下提供产品版本范围；或者在没有关联类和子类的情况下指定协议。

## usb_alloc_urb

### 名字
usb_alloc_urb — 为 USB 驱动程序创建一个新的 urb

#### 概要
```
urb_t * usb_alloc_urb (int iso_packets);
```

#### 参数
iso_packets
此 urb 的等时数据包（iso packets）数量

#### 描述
创建一个供 USB 驱动程序使用的 urb 并返回其指针。如果没有可用内存，则返回 NULL。
如果驱动程序想要将此 urb 用于中断、控制或批量端点，请将 '0' 作为等时数据包的数量。
驱动程序在完成对 urb 使用后应调用 `usb_free_urb`。

## usb_free_urb

### 名字
usb_free_urb — 释放 urb 使用的内存

#### 概要
```
void usb_free_urb (urb_t* urb);
```

#### 参数
urb
指向要释放的 urb 的指针

#### 描述
如果通过调用 `usb_create_urb` 创建了 urb，则在驱动程序完成使用后应调用 `usb_free_urb` 进行进行清理。

## usb_control_msg

### 名字
usb_control_msg — 构建控制 urb，发送它并等待完成

#### 概要
```
int usb_control_msg (struct usb_device * dev, unsigned int pipe, __u8 request, __u8 requesttype, __u16 value, __u16 index, void * data, __u16 size, int timeout);
```

#### 参数
dev
指向要发送消息的 USB 设备指针
发送消息的端点 "pipe"
request
USB 消息请求值
requesttype
USB 消息请求类型
value
USB 消息值
index
USB 消息索引值
data
指向要发送的数据
size
要发送数据的字节长度
timeout
超时前等待消息完成的时间（如果为 0 则永久等待）

#### 描述
此函数向指定的端点发送简单的控制消息并等待消息完成或超时。
如果成功，返回 0，否则返回负错误代码。
不要在中断上下文中（如下半部处理程序）中使用此函数。如果你需要异步消息，或者需要从中断上下文中发送消息，请使用 `usb_submit_urb`

## usb_bulk_msg

### 名字
usb_bulk_msg — 构建批量 urb，发送它并等待完成

#### 概要
```
int usb_bulk_msg (struct usb_device * usb_dev, unsigned int pipe, void * data, int len, int * actual_length, int timeout);
```

#### 参数
- usb_dev
指向要发送消息的 USB 设备指针
- pipe
发送消息的端点 "pipe"
- data
指向要发送的数据指针
- len
要发送数据的字节长度
- actual_length
指向存储实际传输字节长度的位置指针
- timeout
超时前等待消息完成的时间（如果为 0 则永久等待）

#### 描述
此函数向指定的端点发送简单的批量消息并等待消息完成或超时。
如果成功，返回 0，否则返回负错误代码。实际传输的字节数将放在 `actual_length` 参数中。
不要在中断上下文中（如下半部处理程序）中使用此函数。如果你需要异步消息，或者需要从中断上下文中发送消息，请使用 `usb_submit_urb`

## 第 18 章 16x50 UART 驱动

### register_serial

### 名字
register_serial — 在运行时配置 16x50 串口

#### 概要
```
int register_serial (struct serial_struct * req);
```

#### 参数
req
请求结构体

#### 描述
配置请求指定的端口。如果端口存在且正在使用中，则返回错误。如果端口当前不在表中，则将其添加。
然后对端口进行探测，并在必要时自动检测 IRQ。如果此失败，则返回错误。
成功后，端口准备好就绪，并返回线路号。

## unregister_serial

### 名字
unregister_serial — 取消注册 16x50 串口

#### 概要
```
void unregister_serial (int line);
```

#### 参数
line
要取消注册的线路号

#### 描述
取消注册指定的线路，并释放该端口的资源。

## 第 19 章. Z8530 支持

### z8530_interrupt

### 名字
z8530_interrupt — 处理 Z8530 中断

#### 概要
```
void z8530_interrupt (int irq, void *dev_id, struct pt_regs * regs);
```

#### 参数
irq
中断号
dev_id
Z8530 设备
- regs
寄存器

#### 描述
一个正在发生中断的 Z8530 设备。我们为 Z8530 扫描并处理事件。我们为每个 Z8530 芯片使用回调函数。

### z8530_sync_open

### 名字
z8530_sync_open — 打开同步 PIO 的 Z8530

#### 概要
```
int z8530_sync_open (struct net_device * dev, struct z8530_channel * c);
```

#### 参数
dev
网络设备
c
要以同步 PIO 模式打开 Z8530 通道

#### 描述
设置 Z8530 设备。我们拉高 RTS/DTR 并开始网络操作。

### z8530_sync_close

### 名字
z8530_sync_close — 关闭同步 PIO 的 Z8530 通道

#### 概要
```
int z8530_sync_close (struct net_device * dev, struct z8530_channel * c);
```

#### 参数
dev
网络设备
c
要断的 Z8530 通道

#### 描述
关闭 Z8530 接口并切换其中断处理以忽略未来的事件。

### z8530_sync_dma_open

### 名字
z8530_sync_dma_open — 打开 DMA I/O 的 Z8530

#### 概要
```
int z8530_sync_dma_open(struct net_device * dev, struct z8530_channel * c);
```

#### 参数
dev
要附加的网络设备
c
要配置为同步 DMA 模式的 Z8530 通道

#### 描述
为 Z853x 设备设置双向同步 DMA。必须有两个 DMA 通道才能工作。我们假设使用 ISA 驱动的 I/O 以及 PC 的访问限制。

### z8530_sync_dma_close

### 名字
z8530_sync_dma_close — 关闭 DMA I/O

#### 概要
```
int z8530_sync_dma_close(struct net_device * dev, struct z8530_channel * c);
```

#### 参数
dev
网络设备
c
进入丢弃模式的 Z8530 通道

#### 描述
关闭 DMA 模式同步接口。停止 DMA 并释放缓冲区。

### z8530_sync_txdma_open

### 名字
z8530_sync_txdma_open — 打开 TX 驱动 DMA 的 Z8530

#### 概要
```
int z8530_sync_txdma_open (struct net_device * dev, struct z8530_channel * c);
```




#### 参数

- dev
要绑定的网络设备

- c
要在同步 DMA 模式下配置的 Z8530 通道。

#### 描述

为 Z8530 设备设置同步 DMA 传输。要使此工作，必须有一个可用的 ISA DMA 通道。接收端在 PIO 模式下运行，但其具有更大的 FIFO（先存缓冲区）。

## z8530_sync_txdma_close

#### 名称

z8530_sync_txdma_close — 关闭 TX 驱动的 DMA 通道

#### 概要

```
int z8530_sync_txdma_close (struct net_device * dev, struct z8530_channel * c);
```

#### 参数

- dev
要解绑的网络设备

- c
要移入丢弃模式的 Z8530 通道

#### 描述

关闭 DMA/PIO 分离模式的同步接口。停止 DMA 并释放缓冲区。

## z8530_describe

#### 名称

z8530_describe — 统一描述 Z8530 端口

#### 概要

```
void z8530_describe (struct z8530_dev * dev, char * mapping, unsigned long io);
```

#### 参数

- dev
要描述的 Z8530 设备

- mapping
持有映射类型的字符串（例如 "I/O" 或 "Mem"）

- io
涉及的端口值

#### 描述

以标准格式描述 Z8530。我们必须传递 I/O 值，因为端口偏移是不可预测的。此函数的主要目的是尝试获取一种通用格式的报告。

## z8530_init

#### 名称

z8530_init — 初始化 Z8530 设备

#### 概要

```
int z8530_init (struct z8530_dev * dev);
```

#### 参数

- dev
要初始化的 Z8530 设备。

#### 描述

配置 Z8530/Z85C30 或 Z85230 芯片。我们检查设备是否存在，识别类型并对其进行编程，以使其尽可能保持安静并正常运行。这一点非常重要，处于错误状态的 Z8530 有时会进入产生 10kHz 中断流之类的愚蠢模式。

我们设置中断处理程序以丢弃任何事件，以防在重置或设置期间产生这些事件。

返回 0 表示成功，或返回 errno 形式的负值表示问题。

## z8530_shutdown

#### 名称

z8530_shutdown — 关闭 Z8530 设备

#### 概要

```
int z8530_shutdown (struct z8530_dev * dev);
```

#### 参数

- dev
要关闭的 Z8530 芯片

#### 描述

我们设置中断处理器以屏蔽任何中断。然后重置芯片并等待 100uS 以确保重置完成。以防调用者随后尝试进行操作。

## z8530_channel_load

#### 名称

z8530_channel_load — 加载通道数据

#### 概要

```
int z8530_channel_load (struct z8530_channel * c, u8 * rtable);
```

#### 参数

- c
要配置的 Z8530 通道

- rtable
寄存器、值对表

## FIXME

使用 ioctl 允许用户上传表

从系统数据加载 Z8530 通道。我们使用 +16 来指示“主”寄存器。值 255 终止表。

## z8530_null_rx

#### 名称

z8530_null_rx — 丢弃数据包

#### 概要

```
void z8530_null_rx (struct z8530_channel * c, struct sk_buff * skb);
```

#### 参数

- c
数据包到达通道

- skb
缓冲区

#### 描述

在空闲时，我们将接收处理程序指向此函数。与其让 syncppp 处理帧，我们选择直接将它们丢弃。

## z8530_queue_xmit

#### 名称

z8530_queue_xmit — 队列数据包

#### 概要

```
int z8530_queue_xmit (struct z8530_channel * c, struct sk_buff * skb);
```

#### 参数

- c
要使用的通道

- skb
要发送到通道的数据包

#### 描述

队列数据包进行发送。因为即使在 DMA 模式下，Z85230 每个数据包的中断延迟很难达到，所以如果需要，我们在此处切换到 DMA 缓冲区而不是在中断中切换。

## z8530_get_stats

#### 名称

z8530_get_stats — 获取网络统计

#### 概要

```
struct net_device_stats * z8530_get_stats (struct z8530_channel * c);
```

#### 参数

- c
要使用的通道

#### 描述

获取统计信息块。我们在软件中维护统计数据，因为芯片不会为我们完成此。

## 第 20 章 帧缓冲区库 (Frame Buffer Library)

帧缓冲区驱动程序严重依赖四个数据结构。这些结构在 include/fb.h 中声明：fb_info、fb_varinfo、fb_monospec 和 fb_ops。

fb_info 定义了当前状态。fb_varinfo 定义了卡的属性。fb_monospec 定义了起始位置。fb_ops 是函数集合。

## 20.1. 帧缓冲区内存 (Frame Buffer Memory)

## register_framebuffer

#### 名称

register_framebuffer — 注册帧设备

#### 概要

```
int register_framebuffer (struct fb_info);
```

#### 参数

- fb_info

#### 描述

注册帧设备。错误时返回负数 errno，成功时返回 0。

## unregister_framebuffer

#### 名称

unregister_framebuffer — 注销帧设备

#### 概要

```
int unregister_framebuffer (struct fb_info);
```

#### 参数

- fb_info

#### 描述

注销帧设备。错误时返回负数 errno，成功时返回 0。

## 20.2. 帧缓冲区控制台 (Frame Buffer Console)

## fbcon_redraw_clear

#### 名称

fbcon_redraw_clear — 清空屏幕

#### 概要

```
void fbcon_redraw_clear (struct vc_data, struct display * p, int sy);
```

#### 参数

- con
指向当前活动控制台的结构

- p
显示结构

- sy
起始 Y 坐标

- sx
起始 X 坐标

- height
清空高度

- width
清空宽度

#### 描述

清空屏幕的指定区域。所有维度均为像素。

## fbcon_redraw_bmove

#### 名称

fbcon_redraw_bmove — 将屏幕移动到另一个位置

#### 概要

```
void fbcon_redraw_bmove (struct display * p, int sy, int sx, int dy, int dx, int h, int w);
```

#### 参数

- p
显示结构

- sy
起始 Y 坐标

- sx
起始 X 坐标

- dy
目标 Y 坐标

- dx
目标 X 坐标

- h
移动高度

- w
移动宽度

#### 描述

将屏幕的一个区域移动到另一个区域。所有维度均为像素。注意此函数不能与 ypan 或 wrap 配合使用。

## 20.3. 帧缓冲区调色板 (Frame Buffer Colormap)

## fb_alloc_cmap

#### 名称

fb_alloc_cmap — 分配调色板

#### 概要

```
int fb_alloc_cmap (struct fb_cmap * cmap, int len, int transp);
```

#### 参数

- cmap
帧缓冲区调色板结构

- len
cmap 的长度

- transp
如果有透明度则为 1，否则为 0

#### 描述

为调色板 cmap 分配内存。len 是调色板中的条数。错误时返回 -1 errno，成功时返回 0。

## fb_copy_cmap

#### 名称

fb_copy_cmap — 拷贝调色板

#### 概要

```
void fb_copy_cmap (struct fb_cmap * from, struct fb_cmap * to, int fsfromto);
```

#### 参数

- from
帧缓冲区调色板结构

- to
帧缓冲区调色板结构

- fsfromto
确定拷贝方法

# 描述 将调色板内容从 from 拷贝到 to。

## fb_get_cmap

#### 名称

fb_get_cmap — 获取调色板

#### 概要

```
int fb_get_cmap (struct fb_cmap * cmap, int kspc, int (*getcolreg) (u_int, u_int *, u_int *, u_int *, u_int *, struct fb_info *), struct fb_info *info);
```

#### 参数

- cmap
帧缓冲区调色板

- kspc
布尔，0 本地拷贝，1 使用 put_user 函数



```
getcolreg
```
获取颜色寄存器的函数指针

info

帧缓冲区信息结构

# Description

为设备 *info.* 的屏幕获取调色板 *cmap*。

错误时返回负数 errno，成功时返回 0。

# fb_set_cmap

# Name

*fb_set_cmap* — 设置调色板

# Synopsis

```
int fb_set_cmap (struct fb_cmap * cmap, int kspc, int
(*setcolreg)(u_int, u_int, u_int, u_int, u_int, struct fb_info*), struct fb_info * info);
```

# Arguments

cmap

帧缓冲区调色板结构

kspc

boolean

布尔值，0 拷贝本地，1 使用 get_user 函数

setcolreg

获取颜色寄存器的函数指针

info

帧缓冲区信息结构

# Description

为设备 info 的屏幕设置调色板 cmap。

错误时返回负数 errno，成功时返回 0。

# fb_default_cmap

# Name

fb_default_cmap — 获取默认调色板

# Synopsis

```
struct fb_cmap * fb_default_cmap (int len);
```

# Arguments

len

对应对应的调色板大小

# Description

获取特定屏幕深度的默认调色板。len 是特定屏幕深度调色板的大小。

返回指向帧缓冲区调色板结构的指针。

# fb_invert_cmaps

# Name

fb_invert_cmaps — 反转所有默认调色板

# Synopsis

```
void fb_invert_cmaps ( void);
```

# Arguments

void

- 无参数

# Description

反转所有默认调色板。

# 20.4. 帧缓冲区通用函数

# fbgen_get_fix

# Name

fbgen_get_fix — 获取显示器的固定部分

# Synopsis

```
int fbgen_get_fix (struct fb_fix_screeninfo * fix, int con,
struct fb_info * info);
```

# Arguments

- fix
fb_fix_screeninfo 结构

- con
虚拟控制台编号

- info
帧缓冲区信息结构

# Description

获取显示器的固定信息部分并将其放入 device info 上虚拟控制台 con 的 fix 中。

错误时返回负数 errno，成功时返回 0。

# fbgen_get_var

# Name

fbgen_get_var — 获取显示器的用户定义部分

# Synopsis

```
int fbgen_get_var (struct fb_var_screeninfo * var, int con,
struct fb_info * info);
```

# Arguments

var

fb_var_screeninfo 结构

con

虚拟控制台编号

info

帧缓冲区信息结构

# Description

获取显示器的用户定义部分并将其放入 device info 上虚拟控制台 con 的 var 中。

错误时返回负数 errno，成功时返回 0。

# fbgen_set_var

# Name

fbgen_set_var — 设置显示器的用户定义部分

# Synopsis

```
int fbgen_set_var (struct fb_var_screeninfo * var, int con,
struct fb_info * info);
```

# Arguments

var
fb_var_screeninfo 显示器用户定义部分

con

虚拟控制台编号

info
帧缓冲区信息结构

# Description

根据 var 的规定，设置 device info 上虚拟控制台 con 的显示用户定义部分。

错误时返回负数 errno，成功时返回 0。

# fbgen_get_cmap

# Name

fbgen_get_cmap — 获取调色板

# Synopsis

```
int fbgen_get_cmap (struct fb_cmap * cmap, int kspc, int con,
struct fb_info * info);
```

# Arguments

- cmap
帧缓冲区调色板结构

- kspc
布尔值，0 拷贝本地，1 使用 put_user 函数

- con
虚拟控制台编号

- info
帧缓冲区信息结构

# Description

获取虚拟控制台 con 的调色板并将其放入 device info 的 cmap 中。

错误时返回负数 errno，成功时返回 0。

# fbgen_set_cmap

# Name

fbgen_set_cmap — 设置调色板

# Synopsis

```
int fbgen_set_cmap (struct fb_cmap * cmap, int kspc, int con, struct fb_info * info);
```

# Arguments

- cmap
帧缓冲区调色板结构

- kspc
布尔值，0 拷贝本地，1 使用 get_user 函数

- con
虚拟控制台编号

- info
帧缓冲区信息结构

# Description

为 device info 上虚拟控制台 con 设置调色板 cmap。

错误时返回负数 errno，成功时返回 0。

# fbgen_pan_display

# Name

fbgen_pan_display — 滚动或环绕显示

# Synopsis

```
int fbgen_pan_display (struct fb_var_screeninfo * var, int con;
struct fb_var_info * info);
```

# Arguments

- var
帧缓冲区显示用户定义部分

- con
虚拟控制台编号

- info
帧缓冲区信息结构

# Description

对 info 上的虚拟控制台 con 进行滚动或环绕。

此调用只查看 var 中的 xoffset、yoffset 和 FB_VMODE_WRAP 标志。

错误时返回负数 errno，成功时返回 0。

# fbgen_do_set_var

# Name

fbgen_do_set_var — 更改视频模式

# Synopsis

```
int fbgen_do_set_var (struct fb_var_screeninfo * var, int isactive, struct fb_info * info);
```

# Arguments

- var
帧缓冲区显示用户定义部分

- isactive
布尔值，0 激活，1 激活

- info
帧缓冲区结构

# Description

更改 device info 的视频模式。如果 isactive 为非零，将应用更改。

错误时返回负数 errno，成功时返回 0。

# fbgen_set_disp

# Name

fbgen_set_disp — 设置显示

# Synopsis

```
void fbgen_set_disp (int con, struct fb_info * info);
```

# Arguments

- con
虚拟控制台编号

- info
帧缓冲区信息结构

# Description

为 device info 虚拟控制台设置显示。

# fbgen_install_cmap

# Name

fbgen_install_cmap — 安装调色板

# Synopsis

```
void fbgen_install_cmap (int con, struct fb_info * info);
```

# Arguments

- con
虚拟控制台编号

- info
帧缓冲区信息结构

# Description

为 device info 虚拟控制台安装当前调色板。

# fbgen_update_var

# Name

fbgen_update_var — 更新用户定义部分

# Synopsis

```
int fbgen_update_var (int con, struct fb_info * info);
```

# Arguments

- con
虚拟控制台编号

- info
帧缓冲区结构

# Description

更新 device info 上虚拟控制台的显示用户定义部分（var 结构）。由 fbcon.c 调用。

# fbgen_switch

# Name

fbgen_switch — 切换到不同的控制台

# Synopsis

```
int fbgen_switch (int con, struct fb_info * info);
```

# Arguments

- con
虚拟控制台编号

- info
帧缓冲区结构

# Description

切换 device info 上的控制台。

# fbgen_blank

# Name

fbgen_blank — 刷屏

# Synopsis

```
void fbgen_blank (int blank, struct fb_info * info);
```

# Arguments

- blank
布尔值，0 灭屏，1 亮屏

- info
帧缓冲区结构

# Description

对 device info 屏幕刷屏。

# 20.5. 帧缓冲区视频数据库

# fb_find_mode

# Name

fb_find_mode — 寻找有效的视频模式

# Synopsis

```
int __init fb_find_mode (struct fb_var_screeninfo * var, struct fb_info * info, const char * mode_option, const struct fb_videodemode * db, unsigned int dsize, const struct fb_videodemode * default_mode, unsigned int default_bpp);
```

# Arguments

var
帧缓冲区用户定义部分

info
帧缓冲区结构

mode_option
要查找的视频模式

db
视频模式数据库

dsize
db 的大小

default_mode
回退模式

default_bpp
位深

# Description

寻找合适的视频模式，从 mode_option 指定模式开始，回退到 default_mode。如果 default_mode 失败，将尝试视频数据库中的所有模式。

mode_option 的有效标识：

<xres>x<yres>-<bpp>@[refresh> 或 <name>-<bpp>@refresh>，其中 <xres>、<yres><bpp> 和 <refresh> 为数字，<name> 为字符串。

# NOTE

传递的 struct var 不会被清除！这允许你提供 grayscale 和 accel_flags 等字段的值。

失败返回 0，1 表示使用了指定的 mode_option，2 表示使用了忽略刷新率的 mode_option，3 表示使用了默认模式，4 表示回退到任何有效模式。

# __fb_try_mode

# Name

__fb_try_mode — 测试视频模式

# Synopsis

```
int __fb_try_mode (struct fb_var_screeninfo * var, struct fb_info * info, const struct fb_videodemode * mode, unsigned int bpp);
```

# Arguments

var
帧缓冲区用户定义部分

info
帧缓冲区结构

mode
帧缓冲区视频模式结构

bpp
位深

# Description

尝试一种视频模式以测试其对 device info 的有效性。
成功时返回 1。





## 20.6. 缓冲区 Macintosh 视频模式数据库

### console_getmode

#### 名称
console_getmode — 获取当前模式

#### 概要
```
int console_getmode (struct vc_mode * mode);
```

#### 参数
- mode
  虚拟控制台模式结构

#### 描述
用全局 display_info 结构体中的当前模式填充 mode。

注意，此函数仅用于 XPMAC 兼容性。

返回 0。

### console_setmode

#### 名称
console_setmode — 设置当前控制台模式

#### 概要
```
int console_setmode (struct vc_mode * mode, int doit);
```

#### 参数
- mode
  虚拟控制台模式结构
- doit
  布尔值，0 为测试模式，1 为测试并激活模式

#### 描述
如果 doit 不为零，则为所有虚拟控制台设置模式；否则，测试模式的有效性。

注意，此函数仅用于 XPMAC 兼容性。

错误时返回负数 errno，成功时返回 0。

### console_setmap

#### 名称
console_setmap — 设置控制台的调色板映射

#### 概要
```
int console_setmap (int n_entries, unsigned char * red, unsigned char * green, unsigned char * blue);
```

#### 参数
- n_entries
  调色板条目数（最大 16）
- red
  调色板红色组件的值
- green
  调色板绿色组件的值
- blue
  调色板蓝色组件的值

#### 描述
设置全局 palette_cmap 结构并在当前控制台上激活调色板。

注意，此函数仅用于 XPMAC 兼容性。

错误时返回负数 errno，成功时返回 0。

### console_powermode

#### 名称
console_powermode — 设置显示器电源模式

#### 概要
```
int console_powermode (int mode);
```

#### 参数
- mode
  要设置的电源状态

#### 描述
根据 mode 设置电源状态。注意此函数仅用于 XPMAC 兼容性且作用不大。
对于 VC_POWERMODE_INQUIRY 返回 0，对于 VESA 设置返回 -EINVAL，失败时返回 -ENIXIO。

### mac_vmode_to_var

#### 名称
mac_vmode_to_var — 将 vmode/cmode 对转换为 var 结构体

#### 概要
```
int mac_vmode_to_var (int vmode, int cmode, struct fb_var_screeninfo * var);
```

#### 参数
- vmode
  MacOS 视频模式
- cmode
  MacOS 颜色模式
- var
  缓冲区视频模式结构体

#### 描述
将 MacOS 的 vmode/cmode 对转换为缓冲区视频模式结构体。

错误时返回负数 errno，成功时返回 0。

### mac_var_to_vmode

#### 名称
mac_var_to_vmode — 将 var 结构体转换为 MacOS vmode/cmode 对

#### 概要
```
int mac_var_to_vmode (const struct fb_var_screeninfo * var, int * vmode, int * cmode);
```

#### 参数
- var
  缓冲区视频模式结构体
- vmode
  MacOS 视频模式
- cmode
  MacOS 颜色模式

#### 描述
将缓冲区视频模式结构体转换为 MacOS 的 vmode/cmode 对。

错误时返回负数 errno，成功时返回 0。

### mac_map_monitor_sense

#### 名称
mac_map_monitor_sense — 将显示器感应转换为 vmode

#### 概要
```
int mac_map_monitor_sense (int sense);
```

#### 参数
- sense
  Macintosh 显示器感应数字

#### 描述
将 Macintosh 显示器感应数字转换为 MacOS vmode 数字。

返回 MacOS vmode 视频模式数字。

### mac_find_mode

#### 名称
mac_find_mode — 查找视频模式

#### 概要
```
int __init mac_find_mode (struct fb_var_screeninfo * var, struct fb_info * info, const char * mode_option, unsigned int default_bpp);
```

#### 参数
- var
  显示自定义部分
- info
  缓冲区信息结构体
- mode_option
  视频模式名称（参见 mac_modedb[]）
- default_bpp
  默认每像素颜色深度（位）

#### 描述
查找合适的模式。尝试设置由 mode_option 指定模式。如果所需模式的名称以 'mac' 开头，将使用 Mac 视频模式数据库，否则将退回到标准视频模式数据库。

#### 注意
函数被标记为 __init，只能在系统启动期间使用。
返回来自 fb_find_mode 的错误代码（参见 fb_find_mode 函数）。

## 20.7. 缓冲区字体

### fbcon_find_font

#### 名称
fbcon_find_font — 查找字体

#### 概要
```
struct fbcon_font_desc * fbcon_find_font (char * name);
```

#### 参数
- name
  字体字符串名称

#### 描述
根据字符串名称 name 查找指定的字体。

未找到字体返回 NULL，否则返回指定字体的指针。

### fbcon_get_default_font

#### 名称
fbcon_get_default_font — 获取默认字体

#### 概要
```
struct fbcon_font_desc * fbcon_get_default_font (int xres, int yres);
```

#### 参数
- xres
  屏幕 X 轴
- yres
  屏幕 Y 轴

#### 描述
获取指定屏幕尺寸的默认字体。单位为像素。

未找到字体返回 NULL，否则返回所选字体的指针。

