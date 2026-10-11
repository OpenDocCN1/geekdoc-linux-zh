
## 创建和打开数据库

  创建数据库的函数与打开数据库的函数相同，均为 `db_open`。如果指定的数据库不存在，它将先被创建，然后被打开。`db_open` 的语法如下：

```c
int db_open(const char *file, DBTYPE type, u_int32_t flags, int mode,
        DB_ENV *dbenv, DB_INFO *dbInfo, DB **dbpp);
```

  `file` 是要打开的数据库的文件路径名。`type` 表示访问方法，可以是 `DB_BTREE`、`DB_HASH` 或 `DB_RECNO`。如果你不知道现有数据库的类型，可以使用 `DB_UNKNOWN` 来打开它。`flags` 会修改 `db_open` 的行为。如果必要的文件尚不存在，`DB_CREATE` 会创建这些文件。`DB_RDONLY` 以只读方式打开数据库（任何写入尝试都会失败），而 `DB_TRUNCATE` 如果数据库存在，会将其逻辑清零。`mode` 参数是一个八进制值，指定数据库文件的访问权限。它与 `open` 系统调用所需的 `mode` 参数类似。

- "open 系统调用及其 mode 参数"在“文件模式”一节第 134 页中有详细介绍。

  `dbenv` 和 `dbInfo` 参数控制 DB 行为的先进功能，这些功能超出了本书的范围，因此不在这里讨论。将这两个参数设置为 `NULL` 即可获取 DB 的默认行为。最后，`dbpp` 是已打开数据库的句柄，它是 DB（数据库）结构体指针的指针。它会被初始化为适当的值，或者在失败时初始化为 `NULL`。

  `db_open` 初始化的句柄是所有后续数据库操作的关键，因为几乎所有的 Berkeley DB 接口操作都通过句柄中包含的函数指针进行。

## 关闭数据库

  要关闭数据库，请使用 `close` 函数。其原型如下：

```c
int DB->close(DB *db, u_int32_t flags);
```

  `db` 是先前由 `db_open` 调用返回的句柄。`flags` 应为 0 或 `DB_NOSYNC`。`DB_NOSYNC` 指示 DB 在关闭数据库之前不同步或刷新缓存中的数据库数据到磁盘。如果 `flags` 为 0，缓存的数据将被写入磁盘。

> 注意
> `DB_NOSYNC` 是一个不好的选项！Berkeley DB 在自己的缓存中维护信息，并独立于内核将其写出。不同步缓存信息会导致数据不可靠、不一致或损坏。

### 示例

![](img/be588b36b489136ce784030a08a1d3d4_236_0.png)

  该程序 *opendb* 在当前工作目录中打开并关闭一个数据库。

```c
/*
 * opendb.c 打开一个 Berkeley DB 数据库
 */
#include <stdlib.h>
#include <stdio.h>
#include <errno.h>
#include "db.h"

int main(void)
{
    DB *db;
    int ret;

    ret = db_open("test.db", DB_BTREE,
                   DB_CREATE, 0600, NULL, NULL, &db);
    if (ret) {
        perror("db_open");
        exit(EXIT_FAILURE);
    }

    db->close(db, 0);
    exit(EXIT_SUCCESS);
}
```

  `db_open` 调用尝试在当前目录中打开一个名为 `test.db` 的 B+树数据库。如果数据库尚不存在，`DB_CREATE` 标志会指示 DB 创建该文件。在打开（或在必要时创建）数据库后，`db_close` 调用关闭数据库。*opendb* 没有输出，但在当前工作目录中快速运行 `ls` 命令会揭示 `test.db` 已被创建。虽然 `test.db` 文件中不会存储任何记录，但 Berkeley DB 在创建文件时会写入一些管理信息。你不需要担心这一点，因为这些是 DB API 使用的信息。

### 在数据库中存储项目

  要向数据库中添加数据，请使用 `put` 函数，其原型如下：

```c
int DB->put(DB *db, DB_TXN *txnid, DBT *key, DBT *data, u_int32_t flags);
```

  `db` 是先前由 `db_open` 返回的数据库句柄；`txnid` 是事务 ID，这是一个这里未涵盖的先进功能，因此将其设置为 `NULL`。`flags` 必须是 `0`（允许覆盖具有相同键的现有记录）、`DB_NOOVERWRITE`（如果已存在具有相同键的键/值对，则禁止 `put` 操作）或 `DB_APPEND`（仅适用于类型为 `DB_RECNO` 的数据库）之一。如果键已存在，`put` 返回 `DB_KEYEXIST`；标准的返回码也适用。

  为了确保与未来版本的 Berkeley DB 兼容，你在使用 `key` 和 `value` 参数之前应始终先初始化它们。最简单的做法是使用标准 C 库中的 `memset` 调用。例如，假设你需要在程序中使用一个名为 `dbkey` 的键。在使用之前，按照以下代码片段所示对其进行初始化：

```c
DBT dbkey;
memset (&dbkey, 0, sizeof (DBT *));
```

  在此示例中，`memset` 将 `DBT` 关联的所有内存块的值设置为零。

### 示例

![](img/be588b36b489136ce784030a08a1d3d4_237_0.png)

  下一个示例向由 `opendb` 创建的数据库中添加了记录：

```c
/*
* adddb.c - 向 Berkeley DB 数据库中添加记录
*/
#include <stdlib.h>
#include <stdio.h>
#include <errno.h>
#include "db.h"

int main(void)
{
DB *db;
int ret, i = 0;
DBT key, value;

ret = db_open("test.db", DB_BTREE,
DB_CREATE, 0600, NULL, NULL, &db);
if(ret) {
    perror("dbopen");
    exit(EXIT_FAILURE);
}

/* 首先初始化键/值对 */
memset(&key, 0, sizeof(key));
memset(&value, 0, sizeof(value));
/* 设置 key, value 的值 */

key.data = "one";
key.size = sizeof("one");
value.data = "Compiling Programs";
value.size = sizeof("Compiling Programs");
/* 存储它 */
ret = db->put(db, NULL, &key, &value, DB_NOOVERWRITE);
if(ret == DB_KEYEXIST) {
    fprintf(stderr, "key %s exists\n", (char *)key.data);
    exit(EXIT_FAILURE);
} else {
    perror("put");
    exit(EXIT_FAILURE);
}

db->close(db, 0);
exit(EXIT_SUCCESS);
}
```

  同样，此示例没有输出。但是，如果你连续执行两次，第二次运行将失败，因为 flags 值 `DB_NOOVERWRITE` 禁止在指定的键已存在于数据库中时执行 put 操作。在这种情况下，输出将如下所示：

![](img/be588b36b489136ce784030a08a1d3d4_238_0.png)

**输出**

```
$ ./adddb
key one exists
```

  特别需要注意的是，在此示例中，字符串 one 和 Compiling Programs 的空终止符也被存储在数据库中，因此 key 和 value 的 size 成员必须是字符串的长度 *包括末尾的空字符*。这解释了为什么代码在计算字符串长度时使用了 sizeof 而不是 `strlen`（当然，`strlen+1` 也足够了）。

> **提示**
> 通常，使用 Berkeley DB 的程序不会向数据库添加静态数据或编译到程序中的数据。相反，记录是在运行时动态添加的。示例程序使用 `sizeof` 是因为它对静态数据（one 和 Compiling Programs）效果很好。然而，在运行时，你应该使用 `strlen` 调用来确定字符串的长度，并将其返回值加 1 以存储终止空字符。你不需要将终止空字符作为字符串的一部分存储，但这样做可以让你使用标准库的流输出函数，如 `puts` 和 `printf`，这些函数需要空终止符才能正确工作（或根本无法工作）。

## 删除数据库中的项目

  要从 DB 数据库中删除数据，请使用 `del` 函数。它接受 `put` 函数所需的五个参数中的四个。`del` 的原型如下：

```c
int DB->del(DB *db, DB_TXN *txnid, DBT *key, u_int32_t flags);
```

  参数的含义也与 `put` 函数相同。因为你只关心键而不关心数据，所以不需要指定要删除的值。删除键会删除其关联的值。目前，`flags` 没有指定值，因此应为 0。如果找不到指定的键，`del` 返回 `DB_NOTFOUND`；否则，适用标准返回码。

### 示例

![](img/be588b36b489136ce784030a08a1d3d4_239_0.png)

  以下程序从数据库中删除记录：

```c
/*
 * deldb.c - 从 Berkeley DB 数据库中删除记录
 */
#include <stdlib.h>
#include <stdio.h>
#include <errno.h>
#include <string.h>
#include "db.h"

int main(void)
{
    DB *db;
    int ret;
    DBT key;
```
