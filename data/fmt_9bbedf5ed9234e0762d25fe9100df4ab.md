
编程接口遵循上一节关于数据库 API 描述的约定，因此许多细节在此不再重复。相反，本节侧重于该模块的技术细节，以及 `sqlite3` 模块特定的特性。

## 模块级函数

由 `sqlite3` 模块定义的函数：

```
connect(database [, timeout [, isolation_level [, detect_types]])
```

创建一个到 SQLite 数据库的连接。`database` 是指定数据库文件名的字符串。它也可以是字符串 `"memory:"`，在这种情况下将使用内存数据库（注意，这种数据库仅在 Python 运行期间持续，并在退出时丢失）。`timeout` 参数指定了当其他连接正在更新数据库时，等待读写锁释放的时间长度。默认情况下，`timeout` 为 5 秒。当使用如 `INSERT` 或 `UPDATE` 等 SQL 语句时，如果当前没有这些事务，则会自动启动一个新事务。`isolation_level` 参数是一个字符串，为启动此事务的底层 SQL `BEGIN` 语句提供可选的修饰符。可能的值有 `""`（默认值）、`"DEFERRED"`、`"EXCLUSIVE"` 或 `"IMMEDIATE"`。这些设置的含义与底层数据库锁的关系如下：

| 隔离级别 | 说明 |
|---|---|
| `""` (空字符串) | 使用默认的 (DEFERRED)。 |
| `"DEFERRED"` | 启动新事务，但在实际执行第一次数据库操作之前不获取锁。 |
| `"EXCLUSIVE"` | 启动新事务并保证在更改提交之前，没有其他连接可以读取或写入数据库。 |
| `"IMMEDIATE"` | 启动新事务并保证在更改提交之前，没有其他连接可以对数据库进行修改。但其他连接仍然可以读取数据库。 |

```
register_converter(typename, func)
```

注册一个新类型名称，用于 `connect()` 函数中的 `detect_types` 选项。`typename` 是包含查询中将使用的类型名称的字符串，`func` 是一个接受单个字节字符串（byestring）并返回 Python 数据类型的函数。

例如，如果你调用 `sqlite3.register_converter('decimal', decimal.Decimal)`，那么你就可以编写如 `'select price as "price [decimal]" from stocks'` 这样的查询将值转换为 `Decimal` 对象。

```
register_adapter(type, func)
```

为 Python 类型注册一个适配器函数，用于在你定义了存储该类型的值时。`func` 是一个接受该类型实例作为输入并返回 `int`、`float`、UTF-8 编码的字节字符串、Unicode 字符串或缓冲区作为结果的函数。例如，如果你想存储 `Decimal` 对象，你可以使用 `sqlite3.register_adapter(decimal.Decimal, float)`。

```
complete_statement(s)
```

返回字符串 `s` 代表一个或多个由分号分隔的 SQL 语句。这对于编写从用户处读取查询的交互式程序可能有用。

```
enable_callback_tracebacks(flag)
```

确定用户定义的作为转换器和适配器的回调函数中异常的处理方式。默认情况下

## 连接对象

由 `connect()` 函数返回连接对象 `c` 支持 Database API 中描述的标准操作。此外，还提供了以下 `sqlite3` 模块特定的方法：

```
create_function(name, num_params, func)
```

创建一个可以在 SQL 语句中使用的自定义函数。`name` 是包含函数名的字符串，`num_params` 是给出参数数量的整数，`func` 是提供实现的 Python 函数。尽管定义了 Python 函数，参数的类型应该是 `int`、`float`、`str`、`buffer` 或 `None`。

```python
def toupper(s):
    return s.upper()
create_function("toupper", 1, toupper)
# 查询示例用法
cur.execute("select toupper(name),foo from some_table")
```

```
create_aggregate(name, num_params, aggregate_class)
```

创建一个可以在 SQL 语句中使用的自定义聚合函数。`name` 是包含函数名的字符串，`num_params` 是给出参数数量的整数。`aggregate_class` 是实现聚合的类。该类必须支持无参数的初始化、一个接受与 `num_params` 相同数量参数的 `step(params)` 方法以及一个返回结果的 `finalize()` 方法。这是一个简单的示例：

```python
class Averager(object):
    def __init__(self):
        self.total = 0.0
        self.count = 0

    def step(self, value):
        self.total += value
        self.count += 1

    def finalize(self):
        return self.total / self.count

c.create_aggregate("myavg", 1, Averager)
# 查询示例用法
c.execute("select myavg(num) from sometable")
```

聚合通过重复调用带有输入的 `step()` 方法然后调用 `finalize()` 来获得最终值。

```
create_collation(name, func)
```

注册一个用于 SQL 语句的自定义排序函数。`name` 是包含排序函数名的字符串，`func` 接受两个输入并根据第一个输入是否小于、等于第二个输入返回 -1、0 或 1。使用如 `"select * from table collate colname"` 的 SQL 表达式使用自定义函数。

```
c.execute(sql [, params])
```

快捷方法，通过 `c.cursor()` 创建游标对象并执行带有 `params` 参数的 `sql` 语句的游标 `execute()` 方法。

```
c.executemany(sql [, params])
```

快捷方法，通过 `c.cursor()` 创建游标对象并执行带有 `params` 参数的 `sql` 语句的游标 `executemany()` 方法。

```
c.execscript(sql)
```

快捷方法，通过 `c.cursor()` 创建游标对象并执行带有 `sql` 语句的游标 `execscript()` 方法。

```
c.interrupt()
```

中止连接上任何执行中的查询。旨在从单独线程调用。

```
c.iterdump()
```

返回一个迭代器，将整个数据库导出为一系列可以重建数据库的 SQL 语句。

```
c.set_authorizer(callback)
```

注册一个在每次访问列时执行的授权回调。回调函数必须接受五个参数 `callback(code, arg1, arg2, dbname, innername)`。第一个参数 `code` 是一个整数。`dbname` 是包含数据库名的字符串（通常为 `"main"`），`innername` 是尝试访问的视图或触发器的名称。如果允许 `SQLITE_OK`，则回调返回 0；如果 SQL 语句应该失败，返回 `SQLITE_DENY`；如果列应该被视为 Null 而忽略，返回 `SQLITE_IGNORE`。下表列出了 `code` 的值以及 `arg1`, `arg2` 参数的含义：

| Code | Arg1 | Arg2 |
|---|---|---|
| `SQLITE_CREATE_INDEX` | 索引名 | 表名 |
| `SQLITE_CREATE_TABLE` | 表名 | None |
| `SQLITE_CREATE_TEMP_INDEX` | 索引名 | 表名 |
| `SQLITE_CREATE_TEMP_TABLE` | 表名 | None |
| `SQLITE_CREATE_TEMP_TRIGGER` | 触发器名 | 表名 |
| `SQLITE_CREATE_VIEW` | 视图名 | None |
| `SQLITE_CREATE_TRIGGER` | 触发器名 | 表名 |
| `SQLITE_CREATE_VIEW` | 视图名 | None |
| `SQLITE_DELETE` | 表名 | None |
| `SQLITE_DROP_INDEX` | 索引名 | 表名 |
