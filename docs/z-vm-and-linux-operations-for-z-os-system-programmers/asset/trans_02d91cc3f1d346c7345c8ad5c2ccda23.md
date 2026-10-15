

### 表 8-1 z/VM 主要组件标识符

| 前缀 | z/VM 组件 |
| --- | --- |
| DMS | CMS（会话监控系统） |
| DTC | 适用于 z/VM 的 TCP/IP |
| DVH | 适用于 z/VM 的目录维护工具 |
| FCX | 适用于 z/VM 的性能工具包 |
| HCP | CP（控制程序） |
| RAC | RACF 安全服务器 |
| TCP | 适用于 z/VM 的 TCP/IP |

此列表并不详尽。有关更多信息，请参阅 z/VM：CP 消息和代码，GC24-6119，位于：

http://publib.boulder.ibm.com/infocenter/zvm/v5r3/topic/com.ibm.zvm.v53.hcpw0/msgfrmt.htm#msgfrmt

要查找错误消息的解释（包括解决问题提示），请使用 HELP 命令。例如，要查找第 352 页上示例 8-1 中所示错误消息的解释，请键入以下命令：

```
help HCPLGA053E
```

结果显示在示例 8-2 中。

### 示例 8-2 HCPLGA053E 错误消息帮助

```
MSG HCPLGA053E                          All Help Information                 line 1 of 12
(c) Copyright IBM Corporation 1990, 2007

HCPLGA053E  (XAUTOLOG failed for userid:) <userid|value> not in CP directory

Explanation: The user ID supplied was not found in the z/VM directory. If the command was an asynchronous XAUTOLOG, the message indicates which user ID did not get logged on.

System Action: The command is not executed; system operation continues.

User Response: Reissue the command with a valid user ID.

* * * End of File * * *
```

## 8.2 用于错误收集和分析的 z/VM 工具

作为 z/VM 系统操作员，您的职责是确保 z/VM LPAR 可用的所有资源对用户可用，以便用户完成其工作。系统操作员的职责包括收集有关以下任务的信息：

- 记账
- 系统性能
- 系统事件
- 错误记录

z/VM 中提供了一组默认用户来完成这些任务：

- DISKACNT 收集记账和计费信息。
- OPERSYMP 记录症状记录。
- OPERATOR 记录系统事件。
- EREP 记录错误记录。

要检查 z/VM 系统上各种记录的状态，可以使用 query recording 命令（缩写为 q rec），如示例 8-3 所示。

### 示例 8-3 query rec 命令的输出

```
q rec
RECORDING   COUNT   LMT USERID   COMMUNICATION
EREP        ON      00000000 002 EREP      ACTIVE
ACCOUNT     ON      00000000 020 DISKACNT  ACTIVE
SYMPTOM     ON      00000000 002 OPERSYMP  ACTIVE
Ready; T=0.01/0.01 14:58:23
```

本章重点介绍收集系统事件和错误记录。

### 8.2.1 收集有关系统事件的信息

当 z/VM 进行 IPL 时，系统操作员机器（默认为 OPERATOR）会自动登录；如果在 IPL 时指定了 NOAUTOLOG 参数，则不会启动其他机器。在 OPERATOR 控制台上，显示所有与系统相关的消息和错误消息。操作员发出的所有命令以及这些命令的应答也会显示在 OPERATOR 控制台上。

系统操作员机器在 z/VM 配置文件 SYSTEM CONFIG 中定义，如示例 8-4 所示。

### 示例 8-4 系统用户标识配置

```
/*****************************************************************/
/* System Userids */
/*****************************************************************/

System_Userids ,
Operator OPERATOR ,
Account DISKACNT ,
Dump OPERATNS ,
Erep EREP
```

此控制台日志可以保存到 spool 文件中，以便日后分析。如果发生系统异常终止，CP 也会自动将控制台日志保存到 spool 文件中。

### 控制台日志记录状态

要确定控制台活动是否记录到文件中，请发出 QUERY VIRTUAL CONSOLE 命令（缩写为 q v con），如示例 8-5 所示。输出的第一行显示 STOP，表示控制台日志记录未启用。

### 示例 8-5 控制台日志记录状态

```
q v console
00: CONS 0009 ON LDEV L0003 TERM STOP HOST TCPIP FROM
9.57.138.243
00: 0009 CL T NO CONT NOHOLD COPY 001 READY FORM STANDARD
00: 0009 TO LNXGUI PRT DIST LNXGUI FLASCH 000 DEST OFF
00: 0009 FLASH CHAR MDFY 0 FCB LPP OFF
00: 0009 3215 NOEOF 0008 NOKEP NOMS G NOMAME
00: 0009 SUBCHANNEL = 0008

Ready; T=0.01/0.01 15:28:01
```

### 启用控制台日志记录

要在虚拟机（如 LNXGUI）中启用控制台日志记录，请使用命令 CP SPOOL CONSOLE START（缩写为 cp sp con start），如示例 8-6 所示。再次使用 query console 检查状态。输出的第一行应显示 START，表示控制台日志记录已启动。

