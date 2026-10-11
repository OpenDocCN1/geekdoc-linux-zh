
除非对字段执行了其中一个函数，否则该字段无法在聚合表达式中使用。例如，以下表达式将是非法的，因为 `field2` 是单独存在的。从另一个角度来看，聚合字段是在整个记录集上进行计算的，那么会使用 `field2` 的哪一个值呢？

`AVG(fieldname) * 0.05 + field2`

除了整个记录集的数据外，聚合还具有根据数据的分组级别计算表达式的能力。更多细节请参阅 Kylix 帮助文件。在聚合字段有了表达式后，通过将 `Active` 属性设置为 `true` 来激活聚合字段。同样，`ClientDataSet` 有一个 `AggregatesActive` 属性也必须设置为 `true`。查看聚合字段值最简单的方法是将其连接到 `TDBEdit` 字段上。

> 提示：计算字段不能作为任何聚合函数的字段名。相反，请创建一个 `InternalCalcField`，并在该计算字段上执行相应的聚合函数。

## 总结

Kylix 数据集提供了丰富的功能，允许开发者集中管理围绕 ASET 字段的设置、约束和事件。持久性字段对象为开发者提供了一个地方，可以在 Kylix IDE 内部控制和管理结果集字段。使用字段对象是在一个中心位置引入业务规则的极佳方法，并避免了重复编写相同代码的不必要工作。

# 第 4 节

## Kylix 2 开发

## 组件

第 15 章—CLX
第 16 章—编写自定义组件

# 第 15 章 CLX

## 引言

到本书为止，书中多次提到了 Kylix 组件架构，称为 CLX。在本章中，我们将通过深入研究这一强大且可扩展的架构，将 CLX 提升到高度。在本章结束时，CLX 的内部机制将向开发者开放，以便其利用。

CLX 代表 Component Library Cross(X)-Platform（组件库跨平台）。它是构成 Kylix 库的一系列类、对象和类型的统称。CLX 虽有多种形式，但可以细分为四个主要领域：

- `BaseCLX` 包含了 Kylix 架构的所有元素。`BaseCLX` 的细节可以在第 9 章“编译器、运行时库和变体”中找到。

- `DataCLX` 组件使用了 Kylix 和 Delphi 6 中新的 dbExpress 数据架构，以提供对当今各种主流数据库服务器强大且高效的访问。`DataCLX` 是第 12 章（“dbExpress 和 DataCLX”）的关注点，并延续到第 13 章（“客户端数据管理”）。

- `NetCLX` 包含了跨平台的 Internet 架构和组件。`NetCLX` 在第 21 章“网络应用程序”中讨论。

- 最后，`VisualCLX`（也称为 vCLX）指的是使其变得伟大的视觉和非视觉组件。它是本章的主题。

## vCLX 背景

### 什么是 CLX？

![](img/d784fa8294cae585d61ec86b987ea212_336_0.png)

图 15-1 显示了 CLX 如何与环境交互。CLX 的子集（`DataCLX`、`NetCLX` 和 `VisualCLX`）都构建在 `BaseCLX` 层之上，该层与 Qt 交互。

## vCLX 架构

幸运的是，普通开发者不需要理解 vCLX 的细节。Borland 对 vCLX 进行了封装，使得开发者在大多数情况下不需要处理它。然而，即使你只是在 vCLX 表面操作，了解内部发生了什么也是一个好主意。

## VCLX 文件

![](img/d784fa8294cae585d61ec86b987ea212_337_0.png)

vCLX 的讨论涉及对 Qt (C++) 层的描述和策略。请理解在 Kylix 中有一个概念落实的地方。图 15-2 描述了 vCLX 与 Linux 之间的交互。vCLX 的设计是为了减少对特定操作系统的依赖。但在现实中，vCLX 确实会调用操作系统，但仅在绝对需要时。有一个层称为 `DisplayCLX` 代表应用程序交互。`DisplayCLX` 由两个文件组成：`libqtint.so` 和 `Qt.pas`。

### libqtint.so

`libqtint.so` 是一个共享库（有关共享对象的库信息请参阅第 8 章），它动态绑定到 `libQt.so`，即 Qt 库。`libqtint.so` 让 vCLX 访问 Qt 的运行时库。当然，vCLX 并不 Qt 提供的所有函数。vCLX 使用的方法通过该库暴露。

### Qt.pas

由于 `libqtint.so` 是一个包含 C 和 C++ 代码的库，Kylix 必须动态绑定到各种例程并将其导入应用程序。为了实现这一点，Kylix 使用 `Qt.pas` 文件。`Qt.pas` 导入 `libqtint.so` 的功能，以便 vCLX 内部调用这些函数。它包含了很长的类型声明和函数导入。Qt 实际上是一组管理部署在系统上的视觉控件的 C++ 对象。`Qt.pas` 实际上是将这些对象平坦化为大量的函数调用——注意，除了创建对象的调用外，所有的调用都将第一个参数接收一个现有 Qt 对象的句柄。

# 第 15 章：CLX

```
// class declarations

QWidgetH = class(QObject) end;

QButtonH = class(QWidgetH) end;

QCheckBoxH = class(QPushButton) end;

QPushButtonH = class(QPushButton) end;

Q1xBitBtnH = class(QPushButton) end;

QRadioButtonH = class(QPushButton) end;

QToolH = class(QPushButton) end;
```

```
// method declarations

function QButton_create(parent: QWidget; name: PAnsiChar; f: WFlags): QButtonH; dcecl;

procedure QButton_destroy(handle: QPushButton); dcecl;

procedure QButton_text(handle: QPushButton; retval: PWideString); dcecl;

procedure QButton_setText(handle: QPushButton; pl: PWideString); dcecl;
```

```
// external method references. These refer to the corresponding 
// Qt method in libqtintf.so

procedure QButton_destroy; external QtShareName name QtNamePrefix + 'QButton_destroy';

function QButton_create; external QtShareName name QtNamePrefix + 'QButton_create';

procedure QButton_text; external QtShareName name QtNamePrefix + 'QButton_text';

procedure QButton_setText; external QtShareName name QtNamePrefix + 'QButton_setText';
```

![](img/d784fa8294cae585d61ec86b987ea212_338_0.png)

> 注意：`Qt.pas` 动态链接到 `libqtintf.so`，而 `libqtintf.so` 又动态链接到 `libqt.so`。这会对部署产生巨大影响，因为某些系统可能已经有了 `libqt.so`（大约 7 MB）。如果系统中已经存在正确版本的 `libqt.so`，则只需要发布 `libqt.so` 即可。

## 控件与其他实体

所有 Kylix 控件都继承自 `TControl` 类，而 `TControl` 类又继承自 `TComponent`。控件是任何视觉组件（在运行时环境中具有视觉表示的组件）。控件分为两种：`TGControls` 和 `TWidgetControls`。它们之间的主要区别在于，`TGControls` 仅仅是绘制在屏幕上的，而 `TWidgetControls` 则需要来自 Qt 的句柄（handle），可以通过 `Handle` 属性进行访问。vCL 对象实际上是指其底层 Qt 对象（通常称为 widget）的指针。`Handle` 是一个只读属性。下面的代码示例展示了使用 `Handle` 属性获取底层 Qt 对象信息的示例，在本例中是获取类名。

```
procedure TForm1.ButtonClick(Sender : TObject);
begin
  SendMessage(QClassName(Sender as TButton).Handle));
end;
```
