
运行脚本后，服务器返回所有区段数大于5的对象：

OWNER SEGMENT_NAME
DEMO EMPLOYEE 6
DEMO JOB 9
DEMO DEPARTMENT 12

## 导入和导出会话的操作演示

前面的方法需要了解表空间中包含的所有对象。在一种更耗耗时的方法中，你可以对整个数据库进行碎片整理。这可以通过导出整个数据库、使用 `CREATE DATABASE` 命令删除并重新创建数据库，然后导入整个导出文件来实现。

## 将数据库对象从一个模式移动到另一个模式

在很多时候，在模式之间之间移动对象是非常重要的。例如，一个开发者想要有一组表进行测试，但不想影响原始模式中的数据。这对于复制表实例也有用。

首先，为给定的用户账户导出所有内容。通过指定导出实用程序的 `OWNER` 参数来实现。在本文示例中，你会将 `DEMO` 模式复制到 `QUE` 模式，如图 30.6 所示。

图 30.6
将 DEMO 模式复制到 QUE 模式

![](img/563fad4219fcb3a5c1f1e5cc91d831ce_730_0.png)

如果导入的任何对象与现有对象冲突，则仅跳过冲突的对象。

接下来，创建一个尚不存在的新所有账户。此时，你可以通过指定导入实用程序中的 `FROMUSER` 和 `TOUSER` 参数来导入到新模式，如图 30.7 所示。

> **William Page 的第 #91 条提示**
如果你有 `BFILE` 数据，Oracle 仅在数据库中存储指向文件的指针。如果你从一个数据库导出并导入到不同服务器上的另一个数据库，请务必复制所有需要的文件并将放在相同的目录路径下。否则，Oracle 将无法访问相关的 `BFILE` 文件。

## 多个对象和多个对象类型

如果你想将部分表从一个模式移动到另一个模式，或者为了备份目的，需要在导出期间的 `TABLES` 参数规范中指定对象列表。在导入时必须结合 `FROMUSER` 和 `TOUSER` 使用。

要导出一个表，请指定所有者，后接句点和表名，例如 `Owner.Table_Name`。要导出分区，指定所有者，后接句点和表名，然后是逗号，最后是分区名，例如 `Owner.Table_Name:Partition_Name`。

### 图 30.8
将 DEMO 用户账户的所有对象导入到 QE 用户账户。

![](img/563fad4219fcb3a5c1f1e5cc91d831ce_732_0.png)

图 30.9 显示了导出多个对象和对象类型的示例：`PRICE` 表，以及 `EMP` 表五个分区中的两个（`LOW_SALARY` 和 `MEDIUM_SALARY`）。

要将多个对象和对象类型导入到不同的用户账户，请使用指定的 `FROMUSER` 和 `TOUSER` 子句导入。如果你想导入到同一个用户账户，请使用 `FULL=Y` 或所有者指定子句。

## 分区级导入

分区级导入将源表的一组分区或子分区导入到目标表。

注意以下几点：
- 导入始终根据目标表的分区方案存储行。
- 分区级导入允许你从导出文件中的指定分区或子分区中有选择性地检索数据。
- 分区级导入仅插入指定源分区或子分区的行数据。
- 如果目标表是分区的，分区级导入将拒绝任何超出目标表最高分区的行。
- 分区级导入只能在表模式下指定。
- 分区级导出和导入不支持拆分分区。

图 30.9 导出多个对象和对象类型的示例。

![](img/563fad4219fcb3a5c1f1e5cc91d733_0.png)

## 当表空间不匹配时的行为识别

当导入对象时，Oracle 尝试在与其导出时相同的表空间中创建它。有时，当在一个数据库上执行导出并导入到另一个数据库时，表空间并不总是匹配的。例如，导出数据库中的一个对象存储在 `DBA_TOOLS` 表空间中。在导入该对象的数据库中，没有 `DBA_TOOLS` 表空间。

在这种情况下，在导入过程中，导入实用程序尝试在 `DBA_TOOLS` 中创建对象，但由于目标数据库中没有该表空间而失败。然后，导入程序尝试将表创建在对象对象所有者的默认表空间中。如果空间足够且所有者在表空间上有适当的配额，则对象会被导入。否则，将发生错误，且对象不会被导入。

## 将数据库对象从一个表空间移动到另一个表空间

默认情况下，导入尝试在与其导出时相同的表空间中创建对象。如果用户没有该表空间的权限或该表空间不再存在，Oracle 在该用户账户的默认表空间中创建数据库对象。这些属性可以通过导出和导入将数据库对象从一个表空间移动到另一个表空间。要为 `USER_A` 将所有对象从 `TABLESPACE_A` 移动到 `TABLESPACE_B`，请遵循以下步骤：

## 使用 SHOW 和 INDEX 选项

1. 为 `USER_A` 导出 `TABLESPACE_A` 中的所有对象。
2. 执行 `REVOKE UNLIMITED TABLESPACE ON TABLESPACE_A FROM USER_A;` 以取消授予用户账户的任何无限表空间权限。
3. 在表空间上执行 `ALTER USER USER_A QUOTA 0;`。
4. 执行 `ALTER USER USER_A QUOTA UNLIMITED ON TABLESPACE_B;`。
5. 使用导入实用程序并指定 `FROMUSER=USER_A` 和 `TOUSER=USER_A`。
6. 在导入命令中指定 `TABLESPACE=TABLESPACE_B`。
7. 执行导入操作。
8. 验证对象是否已移动。

# 可迁移表空间

```
COMMENT ON COLUMN "PRICE".PRODUCT_ID IS '适用价格的产品编号。在 PRICE 表中可以产品名称';
COMMENT ON COLUMN "PRICE".LIST_PRICE IS '未打折价格（美元$）';
ALTER TABLE "PRICE" ADD FOREIGN KEY (PRODUCT_ID) REFERENCES PRODUCT (PRODUCT_ID) ENABLE;
```

你可以使用 `INDEXFILE` 参数来生成 `INDEX` 语句。`INDEXFILE` 参数的值指定要创建的文件名。默认情况下，除非另有指定，否则 Oracle 会追加 .SQL 扩展名。文中显示了通创建表语句，这些语句已注释，因此在运行脚本时不会执行。`INDEXFILE` 参数不会生成主键或唯一键。列表 30.5 是指定的 `INDEXFILE=X.LOG` 生成的输出文件 `X.LOG` 的部分。请注意 Oracle 如何对所有行进行自动换行，并且没有在每行前后添加引号。这使得索引文件无需进一步修改即可直接投入使用。

```
CREATE TABLE "QUE".PRICE ("PRODUCT_ID" NUMBER(6, 0), "LIST_PRICE" NUMBER(8, 2), "MIN_PRICE"(8, 2), "START_DATE", "END_DATE" DATE) PCTFREE 10 INITRANS 40 MAXITRANS 1 MAXRANS 255 LOGGING STORAGE(INITIAL 10240 NEXT 10240 MINEXTRANS 1 MAXEXTRANS 121 PCTINCREASE 50 FREELISTS 1 FREELIST GROUPS 1) TABLESPACE "USER_DATA";

-- ... 58 rows

QUE;

CONNECT QUE;

CREATE UNIQUE INDEX "QUE".I_PRICE ON "PRICE" ("PRODUCT_ID", "START_DATE") PCTFREE 10 INITRANS 2 MAXRANS 255 STORAGE (INITIAL 10240 NEXT 10240 MINEXTRANS 1 MAXEXTRANS 121) PCTINCREASE 50 FREELISTS 1) TABLESPACE "USER_DATA" LOGGING;
```
