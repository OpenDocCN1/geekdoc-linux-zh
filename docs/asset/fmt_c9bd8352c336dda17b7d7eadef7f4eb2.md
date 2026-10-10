
尽管 `MySQL` 和 `PostgreSQL` 等关系型数据库兴起，`dbm` 数据库在 Linux 中继续发挥着重要作用。使用 `RPM` 的发行版（如 `Red Hat` 和 `SuSE`）使用 `dbm` 作为已安装包信息的底层存储。`LDAP` 的开源实现 `Open LDAP` 也使用 `dbm` 作为一种存储机制。`dbm` 的优势在于它更容易被构建到分布式二进制文件中，因为不需要安装独立的服务器，而且底层库未安装的风险很小。

## 数据管理

`dbm` 数据库允许你使用索引存储大小可变量的结构，并使用索引或顺序扫描数据库来检索结构。`dbm` 数据库用于频繁访问但极少更新的数据，因为创建条目的速度通常比检索速度慢。

到这里，我们遇到了一个小问题：多年来，`dbm` 数据库出现了几个变体，它们的 API 和功能略有不同。原始的 `dbm` 集合、“新”`dbm` 集合、`ndbm` 以及 GNU 的实现 `gdbm`。GNU 的实现也可以模拟旧的 `dbm` 和 `ndbm` 接口，但其原生接口与其他实现相比在本质上有所显著不同。不同的 Linux 发行版带有不同版本的 `dbm` 库，尽管最常见的选择是使用 `gdbm` 库，其安装方式使其能够模拟另外两种接口类型。

在这里我们将集中在 `ndbm` 接口上，因为它没有经过 `X/OPEN` 标准，而且使用原始 `dbm` 实现用起来稍微简单。

## 获取 dbm

如果你对 `dbm` 的其他实现感兴趣，可以在 `http://cs.berkeley.edu/ucb/4bs/` 或通过 `http://www.openbase.org` 找到一个基于 `BSD` 许可的版本。`Sleepcat Software` (`http://www.sleepcat.com`) 是一个开源项目 `The Berkeley Database`，它支持 `dbm`/`ndbm` 历史接口。GNU 版本可以在 `http://www.gnu.org` 找到。

## 故障排除与重装 dbm

本章的编写假设你已经安装了兼容 `X/OPEN` 版本的 `dbm`。如果你在编译这些示例时遇到困难——无论是缺少 `ndbm.h` 头文件、编译器抱怨 `dbm` 未定义，还是程序的编译链接阶段失败——请尝试安装更新的 GNU 版本的 `dbm` 库。

检查你拥有哪个版本，最简单的方法是寻找 `gdbm.h`、`ndbm.h` 和 `dbm.h` 文件。你可能会发现它们后来位于 `/usr/include/gdbm` 等子目录下，这种情况说明底层实现是 `gdbm`。

# 数据管理

如果你熟悉 `SQL` 数据库，你会注意到 `dbm` 数据库并没有关联的表或列结构。这些结构是没有必要的，因为 `dbm` 既不对要存储的每项数据施加固定大小，也不要求数据具有内部结构。`dbm` 库在非结构化的二进制数据块上进行工作。

# dbm 访问函数

现在我们已经介绍了 `dbm` 库工作的基础，可以详细查看这些函数了。主体 `dbm` 函数的原型如下：

```
#include <dbm.h>
```

```
DBM *dbm_open(const char *filename, int file_open flags, mode_t file_mode);
int dbm_store(DBM *descriptor, datum key, datum content, int store_mode);
datum dbm_fetch(DBM *descriptor, datum key);
void dbm_close(DBM *descriptor);
```

# dbm_open

此函数用于打开现有数据库，也可以用于创建新数据库。`filename` 参数是基础文件名，不包含 `.dir` 或 `.pag` 扩展名。

其余参数与你在第 3 章中遇到的 `open` 函数的第二、第三参数相同。我们可以使用 `#defines`。第二个参数控制数据库是否可以只读（`OR`）、写入或两者兼有。如果你正在创建一个新数据库，`flags` 必须与 `O_CREATE` 进行按位或操作以允许创建文件。第三个参数指定将创建的文件的初始权限。

`dbm_open` 返回一个指向 `dbm` 类型的指针。这用于后续对数据库的所有访问。如果失败，则返回 `(DBM *) 0`。

# dbm_store

使用此函数向数据库输入数据。正如我们之前提到的，所有数据都必须使用唯一索引存储。为了定义我们要存储的数据以及引用它的索引，我们设置了两个 `datum` 类型：一个用于引用索引，另一个用于实际数据。最后一个参数 `store_mode` 控制当尝试使用已存在的键（`key`）存储数据时会发生什么。如果设置为 `dbm_insert`，则存储将失败；如果设置为 `dbm_replace`，则新数据将覆盖现有数据且 `dbm_store` 返回 0。在其他错误情况下，`dbm_store` 将返回负数。

# dbm_fetch

`dbm_fetch` 例程用于从数据库检索数据。它接收一个由之前的调用 `dbm_open` 返回的 `dbm` 指针和一个 `datum` 类型（该类型必须设置为指向一个键）。返回一个 `datum` 类型。如果在数据库中找到了与键相关的数据，返回的 `datum` 结构体的 `dptr` 和 `dsize` 值将指向返回的数据。如果未找到键，`dptr` 将设置为 `null`。

# 第 7 章

> 记住，`dbm_fetch` 返回的只是一个包含数据指针的 `datum`。实际数据可能仍存储在 `dbm` 库内部的本地存储空间中，在调用任何其他 `dbm` 函数之前，应将其复制到程序变量中。

# dbm_close

此例程关闭通过 `dbm_open` 打开的数据库，必须传递之前调用 `dbm_open` 返回的 `dbm` 指针。

# 尝试一下——简单的 dbm 数据库

现在我们已经学习了 `dbm` 数据库的基本函数，已经有足够的知识来编写第一个 `dbm` 程序：`dbm.c`。在这个程序中，我们将使用一个名为 `test_data` 的结构。

1.  首先，这里是包含文件、`#defines`、主函数以及 `test_data` 结构的声明：

    ```
    #include <unistd.h>
    #include <stdlib.h>
    #include <stdio.h>
    #include <fcntl.h>
    #include <ndbm.h>
    #include <string.h>

    #define TEST_DB_FILE "/tmp/dbml_test"
    #define ITEMS_USED 3

    struct test_data {
        char misc_chars[15];
        int any_integer;
        char more_chars[21];
    };

    int main() {
    ```

2.  在 `main` 内部，我们设置了 `items_to_store` 和 `items_received` 结构、字符串以及数据类型：

    ```
    struct test_data items_to_store[ITEMS_USED];
    struct test_data item_retrieved;

    char key_to_use[20];
    int i, result;

    datum key_datum;
    datum data_datum;

    DBM *dbm_ptr;
    ```

    在了一个指向 `dbm` 结构指针后，我们现在打开测试数据库进行读写，并在必要时创建它：

    ```
    dbm_ptr = dbm_open(TEST_DB_FILE, O_RDWR | O_CREAT, 0666);
    if (!dbm_dptr) {
        fprintf(stderr, "Failed to open database");
        exit(EXIT_FAILURE);
    }
    ```

    现在我们向 `items_to_store` 中添加一些数据：

    ```
    strcat(items_to_store[1].misc_chars, "bar");
    items_to_store[1].any_integer = 13;
    strcat(items_to_store[1].more_chars, "unlucky?");
    ```

    ```
    strcat(items_to_store[2].misc_chars, "Third");
    items_to_store[2].any_integer = 3;
    strcat(items_to_store[2].more_chars, "baz");
    ```

    对于每个条目，我们需要构建一个引用的键。这是字符串的首字母和整数。这个键随后通过 `key_datum` 标识，而 `data_datum` 指向 `items_to_store`。我们将其存入数据库。
