
# 用于 IBM iSeries 和 AS/400 的 198 入门套件

# 图 11.8D 续

```
ChVar   &Msg      ( '输出队列监控'

                  *BCat

                  &MonName

                  *BCat

                  '在库中不存在'

                  *BCat

                  &PrDlib

                  *TCat )

    Goto SendError

EndDo
```

/* =========================================================== */
/* = 退出                                                  */
/* =========================================================== */

Return

/* =========================================================== */
/* = 错误处理                                 */
/* =========================================================== */

Error:

RcvMsg     MsgType( *Excp ) +
           MsgData(&MsgData ) +
           MsgID(&MsgID ) +
           MsgF(&MsgF ) +
           MsgIB(&MsgIB )

SndPgm     MsgID( CPF0000 ) +
           MsgF( QSYS/ ) +
           MsgData(&MsgData ) +
           Type( *Incomp )

/* =========================================================== */

SendError:

SndPgm     MsgID( CPF98 ) +
           MsgF( QSYS/ ) +
           MsgData( '输出队列监控'
                  &MonName
                  '已删除'
                  &PrDlib )
           Type( *Comp )

/* =========================================================== */

# 用于 IBM iSeries 和 AS/400 的 198 入门套件

# 图 11.8D 续

```
/* ============================================ */
/* / = 错误处理器 =========================== + */
/* / = ============================================ */
Error:
  RcvMsg      MsgType( *Excp )                                 +
             MsgData( &Msgbda ))
             MsgID( &MsgbID )                                    +
             Msf( &Msf )
             MsfLib( &MsfLib )
  MonMsg      ( CPF00000 MCH0000 )
  SndPgmMsg   MsgID( &MsgbID )                                  +
             Msf( &MsfLib/&Msf )                                 +
             MsgData( &Msgbda )                                    +
             ToPgmQ( *Same )
             KeyVar( &KeyVar )
  MonMsg      ( CPF00000 MCH0000 )
  RcvMsg      KeyVar( &KeyVar )                                 +
             Msg( &Msg )
  MonMsg      ( CPF00000 MCH0000 )
  SendError:
  SndPgmMsg   MsgID( CPF00006 )                                 +
             MsgFc( Qsys/QCPFFMsg )                             +
             MsgIat( (D0000 ) *Tcat &Msg )                        +
             ToPgmQ( *Prv )
             MsgType( *Diag )
  MonMsg      ( CPF00000 MCH0000 )
  SndPgmMsg   MsgID( CPF00002 )                                 +
             MsgF( Qsys/QCPFFMsg )                             +
             ToPgmQ( *Prv )                                       +
             MsgType( *Escape )
  MonMsg      ( CPF00000 MCH0000 )
/* ============================================ = */
/* / = 程序结束 ======================== + */
/* / = ============================================ = */
EndPgm
```

第 11 章 即插即用输出队列监控器 199

# 图 11.9A

StrOutQMon 面板

![](img/8569750eb3981f40e85535bc6a297aaf_243_0.png)

# 图 11.9B

StrOutQMon 命令

```
/* ========================== */
/* 命令........... StrOutQMon = */
/* 源类型...... CMD = */
/* 描述... 启动输出队列监控器 = */
/* CPP...............StrOutQMon1A = */
/* VCP...............StrOutQMon2A = */
/* ========================== */
Cmd 'Start Output Queue Monitor ' )
  Parm Kwd( Monhname ) +
      Type( Name ) +
      Len( 10 ) +
      Min( 1 ) +
      Prompt( 'Monitor name' )
```

# 用于 IBM iSeries 和 AS/400 的 200 入门套件

图 11.9C

StrOutQMon 命令处理程序 StrOutQM1A
