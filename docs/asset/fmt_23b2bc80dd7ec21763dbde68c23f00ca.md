
```sql
SELECT custid, lastName FROM tblCustomer WHERE state = "WI"
```

将显示一个包含两列（`custid` 和 `lastName`）的新表，其行数恰好容纳那些 `state` 列包含 `"WI"` 的客户。除了使用 `=` 表示“等于”外，你还可以使用比较运算符 `>`（大于）、`>=`（大于或等于）和 `<=`（小于或等于）。正如你已经在书中通过编程变量中学过的那样，字段值始终包含在引号中，而数值值则不然。

> 提示 习惯上，SQL 关键字（如 `SELECT`）全全大写；本书遵循这一习惯。

要选择记录中的所有字段，请使用星号 `*` 作为通配符；通配符是表示“任何”或“所有”的符号。例如，`SELECT * from tblCustomer WHERE state = "WI"` 将为每个 `state` 为 `"WI"` 的客户选择所有列，而不仅仅是命名的列。要从表中选择所有客户，请在 `SELECT-WHERE` 语句中省略 `WHERE` 子句。换句话说，`SELECT * FROM tblCustomer` 选择所有客户的列。

你在本书中更早的时候就学习了在计算机中进行选择，你可能已经注意到 `SELECT-FROM-WHERE` 语句与编程决策具有相同目的。与程序中的决策语句一样，在使用 SQL 时，你可以在任何代码前加上 `NOT` 操作符以获得否定结果。图 16-4 显示了一个名为 `tblInventory` 的表，其结构如下：`tblInventory(itemNumber, description, quantityStock, price)`。该表包含五条记录。图 16-5 列出了你可能配合 `tblInventory` 使用的几个典型 SQL `SELECT` 语句，并解释了每一个。

| itemNumber | description | quantityStock | price |
|---|---|---|---|
| 144 | Pkg 12 party plates | 250 | 14.99 |
| 231 | Helium balloons | 180 | 2.50 |
| 267 | Paper streamers | 68 | 1.89 |
| 312 | Disposable tablecloth | 20 | 6.99 |
| 383 | Pkg 20 napkins | 315 | 2.39 |

### 图 1b-5: 示例 SQL 语句及解释

| SQL 语句 | 解释 |
|---|---|
| `SELECT custid, lastName FROM tblCustomer` | 从 `tblCustomer` 中选择 `custid` 和 `lastName` |
| `SELECT * FROM tblCustomer WHERE state = "WI"` | 从 `tblCustomer` 中选择 `state` 为 `"WI"` 的所有列 |
| `SELECT itemNumber FROM tblInventory WHERE quantityStock < 50` | 从 `tblInventory` 中选择 `quantityStock` 小于 50 的 `itemNumber` |
| `SELECT * FROM tblInventory WHERE price > 10` | 从 `tblInventory` 中选择 `price` 大于 10 的所有列 |
| `SELECT SUM(quantityStock) FROM tblInventory` | 计算 `tblInventory` 中 `quantityStock` 的总和 |
| `SELECT COUNT(*) FROM tblInventory` | 计算 `tblInventory` 中的记录总数 |

# 关系（RELATIONIPS）

关系（`relationships`）是指数据表之间的关联方式。在关系型数据库中，数据存储在多个表中，这些表通过某些字段（如主键（`primary key`）和外键（`foreign key`））连接起来。关系通常有三种：

- 一一对多（`one-to-many`）
- 多对一（`many-to-one`）
- 多对多（`many-to-many`）

## 理解多对多关系

下面的表展示了另一个一对多的关系示例：

```
tblItems(itemNumber, itemName, itemPurchasedDate,
itemPurchasePrice, itemCategoryId)
tblCategories(categoryId, categoryName,
categoryInsuredAmount)
```
