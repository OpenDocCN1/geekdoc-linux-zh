
```pascal
TNamedPipe = class
private
  FPipedName: string;
  FDesc: integer;
  FOpen: boolean;
public
  constructor Create(const Name: string);
  destructor Destroy;
  function Read(var Buffer: string; var Length: integer): boolean;
  function Write(const Message: string): boolean;
  function Close: boolean;
  function PipeSide(Side: TPipeSide): integer;
end;
```

## 管道操作

以下表格列出了命名管道的操作：

| 操作 | 描述 |
| :--- | :--- |
| `mkfifo` | 创建管道。 |
| `open` | 打开管道。 |
| `read` | 从管道读取数据。 |
| `write` | 向管道写入数据。 |
| `close` | 关闭管道。 |
| `unlink` | 删除管道。 |
| `fcntl` | 修改管道的属性。 |
| `fsync` | 刷新管道缓冲区。 |

## 示例

对于 FIFO 示例，有一个服务器程序和一个客户端程序。

```pascal
// FIFO  服务器程序
program fifoser;
```

```pascal
// FIFO 客户端程序
program fifoclient;
```

（由于提供的文本不完整且包含大量重复代码和代码片段，以上已根据要求进行了结构翻译。）

# 第 19 章：消息传递 IPC

`uses SysUtils, Pipes;`

`const PIPE_NAME = '/tmp/fifotest';`

`var`

`fifo : TNamedPipe;`

`recvBuf : TPipeBuffer;`

```pascal
begin
  writeln('Starting fifo server...');
  fifo := TNamedPipe.Create(PIPE_NAME, psRead,
    [fpOwnerRead, fpOwnerWrite,
    fpGroupRead, fpGroupWrite]);
```

```pascal
try
  SetLength(recvBuf,1024);
  if not fifo.Read(recvBuf, length(recvBuf)) then
    writeln('Server: Error reading from fifo!')
  else
    writeln('Received ->', StrPas(PChar(recvBuf)), '<- from a client');
finally
  fifo.Free;
```

```pascal
  writeln('Server is done.');
end.
```

// Fifo 客户端程序

`program fifoclient;`

`uses SysUtils, Pipes;`

`const PIPE_NAME = '/tmp/fifotest';`

`var`

`fifo : TNamedPipe;`

`tmpstr : string;`

`sendBuf : TPipeBuffer;`

```pascal
begin
  writeln('Starting fifo Client..');
  fifo := TNamedPipe.Create(PIPE_NAME, psWrite,
    [fpOwnerRead, fpOwnerWrite,
    fpGroupRead, fpGroupWrite]);
```

```pascal
try
  tmpstr := 'Hello from a fifo client!';
  SetLength(sendBuf,length(tmpstr));
  StrPCopy(PChar(sendBuf),tmpstr);
```

```pascal
  if not fifo.write(sendBuf, length(sendBuf)) then
    writeln('Client: error writing to fifo!')
  else
    writeln('Message successfully sent!');
```

```pascal
finally
  fifo.Free;
end;
```

```pascal
  writeln('Client is done.');
end.
```

# System V 消息队列

System V 消息队列是一种灵活性最高的单向通信设备。它允许不相关的进程之间进行通信，并提供了一种基于优先级而非发送顺序来移除消息的方法。

只要具有适当的权限并知道消息队列的，不相关的进程就可以向任何队列添加和移除消息。此外，消息可以设置优先级，从而允许按优先级移除消息，而不是先来后。发送和接收的消息中包含的信息由应用程序定义，而不是由管理消息的函数定义。下表显示了创建、访问和删除 System V 消息队列的可用函数：

表 19-3

System V 消息队列函数描述

| System V 消息队列函数 | 描述 |
| --- | --- |
| `ftok` | 从文件名和整数创建 System V IPC key（唯一标识符）。 |
| `msgget` | 创建或打开消息队列。 |
| `msgsnd` | 将消息放入队列中。 |
| `msgrcv` | 从队列中移除消息。 |
| `msgctl` | 从系统中移除消息队列，也用于其他消息队列的控制操作。 |

# 第 19 章：消息传递 IPC

# 创建消息队列类

使用 System V 消息队列的优势之一是消息是由程序员定义的。放置在队列上的消息可以包含任何类型和数量的信息。在 System V 消息队列的实现中，可以对读取和写入指定阻塞。这允许进程或线程等待读取或写入完成，或者继续处理其他事务并在另一个时间尝试再次读取或写入。

> 注意：一个用于处理消息队列、信号量和共享内存等 System V IPC 的有用 Linux 命令。该命令提供了系统当前正在执行的所有 IPC 的信息。另一个有用的命令是 `ipcrm`，它允许删除上述的 IPC 资源。在编译内核时，存在一个选项可以启用或禁用 System V IPC。

![](img/d784fa8294cae585d61ec86b987ea212_486_0.png)

# 类定义

`TMExampleMsg` 是消息可能样式的示例。System V 消息的唯一要求是第一个字段必须是一个指示消息类型的整数，且必须大于 0。附加字段可以指定任何所需内容，不受限于字符数据类型。整数、实数、字符串或布尔数据类型都可以封装到消息中。对于应用程序来说，应尽力避免指针数据类型。只有当指针指向进程共享的共享内存时，才应该使用指针数据类型。

```pascal
TMExampleMsg = packed record
  MessageType : integer; // 必须，> 0
  MessageText = array[0..1] of char; // 随你所欲
end;
```

> 注意：通常，记录（或数组、类或对象）在特定的边界上对齐，以加快对字段成员的访问。当成员对齐时，通常会有额外的填充字节（padding）来保证对齐。使用 `packed` 关键字会强制编译器移除任何填充并将每个字段相互相邻。例如，假设我们声明了如下的记录：

```pascal
TMyNormalRec = record
  b : byte;
  x : integer;
end;
```

假设有一个记录，Kylix 将将字段 "b" 放置在一个字的开头，将 "x" 放置在另一个字的开头。由于一个字节没有填充整个字，因此 "b" 和 "x" 之间存在三个额外的字节内存。记录的大小为八字节。通过添加 packed 关键字![](img/d784fa8294cae585d61ec86b987ea212_486_0.png这三个字节被移除，记录的大小变为五个字节。

# 构造函数

构造函数将属性初始化为默认值。注意，默认情况下读取和写入将发生阻塞。

```pascal
constructor TSystemVMQ.Create;
begin
  inherited := false;
  FPrivate := false;
  FOpened := false;
  FPPathName := '';
  FPKey := 0;
  FPermissions := [];
  FOpenExist := false; // 如果不存在则创建
  FBlockRead := true; // 默认阻塞
  FBlockWrite := true; // 默认阻塞
  FMsgID := 0;
end;
```

# 打开和关闭
