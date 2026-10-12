

你可以看到，迄今为止为 allusers 数据库定义的唯一表是名为“names”的表。

### 3. 要显示“names”表的格式，请在 mysql> 提示符下键入以下命令：

```
mysql> DESCRIBE names;
+-----------+-------------+------+-----+---------+-------+
| Field     | Type        | Null | Key | Default | Extra |
+-----------+-------------+------+-----+---------+-------+
| firstname | varchar(20) |      |     |         |       |
| lastname  | varchar(20) |      |     |         |       |
| streetaddr| varchar(30) |      |     |         |       |
| city      | varchar(20) |      |     |         |       |
| state     | varchar(20) |      |     |         |       |
| zipcode   | varchar(10) |      |     |         |       |
+-----------+-------------+------+-----+---------+-------+
```

### 4. 要为新表添加数据，你可以从 mysql> 提示符使用 `INSERT INTO` 命令。以下是向新表中添加人员姓名和地址的示例：

```
mysql> INSERT INTO names
    -> VALUES ('Jerry','Wingnut','167 E Street',
    -> 'Roy','UT','84103');
```

在此示例中，INSERT INTO 命令指定了“names”表。然后它表明该表中一条记录的值包括名为 Jerry Wingnut 的人，地址为 167 E Street, Roy, UT 84103。

### 5. 要检查数据是否正确输入到新表中，请在 mysql> 提示符下键入以下命令：

```
mysql> SELECT * FROM names;
+-----------+---------+-------------+------+-------+--------+
| firstname | lastname| streetaddr   | city | state | zipcode |
+-----------+---------+-------------+------+-------+--------+
| Jerry     | Wingnut | 167 E Street | Roy  | UT    | 84103   |
+-----------+---------+-------------+------+-------+--------+
```

输出结果显示了你刚刚输入的数据，以你在 names 表中定义的列进行显示。如果你喜欢，可以继续以这种方式添加数据。

逐个输入每个数据项可能很繁琐。作为替代方案，你可以将数据添加到纯文本文件中，然后将其加载到你的 MySQL 数据库中。

## 从文件加载数据

在 mysql 会话期间使用 LOAD DATA 命令，你可以将包含数据库记录的文件加载到你的 MySQL 数据库中。以下是创建要加载到 MySQL 的数据文件时你需要了解的几件事。

-   你可以使用任何 Linux 文本编辑器创建该文件。
-   每条记录（包含表中的所有列）必须位于单独的一行。（换行符表示下一条记录的开始。）
-   使用制表符（Tab）字符分隔每一列。
-   如果要使某条记录的特定列为空，可以在该列位置放置 \N。
-   如果在文件中留有空行，数据库表中也会出现空行。

在此示例中，下文所示的文本被添加到纯文本文件中。该文本的格式可以加载到本章前面创建的"names"表中。要尝试此方法，请键入以下文本到一个文件中。确保在每个值之间插入制表符（此处用多个空格表示）。

| Chris Smith | 175 Harrison Street | Gig Harbor | WA | 98999 | | John Jones | 18 Talbot Road NW | Coventry | NJ | 54889 | | Howard Manty | 1515 Broadway | New York | NY | 10028 |

完成数据输入后，将文本保存到任何可访问的文件名（例如，`/tmp/mysql_names.txt`）。请记住该文件名，以便稍后输入。如果你尚未连接到 mysql 会话，请键入以下命令（假设 mysql 用户名为 root）：

```sql
mysql -u root -p
Enter password: ******
mysql>
```

接下来，通过键入以下内容，将数据库（本例中为 allusers）指定为当前数据库：

```sql
mysql> USE allusers;
Database changed
```

要实际将文件加载到 allusers 数据库中的 names 表，请从 `mysql>` 提示符键入以下命令来加载该文件（在本例中为 `/tmp/mysql_names.txt`）。

> **注意：** 输入文件的完整路径，或者将文件放置在 mysql 命令启动的目录中。在后一种情况下，你可以输入文件名而不指定其完整路径。

```sql
mysql> LOAD DATA INFILE "/tmp/mysql_names.txt" INTO TABLE names;
Query OK, 3 rows affected (0.02 sec)
Records: 3 Deleted: 0 Skipped: 0 Warnings: 0
```

在 `mysql>` 提示符下键入以下内容，以确保记录已正确添加：

```sql
mysql> SELECT * FROM names;
```

| firstname | lastname | streetaddr | city | state | zipcode |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Howard | Mancy | 1515 Broadway | New York | NY | 10028 |

### 了解 MySQL 表

在设置 MySQL 表时，你有很大的灵活性。为了让 MySQL 数据库尽可能高效地运行，你希望列被分配最适合的容量和数据类型，以存储你需要保存的数据。

你可以使用以下表格作为列可分配的不同数据类型的参考。MySQL 中可用的数据类型分为以下几类：数字、时间/日期和字符字符串。在阅读这些表格时，有以下几点需要知道：

-   列的**最大显示大小**为 **255 个字符**。数据类型的"M"选项表示显示（并且在大多数情况下，也是存储）列的字符数。
-   **浮点**数据类型的小数点后最多可以有 **30 位数字**。数据类型的"D"选项表示小数点后允许的浮点数位数。（该值应比正在使用的显示大小值少两位以上。）
-   **UNSIGNED** 选项（在括号中显示）表示只允许在该列中输入正数。这使得列可以容纳更大的正数。
-   **ZEROFILL** 选项（在括号中显示）表示该列中的数据将用零填充。例如，数据类型为 **INTEGER (7) ZEROFILL** 的列中的数字 **25** 将显示为 **0000025**。（任何 **ZEROFILL** 列自动变为 **UNSIGNED**。）
-   括号中显示的所有值都是可选的。
-   如果输入 (M) 和 (D) 值中的任意一个，则必须使用括号。换句话说，不要输入括号，但要输入圆括号。

表 24-2 显示了你可以与 MySQL 一起使用的数字数据类型。

### 表 24-2: 列的数字数据类型

| 数据类型 | 描述 | 所需空间 |
|---|---|---|
| BIGINT[(M)] [UNSIGNED] [ZEROFILL] | 可以包含大整数，允许的值如下：<br>-9223372036854775808 到 9223372036854775807 (无符号)<br>0 到 18446744073709551615 (有符号) | 使用 8 字节 |
| DECIMAL[(M[,D])] [ZEROFILL] | 包含非打包的浮点数（仅支持有符号数）。每位数字存储为单个字符。当你选择显示值 (M) 时，小数点和减号不计入该值。(M) 的值默认为 10。将 D 设置为零（这是默认值）会导致仅使用整数。 | 如果 D 大于 0，使用 M+2 字节<br>如果 D 等于 0，使用 M+1 字节 |
| DOUBLE[(M,D)] [ZEROFILL] | 包含平均大小的双精度浮点数。允许的值包括：-1.7976931348623157E+308 到 -2.2250738585072014E-308 0<br>2.2250738585072014E-308 到 1.7976931348623157E+308。 | 使用 8 字节 |
| DOUBLE PRECISION | 与 DOUBLE 相同。 | 与 DOUBLE 相同。 |
| FLOAT(X) [ZEROFILL] | 包含浮点数。对于单精度浮点数，X 可以小于或等于 24。对于双精度浮点数，X 可以在 25 和 53 之间。显示大小和小数位数未定义。 | 使用 4 字节 |

