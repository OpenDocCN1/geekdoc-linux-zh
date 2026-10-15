
**注意：** 我们看到问题发生在 `procA`，但我们要在源代码中定位它。可执行文件 `App2S` 在分发给客户时去除了调试符号。幸运的是，带有调试信息的可执行文件被保存在一个独立的 `App2S.debug` 文件中。我们退出调试会话 (`q`)，将 `App2S` 可执行文件重命名为 `app2s.symbols`，并重命名了 `App2S.debug`。

- 5. 加载来自 `x64/` 文件夹的 `core.App2S` dump：

```
Microsoft (R) Windows Debugger Version 10.0.27725.1000 AMD64
Copyright (c) Microsoft Corporation. All rights reserved.

Loading Dump File [C:\ALCD2\x64\App2S\core.App2S]
64-bit machine not 64-bit API

************ Path validation summary ************

Response Time (ms) srv*

Deferred srv*

Symbol search path is: srv*

Executable search path:

Generic Unix Version 0 UP Free x64

System Update: not available

Process Update: not available
```

```
(e96.e9): Signal SIGSEG (Segmentation fault) code SEGV_MAPERR (Address not mapped to)

at 00

*** WARNING: Unable to verify timestamp for App2S

App2S+0x1bc

00000000 0401bbc ??
```

- 3. 将日志输出到文件，以防某些命令输出内容过长：

```
0:000:.logopen C:\ALCD2\x64\App2S-WinDbg.log

Opened log file 'C:\ALCD2\x64\App2S-WinDbg.log'
```

- 4. 指定 dump 文件夹为符号路径并重新加载符号：

```
0:000:.symfix; sympath C:\ALCD2\x64\App2S\

Symbol search path is: srv*;C:\ALCD2\x64\App2S\

Expanded symbol path is:

cache*:srv*https://msdl.microsoft.com/download/symbols;c:\alcd2\x64\app2s\
```

```
************ Path validation summary ************

Response Time (ms) Location

srv srv*

OK C:\ALCD2\x64\App2S\
```

```
*** WARNING: Unable to verify timestamp for App2S
```

```
0:000:.reload
```

```
************ Symbol Loading Error Summary ************

Module name Error

App2S The system cannot find the file specified
```

你可以通过开启符号加载诊断 (`!noisy`) 并重复导致符号加载的命令来排查符号相关的问题。你还应该验证你的符号搜索路径 (`.sympath`) 是否正确。

```
0:0000:k

# Child-SP      RetAddr          Call Site

0:000077f3d537d6d8 0000004001c9   App2S!procA+0xe1

1:000077f3d537d800 0000004001c5   App2S!bar_two+0xe

2:000077f3d537d900 0000004007c3   App2S!foo_two+0xe

3:000077f3d5379a0 000000403123   App2S!thread_two+0x16

4:000077f3d537dc80 00000044b4f2   App2S!start_thread+0xf3

5:000077f3d537d7e0 ffffffffffff   App2S!clone+0x3f

6:000077f3d537d880 ffffffffffff   ffffffffffff
```

**注意：** 我们看到问题发生在 `procA`，但我们要在源代码中定位它。可执行文件 `App2S` 在分发给客户时去除了调试符号。幸运的是，带有调试信息的可执行文件被保存在一个独立的 `App2S.debug` 文件中。我们退出调试会话 (`q`)，将 `App2S` 可执行文件重命名为 `app2s.symbols`，并重命名了 `App2S.debug`。

- 5. 加载来自 `x64/` 文件夹的 `core.App2S` dump：

Microsoft (R) Windows Debugger Version 10.0.27725.1000 AMD64
Copyright (c) Microsoft Corporation. All rights reserved.

Loading Dump File `[C:\ALCD2\x64\App2S\core.App2S]`
64-bit machine not 64-bit API

## 系统找不到指定的文件

你可以通过开启符号加载诊断 (`!symbols`) 并重复导致符号加载的命令来排查大多数与符号相关的问题。你还应该验证你的搜索路径 (`.symbols`) 是否正确。

```
0:000> k

# Child-SP      RetAddr             Call Site

00 0000000 8a239b40  00000000  0a00070c

01 0000000 8a239b50  00000000  0a00070b

02 0000000 8a239b70  00000000  0a00070c

03 0000000 8a239b80  00000000  0a0004cd

04 0000000 8a2399a0  00000000  0a44365c

05 0000000 8a2399c8  ffffffff  0xc02e4

06 0000000 8a2399cc  00000000  ffffff

App2!procA+0xc

App2!lib_two+0xc

App2!thread_two+0xc

App2!thread_thread_two+0xc2e4

App2!thread_start+0xc

0xffffffffffff
```

注意：我们看到在 `procA` 中发现了问题，但我们想在源代码中加载它。可执行文件 `App2S` 在分发之前已经去除了调试符号。遗憾的是，带有调试信息的可执行文件被保存在独立的 `App2S.debug` 中。我们退出了调试会 (`q`)，将可执行文件 `App2S` 重命名为 `App2.symbols`，并将 `App2S` 重命名为 `App2s`。

- 5. 再次从 `x64/App2S` 文件夹加载 core dump `_home_ubuntu_ALCD2_A64_App2S.10001.3d452460-e216-4918-b09f-34067205e2.2065.172563749` dump 文件：

Microsoft (R) Windows Version 10.0.22725.1000 AMD64
Copyright (c) Microsoft Corporation. All rights reserved.

Loading Dump File `C:\ALCD2\x64\App2S.core.App2`
64-bit machine is not 64-bit

************ Path validation summary ************
| Response Time (ms) | Location |
| :--- | :--- |
| Deferred | `srv*` |
| Symbol search path: | `srv*` |
| Executable search path: | |

Generic Unix Version UP Free x64
System Update: not available
Process Update: not available
...

`(e96.08)`: Signal `SIGSEGV` (`Segmentation fault`) code `SEGV_MAPERR` (`Address not mapped to memory`) at `0x0`
`*** WARNING: Unable to verify timestamp for App2S`
`App2s!0x1bcbc`:
`00000000 0401bcbb ??`

- 6. 以防某些命令的输出过长，向现有文件中追加日志：

```
0:000> logappend C:\ALCD2\A64\App2S\App2S-WinDbg.log

Opened log file 'C:\ALCD2\A64\App2S-WinDbg.log'
```

- 7. 指定 dump 文件夹为符号路径并重新加载符号：

```
0:000> .symfix;sympath C:\ALCD2\A64\App2S\

Symbol search path is: srv*;C:\ALCD2\A64\App2S\

Expanded Symbol path is:

cache*;SRV*https://msdl.microsoft.com/download/symbols;c:\abcd2\a64\app2s\
```

*********** Path validation summary ************
| Response (ms) | `srv*` |
| :--- | :--- |
| Deferred | `C:\ALCD2\A64\App2S\` |
| OK | |

`*** WARNING: Unable to verify timestamp for App2S`

```
0:000> .reload

*** WARNING: Unable to verify timestamp for App2S
```

*********** Loading Error Summary ************
Module Error
`App2S` The系统找不到指定的文件

你可以通过开启符号诊断 (`!sym`) 并重复导致符号加载的命令来排查大多数与符号相关的问题。你还应该验证你的符号路径搜索 (`.sympath`) 是否正确。

```
0:000> k ChildAddr Call Site

00 00000ffffba2395c8 00000000000007c App25ipro_Exec[/home/ubuntu/ALCD2/A64/App2S/main.c @ 26]

01 00000ffffba2395c8 00000000000007e App25if_thread_tw0[/home/ubuntu/ALCD2/A64/App2S/main.c @ 56]

02 00000ffffba2395c8 00000000000007a App25if_thread_tw0[/home/ubuntu/ALCD2/A64/App2S/main.c @ 56]

03 00000ffffba2395c8 0000000000000c4 App25thread_tw0x10

04 00000ffffba2395c8 fffffffff fffffffff Pr_thread_024

05 00000ffffba2395c8 0000000000000e4 App25thread_start+x8

06 00000ffffba2395c8 000000000000 fffffffff
```

- 8. 如果我们设置了源代码文件夹，我们应该直接看到问题：

```
0:000> .srcpath C:\ALCD2\A64\App2S\

Symbol search path is: srv*;C:\ALCD2\A64\App2S\

Expanded Symbol path is:

cache*;SRV*https://msdl.microsoft.com/download/symbols;c:\abcd2\a64\app2s/
```

## 练习 (x64, GDB)

- **目标**: 识别高负载线程。
- **模式**: 活跃线程；高负载线程；已测试。
- 1. 应用 `App3` 占用 100% CPU（根据 `top` 输出）：

```
$ top

top -13:19 23:14, 0 users, load average: 0.74, 0.25

Tasks: 10 total, 1 running, 9 sleeping, 0 zombie

%CPU(s): 12.5 us, 0.0 sy, 87.5 id, 0.0 wa, 0.0 hi, 0.0 si

Mem: 7912.total, 5555.1 free, 2356.9 used, 2086.6 avail

Mem Swap: 2048.total, 0 free, 2048.0 avail

PID  PR  VIRT    RES SHR TIME

39765 2  42068     1 S   100.0 1:20

117 2  17640    84 S   00:00

31231 2  42068   112 S   00:00

3443 2  17640    68 S   00:00

3444 2  17640    68 S   00:00

34235 2  6992   3248 R   00:02

top
```

它的 core dump 使用 `gdb` 保存的：

```
~/ALCD2/x64/App3$ gdb -o App3.3975

[New Lwp 3976]

[New Lwp 3977]

[New Lwp 3978]

[New Lwp 3979]

[New Lwp 3980]

[Thread debugging by thread_db enabled]

Using host libthread_db "/lib/x86_64-linux-gnu/libthread_db.so".

0x000000000441a80 in nanosleep (1)

Saved core App3.3975

Inferior 1 (process 3975)
```

- 2. 加载 `App3.3975` dump 文件并在 x64 调试器执行：

```
~/ALCD2/x64/App3$ gdb -c App3.3975 -se App3

GNU gdb (debian 8.2+deb) 8.2

Copyright (C) 2018 Software Foundation, Inc.

License GPLv3 - GNU GPL version 3 or later <http://www.gnu.org/licenses/gpl3.html>

此软件允许更改和重新分发。

在法律允许范围内不提供保证。

输入 "show copying" 和 "show warranty" 查看详情。

此 GDB 配置为 "x86_64-linux-gnu"。

输入 "show configuration" 查看配置详情。

更多详细的说明，请访问：

http://www.gnu.org/software/gdb/bugs/

在线查找 GDB 手册或其他文档资源：

http://www.gnu.org/software/gdb/documentation/

需帮助，请输入 "help"。

输入 "apropos word" 搜索与 "word" 相关的命令...

从 App3 读取符号...完成。

[LWP 3975]

[LWP 3976]

[LWP 3977]

[LWP 3978]

[LWP 3979]

[LWP 3980]
```

```
[Thread debugging libthread enabled]
Using host libthread library "/lib/x86_64-linux-gnu/libthread_db.so".
Core 由 "App3" 生成
#0 0x000000000441a80 in nanosleep ()
当前线程为线程 1 (0xf8c6aa70 (LWP 3975))
```

- 3. 以防命令输出过长，向文件设置日志：

```
(gdb) set logging on App3.log
Logging output to App3.log
```

- 4. 列出所有线程：

```
(gdb) info threads

| Id | Target Frame |

| :--- | :--- |

| *1 | 0xf8c0aa7b (LWP 3975) 0x0000000044a80 in nanosleep () |

| 2 | 0xf8c6ca90 (LWP 3976) 0x0000000044a80 in nanosleep () |

| 3 | 0xf8c6c2df (LWP 3977) 0x0000000044a80 in nanosleep () |

| 4 | 0xf8c6a89d (LWP 3978) 0x0000000044a80 in nanosleep () |

| 5 | 0xf8c6b29c (LWP 3979) 0x0000000044a80 in nanosleep () |

| 6 | 0xf8c6aab7 (LWP 3980) 0x0000000044a80 in nanosleep () |
```

- 5. 切换到活跃线程：
