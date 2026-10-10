
### 手动设置编辑模式

如果 `dgAlwaysShowEditor` 为 True，当用户进入某个单元格时，网格会自动进入编辑模式。如果 `dgAlwaysShowEditor` 为 False，当用户按下 F2 时，网格会进入编辑模式。（用户也可以直接开始输入值来覆盖单元格的内容。）但是，如果您希望（为了与其他软件包兼容）在用户按下其他按键——例如按 F9 而不是 F2——时进入编辑模式，该怎么办？

要实现这一点，您需要控制网格进入编辑模式的时机。最佳位置是在网格的 `OnKeyDown` 事件中。在该处理程序中，将网格的 `EditorMode` 属性设置为 True 即可进入编辑模式。

以下代码片段展示了如何在用户按下 F9 时进入编辑模式（而不是在按下 F2 时）。

## 注意事项

为了让这段代码能够正常工作，你必须确保设置了 `dgEditing` 选项。如果未设置，即使代码将 `EditorMode` 设置为 `True`，网格也不会进入编辑模式。

## 检测列何时被调整大小

`TDBGrid` 提供了 `OnColumnMoved` 事件，但没有 `OnColumnSized` 事件。这意味着你可以轻松判断列何时被移动，但要确定列何时被调整大小则困难得多。幸运的是，通过编写一个包含单个重写方法的网格派生类，我们可以实现此功能。

### 清单 6.3 `ETHDBGrid.pas`

```pascal
unit ETHDBGrid;

interface

uses

Windows, Messages, SysUtils, Classes, Controls, Grids, DBGrids;

type

TETHDBGrid = class(TDBGrid)

private

{ Private declarations }

FOnColumnSized: TNotifyEvent;

protected

{ Protected declarations }

procedure ColWidthsChanged; override;

public

{ Public declarations }

published

{ Published declarations }

 property OnColumnSized: TNotifyEvent

 read FOnColumnSized write FOnColumnSized;

end;

procedure Register;

implementation

procedure Register;

begin

 RegisterComponents('ETH', [TETHDBGrid]);

end;

{ TETHDBGrid }

procedure TETHDBGrid.ColWidthsChanged;

begin

 inherited ColWidthsChanged;

 if Assigned(FOnColumnSized) then

 FOnColumnSized(Self);

end;
```

被重写的方法 `ColWidthsChanged` 调用了继承版本，然后触发 `OnColumnSized` 事件（如果你在应用程序中为其提供了事件处理程序）。

这段代码的作用仅仅是通知你某列已被调整大小。它不会告诉你哪一列被调整了大小、原来的宽度是多少，或者新的宽度是多少。提供这些额外信息需要更多的努力，并且会重复 `TDBGrid` 中大量的代码。我更喜欢保持我的派生组件简单直接。

> `TClientDataSetGrid`（将在本章后面讨论）也不提供这个事件处理程序。因此，如果你打算在应用程序中使用 `TClientDataSetGrid` 而不是 `TDBGrid`，你可能希望修改这里显示的代码，使其派生自 `TClientDataSetGrid`。

## 持久化网格设置

用户期望自定义设置能在多次程序运行之间保持持久，网格设置也不例外。当用户调整或重新排序网格中的列时，他们通常期望下次运行应用程序时列的顺序和大小保持不变。

持久化网格列设置并不难。你可以采取两种方法：

- 将设置保存到流或单独的文件中。
- 将设置保存到 Windows 注册表或 ini 文件中。

第一种方法更简单，所以我先介绍它。`TDBGrid` 的 `Columns` 属性提供了 `SaveToFile` 和 `SaveToStream` 方法，你可以使用这些方法以最小的麻烦将列配置保存到文件或流中。以下代码片段展示了如何将列设置保存到文件：

```pascal
TDBGrid.Columns.SaveToFile( 'GRID.CFG' );
```

同样地，要重新加载设置：

```pascal
TDBGrid.Columns.LoadFromFile( 'GRID.CFG' );
```

这种方法的缺点是，如果你的应用程序中有许多不同的网格，你需要为每个网格创建单独的配置文件的来持久化。如果情况如此，你可能希望使用 `SaveToStream` 而不是 `SaveToFile`。通过一点努力，你可以使用 `SaveToStream` 将网格的列配置保存到 ini 文件或 Windows 注册表中。以下过程将列信息保存到 ini 文件：

```pascal
procedure SaveColumnConfiguration(const FileName: string; Grid: TDBGrid;
  const SectionName: string; const Name: string);

var
  ini: TIniFile;
  MemStream: TMemoryStream;

begin
  MemStream := TMemoryStream.Create;
  try
    Grid.Columns.SaveToStream(MemStream);
    MemStream.Seek(0, soFromBeginning);
    ini := TIniFile.Create(FileName);
    try
      ini.WriteBinaryStream(SectionName, Name, MemStream);
    finally
      ini.Free;
    end;
  finally
    MemStream.Free;
  end;
end;
```

这段代码首先创建一个内存流，并将列配置保存到该流中。然后，它将流写入到 ini 文件。经过少量修改，你可以将此代码改为使用 Windows 注册表而不是 ini 文件。

同样地，以下过程从 ini 文件重新加载列信息：

```pascal
procedure LoadColumnConfiguration(const FileName: string; Grid: TDBGrid;
   const SectionName: string; const Name: string);

var
   ini: TIniFile;
   MemStream: TMemoryStream;

begin
   MemStream := TMemoryStream.Create;
   try
      ini := TIniFile.Create(FileName);
      try
         ini.ReadBinaryFileStream(SectionName, Name, MemStream);
         if MemStream.Size > 0 then
            Grid.Columns.LoadFromStream(MemStream);
      finally
         ini.Free;
      end;
   finally
      MemStream.Free;
   end;
end;
```
