
| `mysql_select_db` | `int mysql_select_db (MySQL *connection, const char *dbname);` | 只要用户有适当权限，即可将默认数据库更改为参数指定的数据库。成功时返回 0。 |

| `mysql_shutdown` | `int mysql_shutdown (MySQL *connection);` | 如果你有适当权限，将关闭你连接的数据库服务器。成功时返回 0。 |

# CD 数据库应用程序

现在我们将看到如何创建一个简单的数据库来存储关于你的 CD 信息，然后编写一些代码来访问这些数据。我们现在要创建一个简单的数据库来存储关于你的 CD 信息，然后编写一些代码来访问这些数据。我们将保持非常简单，以便于理解。我们首先创建一个数据库，然后使用它：

```sql
create database blcd;
Database changed;
```

# 第 8 章

## 创建表

现在我们需要确定表的结构。我们将从主表——CD 表开始，它包含了大部分信息。我们需要一个 `id`、一个目录号、标题以及可能的注释：

```sql
CREATE TABLE cd (
  id INTEGER AUTO_INCREMENT PRIMARY KEY,
  title VARCHAR(70) NOT NULL,
  artist_id INTEGER NOT NULL,
  catalogue VARCHAR(30)
);
```

- 一个 `id` 列，自增且是该表的主键
- 标题，最多70个字符
- `artist_id`，整数，我们将用于艺术家表
- 目录号，最多30个字符
- 100个字符的注释

注意只有 `notes` 列可以为空；其他列必须有值。现在是 `artist` 表：

```sql
CREATE TABLE artist (
  id INTEGER AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL
);
```

同样我们有一个 `id` 列和另一个用于艺术家名称列。

最后是 `track` 表：

```sql
CREATE TABLE track (
  cd_id INTEGER NOT NULL,
  track_id INTEGER NOT NULL,
  title VARCHAR(70),
  PRIMARY KEY (cd_id, track_id)
);
```

注意我们声明主键的方式不同。`track` 表的寻常之处在于 `id` 会出现多次，而任何给 `track` `ID`（例如 `track` `one`）在不同的 CD 中也会出现多次。然而，它们的组合是唯一的，因此我们将主键声明为列的组合。这被称为复合键；因为它由多个列组合。

将此 SQL 存储在名为 `create_table.sql` 的文件中，保存在当前目录下，然后并在其中创建数据库和这些表。提供的示例脚本如果表已存在，也会删除它们。

```bash
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \
Your MySQL connection id is 50
Type 'help' or 'h' for help. Type '\c' to clear the buffer.

mysql> use blcd;
Database changed
mysql> \. create_tables.sql
Query OK, 0 rows affected (0.04 sec)
Query OK, 0 rows affected (0.10 sec)
Query OK, 0 rows affected (0.00 sec)
mysql>
```

## 第 8 章

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_391_0.png)

图 8-8

## 添加一些数据

现在我们需要添加一些数据。检查任何数据库设计的最好方法是添加一些示例数据并检查它们是否正常工作。

我们在这里只展示测试导入数据的一个样本，因为对于理解正在发生的情况这并不重要，因为所有的导入基本上都是相似的——它们只是加载了不同的表。这里有两个重要的点需要注意：

- 脚本会删除任何现有数据，以确保脚本从干净的位置开始。
- 将值插入到 `ID` 字段中，而不是让 `AUTO_INCREMENT`（自动递增）发生作用。在这里这样做更安全，因为不同的插入操作需要知道哪些值已被使用，以确保所有数据关系都是正确的，因此最好是强制指定值，而不是让 `AUTO_INCREMENT` 函数自动分配值。

此文件名为 `insert_data.sql`，可以使用我们之前看到的 `\` 命令执行。

350

```sql
-- 删除现有数据
delete from track;
delete from cd;
delete from artist;

-- 现在开始插入数据

-- 首先是艺术家（或团体）表
insert into artist(id, name) values(1, 'Pink Floyd');
insert into artist(id, name) values(2, 'Genesis');
insert into artist(id, name) values(3, 'Einaudi');
insert into artist(id, name) values(4, 'Melanie C');

-- 然后是 cd 表
insert into cd(id, title, artist_id, catalogue) values(1, 'Dark Side of the Moon',
1, 'B00002AD4P');
insert into cd(id, title, artist_id, catalogue) values(2, 'Wish You Were Here', 1,
'B00002AD4DS');
insert into cd(id, title, artist_id, catalogue) values(3, 'A Trick of the Tail', 2,
'B00002AEXMY');
insert into cd(id, title, artist_id, catalogue) values(4, 'Selling England by the
Round, 'B00002A5M');
insert into cd(id, title, artist_id, catalogue) values(5, 'I Giorni', 3,
'B00007WEVY');
insert into cd(id, title, artist_id, catalogue) values(6, 'Northern Star', 4,
'B00004YMS7');

-- 填充曲目
insert into track(cd_id, track_id, title) values(1, 1, 'Speak to me');
insert into track(cd_id, track_id, title) values(2, 2, 'Breathe');
```

以及该专辑的剩余曲目，然后是下一个：

```sql
insert into track(cd_id, track_id, title) values(2, 1, 'Shine on crazy
diamond');
insert into track(cd_id, track_id, title) values(2, 2, 'Welcome to the machine');
insert into track(cd_id, track_id, title) values(2, 3, 'Have a cigar');
insert into track(cd_id, track_id, title) values(2, 4, 'Wish you were here');
insert into track(cd_id, track_id, title) values(2, 5, 'Shine on you crazy diamond
pt2');
```

以此此类……

```sql
insert into track(cd_id, track_id, title) values(4, 1, 'Melodia Africana (part
1)');
insert into track(cd_id, track_id, title) values(4, 2, 'I due fiumi');
insert into track(cd_id, track_id, title) values(4, 3, 'In un\'altra vita');
```

直到最后的曲目：

```sql
insert into track(cd_id, track_id, title) values(6, 11, 'Closer');
insert into track(cd_id, track_id, title) values(6, 12, 'Feel The Sun');
```

## 第 8 章

接下来将此内容保存为 `pop_tables.sql`，并像之前一样在 `mysql` 提示符中使用 `\.` 命令执行。

注意在 `cd` `4` (`I` `Giorni`) 的第 3 首曲目中，曲目名为 "Un un'altra"，带有一个撇引号。为了将其插入数据库，我们必须使用反斜杠 (`\`) 来转义撇引号。

## 尝试一下

现在是检查数据看起来是否合理的好时机。我们可以使用 `mysql` 命令行客户端和一些 SQL 来检查数据是否合理。我们首先从数据库中的每张专辑选择前两个曲目：

```sql
SELECT artist.name, cd.title AS "CD Title", track.track_id, track.title AS "Track" FROM artist, cd, track WHERE artist.id = cd.artist_id AND track.cd_id = cd.id AND track.track_id = track.track_id < 3
```

如果我们在 `MySQL` 中尝试这样做，你可以看到数据看起来如如图 8-9 所示。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_393_0.png)

## 工作原理

这段 SQL 看起来很复杂，但如果你一段一段来看，它并不难。

忽略 `SELECT` 命令中的 `AS` 部分，第一部分仅仅是：

```sql
SELECT artist.name, cd.title, track.track_id, track.title
```

这通过 `tableName.column.name` 告诉我们想要显示哪些列。

352

`SELECT` 语句中的 `AS` 部分，即 `SELECT` `artist.name`、`cd.title` `AS` `"CD` `Title"`、`track.track_id` 和 `track.track_id` `AS` `"Track"`，仅仅是重命名了输出中的列。在这里，`cd` 表的表头 (`cd.title`) 被命名 `"CD` `Title"`，`track.track_id` 列的标题为 `"Track"`。使用 `AS` 为我们提供了更符合用户习惯的输出。从另一种语言调用 SQL 时，你几乎不会使用这些名称，但 `AS` 在命令行上处理 SQL 时非常有用。下一部分也同样直观；它告诉了我们正在使用的表名：

```sql
SELECT artist, cd, track
```

`WHERE` 子句是稍微有点的地方：

```sql
WHERE artist.id = cd.artist_id AND track.cd_id = cd.id AND track.track_id = track.track_id < 3
```

`database_start("rick", "foobar");`

然后我们测试一张 CD：

```c
res = add_cd(Mahler, "Symphony No 1", "4596102", &cd_id);
printf("Result of adding a cd was %d\n", res, cd_id);

memset(ct, 0, sizeof(ct));
ct.cd_id = &cd_id;
strpy(ct.track[0], "Langsam Schleppend");
strpy(ct.track[1], "Kraftig bewegt");
strpy(ct.track[2], "Feierlich und gemessen");
strpy(ct.track[3], "Sturmisch bewegt");
add_tracks(&ct);
```

现在搜索该 CD 并从找到的第一张 CD 中检索：

```c
res = find_cds("Symphony", &cd_res);
printf("Found %d cds, first has ID %d\n", res, cd_res.cd_id[0]);

res = get_cd(cd_res.cd_id[0], &cd);
printf("%get_cd returned %d\n", res);

memset(ct, 0, sizeof(ct));
res = get_cd_tracks(cd_res.cd_id[0], &ct);
printf("%get_cd_tracks returned %d\n", res);
printf("Title: %s\n", cd.title);
i = 0;
while (i < res) {
    printf("\track %d is %s\n", i, ct.track[i]);
    i++;
}
```

最后，我们删除这张 CD：

```c
res = delete_cd(cd_res.cd_id[0]);
printf("Delete_cd returned %d\n", res);
```

然后我们断开并退出：

```c
database_end();

return EXIT_SUCCESS;
}
```

## 实现接口

现在到了更困难的部分：实现我们指定的接口。这些内容都在 `app_mysql.c` 文件中。

我们从一些基础头文件开始，我们需要的全局连接结构、一个标志位 `disconnected`，我们将用它来确保应用程序在没有连接的情况下不访问数据。我们还使用了一个内部函数 `get_artist_id` 来优化代码结构。

## 第 8 章

```c
#include <stdlib.h>
#include <stdio.h>
#include <string.h>

#include "mysql.h"
#include "app_mysql.h"

static MYSQL my_connection;
static int dbconnected = 0;

static int get_artist_id(char *artist);
```

获取数据库连接非常简单，正如我们在章节开头看到的那样，而断开连接更加容易：

```c
int database_start(char *name, char *pwd) {
  if (dbconnected) return 1;

  mysql_init(&my_connection);
  if (!mysql_real_connect(&my_connection, "localhost", name, pwd, "blpcd", 0,
  NULL, 0)) {
    fprintf(stderr, "Database connection failure: %d, %s\n", mysql_errno(my_connection), mysql_error(my_connection));
    return 0;
  }
  dbconnected = 1;
  return 1;
} /* database_end */

void database_end() {
  if (dbconnected) mysql_close(&my_connection);
  dbconnected = 0;
} /* database_end */
```

现在真正的工作开始了，即函数 `add_cd`。我们会先给您提供一些声明，以及一个健全检查，以确保我们已连接到数据库。我们将在编写的所有外部可访问函数中看到这一点。

记住，我们会自动处理艺术家名称：

```c
int add_cd(char *artist, char *title, char *catalogue, int *cd_id) {

  MYSQL_RES *res_ptr;
  MYSQL_ROW mysqlrow;

  int res;
  char is[100];
  char es[100];
  int artist_id = -1;
  int new_cd_id = -1;

  if (!dbconnected) return 0;
```

我们接下来做的事情是检查艺术家是否存在；如果没有，就创建一个。这将在稍后的 `get_artist_id` 函数中处理。

```c
artist_id = get_artist_id(artist);
```

现在有了 `artist_id`，我们可以插入主 CD 记录。注意我们使用了 `mysql_escape_string` 来保护 CD 标题中的特殊字符。
