
```
MonMsg ( CPF2625 ) Exec(
  Do
  RcvMsg    MsgType(*Xcep )
  Rmv( *Yes )
  ChgVar    %Sst(&IPAddrInfo 13 48 )
            ( 'Cannot allocate device description ' )\)
EndDo
```

```
MonMsg ( CPF2634 ) Exec(
  Do
  RcvMsg    MsgType(*Xcep )
  Rmv( *Yes )
  ChgVar    %Sst(&IPAddrInfo 13 48 )
            ( 'Not authorized to device description ' )\)
EndDo
```

```
MonMsg ( CPF2702 ) Exec(
  Do
  RcvMsg    MsgType(*Xcep )
  Rmv( *Yes )
  ChgVar    %Sst(&IPAddrInfo 13 48 )
            ( 'Incompatible device category ' )\)
EndDo
```

```
MonMsg ( CPF8105 ) Exec(
  Do
  RcvMsg    MsgType(*Xcep )
  Rmv( *Yes )
  ChgVar    %Sst(&IPAddrInfo 13 48 )
            ( 'Device description damaged ' )\)
EndDo
```

```
If ( %Sst(&IPAddrInfo 13 48 ) *Eq ' ' )
ChgVar %Sst(&IPAddrInfo 13 48 ) ( (&IPAddr
```

```
SndPgmMsg MsgID(CPF9897 )
  MsgF(QSys/QCPFMSg )
  MsgData(&IPAddrInfo )
  TopPgm(*Same * )
  MsgType(*INFO )
```

```
Goto Loop01
```

继续

## 第 25 章：通过 API 扩展 CL 的范围 425

## 图 25.5F 继续

```
/* ======================================================== */
/* /* = 显示 IP 地址                             = */
/* /* ======================================================== * */
```

DspInfo:

```
ChgVar &In99 ('1' )
nsndF RcdFmt( MsgCtl )
nsndF RcdFmt( DspHdg )
nsndRcvF RcdFmt( DspFtr ) +
If (&In03 *NE '1') +
   GoTo DspInfo
```

```
/* ======================================================== * */
/* /* = 退出                                              = */
/* /* ======================================================== * */
```

Return

```
/* ======================================================== * */
/* /* = 错误处理程序                                     = */
/* = ======================================================== * */
```

Error:

```
RcvMsg MsgType( *Excp ) +
   MsgData(&MsgData ) +
   MsgID(&MsgID ) +
   MsgF(&MsgF ) +
   MsgFLib(&MsgFLib ) +
MonMsg ( CPF00000 MCH0000 )
```

```
SndPgmMsg MsgID(&MsgID ) +
   MsgF(&MsgFLib/MsgF) +
   MsgData(&MsgData ) +
   MsgType(*Escape ) +
MonMsg ( CPF00000 MCH0000 )
```

```
/* ======================================================== * */
/* /* = 程序结束                                         = */
/* /* = ======================================================== * */
```

EndPgm

`DspIpAddrC` 开始初始化显示文件字段 (`&DspQm`)，该字段用于标识调用消息队列，该队列指示消息字幕文件使用程序自身的调用消息队列。

接下来，`DspIpAddr` 处理选定的设备列表。对于列表中的每个项目，程序都会将包含设备名称以及检索到的 IP 地址信息的消息发送到其调用消息队列中。当然，这会导致信息在消息字幕中显示。程序会构建变量 `&IPAddrInfo`。请注意，在执行 `RtvIpAddr` 之前，程序会用设备名称初始化变量 `&IPAddrInfo`。`DspIPAddrC` 根据尝试检索设备 IP 地址的结果向此信息中添加内容。

`DspIPAddrC` 显式地监控 `RtvIPAddr` 可能引起的五种可能异常中的五种。这使得程序能够定制其发送到调用消息队列以进行显示的内容。如果 `RtvIPAddr` 出除了监控之外的任何异常，全局错误处理程序将接收控制权。在几个 `MonMsg` 语句之后，程序检查变量 `&IPAddrInfo` 以确定其是否包含错误信息。如果不包含，则发生错误，程序会将检索到的 IP 地址添加到变量中。最后，`DspIpAddrC` 将其在变量 `&IPAddrInfo` 中构建的消息发送到其调用消息队列进行显示。

一旦程序完成对整个选定设备列表的处理，将通过设置控制指示 `99` 的值并写入显示文件中的记录格式来显示结果。程序写入记录格式的顺序对于确保所有信息的正确显示以及功能键 `F3` 的激活状态至关重要。

## 第 26 章 CL 程序与数据库文件 429

你的程序随后可以使用这些变量，尽管它们没有被显式声明。例如，你可以在程序中包含以下语句：

```cl
If      (*Code *Eq 'A') *And +
        (&&Number *GT 10)) +
        ChgVar  &Code ('B')
```

注意，当你在程序中引用文件时，必须在字段名前前加上 ampersand (`&`)。所有的 CL 变量，包括使用 `DCl` 命令隐式定义的变量以及文件字段定义的变量，在程序中引用时都需要加上 `&` 前缀。

那么程序描述的文件——即不包含外部数据的文件又是如何呢？

假设你使用 `CrtPF`（创建物理文件）命令创建了以下内容：

`CrtPF File(DiskFile)(258)`

并在程序中声明文件 `DiskFile`。与处理外部定义文件一样，CL 编译器会自动提供对程序描述文件的访问。由于没有外部定义的记录格式，编译器会将文件中的每个记录识别为由单个字段组成。该字段始终命名为 `&FileName`，其中 `FileName` 是文件的名称。因此，如果你编写代码为：

`# DCl DiskFile`

你的 CL 程序将识别出一个字段 `&DiskFile`，其长度等于于 `DiskFile` 的记录长度。然后你可以在每次需要操作时提取子字段。在 CL 中，你使用内置函数 `%Sst`（或 `%Substring`）来提取字段。以下语句：

```cl
ChgVar &Field1(%Sst(&DiskFile 1 10))
ChgVar &Field2(%Sst(&DiskFile 11 25))
ChgVar &Field3(%Sst(&DiskFile 50 1))
```

从 `&DiskFile` 单字段中提取了三个子字段。

在使用程序描述的文件时，你需要记住两个规则。首先，每次从文件中读取记录时，都必须提取子字段。与 RPG 不同，CL 没有可以应用于每次读取的全局数据结构概念。在每次读取循环周期中，你都必须使用 `%Sst` 函数来检索子字段。

其次，`%Sst` 函数仅用于字符数据。如果某个位置范围包含数字型数据，你必须将该数据作为字符字段检索，然后将其移动到数字型字段中。你可以使用 `ChgVar`（更改变量）将字符数据移动到数字型字段。你还必须确保变量的类型与你提取的数据类型匹配。

假设 `DiskFile` 中的第 251–258 位包含一个长度为八位的数字数据字段。要将该数据提取到数字型 CL 文件中需要以下 `DCl` 语句和操作：
