
无论“extra”标志的实际含义是什么（我们从未找到很好的描述），它将我们的注意力引向了 `0xa828` 和 `0x7b0`。下面的 `volshell` 命令显示这些块中的一个确实包含了我们嫌疑者的 Unicode 版本。注意实际块从 `0xac7b8` 开始，因为一个 `_HEAP_ENTRY` 是 32 位的。

```
$ python vol.py -f Win2K3SP1x86.vmem --profile=Win2003SP1x86
volshell -p 3988
```

Volatility Foundation Framework 2.4

## 第二部分：Windows内存取证

Process: notepad.exe, Pid: 3988
PEB: `0x7ffd00`, Heap: `0xa0000`, NumberOfHeaps: `0x6`

### 环境变量

进程环境变量由 `PEB.ProcessParameters.Environment` 指向。它们以 NULL 终止字符串组织，类似于注册表中的 `REG_SZ` 值。

当进程创建时，它通常继承自父进程的环境。父进程可以在调用 `CreateProcess` 时通过指定 `lpEnvironment` 参数来覆盖这种默认行为。以下是你通常可以在环境变量中找到的数据类型列表：

- 可执行程序的路径 (`PATH`)
- 可执行程序的扩展名 (`PATHEXT`)
- 临时目录路径
- 用户目录、浏览器历史和应用程序数据文件夹路径
- 用户名、计算机名和域名
- `cmd.exe` 的位置 (`ComSpec`)

### 环境变量攻击

环境变量最常见的攻击类型包括修改 `PATH` 和 `PATHEXT` 变量。修改这些值的效果与搜索劫持类似。例如，考虑以下场景：

```
PATH=C:\windows;C:\windows\system32
PATH=C:\Users\HR101;tmp;C:\windows;C:\windows\system32
```

## 228 第二部分：Windows 内存取证

在此案例中，`PATH` 变量在 `explorer.exe` 中被更新，登录用户转到“开始 > 运行”并输入“calc”，系统将在 `C:\users\HR101\` 目录下搜索名为“calc”的应用，它还会查看 `windows` 和 `system32` 目录。因此，用户将会在无意中执行恶意代码。同样，`PATHEXT` 包含了一个当用户未指定扩展名时将搜索的扩展名列表。例如，如前所述你输入“calc”，系统将首先查找 `calc.com`，然后是 `calc.exe`，接着是 `calc.bat`，以此此类推。由于以下修改，攻击者可以放置一个名为 `.COM;.EXE;.CMD;.VBE` 的文件：

```text
PATHEXT=\.ZZ;.EXE;.CMD;.VBS;.VBE
```

当然，在这些情况下，调用的恶意代码随后会启动合法的 `calc.exe`——因此用户不会怀疑异异常。

### Coreflood 的存在标记

许多恶意软件通过创建全局可用的互斥锁（`mutexes`）来标记其在系统中存在。这有助于防止意外重感染。互斥锁还提供了强有力的取证指标。Coreflood 使用环境来实现非常相似的目的——标记其在进程内的存在。由于 Coreflood 的主要组件是一个 `DLL`，它需要一种方法确保同一个进程不会被注入多次恶意软件，因此他们编写了 `DLL` 的入口函数，根据父进程的 `PID` 创建一个随机字符串。然后，如果该字符串不存在，通过调用 `EnvironmentVariable` 将其添加到进程环境中。否则，`DLL` 将立即卸载。图 8-2 显示了 `DLL` 入口函数的图表（由 `IDA` 生成）。

![](img/9e5979ff6684b5d702.png)

图 8-2：显示 Coreflood 入口点调用的函数图表

### 在进程中猎杀恶意软件

我喜欢在培训课程上问的一个有趣谜题是：根据你学到的，以下进程中有多少感染了 Coreflood 的 `DLL`？注意，我们正在使用 Volatility 的 `envars` 插件来枚举内存转储中的变量。

```
$ python vol.py -f coreflood.img --profile=Win7SP envars
****************************************
Pid 1444 explorer.exe (PPid 644) Block at 0x0000
USERNAME=Administrator
USERPROFILE=C:\Documents and Settings\Administrator
PATHEXT=C:\WINDOWS
[SNIP]
****************************************
Pid 512 explorer.exe (PPid 1444) Block at 0x0000
ProgramFiles=C:\Program Files
PATHEXT=SYSTEM
SESSIONNAME=Console
USERDOMAIN=WORKGROUP
USERNAME=Administrator
USERPROFILE=C:\Documents and Settings\Administrator
PATHEXT=SYSTEM
[SNIP]
****************************************
Pid 560 notepad.exe (PPid 1444) Block at 0x0000
USERNAME=Administrator
USERPROFILE=C:\Documents and Settings\Administrator
PATHEXT=SYSTEM
[SNIP]
****************************************
Pid 220 firefox.exe (PPid 1444) Block at 0x0000
USERNAME=Administrator
USERPROFILE=C:\Documents and Settings\Administrator
PATHEXT=SYSTEM
[SNIP]
```

如果你回答“两个”，那么你是正确的。起初，看起来所有进程都被感染了，它们都包含可疑的变量名。然而，我们提到过子进程通常会继承父进程的变量。我们还提到变量名取决于进程的 `PID`。如果所有进程都被感染了，你只会看到两个唯一的变量名（`PATHEXT` 和）。最后三个进程（`explorer.exe`、`notepad.exe` 和 `firefox.exe`）是由 `PID 1444` 生成的，这解释了为什么它们有一份 `PATHEXT` 副本。你会发现 `explorer.exe` 实际上有两个变量：一个是从父进程继承的，另一个是 Coreflood 为它自己的 `PID` 计算的。

> 注意
> `envars` 插件的 `--silent` 选项会导致它抑制已知变量（基于硬编码白名单）；这在变量名或值不显而易见的情况下非常有用；例如，`PATHEXT`。

### 标准句柄

通过分析进程的标准句柄（standard handles），你可以确定它从哪里获取输入以及向哪里发送输出和错误消息。这在调查远程攻击者的潜在入侵时特别有用。例如，在系统上创建后门命令 shell 的相当常见的方法涉及启动 `cmd.exe` 实例，并将其标准句柄重定向到命名管道或网络套接字。然后，攻击者可以使用 `telnet` 或 `netcat` 连接到目标机器（前提没有防火墙阻止访问）。以下代码显示了使用此技术的后门的源码：

```c
1 mySockAddr.sin_family = AF_INET;
2 mySockAddr.sin_port = htons(31337);
3 mySockAddr.sin_addr.s_addr = htonl(INADDR_ANY);
4
5 if (bind(myMainSock, (SOCKADDR *)&mySockAddr,
6 sizeof(mySockAddr)) == SOCKET_ERROR)
7 {
8 WSCleanup();
9 return(-1);
10 }
11
12 while(1) {
13 myCliSock = SOCKET_ERROR;
14 while (myCliSock == SOCKET_ERROR)
15 Sleep(1);
16 listen(myMainSock, SOMAXCONN);
17 uiSzSockAddr = sizeof(myCliSockAddr);
18 myCliSock = accept(myMainSock,
19 (SOCKADDR *)&myCliSock,
20 (int *)&uiSzSockAddr);
21 }
22 memset(&myPi, 0, sizeof(myPi));
23 memset(&myPi, 0, sizeof(myPi));
```
