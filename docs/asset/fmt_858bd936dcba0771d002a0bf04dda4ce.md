
# 第 6 章：数据库

## 删除数据

```c
err = db_delete(&db, NULL, key, strlen(key)+1, 0);

if (err != DB_SUCCESS) {
    fprintf(stderr, "Error deleting from database: %s\n", dbstrerror(err));
    exit(1);
}
```

## 关闭数据库

最后，当你完成数据库操作时，必须关闭它：

```c
int db_close(DB *db);
```

`db` 参数是待关闭数据库的句柄。

## 打开数据库

如果你正在打开一个现有的数据库，也可以为类型参数指定 `DB_UNKNOWN` 值。如果使用此值，Berkeley DB 将尝试自动确定现有数据库的类型。如果它无法识别数据库类型，`open()` 函数将执行失败。

`flags` 参数指定了如何打开数据库文件。有效值见下表。

| Flag | 描述 |
| --- | --- |
| `DB_AUTO_COMMIT` | 使用事务打开数据库文件。如果调用成功，则打开操作将是可恢复的。如果调用失败，则不会创建数据库文件。 |
| `DB_CREATE` | 如果数据库不存在，则创建它。 |
| `DB_DIRTY_READ` | 数据库上的读取操作可能会请求返回已修改但未保存的数据。 |
| `DB_EXCL` | 如果数据库已存在，则返回错误。 |
| `DB_NOMMAP` | 不将数据库文件映射到内存。 |
| `DB_RDONLY` | 以只读模式打开数据库。 |
| `DB_THREAD` | 使返回的 `DB` 句柄可被多个线程使用。 |
| `DB_TRUNCATE` | 将数据库文件中已存在的任何其他文件截断。 |

Flag 值可以使用逻辑或符号 (`|`) 组合起来。例如，你可以指定标志 `DB_CREATE | DB_EXCL`，这将创建一个新的数据库文件，但如果数据库文件已存在则失败。默认情况下，`DB_CREATE` 标志会打开一个现有数据库。

`mode` 参数指定了文件的 Unix 系统格式。输入值 0 表示所有者和组都具有读写权限，而其他所有人没有权限。此值可以使用标准的 Unix 文件名设置（例如 0664）来指定。

这里是一个创建一个 `DB` 句柄并打开新数据库的示例：

```c
DB *dbp;
int ret;

ret = db_create(&dbp, NULL, 0);
if (ret != 0) {
    perror("create");
    return 1;
}

ret = dbp->open(dbp, NULL, "test.db", DB_BTREE, DB_CREATE, 0);
if (ret != 0) {
    perror("open");
    return 1;
}
```

在这个简短的代码段中，使用 `db_create()` 函数创建了 `DB` 句柄 `dbp`，然后使用它通过 B 树数据库格式以及默认的所有者和组权限创建（或如果已存在则打开使用）数据库文件 `test.db`。

## 添加新数据

现在你已经打开了数据库文件，是时候向其中放入数据了。实现此功能的函数是 `put()`。`put()` 函数如下：

```c
int DB->put(DBT *db, TXN *txn, DBT *key, DBT *data, uint32_t flags)
```

`db` 和 `txn` 参数与 `open()` 函数相同，指定 `DB` 句柄和事务。`key` 和 `data` 参数指定了用于存储数据的数据库键值对。用于每个项的 `DBT` 结构体定义了一个数据元素。因此，`key.data` 包含记录键，而 `data.data` 包含记录数据。

`flags` 参数指定了新数据如何放入数据库中。对于 `DB_QUEUE` 和 `DB_RECNO`，可以使用 `DB_APPEND` 标志将记录添加到数据库文件的末尾。对于 `DB_BTREE` 和 `DB_HASH` 数据库，可以使用 `DB_CREATE` 标志仅在键/数据对不存在时添加记录。`DB_OVERWRITE` 标志用于防止新数据覆盖现有的键。很多人认为这仅限制为记录中的单个数据值。但数据值可以是任何数据类型，包括结构体。C 结构体的每个实例都作为数据值存储在数据库文件中。这在列表 6-1 所示的 `employee.c` 程序中得到了演示。

### 列表 6-1：向 Berkeley DB 数据库添加记录

```c
/*
 * 专业 Linux 编程 - 添加新记录
 */

#include <stdio.h>
#include <db.h>

#define DATABASE "employees.db"

int main() {
    DBT key, data;
    DB *dbp;
    int ret;
    struct data_struct {
        int empid;
        char lastname[50];
        char firstname[50];
        float salary;
    } emp;

    ret = db_create(&dbp, NULL, 0);
    if (ret != 0) {
        perror("create");
        return 1;
    }

    ret = dbp->open(dbp, NULL, DATABASE, NULL, DB_BTREE, DB_CREATE, 0);
    if (ret != 0) {
        perror("open");
        return 1;
    }

    while (1) {
        printf("Enter Employee ID: ");
        scanf("%d", &emp.empid);
        if (emp.empid == 0)
            break;

        printf("Enter Last Name: ");
        scanf("%s", emp.lastname);
        printf("Enter First Name: ");
        scanf("%s", emp.firstname);
        printf("Enter Salary: ");
        scanf("%f", &emp.salary);

        memset(&key, 0, sizeof(DBT));
        memset(&data, 0, sizeof(DBT));

        key.data = &emp.empid;
        key.size = sizeof(emp.empid);
        data.data = &emp;
        data.size = sizeof(emp);

        ret = dbp->put(dbp, NULL, &key, &data, DB_CREATE);
        if (ret != 0) {
            printf("Employee ID already exists\n");
        }
    }

    dbp->close(dbp, 0);
    return 0;
}
```

列表 6-1 中的 `employee.c` 程序创建了一个 `DB` 句柄并将 `employees.db` 文件作为独立数据库打开（注意 `.db` 文件扩展名不是强制要求的，但它通常用于识别数据库文件）。接下来，使用 `while()` 循环向用户查询新员工的信息。用于数据库数据元素的 `emp` 结构体包含一个整数 ID、字符字符串 `lastname` 和 `firstname`，以及一个浮点数 `salary` 值。从用户处获得的值被放入 `emp` 结构体中。在使用 `key` 和 `data` `DBT` 对象之前，始终使用 `memset` 函数清空内存位置是一个好习惯。随后，将 `key` 值设置为员工 ID，并将 `data` 值设置为整个 `emp` 结构体。一旦准备就绪，使用 `DB_CREATE` 标志执行 `put()` 函数，以确保在尝试使用相同的员工 ID 时会报错。注意，如果你想更新现有的员工记录，只需移除 `DB_CREATE` 标志即可。

`while()` 循环进入员工 ID 输入 0。当循环退出时，使用 `close()` 函数正确关闭数据库。编译此应用程序（记住使用正确的头文件和库文件），然后运行它。你应该能够将员工记录添加到数据库中。当你停止程序时，你应该能在目录下看到 `employees.db` 数据库文件。

## 获取数据

一旦数据放入数据库文件，在某个时刻你可能想要获取它。使用 `get()` 函数来实现：

```c
int DB->get(DB *db, TXN *txn, DBT *key, DBT *data, uint32_t flags)
```

与其他函数一样，`db` 参数指定已打开的数据库句柄，`txn` 参数指定事务。`key` 和 `data` 参数都是持有键和数据的 `DBT` 对象。在函数完成时，`data` 参数将填充相应的数据。

`flags` 参数指定了在获取数据时执行的操作。值 0 表示仅获取数据而不执行任何操作。可以使用以下标志：

| Flag | 描述 |
| --- | --- |
| `DB_CONSUME` | 在 `DB_QUEUE` 类型的数据库中，获取队列头的记录并从数据库中删除。 |
| `DB_CONSUME_WAIT` | 与 `DB_CONSUME` 相同，但队列为空则等待记录出现。 |
| `DB_GET_BOTH` | 仅当指定的键和数据与数据库匹配时，返回键/数据对。 |
| `DB_SET_RECNO` | 从数据库中检索键和数据值，而不仅仅是数据值。只能用于 `DB_BTREE` 数据库。 |
| `DB_DIRTY_READ` | 读取未提交的数据。 |
| `DB_MULTIPLE` | 返回多个数据元素。如果 `data.size` 值不够大，则将其设为包含所有数据元素所需的大小。 |
| `DB_RMW` | 在执行检索时获取写锁而非读锁。用于事务。 |

在列表 6-2 中，`employee.c` 程序演示了如何从数据库文件中检索数据：

### 列表 6-2：从 Berkeley DB 数据库检索记录

```c
/*
 * 专业 Linux 编程 - 检索员工记录
 */

#include <stdio.h>
#include <db.h>

#define DATABASE "employees.db"

int main() {
    DBT key, data;
    DB *dbp;
    int ret;
    struct data_struct {
        int empid;
        char lastname[50];
        char firstname[50];
        float salary;
    } emp;

    ret = db_create(&dbp, NULL, 0);
    if (ret != 0) {
        perror("create");
        return 1;
    }

    ret = dbp->open(dbp, NULL, DATABASE, NULL, DB_BTREE, DB_CREATE, 0);
    if (ret != 0) {
        perror("open");
        return 1;
    }

    while (1) {
        printf("Enter Employee ID: ");
        scanf("%d", &emp.empid);
        if (emp.empid == 0)
            break;

        memset(&key, 0, sizeof(DBT));
        memset(&data, 0, sizeof(DBT));

        key.data = &emp.empid;
        key.size = sizeof(emp.empid);
        data.data = &emp;
        data.ulen = sizeof(emp);
        data.flags = DB_DBT_USERMEM;

        ret = dbp->get(dbp, NULL, &key, &data, 0);
        if (ret != 0) {
            printf("Employee ID does not exist\n");
        } else {
            printf("Employee: %d - %s,%s\n", emp.empid, emp.lastname, emp.firstname);
            printf("Salary: $%.2f\n", emp.salary);
        }
    }

    dbp->close(dbp, 0);
    return 0;
}
```

列表 6-2 展示了创建 `DB` 句柄并打开 `employees.db` 数据库文件的标准方法。`while()` 循环首先询问用户要搜索的员工 ID 值。同样，使用 `memset` 函数来清除键数据值，并将员工 ID 输入到 `key.data` 元素中。`data` 元素被设置为 `data_struct` 的一个空实例。

`data` 元素还包含可以指定如何处理数据的标志。`DB_DBT_USERMEM` 标志告诉 Berkeley DB，程序已经设置了自己的内存区域，以便在返回数据后进行处理。

当执行 `get()` 函数时，返回的数据被放在 `emp` 结构体并显示在控制台上。`while()` 循环一直持续，直到输入的员工 ID 为 0。

## 删除数据

另一个实用的功能是从数据库文件中移除记录的能力。`del()` 函数用于：

```c
int DB->del(DB *dbp, DB_TXN *txnid, DBT *key, u_int32_t flags)
```

删除操作基于函数调用中提供的键值。在 Berkeley DB 的当前版本中，`flags` 参数未使用，应设置为 0。

列表 6-3 所示的 `delete.c` 程序演示了如何使用 `del()` 函数删除 `employees.db` 数据库中的指定记录。

### 列表 6-3：从 Berkeley DB 数据库中移除记录

```c
/*
 * 专业 Linux 编程 - 移除员工记录
 */

#include <stdio.h>
#include <db.h>

#define DATABASE "employees.db"

int main() {
    DBT key;
    DB *dbp;
    int ret;
    struct data_struct {
        int empid;
        char lastname[50];
        char firstname[50];
        float salary;
    } emp;

    ret = db_create(&dbp, NULL, 0);
    if (ret != 0) {
        perror("create");
        return 1;
    }

    ret = dbp->open(dbp, NULL, DATABASE, NULL, DB_BTREE, DB_CREATE, 0);
    if (ret != 0) {
        perror("open");
        return 1;
    }

    while (1) {
        printf("Enter Employee ID: ");
        scanf("%d", &emp.empid);
        if (emp.empid == 0)
            break;

        memset(&key, 0, sizeof(DBT));
        key.data = &emp.empid;
        key.size = sizeof(emp.empid);

        ret = dbp->del(dbp, NULL, &key, 0);
        if (ret != 0) {
            printf("Employee ID does not exist\n");
        } else {
            printf(" Employee %d deleted.\n", emp.empid);
        }
    }

    dbp->close(dbp, 0);
    return 0;
}
```

到此时，你已经熟悉了程序的大部分内容。用户指定要删除的员工 ID，该值存储在 `key.data` 元素中，并执行 `del()` 函数。如果删除成功，函数返回值为 0。如果数据库中不存在该键，`del()` 函数将返回 `DB_NOTFOUND` 值。

## 使用游标

`get()` 函数只有在已经知道有效键值的情况下才能检索到数据值。有时，你可能需要在不知道键值是什么的情况下从数据库文件中提取数据。

Berkeley 使用了一种名为“游标”（cursors）的概念来遍历数据库中包含的记录。游标对象用于指向数据库中的某条记录。你可以逐条向前或向后移动游标，以检索下一条或上一条记录。一旦游标到达某条记录，你就可以检索数据、删除它指向的记录，或者在该位置向数据库中插入一条新记录。

使用 `cursor()` 函数从为数据库创建的标准 `DB` 句柄可以创建一个 `DBC` 游标对象：

```c
int DB->cursor(DB *db, DB_TXN *txnid, DBC **cursorp, u_int32_t flags);
```

`cursor()` 函数创建一个指向游标的指针，并将其赋值给 `DBC` 对象指针。一旦创建了游标，就可以使用 `c_get()`、`c_put()` 或 `c_del()` 函数在游标指向的数据库文件所在的位置上获取、存入或删除记录。

当你需要列出数据库中包含的每条记录时，遍历数据库记录就变得非常有用。列表 6-4 所示的 `listemployees.c` 程序演示了如何使用数据库文件中的游标列出所有记录。

### 列表 6-4：从 Berkeley DB 检索多个记录

```c
/*
 * 专业 Linux 编程 - 列出所有记录
 */

#include <stdio.h>
#include <db.h>

#define DATABASE "employees.db"

int main() {
    DBT key, data;
    DB *dbp;
    DBC *cursor;
    int ret;
    struct data_struct {
        int empid;
        char lastname[50];
        char firstname[50];
        float salary;
    } emp;

    ret = db_create(&dbp, NULL, 0);
    if (ret != 0) {
        perror("create");
        return 1;
    }

    ret = dbp->open(dbp, NULL, DATABASE, NULL, DB_BTREE, DB_CREATE, 0);
    if (ret != 0) {
        perror("open");
        return 1;
    }

    ret = dbp->cursor(dbp, NULL, &cursor, 0);
    if (ret != 0) {
        perror("cursor");
        return 1;
    }

    memset(&key, 0, sizeof(DBT));
    memset(&data, 0, sizeof(DBT));

    key.data = &emp.empid;
    key.size = sizeof(emp.empid);
    data.data = &emp;
    data.ulen = sizeof(emp);
    data.flags = DB_DBT_USERMEM;

    while (cursor->c_get(cursor, &key, &data, 0) == 0) {
        printf("Employee: %d - %s %s\nSalary: $%.2f\n", emp.empid, emp.firstname, emp.lastname, emp.salary);
    }

    cursor->close(cursor);
    dbp->close(dbp, 0);
    return 0;
}
```
