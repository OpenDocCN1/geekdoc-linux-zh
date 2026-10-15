
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

同样，此示例没有输出。但是，如果你连续执行两次，第二次运行将失败，因为 `flags` 值 `DB_NOOVERWRITE` 禁止在指定的键已存在于数据库中时执行 `put` 操作。在这种情况下，输出将如下所示：

![](img/be588b36b489136ce784030a08a1d3d4_238_0.png)

**输出**

```
$ ./adddb
key one exists
```

特别需要注意的是，在此示例中，字符串 `one` 和 `Compiling Programs` 的空终止符也被存储在数据库中，因此 `key` 和 `value` 的 `size` 成员必须是字符串的长度 *包括末尾的空字符*。这解释了为什么代码在计算字符串长度时使用了 `sizeof` 而不是 `strlen`（当然，`strlen+1` 也足够了）。

> **提示**
>
> 通常，使用 Berkeley DB 的程序不会向数据库添加静态数据或编译到程序中的数据。相反，记录是在运行时动态添加的。示例程序使用 `sizeof` 是因为它对静态数据（`one` 和 `Compiling Programs`）效果很好。然而，在运行时，你应该使用 `strlen` 调用来确定字符串的长度，并将其返回值加 1 以存储终止空字符。你不需要将终止空字符作为字符串的一部分存储，但这样做可以让你使用标准库的流输出函数，如 `puts` 和 `printf`，这些函数需要空终止符才能正确工作（或根本无法工作）。

## 删除数据库中的项目

要从 DB 数据库中删除数据，请使用 `del` 函数。它接受 `put` 函数所需的五个参数中的四个。`del` 的原型如下：

```c
int DB->del(DB *db, DB_TXN *txnid, DBT *key, u_int32_t flags);
```

参数的含义也与 `put` 函数相同。因为你只关心键而不关心数据，所以不需要指定要删除的值。删除键会删除其关联的值。目前，`flags` 没有指定值，因此应为 0。如果找不到指定的键，`del` 返回 `DB_NOTFOUND`；否则，适用标准返回码。

## 示例

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

## 输出结果

```c
ret = db_open("test.db", DB_BTREE, DB_CREATE, 0600, NULL, NULL, &db);
if(ret) {
    perror("db_open");
    exit(EXIT_FAILURE);
}

/* Initialize the key first */
memset(&key, 0, sizeof(key));
/* The key we want to find */
key.data = "one";
key.size = strlen("one") + 1;
/* Delete it */
ret = db->del(db, NULL, &key, 0);
if(ret == DB_NOTFOUND) {
    /* The key does not exist */
    fprintf(stderr, "key %s not found\n", (char *)key.data);
    exit(EXIT_FAILURE);
} else if(ret) {
    /* Some other error occurred */
    perror("del");
    exit(EXIT_FAILURE);
}

db->close(db, 0);
exit(EXIT_SUCCESS);
```

如果运行此程序两次，第二次运行时它会报告：未找到期望的键 `one`：

![](img/be588b36b489136ce784030a08a1d3d4_240_0.png)

```
$ ./deldb
$ ./deldb
key one not found
```

打开数据库后，`deldb` 试图删除键为 `one` 的记录。如果该键存在，`del` 调用将删除该记录及其关联值。`del` 调用可能失败，原因可能是键不存在（此时 `del` 返回 `DB_NOTFOUND`），或者发生了某种系统错误。另外请注意，该程序使用 `strlen("one") + 1` 来设置键的大小，而不是像上一个示例中使用 `sizeof` 运算符那样。

## 从数据库中检索项目

`get` 函数是从数据库中获取记录的最简单方式。它要求你知道想要获取的数据的键。其原型如下：

```c
int get(DB *db, DB_TXN *txnid, DBT *key, DBT *data, u_int32_t flags);
```

`get` 参数的含义和用法与 `put` 调用完全相同，不同之处在于 `get` 会填充 `data` 所引用的结构。如果找不到指定的键，`get` 将返回 `DB_NOTFOUND`。`flags` 可以是 `0` 或 `DB_GET_BOTH`，在后者情况下，只有当键和值都匹配提供的值时，`get` 才会检索该键/值对。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_241_0.png)

接下来的程序从数据库中检索一个值并显示出来。
