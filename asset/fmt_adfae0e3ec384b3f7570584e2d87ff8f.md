
```c
exit(4);

if ((key = ftok("/home/ul/donm/shared.file",'key')) == (key_t) -1) {
    perror("ftok error");
    exit(4);
}

if ((shmidx=shmget(key, 10, IPC_CREAT|0644)) == -1) {
    perror("shmget error");
    exit(1);
}

if ((shindy=shmget(key, 10, IPC_CREAT|0644)) == -1) {
    perror("shmget error");
    exit(1);
}

mptr = (pthread_mutex_t *)shmat(shmidx, (void *)0, 0);
cvptr = (pthread_cond_t *)shmat(shindy, (void *)0, 0);

pthread_mutexattr_init(&mutex_shared_attr);
pthread_mutexattr_setpshared(&mutex_shared_attr, PTHREAD_PROCESS_SHARED);
status = pthread_mutex_init(mptr, &mutex_shared_attr);
if(status != 0) {
    perror("mutex init failure");
    exit(2);
}

pthread_condattr_init(&cv_shared_attr);
pthread_condattr_setpshared(&cv_shared_attr, PTHREAD_PROCESS_SHARED);
status = pthread_cond_init(cvptr, &cv_shared_attr);
if(status != 0) {
    perror("conditional variable init failure");
}

id = open("shared.file",O_RDWR);

if((mapView = (char*)mmap((caddr_t)0, 100, (PROT_READ|PROT_WRITE,
    MAP_SHARED, id, 0)) == (caddr_t) -1) {
    perror("mmap failure");
    exit(3);
}

tmp = mapView;

cout << "Now display changed file contents before I change 'em!" << endl;
cout << mapView;
cout << "Wait for P1 to say to go..." << endl;
```

# 示例 4–14 使用 mmap 和 munmap 例程在 UNIX 中演示文件映射（续续）

```c
pthread_mutex_lock(mptr);
if (status=pthread_cond_wait(cvptr,
```

# UNIX 中的文件时间

`utime` 例程用于设置文件的访问时间时间和修改时间，其调用序列如下：

```c
int utime(
    const char *path,
    struct utimbuf *times);
```

参数 `path` 描述所感兴趣的文件。如果参数 `times` 为 `NULL`，则文件的访问时间和修改时间被设置为当前时间。该进程必须是文件的所有者或具有写权限才能以这种方式使用 `utime`。如果参数 `times` 不为 `NULL`，则 `times` 被解释为指向 `utimbuf` 结构（定义在 `utime.h` 中）的指针，并将访问时间和修改时间设置为指定结构中包含的值。只有文件的所有者或超级用户可以使用 `utime`。`utimbuf` 结构包含以下成员：

```c
time_t actime;   /* 访问时间 */
time_t modtime;   /* 修改时间 */
```

`utimbuf` 结构成员中的时间是以自 1970 年 1 月 1 日 00:00:00 UTC 以的秒数。`utime` 例程导致最后文件状态更改时间 `st_ctime` 更新。示例 4-15 演示了 `utime` 例程的使用。

# 示例 4-15 演示如何使用 utime 例程

```c
#include <iostream.h>
#include <stdlib.h>
#include <stdio.h>
#include <time.h>
#include <sys/stat.h>
#include <utime.h>
#include <sys/types.h>
#include <unistd.h>
#include <errno.h>

int main (int argc, char *argv[])
{
    struct utimbuf
        times;
    struct stat
        buf;

    int status;
    stat(argv[1], &buf);

    cout << "Current access time of file " << argv[1] <<
         << " is " << ctime(&buf.st_atime) << endl;
    cout << "Current modification time is " <<
         << ctime(&buf.st_mtime) << endl;

    if(status = utime(argv[1], NULL) != 0) {
        perror("utime failure");
    }
    stat(argv[1], &buf);

    cout << "New access time of file " << argv[1] <<
         << " is " << ctime(&buf.st_atime) << endl;
    cout << "New modification time is " <<
         << ctime(&buf.st_mtime) << endl;
}
```

示例 4-15 中的程序利用 `stat` 例程根据命令行调用确定的当前的访问时间和修改时间。`utime` 例程从 `time_t` 数据类型元素显示时间。显示了文件的当前访问时间和修改时间。此处演示的第二个参数设置为 0 的 `utime` 将文件的修改时间和访问时间设置为当前时间。

## 总结

| 函数 | UNIX | Microsoft Windows | 页码 |
| --- | --- | --- | --- |
| 标准 I/O 例程 | `open` | `open` | 104 |
| | `read` | `read` | |
| | `write` | `write` | |
| | | `close` | |
| 同步文件访问 | | `CreateFile` `ReadFile` `WriteFile` `CloseHandle` | 107 |
| 异步文件访问 | AIO 例程 | `ReadFileEx` `WriteFileEx` | 136 112 |
| 使用回调函数的访问 | AIO 例程 | `ReadFileEx` `WriteFileEx` `SleepEx` | 136 112 |
| 文件锁定 | `fcntl` | `LockFile` `UnlockFile` | 139 115 |
| 目录和设备操作 | | `CreateDirectory` `RemoveDirectory` `GetFullPathName` `GetDeviceType` `SetVolumeInformation` | 118 |
| 文件变化通知 | | `FindFirstChangeNotification` `FindNextChangeNotification` | 118 |
| 文件操作 | | `MoveFile` `CopyFile` | 120 |
| 文件定位 | `seek` | `SetFilePointer` | 143 |
| 文件时间 | `stat` | `SetFileTime` | 145 |
| 内存映射文件 | `mmap` `munmap` | `CreateFileMapping` `UnmapViewOf` | 145 |
| 搜索文件 | | `FindFirstFile` | 132 |
| 函数 | UNIX | Microsoft Windows |
| --- | --- | --- |
| 获取文件信息 | `stat`, `lstat` | `GetFileInformationByHandle` | 133 |

## 使用内存

- ANSI C 内存例程 156
- Microsoft Windows 例程 159
- Microsoft Windows 堆例程 177
- 附加内存 181

# ANSI C 内存程序 157

反映了目前为止分配的总内存，显示十个 100 整数缓冲区占用了 +40,000 字节。这说明了潜在的内存泄漏情况。可以想象，如果我们使用 `malloc` 来接收来自 `calloc` 的地址指针，那么指向原始内存分配的指针将会丢失，且 `free` 调用将无法将所有内存归系统。随着时间的推移，内存泄漏可能会损害系统的整体运行，因此需要仔细设计程序来处理这些情况。

# 示例 5-1 使用 malloc、realloc、calloc 和 free 的基本内存分配例程序的演示

```c
#include <stdlib.h>
#include <stdio.h>
#include <malloc.h>

void main( void )
{
    size_t size;
    int *membuf;

if (membuf = (int*)malloc( 1000 * sizeof( int )) == NULL)
    exit( 1 );

size = msize( membuf);
    printf("Size of block after malloc of 1000 ints: %u\n", size);

if (membuf = realloc( membuf, size + ( 1000 * sizeof( int )) == NULL)
    exit( 1 );

size = msize( membuf);
    printf("Size of block after realloc of 1000 more ints: %u\n", size);

if (membuf = calloc( 10, 1000 * sizeof( int )) == NULL)
    exit( 1 );

size = msize( membuf);
    printf("Size of block after calloc of 10 x 1000 ints: %u\n", size);

free(membuf);
    exit( 0 );
}
```

# C++ 的 new 和 delete 操作

虽然可以使用 ANSI 内存程序，但 C++ 支持使用 `new` 和 `delete` 运算符对对象进行自身的动态分配和释放。这些操作符从称为“自由存储”`free store` 的池中对象分配内存。自由存储在 C 中被称为堆 `heap`。`new` 运算符可以在运行时动态分配内存。`delete` 运算符用于释放用 `new` 运算符创建的对象。`delete` 运算符返回类型 `void`。`delete` 的参数必须是 `new` 运算符返回的指针。通过利用 C++ 的析构函数功能，可以设计程序来缓解内存泄漏。示例 5-2 展示了如何实现这一点。

# 示例 5–2 使用析构函数的 C++ 内存分配程序 new 和 delete 演示

```cpp
#include <iostream.h>
class somedata {
public:
    void filldata(int a, int b) { i=a;j=b; }
    ~somedata() { cout << "Cleaning up ...\n"; }
    int get_total() { return i+j; }
};
main()
{
    somedata *p;
    int i;

    p = new somedata[10];
    if(!p) {
        cout << "Unable to perform allocation ...\n";
        return 1;
    }

    for(i=0; i<10; i++)
        p[i].filldata(i, i);
    }

    for(i=0; i<10; i++) {
        cout << "Total " << i << " is: \n";
        cout << p[i].get_total() << "\n";
    }

    delete [] p;
    return 0;
}
```

析构函数用 `~` 前缀定义 `~somedata`。定义了一个两个整数值的数组。`filldata` 函数将工作变量 `i` 和 `j` 赋值为 `i` 的值。`get_total` 返回 `i` 和 `j` 相加的值，依次返回 0, 2, 4, 6, 8 等。此示例中的析构函数实际上显示了一条消息，但演示了在程序终止时可以做什么。

# Microsoft Windows 虚拟内存管理程序

Microsoft Windows 提供系列程序，允许程序员控制虚拟内存环境的性质。虽然这些程序旨在管理 Windows 内存环境的特定方面，但虚拟内存管理 `VMM` 程序在概念上与 ANSI 和 C++ 内存分配程序相同，允许内存的动态分配和释放。分配基于内存保留 `reserving` 和提交 `committing` 的操作，这将在下一步讨论。

虚拟内存管理的基本原理是，不需要整个进程同时存在于内存中，只需要当前执行所需的部分。随着执行的进行，进程的新部分会被带入内存，其他部分会被从内存中移除。有时，被移除的部分需要保存，因为它们包含了必须保留的数据。Windows 将进程阶段化在一个名为分页文件 `paging file` 的特殊系统文件中。分页文件中表示的进程地址空间的那部分被视为已提交 `committed`。也可以在不使用分页文件的情况下保留地址空间。在这种情况下，系统将防止其他进程使用该保留的地址范围，但在这些地址被提交之前，无法使用它们。

## VirtualAlloc 程序

`VirtualAlloc` 程序用于在调用进程的虚拟地址空间中保留并提交页区域。除非下文讨论的 `MEM_RESET` 标志，否则该程序分配的内存将初始化为 0。`VirtualAlloc` 程序具有以下序列：

```c
LPVOID VirtualAlloc (
  DWORD address,
  DWORD size,
  DWORD alloctype,
  DWORD protect );
```

参数 `address` 指定区域的起始地址。如果此参数传递 `NULL`，则系统将确定地址。`Size` 表示该区域的字节大小。参数 `alloctype` 指定分配类型，如表 5.2 所示。`Protect` 指定该区域的访问保护。

# 第 5 章内存操作

| 表 5.2 VirtualAlloc 分配类型 | 含义 |
| :--- | :--- |
| `MEM_COMMIT` | 在分页文件中分配物理存储。 |
| `MEM_RESERVE` | 保留地址空间范围但不分配物理内存。 |
| `MEM_RESET` | 声明区域的内容。 |

| 表 5.3 VirtualAlloc 保护标志 | 含义 |
| :--- | :--- |
| `PAGE_READONLY` | 允许对提交区域进行读取访问。 |
| `PAGE_READWRITE` | 允许对提交区域进行读取和写访问。 |
| `PAGE_EXECUTE` | 允许对提交区域进行执行访问。 |
| `PAGE_EXECUTE_READWRITE` | 允许对提交区域进行执行和写访问。 |
| `PAGE_GUARD` | 对提交区域的任何读取或写入尝试都会导致异常 |
| `PAGE_NOACCESS` | 禁止对提交区域的所有访问。 |
| `PAGE_NOCE` | 禁止对提交区域进行缓存。 |

| 表 5.4 VirtualFree 释放类型描述 | 含义 |
| :--- | :--- |
| `MEM_DECOMMIT` | 取消已提交页区域。尝试提交未提交的区域没有影响。 |
| `MEM_RELEASE` | 释放指定的保留页区域。如果指定，size 必须为 0；地址 必须是 VirtualAlloc 保留该区域时返回的基地址。 |

# 第 5 章内存操作

另一个进程的地址。例程 `VirtualFreeEx` 具有以下调用序列：

```
BOOL VirtualFreeEx (
  HANDLE process,
  LPVOID address,
  DWORD size,
  DWORD freetype
);
```

例程 `VirtualFreeEx` 比 `VirtualFree` 多了一个参数：执行操作所在进程的句柄。

## VirtualLock 例程

`VirtualLock` 例程用于指定进程虚拟地址空间中的某个内存区域，该区域不会产生页错误。`VirtualLock` 具有以下调用序列：

```
BOOL VirtualLock (
  LPVOID address,
  DWORD size
);
```

参数 `address` 表示要锁定页面区域的基地址，`size` 是要锁定区域的大小（以字节为单位）。该例程的意图是通过减少页错误发生的频率来提高性能，如果锁定了太多页面，可能会产生相反的效果。锁定过多页面会导致系统可用内存 减少。一个进程可以锁定的默认最大页数为 30。

## SetProcessWorkingSetSize 例程
