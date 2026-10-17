
1. 声明了一个具有两列的位置迭代器。注意，该列没有名称，只有数据类型。这就是为什么它是一个位置迭代器的原因。

2. 声明了一个变量 `status`。这类似于一个主机变量，用于接收来自迭代器的值。

3. 类似于变量 `poid` 的操作 (2)。

4. 创建了位置迭代器 `iterator1`。

5. 在连接上下文 `ctx1` 中，使用 `select poid, status from purchaseorder` 定义了 `iterator1`。

6. 在开始循环之前，我们将第一条记录获取到主机变量 `poid` 和 `status` 中。这是因为在 (7) 中，我们没有使用 `next()`，而是使用了 `endFetch()`，因此如果你使用 `next()` 与 `endFetch()`，while 循环的条件结束方式会有所不同。

7. 遍历迭代器。

8. 打印每一行检索到的 `poid` 和 `status`。

9. 获取迭代器中的下一条记录。

命名迭代器或位置迭代器可以是可更新的和可滚动的。默认情况下，SQLJ 中的迭代器是只读的，并且只能向前移动。要定义一个可滚动的迭代器，你需要在定义迭代器时实现 `sqlj.runtime.Scrollable`。

要定义一个可更新的光标，你需要在定义迭代器时实现 `sqlj.runtime.ForUpdate`。在定义可更新的迭代器时，你还必须指定想要更新的列。

这与 JDBC 类似。列表 4.24 提供了一个可更新迭代器的示例。

(1)

```
#sql public iterator namediterator implements sqlj.runtime.ForUpdate
with (updateColumns="STATUS") (int poid, String status);
```

(2)

```
namediterator iterator1;
```

(3)

```
#sql {ctx1 { iterator1 = { select poid, status from purchaseorder };
```

(4)

```
while (iterator1.next()) {
```

(5)

```
System.out.println("before update poid: " + iterator1.poid() +
" Status: " + iterator1.status());
```

(6)

```
if (iterator1.status().toUpperCase().compareTo("UNSHIPPED") == 0) {
#sql {ctx1 { update purchaseorder set status =
'shipped' where current of : iterator1 };
}
```

(7)

```
#sql {ctx1 { commit; }
```

#### 列表 4.24 - 一个可更新迭代器的示例

在上述列表中：

1. 声明了一个命名迭代器，由于它实现了 `sqlj.runtime.ForUpdate`，因此被定义为可更新迭代器，并注意它还通过 `with (updateColumns="STATUS")` 指示它将更新哪个列。

2. 声明了命名迭代器 `iterator1`。

3. `iterator1` 被定义为 `select poid, status from purchaseorder` 的结果。

4. 遍历迭代器。

5. 打印迭代器的每一行。

6. 测试 `status` 列的值是否为 "UNSHIPPED"。如果是，则将该值更改为 'shipped'。

7. 提交更改。

### 4.4.5 结合使用 JDBC 和 SQLJ

JDBC 和 SQLJ 可以在单个应用程序中结合使用。例如，可以使用 `ConnectionContext` 对象的 `getConnection` 方法从该对象中检索 JDBC 连接对象，反之亦然。

SQLJ 中的迭代器和 JDBC `ResultSet` 可以相互检索，如下所示：

- 从结果集到迭代器：`#sql iterator = {CAST :result-set }`
- 从迭代器到结果集：使用迭代器的 `getResultSet` 方法。

*列表 4.25* 提供了在一个程序中结合使用 JDBC 和 SQLJ 的示例。

```java
#sql public iterator positionIterator (int, String);
Class.forName("com.ibm.db2.jcc.DB2Driver").newInstance();
Connection con=DriverManager.getConnection(url);
con.setAutoCommit(false);
(1) ctx ctx1=new ctx(con);
positionIterator iterator;
Statement stmt = con.createStatement();
ResultSet rs=stmt.executeQuery("select poid, status from purchaseorder");
(2) #sql [ctx1] iterator={cast :rs};
#sql {fetch :iterator into :poid, :status};
while(!iterator.endFetch()) {
System.out.println("id: "+poid+" status: "+status);
#sql {fetch :iterator into :poid, :status};
}
    iterator.close();
```

**列表 4.25 - 在一个程序中结合使用 JDBC 和 SQLJ**

在上述列表中：

1. 使用连接对象创建 SQLJ 连接上下文。

2. 这展示了如何从 JDBC 结果集中获取结果来创建 SQLJ 迭代器。

### 4.4.6 准备 SQLJ 程序

准备 SQLJ 程序类似于嵌入式 SQL 程序的过程，在那里你必须预编译和绑定程序。在这种情况下，SQLJ 程序需要被转换和定制。*图 4.11* 展示了准备程序 `myprg3.sqlj` 的过程。

![](img/5f6ba170efa3a607142589708531bef8_155_0.png)

**图 4.11 - 准备 SQLJ 程序的步骤**

在该图中，SQLJ 程序 `myprg3.sqlj` 使用 `sqlj` 命令通过 *SQLJ 转换器* 进行处理。SQLJ 转换器检查文件，查找以 "#sql" 开头的行，并将这些行替换为包含 SQLJ 运行时类的生成代码，创建一个带有 `.java` 扩展名的文件。然后它使用 Java 编译器 (`javac`) 编译此文件，创建一个 `.class` 文件。这在该图的底部显示，其中创建了 `myprg3.java` 和 `myprg3.class` 文件。

SQLJ 转换器还会创建，如该图顶部所示，为在 SQLJ 可执行子句中使用的每个连接上下文类创建序列化配置文件。在此示例中，它显示了两个序列化配置文件 `myprg3_SJProfile0.ser` 和 `myprg3_SJProfile1.ser`。这些文件保存关于嵌入式 SQL 的信息。在这些文件之后，调用 `javac` 时会创建一个 `myprg3_SJProfileKeys.class` 文件（图中未显示）。使用带有 `db2sqljcustomize` 命令的 DB2 定制器，在数据库中创建一个包（已编译的 SQL）。

当你想要执行程序时，只需使用命令 `java myprg3` 运行它，这将使用 `myprg3.class` 文件和数据库中的相应包。

> **注意：**
>
> 程序 `myprg3.sqlj` 包含在随本书提供的 zip 文件 `Exercise_Files_DB2_Application_Development.zip` 中。你可以查看、测试和准备此文件。

以下是实际执行所有这些命令及其相应输出的示例。这些是要遵循的步骤：

(1) 运行 SQLJ 转换器（`sqlj` 命令）

```
D:\>sqlj myprg3.sqlj
```

创建了以下文件：

```
myprg3.java, myprg3.class,
myprg3_SJProfile0.ser,
myprg3_SJProfileKeys.class
```

(2) 为每个 `.ser` 文件运行 DB2 定制器（`db2sqljcustomize` 命令）。DB2 定制器可以接受几个参数。它基本上是一个需要连接到数据库的 Java 程序，因为它是存储包的地方。例如：

```
D:\>db2sqljcustomize -url jdbc:db2://localhost:50000/sample -user rfchong -password mypasswd myprg3_SJProfile0.ser
```

其中：
