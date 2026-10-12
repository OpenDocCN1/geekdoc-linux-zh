
| `SQLITE_DROP_TABLE` | 表名 | None |
| `SQLITE_DROP_TEMP_INDEX` | 索引名 | 表名 |
| `SQLITE_DROP_TEMP_TABLE` | 表名 | None |
| `SQLITE_DROP_TEMP_TRIGGER` | 触发器名 | 表名 |
| `SQLITE_DROP_TEMP_VIEW` | 视图名 | None |
| `SQLITE_DROP_TRIGGER` | 触发器名 | 表名 |
| `SQLITE_DROP_VIEW` | 视图名 | None |
| `SQLITE_INSERT` | 表名 | None |
| `SQLITE_PRAGMA` | Pragma 名 | None |
| `SQLITE_READ` | 表名 | 列名 |
| `SQLITE_SELECT` | None | None |
| `SQLITE_TRANSACTION` | None | None |
| `SQLITE_UPDATE` | 表名 | 列名 |
| `SQLITE_ATTACH` | 文件名 | None |
| `SQLITE_DETACH` | 数据库名 | None |
| `SQLITE_ALTER_TABLE` | 数据库名 | 表名 |
| `SQLITE_REINDEX` | 索引名 | None |
| `SQLITE_ANALYZE` | 表名 | None |
| `SQLITE_CREATE_VTABLE` | 表名 | 模块名 |
| `SQLITE_DROP_VTABLE` | 表名 | 模块名 |
| `SQLITE_FUNCTION` | 函数名 | None |

```
c_set_progress_handler(handler, n)
```

注册一个在 SQLite 虚拟机每执行 `n` 条指令时执行一次的回调函数。`handler` 是一个不接受参数的函数。

# 308 第 17 章 Python 数据库访问

连接对象上还了以下属性。

`c.row_factory`

这是一个调用的函数，用于创建表示每个结果行内容的对象。该函数接受两个参数：用于获取结果游标对象以及一个包含原始行结果的元组。

`c.text_factory`

这是一个调用的函数，用于创建表示数据库中文本值的对象。该函数必须接受一个参数，即 UTF-8 编码的字符串。返回值应该是某种字符串。默认情况下，返回一个 Unicode 字符串。

`c.total_changes`

一个整数，表示自数据库连接打开以来已修改的行数。

连接对象的最后一个特性是它们可以与上下文管理器配合使用，自动处理事务。例如：

```python
conn = sqlite3.connect("somedb")
conn.execute("insert into table values (?,?)", ("foo", "bar"))
```

在这个示例中，with 块中的所有语句执行完毕且没有发生错误后，会自动执行 `commit()` 操作。如果抛出任何异常，将执行 `rollback()` 操作并重新抛出该异常。

# 游标与基本操作

要对 sqlite3 数据库进行操作，你必须使用连接的 `cursor()` 方法创建一个游标对象。然后你使用 `execute()`、`executemany()` 或 `executescript()` 方法来执行 SQL 语句。关于这些方法的通用操作的更多细节，请参见数据库 API 章节。这里不再重复信息，而是通过示例代码展示了一组常见的数据库用例。其目的是为可能需要简要复习语法的程序员展示游标对象的操作以及一些 SQL 操作。

## 创建新数据库表

以下代码展示了如何打开数据库并创建一个新表：

```python
import sqlite3
conn = sqlite3.connect("mydb")
cur = conn.cursor()
cur.execute("create table stocks (symbol text, shares integer, price real)")
conn.commit()
```

在定义表时，应该使用几种原始 SQLite 数据类型：`text`、`integer`、`real` 和 `blob`。`blob` 类型是字节字符串，而 `text` 类型被假设为 UTF-8 编码的 Unicode。

## 向表中插入新值

以下代码展示了如何向向表中插入新条目：

```python
import sqlite3
conn = sqlite3.connect("mydb")
cur = conn.cursor()
cur.execute("insert into stocks values (?,?,?)", ('IBM',50,91.10))
cur.execute("insert into stocks values (?,?,?)", ('AAPL',100,123.45))
conn.commit()
```

在插入值时，你应该始终使用所示的 `?` 替换符。每个 `?` 都会由提供的参数值元组中的值进行替换。

如果你有一个序列要插入数据，可以这样使用游标的 `executemany()` 方法：

```python
stocks = [('GOOG',75,380.13), ('AA',60,14.20), ('AIG',125,0.99)]
cur.executemany("insert into stocks values (?,?,?)",stocks)
```

## 更新现有行

以下代码展示了你如何更新现有行中的列：

```python
cur.execute("update stocks set shares=? where symbol=?", (50, 'IBM'))
```

再次，当你需要向 SQL 语句中插入值时，请确保使用占位符和值元组作为参数。

## 删除行

以下代码展示了如何删除行：

```python
cur.execute("delete from stocks where symbol=?", ('SCOX'))
```

## 执行基本查询

以下代码展示了你如何执行基本查询并获取结果：

```python
# 从表中选择所有列
for row in cur.execute("select * from stocks"):
    print row
```

```python
# 选择少数几列
for shares, price in cur.execute("select shares,price from stocks"):
    print shares, price
```

```python
# 选择匹配的行
for row in cur.execute("select * from stocks where symbol=?", ('IBM')):
    print row
```

```python
# 带排序的匹配行
for row in cur.execute("select * from stocks order by shares"):
    print row
```

```python
# 带反排序的匹配行
for row in cur.execute("select * from stocks order by shares desc"):
    print row
```

```python
# 通过共同列名 (symbol) 连接表
for row in cur.execute("select s.symbol, s.shares, p.price from stocks s, prices p using(s.symbol=p.symbol)"):
    print row
```

# DBM 风格数据库模块

Python 包含了许多支持 UNIX DBM 风格数据库的库模块。支持这些数据库的几种标准类型。`dbm` 模块用于读取标准的 UNIX-dbm 数据库。`gbm` 模块用于读取 GNU dbm 文件（http://www.gnu.org/software/gdb）。`dbhash` 模块用于从 Berkeley DB 库读取数据库文件（http://www.oracle.com/database/berley-db/index.html）。`dbm` 模块是一个纯 Python 模块，它独立实现单一 DBM 风格的数据库。

所有这些模块都提供一个实现了持久化字符串字典的对象。也就是说，它的工作方式类似于 Python 字典，但要求所有键和值都限制为字符串。数据库文件通常使用 `open()` 函数的变体打开。

```python
open(filename, flag, [mode])
```

此函数打开数据库 `filename` 并返回一个数据库对象。`flag` 为 'r' 表示只读，'c' 表示如果数据库不存在则创建，'n' 表示强制创建新数据库。`mode` 是创建数据库时使用的整数（在 Unix 上默认为 0666）。

`open()` 函数返回的对象至少支持以下字典操作：

| 操作 | 描述 |
|---|---|
| `d[key] = value` | 将值插入数据库 |
