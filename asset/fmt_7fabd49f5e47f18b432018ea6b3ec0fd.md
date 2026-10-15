
```
            LastNames[Random(12)];
        FCDS.FieldByName('Birthday').AsDateTime := StrToDate('1/1/1950') +
                Random(10000);
        FCDS.FieldByName('Salary').AsFloat := 20000.0 + Random(600) * 100;
        FCDS.Post;
    end;
    FCDS.First;
    finally
        FCDS.EnableControls;
    end;
    t2 := GetTickCount;
    lblFeedback.Caption := Format('%d ms to load %.0n records',
        [t2 - t1, MAX_RECS * 1.0]);
end;

procedure TfrmMain.Statistics1Execute(Sender: TObject);
var
    t1, t2: DWORD;
    msLocateID: DWORD;
    msLocateName: DWORD;
begin
    FCDS.First;
    t1 := GetTickCount;
    FCDS.Locate('ID', 9763, []);
    t2 := GetTickCount;
    msLocateID := t2 - t1;

    FCDS.First;
    t1 := GetTickCount;
    FCDS.Locate('Name', 'Eric Wallace', []);
    t2 := GetTickCount;
    msLocateName := t2 - t1;

    ShowMessage(Format('%d ms to locate ID 9763' +
        #13'%d ms to locate Eric Wallace' +
        #13'%.0n bytes required to store %.0n records',
        [msLocateID, msLocateName, FCDS.DataSize * 1.0, MAX_RECS * 1.0]));
end;

procedure TfrmMain.Save1Execute(Sender: TObject);
var
    t1, t2: DWORD;
begin
    t1 := GetTickCount;
    FCDS.SaveToFile('C:\\Employee.cds');
    t2 := GetTickCount;
    lblFeedback.Caption := Format('%d ms to save data', [t2 - t1]);
end;

procedure TfrmMain.LoadExecute(Sender: TObject);
var
	t1, t2: DWord;
begin
	try
		t1 := GetTickCount;
		FCDS.LoadFromFile('C:\\Employee.cds');
		t2 := GetTickCount;
		lblFeedback.Caption := Format('%d ms to load data', [t2 - t1]);
	except
		FCDS.Open;
		raise;
	end;
end;

end.
```

该应用程序包含五种方法，每一种都值得深入探究：

- `FormCreate` 在运行时创建客户端数据集及其架构。实际上，在设计时创建数据集会更容易一些，但我想向你展示在运行时执行此操作所需的代码。该代码创建了四个字段：*员工 ID、姓名、生日* 和 *薪资*。
- `PopulateExecute` 使用随机数据生成的 10,000 名员工来填充客户端数据集。在该方法的开始部分，我手动将 `RandSeed` 设置为 0，以确保多次运行应用程序时生成相同的数据。

**注意**

> Delphi 随机数生成器通常以当前的日期和时间作为种子。通过手动使用常量值为随机数生成器设置种子，我们可以确保每次运行程序时生成的随机数都是一致的。

- 该方法计算生成 10,000 名员工所需的大约时间，在我的计算机上大约需要半秒钟。
- `Statistics1Execute` 只是测量执行几个 `Locate` 操作所需的时间，并计算在磁盘上存储数据所需的空间量（再次强调，是二进制格式）。我将在本章稍后讨论 `Locate` 方法。
- `Save1Execute` 将数据保存到磁盘，文件名为 `C:\\Employee.cds`。对于以二进制格式保存的客户端数据集，`.cds` 扩展名是标准的，但并非强制要求的。以 XML 格式存储的客户端数据集通常使用 `.xml` 扩展名。

**注意**

> 请确保点击保存按钮，因为创建的文件（`C:\\EMPLOYEE.CDS`）将用于本章剩余的示例应用程序以及下一章中的一些示例。

- `Load1Execute` 从文件中将数据加载到客户端数据集。如果 `LoadFromFile` 失败（可能是因为文件不存在或不是有效的文件格式），客户端数据集将保持在关闭状态。因此，当引发异常时，我会重新打开客户端数据集。

图 3.5 显示了 CDS 应用程序在我的计算机上运行的情况。请注意显示在定位记录上的惊人时间。即使搜索几乎整个数据集来查找 ID 9763，在我的计算机上也只需大约 10 毫秒。

![](img/fe651f295b5f960d5463c4fb581d2281_124_0.png)

**图 3.5**

运行时的 CDS 应用程序。

# 导航客户端数据集

如果没有前进和/或后退的手段，数据集就毫无价值。Delphi 的数据集提供了许多用于遍历数据集的方法。以下各节讨论 Delphi 对数据集导航的支持。

## 顺序导航

遍历数据集最基本的方式是按顺序向前或向后移动。例如，在打印报告时，或者出于其他原因，你可能希望遍历数据集。Delphi 提供了四种简单的方法来实现这一点：

- `First` 移动到数据集中的第一个记录。`First` 总是成功的，即使数据集为空。如果为空，`First` 会将数据集的 `EOF`（文件末尾）属性设置为 `True`。
- `Next` 移动到数据集中的下一个记录（如果 `EOF` 属性尚未设置）。如果 `EOF` 为 `True`，则 `Next` 将失败。如果对 `Next` 的调用到达文件末尾，它会将 `EOF` 属性设置为 `True`。
- `Last` 移动到数据集中的最后一个记录。`Last` 总是成功的，即使数据集为空。如果为空，`Last` 会将数据集的 `BOF`（文件开始）属性设置为 `True`。
- `Prior` 移动到数据集中前一个记录（如果 `BOF` 属性尚未设置）。如果 `BOF` 为 `True`，则 `Prior` 将失败。如果对 `Prior` 的调用到达文件开始，它会将 `BOF` 属性设置为 `True`。

以下代码片段展示了如何使用这些方法来遍历数据集：

```
if not ClientDataSet1.IsEmpty then begin
    ClientDataSet1.First;
    while not ClientDataSet1.EOF do begin
        // Process the current record

        ClientDataSet1.Next;
    end;
end;

ClientDataSet1.Last;
while not ClientDataSet1.BOF do begin
    // Process the current record

    ClientDataSet1.Prior;
end;
```

![](img/fe651f295b5f960d5463c4fb581d2281_125_0.png)

## 随机访问导航

除了 `First`、`Next`、`Prior` 和 `Last`（它们提供在数据集中的顺序移动）之外，`TClientDataSet` 提供了两种直接移动到特定记录的方式：书签和记录号。

### 书签

与客户端数据集一起使用的书签与纸质书籍中使用的书签非常相似：它标记了数据集中的位置，以便你以后可以快速返回。

你可以对书签执行三种操作：设置书签、返回书签和释放书签。以下代码片段展示了如何执行这三种操作：
