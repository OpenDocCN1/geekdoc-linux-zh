
```cpp
        ReadFile(n
        cout << "Waiting for memory status change notification..." << endl;

    ReadFile(
        mailslot,
        action,
        sizeof(action),
        &binput,
        (LPOVERLAPPED)NULL);

    switch (atoi(action)){
        case 1:
            ReadFile(
                mailslot,
                memoryamount,
                sizeof(memoryamount),
                &binput,
                (LPOVERLAPPED)NULL);
            cout << memoryamt << " bytes of memory to be reserved" << endl;

            ReadFile(
                mailslot,
                action,
                sizeof(action),
                &binput,
                (LPOVERAPPED)NULL);
            cout << action << " code detected for protection type" << endl;
            region = VirtualAlloc(
                NULL,
                atoi(memoryamt),
                MEM_RESERVE,
                prottype[atoi(action)]));
            if(region == NULL) cout << "VirtualAlloc status = *" << GetLastError() << endl;

            VMstat();
            break;
        case 2:
            ReadFile(
                mailslot,
                memoryamt,
                sizeof(memoryamt),
                &binput,
                (LPOVERAPPED)NULL);
            cout << memoryamt << " bytes of memory to be committed" << endl;

            ReadFile(
                mailslot,
                action,
                sizeof(action),
                &binput,
                (LPOVERAPPED)NULL);
            cout << action << " code detected for protection type" << endl;
            region = VirtualAlloc(
                atoi(memoryamt),
                MEM_COMMIT,
                prottype[atoi(action)]));
            if(region == NULL) cout << "VirtualAlloc status = *" << GetLastError() << endl;

            VMstat();
            break;
        case 3:
            {
                ReadFile(
                    mailslot,
                    memoryamt,
                    sizeof (memoryamt),
                    &binput,
                    (LPOVERAPPED)NULL);
                cout << memoryamt << " bytes to be made free" << endl;

                ReadFile(
                    mailslot,
                    action,
                    sizeof(action),
                    &binput,
                    (LPOVERAPPED)NULL);
                cout << action << " detected for free operation" << endl;

                if(VirtualFree(
                    region,
                    atoi(memoryamt),
                    freetype[atoi(action)]) == 0){
                    cout << "VirtualFree status = " << GetLastError() << endl;
                }

                VMstat();
            }
            break;
        case 4:
            {
                ReadFile(
                    mailslot,
                    memoryamt,
                    sizeof (memoryamt),
                    &binput,
                    (LPOVERAPPED)NULL);
                cout << memoryamt << " bytes of region to be locked" << endl;

                if(VirtualLock(
                    region,
                    atoi(memoryamt)) == NULL){
                    cout << "VirtualLock status = " << GetLastError() << endl;
                }

                VMstat();
            }
            break;

        case 5:
            {
                ReadFile(
                    mailslot,
                    memoryamt,
                    sizeof (memoryamt),
                    &binput,
                    (LPOVERAPPED)NULL);
                cout << memoryamt << " bytes of region to be unlocked" << endl;

                if(VirtualUnlock(
                    region,
                    atoi(memoryamt)) == NULL) {
                    cout << "VirtualUnlock status = " << GetLastError() << endl;
                }

                VMstat();
                break;
            }
        case 6:
            {
                cout << "Terminating..." << endl;
                exit(0);
            }
        default:
            cout << "Unknown action code" << endl;
            break;
    }
}
```

上文已解释 `SERIALIZE`。`lpMem` 参数是一个指向要确定大小的内存块的指针。

`HeapAlloc` 函数从堆中重新分配一块内存。此函数允许你调整内存块的大小并更改其他内存属性。`HeapAlloc` 例程具有以下调用序列：

```
LPVOID HeapAlloc(
    HANDLE hHeap,
    DWORD dwFlags,
    LPVOID lpMem,
    DWORD dwBytes
);
```

参数 `hHeap` 表示进行内存重新分配的堆句柄。`dwFlags` 参数可以具有表 5.8 中描述的相同传递值，再加上 `HEAP_ALLOC_IN_PLACE_ONLY`，它指定在重新分配内存块到更大的尺寸时不时不发生移动。如果未指定此标志且重新分配请求为更大的大小，函数可能会将内存块移动到新位置。如果指定了此标志且内存块在不移动的情况下无法扩大，函数将失败，并保持原始内存块不变。参数 `lpMem` 是指向函数重新分配的内存块的指针。该指针是通过调用 `HeapAlloc` 或 `HeapFree` 函数获得的。参数 `dwBytes` 表示内存块的新大小，单位为字节。可以使用此函数增加或减少内存块的大小。

`HeapFree` 例程释放由 `HeapAlloc` 或 `HeapFree` 从堆中分配的内存块，并具有以下调用序列：

```
BOOL HeapFree (
    HANDLE hHeap,
    DWORD dwFlags,
    LPVOID lpMem
);
```

`HeapFree` 的所有参数含义均与之前的例程相同。参数 `dwFlags` 只能设置为 `HEAP_NO_SERIALIZE`。

## 其他实用的堆例程

其他例程对于堆管理可能非常方便。表 5.9 列出了其中一些函数。

### HeapCreate 例程

默认堆可能无法满足你，你可以使用 `HeapCreate` 例程启动自己的堆，该例程具有以下调用序列：

```
HANDLE HeapCreate(
    DWORD flOptions,
    DWORD dwInitialSize,
    DWORD dwMaximumSize)
```

参数 `dwInitialSize` 指定堆的初始大小，单位为字节。该值决定了分配给堆的初始物理存储量。如果 `dwMaximumSize` 为非零值，它指定了堆的最大 own，单位为字节。此外，如果 `dwMaximumSize` 为非零值，则堆无法增长，且存在绝对限制。堆中内存块的最大尺寸小于 `0x7FFFF8`。分配更大块的请求将不会成功，即使 `flOptions` 可以设置为 `HEAP_NO_GENERATE_EXCEPTIONS`。如果 `dwMaximumSize` 为 0，则表示堆可以增长。示例 5-4 是一个关于如何使用某些堆例程的初级示例。在这个示例中，通过调用 `GetProcessHeap` 获取默认堆句柄，然后从从中分配了 10000 字节。调用 `HeapSize` 来确认已分配的存储量。调用 `HeapFree` 来释放已分配的内存，并再次调用 `HeapSize` 来确认目前已分配的存储量。最后，调用 `HeapFree` 将分配的堆存储返回给系统。

### 示例 5-4 某些堆内存管理例程的演示

```
#include <iostream.h>
#include <windows.h>

HANDLE hHeap;
CHAR *lpMem;
DWORD size;

void main() {
  hHeap = GetProcessHeap();
  lpMem = (char *)HeapAlloc(hHeap, 0, 10000);
  size = HeapSize(hHeap, 0, lpMem);
  cout << "Heap size is " << size << " bytes."<<endl;
  lpMem = (char *)HeapRealloc(hHeap, 0, lpMem, 30000);
  size = HeapSize(hHeap, 0, lpMem);
  cout << "New heap size is " << size << " bytes."<<endl;
  if ((char *)HeapFree(hHeap, 0, lpMem) == NULL)
    cout << "HeapFree error: " << GetLastError() << endl;
}
```

---

### 表 5.9 其他方便的堆管理例程

| 堆例程 | 函数描述 |
|---|---|
| `HeapValidate (HANDLE hHeap, DWORD dwFlags, LPCVOID lpMem);` | 该函数尝试验证指定的堆，扫描堆中的所有内存块，并验证由堆管理器维护的堆控制结构是否处于一致状态。你也可以使用此函数在不指定堆的情况下验证单个内存块，而不检查整个堆的有效性。返回非零值表示堆有效。 |
| `HeapCompact (HANDLE hHeap, DWORD dwFlags, LPCVOID lpMem);` | 该函数扫描堆中的所有内存块，并验证由堆管理器维护的堆控制结构是否处于一致状态。此例程也可用于验证指定堆内的单个内存块，而不检查整个堆的有效性。例程返回非零值。 |
| `UINT HeapCompact (HANDLE hHeap, DWORD dwFlags);` | 该函数尝试紧凑指定的堆。通过合并相邻的空内存块并放弃大型的空内存块来紧凑堆。 |
| `HeapLock (HANDLE hHeap);` | 函数尝试获取与指定的堆相关的临界区或锁。调用线程拥有堆锁。 |
| `HeapUnlock (HANDLE hHeap);` | 仅调用线程将释放堆锁。 |

# Solaris 中额外的内存管理函数

| 表 5.11 | memcnt1 函数 cmd 参数的描述 |
| 命令 | 描述 |
| MC_LOCK | 锁定内存中范围内的页。用于支持 mlock。arg 被忽略，但必须为 0。 |
| MC_LOCKAS | 锁定内存中地址空间内的页。addr 和 len 被忽略，但必须设置为 0。arg 表示一个由标志 MCL_CURRENT（当前映射）或 MCL_FUTURE（未来映射）构建的整数。 |
| MC_SYNC | 将范围内具有属性 `attr` 的所有已修改页面写入其支撑存储（backing store）。用于支持 sync。arg 代表一个标志，可以与以下内容进行按位或（OR）操作：MS_SYNC，在所有 I/O 操作完成后返回；MS_ASYNC，在所有 I/O 操作调度完成后后立即返回；以及 MS_INVALIDATE，使内存中的所有缓存数据失效。 |
| MC_UNLOCK | 解锁内存中具有属性 `attr` 的范围内的页。arg 被忽略，但必须为 0。 |
| MC_UNLOCKAS | 移除地址空间内存，以及地址空间中具有属性 `attr` 的所有页的锁。addr 和 len 必须为 0：arg 被忽略，但必须为 0。 |

| 表 5.12 | 例 memcnt1 attr 参数的描述 |
| 属性 | 描述 |
| SHARED | 页位于映射共享区域中。 |
| PRIVATE | 页位于映射私有区域中。 |
| PROT_READ | 页可读。 |
| PROT_WRITE | 页可写。 |
| PROT_EXEC | 页可执行。 |
| PROC_TEXT | 具有读和执行权限的私有映射段。 |
| PROC_DATA | 具有写权限的私有映射段。 |

## 例 mlock 和 munlock

`mlock` 和 `munlock` 例用于锁定和解锁内存页，具有以下调用序列：

```c
int mlock (
    caddr_t addr,
    size_t len);

int munlock (
    caddr_t addr,
    size_t len);
```

# 第 5 章 内存操作

`lock` 和 `unlock` 函数用于根据 `addr`、`len` 参数确定的页范围。如果两个不同的进程锁定同一个页，该页将保持锁定状态，直到两个进程都移除它们的锁。锁是不嵌套的；然而，同一个进程中对同一地址的操作将通过一次 `unlock` 全部移除。通过 `mlock` 建立的锁在 `fork` 调用后不会被子进程继承由于对系统资源的影响，`mlock` 和 `munlock` 的使用限制在具有超级权限的进程。

# getpagesize 例

`getpagesize` 例计算一个页的字节数，具有以下调用序列：

```c
int pagesize = getpagesize(void);
```

页大小是系统页大小，不一定与底层的硬件页大小相同。

# mlock 和 munlock 例

`mlock` 例锁定内存中所有由地址空间映射的页，具有以下调用序列：
