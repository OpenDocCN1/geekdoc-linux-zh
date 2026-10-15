
| TYPE_ID | OID | NAME | BIRTHYEAR | SALARY | MAJOR | ARCHIVE |

|---|---|---|---|---|---|---|

| 105 | 10 | John | 1968 | | - | - |

| 107 | 30 | Pat | 1970 | 60000 | - | - |

| 109 | 50 | Franz | 1975 | | Pol | 2.5 |

图 7–50 层次表（H-Table）的逻辑视图

H-Table 的第一列是 `TYPE_ID`。该列的每个值指定了插入行的类型化表结构。一旦定义了结构化类型和类型化表，DB2 系统目录表就会存储它们的信息。可以通过图 7–51 所示的 `SYSCAT.TYPES` 视图查看每个结构化类型。`SYSCAT.TYPES` 视图中的 `SOURCE` 列是创建根类型时通过 `REF USING` 子指定的内置类型名称。你可以看到 `EMP_T` 和 `STUDENT_T` 继承了根类型 `PERSON_T` 的属性。

```sql
SELECT TYENAME, SOURCE, METATYPE FROM SYSCAT.TYPES
```

| TYENAME | SOURCE | METATYPE |

|---|---|---|

| PERSON_T | INTEGER | R |

| EMP_T | INTEGER | R |

| STUDENT_T | INTEGER | R |

图 7–51 类型化表的系统目录视图

在此示例中，仅提取了结构化类型的行。`SOURCE` 列将为 `NULL`，内置类型的 `METATYPE` 列将为 `R`。对于用户定义类型，`METATYPE` 列将为 `T`。

`SYSCAT.HIERARCHIES` 系统目录视图包含了子表与其直接父表之间、以及子类型与其直接父类型之间的关系。图 7–52 显示了来自 `SYSCAT.HIERARCHIES` 的某些信息。

```sql
SELECT METATYPE, SUB_NAME, SUPER_NAME, ROOT_NAME FROM SYSCAT.HIERARCHIES;
```

| METATYPE | SUB_NAME | SUPER_NAME | ROOT_NAME |

|---|---|---|---|

| R | EMP_T | PERSON_T | PERSON_T |

| R | STUDENT_T | PERSON_T | PERSON_T |

| U | EMP | PERSON | |

| U | STUDENT | PERSON | |

图 7–52 层次关系的系统目录视图

`SYSCAT.HIERARCHIES` 视图的 `METATYPE` 列将对象的关系类型编码如下：

- R - 结构化类型之间
- U - 类型化表之间
- W - 类型视图之间

类型视图将在本章后后描述。

## 引用列

在类型化表定义中，可以将列定义为指向另一个类型化表的引用列。被引用的类型化表被称为目标表。引用列持有与目标表 `OID` 值对应的值并清晰地标识目标表中的行。引用列的数据类型为 `REFERENCE`，与目标表中的 `OID` 类型相同。引用列类似于外键；但是，不像外键，在插入、更新或删除等操作时不进行评估。

查看图 7–53。它显示了一个类型化表 `EMP`，它有一个指向另一个类型化表 `DEPT` 的引用列。这种关系在执行 `CREATE TABLE` 语句时定义，被称为范围（scope）。

DEPT

| OID | NAME | LOCATION |

|---|---|---|

| 45 | ADV | DALLAS |

| 2 | ADM | AUSTIN |

EMP

| OID | NAME | SALARY | DEPREF |

|---|---|---|---|

| 23 | JON | 45000 | 2 |

| 67 | MEL | 60000 | 88 |

```sql
INSERT INTO Dept VALUES (Dept_t (2), 'ADM','AUSTIN')
INSERT INTO Emp VALUES (Emp_t (23), 'JON',45000,Dept_t (2))
```

图 7–53 引用列关系

如图 7–53 所示，引用列可以具有目标表所不具有的值。注意转换函数 `DEPT_T` 用于为引用列提供值。

引用列通过 `CREATE TYPE` 和 `CREATE TABLE` 语句定义。图 7–54 显示了设置引用列的 `CREATE TYPE` 语句，假设根类型 `PERSON_T` 已经定义，如第 379 页的图 7–44 所示。

### 结构化类型与类型表

```sql
CREATE TYPE Dept_t AS (name CHAR(40),location CHAR(20))
REF USING INTEGER MODE DB2SQL;
```

```sql
CREATE TYPE Emp_t UNDER Person_t
AS (Salary INTEGER, Deptref REF(Dept_t)) MODE DB2SQL;
```

图 7-54 定义引用列的 Create 类型语句

在我们的示例中，`DEP_T` 是一个不同表层次结构的根类型，它与 `EMP_T` 和 `PERSON_T` 所属于的层次不同。`EMP_T` 的定义提供了两个属性：一个是 `SALARY`，类型为 `INTEGER`；另一个是 `DEPTREF`，引用类型。`Deptref(Dept_t)` 意味着类型为 `type_t` 的属性 `DEPTREF` 是引用类型，且引用的目标是行类型为 `DEP_T` 或其子类型的表行。

你需要根据图 7-54 中定义的结构化类型创建类型表。图 7-55 显示了用于定义引用列（定义范围）的示例 `CREATE TABLE` 语句。此示例中的第二个 `CREATE TABLE` 语句创建了一个带有引用列的表。

```sql
CREATE TABLE Of Dept_t (REF IS OID GENERATED);

CREATE TABLE Of Emp_t UNDER Person
INHERIT SELECT PRIVILEGES
(Deptref REF WITH OPTIONS SCOPE DEPT);
```

图 7-55 创建带有引用列的表

在 `CREATE TABLE` 语句中，`DEPTREF WITH OPTIONS SCOPE DEPT` 意味着 `DEPTREF` 列中的值指向 `DEPT` 表中的行或 `DEPT` 表中任何子表中的值。

## 解引用运算符

解引用操作符 (`->`) 从具有匹配 `OID` 列的行返回目标表或其子表的具名列值。下面的示例显示了一个使用解引用运算符的 `SELECT` 语句。

```sql
SELECT E.name from E
WHERE E.Deptref->location='AUSTIN';
```

## 第 7 章 高级 SQL

在这个示例中，每个 `DEPTREF` 列的值都经过了查询和检查。我们检查目标表（`DEPT` 表）或其子表是否存在 `OID` 值相同的行。如果找到了这样的行，则从该行获取 `LOCATION` 列的值并返回。该 `DEPTREF->LOCATION` 能够正常工作。如果返回值为 `AUSTIN`，则该谓词为真。

上述使用解引用运算符 (`->`) 的 `SELECT` 语句可以使用 `JOIN` 操作重写。接下来的示例显示了使用 `JOIN` 操作的对应 SQL 语句。

```sql
SELECT E.name from emp E, dept D
WHERE E.deptref = D.oid
AND D.location = 'AUSTIN'
```

## 视图层次结构

类型视图是定义基于结构化类型的视图。你可以像使用类型表创建表层次结构一样，使用类型视图创建层次结构。图 7–56 显示了定义类型视图的 `CREATE VIEW` 语句。在我们的示例中，使用 `PERSON_T` 类型和 `EMP_T` 类型创建了两个类型视图 `PERSON_V` 和 `EMP_V`。`PERSON_V` 视图定义为层次结构的根视图，引用 `PERSON` 表的所有列和行。`EMP_V` 视图被定义为 `PERSON_V` 视图的子视图，引用 `EMP` 表的所有列和行。

注意，`PERSON_V` 的定义使用了 `ONLY` 子句，因此只从 `PERSON` 表中选择行。这是必要的，因为 `PERSON_V` 视图有一个子视图（`EMP_V`），且 `PERSON_V` 视图不应包含分配给 `EMP_V` 视图的行。记住，在同一个层次结构中不允许存在重复的 `OID` 值。

即使使用 `FROM PERSON` 代替 `FROM ONLY(PERSON)`，第一个 `CREATE VIEW` 语句也会执行；但在创建 `EMP_V` 视图时，你会得到错误，因为所有符合 `EMP_V` 定义全选的行都被 `PERSON_V` 视图引用。你不需要为 `EMP_V` 视图使用 `ONLY` 子句，因为 `EMP_V` 视图没有任何子视图。
