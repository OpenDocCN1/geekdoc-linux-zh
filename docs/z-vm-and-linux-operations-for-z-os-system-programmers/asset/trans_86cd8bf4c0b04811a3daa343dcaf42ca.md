

14:59:07 AUTO LOGON *** DTCVSW2 USERS = 9 BY AUTOLOGI
14:59:07 AUTO LOGON *** TCPIP USERS = 10 BY AUTOLOGI
14:59:07 * MSG FROM EREP :1 RECORDING FILE(S), 40 RECORDS, A DISK 03 % FULL
14:59:07 * MSG FROM DISKACNT:17 RECORDING FILE(S),1097 RECORDS, A DISK 27 % FULL
14:59:07 HCPRC8064I Recording data retrieval has been started; recording *LOGREC for userid EREP.
14:59:07 HCPRC8064I Recording data retrieval has been started; recording *ACCOUNT for userid DISKACNT.
14:59:07 * MSG FROM OPERSYMP: 26 RECORDING FILE(S), 26 RECORDS, A DISK 04 % FULL
14:59:07 HCPRC8064I Recording data retrieval has been started; recording *SYMPTOM for userid OPERSYMP.
14:59:08 3020-3022 ATTACHED TO TCPIP BY TCPIP
14:59:08 AUTO LOGON *** FTPSERVE USERS = 11 BY TCPIP

## 5.2.2 热启动、强制启动、冷启动和干净启动

z/VM 为您提供了四种基本启动类型：热启动、强制启动、冷启动和干净启动。它们之间的区别在于 CP 恢复系统环境的数量多少，其中热启动恢复最多，而干净启动保留最少。

如果热启动失败，在使用强制启动或冷启动之前，请联系您的系统支持人员，因为关键文件可能会丢失。

要恢复系统环境，您必须先保存它。当您发出 SHUTDOWN 命令并收到响应 SHUTDOWN COMPLETE 时，CP 会保存系统环境中的以下部分：

- 任何存储中的记账、EREP³ 和症状记录
- 记账、EREP 和虚拟机是症状记录记录服务，通常将这些记录从存储传输到磁盘。如果这些虚拟机未进行检索，记录将保留在存储中。SHUTDOWN 命令会将仍在存储中的任何记录写入 DASD 上的检查点区域，以便在下次 IPL 期间将记录返回到存储以供检索。

- 系统日志消息
- 系统日志消息在用户登录或重新连接时向用户传达信息。

- 搁置文件队列

> ³ EREP：环境记录编辑和打印。EREP 读取硬件和软件生成的错误和其他环境记录，编辑记录并生成打印报告。

搁置文件是磁盘上的数据集合，等待由真实或虚拟的阅读器、打印机或穿孔机处理。SHUTDOWN 命令保存有关定位这些搁置文件的队列的信息。

> 注意：热启动或强制启动后，搁置文件可能不会按相同顺序恢复。

> z/OS 类比：z/VM 的 SHUTDOWN 命令类似于 HALT（Z EOD）命令，只是 z/OS 不保留热数据。

## 系统数据文件队列

系统数据文件队列保存以下数据集合，称为系统数据文件：命名保存系统（NSS）、不连续保存段（DCSS）、映像库、用户类重构（UCR）文件、消息存储库文件和系统跟踪文件。

- 命名保存系统（NSS）是用户已命名并保留在系统数据文件中的操作系统副本。用户可以通过其名称加载操作系统，这比通过设备号加载更有效。
- 不连续保存段（DCSS）是指用户已命名并保留在系统数据文件中的一个或多个存储页。当定义为可共享的不连续保存段被加载时，一个以上的用户可以访问它。
- 映像库是一组包含在系统数据文件中的模块，它们定义打印机用于打印搁置文件的间距、字符和复制修改数据。
- 用户类重构（UCR）文件扩展命令和 DIAGNOSE 代码的特权类。这使您的安装可以自定义 z/VM 的特权类结构。
- 消息存储库文件包含翻译成国家语言的 z/VM 消息和响应。
- 系统跟踪文件包含系统内发生的事件记录。使用这些文件来确定系统问题的来源。

SHUTDOWN 命令保存有关定位这些系统数据文件的队列的信息。

## 单位记录设备、显示器和 3270 打印机的状态

