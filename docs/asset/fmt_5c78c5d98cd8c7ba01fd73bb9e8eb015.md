
`pipe(pipeID);`

```c
if(fork() == 0) { // 子进程
  read(pipeID[0], childBuf, len);
} else { // 父进程
  write(pipeID[1], msgChild, len);
}
```

以下代码片段说明了如何在 UNIX 中使用管道来实现图 2.8 所示的并发处理：

```c
int A_to_B[2], B_to_A[2];

main() {
  pipe(A_to_B);
  pipe(B_to_A);
  if (fork()==0) { /* 第一个子进程 */
    execve("prog_A.out", ...);
    exit(1);
  }
  if (fork()==0) { /* 第二个子进程 */
    execve("prog_B.out", ...);
    exit(1);
  }
  /* 父进程 */
  wait(...);
  wait(...);
}
```

```c
proc_A() {
  while (TRUE) {
    // 计算 A1
    write(A_to_B[1], x, sizeof(int)); // 使用此管道发送信息
    // 计算 A2
    read(B_to_A[0], y, sizeof(int)); // 使用此管道获取信息
  }
}
```

```c
proc_B() {
  while (TRUE) {
    read(A_to_B[0], x, sizeof(int)); // 使用此管道获取信息
    // 计算 B1
    write(B_to_A[1], y, sizeof(int)); // 使用此管道发送信息
    // 计算 B2
  }
}
```

### UNIX 中的非阻塞读取

任何文件、管道读端、文件描述符或套接字都可以通过 UNIX 中的 `ioctl()` 调用配置为非阻塞语义。在调用后，对流进行 `read()` 返回错误代码为 BSD 中的 `EWOULDBLOCK`（或 POSIX 中的 `EAGAIN`）。此外，`read()` 将返回 0 表示空。程序可以通过检查长度值是否非零来判断读取是否成功。以下代码片段说明如何使用 `ioctl()` 将管道读端从阻塞行为切换为非阻塞：

```c
#include <sys/ioctl.h>

int errno; /* 非阻塞读标志 */
...
main() {
  int pipeID[2];
  ...
  pipe(pipeID);
  /* 将管道读端切换到非阻塞模式 */
  ioctl(pipeID[0], FIONBIO, &on);
  ...
  while(..) {
    /* 轮询管道读端 */
    read(pipeID[0], buffer, BUFLEN);
    if (errno!=EWOULDBLOCK){
      /* 管道中有可用信息-处理它 */
    } else {
      /* 检查管道-执行其他操作 */
    }
  }
}
```

## Windows 中的匿名管道

Windows 也支持匿名管道。管道一旦创建，可以使用 `ReadFile()` 和 `WriteFile()` 对管道的两端进行读写。

## 练习 9.1 使用管道

你可以使用以下函数创建管道：

```c
BOOL CreatePipe(
    HANDLE hReadPipe,                // 句柄变量地址
    HANDLE hWritePipe,               // 写句柄变量地址
    LPSECURITY_ATTRIBUTES lpPipeAttributes, // 安全属性指针
    DWORD nSize                      // 为管道预留的字节数
);
```

你必须为读写句柄（`hReadPipe` 和 `hWritePipe`）分配空间，然后提供结果指针、安全属性以及建议的字节数 `nSize` 来实现管道（操作系统将该值作为确定实现管道所需内存的参数）。传递零是允许的，这意味着 Windows 将使用默认管道大小。如果你尝试读取空管道，`ReadFile()` 将阻塞调用线程，直到管道中有数据。如果你尝试向满管道写入，`WriteFile()` 将阻塞直到有空间可以写入字符。由于管道本质上是操作系统缓冲区（以文件形式打开），Windows 不支持 `seek` 操作。使用管道的挑战在于如何设置它们以便多个进程可以使用。第一个问题是匿名管道是由一个进程创建的，读写句柄位于该进程的地址空间中。另一个进程如何从创建进程获取文件句柄？将句柄从一个进程传递到另一个进程的标准技术是使用全局名称（匿名管道没有名称）、继承和句柄复制。

这是 Hart [1997] 使用的一种技术，利用了使用管道的进程是兄弟关系，共同父进程创建管道并传递重定向后的输入输出句柄：

```c
int main(int argc, char argv[]) {
    HANDLE readPipe, writePipe;
    SECURITY_ATTRIBUTES pipeSA;
    STARTUPINFO pStartInfo;
    ...
    // 创建管道
    pipeSA.nSize = sizeof(SECURITY_ATTRIBUTES);
    pipeSA.lpSecurityDescriptor = NULL;
    pipeSA.bInheritHandle = TRUE;
    if (!CreatePipe(&readPipe, &writePipe, &pipeSA, 0)) {
        fprintf(stderr, "...\n", GetLastError());
        ExitProcess(1);
    }
    // 创建写入进程
    // 将句柄设为可继承
    printf("Main: Creating process\n");
    ZeroMemory(&pStartInfo, sizeof(STARTUPINFO));
```

## 第九章 高层同步与进程间通信

```c
srcStartInfo.cb = sizeof(STARTUPINFO);
srcStartInfo.hStdInput = GetStdHandle(STD_INPUT_HANDLE);
srcStartInfo.hStdOutput = pfWritePipe;
srcStartInfo.hStdError = GetStdHandle(STD_ERROR_HANDLE);
srcStartInfo.dwFlags = START_USEHANDLES;
if(!CreateProcess(..., &srcStartInfo, ...)) {
    fprintf(stderr, "...", GetLastError());
    ExitProcess(1);
}
```
