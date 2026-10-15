
```
INSERT INTO hr.employees VALUES(3, 'Paul', 'Smith', 'M',
DEFAULT, 'C03', '919-555-5656', '33-44-5555',
39250.00, 3500.00);
```

一旦授予了此豁免以及适当的安全标签，用户 `HR_STAFF` 将能够执行之前显示的 `ALTER TABLE` 语句而不会产生错误。（或者，可以使用 `CREATE TABLE` 语句创建 `EMPLOYEES` 表并用适当的安全标签保护每一列，前提是用户 `HR_STAFF` 拥有创建所需的所需的。）

用户 `HR_STAFF` 拥有所有列的读写访问权限（带有 `DB2LBACWRITEARRAY WRITEDOWN` 豁免），因此这些语句执行成功。如果用户 `HR_STAFF` 尝试查询表，他将能够看到所有列，因为他授予了数组中的最高安全级别。

现在，当 `MANAGER1` 尝试读取表中的每一列时，将产生错误，说明他没有对 `SSN` 列的“读”（READ）权限。然而，`MANAGER1` 能够执行以下指定的列查询：

# 第8章：安全

```
SELECT f_name, l_name, hire_date, salary, bonus
FROM hr.employees
```

现在，如果 `EMPLOYEE1` 尝试执行相同的查询，将产生错误，说明她没有对 `BONUS` 列的“读”（READ）权限。但 `EMPLOYEE1` 尝试执行以下查询将成功：

```
SELECT f_name, l_name, gender, dept_id, phone
FROM hr.employees
```

此外，如果 `MANAGER1` 或 `EMPLOYEE1` 尝试插入额外的记录或更新现有信息，他们将得到错误，说明没有权限对表执行该操作。

## 结合行级和列级 LBAC

有时你希望限制单个用户对特定行列组合的访问。在这种情况下，你必须在表定义中包含一个数据类型为 `DB2LABEL` 的列，在表的每一列中添加 `SECURED WITH [SecurityLabel]` 选项，并使用 `CREATE TABLE` 语句的 `SECURITY POLICY` 子句或 `ALTER TABLE` 语句的 `ADD SECURITY POLICY` 子句与表关联。通常，你还会创建两个安全标签组件——一个用于行，一个用于列——并使用这两个组件构建构建的安全策略。

例如，假设你通过执行以下命令创建了两个安全标签组件：

```
CREATE SECURITY LABEL COMPONENT som_level
ARRAY ['CONFIDENTIAL', 'CLASSIFIED', 'UNCLASSIFIED'];
```

```
CREATE SECURITY LABEL COMPONENT som_country
TREE ('NA' ROOT, 'CANADA' UNDER 'NA', 'USA' UNDER 'NA');
```

你将通过执行类似下面的 `CREATE SECURITY POLICY` 命令来创建一个安全策略：

```
CREATE SECURITY POLICY sec_policy sec_policy
COMPONENTS som_level, som_country
WITH DB2LBACRULES
```

在与各个列关联了适当的安全标签后，你将为每个用户授予正确的安全标签并进行几次测试以确保数据访问符合预期。

### 问题 4

用户 `USER1` 需要从 `SALES` 数据库中删除名为 `ORDERS_V` 的视图，该视图基于名为 `ORDERS` 的表。假设用户 `USER1` 不拥有任何权限，在允许用户 `USER1` 删除该视图之前，必须授予以下哪些权限？

A. 对 `ORDERS_V` 视图的 `DROP` 权限

B. 对 `ORDERS` 表的 `CONTROL` 权限

C. 对 `ORDERS_V` 视图的 `DROP` 权限

D. 对 `ORDERS_V` 视图的 `CONTROL` 权限

### 问题 5

下列哪项标识了实例如何执行身份验证？

A. 实例使用的操作系统

B. 实例使用的通信配置

C. `DB2` 注册表

D. `DB2` 数据库管理器配置

### 问题 6

在执行以下 SQL 语句后：

```
GRANT ALL PRIVILEGES ON TABLE employee TO USER user1
```

假设用户 `USER1` 没有其他权限或特权，`USER1` 被允许执行以下哪些操作？

A. 掉 `EMPLOYEE` 表上的索引。

B. 将 `EMPLOYEE` 表上的所有权限授予其他用户。

C. 修改表定义。

D. 删除 `EMPLOYEE` 表。

### 问题 7

名为 `USER1` 的用户被授予了 `DBADM` 权限。假设没有授予其他权限/特权，且已从 `PUBLIC` 组撤销了所有权限，如果执行以下 SQL 语句：

```
REVOKE DBADM ON DATABASE FROM user1
```

用户 `user1` 将拥有哪些权限/特权？

nA. 无

B. `CONNECT`

C. `SYSCTRL`

D. `EXECUTE`

### 问题 8

用户 `USER1` 想要调用一个动态从表中表中检索数据的 SQL 存储过程。为了调用该存储过程，用户 `USER1` 必须具备哪两个权限？

A. 对存储过程的 `EXECUTE` 权限。

B. 对存储过程的 `CALL` 权限。

C. 对存储过程检索数据所在表的 `SELECT` 权限。

D. 对存储过程的包的 `EXECUTE` 权限。

E. 对存储过程的 `SELECT` 权限。

## 问题 9

下列哪些权限允许用户删除已为表定义的外键？

A. 对表的 `ALTER` 权限。

B. 对表的 `DELETE` 权限。

C. 对表的 `DROP` 权限。

D. 对表的 `UPDATE` 权限。

## 问题 10

下列哪些权限允许用户为嵌入式 SQL 程序生成包并将其存储在数据库中？

- A. `BIND`
- B. `BINDADD`
- C. `CREATE_EXTERNAL_ROUTINE`
- D. `CREATE_NOT_FENCED_ROUTINE`

## 问题 11

关于 `DB2` 安全，以下哪种说法是不正确的？

- A. 如果使用 Microsoft Active Directory 验证用户，则必须创建一个自定义的安全插件。
- B. 只有具有 Security Administrator（安全管理员）权限的用户才允许授予和撤销 `SETSESSIONUSER` 权限。
- C. 用户和组在授予权限之前必须存在。
- D. 如果持有表 `SELECT` 权限的用户创建了基于该表的视图，随后其 `SELECT` 权限被撤销，则该视图将保持可运行。

## 问题 12

`USER1` 拥有调用名为 `GEN_RESUME` 的存储过程所需的权限。`USER2` 需要能够调用该过程——而 `USER1` 以及 `PUBLIC` 组的所有成员不应再被允许调用该过程。下列哪些语句可以实现这一目标？

- A. `GRANT EXECUTE ON ROUTINE gen_resume TO user2 EXCLUDE user1, PUBLIC`
- B. `GRANT EXECUTE ON PROCEDURE gen_resume TO user2; REVOKE EXECUTE ON PROCEDURE gen_resume FROM user1, PUBLIC;`
- C. `GRANT CALL ON ROUTINE gen_resume TO user2 EXCLUDE user1, PUBLIC`
- D. `GRANT CALL ON PROCEDURE gen_resume TO user2; REVOKE CALL ON PROCEDURE gen_resume FROM user1, PUBLIC;`

## 问题 13

下列哪项未用于限制对基于标签的访问控制 (`LBAC`) 保护的表中单行的访问？

- A. 一个或多个安全配置文件
- B. 安全策略
- C. 一个或多个安全标签
- D. `DB2SECSECURITYLABEL` 列

## 问题 14

关于基于标签的访问控制 (`LBAC`)，以下哪种说法是不正确的？

- A. `LBAC` 可用于限制对单独行和列的访问。
- B. 被授予不同 `LBAC` 安全标签的用户执行相同查询时将获得不同的结果。
- C. 只有具有 `SYSADM` 或 `SECADM` 权限的用户允许创建安全策略和安全标签。
- D. 安全标签组件代表用于判断用户是否应该访问特定数据的标准。

## 问题 15

以下哪个 SQL 语句允许名为 `USER1` 的用户写入 `LBAC` 保护的列，而这些列所保护的 `LBAC` 标签的安全级别低于 `USER1` 所拥有的 own？

- A. `GRANT EXEMPTION ON RULE DB2LBACWRITEARRAY WRITEDOWN FOR sec_policy TO user1`
- B. `GRANT EXEMPTION ON RULE DB2LBACWRITEARRAY WRITEDOWN FOR sec_policy TO user1`
