
/* ======================== */

/* 命令....... RtvIPAddr         = *

/* 描述... 获取设备 IP 地址 = *

/*                                              *

/* CrtCmd Cmd( YourLib/RtvIPAddr ) + * *

/* Pgm( YourLib/RtvIPAddrC )      + *

/* Allow(*IPgm *IMod *IRex )      + *

/* ======================== */

Cmd

    Prompt( 'Retrieve IP Address' )

    Parm

        Kwd( Dev ) +

        Type(* Name ) +

        Len( 10 ) +

        Dft( *Requester ) +

        SpCVal( *Requester ) +

        Expr( *Yes ) +

        Prompt( 'Device' )\)

    Parm

        Kwd( IPAddr ) +

        Type(* Char ) +

        Len( 15 ) +

        RtnVal( *Yes ) +

        Prompt( 'CL Var for IPADDR )               (15) )

```
## 图 25.4C
RtvIPAddr 命令处理程序 RtvIPAddrC
```

/* ======================== */

/* 程序....... RtvIPAddrC          = *

/* 描述... 获取设备 IP 地址 = *

/*                                              *

/* CrtCLPgm Pgm( YourLib/RtvIPAddrC )   = *

/* SrcFile YourLib/YourSrcF )          = *

/* ======================== */

(

Pgm                                     +

    &Dev                                +

    &IPAddr                             +

)

/* - 变量声明             */

Dcl    &Dev             *Char ( 10 ) )

Dcl    &IPAddr         *Char ( 15 ) )

Dcl    &RcvVar      *Char ( 892 ) )

Dcl    &RcvVarLen  *Char ( 4 ) )

Dcl    &RcvVar      *Char ( 8 ) )

```
## 414 IBM iSeries 和 AS/400 启动包

图 25.4C 继续
```

Dcl &APIError *Char ( 8 )

nDcl &AEBytesPrv *Char ( 4 )

nDcl &NoIPAddr *Char ( 15 )

nDcl &MsgID *Char ( 7 )

nDcl &MsgData *Char ( 256 )

nDcl &Msgf *Char ( 10 )

nDcl &MsgFLib *Char ( 10 )
```

```
/*

/*

全局错误捕获

/*

/*

```
```

MonMsg ( CPF0000 MCH0000 ) Exec(

Goto Error )

```
```

/*

/*

初始化信息

/*

/*

```
```

ChgVar &NoIPAddr ( X'00000000000000000000000000000000' )

ChgVar &Format ( 'DEVED0600' )

ChgVar %Bin( &RcvVarLen ( 892 )

ChgVar %Bin( &AEBytesPrv ( 0 )
```

```
/*

/*

如有必要，获取当前设备名称

/*

/*

```
```

If ( &Dev *Eq '*REQUESTER' )

RtvJobA Job( &Dev )
```

```
/*

/*

获取点分 IP 地址

/*

/*

```
```

ChgVar %XSst( &APIError 1 4 ) ( &AEBytesPrv )

Call

QCDRDBevD

( &RcvVar

&RcvVar

&Format

&Dev

&APIError )
```

```

ChgVar &IPAddr ( %XSst( &RcvVar 878 15 ) )

If

( &IPAddr *Eq &NoIPAddr ) *Or

( &IPAddr *Eq ' ' )

&IPAddr ( '*None' )
```

```

Return
```

## 第 25 章 使用 API 扩展 CL 的范围 415

## 图 25.4C 继续
```

/* --------------------------------------------------------------------*

/* - 错误处理程序（将错误消息传递给调用者） - */

/* --------------------------------------------------------------------*/

Error:
```
RcvMsg          MsgType(*Excp) +
Rmv(* Yes) +
MsgDta(&MsgDta ) +
MsgID(&MsgID ) +
MsgF(&MsgF ) +
MsgFLib(&MsgFLib ) +
MonMsg          ( CPF0000 MCH0000 )

SndPgmMsg      MsgID(&MsgID ) +
MsgF(&MsgFLib/&MsgF ) +
MsgDta(&MsgDta ) +
MsgType(*Escape ) +
MonMsg          ( CPF0000 MCH0000 )
```

首先，注意程序变量声明中 API 错误结构变量 `&APIError` 的定义。我们定义此结构以使用全局错误处理器来捕获任何长度为八字节的错误，因为错误可能会发生并传递回调用程序。

在初始化部分，我们将变量 `&NoIPAddr` 的值设置为十六进制字符串，对于当前未使用 IP 地址的适用设备，API `QCDDevD` 会返回该值。注意，我们还将提供的（Provided）子字段 `&AEBytesPrv` 设置为 0（零），表示 API 在遇到错误时将抛出异常。当特殊值为 `*Requester` 时，程序继续获取当前设备名称。

在调用 API 之前，程序通过将提供的值放在前四个字节来构造 API 错误结构变量。然后程序调用 API `QCDDevD` 获取所选设备的 IP 地址。如果 API 遇到错误，控制将传递给全局错误处理器，它接收异常并将其传递回调用程序。如果没有发生错误，程序继续从 API 返回信息的第 878-892 字节处提取 IP 地址值。如果返回的 IP 地址字符串为空，程序将将 IP 地址返回为 `*None`。

一个可以充分利用 `RtIPAddr` 命令的需求是：使用 `RunRmtCmdd`（运行远程命令）在具有 TCP/IP 地址的 PC 上启动程序。你通过在 `RunRmtCmdd` 的参数中指定 PC 的 IP 地址，来指定该命令适用的 PC。

![](img/85697eb97553456a828183553f0.png)

## 460

## 460

# 显示地址

有时，操作人员可能需要知道与一个或多个设备关联的 IP 地址，以便诊断和解决问题。`RtIPAddr` 命令可以满足此类需求。

图 25.4C 继续

图 25.4A 显示了示例：

| 设备 | IP 地址 |
|---|---|
| AS400 | 192.168.0.1 |
| TCP | 192.168.0.2 |
| QCONSOLE | 192.168.0.3 |
| QADISP | 192.168.0.4 |
| QTIDA | 192.168.0.5 |
| TAP01 | 192.168.0.6 |
| F001 | |

## 461

注意输出跨越了两个屏幕。信不信，，输出是一个由 CL 程序加载并显示的子标题。让我们看看 `DspAddr` 如何利用一种方便的技术在子文件（subfile）中显示来自 `RIPAddr` 的输出。

图 25.5B 显示了文件 `DspAddr` 的源码。`DspAddr` 使用该显示文件来显示检索到的 IP 地址（如图 25.5A 所示）。

## 图 25.5B
