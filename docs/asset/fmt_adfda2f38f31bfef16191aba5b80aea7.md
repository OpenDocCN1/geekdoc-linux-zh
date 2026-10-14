
```
****************************************************************************
* 输入参数
****************************************************************************
D EntryParms...
D                    PR               ExtPgm( 'ADDOUTQMBB' )
D                               10
D                               10
D                               10
D EntryParms...
D                    PI               10
OutQName                        10
OutQLib                          10
NameIn                          10
OtherMon
```

****************************************************************************

* 键列表

****************************************************************************

C Key                   KList

C OutQLib

C OutQName

# 第 11 章 随插即用输出队列监控

## 图 11.6F 继续

```
****************===========================================
* 读取并判断输出队列是否被
* 另一个监控程序监控 =
****************============================================
C  Key               Chain               OutQMOn
C  If                Found ) and
C                  MonName <> MonName
C  Eval              OtherMon = *Mon
C  Else              OtherMon = *Blank
C  Eval               EndIf
```

************************************************===========

* 退出程序

*============================================

## 图 11.7A RmvOutQM 面板

![](img/856975eb3981f40e853bc0a227.png)

# IBM iSeries 和 AS/400 184 入门套件

## 图 11.7B 命令 RmvOutQ

```
/* =================RmvOutQ = */
* 命令.......RmvOutQ =
* 源代码类型... CMD =
* 描述... 移除输出队列监控项 =
* CPP...........RmvQM1A =
* VCP...........RmvQM2A =
=================================
Cmd               Prompt(' 删除输出队列监控项' ')
Parm               Kwd( MonName)
Type(* Name)
Len( 10 )
Min( 1 )
Prompt(' 监控名称 ')
Parm               Kwd( OutQ)
Type(* QualOut)
Min( 1 )
Max( 25 )
SngVal(( *ALL ))
Prompt( ' 输出队列 ')
QualOutQ:        Qual(* Name)
Len( 10 )
Qual(* Name)
Len( 10 )
DftC(( *Lib ))
SpcVal(( *Lib
(*CurLib ))
Prompt(' 库 ))
```

# 图 11.7C RmvOutQM 命令处理程序 RmvQM1A

```
/* ================================================= */
* 程序.......RmvQM1A =
* 源代码类型... LNSE =
* 类型.......RmvOutQM 的命令处理程序 =
* 描述... 移除输出队列监控项 =
* 参数 =
* &MonName 输入监控名称 =
* &Outq 输入多达 25 个输出队列名称列表 = */
=================================
Pgm               (
                  &MonName
                  &Outq
                  )

/* ================================================= */
* 变量声明 ===================================
Dcl               &MonName      *char( 10 )
Dcl               &Outq         *char( 25 )
Dcl               &OutQName     *char( 10 )
Dcl               &OutQLib*char( 10 )
```

# 第 11 章 随插即用输出队列监控

## 图 11.7C 继续

```
Dcl               $OutCount      *char( 2 )
Dcl               $OutCountN     *Dec( 2 )
Dcl               $LoopCount     *Dec( 3 )
Dcl               $Offset        *Dec( 0 )
Dcl               $RcvVar        *char( 60 )
Dcl               $RcvLen         *char( 4 )
Dcl               $Format        *char( 'X00025' )
Dcl               $QuaJob        *char( 'JOB100' )
Dcl               $IntJobID      *char( 26 )
Dcl               $PrdLib        *char( 16 )
Dcl               $MsgId         *Dec( 10 )
Dcl               $Msgf          *char( 4 )
Dcl               $MsgfLiba     *char( 10 )
Dcl               $MsgfLibta     *char( 10 )
```

```
/* ================================================= */
/ 全局错误监控                                    
/* ================================================= */
```

MonMsg          ( CPF0000 MCH0000 ) Exec(

Goto                Error )

```

```

/* ================================================= */

/ 获取库名                                        

/* ================================================= */

```

```

Call            QUsr                               +

                (                                     

                &RcvVar                               +

                &RcvLen                               +

                &Format                               +

                &QuaJob                               +
