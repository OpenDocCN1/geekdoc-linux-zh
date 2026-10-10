
列表 3.6 包含范围形式的源代码。范围形式会提示用户输入薪资下限和上限。

## 列表 3.6 RangeFilter—RangeForm.pas

```pascal
unit RangeForm;

interface

uses
   SysUtils, Classes, QGraphics, QControls, QForms, QDialogs, QExtCtrls,
   QStdCtrls;

type
   TfrmRange = class(TForm)
      pnlClient: TPanel;
      pnlBottom: TPanel;
      Label1: TLabel;
      Label2: TLabel;
      ecLower: TEdit;
      ecUpper: TEdit;
      btnOk: TButton;
      btnCancel: TButton;
      procedure btnOkClick(Sender: TObject);
   private
      function GetHighValue: Double;
      function GetLowValue: Double;
      { Private declarations }
   public
      { Public declarations }
      property LowValue: Double read GetLowValue;
      property HighValue: Double read GetHighValue;
   end;

implementation

{$R *.xfm}

{ TfrmRange }

function TfrmRange.GetHighValue: Double;
begin
   Result := StrToFloat(ecUpper.Text);
end;

function TfrmRange.GetLowValue: Double;
begin
    Result := StrToFloat(ecLower.Text);
end;

procedure TfrmRange.btnOkClick(Sender: TObject);
var
    LowValue: Double;
    HighValue: Double;
begin
    try
        LowValue := StrToFloat(ecLower.Text);
        HighValue := StrToFloat(ecUpper.Text);

        if LowValue > HighValue then begin
            ModalResult := mrNone;
            ShowMessage('The upper salary must be >= the lower salary');
        end;
    except
        ModalResult := mrNone;
        ShowMessage('Both values must be a valid number');
    end;
end;
```

图 3.8 展示了 RangeFilter 应用程序的运行情况。

![](img/fe651f295b5f960d5463c4fb581d2281_147_0.png)

## 图 3.8

RangeFilter 对数据集应用范围过滤和筛选。

## 搜索

除了从客户端数据集中过滤掉不感兴趣的记录外，TClientDataSet 还提供了一些用于快速定位特定记录的方法。其中一些方法要求数据集上存在活动的索引，而另一些则不需要。搜索方法将在以下章节中详细介绍。

### 非索引搜索技术

在本节中，我将讨论那些不需要客户端数据集中存在活动索引的搜索技术。这些方法不使用索引，而是通过对数据集执行顺序搜索来查找第一个匹配的记录。

### Locate

Locate 也许是 TClientDataSet 搜索方法中最通用的一个。你可以使用 Locate 基于任意给定字段或字段组合来搜索记录。Locate 还可以基于部分匹配来搜索记录，并且可以执行不区分大小写的匹配。

TClientDataSet.Locate 的定义如下：

```pascal
function Locate(const KeyFields: string; const KeyValues: Variant;
  Options: TLocateOptions): Boolean; override;
```

第一个参数 KeyFields 指定要搜索的字段（或字段集合）。在搜索多个字段时，请用分号将它们分开（例如，‘Name;Birthday’）。

第二个参数 KeyValues 表示要搜索的值。值的数量必须与关键字段的数量完全匹配。如果只有一个搜索字段，你只需在此处传入要搜索的值。若要搜索多个值，你必须将值作为变体数组传入。执行此操作的一种方法是调用 VarArrayOf，如下所示：

```pascal
VarArrayOf(['John Smith', '4/15/1965'])
```

最后一个参数 Options 是一个集合，决定了搜索的执行方式。表 3.11 列出了可用的选项。

#### 表 3.11 Locate 选项

| 值 | 描述 |
| :--- | :--- |
| loPartialKey | KeyValues 不一定代表精确匹配。Locate 找到第一个字段值以 KeyValues 中指定值开头的记录。 |
| loCaseInsensitive | Locate 在搜索字符串字段时忽略大小写。 |

这两个选项仅适用于字符串字段。如果你在非字符串搜索中指定了它们，它们将被忽略。

如果找到匹配记录，Locate 返回 True；如果未找到匹配项，则返回 False。在匹配的情况下，该记录会被设为当前记录。

以下示例有助于说明这些选项：

```pascal
ClientDataSet1.Locate('Name', 'John Smith', []);
```

这搜索名称为 'John Smith' 的记录。

```pascal
ClientDataSet1.Locate('Name', 'JOHN', [loPartialKey, loCaseInsensitive]);
```
这搜索名称以 'JOHN' 开头的记录。这会找到 'John Smith'、'Johnny Jones' 和 'JOHN ADAMS'，但不会找到 'Bill Johnson'。

```pascal
ClientDataSet1.Locate('Name;Birthday', VarArrayOf(['John', '4/15/1965']), [loPartialKey]);
```

这搜索名称以 'John' 开头且生日为 1965 年 4 月 15 日的记录。在这种情况下，loPartialKey 选项仅适用于名称。尽管生日以字符串形式传入，但底层字段是日期字段，因此 loPartialKey 选项仅对该字段被忽略。

### Lookup

Lookup 在概念上与 Locate 相似，只是它不会更改当前记录指针。相反，Lookup 返回记录中一个或多个字段的值。此外，Lookup 不接受 Options 参数，因此你无法执行基于部分关键字或不分大小写的查找。

Lookup 的定义如下：

```pascal
function Lookup(const KeyFields: string; const KeyValues: Variant; const ResultFields: string): Variant; override;
```

KeyFields 和 KeyValues 指定要搜索的字段以及要搜索的值，正如 Locate 方法中那样。ResultFields 指定你想要返回数据的那些字段。例如，要返回名为 John Doe 的员工的生日，你可以编写以下代码：

```pascal
var
  V: Variant;
begin
  V := ClientDataSet1.Lookup('Name', 'John Doe', 'Birthday');
end;
```

以下代码返回 ID 号为 100 的员工的姓名和生日。

```pascal
var
V: Variant;
begin
V := ClientDataSet1.Lookup( 'ID', 100, 'Name;Birthday');
end;
```

如果未找到请求的记录，V 将被设置为 NULL。如果 ResultFields 包含单个字段名，则在从 Lookup 返回时，V 是一个包含 ResultFields 中列出的字段值的变体。如果 ResultFields 包含多个单字段名，则在从 Lookup 返回时，V 是一个包含 ResultFields 中列出的各字段值的变体数组。

> 关于变体数组的全面讨论，请参见我的著作《Delphi COM Programming》，由 Macmillan Technical Publishing 出版。

以下代码片段展示了如何访问从 Lookup 返回的结果。

```pascal
var
V: Variant;
begin
V := ClientDataSet1.Lookup( 'ID', 100, 'Name');
if not VarIsNull(V) then
ShowMessage( 'ID 100 refers to ' + V);

V := ClientDataSet1.Lookup( 'ID', 200, 'Name;Birthday');
if not VarIsNull(V) then
ShowMessage( 'ID 200 refers to ' + V[0] + ', born on ' + DateToStr(V[1]));
end;
```

### 索引搜索技术

前面提到的搜索技术不需要活动索引（实际上，它们甚至不需要数据集建立索引），但 TDataSet 还支持几种索引搜索操作。这些包括 FindKey、FindNearest 和 GetOKey，将在以下章节中讨论。

#### FindKey

FindKey 在当前索引的关键字段上搜索精确匹配。例如，如果数据集当前按 ID 索引，FindKey 将在 ID 字段上搜索精确匹配。如果数据集按姓和名索引，FindKey 将在姓和名两个字段上搜索精确匹配。

FindKey 接受一个参数，该参数指定要搜索的值。它返回一个布尔值，指示是否找到匹配的记录。如果未找到匹配项，当前记录指针保持不变。如果找到匹配记录，它将被设为当前记录。

FindKey 的参数实际上是一个值数组，因此你需要将值放在方括号中，如下面的示例所示：

```pascal
if ClientDataSet.FindKey([25]) then
    ShowMessage('Found ID 25');
...
if ClientDataSet.FindKey(['Doe', 'John']) then
    ShowMessage('Found John Doe');
```

你需要确保要搜索的值与当前索引匹配。因此，你可能希望在调用 FindKey 之前设置索引。以下代码片段说明了这一点：

```pascal
ClientDataSet1.IndexName := 'byID';
if ClientDataSet.FindKey([25]) then
    ShowMessage('Found ID 25');
...
ClientDataSet1.IndexName := 'byName';
if ClientDataSet.FindKey(['Doe', 'John']) then
    ShowMessage('Found John Doe');
```

#### FindNearest

FindNearest 的工作方式与 FindKey 相似，只是它找到大于或等于传入值的第一个记录。这取决于 KeyExclusive 属性的当前值。

如果 KeyExclusive 为 False（默认值），FindNearest 找到大于或等于传入值的第一个记录。如果 KeyExclusive 为 True，FindNearest 找到大于传入值的第一个记录。

如果 FindNearest 未找到匹配记录，它会将当前记录指针移动到数据集的末尾。

#### GotoKey

GotoKey 执行与 FindKey 相同的功能，只是你在调用 GotoKey 之前设置搜索字段的值。以下代码片段展示了如何做到这一点：

```pascal
ClientDataSet1.IndexName := 'byID';
ClientDataSet1.SetKey;
ClientDataSet1.FieldName('ID').AsInteger := 25;
ClientDataSet1.GotoKey;
```

![](img/fe651f295b5f960d5463c4fb581d2281_151_0.png)

