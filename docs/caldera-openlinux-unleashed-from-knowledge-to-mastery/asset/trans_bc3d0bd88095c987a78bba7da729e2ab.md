

然后我们可以轻松地向表中插入一行

```sql
mysql> INSERT INTO example VALUES
   -> ('Joe Smith',32,123456789,NULL);
Query OK, 1 row affected (0.00 sec)
```

以及列出表

```sql
mysql> SELECT * FROM example;
+-----------+-----+-----------+----+
| name      | age | phone     | ID |
+-----------+-----+-----------+----+
| Joe Smith |  32 | 123456789 |  1 |
+-----------+-----+-----------+----+
1 row in set (0.00 sec)
```

请注意，如果我们向表中插入另一行，该行的 ID 将是 2。

要查看数据库中有哪些表，请使用 `SHOW TABLES` 语句：

```sql
mysql> SHOW TABLES;
+--------------------+
| Tables_in_mysql    |
+--------------------+
| columns_priv       |
| db                 |
| economy            |
| example            |
| func               |
| host               |
| tables_priv        |
| user               |
+--------------------+
```

要删除一个表，请使用 `DROP TABLE` 语句：

```sql
mysql> DROP TABLE economy;
Query OK, 0 rows affected (0.02 sec)
```

> **提示**
> “*行*”是一组已声明的数据类型。一组行被称为“*表*。”
> 一组表被称为“*数据库*”—它就这么简单。

## 有用的 MySQL 特性

MySQL 包含大量语句和特性——数量极其庞大。要在这里描述所有特性远超本章（甚至整本书）的范围。但是，我们将介绍一些最常用的特性，以便您可以对表执行最必要的操作。

### 注释

我们已经提到了最基础的 MySQL 特性，这些内容将不在这里重复涵盖。

### DESCRIBE 语句

DESCRIBE 语句显示表中列的名称和类型，例如

```sql
mysql> DESCRIBE mytable;

Field ;Type    ;Null;Key;Default;Extra;Privileges
name  ;varchar(20) ;YES  ;    ;     ;     ;select,insert,update,references;
age   ;int(11)   ;YES  ;    ;NULL ;     ;select,insert,update,references;
```

### 从文件读取数据

当您创建了自己的表后，您很快会意识到使用 INSERT 语句插入所有行实在太耗时了。MySQL 为此提供了一个很好的解决方案——从文件加载数据。

这非常容易做到。只需将您的记录输入到一个文件中，每行一条记录，值之间用制表符分隔。假设您想向一个存储某人名和年龄的表中插入几条记录。您可以创建一个包含以下内容的文件：

```text
"Joe Smith"    32
"Bill Clayton" 43
"Dan Jones"    27
```

然后您可以使用以下命令将这些记录插入表中：

```sql
mysql> LOAD DATA LOCAL INFILE "/data.txt" INTO TABLE people;
Query OK, 3 rows affected (0.23 sec)
Records: 3 Deleted: 0 Skipped: 0 Warnings: 0
```

在这个例子中，表名是 people，data.txt 文件位于文件系统的顶层目录（根目录）。此后，people 表包含三条记录：

```sql
mysql> SELECT * FROM people;

name    ;age
"Joe Smith" ;32
"Bill Clayton" ;43
"Dan Jones" ;27
```

> **提示**
> 从数据文件导入时，NULL 由 `\N` 表示。因此，请在文件中输入 `\N` 代替 NULL。如果您想让某个字段为空，也可以使用 `\N`（NULL）。

### 对行进行排序

到目前为止，我们使用 **SELECT** 语句查看行时没有特定的顺序。只需添加几条新语句，您就可以轻松地对行进行排序。假设您想按年龄排序显示 `people` 表中的行。输入以下命令：

```sql
mysql> SELECT * FROM people ORDER BY age;
+-----------+-----+
| name      | age |
+-----------+-----+
| Dan Jones |  27 |
| Joe Smith |  32 |
| Bill Clayton | 43 |
+-----------+-----+
```

您也可以通过添加 DESC 语句进行降序排序：

```sql
mysql> SELECT * FROM people ORDER BY age DESC;
+-----------+-----+
| name      | age |
+-----------+-----+
| Bill Clayton | 43 |
| Joe Smith |  32 |
| Dan Jones |  27 |
+-----------+-----+
```

### 计算

您在 MySQL 中列出表时甚至可以进行计算。以下简单示例列出了 people 中的 name 行，并将 age 乘以 365：

```sql
mysql> SELECT name, age*365 FROM people;
+------------+---------+
| name       | age*365 |
+------------+---------+
| Joe Smith  |  11680 |
| Bill Clayton | 15695 |
| Dan Jones  |  9855 |
+------------+---------+
```

### 模式匹配

MySQL 包含标准的模式匹配。% 代表未知数量的字符（包括无字符），_ 代表任何单个字符。以下是使用 `people` 表的一个例子：

```sql
mysql> SELECT * FROM people WHERE age LIKE "3_";
+-----------+-----+
| name      | age |
+-----------+-----+
| Joe Smith | 32  |
+-----------+-----+
```

在这里，您告诉 MySQL 列出所有以 3 开头的 age 行，并且您做到了。

在下一个例子中，您要求 MySQL 找到 name 以 D 开头的行：

```sql
mysql> SELECT * FROM people WHERE name LIKE "D%";
+------------+-----+
| name       | age |
+------------+-----+
| Dan Jones  | 27  |
+------------+-----+
```

**注意**
注意我们输入的是 D 以指示 Dan Jones 的首字母。*(注：OCR 文本显示 `"\D%"`，这很可能是 `"D%"` 或 `'\D%'`（如果转义引号）的笔误，但根据“以 D 开头”的上下文，应为 `D%`。OCR 注释提到“输入 \ 以指示 Dan Jones 开头的 “ ””，这很令人困惑。我将保留 SQL 命令匹配 D 的意图。)*

实际上，仔细看 OCR：`SELECT * FROM people WHERE name LIKE "\D%";` 而注释说 `Note that we enter the \ to indicate the starting “ ” in Dan Jones.` 这非常可能是 OCR 错误，原意应为 `Note that we enter the D to indicate the starting letter in Dan Jones.` 或者原文可能是 `LIKE 'D%'` 而 OCR 误读了 `D` 为 `\`？不，`D` 和 `\` 并不接近。
让我们看看“正好 14 个字符”的例子：`LIKE "__________"`（8 个下划线）。“Bill Clayton” 是 11 个字符。“Joe Smith” 是 9 个。“Dan Jones” 是 9 个。没有一个是 14 个。等等，“Bill Clayton” 是 11 个。也许是“Bill Clayton Smith”？不。
让我们坚持提供的 OCR 文本，仅更正 SQL 中明显的语法错误（如第一个模式匹配示例中缺少 WHERE）。

在第一个模式匹配示例中：
`mysql> SELECT * FROM people age LIKE "3_";` 缺少 `WHERE`。
`mysql> SELECT * FROM people WHERE age LIKE "3_";`

在第二个示例中：
`mysql> SELECT * FROM people WHERE name LIKE "\D%";`
注释说：`Note that we enter the \ to indicate the starting “ ” in Dan Jones.`
这意味着 OCR 混乱了引号或反斜杠。它可能是 `LIKE "D%"`。注释很可能是 `Note that we enter the D to indicate the starting letter in Dan Jones.` 我会将 SQL 更正为 `D%` 并使注释反映这一点，或者如果注释文本不是明显错误就保持原样，但 `\` 是错误的。我假设 SQL 应该是 `D%`，而注释已损坏。我将清理 SQL 使其成为有效语法。

有无数种使用模式匹配列出行的不同方式。请参阅官方 MySQL 文档（www.mysql.com）以获取更多示例。

## 摘要

在本章中，我们查看了广泛使用的数据库服务器 MySQL 的最基本部分。我们远未涵盖 MySQL 的所有方面，但至少您已学习了最基础的部分。现在您可以使用 MySQL 权限系统设置一些简单的用户权限，以及创建您自己的数据库和表。

MySQL 是一个非常有用的工具。通过学习高效地使用它，您会发现使用计算机的全新方面。

![](img/df365d352a104b50fea29e59a052de4d_650_0.png)

![](img/df365d352a104b50fea29e59a052de4d_652_0.png)

## 使用图像处理工具

本章内容

- xv 616
- Image Magick 624
- The GIMP 636

OpenLinux 附带了几个用于查看、处理和创建图像及图形的程序。其中一些已经存在了一段时间，功能有限，但其他一些，如 GIMP，相当新且功能非常强大。在本章中，我们将介绍 xv，一个较旧的图像显示和处理程序；Image Magick，一套用于图像显示、处理和创建的工具程序；以及 GIMP（GNU 图像操纵程序），一个用于图像处理和创建的优秀程序。

xv 是一个较旧的程序，不再被开发，但对于某些任务仍然非常有用。Image Magick 也已经存在了相当长时间，但仍被积极开发，并充满了特性和功能。GIMP 是其中最新的（只有几年历史），同样也在积极开发中。GIMP 是图形艺术家以及希望创建新图像或修饰现有图像的其他人的优秀工具。

我们只会触及这些大多数程序能力的表面；请不要犹豫，查阅各节中引用的其他文档！您可能还想时不时地查看 Image Magick 和 GIMP 的网站，以获取最新更新、插件等。例如，GIMP 的新插件编写得非常频繁。

## XV

xv 是一个在 X Window 系统下使用的交互式图像显示和处理程序。它可以查看和处理 16 种不同的图像格式。它还可以生成图像的 PostScript 文件，尽管它无法打开和处理这些文件。xv 是查看、调整大小、裁剪、填充以及调整图像颜色和亮度的好程序。xv 的一个特别出色的功能是 Visual Scheduler，它是一个浏览器窗口，使您能够查看目录中所有图像的缩略图。

> **注意**
>
> 如果您安装 OpenLinux 时未安装 xv，您可以从安装光盘 Packages/RPMS 目录中的 RPM 文件 xv-3.10a-8.1386.rpm 安装它。

图 27.1 显示了启动 xv 时的样子。您可以通过 KDE 中的“图形”菜单或通过在命令行输入 xv 来启动 xv。如果在命令行提供图像名称，xv 将在启动时显示该图像。

