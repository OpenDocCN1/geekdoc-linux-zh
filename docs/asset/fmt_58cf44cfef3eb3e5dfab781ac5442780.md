
# 178 IBM iSeries 和 AS/400 启动工具包

## FIGURE 11.6D

```
AddOutQME 命令处理程序 AddOutQM1B — 添加控制记录
===========================================
* 程序.......AddOutQM1B               =
* 源类型....      RPGLE                            =
* 描述....AddOut 监控项 — 添加控制记录 =
===========================================
FOutQMonE U F A E               K Disk
===========================================
*               输入参数                       =
===========================================
D EntryParms...    PR               ExtPgm( 'ADDOUTQM1B' )
D                                 10
D                                 10
D EntryParms...    PI
D OutQName                        10
D OutQLib                         10
D MonName                         10
===========================================
*               键列表                                =
```

```
MonMsg    ( CPF0000 MCH0000 ) Exec(
Goto      Error
)
/* = 获取产品库名称 **/
/* ============================================ **/
Call      QUsrJob(
               &RcvVar
               &RcvVarLen
               &Format
               &QualJob
               &IntJobID
               )
ChgVar    &Nbr4      ( %Bin(&RcvVar 65 ))
ChgVar    &Offset    ( &Nbr4 * 11 ) + 81 )
ChgVar    &PrdlLib   ( %Sst(&RcvVar &Offset 10 ) )
/* = 验证输出队列监控程序是否存在 **/
/* ============================================ **/
ChkObj    Obj(&PrdlLib&MonName)
               ObjType(*Pgm )
MonMsg    ( CPF0801 ) Exec(
Do
               ChgVar    &Msg1     ( 'Output queue monitor program'
                                     *BCat
                                     &MonName
                                     *BCat
                                     'does not exist in Library'
                                     *BCat
                                     &PrdlLib
                                     *TCat
Goto      SendError
                               .')
EndDo
/* ============================================ */
/* = 验证输出队列监控数据队列不存在 = */
ChkObj       ObjObj(&Prdlib&MonName )
               ObjType(*Dtak)
MonMsg          ( CPF9801 ) Exec(
               Return
)
/* ============================================ */
/* = 输出队列监控数据队列已存在 = */
/* ============================================ */
ChgVar       &Msg               ( 'Output queue monitor' +
                              *BCat +
                              *MonName +
                              *BCat +
                              'already exists' +
                              *TCat +
                              '.')
GoTo         SendError
/* ============================================ */
/* = 错误处理器 ===================================== = */
/* ============================================ */
Error:
RcvMsg       MsgType(*Excp ) +
               MsgDta(&Msgta ) +
               MsgID(&MsgID ) +
               Msgf(*Msg ) +
               MsgFLib(&MsgLib) +
MonMsg        ( CPF00000 MCH0000 )
ndPgmMsg    MsgID(&MsgID ) +
               Msgf(&MsgLib&SGF) +
               MsgDta(&Msgta ) +
               ToPgmd(*Same) +
               KeyVar(&KeyVar) +
MonMsg        ( CPF00000 MCH0000 )
RcvMsg       KeyVar(&KeyVar ) +
               Msg(&Msg)
MonMsg        ( CPF00000 MCH0000 )
SendError:
ndPgmMsg    MsgID(CPF00006 Msg) +
               MsgF( QSYS*/QCPMFsg ) +
               MsgDta('*0000'*TCat &Msg ) +
               ToPgmd(*Prv) +
               MsgType(*Diag )
MonMsg        ( CPF00000 MCH0000 )
SndPgmMsg MsgID( CPF0002 )               +
             MsgF( QSYS/QCPMFsg ) +
             ToPgmQC(* Prv )                     +
             MsgType( *Escape )
MonMsg                  ( CPF00000 )               */
/* ===================================================================== = */
/* = 程序结束                                                             = */
/* ===================================================================== = */
EndPgm
```
