#  55.5 Borland编译器

下面所示的是Borland Delphi编译器以及C++ Builder的命名空间：

@Application@IdleActionsq
@Application@ProcessMDIaccels$qp6tagMSG
@Module@bctr$qppvtl
@Module@bdtrsq
@Module@ValidWindows$qp4TWindows
@TrueColorTo8BitNsqpviiiitliitiii
@TrueColorTo6BitNsqpviiiitliitiiiii
@DIB24BitToBitBitmap$qpviiiiitliitiii
@TrueBitmap@bctrsqpr
@TrueBitmap@bctrsqvr
@TrueBitmap@bctrsqqillii

> 由Borland编译出来的程序，其符号名称以字符“@”开头，后面几个字母分别代表：类名称、方法名称以及方法的参数类型。

这些符号名称可能出现在exe文件的输入表、dll文件的输出表以及调试数据等数据中。

VCL的全称是Borland Visual Component Libraries，意思是Borland的可视化组件库。它们保存在bpl文件中，而不是保存在dll文件中。比如文件vcl50.dll和rtl60.dll。

由Borland编译出来的程序还会导致BorLNDMM. DLL文件。

#  55.5.1 Delphi语言代码

通过观察我们看不出，几乎所有的Delphi可执行文件的代码起始部分都有一个“Boolean”字符串，后面跟着其他数据类型的类型名称。

这里列出一个非常典型的Delphi程序的代码片段，它就位于Win32程序的PE头部之后。

```
00000400 04 10 00 03 07 42 6f 6f 6c 65 61 6e 01 00 00
|...@Boolean...l|
00000410 00 01 00 00 00 00 10 40 00 00 05 46 61 61 6c 73 65
```