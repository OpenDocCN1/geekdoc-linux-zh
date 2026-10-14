
# IBM iSeries 和 AS/400 启动包

## EndOutQM1A 命令处理程序

``` 
/* ==================EndOutQMon 命令处理程序 EndOutQM1A =// */
/* = 程序.......EndOutQM1A                               = */
/* = 源类型......CLLE                                     = */
/* = 类型...........EndOutQMon 的命令处理程序         = */
/* = 描述...结束输出队列监控                   = */
/*                                                                           */
/* = 参数                                              = */
/* = &MonName           输入监控器名称                = */
/*                                                                           */

Pgm                                                          +
  &MonName                                                   +
)

/* ===================变量声明 ================== */
Dcl &MonName      *Char (10)
Dcl &RcvVar       *Char (600)
Dcl &RcvVarLen   *Char (4)      ('*X0000258')
Dcl &QualJob     *Char (26)      ('*J0B1070D')
Dcl &IntJobID    *Char (16)
Dcl &Sffset       *Dec (4)
Dcl &Nbr4         *Dec (4)
Dcl &Data         *Dec (12)
Dcl &Dataelen      **Dec (5)      *128)
Dcl &MsgID        *Char (10)
Dcl &Msgta        *Char (7)
Dcl &Msgf        *Char (10)
Dcl &MsgLib       *Char (10)

/* ===================全局错误监控 == */
/* = 全局错误监控                               = */
MonMsg (CPF0000 MCH0000) Exec(+
    Goto               Error      )

/* ==================检索库名 == */
/* = 检索库名                          = */

Call              QUsr                                     
  &RcvVar                                                     
  &RcvVarLen                                                  
  &Format                                                     
  &QualJob                                                    
  &IntJobID                                                   
)
ChgVar &Nbr4             ((%Bin(&RcvVar 65)))
ChgVar &Offset                                 ((&Nbr4 11))
ChgVar &PrdLib                               (%Sst(&RcvVar&Offset))
```

图 11.10C 续

``` 
/* ============================================ */

/* = 发送结束监控                    */

/* ============================================ */

Call       QUsr                             +

           &MonName                               +

               &PrdLib                               +

               &Data                               +

           )

/* ============================================ */

/* = 发送完成消息                           */

/* ============================================ */

SndPgmMsg MsgID(CPF8998) +

           Msgf(QSys/QCPFMsg) +

           MsgData('输出队列监控' *BCat +

                  &MonName +

                  *BCat +

                  '已结束') +

           MsgType(*Comp)

```

EndPgm

# 第11章 即插即用输出队列监控器 207

图 11.10D

``` 
/* ============================================*/

/* = 有效性检查程序 EndQM2A */

/* = 程序.......EndQM2A                               = */

/* = 源类型....CLE                               = */

/* = 类型...........EndOutQMon 的有效性检查程序 = */

/* = 描述...结束输出队列监控                   = */

/* =                                            */

/* = 参数                                              = */

/* = &MonName         监控名称                         */

/* ============================================*/

Pgm                                                          +

  &MonName                                                   +

)

/* ===================变量声明 ================== */

Dcl &MonName      *Char (10)

Dcl &RcvVar       *Char (600)

Dcl &RcvVarLen   *Char (4)      ('*X0000258')

Dcl &QualJob     *Char (26)      ('*J0B1070D')

Dcl &IntJobID    *Char (16)

Dcl &Sffset       *Dec (4)

Dcl &Nbr4         *Dec (4)

Dcl &Data         *Dec (12)

Dcl &Dataelen      *Dec (5)      (128)

Dcl &MsgID        *Char (10)

Dcl &Msgta        *Char (7)

Dcl &Msgf         *Char (10)

Dcl &MsgLib       *Char (10)

/* ===================全局错误监控 == */

/* = 全局错误监控                               = */

MonMsg (CPF0000 MCH0000) Exec(+

    Goto               Error      )
```
