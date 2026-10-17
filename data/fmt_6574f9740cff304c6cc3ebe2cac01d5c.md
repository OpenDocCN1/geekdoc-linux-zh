
## B.5 附录总结

在本附录中，你学习了如何使用 SQL 语言创建数据库模式，以及如何从数据库中插入、更新、检索、修改和删除记录。

## B.6 你应该知道什么

- 1. 如何从数据库表中检索所有记录？
- 2. 如何根据特定标准从表中检索选定的记录集或单条记录？
- 3. 如何在数据库中筛选和排序记录？
- 4. 如何从数据库中筛选一行或多行数据？
- 5. 如何创建一个数据库？
- 6. 如何创建数据库表？
- 7. 如何为字段分配主键？
- 8. 记录是如何插入到数据库表中的？
- 9. 表中的记录是如何更新的？
- 10. 如何删除一条记录？

## 练习 B
### 你懂我的语言吗？

- 1. 进入 MySQL 控制台，使用 `show` 命令列出所有数据库。使用 `mysql` 数据库。现在显示它的所有表。
- 2. 创建一个名为 `school` 的新数据库。创建数据库后，你需要能够使用它：`use school`;
- 3. 创建一个名为 `student` 的表。该表将包含以下字段：
    - `FirstName`
    - `LastName`
    - `Email`
    - `CellPhone`
    - `Major`
    - `GPA`
    - `StartDate`
    - `StudentId`（主键）

以下信息是你将用于定义表的数据类型。请上网查找类似的表格作为参考。

| 数据类型 | 描述 |
| :--- | :--- |
| `integer`(size) | |
| `int`(size) | |
| `smallint`(size) | |
| `tinyint`(size) | 仅存储整数 |

括号中的 `size` 指定最大位数。

| 数据类型 | 描述 |
| :--- | :--- |
| `decimal`(size, d) | |
| `numeric`(size, d) | 存储带小数的数字。 |

`size` 中指定的数字是最大位数。`d` 中指定的数字是小数点右边的最大位数。

| 类型 | 描述 |
| :--- | :--- |
| char(size) | 存储固定长度的字符串（可以包含字母、数字和特殊字符）。括号中的 size 指定固定大小。 |
| varchar(size) | 存储可变长度的字符串（可以包含字母、数字和特殊字符）。括号中的 size 指定最大大小。 |
| date(yyyy/mm/dd) | 存储日期。 |

- 4. 使用 SQL `describe` 语句显示用于创建 `school` 数据库的信息。
- 5. 向表中插入三行数据：

第 1 行：
| 字段 | 值 |
| :--- | :--- |
| FirstName | John |
| LastName | Doe |
| Email | johndoe@smileyface.edu |
| CellPhone | 408-333-3456 |
| Major | CIS |
| GPA | 2.8 |
| StartDate | 09/22/2004（使用正确的日期格式！） |
| StudentID | 1 |

第 2 行：
| 字段 | 值 |
| :--- | :--- |
| FirstName | Mary |
| LastName | Chin |
| Email | mchin@qmail.com |
| CellPhone | 408-204-1234 |
| Major | Biology |
| GPA | 3.3 |
| StartDate | 06/22/2003 |
| StudentID | 2 |

第 3 行：
| 字段 | 值 |
| :--- | :--- |
| FirstName | Sadish |
| LastName | Pamel |
| Email | sadis@univ_ab.edu |
| CellPhone | 415-204-1234 |
| Major | CIS |
| GPA | 3.9 |
| StartDate | 06/22/2003 |
| StudentID | 2 |

- 6. 使用 `show` 命令显示所有字段。
- 7. 使用 `select` 语句显示以下内容（在空白行中编写你的查询）：
    - a. 所有列的数据
    - b. 学生的姓名和姓氏
    - c. 学生的姓名、姓氏和专业
    - d. 学生的手机和电子邮件地址
    - e. 任何不同的专业
    - f. 仅 2 行
- 8.
    - a. 选择 GPA 超过 3.0 的所有学生。
    - b. 选择 GPA 在 3.0 和 4.0 之间的所有学生。
    - c. 选择手机号码在 408 区号的学生。
    - d. 显示 2003 年入学的学生的行。
    - e. 选择主修 CIS 且 GPA 超过 3.5 的学生姓名。
    - f. 如果电子邮件地址以 `.com` 结尾，则选择学生的名字和电子邮件地址。
- 9.
    - a. 向表中插入一条新记录。
    - b. 按姓氏对学生表进行排序。
    - c. 按 GPA 降序对学生表进行排序。
- 10. 将 Mary 的电话号码改为 650-123-4563。
- 接下来的三个问题涉及 SQL 函数：
- 11. 找出所有学生的平均 GPA。
- 12. 找出表中的行数。
- 13. 使用 SQL 函数打印今天的日期。

## 附录 C
### 简介 Moose（Perl 5 的后现代对象系统）

![](img/8556abcb353c0991f12099420ec28735_804_0.png)

Moose 为你提供了一种替代方案，以旧式方法编写面向对象的 Perl，如第 14 章“Bless Those Things!（面向对象的 Perl）”所述。它通过引入 C++ 和 Java 程序员熟悉的特性来现代化 Perl 的对象系统，使 Perl 的 OO 更加一致、易用和强大。（Moose 基于元对象编程（MOP）的思想，这意味着对象系统本身也是一个对象，一个构建在 Perl OO 系统之上的框架。）

Moose 是 Perl 5 对象系统的扩展，它通过提供一组导出的函数来声明类、提供属性和访问器方法、设置默认值、执行继承、类型验证等，从而简化了创建类的过程。它简化了编写面向对象 Perl 的过程，使你能够专注于项目而不是机制。但你并不因为使用 Moose 就被限制为只能按 Moose 的方式做每件事；它在那里帮助你，并提供强大的扩展来执行许多 OO 任务。首先，请查看 Moose::Manual 文档：

```
perldoc Moose::Manual
```

## C.1 入门

要在命令行获取文档，请输入：

```
perldoc Moose
```

或访问网站，<http://metacpan.org/pod/Moose>。

要在你的程序开始，请输入：

```
use Moose;
```

## C.2 构造函数

父类将是 `Moose::Object`（除非你的类已经有父类），虽然起初我们不会担心 `Moose::Object`，只需知道它的存在。当你加载 Moose 时，`strict` 和 `warnings` 会自动为你打开。`Moose::Object` 提供了一个名为 `new` 的默认构造函数，允许你在创建对象时无需担心移位掉类名、“加冕”（blessing）等复杂操作。

Moose 创建类，调用构造函数，将对象加冕（bless），并返回加冕后的哈希引用。（当带参数调用 `new` 构造函数时，它接受哈希或哈希引用，否则会产生错误。）以下是一个极简的 Moose 脚本：

```perl
# (Module Dog.pm)

package Dog;

use Moose;    # Load Moose

1;

--------------------------

# (user.pl)

use Dog;

my $dogref = Dog->new;

# Call Moose constructor; get back a reference to a hash.

use Data::Dumper;

print Dumper($dogref);

# Displays a blessed object in the Dog class

--------------------------

# (Output)

$VAR1 = bless( {}, 'Dog' );
```
