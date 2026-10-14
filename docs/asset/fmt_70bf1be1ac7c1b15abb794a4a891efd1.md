
为了示例演示，输入图 12-2 所示的信息。

由于在此示例中数据库和 Zope 服务器都在同一台电脑上，我们省略了 `[Host]` 参数。请替换适用于你的数据库服务器的用户名和密码。

恭喜你！你刚刚建立了 Zope 与你的 MySQL 数据库之间的连接，你现在可以从 Zope 内部访问你的 MySQL 数据。

添加 Z MySQL 数据库连接

| Id | `MySQL_database_connection` |
| :--- | :--- |
| Title | MySQL Database Connection |
| 输入 Database Connection String 1 | |
| 立即连接 | Add |

图 12-1：创建 Z MySQL 连接

输入连接字符串 `myDB`

图 12-2：连接字符串

### 12.3.5.2 检查数据库连接

要检查数据库连接状态，点击 `MySQL_database_connection`。你应该看到类似图 12-3 所示的界面。要随时关闭连接，点击 Close Connection；重新打开，点击 Open Connection。在 Properties（属性）选项卡上，你可以更改数据库的 Title 和 Connection String 参数。

| Status | Properties | Text | Browse |
| :--- | :--- | :--- | :--- |
| MySQL Database Connection of: `/MySQL_database_connection` | | | |
| `database_connection` is open | | | |

图 12-3：状态界面

## 12.3.6 向数据库测试 SQL 查询

要测试你的数据库，编写一个查询以确定 `user` 表中哪些记录。为此，向数据库发送以下 SQL 语句：

```sql
select * from user
```

当你点击 Test 标签时，你应该看到类似图 12-4 所示的界面。在 Query 字段中输入以下 SQL（如图 12-4 所示）：

```sql
select * from user
```

使用此界面，你可以从 Zope 内部向 MySQL 数据库提交 SQL 语句，而无需切换到 MySQL Monitor。

![](img/4328ce54752f48bf4536fb6.png) 你可以在 Query 字段中编写各种 SQL 语句来查询数据库、创建新表或输入新数据。现在数据库已连接到 Zope，你可以通过在 Query 字段中输入 12.3.3 节在 MySQL Monitor 中创建的表。

## 12.4 填充表

在向 `user` 表填充数据之前，你必须在 Zope 中创建表 12-2 中列出的对象。

表 12-2：创建用户的对象

| 对象名称 | 功能 |
| :--- | :--- |
| `userAddForm_html` | 用户数据的输入表单。 |
| `userAdd_html` | 将值传递给 SQL 方法 `userInsert_sql` 并向用户报告结果。 |
| `userInsert_sql` | 在数据库中写入值的 SQL 方法。 |

前面提到的你可以在 Query 字段中编写 SQL 查询来填充 `user` 表。如果你希望没有 Zope 管理界面的用户也能访问并使用数据库，你必须为 `name`、`city`、`address` 等字段创建单独的输入表单。

### 12.4.1 addUserForm_html 方法

使用 Listing 12-1 中的代码创建输入表 `addUserForm.html`。

Listing 12-1：`addUserForm.html`

正如 Listing 12-1 开头所示，当提交此表单时，会调用 DTML 方法 `addUser_html`。`addUser_html` 方法将执行插入新记录的 SQL 查询。变量 `userid`（第三行）接收的值是从当前系统时间生成的字符串。这确保了 `userid` 是唯一的（作为 `user` 表的主键，因为系统时间绝不会重复）。你现在需要创建一个名为 `userAdd_html` 的 DTML 方法，它将值传递给 SQL 方法 `insert_sql` 并通知你已在 `user` 数据库中成功。由于此 DTML 方法无法向数据库写入数据，你将创建一个写入输入值的 SQL 方法（见 12.4.3 节）。

### 12.4.2 userAdd_html 方法

输入 Listing 12-2 所示的代码创建 DTML 方法 `userAdd_html`。

#### Listing 12-2：`userAdd_html`

```html
1: <dt-var standard_html_header>
2: <dt-if name="Create">
3: <dt-try>
4: <dt-call name="userInsert_sql">
5: 用户 <dt-var name="firstname">
6: <dt-var name="lastname">
7: 已成功添加到数据库中。
8: <dt-except>
9: 抱歉，用户未添加到数据库，
10: 因为发生了错误。
11: </dt-try>
12: <center>
13: <form action="<dt-var name="URL1">
14: <input type="submit" name="userAdd_html:method"
15: value="创建另一个用户">
16: <input type="submit" name="index_html:method" value="完成">
17: </form>
18: </center>
19: <dt-else>
20: <dt-call expr="RESPONSE.redirect('index_html')">
21: </dt-if>
22: <dt-var standard_html_footer>
```

让我们仔细观察这段代码在提交 `userAdd_Form` 时是如何工作的。

首先，查看 Create 按钮是否使用了 `dtml-if`（第 2 行）。如果是，打开一个 `dtml-try` 块（第 3 行），在其中调用 SQL 方法 `insert_sql`（第 4 行）；因为此 SQL 方法不返回结果，该方法通过 `dtml-call` 成功执行。

## 12.4.3 insert_sql 方法

现在你将创建一个名为 `userInsert_sql` 的 Z SQL 方法。

只有在数据库连接处于激活状态时，你才能创建 SQL 方法。

- 1. 从文件夹的添加菜单中，选择 Z SQL Method。出现如图 12-5 所示的管理界面。

![](img/43a28cce5475b2f487bf455365567fb6_256_0.png)

图 12-5：创建一个 SQL 插入方法

- 2. 对于 `id`、`editor`，选择 `MySQL_database_connection`。
- 3. 在 Connection Id 字段中，输入所有要传递给此 SQL 方法的值，如下所示（请确保每个单独参数之间留有一个空格）：
- 4. 在 Arguments 字段中，输入 `userid firstname lastname address zipcode city telephone`
- 5. 在 Query 字段中，输入以下 SQL 语句：

```sql
INSERT INTO user
(userid,firstname,lastname,address,zipcode,city,telephone)
VALUES
  ('<dml-var name="userid" sql_quote',
  '<dml-var name="firstname" sql_quote',
  '<dml-var name="lastname" sql_quote',
  '<dml-var name="address" sql_quote',
  '<dml-var name="zipcode" sql_quote',
  '<dml-var name="city" sql_quote',
  '<dml-var name="telephone" sql_quote'>)
```
