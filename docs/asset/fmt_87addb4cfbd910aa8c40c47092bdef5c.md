
```delphi
procedure TransferFunds(FromAccountID: Integer; ToAccountID: Integer;
  Amount: Double);
var
  SQL: string;
  Params: TParams;
begin
  Params := TParams.Create;
  try
    SQL := 'INSERT INTO ACCOUNTDETAIL (ACCOUNTID, TRANSDATE, AMOUNT) ' +
           'VALUES (:AccountId, :TransDate, :TransAmount)';
    Params.ParamByName('AccountId').Value := FromAccountID;
    Params.ParamByName('TransDate').Value := Date;
    Params.ParamByName('TransAmount').Value := -Amount;
    SQLConnection1.Execute(SQL, Params);
    
    Params.ParamByName('AccountId').Value := ToAccountID;
    Params.ParamByName('TransAmount').Value := Amount;
    SQLConnection1.Execute(SQL, Params);
  finally
   Params.Free;
end;
end;
```

从概念上讲，这段代码片段为源账户创建了一笔提款记录，并为目标账户创建了一笔存款记录。起初，这段代码似乎没有什么问题，但让我们来看看其中可能出现的情况。

如果在记录提款和记录存款之间发生断电、连接故障或其他灾难性故障，会发生什么？储蓄账户中的钱会被扣除，但永远不会被存入支票账户（这让 Customer 先生变得非常不高兴，甚至可能不再是该银行的*客户*）。

如果代码反过来，先创建存款再创建提款，则可能发生相反的情况：存款被记录，但提款从未发生（这让 Customer 先生非常高兴，并且多了 $100，但银行却亏损了）。

显然，ATM 软件需要确保提款和存款要么都发生，要么都不发生。这正是事务设计要处理的问题。

接下来的几个部分将描述如何检测给定数据库是否支持事务、如何开始（以及随后结束）事务，以及如何处理多个（和嵌套的）事务。

## 检查事务支持

如果你正在编写一个仅适用于单一数据库后端（如 Oracle 或 InterBase）的应用程序，在开始编码之前你就知道该数据库支持事务。如果你正在编写一个可以访问许多不同数据库后端的通用应用程序，你不知道选定的数据库后端是否支持事务。

`TSQLConnection` 提供了一种检测底层数据库引擎是否支持事务的方法：`TransactionsSupported` 属性。在检查 `TransactionsSupported` 之前，你需要建立到数据库的连接，例如：

```delphi
SQLConnection1.Open;
...
if SQLConnection1.TransactionsSupported then begin
   // 继续事务代码
end else begin
   // 不支持事务 - 采用替代代码或退出
end;
```

## 开始事务

当你确定数据库支持事务后，就可以开始一个事务。首先，调用 `SQLConnection.StartTransaction` 方法。`StartTransaction` 定义如下：

```delphi
procedure StartTransaction( TransDesc: TTransactionDesc);
```

`TTransactionDesc` 是一个记录类型，详细描述事务。其定义如下所示：

```delphi
TTransactionDesc = packed record
TransactionID : LongWord; { Transaction id }
GlobalID : LongWord; { Global transaction id }
IsolationLevel : TTransIsolationLevel; {Transaction Isolation level}
CustomIsolation : LongWord; { DB specific custom isolation }
end;
```

表 1.6 展示了 `TTransactionDesc` 记录中各个字段的意义。

### 表 1.6 TTransactionDesc 字段

| 字段 | 定义 |

|---|---|

| TransactionID | 用户定义，本地事务编号，用于在应用范围内唯一标识该事务。 |

| GlobalID | 用于 Oracle 事务，定义一个在整个 Oracle 数据库中必须唯一的事务编号。 |

| IsolationLevel | 用于指定此事务如何反应其他事务。该字段的有效值列于表 1.7。 |

| CustomIsolation | 当 IsolationLevel 设置为 x11CUSTOM 时，标识自定义隔离级别。目前没有任何 dbExpress 驱动支持此项。 |

表 1.7 展示了 `TTransactionDesc` 的 `IsolationLevel` 字段的有效设置。

### 表 1.7 有效的 IsolationLevel 值

| 字段 | 定义 |

|---|---|

| x11DIRTYREAD | 事务可以看到由其他事务做出的所有更改，即使这些更改尚未提交。Oracle 不支持此事务隔离级别。 |

| x11READCOMMITTED | 事务只能看到那些由其他事务做出的、且在本事务开始前和本事务开始后已提交的更改。 |

| x11REPEATABLEREAD | 事务只能看到那些由其他事务做出的更改，且仅当这些更改在本事务开始前已提交时。 |

| x11CUSTOM | 特定于数据库的隔离级别。CustomIsolation 指定实际的隔离级别。目前没有任何 dbExpress 驱动支持此项。 |

以下代码片段展示了如何开始一个事务。

```delphi
var
  TransDesc: TTransactionDesc;
begin
  TransDesc.TransactionID := 1;
  TransDesc.IsolationLevel := x11READCOMMITTED;
  SqlConnection1.StartTransaction(TransDesc);
end;
```

## 提交事务

在事务中执行了相应的 SQL 命令后，你可能希望*提交*该事务。这将结束该事务，并保存该事务期间所做的任何更改。提交事务很简单，只需调用 `TSQLConnection.Commit`，如下面的代码行所示：

```delphi
SqlConnection.Commit(TransDesc);
```

## 回滚事务

有时，你启动一个事务，但后来发现你不想保存该事务期间所做的更改。如果出现这种情况，你可以*回滚*事务，而不是提交它。回滚事务会结束该事务，但在该事务上下文中所做的所有更改都会被丢弃。

要回滚事务，请调用 `TSQLConnection.Rollback`，如下所示：

```delphi
SqlConnection1.Rollback(TransDesc);
```

## 多个事务

你并不限于一次只能有一个事务。事务可以嵌套或重叠。图 1.7 在概念上展示了嵌套和重叠事务的样子。

![](img/fe651f295b5f960d5463c4fb581d2281_53_0.png)

## 图 1.7

*事务可以嵌套或重叠。*

并非所有数据库都支持多事务。不幸的是，要确定数据库是否支持多事务，无法通过检查某个简单的属性来实现。`TSQLConnection` 包含一个名为 `FSupportsMultiTrans` 的私有字段，但没有公共访问接口。不过，情况并非毫无希望，你可以使用以下函数来获取该属性的值：

```pascal
function SupportsMultiTrans(conn: TSQLConnection): Boolean;
var
  Supported: LongBool;
  PropSize: SmallInt;
begin
  conn.MetaData.GetOption(eMetaSupportsTransactions, @Supported,
    SizeOf(Integer), PropSize);
  Result := Supported;
end;
```

如果数据库不支持多事务，你应当避免在事务处于活动状态时调用 `StartTransaction`。你可以通过检查 `InTransaction` 属性来测试当前是否有活动的事务，如下所示：

```pascal
if not SQLConnection1.InTransaction then
  // 此时开始事务是安全的
```
