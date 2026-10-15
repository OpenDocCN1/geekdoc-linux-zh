
# Delphi 流式支持

Delphi 为派生自 `TPersistent` 的组件以及 `TCollection` 系列类的辅助函数提供了流式支持。

## 组件包装器示例

为了让之前描述的整数列表的流式化过程更加自动化，让我们为这些数据创建一个组件包装器。

```delphi
TIntegerItem = class(TCollectionItem)
private
    FNumber: Integer;
published
    property Number: Integer read FNumber write FNumber;
end;

TIntegerList = class(TComponent)
private
    FIntList: TCollection;
published
    property IntList: TCollection read FIntList;
end;
```

诚然，对于像整数列表这样简单的数据结构来说，这可能有点大材小用，但同样的概念也适用于包含多个字段或复杂子数据的组件。

> 注意
> 
> 本书不在详细讨论 Delphi 流式支持的范围内。有关流式技术的更多信息，请参阅《组件编写指南》或终极参考资源——VCL/CLX 源代码本身。如果你有幸拥有 Danny Thorpe 所著的《Delphi 组件设计》一书，其中关于 Delphi 流式机制的一章也非常有参考价值。

## 文件 BLOB

BLOB 字段的另一种常见用途是将整个文件存储在 BLOB 中。例如，假设你有大量 PDF 文档需要编目，并希望允许用户阅读这些文档。

通过将 PDF 文件存储在 BLOB 字段中，你可以比较轻松地创建一个应用程序，该应用允许用户按类别或关键词搜索 PDF，并在其计算机上查看该文件。

你可以使用字段的 `LoadFromFile` 方法将外部文件加载到 BLOB 字段中，如下面的代码片段所示：

```delphi
var
  B: TBlobField;
begin
  B := ClientDataSet1.FieldByName('AttachedFile');
  B.LoadFromFile('C:\PROPOSAL.PDF');
end;
```

如果你想将文件保存回磁盘（例如，为了将其加载到 Acrobat Reader 等应用程序中），你可以编写以下代码：

```delphi
var
  B: TBlobField;
begin
  B := ClientDataSet1.FieldByName('AttachedFile');
  B.SaveToFile('C:\TEMP.PDF');
end;
```

## BLOB 字段的局限性

尽管 BLOB 非常有用，但它们确实存在几项限制。具体来说：

- 你目前无法（currently）在 BLOB 字段上执行筛选。新一代的关系型数据库（如 Informix）支持在 BLOB 上进行搜索。一旦此功能被添加到核心 dBExpress 技术中，`TClientDataSet` 很可能也会随之更新以支持该功能。
- 你无法在 BLOB 字段上执行定位（locate）或其他搜索技术。
- 第 8 章“DataSnap”中讨论的 DataSnap 数据调节（reconciliation）功能不适用于 BLOB 字段。不过，在同一章中你将看到一种变通方法。

以下示例演示了本节讨论的一些 BLOB 技术。列表 4.4 显示了 BLOB 应用程序的源代码。

### 列表 4.4 BLOBs—MainForm.pas
