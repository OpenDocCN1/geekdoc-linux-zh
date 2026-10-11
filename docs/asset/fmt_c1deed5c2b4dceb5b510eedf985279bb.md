
# 数据库优化
第 18 章

```
ActualTime := Now;

if not IBTransaction1.InTransaction then
  IBTransaction1.StartTransaction;

Active := True;

// 在第二个 memo 中显示查询执行时间
Memo2.Lines.Add('Time to execute query: ' + FormatDateTime('hh:nn:ss.zzz', Now - ActualTime));
Memo2.Lines.Add(Plan);

// 不返回结果集，使用 ExecSql 执行
else
  if IBTransaction1.InTransaction then
    IBTransaction1.Rollback;
end;
```

# 优化查询

现在你有一种方法来测试你的语句。最初，你将创建一个语句从表中检索记录：

```
SELECT * FROM TABLE1 WHERE DESCRIPTION BETWEEN 'B'
```

第二个 memo 中的结果是：

```
Time to execute query: 00:00:00.069
PLAN (TEST_TABLE1 NATURAL)
```

# DataCLX
第四部分

img/cb7f7288580e05eab3a6dcf423bcc2f2_833_0.png

图 18.2

它使用了 IBX 组件：一个 `TIBDatabase`、一个 `TIBQuery` 和一个 `TIBTransaction`，拥有三个窗格。第一个窗格是用于输入查询的 memo 控件。当你点击按钮时，查询被执行，其结果显示在第二个窗格的 `TDBGrid` 中，该网格使用了连接到 `TIBQuery` 的 `TDataSource`。第三个窗格显示执行查询的时间，它使用了 InterBase 用于检索查询结果的计划。计划通过 `TIBQuery` 的 `plan` 属性获取。`Execute` 按钮的 `OnClick` 事件处理器程序为：

```
procedure TForm1.ButtonClick(Sender: TObject);
var
  ActualTime : DateTime;
begin
  with IBQuery1 do begin
    if Active then begin
      if IBTransaction1.InTransaction then
        IBTransaction1.Commit;
    Close;
  end;
  // 将 memo 行赋值给 TIBQuery 的 SQL 属性
  Sql := Memo1.Lines;
  try
    // 获取实际时间
    ActualTime := Now;
```

```
 // 打开查询 - 如果无法通过 Active := True 打开
 //（没有结果集）
 // 抛出异常
DatabaseError do
 // 获取实际时间
ActualTime := Now;
if not IBTransaction1.InTransaction then
  IBTransaction1.StartTransaction;
Active := True;
// 在第二个 memo 中显示查询执行时间
Memo2.Lines.Add('Time to execute query: ' + FormatDateTime('hh:nn:ss.zzz', Now - ActualTime));
Memo2.Lines.Add(Plan);
// 不返回结果集，使用 ExecSql 执行
else
  if IBTransaction1.InTransaction then
    IBTransaction1.Rollback;
end;
```

# 优化查询

...（后续翻译内容）

```
Time to execute query: 00:00:00.069
PLAN (TEST_TABLE1 NATURAL)
```

# DataCLX
第四部分

通过保持索引简单并有策略地建立索引，让优化器选择正确的计划会更好。你还应该注意，查询优化器通常在 InterBase 的每一个新版本中都会增强。

如果你决定确实要指定查询应该使用的计划，请在 `SELECT` 语句中包含 `PLAN` 关键字。

以下语句说明：

```
select order_no,sum(total_value) from test_table2
where order_date = '3/1/2001' group by order_no
```

当运行该查询时，你会在备录中得到此结果：

```
Time to execute query: 00:00:00.265
PLAN (TEST_TABLE2 ORDER RDB$PRIMARY11)
```

优化器将使用表2 的主索引。它使用 `ORDER_NO` 字段来检索行。由于你需要某个特定日期的记录，你可以尝试使用 `TEST_ORDER_INDEX`，它使用 `ORDER_DATE` 字段。可以通过以下查询实现：

```
SELECT ORDER_NO,SUM(TOTAL_VALUE)
FROM TEST_TABLE2
WHERE ORDER_DATE = '3/1/2001'
GROUP BY ORDER_NO
PLAN (TEST_TABLE2 ORDER TEST_ORDER_DATE)
```

这一次，当你运行查询时，你得到了此结果：

```
Time to execute query: 00:00:00.031
PLAN SORT ((TEST_TABLE2 INDEX (TEST_ORDER_DATE)))
```

这比之前的查询快了 20 多倍。如你所见，只需对查询进行微调、更改顺序、创建索引并修改原始计划，就能让你的查询飞起来，你的客户一定会非常感谢。当你设计查询时，可以使用像你用过的工具工具来查看发生了什么，并相应地优化你的查询。

# 使用 Gfix 设置数据库缓存缓冲区

有许多方法可以设置 InterBase 服务器上的缓存缓冲区数量。最好的方法是设置每个数据库分配的缓存缓冲区数量。目前无法通过 GUI 界面设置此值。你必须手动编辑 `ibconfig` 文件，或使用 `gfix` 命令设置缓冲区，如下：

```
Gfix -buffers 10000 -user sysdba -password masterkey \path\to\mydabase.gdb
```
