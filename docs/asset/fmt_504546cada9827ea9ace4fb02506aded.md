
```c
#include <windows.h>
#include <stdio.h>

void ScanDir(char *dirname, int indent)
{
    BOOL fFinished;
    HANDLE hList;
    TCHAR szDir[MAX_PATH+1];
    TCHAR szSubDir[MAX_PATH+1];
    WIN32_FIND_DATA FileData;

    // 获取正确的目录路径
    sprintf(szDir, "%s*", dirname);

    // 获取第一个文件
    hList = FindFirstFile(szDir, &FileData);
    if (hList == INVALID_HANDLE_VALUE)
    {
        printf("No files found\n\n");
    }
    else
    {
        // 遍历目录结构
        fFinished = FALSE;
        while (!fFinished)
        {
            // 检查对象是否为目录
            if (FileData.dwFileAttributes & FILE_ATTRIBUTE_DIRECTORY)
            {
                if (strcmp(FileData.cFileName, ". ") != 0 &&
                    strcmp(FileData.cFileName, ".. ") != 0)
                {
                    printf("%s%s\n", indent, "    " * indent, FileData.cFileName);
                    // 获取子目录的完整路径
                    sprintf(szSubDir, "%s\\%s", dirname, FileData.cFileName);
                    ScanDir(szSubDir, indent + 4);
                }
            }
            else
                printf("%s%s\n", indent, "    " * indent, FileData.cFileName);

            if (!FindNextFile(hList, &FileData))
            {
                if (GetLastError() == ERROR_NO_MORE_FILES)
                {
                    fFinished = TRUE;
                }
            }
        }
        CloseHandle(hList);
    }
}
```

```
}
}
FindClose(hList);
}
void main(int argc, char *argv[])
{
    char *pszInputPath;
    char pwd[2] = ".";

    if (argc < 2)
    {
        printf("Argument not supplied - using current directory.\n");
        pszInputPath = pwd;
    } else
    {
        pszInputPath = argv[1];
        printf("Input Path: %s\n\n", pszInputPath);
    }

    ScanDir(pszInputPath, 0);

    printf("\ndone.\n");
}
```

# 352 UNIX 应用指南

```c
memset(buffer, '\0', sizeof(buffer));
if (pipe(file_pipes) == 0) {
    data_out = write(file_pipes[1], data, strlen(data));
    printf("W %d bytes\n", data_out);
    data_in = read(file_pipes[0], buffer, BUFSIZ);
    printf("Read %d bytes: %s\n", data_in, buffer);
    exit(EXIT_SUCCESS);
}
exit(EXIT_FAILURE);
```

## Win32 示例：低级管道调用

```c
#include <windows.h>
#include <stdlib.h>
#include <stdio.h>
#include <io.h>
#include <fcntl.h>
#include <process.h>
```

```c
void main() {
    size_t data_out, data_in;
    int file_pipes[2];
    const char data[] = "ABCDE";
    char buffer[BUFSIZ + 1];

    memset(buffer, '\0', sizeof(buffer));
    if (_pipe(file_pipes, 32, _O_BINARY) == 0) {
        data_out = write(file_pipes[1], data, strlen(data));
        printf("W %d bytes\n", data_out);
        data_in = read(file_pipes[0], buffer, BUFSIZ);
        printf("Read %d bytes: %s\n", data_in, buffer);
        exit(EXIT_SUCCESS);
    }
    exit(EXIT_FAILURE);
}
```

## 更多管道示例

为了帮助你理解使用管道进行进程间通信的应用程序中所需的更改，附录中包含了另外两个示例。它们是：

- 附录 9.5：跨进程的管道
- 附录 9.6：作为标准输入/输出的管道

## 命名管道 (FIFOs)

上一节涵盖了进程管道。在本节中，展示了几个命名管道的示例。它们有时被称为先进先出（FIFO）。

## 第 9 章：Win32 代码转换

## 使用命名管道进行进程间通信

为了展示如何将使用 FIFO 的 UNIX 代码转换为 Windows 代码，这里有一个创建一个命名管道的简单示例。为了简单起见，该示例使用了最少的安全限制。该示例在 UNIX 中使用 `mkfifo` 函数，而在使用 Win32 时使用 `CreateNamedPipe` 函数。这两个函数之间存在显著差异。然而，这两个函数的目的是相同的，即 `CreateNamedPipe` 函数对管道的配置提供了更大程度的控制。详细细节超出了本指南的范围，但你可以在 MSDN 网站上找到 `CreateNamedPipe` 的链接。

可以在以下附录中查看完整示例：

- 附录 9.8：创建命名管道
- 附录 9.9：打开 FIFO
- 附录 9.10：使用 FIFOs 进行进程间通信

## 消息队列

Microsoft Win32 默认并不支持消息队列。如果你想在应用程序中使用消息队列，应该使用微软消息队列（也称为 MSMQ）。消息队列在其他微软文档中有有详尽介绍，因此在此仅进行简要描述。

> 注意：有关消息队列的更多信息，请参阅 http://microsoft.com/msmq/default.htm。

消息队列允许运行在不同时间的应用程序跨异构网络和可能临时离线的系统进行通信。应用程序向队列发送消息并从队列中读取消息。消息队列提供了保证的消息投递、高效的路由、安全性以及基于优先级的消息。它可以用于实现需要高性能的异步和同步场景解决方案。

## Sockets 与网络

Windows Sockets 2 使用了最初由伯克利软件发行版 (BSD) UNIX 流行的套接字模型。后来被适配到 Microsoft Windows 并在 Windows Sockets 1.1 中。

Winsock 的主要目标之一是提供一个协议无关的接口，完全能够支持新兴的网络能力，例如实时多媒体通信。

Winsock 是一个接口，而不是协议。作为一个接口，它被用于发现和利用任意底层传输协议的通信能力。因为它不是协议，所以它不会以任何方式影响线缆上的比特位，也不需要在这通信链路的两端使用。

Windows Sockets 编程以前集中在 TCP/IP。某些适用于 TCP/IP 的编程实践并不适用于所有协议。因此，Winsock API 在需要时添加了新函数来处理多种协议。

Winsock 改变了其架构，以便更方便地访问多个传输协议。遵循 Windows 开放系统体系 (WOSA) 模型，Winsock 现在在应用程序接口 (API) 与协议栈之间定义了一个标准的服务提供接口 (API)，其函数从 `Ws_32.dll` 导出。因此，Winsock 的支持不再局限于 Windows Sockets 1.1 那样的 TCP/IP 协议栈。更多信息请参阅 Microsoft Visual Studio 中关于“Windows Sockets 2 Architecture”的讨论。

开发 Windows Sockets 2 应用程序面临新的挑战。当套接字仅支持 TCP/IP 时，开发者可以创建一个仅支持两种套接类型的应用程序：无连接和面向连接。无连接协议使用 `SOCK_DGRAM` 套接字，面向连接的协议使用 `SOCK_STREAM` 套接字。这些只是新套接字类型中的两种。此外，开发者不再依赖套接字类型来描述传输协议的所有本质属性。

Sockets 不是 Win32 库的一部分。你需要咨询平台 SDK 以获取有关 Winsock API 的详细信息。平台 SDK 的在线帮助包含完整的示例，演示了如何实现基于套接字的客户端和服务器应用程序。要对 UNIX 套接字和 Winsock 进行深层比较，请参阅 Microsoft Platform SDK 中关于“Socket Programming Considerations”的讨论。

## 进程环境

进程环境包含几个关键元素，在此处进行了解释。也简要描述了这些元素在 Windows 中的显著差异。本节仅讨论 POSIX。

## 环境变量

每个进程都有与其关联的环境块。环境块是分配在进程地址空间内的一个内存块。每个块包含一组键值对。UNIX 和 Windows 都支持进程环境块。具体的差异取决于你所处理的 UNIX 供应商和版本。有关你可以用于比较的信息，请参阅 MSDN 文章“Changing Environment Variables”，http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dllproc/529f

还提供了 Win32 和 POSIX 环境变量之间的差异总结。

## POSIX 与 Win32 环境变量的区别

Win32 支持 ANSI 版本以及 Unicode 变体。Unicode 变体以 `_w` 前缀开头。在应用程序中使用 `_w` 前缀有助于确保编译时链接到正确的变体。除了 `putenv` 和 `getenv` 等 ANSI 函数外，Win32 还支持 `GetEnvironmentVariable`、`ExpandEnvironmentStrings` 和 `SetEnvironmentVariable` 函数。此示例仅显示 ANSI 函数，并提供了从 UNIX 代码 Win32 代码的简单方法。

以下是访问环境块的简单示例。该示例在 POSIX 和 Win32 中同样有效。

```c
#include <stdlib.h>
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])
{
    char *var, *value;

    if(argc == 1 || argc > 3) {
        fprintf(stderr,"usage: environ var [value]\n");
        exit(1);
    }
    var = argv[1];
    value = getenv(var);
    if(value) {
        printf("Variable %s has value %s\n", var, value);
    } else {
        printf("Variable %s has no value\n", var);
    }
    if(argc == 3) {
        char *string;
        value = argv[2];
        string = (char *)malloc(strlen(var)+strlen(value)+2);
        if(!string) {
            fprintf(stderr,"out of memory\n");
            exit(1);
        }
        strcpy(string,var);
        strcat(string,"=");
        strcat(string,value);
        printf("Calling putenv: %s\n",string);
        if(putenv(string) != 0) {
            fprintf(stderr,"putenv failed\n");
        }
    }
}
```

```c
free(string);
exit(1);

value = getenv(var);
if(value)
    printf("New value of %s is %s\n", var, value);
else
    printf("New value of %s is null??\n", var);

exit(0);
```

# 临时文件

UNIX 和 Win32 都支持创建临时文件的函数。以下示例在 UNIX 和 Win32 中同样有效，无需修改。

`tmpnam()` 函数返回指向临时文件名的指针。`tempname` 函数也这样做，但你也可以用它来指定目录和文件名前缀。

```c
#include <stdlib.h>
#include <stdio.h>
```

```c
int main() {
    char tmpname[L_TMPNAM];
    char *filename;
    FILE *tmpfp;

    filename = tmpnam(tmpname);

    printf("Temporary file name is: %s\n", filename);

    tmpfp = tmpfile();
    if(tmpfp) {
        printf("Opened a temporary file OK\n");
        exit(0);
    } else {
        perror("tmpfile");
        exit(1);
    }
}
```

# 计算机信息

有时，有必要获取计算机信息。当应用程序设计为支持多个用户或不同类型的硬件和操作系统时，这一点尤为重要。应用程序所需的信息包括：

- 主机名
- 系统名称
- 计算机的网络级别
- 操作系统的发布级别
- 操作系统系统的版本号
- 硬件平台名称

在 UNIX 中，你可以结合使用 `hostname` 和 `uname` 来获取这些信息。使用 Windows 时，你可以选择使用 `hostname`，但 Win32 API 并不直接提供标准的 `uname`。可以通过 POSIX 层来添加 `uname`，该层具有获取一组与 `uname` 函数提供的信息类似的信息的功能。这些映射在本文中介绍，但建议考虑使用 Windows 管理规范 (WMI) API。WMI 接口具有高度可扩展性，不仅支持关于平台的静态信息，还支持配置和性能数据等动态信息。另一个可以考虑的源是 Active Directory 服务 (ADSI)，它是一个 COM 接口，便于访问存储在 Active Directory 数据库中的信息。这两种接口都是在 Windows 2000 及更高版本的计算机上收集信息的首选机制。以下示例中没有使用但非常有用的函数是 `GetVersionEx` 和 `GetVersionInfo`。

# UNIX 示例：使用系统信息

```c
#include <unistd.h>
#include <stdio.h>
#include <sys/utsname.h>

int main() {
    char computer[256];
    struct utname uts;

    if(uname(computer, &uts) != 0) {
        fprintf(stderr, "Could not get host information\n");
        exit(1);
    }

    printf("Computer host name is %s\n", computer);
    printf("System is %s %s\n", uts.sysname, uts.machine);
    printf("Nodename is %s\n", uts.nodename);
    printf("Version is %s, %s\n", uts.release, uts.version);
    exit(0);
}
```
