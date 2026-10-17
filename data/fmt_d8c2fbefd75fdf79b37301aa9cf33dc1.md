
# 线程特定数据 (Thread-Specific Data)

在许多多线程应用程序中，不同的线程想要访问一个所有线程都可以访问的变量，例如增加某些全局计数器时。然而，在某些情况下，线程可能想要使用一个变量，该变量的值取决于访问数据的是哪一个线程。

在 Linux 中，每当创建一个线程时，它也会为该线程创建一个唯一的存储区域，用于包含该线程特定的数据。该区域被称为线程特定数据区域（thread-specific data area）。

```pascal
type
  thread_key_t = Cardinal;
  TPThreadKey = pthread_key_t;
```

从线程特定数据区域存储和读取值是通过称为“键”（keys）的机制实现的。键是一个类型为 `TPThreadKey` 的实际值，可以被许多线程访问。数据实际上并不是从这个 `TPThreadKey` 读取或写入的，键被用作指向线程特定数据区域中特定值的索引。

为了在线程中使用键，`TPThreadKey` 变量需要在任何函数或类的作用范围之外声明，这样 `TPThreadKey` 才是可访问的，并贯穿应用程序的生命周期。

然而，键在被创建之前是无法使用的。键是通过调用 `thread_key_create` 创建的。

```pascal
type
  ThreadKeyDestructor = procedure(Value: Pointer); cdecl;
```

```pascal
function thread_key_create(var Key: TPThreadKey; Destructor: ThreadKeyDestructor): Integer;
```

`thread_key_create` 函数接受两个参数。第一个参数是 `TPThreadKey` 变量，将用于存储线程特定数据。第二个参数是在线程终止或取消时调用以清理分配给线程的任何内存的函数；该函数将在终止线程的上下文中被调用。

一旦使用 `thread_key_create` 创建了键，每个线程现在就可以分别使用 `pthread_getspecific` 和 `pthread_setspecific` 函数向键读取和写入它自己的数据。

```pascal
function pthread_setspecific(Key: TPThreadKey; Value: Pointer): Integer;
function pthread_getspecific(Key: TPThreadKey): Pointer; cdecl;
```

要为当前调用线程写入值，可以使用 `pthread_setspecific` 函数。`pthread_setspecific` 函数接受两个指针，第一个是 `TPThreadKey` 变量，第二个是将为调用线程存储的指针。线程特定键中可以存储的唯一数据是指针。由于指针可以指向任何类型的数据或结构，这意味着线程特定数据是非常灵活的。

从线程特定键中读取值也是一种简单的方法。要从键中读取，你只需要使用 `pthread_getspecific` 函数。该函数接受一个参数，返回调用线程的指针。返回的值将是有效指针，或者如果线程特定数据未由当前线程设置则为 `nil`。

一旦你完成了对线程键的使用，删除它就像调用 `pthread_key_delete` 一样简单。此函数仅接受一个参数，即 `TPThreadKey` 变量。使用此函数将调用键的析构函数，并应谨慎使用。

```pascal
function pthread_key_delete(Key: TPThreadKey): Integer;
```

所以你可能会问，在哪里使用线程特定数据？如果你查看了本章之前的示例，你会看到屏障（barrier）示例。在屏障示例中，我们知道有多少个线程被创建，所以初始化屏障是容易的。但如果不知道有多少个线程被创建呢？

函数库，如 Pascal 单元或共享对象，使用线程特定数据获益最大。在许多情况下，旧的函数是假设单元只会被单个线程使用的，因此变量是在单元中定义的。但对于那些需要多线程的遗留 Pascal 单元呢？示例 6.23 展示了如何修改示例 6.22 中的单元，使单元现在是线程安全的。

## 示例 6.22 一个并非为多线程设计的简单单元

```pascal
unit FunctionCaller;

interface
  procedure CallSomeProc;
  function HowManyTimesCalled: integer;

implementation
var
  __ManyTimesCalled: integer = 0;

procedure CallSomeProc;
begin
  // 执行某些操作
  // 增加该函数被调用的次数
  inc(__ManyTimesCalled);
end;

function HowManyTimesCalled: integer;
begin
  Result := __ManyTimesCalled;
end;
```

你可以看到，无论哪个线程调用函数，单元都会增加同一个变量 `__ManyTimesCalled`。为了让多个线程访问它们自己的计数，使用了线程键来存储它们自己的值。作为结果，我们可以更改函数的实现而无需更改函数的接口。这是假设有某些需要多线程的遗留 Pascal 单元。

## 示例 6.23 使用线程键的多线程版本库

```pascal
unit FunctionCallerCounter;

interface
  procedure CallSomeProc;
  function HowManyTimesCalled: integer;

implementation
uses
  Libc;

var
  HowManyTimesCalledKey: PThreadKey;
  RunOnce: integer = PTHREAD_ONCE_INIT;

procedure RemoveHowManyTimesCalledKey(ValueInKey: Pointer); cdecl; forward;

procedure CallSomeProc;
var
  Value: integer;
  Data: ^Integer;
begin
  // 执行某些操作
  // 增加该函数被调用的次数
  Data := Pointer(thread_getspecific(HowManyTimesCalledKey));
  If Data = nil then
    Value = 0
  else
    Value := Data^;
  inc(Value);
  // 让我们分配内存
  // 将新的键值存回
  If Data = nil then
    new(Data);
  Data^ := Value;
  pthread_getpecific(HowManyTimesCalledKey, Data);
end;
```

```pascal
function HowManyTimesCalled: integer;
var
  Data: ^Integer;
begin
  // 返回此函数在当前线程被调用的次数
  Data := thread_getspecific(HowManyTimesCalledKey);
  if Data = nil then
  begin
    // 还没有人调用此函数
    Result := 0;
  else
    Result := Data^;
end;
```

```pascal
{ Key 的析构函数 }
procedure RemoveManyTimesKeyValue(ValueIn: Pointer); cdecl;
begin
  // 此函数需要移除数据
  FreeMem(ValueIn, sizeof(integer));
end;

initialization
  pthread_key_create(HowManyTimesCalledKey, RemoveManyTimesKeyValue);
finalization
  pthread_key_delete(HowManyTimesCalledKey);
end.
```

# 信号与线程

单线程应用中的信号处理足够简单，但当涉及多个线程时，情况就会变得糟糕。单线程进程中的信号会有它自己的信号掩码和信号处理器。当引入多个线程时，由于 Linux 创建线程的方式，情况会变得有点复杂。

这是因为在 Linux 下，每个新创建的线程实际上都是一个进程，并将共享内存空间、文件描述符、工作目录和信号处理器。由于每个线程在内部都是一个进程，可以使用 `pthread_sigmask` 函数更改线程的信号掩码。该函数对进程的作用方式与 `sigprocmask` 类似。这意味着，如果信号发送给某个线程但并非所有线程都阻塞了该信号，信号仍然会通过。此外，当信号发送到进程时，最多只有一个线程会接收到信号。使用 `kill` 函数向进程组发送信号将让你能够向所有线程发送信号。

你还应该注意，在 LinuxThreads 环境下，发送到进程的信号会导致进程终止。像 `SIGKILL` 这样的信号就是此类。进程中的一个线程接收到这种类型的信号，所有线程都将被终止。其他信号不会导致线程终止，例如 `SIGALRM` 信号实际上会被发送到触发信号发送的线程。例如，从一个线程使用 `alarm` 函数将只会向该线程发送 `SIGALRM`。

在处理信号和 POSIX 线程时，另一个注意点是，某些 LinuxThreads 使用 `SIGUSR1` 和 `SIGUSR2` 信号来管理进程线程的挂起。因此，在多线程应用中使用这些线程并不是一个好主意。

混合信号和线程是可能的，但不建议这样做。如果你需要事件通知，通常使用同步方法更好，例如互斥锁（mutex）、信号量（semaphore）、屏障（barrier）或条件变量。如果你在多线程应用中避免使用信号，你的应用程序将会运行得更好。

# 与 CLX 的 TThread 对象集成

Kylix 中用于管理 POSIX 线程的许多函数依赖于 `pthread_create` 函数成功调用后返回的线程标识符。因此，处理 POSIX 线程就是一个使用此线程标识符并编写适当函数来实现所需效果的问题。

正如之前提到的，创建多线程应用是困难的，并且会为你的应用增加许多复杂性。如果你想减少多线程应用的复杂性，请使用 CLX 类 `TThread`，它封装了 POSIX 线程的大部分功能，与直接调用 POSIX 线程函数相比，它非常简单。`TThread` 的支持并不具备 POSIX 线程的所有功能，在某些情况下，你可能想在 POSIX 调用和 `TThread` 类之间混合代码。

`TThread` 类的 `ThreadId` 属性用于获取传递给任何需要线程标识符的 POSIX 线程函数。可以在 6.24 节 `TPOSIXThread` 的 `SendSignal` 方法中看到。

某些 POSIX 函数仅对调用线程有效，例如 6.24 节 `SigMask` 和 `KillTheOtherThreads` 方法中列出的 `pthread_sigmask` 和 `kill_other_threads_np` 函数。与其获取线程的 `ThreadID`，不如只在线程的上下文中进行调用。在这个示例中，POSIX 函数中的调用代码必须在当前线程执行，因此被放置在保护区域中，以便它们只能由该类及其任何后类调用。这应该确保 `SigMask` 和 `KillTheOtherThreads` 函数仅在调用线程的上下文中被调用。

## 6.24 - 扩展 TThread 的行为

```pascal
unit POSIXThread;

(*
此类演示了我们如何通过使用一些 POSIX 线程函数
扩展普通的 TThread 类。
*)

interface
uses Classes, Libc;

type
  POSIXThread = class(TThread)
  protected
    // 杀死所有其他线程
    procedure KillTheOtherThreads;
    // 处理当前线程信号掩码的方法
    function SigMask(How: Integer; newMask: PSigset; OldMask: PSigset): integer;
  public
    // 向此线程发送信号
    function SendSignal(SignNum: integer): integer;
  end;
```

```pascal
implementation

procedure POSIXThread.KillTheOtherThreads;
begin
  // 杀死应用程序中除调用线程外的所有线程。
  kill_other_threads_np;
end;
```

```pascal
function POSIXThread.SendSignal(SignNum: integer): integer;
begin
  // 此函数将向线程发送信号。
  // 这使用 TThread 的 Handle 属性来获取标识符
  Result := pthread_kill(Handle, SignNum);
end;
```

```pascal
function POSIXThread.SigMask(How: Integer; newMask: PSigset; OldMask: PSigset): integer;
begin
  // 此函数仅为调用线程进行了封装。
  Result := pthread_sigmask(How, newMask, OldMask);
end;
```

你应用程序中对线程的大部分支持都包含在 `TThread` 类中。寻找使用 POSIX 特性扩展 `TThread` 类的方法，而这些功能已经存在了。当你想要混合 `TThread` 和 POSIX 线程函数，可能是为了添加信号量、互斥锁、条件变量等功能。

# API 参考

## `__pthread_initialize` LibC.pas

### 语法

```pascal
procedure __pthread_initialize;
```

### 描述

`__pthread_initialize` 函数将初始化 LinuxThreads 库。通常它不会调用此函数，因为当你第一次创建线程时，库会自行初始化。

### 另请参

`pthread_create`

## `_pthread_cleanup_pop` LibC.pas

### 语法

```pascal
procedure _pthread_cleanup_pop(var Buffer: TThreadCleanupBuffer; Execute: Integer);
```

### 描述

每个线程都可以包含一个在线程取消或退出时调用的函数列表。`_pthread_cleanup_pop` 函数将移除顶部的清理处理器。

该函数提供了在从列表中移除之前执行清理处理器的机会。

### 参数

- **Buffer**: Buffer 参数是一个 `TThreadCleanupBuffer` 变量，它实际上是一个包含当前线程清理函数的链表。当线程取消或退出时，存储在列表中函数将被执行。此参数是当前线程使用的缓冲区，其顶端元素将被移除。
- **Execute**: 此参数决定在从列表顶部移除之前是否执行清理处理器。将此参数设置为非零值将导致执行清理函数。将此参数设置为 0 将导致不执行该函数。

### 另请参

`_thread_cleanup_push`, `_thread_cleanup_push_defer`, `_thread_cleanup_restore`

## `_thread_cleanup_pop_restore` LibC.pas

### 语法

```pascal
procedure _thread_cleanup_pop_restore(
  Buffer: PThreadCleanupBuffer;
  Execute: Integer
);
```

### 描述

`_thread_cleanup_pop_restore` 函数的行为与 `_thread_cleanup_pop` 函数相同，然而，它会从清理列表中移除顶部的清理处理程序。然而，此函数用于恢复当前线程的取消状态，该状态之前由于调用了 `_thread_cleanup_push` 被设置为延迟取消。

### 参数

- **Buffer**: Buffer 参数是一个 `TPthreadCleanupBuffer` 变量，它实际上是一个包含当前线程清理函数列表的链表。当线程取消或退出时，将执行存储在该列表中的函数。此参数是当前线程使用的缓冲区，其最顶部的元素将从列表中移除。
- **Execute**: 此参数决定了在从列表顶部移除清理处理程序之前是否执行它。将此参数设置为非零值将导致执行清理函数。将此参数设置为 0 则将不执行该函数。

### 另请参

`_thread_cleanup_push`, `_thread_cleanup_push_defer`, `_thread_cleanup_pop`
