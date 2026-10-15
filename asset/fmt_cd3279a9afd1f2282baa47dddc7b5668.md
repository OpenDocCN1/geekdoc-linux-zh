
```pascal
type
  TfmThreadDemo = class(TForm)
    bCanCancel: TCheckBox;
    Label: TLabel;
    cbCancelType: TComboBox;
    Label2: TLabel;
    btnCreateThread: TButton;
    btnCancelThread: TButton;
    tmrDisplayStatus: TTimer;
    lblStatusCounter: TLabel;
    procedure btnCreateThreadClick(Sender: TObject);
    procedure FormCreate(Sender: TObject);
    procedure FormDestroy(Sender: TObject);
    procedure tmrDisplayStatus(Sender: TObject);
    procedure btnCancelThreadClick(Sender: TObject);
  private
    { 私有声明 }
  public
    { 公共声明 }
    var
      ThreadID: TThreadId;
      Counter: Integer;
      CanCancel: Boolean;
      ImmediateCancel: Boolean;
      Mutex: pthread_rwlock_t;
      Attr: pthread_rwlockattr_t;
      procedure ThreadFunction(Data: Pointer);
  end;
```

```pascal
procedure TfmThreadDemo.btnCreateThreadClick(Sender: TObject);
begin
  btnCreateThread.Enabled := false;
  CanCancel := cbCancel.Checked;
  ImmediateCancel := cbCancelType.Item = 0;

  Counter := 0;
  pthread_rwlockattr_init(Attr);
  pthread_rwlockattr_setshared(Attr, PTHREAD_PROCESS_PRIVATE);
  pthread_rwlockattr_setkindnp(Attr, 0);
  pthread_rwlock_init(Mutex, @Attr);

  pthread_create(ThreadID, @Attr, @ThreadFunction, nil);
  tmrDisplayStatus.Enabled := true;
end;

procedure TfmThreadDemo.FormCreate(Sender: TObject);
begin
  tmrDisplayStatus.Enabled := false;
end;

procedure TfmThreadDemo.FormDestroy(Sender: TObject);
begin
  tmrDisplayStatus.Enabled := false;
  pthread_join(ThreadID);
  pthread_rwlock_destroy(Mutex);
  pthread_rwlockattr_destroy(Attr);
end;

procedure TfmThreadDemo.tmrDisplayStatus(Sender: TObject);
begin
  try
    pthread_rwlock_lock(Mutex);
    lblStatusCounter.Caption := IntToStr(Counter);
  finally
    pthread_rwlock_unlock(Mutex);
  end;
end;

procedure TfmThreadDemo.btnCancelThreadClick(Sender: TObject);
begin
  pthread_cancel(ThreadID);
end;

procedure TfmThreadDemo.ThreadFunction(Data: Pointer);
begin
  repeat
    pthread_setcancelstate(if ImmediateCancel then PTHREAD_CANCEL_ENABLE else PTHREAD_CANCEL_DISABLE, nil);
    if ImmediateCancel then
      pthread_setcanceltype(PTHREAD_CANCEL_ASYNRONUS)
    else
      pthread_setcanceltype(PTHREAD_CANCEL_DEFERRED);

    pthread_rwlock_lock(Mutex);
    inc(Counter);
    pthread_rwlock_unlock(Mutex);
    sleep(1000);
  until false;
end;

end.
```

# 第 6 章

## pthread_setschedparam

### 描述

`pthread_setschedparam` 函数用于更改由 `TargetThreadID` 参数指定的线程的调度策略和优先级。该线程可能的调度策略包括轮询调度（round robin）、先进先出（FIFO）调度和显式调度（explicit scheduling）。轮询调度和 FIFO 仅适用于以超级用户身份运行的进程，因为这些策略仅用于实时系统。

### 参数

- **TargetThreadID**: 此参数是将被更改其调度信息的线程的 ThreadID。

- **Policy**: 这是要为线程设置的调度策略。该参数的可用选项有用于轮询调度的 `SCHED_RR`、用于先进先出的 `SCHED_FIFO` 以及用于显式调度的 `SCHED_OTHER`。除这些值以外的任何值将导致函数失败并返回 `EINVAL` 错误。

```pascal
const
  SCHED_OTHER = 0;
  SCHED_FIFO = 1;
  SCHED_RR = 2;
```

- **Param**: 该参数是一个指向 `TSchedParam` 结构的指针，其中包含优先级值。`TSchedParam` 中 `sched_priority` 字段的值必须位于所用调度策略的最小值和最大值之间。调度策略的最小值和最大值可以通过 `sched_get_priority_min` 和 `sched_get_priority_max` 函数找到。

```pascal
type
  TSchedParam = record
    sched_priority: Integer;
  end;
```

### 返回值

如果函数执行成功，将返回 0。如果调度策略不是 `SCHED_OTHER`、`SCHED_FIFO`、`SCHED_RR`，或者优先级对于所使用的策略无效，则函数将返回 `EINVAL` 错误。如果调度被设置为 `SCHED_FIFO` 或 `SCHED_RR` 且进程未以超级用户身份运行，函数将返回 `EPERM` 错误代码。如果线程已被取消，函数还将返回 `ESRCH`。

### 另请参阅

`pthread_attr_setschedparam`, `pthread_attr_setschedpolicy`, `pthread_getschedparam`

### 示例

- 列表 6.34 - 使用 `pthread_setschedparam` 函数

```pascal
pthread_setschedparam(pthread_self, SCHED_RR,
sched_get_priority_min(SCHED_RR));
```

## pthread_setspecific LibC.pas

### 语法

```pascal
function pthread_setspecific(
  Key: TPThreadKey;
  Ptr: Pointer;
): Integer;
```

### 描述

在 POSIX 线程应用程序中，线程可以包含特定于调用线程的数据。这些线程特定数据使用 `TPThreadKey` 变量进行访问。与变量不同，线程特定数据需要通过 `pthread_get` 和 `pthread_setspecific` 接口函数进行访问。

`pthread_setspecific` 函数将为当前线程设置线程特定数据键的值。该函数仅存储作为 `Ptr` 参数传递的线程特定数据的指针。任何对 `pthread_specific` 函数的后续调用将返回传递给此函数的指针。

### 参数

- **Key**: 这是一个 `TPThreadKey` 变量，该变量是通过调用 `pthread_key_create` 函数创建的线程特定数据键。

- **Ptr**: 这是一个指向数据块的指针，该数据将被存储且仅可从当前线程访问。

### 返回值

如果函数执行成功，将返回 0。如果作为参数传递的 `TPThreadKey` 无效且未使用 `pthread_key_create` 初始化，则函数将失败。在这种情况下，函数将返回 `EINVAL` 错误代码。

### 另请参阅

`pthread_key_create`, `pthread_key_delete`, `pthread_getspecific`

### 示例

参见列表 6.23 - 使用线程键的多线程版本库。

## pthread_sigmask LibC.pas

### 语法

```pascal
function pthread_sigmask(
  How: Integer;
  const NewMask: PSigSet;
  OldMask: PSigSet;
): Integer;
```

### 描述

`pthread_sigmask` 函数将改变当前线程接受信号的方式。该函数类似于 `sigprocmask` 函数，但 `pthread_sigmask` 仅适用于当前调用线程而不是当前进程。该函数允许你精确定义当前线程将阻塞的信号、将信号集添加到阻塞线程列表中，以及从当前线程中移除阻塞信号。

### 参数

- **How**: `How` 参数定义要添加到当前列表的信号集。可能的值包括：`SIG_SETMASK`，意味着 `NewMask` 参数中的信号集将在当前线程阻塞；`SIG_BLOCK`，意味着 `NewMask` 参数中的信号集将添加到当前线程已阻塞的信号集中；以及 `SIG_UNBLOCK`，意味着传递给 `NewMask` 参数的信号集将从当前线程的信号集中移除。

- **NewMask**: 此参数是一个指向 `TSig` 信号集的指针。该参数与 `How` 参数配合使用，用于从当前线程的阻塞信号集中定义、添加或移除信号。

- **OldMask**: `OldMask` 参数是一个指向 `TSig` 变量的指针。当此参数不为 nil 时，调用此函数后，调用此函数之前的当前线程信号集将存储在该参数指向的 `TSigSet` 中。

### 返回值

如果函数执行成功，将返回 0。如果 `How` 参数不是 `SIG_SETMASK`、`SIG_BLOCK` 或 `SIG_UNBLOCK`，则函数将失败并返回 `EINVAL` 错误。

### 另请参阅

`pthread_kill`, `sigprocmask`, `sigaction`, `sigwait`

### 示例

参见列表 6.24 - 扩展的 pthread。

## pthread_spin_destroy LibC.pas

### 语法

```pascal
function pthread_spin_destroy(
  Lock: TThreadlock;
): Integer;
```

### 描述

`pthread_spin_destroy` 函数将销毁通过调用 `pthread_spin_init` 创建的自旋锁资源。在 Linux 实现中，此函数不执行操作并始终成功。

### 参数

- **Lock**: 有效的自旋锁。

### 返回值

无返回值。

## pthread_spin_init LibC.pas

### 语法

```pascal
function pthread_spin_init(
  var Lock: TThreadlock;
  ProcessShared: Integer
): Integer;
```

### 描述

`pthread_spin_init` 函数设置 `TThreadlock` 变量用于多线程应用程序。该函数将清除自旋锁使其处于未锁定状态。

### 参数

- **Lock**: 要初始化的自旋锁。

- **ProcessShared**: 自旋锁是否可以在进程间共享。在 Linux 上，此参数被忽略，因为自旋锁仅在进程间共享。

### 返回值

此函数始终返回 0。

### 另请参阅

`pthread_spin_destroy`, `pthread_spin_lock`, `pthread_spin_unlock`

## pthread_spin_lock LibC.pas

### 语法

```pascal
function pthread_spin_lock(
  var Lock: TThreadlock;
): Integer;
```

![pthread_spin_lock](img/890ec6003.png)

### 描述

`pthread_spin_lock` 函数将锁定自旋锁，以类似于 mutex 保护代码段的方式。自旋锁与互斥锁不同，它的实现旨在保护资源的最快方法。

### 参数

- **Lock**: 将被锁定的自旋锁。

### 返回值

此函数始终返回 0。

## pthread_spin_trylock LibC.pas

### 语法

```pascal
function pthread_spin_trylock(
  var Lock: TThreadlock;
): Integer;
```

### 描述

`pthread_spin_trylock` 函数尝试以与 `pthread_spin_lock` 函数相同的方式锁定自旋锁，但该函数不会阻塞直到获取自旋锁，而是将返回一个错误代码表示无法立即获取锁。

### 参数

- **Lock**: 将被锁定的自旋锁。

### 返回值

如果可以立即获取自旋锁，函数将返回 0。如果无法立即获取锁，函数将返回 `EBUSY` 错误代码。

## pthread_spin_unlock LibC.pas

### 语法

```pascal
function pthread_spin_unlock(
  var Lock: TThreadlock;
): Integer;
```

### 描述

`pthread_spin_unlock` 函数释放之前通过调用 `pthread_spin_lock` 或 `pthread_spin_trylock` 获取的自旋锁（spin lock）。在自旋锁被解锁后，其他线程将获得获取该自旋锁的机会。

### 参数

- **Lock**: 这是将要解锁的自旋锁变量。

### 返回值

此函数始终返回 0。

### 另请参阅

`pthread_spin_init`, `pthread_spin_destroy`, `pthread_spin_lock`, `pthread_spin_trylock`

## pthread_testcancel LibC.pas

### 语法

```pascal
procedure pthread_testcancel;
```

### 描述

`pthread_testcancel` 函数用于检查是否已通过 `pthread_cancel` 函数或其他机制请求了终止线程的终止。如果该线程已被取消，此函数将终止该线程。如果另一个线程正在使用 `pthread_join` 函数等待此函数，则返回的数据将如同调用了 `pthread_exit(PTHREAD_CANCELED)` 一样。

```go
const
  PTHREAD_CANCELED = Pointer(-1);
```

### 另请参阅

`pthread_cancel`, `pthread_setcancelstate`, `pthread_setcanceltype`

### 示例

参见列表 6.10 - 使用线程池的网络服务器。

## pthread_yield LibC.pas

### 语法

```pascal
function pthread_yield: Integer;
```

### 描述

`pthread_yield` 函数允许其他线程处理，而不会导致当前线程阻塞。由于 POSIX 线程在 Linux 上是通过进程实现的，该函数内部调用了 `sched_yield` 以允许其他进程运行的能力。

### 返回值

如果函数执行成功，将返回 0。如果执行失败，它将返回一个有效的错误代码。

## sem_close LibC.pas

### 语法

```pascal
function sem_close(
  var __sem: TSemaphore
): Integer;
```

### 描述

理论上，`sem_close` 函数会在具名信号量（named semaphore）不再需要时，对其执行任何清理操作。由于 Linux 的 POSIX 线程实现不支持信号量，调用此函数将始终导致返回 `ENOSYS` 错误。

### 返回值

由于此函数未实现，该函数将始终返回 -1，且调用 `errno` 函数将返回 `ENOSYS` 错误代码。

### 另请参阅

`sem_init`, `sem_destroy`, `sem_open`

## sem_destroy LibC.pas

### 语法

```pascal
function sem_destroy(
  var __sem: TSemaphore
): Integer;
```

### 描述

`sem_destroy` 函数会在无名信号量（unnamed semaphore）不再需要时，对其执行任何清理操作。传递给函数的应该是通过调用 `sem_init` 函数的无名信号量。通过 `sem_open` 函数创建的具名信号量应该使用 `sem_close` 函数来管理信号量的清理过程。

### 参数

- **__sem**: 此参数是使用 `sem_init` 函数初始无名信号量。

### 返回值
