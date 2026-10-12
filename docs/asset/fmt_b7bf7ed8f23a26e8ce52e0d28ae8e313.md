
根据需要，某些参数无法直接从 Oracle Net Manager 添加，必须手动添加。这些可选参数还附带了监听器名称，以便您可以判断它们属于哪个监听器定义。例如，如果为默认监听器设置了 `STARTUP_WAIT_TIME` 参数，则创建的参数为 `START_WAIT_TIME_LISTENER`。

## 重新加载监听器

如果监听器正在运行，且手动或通过 Oracle Net Manager 对 `listener.ora` 文件进行了修改，则必须重新加载监听器以使用最新信息刷新监听器。`reload` 命令将重新读取 `listener.ora` 文件以获取新定义。如你所见，重新加载监听器不需要停止并启动监听器。虽然停止并重启监听器也可以实现重新加载，但使用 `reload` 命令更好，因为监听器实际上并没有停止，这使得该过程更加高效。以下代码显示了 `reload` 命令的示例：

![](img/4d4ebf1b63c52ce2a364aa79830c39e0_99_0.png)

重新加载监听器对连接到 Oracle 服务的器的客户端不会产生任何影响。

```
C:\lsnrctl reload
```

LSNRCTL for 32-bit Windows: Version 9.0.1.1.1 – Production on 08-OCT-2001 20:34:26

Copyright (c) 1991, 2001, Oracle Corporation. All rights reserved.

Connecting to

(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=mprntw507953)(PORT=1521)))

The command completed successfully

## 显示监听器状态

你可以使用 `status` 命令显示监听器的状态。`status` 命令显示监听器是否处于状态、日志和跟踪文件的位置、监听器运行了多久以及监听器的服务。这是验证监听器是否正常运行且无问题的快速方法。下面的代码显示了 `lsnrctl` 命令的结果。

```
C:\lsnrctl status
LSNRCTL for 32-bit Windows: Version 9.0.1.1.1 – Production on 08-OCT-2001 20:36:14
Copyright (c) 1991, 2001, Oracle Corporation. All rights reserved.
```

# 56 第 2 章 · 在服务器上配置 Oracle Net

Connecting to

(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP))HOST=mprntw507953)

(PORT=1521))

监听器状态 (STATUS of the LISTENER)

| 别名 (Alias) | 监听器 (LISTENER) |
| --- | --- |
| 版本 (Version) | TNSLSNR for 32-bit Windows: Version 9.0.1.1.1 - Production |
| 日期 (Start Date) | 08-OCT-2001 20:32:11 |
| 运行时间 (Uptime) | 0 days 0 hr. 4 min. 4 sec off |
| 跟踪级别 (Trace Level) | OFF |
| 安全 (Security) | OFF |
| SNMP | OFF |

监听器参数文件 (Listener Parameter File)

`D:\oracle\ora90\network\admin\listener.ora`

监听器日志文件 (Listener Log File)

`D:\oracle\ora90\network\log\listener.log`

结束端点摘要 (Ending Endpoints Summary...)

(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp))HOST=mprntw507953.cmg.com)(PORT=1521))

(DESCRIPTION=(ADDRESS=(PROTOCOL=ipc))(PIPENAME=\\pipe\_EXTPROCOIPC))\n(DESCRIPTION=(ADDRESS=(PROTOCOL=tcps))HOST=127.0.0.1)(PORT=2482))(PRESENTATION=GOP)(SESSION=RAW))

(DESCRIPTION=(ADDRESS=(PROTOCOL=tcps))HOST=127.0.0.1)(PORT=2481))(PRESENTATION=GOP)(SESSION=RAW))

(DESCRIPTION=(ADDRESS=(PROTOCOL=tcps))HOST=127.0.0.1)(PORT=9090))(PRESENTATION=http:///admin)(SESSION=RAW))

(DESCRIPTION=(ADDRESS=(PROTOCOL=tcps))HOST=127.0.0.1)(PORT=8080))(PRESENTATION=http:///admin)(SESSION=RAW))

服务摘要 (Services Summary...)

服务 "MWJ" 有 2 个实例 (instance)。实例 "MWJ" 状态为 UNKNOWN，该服务有 1 个处理器 (handler)。

实例 "MWJ" 状态为 READY，该服务有 3 个处理器 (handler)。

服务 "PLSExtProc" 有 1 个实例 (instance)。实例 "PLSExtProc" 状态为 UNKNOWN，该服务有 1 个处理器 (handler)。

命令执行成功 (The command completed successfully)

# 使用 lnrctl 管理监听器 57

## 列出监听器的服务

`services` 命令显示服务的信息，例如服务是否有任何生成的进程 (spawned) 或派生进程 (dispatched)，以及每个服务接受和拒绝的连接数。这是检查监听器是否正在监听特定服务的方法。下面的代码显示了 `services` 命令的示例：

```
C:\lsnrctl services
```

LSNRCTL for 32-bit Windows: Version 9.0.1.1.1 - Production on 08-OCT-2001 20:39:14

Copyright (c) 1991, 2001, Oracle Corporation. All rights reserved.

Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=TCP))(HOST=mprntw507953)(PORT=1521))

服务摘要 (Services Summary)...

服务 "MWJ" 有 2 个实例 (instance)。实例 "MWJ" 状态为 UNKNOWN，该服务有 1 个处理器 (handler)。

```
处理器 (s):
"DEDICATED" established:0 refused:0 LOCAL SERVER
```

实例 "MWJ" 状态为 READY，该服务有 3 个处理器 (handler)。

```
处理器 (s):
"DEDICATED" established:0 refused:0 current:0 state:ready
DISPATCHER <ADDRESS=(PROTOCOL=tcp))(HOST=mprntw507953.cmg.com)(PORT=1038))
Copyright ©2002 SYSEX, Inc., Alameda # 58 第 2 章 · 在服务器上配置 Oracle Net

"DEDICATED" established:0 refused:0 current:2 state:ready
DISPATCHER <ADDRESS=(PROTOCOL=tcp))(HOST=mprntw507953.cmg.com)(PORT=1036))
"DEDICATED" established:0 refused:0 LOCAL SERVER
服务 "PLSExtProc" 有 1 个实例 (instance)
实例 "PLSExtProc" 状态为 UNKNOWN，该服务有 1 个处理器 (handler)。
```

处理器 (s):

"DEDICATED" established:0 refused:0 LOCAL SERVER
