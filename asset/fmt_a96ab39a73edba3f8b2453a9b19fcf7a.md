
```
if (conn != NULL) PQfinish(conn);

exit(EXIT_FAILURE);

}
```

我们检查所有列中的 `NULL` 值。当我们运行它时，会得到：

Connected OK
2 columns in the result set
Field 0: Name age, Internal size 4
Field 1: Name fname, Internal size -1
DATA: 4
DATA: Adrian
DATA: 4
DATA: Allen
DATA: 1
DATA: NULL

这就是对 libpq 库的全部介绍。我们已经学习了如何使用 libpq 库访问数据库中的数据，并使用游标逐行检索数据。我们还看到了如何提取列信息以及处理数据库中的 `NULL` 值。

# 第 4 章

## ECPG

现在是时候查看结合 SQL 和 C 的替代方法了，通过将 SQL 语句嵌入 C 代码中，并在调用 C 编译器之前对其进行预处理，转换为 C 编译器可以理解的内容。虽然仍然有一个库来提供 C 调用与数据库的接口，但细节隐藏在预处理器之后。

PostgreSQL 的 `eccpg` 遵循在 C 代码中嵌入 SQL 的 ANSI 标准，对于用过 Oracle 的 PRO'C 或 Informix 的 SQL-C 等系统的程序员来说，接下来的内容将会非常熟悉。在编写时，嵌入 SQL 的某些用特性尚未支持，且随 PostgreSQL 一起分发的 `eccpg` 标准文档相当有限。

由于我们已经学习了许多 SQL 基础知识，这一部分实际上非常短。我们解决的第一个问题是界定 `eccpg` 预处理器需要处理的文件中的语句。这是通过源码中的特殊序列实现的，该序列以 `exec sql` 开头，包含你想要执行的 SQL，并以 `;` 结束。根据具体的语法，正如你稍后将看到的，这可以行需要处理的单行，也可以用于标记需要预处理的区域。

如果我们想写一个简单的 C 程序，在某些 C 代码中间执行单个的 `UPDATE` 语句，我们只需要在源码中做一件事——嵌入 `UPDATE` SQL 语句。

能更简单一点吗？让我们写一个带有嵌入 SQL 的非常简单的 C 程序来更新表。按照惯例，我们使用 `.pgc` 扩展名。以下是 `upd1.pgc`：

```c
#include <stdlib.h>

exec sql sqlca;

main() {
    exec sql connect to 'rick@gw';
    exec sql UPDATE children SET name = 'Gavin' WHERE childno = 9;
    exec sql COMMIT WORK;
    exec sql disconnect all;
    return EXIT_SUCCESS;
}
```

起初，这看起来完全不像 C 代码。然而，如果你忽略以 `exec sql` 开头的行，你会发现它只是一个最小的 C 程序。要编译此程序，我们需要两个阶段的过程。首先，我们必须运行 `eccpg` 预处理器，然后编译生成的 C 文件，并将其与 `eccpg` 库链接。为了编译此程序，你可能需要为 `eccpg` 添加 `-I` 选项，根据你的安装情况告诉它去哪里查找包含文件。对于这个程序，命令是：

```bash
$ ccpg -I/usr/include/postgresql upd1.pgc
$ gcc -o upd1 upd1.c -lpq
```

嵌入 SQL 时我们总是需要的功能是包含一个头文件。由于我们几乎总是需要它，`pgc` 文件通常于：

```c
exec sql include sqlca;
```

这会导致 `eccpg` 包含 `sqlca.h`，该文件默认情况下位于 `/usr/include/` 中，但取决于你的安装，它可能会不同。这个重要的包含声明了一个 `sqlca` 结构体，变量名相同，允许我们确定 SQL 语句的结果。

## 小结

让我们简单总结一下这个解释：

| `sqlca.code` | 严重错误时包含负值，0 表示成功，100 表示未找到数据。 |
| `sqlca.sqlerrm` | 包含文本错误消息。 |
| `sqlca.sqlerd[2]` | 包含影响的行数。 |
| `sqlca.sqlwarn[0]` | 当检索到数据但未正确传输到程序时，设置为 'W'。 |

尝试一下，通过修改我们的 `upd1.pgc` 文件以包含 `sqlca`，并使用无效的表名故意让失败：

```c
#include <stdlib.h>
#include <stdio.h>
exec sql include sqlca;
main() {
    exec sql connect to 'rick@gw';
    exec sql BEGIN WORK;
    exec sql UPDATE Children set name = 'Emma' WHERE age = 0;
    printf("error code %d, message %s, rows %d, warning %c\n", sqlca.sqlcode, sqlca.sqlerrm.sqlerrm, sqlca.sqlerd[2], sqlca.sqlwarn[0]);
    exec sql COMMIT WORK;
    exec sql disconnect all;
    return EXIT_SUCCESS;
}
```

这是 `upd2.pgc`。高亮行显示了重要的变化。按如下方式编译：

```
ecpg -I/usr/include/postgresql upd2.pgc
gcc -g -o upd2 -I /usr/include/postgresql/ upd2.c -lepq -lpq
```

这一次当我们运行它时，生成了一个错误：

```
error code -400, message Postgres error: ERROR: XXchildren: Table does not exist.
line 10, rows 0, warning
```

如你所见，它虽然基础但有效。

现在我们已经了解了基础知识，可以讨论一个重要问题——我们如何访问嵌入在 `.pgc` 文件中的 SQL 语句返回的数据？

## PostgreSQL 接口

答案实际上非常简单，依赖于被称为主机变量的变量，这些变量可以被由 `exec sql ...;` 限定的语句和普通的 C 编译器共同访问。

我们通过一个声明区域来实现这一点，该区域会被 `ecpg` 处理器和 C 编译器共同处理。这是通过在特殊的声明区域内声明 C 变量实现的，这也告诉了 `ecpg` 处理器处理它们。我们使用限定语句：

```
exec sql begin declare section;
```

以及

```
exec sql end declare section;
```

假设我们想声明两个变量 `child_name` 和 `child_age`，它们旨在嵌入式 SQL 和程序剩余部分的 C 代码中都是可访问的。我们需要：

```
exec sql begin declare section;
```

```
int child_age;
VARCHAR child_name[50];
```

```
exec sql end declare section;
```

你会注意到这里有两个奇怪的地方，首先是作为字符串的“魔术数字”50，其次是 `VARCHAR` 不是一个普通的 C 类型。我们被迫在这里使用字面量，因为这部分代码在 C 编译器运行之前就会被 `ecpg` 处理了，因此无法使用 `#define` 或常量。使用 `VARCHAR` 的原因是 `children` 表中 `fname` 列的 SQL 类型不是一个由 `ecpg` 预处理器在 C 编译器看到它之前转换为合法的 C 结构的类型。我们必须在声明中使用 PostgreSQL 类型，源文件中该行的结果是创建一个名为 `child_name` 的结构，它包含两个成员：一个字符数组 `arr` 和一个整数 `len`，用于存储 C 编译器从这一行看到的内容实际上是：

```
struct varchar_child_name (int len; char arr[50]); child_name;
```

现在我们有两个变量，在 SQL 和 C 中都是可见的。我们使用 SQL 语法的扩展 `into` 关键字将数据从表中检索到命名变量中，这些变量通过在名称前加上冒号 `:` 来定义。这意味着它们不会与值或表名混淆。注意，`into` 与某些厂商支持的允许从一个表选择数据到另一个表的扩展不同。在嵌入式 SQL 中，`into` 关键字的含义略有不同。

```
exec sql SELECT fname into :child_name FROM children WHERE age = :child_age;
```
