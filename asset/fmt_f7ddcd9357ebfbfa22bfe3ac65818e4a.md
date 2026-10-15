
**图 1.4** 显示了从 `CONMAN` 数据库返回的表、字段和索引名称。

![图 1.4：CONTACTS 表的列和字段列表。](img/fe651f295b5f960d5463c4fb581d2281_37_0.png)

**图 1.5** 显示了 `CONTACTSBSYSTATE` 存储过程的参数列表。

![图 1.5：CONNECTBYSTATE 过程输出的长参数列表中的参数名称和类型。](img/fe651f295b5f960d5463c4fb581d2281_38_0.png)

**列表 1.2** 中的大部分代码相当简单直接。然而，有两点值得注意，我想特别指出。

首先，`cbProcedureClick` 方法展示了如何循环遍历存储过程的参数，以确定其名称、类型及其他属性。

其次，VCL/DataCLX 中存在一个 bug，实际上阻止了您同时获取表、视图和系统表的元数据。如果您同时勾选“表”、“视图”和“系统表”，`GetTableNames`（位于 `connAfterConnect` 方法中）将不会返回任何信息。请在您的应用中留意这一点。如果需要获取这三种类型的所有信息，您可以执行类似以下操作：

```pascal
var
  SL: TStringList;
begin
  SL := TStringList.Create;
  try
    SQLConnection1.TableScope := [tsTable, tsView];
    SQLConnection1.GetTableNames(ListBox1.Items, False);
    SQLConnection1.GetTableNames(SL, True);
    ListBox1.Items.AddStrings(SL);
  finally
    SL.Free;
  end;
end;
```

这段代码首先仅获取表和视图信息，并将结果放入列表框。接下来，它仅获取系统表，并将结果放入一个临时字符串列表。最后，它将临时字符串列表中的字符串添加到列表框中。因此，列表框中包含表、视图和系统表。

从上述讨论中可以看出，`TSQLConnection` 返回的模式信息极其基础。除了存储过程参数外，唯一的数据是

`TSQLConnection` 对表、字段、索引和存储过程返回的是它们的名称。在下一章中，我将展示如何从数据库中检索更详细的模式信息。

## 执行 DDL 和 DML 语句

你在数据库上执行的最常见操作是 DDL（数据定义语言）和 DML（数据操作语言）语句。你可以直接通过 `TSQLConnection` 执行 DDL 和 DML 语句。返回游标的 DML 语句（即 SQL SELECT 语句）除了 `TSQLConnection` 之外，还需要一个数据集组件，正如你在第 3 章“客户端数据集基础”中将要看到的那样。

### DDL 命令

DDL 命令是操作数据库模式而非数据本身的语句。在上一节中，我展示了如何检索有关数据库模式的信息。在这一节中，我将展示如何更改数据库模式。

`TSQLConnection` 提供了一个名为 `ExecuteDirect` 的方法，你使用它来执行 DDL 命令。`ExecuteDirect` 接受一个参数，即要执行的 SQL 命令。成功时返回 0，失败时返回 dbExpress 错误代码。dbExpress 错误代码可以在随 Delphi 提供的文件 `DBXpress.pas` 中找到。

名称 `ExecuteDirect` 中的 `Direct` 部分源于该语句直接发送到数据库这一事实。该语句在执行前不会进行预处理，并且不能包含任何参数。（参数化 SQL 语句将在本章后面标题为“参数化 SQL 语句”的章节中讨论。）

> **注意**
>
> 一些数据库不支持直接执行 SQL。在这些数据库上，dbExpress 将在内部预处理 SQL 语句，然后执行它。

#### 创建表

你可以发出的最简单且最有用的 DDL 命令之一是创建数据库中一个新表的命令。假设你想创建一个名为 `EMPLOYEE` 的表，其结构如表 1.5 所示。你需要发出以下语句：

```sql
SQLConnection1.ExecuteDirect('CREATE TABLE EMPLOYEE (EMPNO INTEGER, ' +
    'NAME VARCHAR(30), ' +
    'HIREDATE DATE, SALARY DOUBLE PRECISION');
```

**表 1.5** 示例 `EMPLOYEE` 表定义

| 列名 | 定义 |
| :--- | :--- |
| EMPNO | INTEGER |
| NAME | VARCHAR(30) |
| HIREDATE | DATE |
| SALARY | DOUBLE PRECISION |

#### 创建数据库

你不能使用 `ExecuteDirect` 来创建一个新的 InterBase 数据库。以下代码行不起作用：

```sql
SQLConnection1.ExecuteDirect('CREATE DATABASE ''C:\NewData.gdb''');
```

如果你尝试执行此代码，你会收到以下异常：

```
Cannot prepare a CREATE DATABASE/SCHEMA statement.
```

InterBase 客户端不允许直接执行 DDL 或 DML，因此 dbExpress 驱动程序会尝试预处理并执行 `CREATE DATABASE` 语句。由于 InterBase 不允许预处理 `CREATE DATABASE` 语句，因此会引发异常。

如果你的应用程序需要具备创建新 InterBase 数据库的能力，你需要找到另一种方法。一种方法是在程序目录中保留一个空数据库副本，当用户创建新数据库时将其复制。

我在自己的经验中发现以下方法很有用：将空数据库的副本作为资源保存在你的应用程序中。当用户创建新数据库时，将该资源保存为磁盘上用户选择的文件名的文件。下面的说明展示了如何在 Windows 环境中做到这一点。注意，这是特定于 Windows 的，不能用于 Linux 或跨平台应用程序。

首先，你需要创建一个资源脚本文件，将你的空数据库转换为资源。假设你在 `D:\Interbase` 目录中有一个空数据库副本，以下脚本文件创建一个名为 `EMPTYDB` 的资源：

```
EMPTYDB RCDATA DISCARDABLE "D:\Interbase\Empty.GDB"
```

将此脚本保存为 `EmptyDB.RC`。要从资源脚本创建 `.RES` 文件，请执行以下命令：

```
BRC32 EMPTYDB.RC
```

这将创建文件 `EMPTYDB.RES`，可以将其包含在你的应用程序中。在你的程序代码的某个位置，包含列表 1.3 中的代码。

**列表 1.3** 从资源创建空数据库的代码

```pascal
{$R EmptyDB.RES}  // 将空数据库添加到程序可执行文件中

procedure CreateDatabase(const DatabaseName: string);
var
  HResrc: THandle;
  Stream: TResourceStream;
begin
  HResrc := FindResource(HInstance, PChar('EMPTYDB'), RT_RCDATA);
  if HResrc <> 0 then begin
    try
      Stream := TResourceStream.Create(HInstance, 'EMPTYDB', RT_RCDATA);
      Stream.SaveToFile(DatabaseName);
    finally
      Stream.Free;
    end;
  end
  else
    raise Exception.Create('Internal error: unable to create database.');
end;
```

现在，当你要在应用程序中创建新数据库时，只需调用 `CreateDatabase`，并传入数据库的完整路径名，如下所示：

```
CreateDatabase( 'C:\NewDatabase.gdb' );
```

在开发应用程序的过程中，如果你更改了数据库模式，必须记住重新发出 `BRC32` 命令（如前所示），以重新创建 `EMPTYDB.RES` 文件。否则，你的应用程序内部将包含一个不正确的空数据库。

处理这种情况的另一种方法是直接从应用程序内部进行低级别的数据库 API 调用。这种方法的好处是跨平台，但你需要学习针对特定数据库后端的适当 API 命令。

### DML 命令

DDL 命令用于定义数据库模式，而 DML 命令用于操纵（读取、写入和更新）数据库中的数据。

#### 简单 SQL 语句

最简单的 DML 语句是不接受参数且不返回行的语句。例如，你可能想要删除所有 *Active* 状态为 N 的员工。为此，你需要发出以下语句：
