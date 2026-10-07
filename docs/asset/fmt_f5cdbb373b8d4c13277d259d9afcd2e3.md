
```c
if ((shmidy=shmget(keyy, 10, IPC_CREAT|0644)) == -1) {
    perror("shmget error");
    exit(1);
}

mptr = (pthread_mutex_t*)shmat(shmidx, (void *)0, 0);
cvptr = (pthread_cond_t*)shmat(shmidy, (void *)0, 0);

pthread_mutexattr_init(&mutex_shared_attr);
pthread_mutexattr_setpsared(&mutex_shared_attr, PTHREAD_PROCESS_SHARED);
status = pthread_mutex_init(mptr, &mutex_shared_attr);
if(status != 0) {
    perror("mutex failure");
    exit(2);
}

pthread_condattr_init(&cv_shared_attr);
pthread_condattr_setpsared(&cv_shared_attr, PTHREAD_PROCESS_SHARED);
status = pthread_cond_init(cvptr, &cv_shared_attr);
if(status != 0) {
    perror("conditional variable failure");
    exit(2);
}

fid = open("shared.file",O_RDWR);

if(mapView = (char*)mmap((caddr_t)0, 100, PROT_READ|PROT_WRITE, MAP_SHARED, fid, 0)) == ((caddr_t)-1) {
    perror("mmap failure");
    exit(3);
}

tmp = mapView;

cout << "Contents of shared file before P2 makes changes " << endl;
cout << mapView;
cout << "\Tell P2 to start ..." << endl;

if((status = pthread_cond_signal(cvptr) != 0))
    perror("condition variable signal error");
    exit(2);

cout << "mptr = " << mptr << " cvptr = " << cvptr << " <<" << endl;
cout << "Wait for P2 to say file changed ..." << endl;
```
```cpp
pthread_mutex_lock(mptr);

if(status=pthread_cond_wait(cvptr, mptr) != 0) {

    perror("condition variable wait error");

    exit(2);

}

pthread_mutex_unlock(mptr);

cout << "Now display changed contents" << endl;

cout << mapView;

for(i=0; i<=9; i++) {

    mapView[i]='X';

}

cout << "\nTell P1 can now look at changed file ..." << endl;

cout << " ... hit RETURN when ready ..." << endl;
```
```cpp
cin.getline(ret,100);

munmap((caddr_t)0, 100);

if((status = pthread_cond_signal(cvptr) != 0))
    perror("condition variable signal error");
    exit(2);

shmctl(shmidx, IPC_RMID, (struct shmid_ds *) 0);
shmctl(shmidy, IPC_RMID, (struct shmid_ds *) 0);

exit(0);
```

## 总结

| Function | UNIX | Microsoft Windows | Page |
| --- | --- | --- | --- |
| ANSI C standard routines | malloc calloc realloc free alloca | malloc calloc realloc free alloca | 156 156 |
| Heap management routines | — | HeapAlloc HeapFree HeapReAlloc HeapSize HeapValidate HeapCreate HeapLock Unlock | — 177 |
| Virtual memory management | mctl memctl mlock munlock | VirtualAlloc VirtualFree VirtualProtect ProcessWorkingSetSize | 181 159 |
| Acquire memory management information | getpagesize | GlobalMemoryStatus GetSystemInfo | 184 166 |
| Shared memory routines | — | shget shctl shmop | — 185 |

## 网络与其他通信机制

### 章目标

- 基础 Windows 通信....... 194
- Microsoft Windows 和 UNIX TCP/UDP通信........ 203
- UNIX 无名管道........ 213
- UNIX 命名管道........ 214
- UNIX 消息服务........ 217

> 网络是今天所有计算机系统中不可或缺的一部分。由于进程间通信是网络的近亲，它在本章中也将被讨论。这种区分是值得的；因为某些形式的进程间通信并不依赖于使用 TCP/IP 等协议的网络。

UNIX 和 Microsoft Windows 都提供了许多执行网络和进程间通信任务的。通过在 Windows 中使用 winsock 库，可以灵活地编写在 UNIX 和 Microsoft Windows 环境之间运行的面向 TCP 或 UDP 的客户端/服务器程序。

本章根据此方向进行分类，并在表 6.1 中表示。

**表 6.1** Windows 和 UNIX 通信与网络设施分类

| 连接面向型 | 无连接面向型 |
| :--- | :--- |
| Windows | UNIX | Windows | UNIX |
| 命名管道 | 命名管道 | 邮件槽 | 无名管道 |
| 通过 winsock 的 TCP | TCP | 通过 winsock 的 UDP | TCP |

## Windows Windows 通信

Microsoft Windows 提供了连接面向型和无连接面向的通信设施，包括邮件槽、命名管道，以及通过 winsock 库实现的 UDP 和 TCP 网络通信。

### 邮件槽 (Mailslots)

邮件槽是一种无连接面向的通信机制。邮件槽通信无法跨越网络路由器进行工作，必须在位于连续网段的机器上使用。通过 `CreateMailslot` 例程创建邮件槽，其调用序列如下：

```cpp
HANDLE CreateMailslot(
  LPCTSTR name,
  DWORD msgsize,
  DWORD timeout,
  LPSECURITY_ATTRIBUTES secattr
);
```

邮件槽对象对于创建它的机器是局部的。`name` 参数指向一个以 NULL 终止的字符串，该字符串必须符合以下语法：

```
\\mailslot\[path]name
```

`name` 字段必须是唯一的，并可以包含由反斜杠创建的多个级伪目录。例如，`\\mailslot\\mymailslot` 和 `\\mailslot\\va2mymailslot` 是有效名称。`name` 参数指定发送到邮件槽的单条消息的最大尺寸（以字节为单位）。将此参数设置为 0 意味着消息可以是任意大小。`timeout` 参数可以设置为两个值之一：0，意味着如果没有消息则立即返回；或者 `MAILSLOT_WAIT_FOREVER`，意味着无限等待消息的出现。`timeout` 特性适用于从该邮件槽进行的所有后续读取操作。最后一个参数 `secattr` 指向一个安全属性结构，该结构将在下一章中讨论。

要向邮件槽写入内容，您需要使用 `CreateFile` 例程并根据表 6.2 指定邮件槽名称。

**表 6.2** 邮件槽名称与 `CreateFile` 例程的关联用法**

| 格式 | 用法 |
| :--- | :--- |
| \\.\mailslot\name | 获取本地邮件槽的客户端句柄 |
| \\computer\mailslot\name | 获取远程邮件槽的客户端句柄 |
| \\domainname\mailslot\name | 获取指定域内所有指定名称的邮件槽的客户端句柄。写入限制为 400 字节 |
| \\*\mailslot\name | 获取系统主域内所有指定名称的邮件槽的客户端句柄。写入限制为 400 字节 |

可以使用 `MailslotInfo` 例程来获取有关指定邮件槽的信息，其调用序列如下：

```cpp
BOOL GetMailslotInfo(
  HANDLE mailslot,
  DWORD maxmsgsize,
  DWORD nextsize,
  DWORD msgcnt,
  DWORD readto
);
```

`mailslot` 参数代表邮件槽的句柄。如果调用者对此调用返回的任何信息都不感兴趣，可以将任何一个参数设置为 NULL。`maxmsgsize` 参数指向一个位置，该位置将返回返回该邮件槽的最大消息尺寸（以字节为单位）。此值可以大于或等于 `CreateMailslot` 调用中使用的 `msgsize` 参数所指定的值。`nextsize` 参数指向一个位置，该位置将返回返回下一条消息的大小（以字节为单位）。如果没有下一条消息，则返回 `MAILSLOT_NO_MESSAGE`。参数 `msgcnt` 指向一个位置，该位置将返回函数返回时等待被读取的消息总数。参数 `readto` 指向一个位置，该位置将返回在发生超时之前，读取操作可以等待消息写入邮件槽的时间（以毫秒为单位）。示例 6-1 通过展示一个发送者-接收者进程演示了邮件槽的使用。由于使用了相同的邮件槽名称，这些程序被配置为在同一台机器上运行。在一个 MS-DOS 中运行发送者，在另一个 MS-DOS 中运行接收者。接收者将简单地等待来自发送者的消息。发送者将提示您输入要发送给接收者的消息，接收者将回显该消息。

示例 6–1 使用邮件槽 API、发送者和接收者的演示

```cpp
// 邮件槽发送者 ...

#include <windows.h>
#include <iostream.h>
#include <string.h>

int main(){
    char txt2nd[100];
    DWORD buflen=100, nbout;
    HANDLE hMailslot;
    BOOL status=hMailslot=CreateFile("\\\\mailslot\\myMsg", GENERIC_WRITE, FILE_SHARE_READ,
    (LPSECURITY_ATTRIBUTES) NULL, OPEN_EXISTING, FILE_ATTRIBUTE_NORMAL,
    (HANDLE) NULL);

    if (hMailslot == INVALID_HANDLE_VALUE)
    {
        cerr << "CreateFile failure: " << GetLastError() << endl;
        return (1);
    }

    for(;;)
    {
        cout << "Enter text string to send: ";
        cin >> txt2nd;
        cout << "Mail call!" << endl;
        status=WriteFile(hMailslot, txt2nd, (DWORD) strlen(txt2nd)+1, &nbout,
        (OVERLAPPED) NULL);

        if (!status)
        {
            cerr << "WriteFile failure: " << GetLastError() << endl;
            CloseHandle(hMailslot);
            return (1);
        }
    }
}
```

### Windows 通信

示例 6–1 使用邮件槽 API、发送者和接收者的演示（续）

```cpp
// 邮件槽接收者 ...

#include <windows.h>
#include <iostream.h>

int main()
{
    HANDLE hMailslot;
    DWORD nxtsz, messages, nread;
    BOOL status;
    char txt2nd[80];

    hMailslot=CreateFile("\\\\mailslot\\myMsg", GENERIC_READ, FILE_SHARE_READ,
    (LPSECURITY_ATTRIBUTES) NULL, OPEN_EXISTING, FILE_ATTRIBUTE_NORMAL,
    (HANDLE) NULL);

    if (hMailslot == INVALID_HANDLE_VALUE)
    {
        cerr << "CreateFile failure: " << GetLastError() << endl;
        return (1);
    }

    for(;;)
    {
        status=GetMailslotInfo(hMailslot, 0, &nxtsz, &messages, &nread);
        if (!status)
        {
            cerr << "GetMailslotInfo failure: " << GetLastError() << endl;
            CloseHandle(hMailslot);
            return (1);
        }

        if (!ReadFile(hMailslot, txt2nd, nxtsz, &nread,
        (OVERLAPPED) NULL))
        {
            cerr << "ReadFile failure: " << GetLastError() << endl;
            CloseHandle(hMailslot);
            return (1);
        }
        cout << txt2nd << endl;
        Sleep(1000);
    }
}
```

### Microsoft Windows 命名管道

命名管道为两个进程之间提供面向连接通信路径。与邮件槽不同，命名管道可以在广域网上通信。

#### CreateNamedPipe API

命名管道在服务器进程中通过调用 `CreateNamedPipe` 创建，其调用序列如下：

```cpp
HANDLE CreateNamedPipe(
  LPCTSTR name,
  DWORD openmode,
  DWORD pipodem,
  DWORD maxinstances,
  DWORD outbufsize,
  DWORD inbufsize,
  DWORD deftimout,
  LPSECURITY_ATTRIBUTES secattr
);
```

`name` 参数指向一个以 NULL 终止的字符串，该字符串唯一标识管道。字符串名称必须具有以下语法：

\\.\pipename

`pipename` 部分可以包含反斜杠以外的任何字符，包括数字和特殊字符。整个管道名称字符串可以长 256 个字符。管道名称不区分大小。`openmode` 参数根据表 6.3 表征访问模式、通过模式、重叠模式和安全模式。

`pipe` 参数指定管道句柄的类型、读取和等待模式。表 6.4 列出了 `pipe` 可能的所有不同值。`instances` 参数代表可以为此管道创建的最大实例数（副本）。所有实例必须指定相同的数量。可以创建的管道实例数量限于系统资源的可用性。`outbufsize` 和 `inbufsize` 代表为输出和输入缓冲区保留的字节数。命名管道每个端实际保留的缓冲区是系统默认值、最小或最大值或向上到下一个分配边界的指定尺寸。`deftimout` 参数在 `WaitNamedPipe` 函数指定 `WAIT_USE_DEFAULT` 时指示超时值（毫秒），这对于所有管道实例必须相同。`secattr` 参数指定与命名管道关联的安全属性结构。该参数的细节将在第 7 章中讨论。

## Windows 基础通信 199

| 表 6.3 CreateNamedPipe API 的 openmode 参数设置 | |
|---|---|
| 模式 | 含义 |
| 访问模式^1 | |
