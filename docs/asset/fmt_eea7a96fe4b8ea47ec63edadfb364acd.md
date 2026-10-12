
此程序没有任何担保。输入 `help warranty` 查看详情。

`NOTE: stdin: not a tty`

`GNU gdb (GDB) 7.0`

`Copyright (C) 2009 Free Software Foundation, Inc.`

好了，现在我们了解了细微差别，让我们崩溃吧。Kdump 正在后台执行它的魔法。如果你进入了 `crash` 提示符（无论使用旧语法还是新语法），则说明一切正常。

## 崩溃分析 (crash) 165

在法律允许范围内，本软件不提供任何保证。输入 `show copying` 和 `show warranty` 查看详情。

```
This GDB was configured as "x86_64-unknown-linux-gnu"...

please wait... (gathering kmmem slab cache data)

please wait... (gathering module symbol data)

please wait... (gathering task table data)

please wait... (determining panic task)

SYSTEM MAP: /boot/System.map-2.6.32.59-0.3.1-default
DEBUG KERNEL: /boot/vmlinux-2.6.32.59-0.3.1-default (2.6.32.59-0.3.1)
DUMPFILE: /tmp/dump/2013-03-05-12:57/vmcore

CPUS: 32

DATE: Tue Mar 5 12:56:34 2013

UPTIME: 57 days, 15:12:55

LOAD AVERAGE: 15.67, 15.93, 15.07

TASKS: 882

NODENAME: ics010745

RELEASE: 2.6.32.59-0.3.1-default

VERSION: #1 SMP 2012-04-27 11:14:44 +0200

MACHINE: x86_64 (2600 Mhz)

MEMORY: 128 GB

PANIC: *[496889.568159] Oops: 0000 [#1] SMP * (check log for details)

PID: 27010

COMMAND: "task.bin"

TASK: ffff880a8e68a500 [THREAD_INFO: ffff880a77f98000]
nCPU: 19

STATE: TASK_RUNNING (PANIC)
```

Copyright ©Intel Corporation. All rights reserved.

## Crash 命令

一旦 `crash` 运行并且你正面对 `crash` 提示符时，就是时候尝试一些 `crash` 命令了。在本教程中，我们不会过度关注命令本身或理解你的输出。目前，这只是我们所需内容的简要概述。`crash` 命令在红帽白皮书中有更详细的列出（Anderson, n.d.）。事实上，该文档包含了你处理 `crash` 时所需的所有内容。以下是你将需要的一些少量重要且实用的命令。

### 回溯 (Backtrace)

`backtrace` 命令显示内核堆栈回溯。如果不提供参数，则显示当前上下文的堆栈回溯。
