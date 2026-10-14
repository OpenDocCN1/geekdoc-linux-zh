
```
Mon Nov 26 2012 23:01:54, .acb, [ENG THREAD] svchost.exe PID: 1024/TID: 276
Mon Nov 26 2012 23:01:54, ..acb, [ENG THREAD] svchost.exe PID: 1024/TID: 508
Mon Nov 26 2012 23:01:54, ..acb, [ENG THREAD] svchost.exe PID: 1024/TID: 528
Mon Nov 26 2012 23:01:54, ..acb, [ENG THREAD] svchost.exe PID: 1024/TID: 536
Mon Nov 26 2012 23:01:54, ..acb, [ENG THREAD] svchost.exe PID: 1024/TID: 652
Mon Nov 26 2012 23:01:54, ..acb, [ENG THREAD] svchost.exe PID: 1024/TID: 936
```

如果你列出 PID 1024 的 DLL，你将会发现 `6to4.exe` 确实被加载了。

```
$ python.py -f ENG-USTXOU-148/memdump.bin dlllist -p 1024
Volatility Volatility Framework 2.4
********************************************************************
svchost.exe pid: 1024
Command line : C:\WINDOWS\System32\svchost.exe -k netsvcs
Service Pack 3
Base Size LoadPath
0x01000000 0x0600 0xffff:C:\WINDOWS\System32\svchost.exe
0x7c900000 0x0f00 0xffff:C:\WINDOWS\System32\ntdll.dll
[snap]
0x01000000 0x01c0 0xc1 : c:\windows\system32\6to4.exe
[snap]
```

你还可以使用 `svcscan` 查询检查是否有 `6to4` 服务在运行。如输出所示，该服务确实在运行。根据其序号 228，它也是在系统启动后创建的（也就是说它是新的）。正如第 12 章所述，序号应该与服务的字母顺序一致。在这种情况下，`6to4` 的序号应该更低，但相反，它很高。此外，由于该服务在系统启动后 1 秒内运行，这是一个良好的迹象，迹象如下：

```
$ python.py -f ENG-USTXOU-148/memdump.bin svcscan
[snap]
Offset: 0x389d60
Order: 228
Process ID: 6to4
Service Name: 6to4
Display Name: Microsoft Device Manager
Service Type: SERVICE_WIN32_PROCESS
Service State: SERVICE_RUNNING
Binary Path: C:\WINDOWS\System32\svchost.exe
```

此时你已经识别了恶意活动的来源、引入代码的进程、持久化机制以及恶意软件活跃的时间范围。

# 查找攻击者

如果你继续寻找附近的迹象，你会注意到许多表明远程攻击者使用恶意软件的事件。例如，系统中出现了一个名为 `WINDOWS` 的目录，访问了 `ipconfig.exe` 工具，并下载了另一个执行文件 (`ps.exe`)。在此期间，创建了 `net` 命令的 Prefetch 文件。`net` 命令提供了多种功能，包括添加账户、查看域和添加网络共享。以下是相关输出：

+ Mon Nov 26 2012 23:03:10,mac [ENG FILE_NAME] WINDOWS\webui (Offset: 0xbc2100)

Mon Nov 26 2012 23:03:21,[MFT STD_INFO] WINDOWS\system32\ipconfig.exe (Offset: 0xc82640)

Mon Nov 26 2012 23:06:34,mac [ENG FILE_NAME] WINDOWS\ps.exe (Offset: 0x159830)

Mon Nov 26 2012 23:07:53,mac [ENG FILE_NAME] WINDOWS\Prefetch\NET.EXE-01A5C3.pf (Offset: 0xd2d58)

根据这些新的系统事件，你可以扩大调查。例如，如果你搜索创建的目录 (`webui`)，你可能会注意到在该目录下随后创建了其他几个文件：

```
$ mtime -B -d UTC
grep -i webui | grep FILE_NAME
Mon Nov 26 2012 23:06:47,mac [ENG FILE_NAME] WINDOWS\webui\gs.exe (Offset: 0x1627c0)
Mon Nov 26 2012 23:06:52,mac [ENG FILE_NAME] WINDOWS\webui\ra.exe (Offset: 0xa17ff90)
Mon Nov 26 2012 23:06:56,mac [ENG FILE_NAME] WINDOWS\webui\sl.exe (Offset: 0x155ff00)
Mon Nov 26 2012 23:06:59,mac [ENG FILE_NAME] WINDOWS\webui\wc.exe (Offset: 0x155ff40)
Mon Nov 26 2012 23:07:31,mac [ENG FILE_NAME] WINDOWS\webui\net.exe (Offset: 0xdde4e8)
Tue Nov 27 2012 00:49:01,mac [ENG FILE_NAME] WINDOWS\webui\system.dll (Offset: 0x924e80)
Tue Nov 27 2012 00:57:20,mac [ENG FILE_NAME] WINDOWS\webui\svchost.dll (Offset: 0xa39aec00)
Tue Nov 27 2012 01:01:39,mac [ENG FILE_NAME] WINDOWS\webui\https.dll (Offset: 0x109cf7a)
```

# 第二部分：Windows 取证

Nov Nov 27 2012 01:14:48,mac [ENG FILE_NAME] WINDOWS\webui\netstat.dll (Offset: 0x01b9740)

Nov Nov 27 2012 01:26:47,mac [ENG FILE_NAME] WINDOWS\webui\system.bat (Offset: 0x01b9780)

还有迹象表明，这些执行文件（特别是 `SL.EXE` 和 `GS.EXE`）在下载到系统后立即运行了：

Mon Nov 26 2012 23:10:25,...a [ENG STD_INFO] WINDOWS\system32\wshtip.dll (Offset: 0x032cf00)

Mon Nov 26 2012 23:10:25,...a [ENG STD_INFO] WINDOWS\system32\wsock.dll (Offset: 0x030d00)

Mon Nov 26 2012 23:10:25,...a [ENG STD_INFO] WINDOWS\system32\hnetcfg.dll (Offset: 0x03e2fe00)

Mon Nov 26 2012 23:10:35,mac [ENG FILE_NAME] WINDOWS\Prefetch\SL.EXE-01EEA23.pf (Offset: 0x0311400)

Mon Nov 26 2012 23:11:58,mac [ENG REGISTRY]Security\Secrets

Mon Nov 26 2012 23:11:58,mac [ENG FILE_NAME] WINDOWS\Prefetch\GS.EXE-3796d69.pf

`GS.EXE` 文件执行的同时，`SECURITY` 配置单元的 `Policy` 键被访问。这表明 `GS EXE` 执行文件正在访问本地安全权威 (`SA`) 密钥，攻击者可以使用这些提取密码域哈希值。使用缓存转储，你可以了解攻击者可能获取了哪些密码：

```
$ python vol -f ENG_USTXOU-148/memdump.bin cached
Volatility Framework 2.4
```

你可以通过从内存中提取来更深入地了解 `GS.EXE` 执行文件。如果进程正在运行，你可以像第 8 章那样使用 `procdump` 进行转储。否则，你需要使用 `flascan` 找到其 `_FILE_OBJECT` 对象的物理偏移：
