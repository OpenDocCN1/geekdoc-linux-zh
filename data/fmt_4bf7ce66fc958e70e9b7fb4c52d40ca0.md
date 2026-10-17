
unit FormDataMain;

```pascal
interface
uses
SysUtils, Types, Classes, QGraphics, QControls, QForms,
Dialogs, DB, SQLEpr, FMTBCD, Provider, DBClient, QextCtrls,
DBCtrls, Qgrids, DBGrids, DBXpress, QcomCtrls;
type
TfrmCustomer = class(TForm)
  dbgrdEmployee: TDBGrid;
  dtscEmployee: TDataSource;
  clintdstEmployee: TClientDataSet;
  dtstprvdrEmployee: TDataSetProvider;
  ltbrMain: TToolbar;
  btnFirst: TButton;
  btnPrior: TButton;
  btnNext: TButton;
  btnLast: TButton;
  btnPageUp: TButton;
  btnPageDown: TButton;
  procedure TbtnPageUpClick(Sender: TObject);
  procedure TbtnPageDownClick(Sender: TObject);
private
  { 私有声明 }
public
  { 公有声明 }
end;
const
  PAGE_DOWN = 8;
PAGE_UP = -8;
var
  frmCustomer: TfrmCustomer;
implementation
uses DataModule;
{ * }
procedure TfrmCustomer.btnFirstClick(Sender: TObject)
begin
  // 此方法用作导航
//按钮的事件处理器。
  case (Sender).Tag of
    0: dtscEmployee.First;
    1: dtscEmployee.Prior;
    2: dtscEmployee.Next;
    3: dtscEmployee.Last;
  end;
end;
procedure TfrmCustomer.btnPageDownClick(Sender: TObject)
begin
  // 此方法用作页向上和
// 页向下按钮的事件处理器。
  case (Sender).Tag of
    4: dtscEmployee.MoveBy(PAGE_UP);
    5: dtscEmployee.MoveBy(PAGE_DOWN);
  end;
end;
```

![](img/d784fa8294cae585d61ec86b987ea212_303.png)

# 第 13 章：客户端数据管理

## 过滤

来自服务器的数据通常需要在客户端进行过滤。`ClientDataSets` 通过 `Filter` 和 `Filtered` 属性提供过滤功能。`Filter` 是一个与 `WHERE` 子句语法类似的字符串。下表显示了有效的运算符。

### 表 13-1

| 运算符 | 描述 |
| --- | --- |
| <, >, <=, >= | 小于、大于、小于等于、大于等于 |
| =, <> | 等于、不等于 |
| AND, NOT, OR | 测试表达式真假 |
| IS NULL, IS NOT NULL 测试是否为空 |
| +, *, / | 对数值进行算术运算（+ 也用于日期值） |
| Upper, Lower | 字符串的大小 |
| Trim, TrimLeft, TrimRight | 去除字符串两端空格 |
| Substring | 返回从特定索引开始的子字符串 |
| Year, Month, Day | 返回日期的特定元素 |
| Hour, Minute, Second | 返回时间的特定元素 |
| Date | 返回当前日期或时间 |
| Like | 在字符串中搜索字符串模式 |
| In | 测试值是否在集合中 |
| * | 通配符。允许部分匹配 |

使用这些运算符，开发者可以为特定的数据集指定复杂的过滤器。要在运行时应用过滤器，将 `Filtered` 属性设置为 `true`。`Filtered` 属性也可用于判断过滤器是否已应用。为了防止用户看到公司总裁的信息，将 `Filter` 属性设置为：

```
JOB_CODE <> 'VP'
```

> 提示：记住，由于 `Filter` 属性类似于 SQL 语句中的 `WHERE` 子句，某些数据类型的值可能需要引号以形成有效的过滤器字符串。

## 搜索

在客户端数据搜索数据有两种方式：使用 `FindKey` 和 `FindNearest` 方法，或使用 `Locate` 方法。

### FindKey/FindNearest 方法

`FindKey` 和 `FindNearest` 允许用户通过逗号分隔的值列表指定记录。最常用的用法是提供数据的主键。如果找到了记录，指针将置于该记录。如果没有找到，指针将保持在当前位置且函数返回 `false`。`FindKey` 和 `FindNearest` 的主要区别在于 `FindKey` 搜索精确匹配，而 `FindNearest` 搜索最接近的匹配。

```php
procedure TrmEmployee.edtCodeSearchChange(Sender: TObject);
begin
  clndtEmployee.IndexFieldNames := 'Job_Code';
  if not clndtEmployee.FindNearest([edtSearch.Text]) then
    raise EJobNotFound.Create('未找到该作业代码。');
end;
```

在此示例中，`FindNearest` 用于提供增量搜索。由于该函数被用在 Edit 控件的 `OnChange` 事件中，因此每当用户在控件中输入（或删除）字符时都会被调用。

提示：`FindKey` 和 `FindNearest` 方法会在当前索引上自动搜索。要在特定字段上搜索，必须像上例那样显式设置索引。`Locate` 方法（见下一节）允许用户指定搜索字段以及搜索值，它是搜索数据值更常用的方法。

## Locate 方法

`Locate` 方法是一种查找结果集数据更流畅的方法。与 `FindKey` 和 `FindNearest` 方法不同，`Locate` 允许开发者不仅指定要查找的值，还指定查找的字段。`Locate` 是一个布尔方法，在完成后返回成功代码。如果找到记录，记录指针将移动到该位置且 `Locate` 返回 `true`。如果未找到记录，记录指针将留在当前位置且 `Locate` 返回 `false`。`Locate` 接受三个参数：搜索字段的、要搜索的值以及一组搜索选项（`TLocateOptions`）。

```php
procedure TrmEmployee.sptxtNameFindClick(Sender:TObject);
var SearchValue:Variant;
SearchFields:String;
begin
// 此方法被用作名称和
// ID 搜索按钮的事件处理程序。
SearchValue := edtButton.Text;
case (Sender as TButton).Tag of
  0 : SearchFields := 'Last_Name';
  1 : SearchFields := 'Emp_No';
end; // case 语句。
```

```php
if not clndtEmployee.Locate(SearchFields,SearchValue,[loCaseInsensitive,loPartialKey]) then
  Dlg('未找到员工','找不到指定的员工。',mtError,[mbOK],0);
```

```php
end;
```
