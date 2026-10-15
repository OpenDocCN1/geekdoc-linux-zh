
********************************************************************

/* 5769SS1 V4R4M0 990521      RTVCLSRC 输出      07/13/00 10:42:48 */

/* 程序名                        : QSTRUP             PN* */
/* 库名                            : QSYS               PL* */
/* 原始源文件                     :                    SN* */
/* 库名                            :                    SL* */
/* 原始源成员                     :                    SM* */
/* 源文件更改                     :                    SC* */
/* 日期/时间                       :                    *NOPATCH  PO* */
/* 配置文件                         :                    *USER     UP* */
/* 文本                            :                    TY* */
/* 所有者                         :                    OW* */
/* 补丁更改 ID                   :                    QSYS   PC* */
/* 补丁 APAR ID                   :                    PA* */
/* 用户修改标志                   :                    *NO      UM* */

********************************************************************

```
PGM

  CL VAR(&STRWTRS) TYPE(CHAR) LEN(1)

  CL VAR(&CTLSBSD) SBSD(CHAR) LEN(20)

  CL VAR(&CTPYR) TYPE(CHAR) LEN(90) VALUE('5769-SS1 (C) COPYRIGHT-
  \000IBM CORP 1980, 1999. LICENSED MATERIAL - PROGRAM PROPERTY OF IBM')

  QSYS/STRBS SBSD(QSPL)

  MONMSG MGID(CPF0000)

  QSYS/STRBS SBSD(QSERVER)

  MONMSG MGID(CPF0000)

  QSYS/STRBS SBSD(QSURWRK)

  MONMSG MGID(CPF0000)

  QSYS/RLSJBOQ JBQ4(QPL/QS36MRT)

  MONMSG MGID(CPF0000)

  QSYS/RLSJBOQ JBQJ(QPL/QS36EVOKE)

  MONMSG MGID(CPF0000)

  QSYS/STRCNUP

  MONMSG MGID(CPF0000)

  QSYS/RTVSYSVAL SYSVAL(&CTLSBSD) RTVNVAR(&CTLSBSD)

  IF COND (&CTLSBSD = *NE 'QCTL') : QSYS') AND (&CTLSBSD NE-
  'QCTL' : QGPL) THEN (GOTO CMDMLB(DONE))

  QGPL

  QSYS/STRBS SBSD(QINTER)

  MONMSG MGID(CPF0000)

  QSYS/STRBS SBSD(QBATCH)

  MONMSG MGID(CPF0000)

  QSYS/STRBS SBSD(QCMNN)

  MONMSG MGID(CPF0000)

DONE:

  QSYS/RTVSYSVAL SYSVAL(&QSTRPRTWTR) RTVNVAR(&STRWTRS)

  IF COND (&STRWTRS = '01') THEN (GOTO CMDMLB(NOWRS))

  CALL PGM(QSYS/QWCSWTRS)

  MONMSG MGID(CPF0000)

NOWRS:

  RETURN *

  CHGVAR VAR(&CPYR) VALUE(&CPYR)

  ENDPGM *
```

IBM iSeries 和 AS/400 入门套装 30

获取源码后，你可以对其进行修改以执行额外的功能。图 2.4 显示了一个用户修改的启动程序示例，当 QCDl 是控制子系统时，你可能会使用它，该程序增加了 QPgnr、QRemote 和 QLocal 子系统。

示例程序还会检查 `QAbnormSw` 系统值的状态，只有当系统之前是正常结束时，才会启动这些子系统。

## 图 2.4
## 修改后的启动程序

```
/* ============================================ */
/* 程序......... StartSys                    = */
/* 源类型...   CLP                         = */
/* 描述... 系统启动             = */
/* ============================================ */
```

```
Pgm
```

```
/* ============================================ */
/* 变量声明                       = */
/* ============================================ */
```

```
Dcl         &StrWtrs   *Char      ( 1 )     
Dcl         &AbnormSw  *Char      ( 1 )     
```

```
/* ============================================ */
/* = 全局错误处理程序                     = */
/* ============================================ */
```

```
MonMsg          ( CPF0000 MCH0000 )
```

```
/* =========================================================== */
/* = 启动基础子系统                  = */
/* =========================================================== */
```

```
StrSbs      QSpl
StrSbs      QServer
StrSbs      QUsrrk
```

```
/* =========================================================== */
/* = 启动操作助手清理操作 = */
/* =========================================================== */
```

```
StrClInUp
```

```
/* =========================================================== */
/* = 如果系统之前正常结束，则启动子系统 = */
/* ============================================================ */
```

```
RtvSysVal   QAbnormSw   (&AbnormSw )
```

## 图 2.4 延续

```
If ( &AbnormSW *Eq '0' ) +
```

```
Do
  StrSbs QInter
  StrSbs QBatch
  StrSbs QCmn
  StrSbs Pgmr
  StrSbs QRemote
  StrSbs QLocal
EndDo
```

```
/* ============================================ */
/* = 如果有指示，则启动写入器 = */
/* ============================================ */
```

```
RtvSysVal QStrprWtr (&StrWtrs )
If (&StrWtrs *Eq '1') +
```
