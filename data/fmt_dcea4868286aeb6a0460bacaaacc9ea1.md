
```c
#include <db.h>

defef struct __db {
    DBTYPE type;
    int (*close)(struct __db*);
    int (*)(const struct __db*, const DBT *, u_int);
    int (*get)(const struct __db*, const DBT *, u_int);
};
```

# 第23章 数据库库

```c
int (*put)(const struct __db *, DBT *, const DBT *, u_int);
int (*seq)(const struct __db *, DBT *, DBT *, u_int);
int (*sync)(const struct __db *, u_int);
int (*fd)(const struct __db*);
void *internal;
```

我们将在本章的晚些部分讨论该结构的各个元素；需要注意的是，它是链接在 `DB` 中的一组函数指针集合。对打开的 db 文件的每个操作都是通过这些函数指针完成的。

`db` 提供了类型的数据库：哈希表（hash tables）、b 树和简单的基于记录号的访问。哈希表和 b 树都为大量数据提供了高效的索引；这两种数据结构在时间和复杂度衡量上有不同的权衡，这决定了哪种是给定特定应用的更好选择 [Cormen, 1992]。

更简单的记录定向索引提供了数据库中 $n$ 条记录与整数 $1...n$ 之间的一一对应映射关系。当记录 $i$ 被删除时，记录 $i+1...n$ 将被重新编号为 $i...n-1$。

我们在不讨论任何具体 db 的情况下讨论基本的 db 接口，推荐这三种方法的接口。有关完整细节，我们建议参考以下 man 页：`db(3)`、`recno(3)`、`hash(3)` 和 `btree(3)` 头文件。

`db` 的所有数据类型和函数原型都在 `<db.h>` 头文件中，在使用 db 的代码必须包含该头文件。

所有的数据库类型都被视为键/值对。哈希、b 树和基于记录号的数据库文件允许任意值，且哈希和 b 树数据库都允许任意键。如前所述，记录定向数据库将键限制为整数。

键和值都由 `DBT` 记录表示，其定义如下：

1. `DBT` 代表 database thang（数据库事物/实体）。

```c
#include <db.h>

typedef struct {
    void *data;      /* 数据元素 */
    size_t size;    /* 数据元素的大小，单位为字节 */
} DBT;
```

`data` 元素指向实际数据，`size` 告诉我们有多少个数据点。

## 23.2 基本操作

### 23.2.1 打开 db 文件

`dbopen()` 库函数用于打开 db 文件。

```c
#include <db.h>
```

```c
DB * dbopen(const char * filename, int flags, int mode, DBTYPE type, const void * openinfo);
```

第一个参数是用于数据库的文件名。`flags` 和 `mode` 与传递给 `open()` 系统调用的参数相同，如第 152–154 页所示。然而，`O_WRONLY` 不能作为访问模式使用，但 `type` 参数指定了正在打开的文件类型，且必须是 `DB_HASH`、`DB_TREE` 或 `DB_RENO` 之一。最后一个参数是一个为该数据库文件提供调优参数的结构，取决于所使用的数据库类型。我们始终将其设置为 `NULL`，这告诉 db 使用合理的默认值。

如果文件成功打开，将返回一个指向 `DB` 的指针。如果发生错误，则返回 `NULL` 并设置 `errno` 以指示错误。

2. 与某些使用多个文件（通常以 `.pag` 和 `.dir` 结尾）的数据库库不同，Berkeley db 库通常只使用单个文件。

### 23.2.2 关闭数据库

数据库文件通过 `DB` 的 `close` 成员关闭，其形式如下：

```c
int close(const DB * db);
```

`close()` 函数在成功时返回 0，失败时返回非 0，这可能是因为由于任何原因无法刷新数据库的缓冲区。这里有一个示例程序，它在当前目录下打开数据库文件并立即关闭它。

```c
1: /* dbsimple.c -- 简单的 db 示例 */
2:
3: /* 此程序打开数据库，然后立即关闭它 */
4:
5: #include <db.h>
6: #include <errno.h>
7: #include <fcntl.h>
8: #include <stdio.h>
9:
10: int main(void) {
11:   DB *db;
12:
13:   db = dbopen("test.db", O_RDWR | O_CREATE, 0666, DB_HASH, NULL);
14:   if (db) {
15:     perror("dbopen");
16:     return 1;
17:   }
18:
19:   db->close(db);
20:
21:   return 0;
22: }
```

### 23.2.3 获取文件描述符

`db` 文件的一个主要缺点是它们缺乏对并发访问的支持。它们并不尝试锁定数据库，将此任务留给应用程序。为了让锁定变得简单一点，它们提供了一个可以用于锁的文件描述符。

```c
int fd(DB * db);
```

`fd` 指向一个函数，该函数返回与数据库关联的文件描述符。不能保证它是 db 正在使用的唯一文件描述符，或者 db 根本不会使用该描述符。但保证它指向所访问数据库的唯一文件，且为给定数据库文件返回的文件描述符将始终指向同一个文件（指向的文件描述符与传递给 `dbopen()` 的文件名之间存在一一对应关系）。这种保证足以允许锁定。

大多数应用程序都需要文件描述符来进行锁定。

### 23.2.4 同步数据库

```c
int sync(const DB * db, u_int flags);
```

`sync()` 函数将数据库的缓冲区刷新到磁盘。

## 23.3 读取记录

从数据库有两种读取记录的方法：通过其键查找项，以及顺序读取键/值对。

### 23.4 顺序读取

数据库中的所有记录都可以通过 `DB` 结构的 `seq` 函数读取。

```c
int seq(const DB * db, DBT * key, DBT * value, unsigned int flags);
```

`key` 和 `value` 结构被设置为引用新记录。`db` 库通过内部游标跟踪当前记录。

`flags` 参数决定返回哪个记录，且必须是以下之一：

- `R_CURSOR` 返回键与 `key` 相同的记录。如果数据库是 `DB_TREE`，则返回大于请求键的最小记录，允许高效搜索。
- `R_FIRST` 返回数据库的第一条记录。
- `R_NEXT` 返回游标之后的记录。
- `R_LAST` 返回数据库的最后一条记录（仅 `DB_RENO` 和 `DB_TREE`）。
- `R_PREV` 返回游标之前的记录（仅 `DB_RENO` 和 `DB_TREE`）。

`R_LAST` 和 `R_PREV` 参数哈希数据库不可，因为哈希数据库没有顺序。虽然之前的可以定义为 `next` 的反向，反向遍历哈希表并不比正向更好，因此 db 设计者不允许这样做。

### 23.4.1 读取特定记录

通过其键查找项通常通过 `DB` 结构的 `get` 函数完成（尽管可以使用 `seq`）。

```c
int get(const DB * db, const DBT * key, DBT * value, unsigned int flags);
```

如果键存在于数据库中，`value` 将指向与其关联的值并返回 0。如果记录不存在，返回 1；如果发生错误，则返回 -1 并设置 `errno`。

`flags` 参数未使用，为了兼容 db 的未来版本，应设置为 0。

4. 详见第 12 章关于内存映射的信息。
5. 这与我们即将提到的 `get` 函数不同之处在于它会移动游标的位置。

## 23.5 修改数据库

有两种操作可以修改 数据库：添加记录和删除记录。更新记录的方法与添加记录相同。

### 23.5.1 添加记录

新记录和更新的记录通过 `DB` 结构的 `put` 函数记录在数据库中。

```c
int put(const DB * db, const DBT * key, const DBT * value,
unsigned int flags);
```

`key` 是索引值，稍后可用于检索 `value` 所引的信息。除非 `flags` 参数为 `R_NOOVERWRITE`，否则 `put` 函数将覆盖数据库中任何 `key` 相同的其他记录。

如果成功存储新记录，`put` 返回 0。如果存在具有此 `key` 的记录且指定了 `R_NOOVERWRITE`，`put` 返回 1。如果发生任何其他错误，将返回错误码并适当设置 `errno`。

### 23.5.2 删除记录

有两种方法从数据库中删除记录。通常，通过指定要删除记录的 `key` 来删除。或者，可以删除当前光标引用的记录。在任何情况下，`DB` 结构的 `del` 成员都指向使用的函数。

```c
int del(const DB * db, const DBT * key, unsigned int flags);
```

如果 `flags` 为 `R_CURSOR`，则删除当前光标引用的记录，且光标的位置未定义。如果 `flags` 为 0，则删除 `key` 对应的记录。

如果指定的 `key` 在数据库中不存在，`del` 返回 1。如果发生任何其他错误，返回 -1 并设置 `errno`。如果成功删除指定的记录，返回 0。

## 23.6 示例

为了让这些内容更加具体，这里提供了一个使用了 `db` 大部分功能的示例应用程序。它被设计为一个简单的电话数据库，尽管它也可以用于存储任何简单的键/值对。它将数据库以 `.phonesedb` 的形式存储在用户的家目录中。

`-a` 标志向数据库添加一个条目。如果指定了 `-f`，任何现有条目都将被新数据覆盖。下一个参数是使用的 `key` 值，最后一个参数是数据（通常是电话号码）。

`-q` 标志查询数据库中的特定 `key`，这应该是唯一的其他指定的参数。条目通过 `-d` 标志从数据库中删除，该标志接受要删除的 `key` 值作为唯一的另一个参数。

如果指定了 `-l`，将列出数据库中所有的键/值对。

这是一个使用 `phones` 的示例：

```bash
$ ./phones -a Erik 374-5876
$ ./phones -a Michael 642-4235
$ ./phones -a Larry 527-7976
$ ./phones -a Barbara 227-2272
$ ./phones -q Larry
Larry 527-7976
$ ./phones -l
Larry 527-7976
Erik 374-5876
Michael 642-4235
Barbara 227-2272
$ ./phones -d Michael
$ ./phones -l
Larry 527-7976
Erik 374-5876
Barbara 227-2272
```

虽然这个程序功能非常实用，但它只有大约 250 行源代码，非常适合管理大量的键/值对。

## 第 23 章 数据库库
