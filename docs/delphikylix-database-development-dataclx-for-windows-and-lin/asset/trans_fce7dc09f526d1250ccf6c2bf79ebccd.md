
## 创建数据库

无法使用 ExecuteDirect 创建新的 InterBase 数据库。以下代码行不起作用：

```
SQLConnection1.ExecuteDirect('CREATE DATABASE '''C:\NewData.gdb''');
```

如果尝试执行此代码，你将收到以下异常：

```
Cannot prepare a CREATE DATABASE/SCHEMA statement.
```

InterBase 客户端不允许直接执行 DDL 或 DML，因此 dbExpress 驱动程序会尝试准备，然后执行 CREATE DATABASE 语句。由于 InterBase 不允许准备 CREATE DATABASE 语句，因此会引发异常。

如果你希望你的应用程序能够创建新的 InterBase 数据库，你需要找到另一种方法。一种方法是在程序目录中保留一个数据库的空副本，并在用户创建新数据库时将其复制。

在我自己的经验中，我发现以下方法很有用：将空数据库的副本作为资源保存在你的应用程序中。当用户创建新数据库时，将该资源以用户选择的文件名保存到磁盘上。以下说明介绍了如何在 Windows 环境中实现这一点。请注意，这是 Windows 特有的，不能用于 Linux 或跨平台应用程序。

首先，你需要创建一个资源脚本文件，将你的空数据库转换为资源。假设你在 D:\Interbase 目录中有一个数据库的空副本，以下脚本文件将创建一个名为 EMPTYDB 的资源：

```
EMPTYDB RCDATA DISCARDABLE "D:\Interbase\Empty.GDB"
```

将此脚本保存为 EmptyDB.RC。要从资源脚本创建 .RES 文件，请执行以下命令：

```
BRC32 EMPTYDB.RC
```

这将创建文件 EMPTYDB.RES，该文件可以包含在你的应用程序中。在你的程序代码的某处，请包含列表 1.3 中的代码。

### 列表 1.3 从资源创建空数据库的代码

```
{$R EmptyDB.RES}    // 将空数据库添加到程序可执行文件

procedure CreateDatabase(const DatabaseName: string);
var
    HRsrc: THandle;
    Stream: TResourceStream;
begin
    HRsrc := FindResource(HInstance, PChar('EMPTYDB'), RT_RCDATA);
    if HRsrc <> 0 then begin
        Stream := TResourceStream.Create(HInstance, 'EMPTYDB', RT_RCDATA);
        try
            Stream.SaveToFile(DatabaseName);
        finally
            Stream.Free;
        end;
    end else
        raise Exception.Create('Internal error: unable to create database.');
end;
```

现在，当你在应用程序中想要创建新数据库时，只需调用 CreateDatabase，并传入数据库的完整路径名，如下所示：

```
CreateDatabase( 'C:\NewDatabase.gdb' );
```

在开发应用程序时，如果你更改了数据库模式，你必须记得重新发出 **BRC32** 命令（如上所示）以重新创建 EMPTYDB.RES 文件。否则，你将在应用程序内部得到一个不正确的空数据库。

处理这种情况的另一种方法是在应用程序内部直接调用数据库 API 的低级接口。这种方法的好处是跨平台，但你必须学习针对相关数据库后端的相应 API 命令。

## DML 命令

DDL 命令用于定义数据库模式，而 DML 命令用于操作（读取、写入和更新）数据库中的数据。

## 简单 SQL 语句

最简单的 DML 语句是不带参数且不返回行数的语句。例如，你可能想要删除所有 *Active* 状态为 N 的员工。为此，你将发出以下语句：

```
SQLConnection1.ExecuteDirect('DELETE FROM EMPLOYEE WHERE Active = ''N''');
```

注意前面的代码片段中，‘N’ 被引号包围。手动引用字符串常量的更好方法是使用 RTL 函数 `QuotedStr`。`QuotedStr` 接受一个字符串参数并返回带引号的字符串。使用 `QuotedStr` 的主要原因之一是它能正确处理包含引号的字符串常量。例如，给定名字 O’Toole，你知道如何手动引用它吗？正确的方法是 ‘O’‘Toole’

使用 `QuotedStr`，你不需要担心如何正确引用字符串。前面的 `ExecuteDirect` 调用变为

```
SQLConnection1.ExecuteDirect('DELETE FROM EMPLOYEE WHERE Active = ' + 
    QuotedStr('N'));
```

## 参数化 SQL 语句

很多时候，你希望多次执行同一个基本 SQL 语句，仅更改传递给语句中参数的值。例如，假设你想将多条记录插入之前创建的 EMPLOYEE 表中。要插入员工 John Doe，你需要执行以下 SQL 语句：

```
SQLConnection1.ExecuteDirect('INSERT INTO EMPLOYEE VALUES (123,
    ''John Doe'', ''5/15/1994'', 35000)');
```

再次说明，这里可以使用 `QuotedStr` 代替手动引用字符串。

对于你要添加的每个员工，你都需要创建并执行类似的 SQL 语句。参数化 SQL 语句允许你创建一种语句 *模板*，你可以通过在执行前轻松填入适当的值来生成每个语句。对于 EMPLOYEE 表，SQL INSERT 语句变为以下内容：

```
INSERT INTO EMPLOYEE VALUES (:EmpNumber, :Name, :Hired, :Salary)
```

每个要插入数据库的值都用参数替换。参数很容易检测，因为它们以冒号开头。内部地，dbExpress 组件解析 SQL 语句，并将参数转换为核心 dbExpress 代码支持的问题符。进而，dbExpress 驱动程序用后端数据库引擎支持的参数标记符替换这些问号。

例如，对于前面的 INSERT 语句，TSQLConnection 将其更改为

```
INSERT INTO EMPLOYEE VALUES (?, ?, ?, ?)
```

dbExpress 驱动程序可能会用特定于数据库服务器的其他结构替换这些问号。

> 参数的名称不需要与表中的底层列名相同。请注意前面的代码片段中，我将参数命名为 `EmpNumber` 而不是 `EmpNo`，以及 `Hired` 而不是 `DateHired`。

创建 SQL 语句后，在执行之前需要填写每个参数的值。以下代码片段展示了如何做到这一点：

```
Params := TParams.Create(nil);
try
   // 创建参数
   Params.CreateParam(ftInteger, 'EmpNumber', ptInput);
   Params.CreateParam(ftString, 'Name', ptInput);
   Params.CreateParam(ftSQLDate, 'Hired', ptInput);
   Params.CreateParam(ftFloat, 'Salary', ptInput);

   // 为参数赋值
   Params.ParamByName('EmpNumber').Value := 123;
   Params.ParamByName('Name').Value := 'John Doe';
   Params.ParamByName('Hired').Value := '5/15/1994';
   Params.ParamByName('Salary').Value := 35000;

   // 执行语句
   SQLConnection1.Execute('INSERT INTO EMPLOYEE VALUES (:EmpNumber, :Name, '
   +':Hired, :Salary)', Params);
finally
   Params.Free;
end;
```

你可能想知道为什么你会想这样做，而不是直接执行每个语句。毕竟，创建参数并赋值需要更多的努力。此外，在我的开发机器上的计时测试表明，第二种方法所需的时间大约是第一种方法的两倍。

在需要重复执行同一语句的情况下，我仍然偏好使用参数化查询，原因如下：

-   简单性。给定一个长而复杂的 SQL 语句，手动形成 SQL 语句往往很困难。考虑到在 Pascal 语言中必须对单引号进行加倍，正确对齐引号很容易出错。
-   健壮性。假设某个员工名字中包含引号，例如 Frank O'Donnell。如果你不使用参数，这个引号看起来就像是名字的结束引号。无参数的 SQL 语句将看起来像这样：
    INSERT INTO EMPLOYEE VALUES (123, 'Frank O'Donnell', '5/15/1994', 35000)
    在这种情况下，名字看起来是 Frank O，而语句中的下一个字符（D）是一个错误。你可以通过对名字进行双重引用来解决这个问题，如下所示：
    INSERT INTO EMPLOYEE VALUES (123, 'Frank O''Donnell', '5/15/1994', 35000)
-   当使用参数时，真正的关系数据库可以编译已准备好的语句，然后在后续对该 SQL 语句的所有调用中使用该编译版本。在重复发出相同的 SQL 语句时，这完全补偿了准备 SQL 语句所需额外时间。

使用 `QuotedStr` 自动引用字符串有助于缓解前两个“问题”。

## 返回游标的 SQL 语句

在前两节中，我讨论了简单和参数化的 SQL 语句，但到目前为止，没有语句从数据库服务器返回任何数据。SELECT 语句是最常用的 DML 语句。那么，我为什么回避它呢？

这是因为 SELECT 语句返回数据，你需要有一个地方来放置结果数据。对于 dbExpress，那个地方是 TCustomSQLDataSet，我将在下一章中详细讨论。目前，我将快速概述如何从 TSQLConnection 检索数据。

Execute 方法，我在前面一节中讨论过，实际上接受第三个参数：指向结果集的一个指针。

```
function Execute(const SQL: string; Params: TParams;
ResultSet: Pointer = nil): Integer;
```

如果你不向 Execute 传递第三个参数，它默认为 nil，这意味着该语句不返回结果集。

> **注意**
> 如果你为 ResultSet 传递一个 nil 值，而 SQL 命令实际上确实返回了一个结果集，该结果集将被简单地丢弃。不会引发异常，也不会返回错误。
