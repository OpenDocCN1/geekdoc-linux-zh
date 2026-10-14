
以下列表描述了代码的工作原理：

- 第 9 行：将 `xxxxx`（已删除）复制到 `szInfectSignature` 变量。这之后被用作感染标记，防止恶意软件多次替换同一个文件。
- 第 11-23 行：打开 `Svchost` 注册表项和 `netsvcs` 值。这返回一个包含所有需要网络访问的服务名的字符串列表（`REG_MULTI_SZ`）。恶意软件遍历列表并选择一个进行劫持。通过利用 `netsvcs` 组而不是随机选择服务，恶意软件确保了网络功能的可用性（依赖关系）。
- 第 24-54 行：对于 `netsvcs` 组中的每个服务，恶意软件查询 `Parameters` 子项下的 `ServiceDll` 路径。它展开任何环境变量（例如 `%SystemRoot%`）以获取完整并将并将存储在 `FileName` 中。
- 第 55-66 行：恶意软件构建两个临时路径以准备后续感染。它将原始二进制文件复制到 `OrigFileCopy`（扩展名为 `.txt`），并将新 DLL 放到初始位置 `NewDllFile`（扩展名为 `.tmp`）。
- 第 67-97 行：恶意软件打开原始二进制文件（`FileName`）的句柄，并将文件的最后 1024 字节读取到缓冲区扫描签名。如果发现签名，循环将进入 `netsvcs` 组中的下一个服务，因为当前服务已经被替换。
- 第 98-113 行：从恶意软件的资源部分检索二进制资源（替换 DLL 的主体），并打开 `NullFile` 的句柄准备将其写入磁盘。
- 第 114-132 行：恶意软件更改文件系统元数据（特别是时间戳），使其看起来新 DLL 实际上于 2005 年 2 月 18 日 20:02:00 创建。它将资源数据写入文件。
- 第 133-145 行：在新 DLL 末尾附加签名，防止恶意软件在未来再次替换它。
- 第 146-167 行：恶意软件将新 DLL（`NewDllFile`）从临时目录移动到原始二进制文件的位置（`FileName`）。它设置了 NTFS 隐藏属性，用户需要更改资源管理器的默认设置才能在目录列表中看到文件。最后，它删除了两个临时文件。

目标服务。它本质上是在寻找 `_SERVICE_RECORD` 结构。如图 12-3 所示，当它找到匹配项时，会减去 8（参见指令 `eax, [esi-8]` 指令），因为在 32 位系统上，`ServiceName` 位于 `_SERVICE_RECORD` 结构体偏移 8 处。这使得 Blazer 指向 `_SERVICE_RECORD` 结构的基地址。接下来，它会覆盖上上一个结构的 `Flink` 和 `Blink` 值，这有效地使得该服务从活动机器的所有服务中“消失”。

```
00017E5 push esi

00017F6 push esi

00017D7 mov [esp+18], esi

00017EA mov esi, 300080H; Minimum address
```

```
00017E8 mov edi

00017EF cmp top_loop, esi

00017F0 mov [ebp+Start], esi

00017F3 mov edi, 500080H; Maximum address

00017F6 j short done searching
```

```
00017A3 push [eax,var_h]

00017A4 call, [esp+addressToSearch]

00017A7 mov esi

00017A6 j short next add
```

```
0001804 mov eax, done_searching

0001807 mov esi, [ebp+10]

000180A mov edi, large F0.0, eax

000180E push esi

0001810 lea eax, ebx

0001813 j short loop end
```

```
00018B5 push [eax,ServiceHide]; wchar = t

00018B8 call, [esp]; wchar = t

00018BB mov ds, eax

00018BE test eax, eax

00018C1 j short next add
```

```
0001907 mov edi, eax

000190A mov [ebp+ServiceRecord], PreviousServiceRecord

000190D mov esi, SERVICE_RECORD.ServiceRecord

0001910 mov eax, SERVICE_RECORD.ServiceRecord

0001913 mov edi, SERVICE_RECORD.ServiceRecord

0001916 mov [ebp+ServiceRecord], PreviousServiceRecord

0001919 j short next add
```

```
0001925 mov eax, [ebp+10]

0001928 mov esi, [ebp+var_h]

000192B mov edi, [ebp+Start]

000192E j short loop
```

```
00019A7 mov next_add

00019AA mov [ebp+var_h], FFFFFFFFH

00019AD3 add esi, 4

00019A6 j short top_loop
```

![](img/9e59079ff66884b5d70128a9edb02f4c_388_0.png)

脱链操作（unlink）发生：

图 12-3：木马通过脱链服务来隐藏服务。

此时，用户无法再依赖上述任何在活动机器上列举服务的方法（即 MMC、`sc query`、`PowerShell` 或 `PsService exe`）。尽管隐藏的服务仍在运行，但 KMS（内核模式管理器）对其存在一无所知，因此大多数分析工具的结果都会被污染。例如，考虑：

# 364 第二部分：Windows 内存取证

一个运行 Windows 安全中心的系统。你可以通过以下命令获取有关服务的详细：

```
C:\>sc query wscvc

SERVICE_NAME: wscvc

  TYPE : 20 WIN32_SHARE_PROCESS

  STATE : 4 RUNNING

           (STOPPABLE,NOT_PAUSABLE,ACCEPTS_SHUTDOWN) 

  WIN32_EXIT_CODE : 0 (0x0)

  SERVICE_EXIT_CODE : 0 (0x0)

  CHECKPOINT : 0x0

  WAIT_HINT : 0x0
```

你可以看到服务正在运行。现在，使用 `net stop` 停止服务并查询该服务的状态。你应该看到它处于停止状态：

```
C:\>net stop wscvc

The Security Center service is stopping.

The Security Center service was stopped successfully.
```

```
C:\>sc query wscvc

SERVICE_NAME: wscvc

  TYPE : 20 WIN32_SHARE_PROCESS

  STATE : 1 STOPPED

           (NOT_STOPABLE,NOT_PAUSABLE,IGNORES_SHUTDOWN)

  WIN32_EXIT_CODE : 0 (0x0)

  SERVICE_EXIT_CODE : 0 (0x0)

  CHECKPOINT : 0x0

  WAIT_HINT : 0x0
```
