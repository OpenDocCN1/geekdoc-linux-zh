
# Web
## 第五部分

此代码使用 Web 模块的 `OnBeforeDispatch` 事件处理程序来激活 `SqlConnection` 组件（该组件在设计时是没有连接的）。在 `SqlConnection` 组件的 `OnBeforeConnect` 事件处理程序中，你可以使用 `IFDEFs` 设置特定平台的属性 `LibraryName`、`VendorLib` 以及 `Database`（可以在 `SqlConnection` 组件的 `Params` 属性中找到）。

唯一的缺点是，Web 模块无法在 Kylix (Linux) 和 Delphi 6 (Windows) 环境中同时实现跨平台并在设计时激活，但我认为最好是选择一个环境来开发 Web 模块应用程序，另一个环境作为简单的编译器（为“另一个”平台生成可执行文件）。

## 总结

你已经学习了所有内容。Web 模块、Web 操作项、页面生成器和表格生成器，针对 CGI 和 DSO。你遇到过问题，并解决了它们或产生了通变方案。在此过程中，你编写了一些非常有用且强大的示例程序。

总而言之，我希望已经展示了 Kylix WebBroker 技术是互联网服务器端开发的一套强大工具。我将在日常工作以及我的网站 http://www.drbob42.com 上继续挑战 Web Modules 的极限。

# 符号

- `&` (ampersand) 字符 (C/C++), 63
- `@` (at) 字符在 Object Pascal 代码中, 63
- 在变量地址中, 87
- `^` (caret) 字符用于访问变量信息, 631
- 使用指针寻址内存, 632
- `$` (dollar) 字符，作为十六进制符号, 87
- `=` (equal) 字符，作为等号运算符, 86
- `/` (斜杠) 字符，作为除法运算符, 84-85
- `<` (小于) 字符，作为不等号运算符, 86
- `%` (百分比) 字符，在类搜索中, 739
- `+` (加) 字符用于字符串拼接, 85
- `;` (分号) 字符，在数据字段列表中, 693
- `_` (下划线) 字符，在类搜索中, 739

# A

- 抽象类
- 从...构建组件, 490
- 创建派类, 491
- `TComponent`, 491
- `TControl`, 493
- `TCustomControl`, 490, 493
- `TGraphicControl`, 491, 492
- `TWidgetControl`, 490

# 抽象数据类型

- 抽象数据类型, 725
- 声明抽象方法, 164-165, 使用, 160-163
- 抽象，核心类, 730-731
- 访问方法, 476
- 访问权限 (Linux), 641-642
- 访问权利 (Linux), 647
- 访问数据集 `TDataDataProvider` component, 697-698
- `TSQLClientDataSet` component, 698-699
- `TSQLMonitor`, 699
- 浮点类型的精度, 108, 119
- `ACTION` 参数 (CGI 表单), 820
- 操作，分配到数据模块, 776-778
- Actions 编辑器 (WebBroker 模块), 835-836
- Actions 属性 (`TWebmodule` component), 835
- Activate 按钮 (项目管理器)，查看, 226
- Active 属性 (`TClientDataSet` component), 691
- ActiveStatements (`TSQLConnection` component), 685
- Active_Genre (应用程序), 764-765
- Active_Parts (应用程序), 765
- AddIndex 方法 (`TClientDataSet` component), 693
- AddRef, 187-190 与 dbExpress 类, 750
- AddRef 目录, 189
- 地址邮件, 34-135 变量, `@` 87
- ADO (数据对象), Delphi 5, 683
- Afterinsert (模块), 771-772
- 聚合字段，与数据组件, 715-716
- C++ 中的算法, 218 命令行编译器
- 在 Form Designer 中对齐组件, 306
- Alt+F 键, 20
- Anchor 属性, 35-36，应用于按钮, 36
- `(+)` 运算符, 85
- 动物声音，添加到按钮, 140-141
- ANSI SQL, 92
- ANSI C++, 666
- ANSI Pascal, 到 Object Pascal, 98
- ANSI SQL, dbExpress 支持, 720
- ANSIString 类型 (Object Pascal), 114, 117
- 启用内存, 119 终止于 119
- 计数, 119-121 使用, 118
- Apache Web 服务器, 818 用于 CGI 应用, 820-826, 828
- 在 Kylix 中写入, 826 运行 WebApp2 服务器, 839-841
- 服务器应用程序, 833-834
- API 调用参数，查看列表, 247
- 应用程序, 310 添加自定义样式，在 Qt 程序中, 341
- 应用程序，添加到属性, 226
- ApplyUpdates (`TClientDataSet` component), 676, 694-695
- 架构 (`TCanvas` object), 536
- 伪 3D 引擎, 579-582
- 数组属性, 478
- ArrayProp 属性 (`TMMyProps` object), 487-488
- 简要映射, 911

## 数组

- 二进制文件 MyBase 格式, 675
- 数组常量, 127-128
- xfm 文件, 33
- 绑定记录缓冲区，声明, 126-127, 748-749
- 多维对象, 132-133
- Bitmap 属性 (`Tbrush`), 546
- 对象, 121
- Variant 过程, 204
- 添加到程序, 362-364
- as 运算符，带类型转换, 126
- 在组件面板上, 126
- 汇编语言，在创建图标时, 508
- Page, 509
- 单元过程, 118
- 使用 图形显示, 297
- 保存到, 534, 566-569
- 赋值运算符 (`=`), 84
- 黑盒代码，恐惧, 25
- 异步写入，每, 803
- 拷贝 (blitting), 535
- 移除显示, 299
- BlockRead/Write 函数 (Pascal), 636-637
- X/客户端服务器连接, 299
- 签签组件 (`TBookMarkList`)，添加到数据模块, 709-712
- 布尔操作，作为 Pascal, 99
- 布尔类型 (Object Pascal), 232-234
- BorderWidth 属性，带方法, 234-236
- TEFFancyClass 组件, 236-234
- 自动生成代码，自动实现, 506-508
- Avydia 方法，创建在, 232-234
- Borland Database Engine (BDE), 683, 718
- dbExpress 比较, 729-730
- .bash profile 脚本，与包运行, 392
- BASH 脚本，使用 `TFileStream` 类写入, 643
- BasicType 程序, 205-207
- BCD (二进制编码码), 108
- 处理过程，为, 109-110
- `Tbcd` 类型, 108
- 使用 BCD 类型, 110-114
- BcdAdd 过程, 114
- BcdCompare 过程, 110
- BcdMultiply 过程, 114
- BcdSubract 过程, 114
- BcdToCurr 过程, 110
- BcdToDouble 过程, 109
- BcdToInteger 过程, 110
- BcdToStr 过程, 109
- BCDVariant 程序，列表为, 110-114
- bin., 结束, 220
- ge.状态, 70
- beginTransaction() 方法 (`SQLConnection` 类), 751-752
- BeWidth 属性，与
- TEFFancyClass 组件, 506-508

# B

- 后置双缓冲使用, 584
- 在游戏引擎中, 583
- BaseForm (非矩形表单)，代码列表, 368-370
- 添加, 254
- 断点窗口 (调试工具), 243

# 简要映射,

