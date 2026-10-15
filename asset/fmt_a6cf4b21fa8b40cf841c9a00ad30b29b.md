
```
q set
MSG ON , WNG ON , EMSG ON , ACNT OFF, RUN OFF
LINEDIT ON , TIMER OFF , ISAM OFF, ECMODE ON
ASSIST OFF , PAGEX OFF, AUTOPOLL OFF
IMSG ON , SMSG OFF , AFFINITY NONE , NOTRAN OFF
VMSAVE OFF, 370E OFF
STBYPASS OFF , STMULTI OFF 00/000
MIH OFF , VMCONIO OFF , CPCONIO OFF , SVCACCL OFF , CONCEAL OFF
MACHINE XA , SVC76 CP, NOPDATA OFF, IOASSIST OFF
CCWTRAN ON, 370ACCOM OFF, TIMEBOMB IDLE
```

图 2-2 `q set` 命令的输出

#### 2.1.2 indicate

`indicate` 命令是获取 z/VM 系统整体状态信息的极佳来源。`indicate` 命令的响应会根据发出该命令的虚拟机的 CP 类而异。本书中的示例假设你从具有适当 CP 类的虚拟机（如 MAINT 用户 ID）发出命令。

使用 `indicate load` 显示宿主系统的操作负载：

- 系统中每个在线处理器的使用百分比和 CPU 类型
- 关于扩展存储的信息
- 关于迷你磁盘缓存的信息
- 分页速率
- 调度、合格和休眠列表中的用户数量

在图 2-3 中查看 `indicate` 命令的响应。

请注意，Load 是 `indicate` 命令的默认操作数。

```
indicate load
AVGPROC-0004
XSTORE-000004/SEC MIGRATE-0000/SEC
MDC READS-000001/SEC WRITES-000001/SEC HIT RATIO-100%
PAGING-2/SEC STEAL-00%
Q0-00001(00000)                      DORMANT-00022
Q1-00001(00000)    E1-00000(00000)
Q2-00000(00000)    EXPAN-001 E2-00000(00000)
Q3-00002(00000)    EXPAN-001 E3-00000(00000)

PROC 0000-001% CP    PROC 0001-000% CP
PROC 0002-000% CP    PROC 0003-000% CP

LIMITED-00000
Ready; T=0.01/0.01 11:38:16

RUNNING   VMLINUX8
```

图 2-3 `indicate load` 命令

使用 `indicate paging` 执行以下操作：

- 显示处于页面等待状态的虚拟机列表。
- 显示所有系统用户的页面驻留数据。

使用带有 `wait` 操作数的命令来识别当前处于页面等待的虚拟机，并显示每个虚拟机在辅助存储和扩展存储中分配的页数。这是默认行为。

当 `indicate queues` 命令显示系统中相当大比例的活跃用户持续处于页面等待状态时，请使用 `paging wait`。

当带有 `all` 操作数发出时，该命令显示系统中所有用户的页面驻留数据。图 2-4 展示了 `indicate paging wait` 命令的一个示例。

```
indicate paging wait
No users in page wait
Ready; T=0.01/0.01 15:57:33
indicate paging all
MAINT 000000:001396 TEACHOR2 008162:054438 LXORINST 001847:010210
TEACHOR1 020713:241153 LNXMAINT 000000:00175 LNXINST 022184:080382
FTPSERVE 000000:001412 TCPIP 000226:002578 USER15 000000:000875
TCPM AINT 000000:002000 USERI 000000:000887 EREP 000000:001233
OPERSYMP 000000:001266 DISKACNT 000003:001227 LOGNSYSC 000000:000000
DTCVSW2 000004:002518 DTCVSW1 000000:002566 MSERVR 000000:001181
VMSERVU 000000:001181 VMSERVS 000000:001326 OPERATOR 000000:000001
LXOR4 000000:000000 LXOR1 000000:000001 PERFSVM 000000:000000
LXOR3 002022:000001 LXOR14 000000:000901
Ready; T=0.01/0.01 15:57:41

RUNNING VMLINUX8
```

图 2-4 `Indicate paging` 命令

使用 `indicate queues` 命令（见图 2-5）按优先级顺序显示调度列表和合格列表的当前成员。使用 `exp` 操作数发出时，它显示有关正在处理事务的用户扩展信息。

```
indicate queues
MAINT      Q1 R00 00000686/00000666 LXORINST      Q1 PS 00515332/00515287
LXOR1      Q1 PS 00137239/00137193 LXOR3         Q3 PS 00115756/00138801
TCPIP      Q0 PS 00001026/00000447
Ready; T=0.01/0.01 16:02:32
indicate queues exp
MAINT      Q1 R00 00000686/00000666 .I.. .0005 A00
LXOR3      Q3 PS 00115756/00138801 .D.. 99999 A02
TCPIP      Q0 PS 00001026/00000447 .I.. 99999 A03
Ready; T=0.01/0.01 16:02:34

RUNNING    VMLINUX8
```

图 2-5 `Indicate queues` 命令

用户 ID 后面的第一列指示用户 ID 的列表状态：

- Q0：调度列表，并豁免合格列表延迟
- Q1：调度列表，并作为 E1 用户输入
- Q2：调度列表，并作为 E2 用户输入
- Q3：调度列表，并作为 E3 用户输入
- E1：E1 合格列表
- E2：E2 合格列表
- E3：E3 合格列表
- L0：限制列表，并豁免合格列表延迟
- L1：限制列表，且用户作为 E1 用户输入调度列表
- L2：限制列表，且用户作为 E2 用户输入调度列表
- L3：限制列表，且用户作为 E3 用户输入调度列表

关于 `indicate` 命令以及如何解释对该命令的响应的更多信息，可参阅手册 *z/VM CP Commands and Utilities Reference*（z/VM CP 命令和实用程序参考），SC24-6081-05。

#### 2.1.3 query srm

要概览 CP 调度器使用的系统级参数，我们使用 `query srm` 命令。一些问题可能由此系统资源参数设置不当引起。图 2-6 中可以看到 `query srm` 命令的响应。

```
q srm
IABIAS : INTENSITY=90%; DURATION=2
LDUBUF : Q1=100% Q2=75% Q3=60%
STORBUF: Q1=125% Q2=105% Q3=95%
DSPBUF : Q1=32767 Q2=32767 Q3=32767
DISPATCHING MINOR TIMESLICE = 5 MS
MAXWSS : LIMIT=9999%
...... : PAGES=999999
XSTORE : 0%
Ready; T=0.01/0.01 11:42:45

RUNNING VMLINUX8
```

图 2-6 `query srm` 命令

关于如何设置和调整 srm 参数的更详细信息，请参阅 *Linux on IBM System z: Performance Measurement and Tuning*（Linux on IBM System z：性能测量与调优），SG24-69261。

#### 2.1.4 query alloc page

要检查系统可用和已使用的分页空间量，请使用 `query alloc page` 命令。长期高比例的分页空间使用率可能会导致性能问题，如果分页空间不再可用，还可能导致 ABEND。

> **注：** 当大约 90% 的分页空间被使用时，z/VM 会警告分页空间问题。

图 2-7 提供了 `query alloc page` 命令的一个示例。
