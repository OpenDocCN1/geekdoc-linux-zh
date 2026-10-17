
`$ libc.so.6`
GNU C 库发布版本 2.3.3，由 Roland McGrath 等编写。
Copyright (C) 2004 Free Software Foundation, Inc.
这是自由软件；请查看源码获取副本。
不提供任何保证；即使对于商业用途或特定用途。

由 GNU CC 版本 3.4.2 20041017 (Red Hat 3.4.2-6.fc3) 编译。
2004-10-27 编译于 Linux 2.4.20 系统。

可用扩展：
- 由 Peter Nother 编写的 GNU libio
由 Michael Glad 等人编写的 crypt 插件版本 2.1
由 Ulrich Drepper 等人编写的 Native POSIX Threads 库
- BIND-8.2.3-T5B
由 Thorsten Kukuk 编写的 NIS(YP)/NIS+ NSS 模块 0.19
由 Simon Josefsson 编写的 GNU Libid
包含线程本地存储支持

有关错误报告说明，请参阅：
<http://www.gnu.org/software/libc/bugs.html>.

如前述输出所示，`libc.so.6` 与 Ulrich Drepper 的原生线程库链接在一起。

## 6.10.1 HP-UX 和 Linux 中的线程支持

HP-UX 宣布正式支持 POSIX 1003.1，并在其 HP-UX 11 版本中停止支持新应用程序使用 DCE 线程。尽管 DCE 线程的支持仍然。将这些应用程序迁移到 Linux 要求它们遵循这些标准新的 POSIX 1003.1 标准。表 6-15 比较了 HP-UX 和 Linux 上的 DCE 线程和 POSIX 线程。

## 6.10 线程

表 6-15
Linux 与 HP-UX 线程实现对比

| HP-UX DCE | HP-UX POSIX | Linux NPTL |
| --- | --- | --- |
| `atfork` | `pthread_atfork` | `pthread_atfork` |
| `hp__pthread_equal` | None | None |
| `pthread_cancel_thread` | `pthread_cancel` | `pthread_cancel` |
| `pthread_attr_create` | `pthread_attr_init` | `pthread_attr_init` |
| `pthread_attr_delete` | `pthread_attr_destroy` | `pthread_attr_destroy` |
| `pthread_attr_getardsize_np` | `pthread_attr_getardsize` | `pthread_attr_getardsize` |
| `pthread_attr_getinherited` | `pthread_attr_getinherited` | `pthread_attr_getinherited` |
| `pthread_attr_getprio` | `pthread_attr_getchedparam` | `pthread_attr_getchedparam` |
| `pthread_attr_getsched` | `pthread_attr_getchedpolicy` | `pthread_attr_getchedpolicy` |
| `pthread_attr_getstacksize` | `pthread_attr_getstacksize` | `pthread_attr_getstacksize` |
| `pthread_attr_setguardsize_np` | `pthread_attr_setguardsize` | `pthread_attr_setguardsize` |
| `pthread_attr_setinherited` | `pthread_attr_setinherited` | `pthread_attr_setinherited` |
| `pthread_attr_setprio` | `pthread_attr_setchedparam` | `pthread_attr_setchedparam` |
| `pthread_attr_setchedched` | `pthread_attr_setchedpolicy` | `pthread_attr_setchedpolicy` |
| `pthread_attr_setstacksize` | `pthread_attr_setstacksize` | `pthread_attr_setstacksize` |
| `pthread_cancel` | `pthread_cancel` | `pthr_cancel` |
| `pthread_cond_broadcast` | `pthread_cond_broadcast` | `pthread_cond_broadcast` |
| `pthread_cond_destroy` | `pthread_cond_destroy` | `pthread_cond_destroy` |
| `pthread_cond_init` | `pthread_cond_init` | `pthread_cond_init` |
| `thread_cond_signal` | `thread_cond_signal` | `thread_cond_signal` |
| `thread_cond_signal_int_np` | None | None |
| `thread_cond_timedwait` | `thread_cond_timedwait` | `thread_cond_timedwait` |
| `thread_cond_wait` | `thread_cond_wait` | `thread_cond_wait` |
| `thread_condattr_create` | `thread_condattr_init` | `thread_condattr_init` |
| `thread_condattr_delete` | `thread_condattr_destroy` | `thread_condattr_destroy` |
| `thread_create` | `thread_create` | `thread_create` |
| `thread_ctxb_hpux` | None | None |
| `thread_delay_np` | `nanosleep` | `nanosleep` |
| `thread_detach` | `thread_detach` | `thread_detach` |
| `thread_equal` | `thread_equal` | `thread_equal` |
| `thread_exit` | `thread_exit` | `thread_exit` |
| `thread_get_expiration_np` | `get_expiration_time` | `get_expiration_time` |
| `thread_getrio` | `thread_getschedparam` | `thread_getschedparam` |
| `thread_scheduler` | `thread_getschedparam` | `thread_getschedparam` |
| `thread_getspecific` | `thread_getspecific` | `thread_getspecific` |
| `thread_is_multithreaded_np` | None | None |
| `thread_join` | `thread_join` | `thread_join` |
| `thread_keycreate` | `thread_key_create` | `thread_key_create` |
| `thread_lock_global_np` | None | None |
| `thread_mutex_destroy` | `thread_mutex_destroy` | `thread_mutex_destroy` |
| `thread_mutex_init` | `thread_mutex_init` | `thread_mutex_init` |
| `thread_mutex_lock` | `thread_mutex_lock` | `thread_mutex_lock` |
| `thread_mutex_trylock` | `thread_mutex_trylock` | `thread_mutex_trylock` |
| `pthread_mutex_unlock` | `thread_unlock` | `thread_unlock` |
| `pthread_mutexattr_create` | `thread_mutexattr_init` | `thread_mutexattr_init` |
| `pthread_mutexattr_delete` | `thread_mutexattr_destroy` | `thread_mutexattr_destroy` |
| `pthread_mutexattr_getkind_np` | None | None |
| `pthread_mutexattr_setkind_np` | None | None |
| `pthread_once` | `thread_once` | `thread_once` |
| `pthread_self` | `thread_self` | `thread_self` |
| `pthread_setasynccancel` | `thread_setcanceltype` | `thread_setcanceltype` |
| `pthread_setcancel` | `thread_setcancelstate` | `thread_setcancelstate` |
| `pthread_setprio` | `thread_setschedparam` | `thread_setschedparam` |
| `pthread_setscheduler` | `thread_setschedparam` | `thread_setschedparam` |
| `pthread_setspecific` | `thread_setspecific` | `thread_setspecific` |
| `pthread_signal_to_cancel_np` | None | None |
| `pthread_testcancel` | `thread_testcancel` | `thread_testcancel` |
| `pthread_yield` | `sched_yield` | `sched_yield` |
| `sigprocmask` | `thread_sigmask` | `thread_sigmask` |
| `sigwait` | `sigwait` | `sigwait` |

尽管 HP-UX 11 和 Linux 都实现了 POSIX 1003.1，但在平台实现上存在细微差异。表 6-16 和表 6-17 显示了这些差异。

### 表 6-16
HP-UX 与 Linux 的 API 差异

| API | 差异 |
| --- | --- |
| `pthread_create` | Linux: 未实现 |
| `pthread_attr_cancel` | Linux: 未实现 |
| `pthread_cond_init` | Linux: 未实现 |
| `pthread_cond_destroy` | Linux: 未实现 |
| `pthread_cond_broadcast` | Linux: 未实现 |
| `pthread_mutex_init` | Linux: 未实现 |
| `pthread_mutex_destroy` | Linux: 未实现 |
| `pthread_mutex_lock` | Linux: 未实现 |
| `pthread_mutex_trylock` | Linux: 未实现 |
| `pthread_mutex_unlock` | Linux: 未实现 |
| `pthread_mutexattr_create` | Linux: 未实现 |
| `pthread_mutexattr_delete` | Linux: 未实现 |
| `pthread_mutexattr_getkind_np` | Linux: 未实现 |
| `pthread_mutexattr_setkind_np` | Linux: 未实现 |
| `pthread_once` | Linux: 未实现 |
| `pthread_self` | Linux: 未实现 |
| `pthread_setasynccancel` | Linux: 未实现 |
| `pthread_setcancel` | Linux: 未实现 |
| `pthread_setprio` | Linux: 未实现 |
| `pthread_setscheduler` | Linux: 未实现 |
| `pthread_setspecific` | Linux: 未实现 |
| `pthread_signal_to_cancel_np` | Linux: 未实现 |
| `pthread_testcancel` | Linux: 未实现 |
| `pthread_yield` | Linux: 未实现 |
| `sigprocmask` | Linux: 未实现 |
| `sigwait` | Linux: 未实现 |
| `pthread_attr_create` | Linux: 未实现 |
| `pthread_attr_delete` | Linux: 未实现 |
| `pthread_attr_getardsize_np` | Linux: 未实现 |
| `pthread_attr_getinherited` | Linux: 未实现 |
| `pthread_attr_getprio` | Linux: 未实现 |
| `pthread_attr_getsched` | Linux: 未实现 |
| `pthread_attr_getstacksize` | Linux: 未实现 |
| `pthread_attr_setguardsize_np` | Linux: 未实现 |
| `pthread_attr_setinherited` | Linux: 未实现 |
| `pthread_attr_setprio` | Linux: 未实现 |
| `pthread_attr_setchedched` | Linux: 未实现 |
| `pthread_attr_setstacksize` | Linux: 未实现 |
| `pthread_cancel_thread` | Linux: 未实现 |
| `hp__pthread_equal` | Linux: 未实现 |
| `thread_delay_np` | Linux: 未实现 |
| `thread_detach` | Linux: 未实现 |
| `thread_equal` | Linux: 未实现 |
| `thread_exit` | Linux: 未实现 |
| `thread_get_expiration_np` | Linux: 未实现 |
| `thread_getrio` | Linux: 未实现 |
| `thread_scheduler` | Linux: 未实现 |
| `thread_getspecific` | Linux: 未实现 |
| `thread_is_multithreaded_np` | Linux: 未实现 |
| `thread_join` | Linux: 未实现 |
| `thread_keycreate` | Linux: 未实现 |
| `thread_lock_global_np` | Linux: 未实现 |
| `thread_mutex_destroy` | Linux: 未实现 |
| `thread_mutex_init` | Linux: 未实现 |
| `thread_mutex_lock` | Linux: 未实现 |
| `thread_mutex_trylock` | Linux: 未实现 |
| `pthread_mutexattr_create` | Linux: 未实现 |
| `pthread_mutexattr_delete` | Linux: 未实现 |
| `pthread_cond_broadcast` | Linux: 未实现 |
| `pthread_cond_destroy` | Linux: 未实现 |
| `pthread_cond_init` | Linux: 未实现 |
| `thread_cond_signal` | Linux: 未实现 |
| `thread_cond_signal_int_np` | Linux: 未实现 |
| `thread_cond_timedwait` | Linux: 未实现 |
| `thread_cond_wait` | Linux: 未实现 |
| `thread_condattr_create` | Linux: 未实现 |
| `thread_condattr_delete` | Linux: 未实现 |
| `thread_create` | Linux: 未实现 |
| `thread_ctxb_hpux` | Linux: 未实现 |

### 表 6-17
HP-UX 与 Linux 线程属性值

| 属性 | HP-UX | Linux |
| --- | --- | --- |
| `contention` | `PTHREAD_SCOPE` | 未实现 |
| `detachstate` | `PTHREAD_JOINABLE` | `PTHREAD_JOINABLE` |
| `inheritsched` | `PTHREAD_INHERIT_SCHED` | `PTHREAD_INHERIT_SCHED` |
| `priority` | `PTHREAD_PRIO_ANY` | 未实现 |
| `policy` | `SCHED_OTHER` | `SCHED_OTHER` |
| `stacksize` | 2MB | 2MB |
| `type` | `PTHREAD_CREATE` | `PTHREAD_CREATE` |
| `guardsize` | 4K | 4K |
| `binding` | `PTHREAD_BIND_SELF` | `PTHREAD_BIND_SELF` |

### 6.10.2 HP-UX 与 Linux 线程差异

尽管 HP-UX 11 和 Linux 都实现了 POSIX 1003.1，但在平台实现上存在细微差异。表 6-16 和 6-17 显示了这些差异。

### 6.10.2.4 互斥锁API差异

创建和销毁互斥锁属性的 DCE 线程 API 在 POSIX.1-1996 中发生了变化。DCE 线程使用 `pthread_mutexattr_create` 和 `pthread_mutexattr_delete`，而 POSIX.1-1996 分别使用 `pthread_mutexattr_init` 和 `pthread_mutexattr_destroy`。

POSIX1003.1c 引入了互斥锁的静态初始化。以下是静态化的示例：

```
