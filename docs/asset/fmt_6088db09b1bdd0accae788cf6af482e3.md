
# 用于 IBM iSeries 和 AS/400 的 202 入门套件

# 图 11.9D 续

```
/* ========================================================== */
/* = 程序......      StOutQMon                          */
/* = 源......      CLE                                = */
/* = 类型........      StOutQMon 的有效检查程序  = */
/* = 描述... 启动输出队列监控器              = */
/* = 参数                                        = */
/* ========================================================== */
```

```
/* ========================================================== */
/* = &MonName         输入 监控器名称                   = */
/* ========================================================== = */
```

```
Pgm      (                                           
            &MonName                                             
                     )
```

```
/* = 变量声明 */
/* ============================================================ */
Dcl      &MonName   *Char ( 10 )
Dcl      &RcvVar    *Char ( 600 )
Dcl      &RcvVarLen  *Char ( 4 )       ( 'X0000258' )
Dcl      &Format     *Char ( 8 )       ( 'JOB0I700' )
Dcl      &QualJob   *Char ( 26 )       ( ' ' )
Dcl      &IntJobID   *Char ( 16 )
Dcl      &PrdSlib   *Char ( 10 )
Dcl      &Nbr4      *Dec ( 4 )
Dcl      &MsMsg       *Char ( 512 )
Dcl      &MsgID     *Char ( 7 )
Dcl      &MsgData    *Char ( 100 )
Dcl      &MsgLib    *Char ( 10 )
Dcl      &KeyVar     *Char ( 4 )
```

```
/* = 全局错误监控 */
/* ============================================================ */
MonMsg      ( CP00000 MCH0000 ) Exec(c)
Goto           Error                                 )
```

```
/* = 检索产品库名 */
/* ============================================================ */
Call         QUsrJobI(
               &RcvVar
               &RcvVarLen
               &Format
               &QualJob
               &IntJobID
                                            )
```

```
ChgVar       &Nbr4       ( %Bin(&RcvVar)65 4 ) )
ChgVar       &Offset     ( &Nbr4 * 11 ) + 81 )
ChgVar       &PrdLib     ( %Sst(&RcvVar) 10 ) )
```

```
/* = 验证输出队列监控器数据队列是否存在 */
/* ============================================================ */
ChkObj       Obj(&PrdlLib/&MonName )
               ObjType(*Daq )
```

```
MonMsg       ( CPF9801 ) Exec(c)
Do             ( 'Output queue monitor'
               ChgVar     &MsMsg
                          *BCat
                          *BCat
                          &MonName
                          *BCat
                          'does not exist in library'
                          *BCat
                          &PrdLib
                          *TCat
                               )
Goto           SError
EndDo
```

# 第11章 即插即用输出队列监控器 203

图 11.9D 续
