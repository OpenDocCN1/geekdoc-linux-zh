
==================================================================

nRtvJobA   Type(&Type                                     +

          &SbmMsgQ(&SbmMsgQ)                            +

          &SbmMsgQLib(&SbmMsgQLib)                      n

.

==================================================================

/* =                                                                    = *

/* = Send message to external user or submitter         = *

==================================================================

/* =                                                                    = *

/* = If job is running in batch, send the message to the - = *

/*   message queue retrieved from job attributes          - = *

If       (&Type *Eq '0')                                   +

         SndUsrMsg  Msg('The daily report is available for printing.') +

           MsgType(&Info)                                 +

           ToMsg(&SbmMsgQLib/SbmMsgQ)

```
## 图 29.2 续
```

/* ------------------------------------------------------ */

/* If job is running in batch, send the message to the - */

/* message queue retrieved from job attributes          - */

/* *Requester                                            */

If ( &Type*Eq '1' ) +

    SndUsrMsg Msg('The daily report is available for printing.') +

    MsgType('Info') +

    To(*Requester)

/* ====================================================== */

/* End of program                                                      */

```
EndPgm

IBM iSeries 和 AS/400 470 入门工具包

## 图 29.3
使用 SndUsrMsg 的示例 CL 程序

```
/* ================================================== */
/* = 程序....... MsgSample2             = */
/* = 源类型... CLP                            = */
/* = 描述... SndUsrMsg 演示      = */
/* ================================================== */
```

```
Pgm
/* ================================================== */
/* = 变量声明                        = */
/* ================================================== */
```

```
Dcl         &Reply      *Char      ( 1 )
Dcl         &DailySts   *Char      ( 1 )
```

```
/* ================================================== */
/* = 获取每日报告状态               = */
/* ================================================== */
```

```
RtvDtaAara  DtaAra( DailyLib/DailyRpt )
            RtnVar(&DailySts )
```

```
/* ================================================== */
/* = 如果每日报告已运行，提示用户验证     = */
/* = 是否应该再次执行每日报告             = */
/* ================================================== */
```

```
If
    (&DailySts *Eq 'Y' )
    Do
```

```
SendMsg:
    SndUsrMsg Msg('今日已运行每日报告。' +
               &Clat +
               '是否再次运行？(Y,N)' +
               Values('Y' 'N') +
               Dft('N') +
               MsgType(*Inq +
               ToUsr(*Requester) +
               MsgRpy(&Reply )
```

```
If
    (&Reply *Eq 'Y' )
    Goto
        RunRpt
```

```
If
    (&Reply *Eq 'N' )
    Goto
        CnlRpt
```

```
GoTo
    SendMsg
EndDo
```

## 第 29 章 程序会对话 471

# 图 29.3 继续

```
/* ========================================== */
/* /* 运行报告 = * */
/* /* ========================================== */
```

RunRpt:

```
Call            DlyRpt
SndUsrMsg Msg('每日报告已可以打印。')  +
                 MsgType(* Info )  +
                 ToUsr(*Requester )
                 End
```

GoTo

```
/* ========================================== */
/* /* 取消报告 = * */
/* /* ========================================== */
```

CnlRpt:

```
SndUsrMsg Msg('每日报告请求已取消。')  +
                 MsgType(* Info )  +
                 ToUsr(*Requester )
```

```
/* ========================================== */
/* /* = 程序结束 = * */
/* /* ========================================== */
```
