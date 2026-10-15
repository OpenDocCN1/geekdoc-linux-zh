
- `EINVAL` - `attr` 不是线程属性或 `sched_p` 无效（仅设置）

`int pthread_attr_getschedpolicy(const pthread_attr_t *attr, int *policy);`

`int pthread_attr_setschedpolicy(pthread_attr_t *attr, int *policy);`

获取或设置使用 `attr` 的线程所使用的调度策略。

```
Policy = SCHED_FIFO
SCHED_RR
SCHED_OTHER
```

# Posix 线程 (Pthreads) 应用程序接口

默认值取决于实现。

## 错误 (Errors)

- `ENOSYS` – 不支持优先级调度
- `EINVAL` – `attr` 不是线程属性或 `policy` 无效（仅设置）

`int pthread_attr_getscope(const pthread_attr_t *attr, int *scope);`

`int pthread_attr_setscope(pthread_attr_t *attr, int scope);`

获取或设置用 `attr` 创建的线程的“竞争范围（contention scope）”。

```
scope = PTHREAD_SCOPE_PROCESS
PTHREAD_SCOPE_SYSTEM
```

默认值取决于实现。

## 错误 (Errors)

- `ENOSYS` – 不支持优先级调度
- `EINVAL` - `attr` 不是线程属性或 `scope` 无效（仅设置）

# 互斥锁 (Mutexes)

`int pthread_mutex_init(pthread_mutex_t *mutex, const pthread_attr_t *mutex_attr);`

创建一个互斥锁对象。如果非空，`*mutex_attr` 提供可选属性。

## 错误 (Errors)

- `EAGAIN` – 资源不足
- `ENOMEM` – 互斥锁对象内存不足
- `EPERM` – 无权限执行此操作
- `EBUSY` – `*mutex` 已经初始化
- `EINVAL` – `*mutex_attr` 不是互斥锁属性

# 用于嵌入式和实时应用的 Linux (Linux for Embedded and Real-time Applications)

`int pthread_mutex_destroy(pthread_mutex_t *mutex);`

销毁不再需要的现有互斥锁。

## 错误 (Errors)

- `EBUSY` - `mutex` 正在使用
- `EINVAL` - `mutex` 不是互斥锁

`int pthread_mutex_lock(pthread_mutex_t *mutex);`

锁定互斥锁。如果互斥锁已锁定，调用线程将被阻塞，直到互斥锁随后被解锁。返回后，调用线程“拥有”互斥锁，直到它调用 `pthread_mutex_unlock()`。

## 错误 (Errors)

- `EINVAL` - 线程优先级超过互斥锁的优先级上限。
- `EINVAL` - `mutex` 不是互斥锁

`int pthread_mutex_trylock(pthread_mutex_t *mutex);`

如果互斥锁处于解锁状态则锁定它。如果已锁定则立即返回错误代码。这是一种非阻塞锁定方法。

## 错误 (Errors)

- `EINVAL` - 线程优先级超过互斥锁上限。
- `EBUSY` - 互斥锁已锁定
- `EINVAL` - `mutex` 不是互斥锁对象
- `EDEADLK` - 调用线程已拥有互斥锁

`int pthread_mutex_unlock(pthread_mutex_t *mutex);`

解锁互斥锁。如果有线程等待该互斥锁，其中一个将被唤醒并成为新的所有者。唤醒顺序取决于调度策略。

# Posix 线程 (Pthreads) 应用程序接口

## 错误 (Errors)

- `EINVAL` – `mutex` 不是互斥锁
- `EPERM` – 调用线程未拥有互斥锁

# 互斥锁属性 (Mutex Attributes)

`int pthread_mutexattr_init(pthread_mutexattr_t *mutex_attr);`

用默认值初始化互斥锁属性。

## 错误 (Errors)

- `ENOMEM` – 属性对象内存不足

`int pthread_mutexattr_destroy(pthread_mutexattr_t *mutex_attr);`

销毁互斥锁属性。

## 错误 (Errors)

- `EINVAL` – `mutex_attr` 不是互斥锁属性

`int pthread_mutexattr_getkind_np(const pthread_mutexattr_t *mutex_attr, int *kind);`

`int pthread_mutexattr_setkind_np(pthread_mutexattr_t *mutex_attr, int kind);`

获取或设置互斥锁的“类型（kind）”。这是一个非移植的 Linux 扩展。详情详见第 11 章。

```
kind =
PTHREAD_MUTEX_FAST_NP
PTHREAD_MUTEX_RECURSIVE_NP
PTHREAD_MUTEX_ERRORCHECK_NP
```

## 错误 (Errors)

- `EINVAL` – `mutex_attr` 不是互斥锁属性
- `EINVAL` – `kind` 无效（仅设置）

# 用于嵌入式和实时应用的 Linux (Linux for Embedded and Real-time Applications)

`int pthread_mutexattr_getpriorityceiling(const pthread_mutexattr_t *mutex_attr, int *prioceiling);`

`int pthread_mutexattr_setpriorityceiling(pthread_mutexattr_t *mutex_attr, int nprioceiling);`

获取或设置线程在拥有用 `attr` 创建的互斥锁时运行的优先级上限。RTAI Pthreads 中未实现。

## 错误 (Errors)

- `ENOSYS` – 不支持优先级调度
- `EINVAL` - `attr` 不是互斥锁属性对象或 `nprioceiling` 无效（仅设置）
- `ENOPERM` – 无权限设置优先级上限

`int pthread_mutexattr_getprotocol(const pthread_mutexattr_t *mutex_attr, int *protocol);`

`int pthread_mutexattr_setprotocol(pthread_mutexattr_t *mutex_attr, int protocol);`

获取或设置处理优先级反转的互斥锁协议。RTAI Pthreads 中未实现。

```
protocol = PTHREAD_PRIO_NONE
PTHREAD_PRIO_INHERIT
PTHREAD_PRIO_PROTECT
```

## 错误 (Errors)

- `ENOSYS` – 不支持优先级调度
- `EINVAL` - `attr` 不是互斥锁属性对象或 `protocol` 无效（仅设置）
- `ENOTSUP` – 协议值不支持

# Posix 线程 (Threads) 应用程序接口

## 条件变量

```
int pthread_cond_init (pthread_cond_t *cond, const pthread_condattr_t
                                     *cond_attr);
```

创建一个条件变量对象 `cond`。如果 `cond_attr` 不为空，则 `cond_attr` 提供可选属性。

### 错误

- `EAGAIN` – 内存以外的资源不足
- `ENOMEM` – 创建条件变量对象内存不足
- `EBUSY` – `cond` 已经初始化
- `EINVAL` – `cond_attr` 不是条件变量属性

```
int pthread_cond_destroy (pthread_cond_t *cond);
```

销毁一个不再需要的现有 `cond`。

### 错误

- `EBUSY` – `cond` 正在使用
- `EINVAL` – `cond` 不是条件变量

```
int pthread_cond_wait (pthread_cond_t *cond, pthread_mutex_t *mutex);
```

在条件变量 `cond` 上等待，直到被信号或广播唤醒。在 `pthread_cond_wait()` 内部，`mutex` 会解锁（等待前）并重新加锁（等待后）。

### 错误

- `EINVAL` – `cond` 或 `mutex` 无效
- `EINVAL` – 并发等待使用了不同的互斥锁
- `EINVAL` – `mutex` 不由调用线程持有
