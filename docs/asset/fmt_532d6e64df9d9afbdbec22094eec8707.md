
## 错误处理示例

```
Error:
  If        (&ErrorFlag ) +
    Do
      SndPgmMsg MsgID( CPF9897 ) +
                MsgID( QSys/QCPFMsg ) +
                MsgData( 'Error in PrtObjAut. See joblog.' ) +
                MsgType( *Escape )
      MonMsg    ( CPF0000 MCH0000 ) Exec(
      Return
  EndDo
  ChgVar     (&ErrorFlag '1 ')

RcvMsg     MsgType( *Excp ) +
            MsgData(&MsgData ) +
            MsgID(&MsgID ) +
            MsgF( &MsgF ) +
            MsgFLIB(&MsgFLIB)

MonMsg     ( CPF0000 MCH0000 )

SndPgmMsg MsgID(&MsgID ) +
            MsgF( &MsgFLIB/&MsgF ) +
            MsgData(&MsgData ) +
            MsgType( *Escape )

MonMsg     ( CPF0000 MCH0000 )
```

### 图 26.3B 续

```
/* =========================================================== */
/* = 清理并退出程序                                     = */
/* =========================================================== */
```

#### Exit:

```
DltF          QTemp/ObjList
MonMsg        ( CPF0000 MCH0000 )
```

```
/* =========================================================== */
/* = 程序结束                                              = * */
/* =========================================================== */
```

`EndPgm`

# 第 27 章

## CL 程序与显示文件

在第 26 章中，我们讨论了如何使用 CL 程序处理数据库文件。我们讨论了声明文件、提取字段定义（包括外部描述的和程序描述的定义）以及处理数据库记录。在本章中，我们将讨论 CL 程序如何与显示文件配合工作。

对于某些需要显示的情况，CL 是一个合适的选择。例如，CL 与用于菜单显示文件配合得很好，因为在菜单环境中，CL 是覆盖文件、更改用户库列表、提交作业和检查权限最常用的语言。

CL 也是实现友好界面的流行选择，用户可以为用于打印报告或执行查询的程序输入参数。例如，CL 程序可以提供一个易于理解的面板，提示用户输入开始时间。

## 显示文件基础

对于显示文件，你必须使用 `Dcl` 命令来标识你想要处理的文件。`Dcl` 命令让编译器定位文件并获取字段定义。图 27.1 显示了用于显示文件的 DDS，图 27.2 显示了声明该显示文件的 CL 代码示例。

```
/* =========================================================== */
/* = 文件声明                                     = */
/* = 源类型... DDS                               = */
/* = 说明... 菜单文件                             * */
/* =========================================================== */
```

### IBM iSeries 和 AS/400 的 444 入始包

### 图 27.2

部分 CL 编译器列表

```
5769SS51 V4R4M0 990521 Control Language USER/MENU
Program                 : *USERMENU
Library                : QUSER
Source file             : *QLSRC
Library                : *USERMENU
Source member name     : USER/00
Source printing options : *SOURCE *XREF *GEN
Program generation options: *MLIST *XREF *NOPATCH
User profile            : *USER
Program logging        : *JOB
Allow CL command  : *YES
Replace program        : *YES
Target release         : V4R4M0
Authority              : *LIBERT
Sort sequence           : *MESK
Language identifier    : *JOB
Text                   Compiler               : IBM AS400 Control Language
SEQNR  *....1 +....2 +....3 +....4 +....5 +....6 +
100-/*= Program................=
200-/*= UserMenu =
300-/*= Description.. Sample CL program =
400-/*= =
500-/*= =
600-/*= Pgm =
700-/*= =
800-/*= File description =
900-/*= ====================
1000-/*= =
1100-/* File (UserMF)
1200-QUALIFIED FILE NAME - USER/USERMENU
RECORD FORMAT - MENU
CL VARIABLE  TYPE  LENGTH  PRECISION TEXT
$IN03         *L
OPTION        2
RECORD FORMAT - *MGSFL
CL VARIABLE  TYPE  LENGTH  PRECISION TEXT
$IN03         *L
MSGKEY       *CHAR        4
PGM          *CHAR        10
RECORD FORMAT - *MGSCTL
CL VARIABLE  TYPE  LENGTH  PRECISION TEXT
$IN03         *L
IN40                 1
RECORD FORMAT - PROMPT01
CL VARIABLE  TYPE  LENGTH  PRECISION TEXT
$IN03         *L
IN40                 1
PGM          *CHAR        10
IN12         *L
IN61         *L               Territory required.
IN62         *L               Invalid Territory ID.
IN63         *L               Sales Rep ID required.
IN64         *L               Invalid Sales Rep ID.
$TERRID      *CHAR        3
$SLSRPID     *CHAR        5
$BORDER       *CHAR        1
DETAIL        *CHAR        1
```

## CL 显示文件示例

让我们来看看如何将 CL 与显示文件结合用于菜单和提示屏幕。图 27.3 显示了基于图 27.1（第 441 页）中 DDS 的一个菜单。

### 图 27.3

示例用户菜单

![](img/8569750eb3981f40e8553bc6a297aaf_487_0.png)

从 DDS 中，你可以看到记录格式 `Menu` 显示菜单选项列表，而记录格式 `MsgSfl` 和 `MsgCt` 控制将消息发送到程序消息队列的消息子文件。记录格式 `Prompt01` 是一个面板，允许用户为“批报告 1”输入选择值。
