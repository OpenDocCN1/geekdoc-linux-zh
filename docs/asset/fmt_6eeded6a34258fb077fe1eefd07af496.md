
书中的源码包含了 `URL` 和隐藏字段解决方案，允许你在编译时选择要使用的状态。

用于保持状态信息并使用其浏览表格的技术也可以用于其他地方。请注意，虽然你使用了 `RecNr` 来保留当前记录，但你也可以传递当前的唯一键值并使用它们搜索记录。在用户浏览时添加新记录时，这可能更为精确。

# 高级页面生成

你看到了 `PageProducers` 和 `TableProducers` 的作用。然而，当你组合这些组件并将一个的“输出”连接到另一个的“输入”时，变得非常有趣。特别是当你动态创建 `ContentProducing` 组件时（你可以从一个空的 模块开始并使用三个操作项，即 `/table/`、`/field` 和 `/browse`）。首先，选择带有 `/table` 路径的 `ActionItem` 并编写 `OnAction` 事件处理程序。

现在要构建的示例是一个 dbExpress 表格查看器，它动态指定表名和字段名。为了列出可用的 `TableNames`，你只需调用 `SQLConnection` 组件的 `TableView` 方法，并传递 `StringList` 作为参数：

```pascal
procedure TWebModule.WebModule1ActionItem3Action(Sender: TObject);
Request: TWebRequest; Response: TWebResponse; var Handled: Boolean);
const
WebApp42 = '/cgi-bin/WebApp42';
var
TableNames: StringList;
i: Integer;
begin
Response.Content := '<h1>Table Selection</h1><hr><p>';
TableNames := TStringList.Create;
TableNames.Sorted := True;
try
begin
Connected := True; // 以防万一
GetTableNames(TableNames)
end;
Response.Content := Response.Content +
'Please select a database table.'
'<form action=' + WebApp42 + '/field' method=post>' +
'<table>'
Response.Content := Response.Content +
'<tr align=right>Master:</td><td><select name='master'>
for i:=0 to Pred(TableNames.Count) do
Response.Content := Response.Content +
'<option value=' + TableNames[i] + '''>TableNames[i];
Response.Content := Response.Content +
'</select></td></tr>'
```

最终的选择结果可以在 Netscape 中的图 21.13 所示。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_917_0.png)

图 21.13

表格选择。在选择 `TableName` 并点击提交按钮后，将执行 `/field` 项，其实现如下：

```pascal
procedure TWebModule.WebModule1ActionItem4Action(Sender: TObject);
Request: TWebRequest; Response: TWebResponse; var Handled: Boolean);
const
WebApp42 = '/cgi-bin/WebApp42';
var
TableName: String;
i: Integer;
begin
Response.Content := '<h1>Table Fields</h1><hr><p>' +
'<form action=' + WebApp42 + '/browse' method=post>' +
'<input type=hidden name=master value=' +
Request.ContentFields.Values['master'] + '>';
with TSQLTable.Create(nil) do
try
SQLConnection := SQLConnection1;
TableName := Request.ContentFields.Values['master'];
FieldDefs.Update; // 无需实际打开表
Response.Content := Response.Content +
'<table><td width=200 bgcolor=#FFF00><<b>Table:</b> ' +
TableName + '<td bgcolor=cccccc valign=top>';
for i:=0 to Pred(FieldDefs.Count) do
Response.Content := Response.Content +
'<input type=checkbox checked name='M' ' +
FieldDefs[i].DisplayName + ' value='on' ' +
FieldDefs[i].DisplayName + ' <br>';
finally
Free
end;
Response.Content := Response.Content +
'</td></tr></table>' +
'<input type=reset><input type=submit>' +
'</form>'
```

注意，你需要将之前选值的 Table 字段传递到下一个 Web 页面（这样你就可以用它与选定的 FieldNames 组合）。这是通过传递名为 `Master` 的隐藏字段来实现（是的，它被称为 `Master`，因为稍后我们还会用它扩展一个 `Detail`）。

## Web

![](img/cb7f288580e05ab3a6dcf42bcc2f_19_0.png)

### 图 21.14
指定字段。

在选择了字段（如 `CUST_NO`、`CUSTOMER`、`CONTACT_FIRST`、`CONTACT_LAST`、`PHONE_NO`、`CITY` 和 `COUNTRY`）并点击 `Submit` 按钮后，执行的 `/browse` 实现如下：

```pascal
procedure TWebModule1.WebActionItem(Sender:Object);
var
  Request: TWebRequest; Response: TWebResponse; var Handled: Boolean;
const
  WebApp42 = '/cgi-bin/WebApp42';
var
  Master: TSQLTable;
  Str, Submit: String;
  i: Integer;
begin
  Str := '<h1>Table Contents</h1><hr><p>' +
         '<form action=\'' + WebApp42 + '/browse\' method=\'post\'' +
         '<input type=hidden name=\'master\' value=\'' +
         Request.ContentFields.Values['master'] + '\'>' +
         '<input type=submit name=Submit value=\"First\"> ' +
         '<input type=submit name=Submit value=\"Previous\"> ' +
         '<input type=submit name=Submit value=\"Next\"> ' +
         '<input type=submit name=Submit value=\"Last\">';
  Master := TSQLTable.Create(nil);
  try
    with Master do
    begin
      SQLConnection := SQLConnection1;
      TableName := Request.ContentFields.Values['master'];
      Open;
      for i := 0 to Pred(Fields.Count) do
        if Request.ContentFields.Values['M' + Fields[i].FieldName] = 'on' then
```
