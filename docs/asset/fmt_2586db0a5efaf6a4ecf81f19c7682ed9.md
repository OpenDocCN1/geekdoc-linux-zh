
如列表 8.1 和 8.2 所示，共享对象的结构与应用程序并没有很大区别。应用程序和共享对象区别在于，在这种情况下，应用程序中拥有实际调用函数的代码。

```pascal
// 列表 8.2 - 一个共享对象
library SimpleSystem;

uses
  SysUtils;

function GetAmount(Amount: double): double;
begin
  // 这是针对金额的税费
  Result := Amount * 0.10;
end;

function GetTaxName: string;
begin
  Result := 'Simple System';
end;

procedure GetVersion(var MaxVersion, MinVersion: integer);
begin
  MaxVersion := 1;
  MinVersion := 0;
end;

exports
  GetAmount,
  GetTaxName,
  GetVersion;
```

## 使用 Kylix 创建的共享对象

在你编译并安装共享对象之后，你应该开始设置应用程序。

为了给共享对象设置客户端应用程序，你需要方法访问存储在共享对象中的函数。幸运的是，Kylix 有一种简单的方法来实现。你可以通过像在共享对象内部声明函数的方式来告诉 Kylix 某个函数位于共享对象，但要加上 `external` 声明、共享对象的文件以及该函数在共享对象内部的名称。例如：

```pascal
external 'filename.so' name 'myfunction';
```

名称声明是可选的，当你在应用程序中调用的名称与共享对象中的函数名称不同时，就会使用它。

声明列表 8.2 中函数的代码看起来就像列表 8.3 中的代码。

## 列表 8.4 - 使用共享对象的应用程序

```pascal
unit unitTaxClient;

interface

uses
  SysUtils, Types, Classes, Variants, QGraphics, QControls, QForms, QDialogs,
  QStdCtrls, TaxClientRoutines;

type
  TfrmTaxSharedObjClient = class(TForm)
    Label1: TLabel;
    lblTaxName: TLabel;
    Label3: TLabel;
    lblTaxVersion: TLabel;
    Label5: TLabel;
    edAmount: TEdit;
    btnCalculateTax: TButton;
    lblResultingTax: TLabel;
    procedure FormCreate(Sender: TObject);
    procedure btnCalculateTaxClick(Sender: TObject);
  private
    { 私有声明 }
  public
    { 公有声明 }
  end;

var
  frmTaxSharedObjClient: TFrmSharedObjClient;

implementation

{$R *.xfm}

procedure TFrmTaxSharedObjClient.FormCreate(Sender: TObject);
var
  MajVersion, MinVersion: integer;
begin
  lblTaxName.Caption := GetTaxName;
  GetVersion(MajVersion, MinVersion);
  lblTaxVersion.Caption := Format('%.d.%d', [MajVersion, MinVersion]);
end;

procedure TFrmTaxSharedObjClient.btnCalculateTaxClick(Sender: TObject);
begin
  lblResultingTax.Caption := FloatToStr(
    GetTaxAmount(StrToCurr(edAmount.Text)));
end;
```

## 508 第 8 章

图 8.2 - 共享客户端应用程序

![](img/890ec60032b6e2e34a8379c8a73731b2_530_0.png)

现在共享对象的客户端应用程序已经编写完成，你将能够利用业务规则与业务逻辑分离。在构建应用程序时，将业务规则与应用程序分离通常是一个好主意。这样，当你发布应用程序时，如果业务规则存储在共享对象中，你只需要将共享对象作为更新进行即可。如果你知道业务规则可能会发生变化，这是一个有效的解决方案。

## 在 C 中创建共享对象

现在你已经创建了第一个共享对象以及访问该对象的应用程序，你可能会发现自己掌握了关于操作共享对象的所有知识。然而，Kylix 是 Linux 开发领域的新手。由于 Linux 是用 C 语言编写的，你遇到的大多数共享对象也是用 C 编写的。因此，在导入其他共享对象时，了解 C 编写的共享对象是如何制作的对于理解如何更高效使用这些共享对象很重要。

因此，我们将从 C 创建一个共享对象文件以演示将其导入我们的应用程序。我们将使用与 Kylix 共享对象相同的函数，但我们将修改库使其可以用 C 编写并使用标准的 C 数据类型。共享对象的代码及其 Makefile 分别可以在列表 8.5 和 列表 8.6 中找到。

### 列表 8.5 - 共享对象文件的 C 代码

```c
#include <stdio.h>
#include <string.h>

extern double GetTaxAmount(double amount) {
    //这返回金额的三分之一
    return amount / 3;
}

extern void GetVersion(int *majorVersion, int *minorVersion) {
    *majorVersion = 2;
    *minorVersion = 1;
}

extern void GetTaxName(char *TaxName) {
    strcpy(TaxName, "A C written Tax Library\0");
}
```

### 列表 8.6 - C 编写的共享对象的 Makefile

```makefile
# 共享对象文件的 Makefile，用于演示在 C 中创建
# 共享对象文件然后在 Kylix 中调用它
#
# 由 Glenn Stephens 编写于《Tomes of Kylix - The Linux API》
# 由 Ward Publishing 出版 www.wordquare.com

AnotherTaxLibrary.so:AnotherTaxLibrary.c
gcc -FPIC -c -g AnotherTaxLibrary.c -o AnotherTaxLibrary.o
gcc -g -shared -Wl,-son,AnotherTaxLibrary.so -o AnotherTaxLibrary.so
AnotherTaxLibrary.o -lc
```

如果你熟悉 C 语言编程，那么列表 8.5 中的代码看起来会非常清晰。如果你不熟悉 C 语言，不要担心，我们将通过一些帮助你轻松导入库的规则。当你从共享对象导入函数时，如果你只有 C 语言定义，以下简单规则将帮助你完成许多转换。

## 从 C 编写的库中导入函数的规则

- 规则 1. 理解 C 和 Kylix 函数中参数和返回值的工作方式。

当你查看 Kylix 中的一个普通函数时，你将看到如下结构：

```pascal
function FunctionName(ParameterName: ParameterType): ReturnType;
```

C 函数的声明与下文代码所示略有不同：

`ReturnType FunctionName(ParameterType ParameterName);`

此外，如果 C 函数中的 `ReturnType` 是 "void"，你处理的是一个过程（procedure）而不是函数（function）。

你还需要记住 C 是一种大小写敏感的语言，在 Kylix 中命名函数时，确保它们与 C 对应项的大小写匹配。

- 规则 2. C 使用与 Kylix 不同的调用约定。

在 Kylix 下，调用约定与 C 不同。在 C 中，调用约定是 `cdecl`。

（注：原文中存在大量重复的“规则 2”及乱码，此处已去重处理）

## 第 8 章

你应该注意到列表 8.7 遵循了共享对象文件的转换规则。对于 `GetTaxAmount` 函数，Kylix 参数与其在 C 语言中的声明一致，且函数使用了 `cdecl` 调用约定。库中的 `GetVersion` 声明为 `void` 函数，这意味着它内部是一个过程（procedure）。你还会注意到 C 声明使用指针类型，而其对应的 Kylix 等效类型使参数变成了一个变量，函数实际上更改了参数的值。最后，`GetClassName` 展示了 C 字符串数据的使用以及如何将它们转换为 Kylix 字符串。任何 C 字符串都将作为字符数组的指针传递，这在 Kylix 中用用 `PChar` 数据类型表示。

本节提供了足够的在你的应用程序中链接共享对象文件的知识，你可能会遇到不知道库存储在何处的情况，或者你有许多共享库为你的应用程序创建一个插件系统，以便你的应用程序可以根据使用的库进行动态更改。为了处理这些情况，你将能够在运行时动态加载共享对象。

## 动态加载共享对象

通过不绑定到特定的文件名，你可以为你的应用程序创建一个插件框架，允许不同的共享对象以多态的方式运行。将一组共享对象作为框架还允许非 Kylix 语言的开发者为你的应用程序开发插件。我们已经在税收系统中看到了这一点，因此我们将修改现有的系统，动态调用任何以相同方式实现相同函数的共享对象。

要动态访问共享对象函数，你将使用 `dlopen`、`dlsym` 和 `dclose` API 函数。`dlopen` 返回共享对象的引用，`dlsym` 找到你将要用的函数的位置，而 `dclose` 释放共享对象。

`dlsym` 返回的实际上是函数在共享库中的内存位置。要调用它，你需要一个相应函数类型的变量。

你需要声明一个函数类型以便访问这些函数。到目前为止，我们一直在声明函数以及函数所链接的共享对象。为了演示插件的强大之处，列表 8.8 显示了相同插件的 Kylix 实现，它使用了与 C 库相同的函数，但是用 Kylix 编写的。

### 8.8 - 插件库的 Kylix 实现

```pascal
library KylixPluginTaxLibrary;
{
此库的设计用于与演示动态加载共享对象的插件系统兼容。
这还证明了插件可以使用两种完全不同的编程语言来编写。

由 Wordware 于 2001 年出版《imes of Kylix - The Linux API》
}

uses
  SysUtils;

function GetTaxAmount(Amount: double): double; cdecl; export;
begin
  //让我们返回 6.25% 的结果
  Result = Amount * 0.0625;
end;

procedure GetVersion(var MajorVersion, MinorVersion: integer); cdecl; export;
begin
  MajorVersion := 0;
  MinorVersion := 9;
end;

procedure GetTaxName(TaxName: PChar); cdecl; export;
begin
  StrPCopy(TaxName, 'A Cool Kylix plugin');
end;

exports
  GetTaxAmount,
  GetVersion,
  GetTaxName;
```

现在我们有一个 C 共享对象和一个 Kylix 共享对象，我们应该能够实现插件系统。但是首先，你需要函数的过程类型，以便你可以使用过程类型的变量来调用这些函数。税收系统的过程类型看起来类似于列表 8.9 中的代码。

### 列表 8.9 - 插件系统使用的过程类型

```pascal
unit TaxFunctionDeclarations;
interface

type
  GetTaxAmount = function(Amount: double): double; cdecl;
  GetVersion = procedure(var MajorVersion, MinorVersion: integer); cdecl;
  GetTaxName = procedure(TaxName: PChar); cdecl;

implementation
end.
```

现在过程类型已经创建，你可以使用 `dlopen` 和 `dlsym` 函数返回函数调用的位置。这个过程相对直接。你使用 `dlopen` 打开库，通过 `dlsym` 函数请求税收函数的位置。一旦完成工作，使用 `dclose` 函数关闭库。这就是列表 8.10 中插件系统所做的，它展示了创建一个可以使用多种语言开发的应用程序插件框架的完整威力。

图 8.3 - 税收库插件系统

列表 8.10 - 动态加载共享对象的代码
