
```c
int pthread_join(pthread_t tid, void **status);
pthread_t self(void);
int pthread_cond_destroy(pthread_cond_t *cond);
pthread_cond_getattr(const pthread_cond_t *cond);
int pthread_cond_init(pthread_cond_t *cond);
int pthread_cond_signal(pthread_cond_t cond);
int pthread_cond_broadcast(pthread_cond_t cond);
int pthread_cond_wait(pthread_cond_t cond, pthread_mutex_t *mutex);
int pthread_cond_timedwait(pthread_cond_t cond, pthread_mutex_t *mutex, const timespec *abtime);
int pthread_mutex_destroy(pthread_mutex_t *mutex);
int pthread_mutex_init(pthread_mutex_t *mutex);
int pthread_mutex(pthread_mutex_t *mutex);
int pthread_mutex_lock(pthread_mutex_t *mutex);
int pthread_mutex_timedlock(pthread_mutex_t *mutex, const timespec *abtime);
int pthread_mutex_unlock(pthread_mutex_t *mutex);
pthread_mutex_getattr(const pthread_mutex_t *mutex);
int pthread_mutex_setattr(pthread_mutex_t *mutex, const pthread_mutexattr_t *attr);
int pthread_rwlock_destroy(pthread_rwlock_t *rwlock);
int pthread_rwlock_init(pthread_rwlock_t *rwlock);
int pthread_rwlock_rdlock(pthread_rwlock_t *rwlock);
int pthread_rwlock_rdunlock(pthread_rwlock_t *rwlock);
int pthread_rwlock_wrlock(pthread_rwlock_t *rwlock);
int pthread_rwlock__unlock(pthread_rwlock_t *rwlock);
pthread_rwlock_getattr(const pthread_rwlock_t *rwlock);
int pthread_rwlock_setattr(pthread_rwlock_t *rwlock, const pthread_rwlockattr_t *attr);
```

致 Usenet 社区；
感谢回答了许多问题，
以及提供的许多常见问题解答。

序言 xiii

# 第 1 部分 引言 1

## 第 1 章 引言 3
- 1.1 进程、线程与信息共享 5
- 1.2 IPC 对象的持久性 6
- 1.3 命名空间 7
- 1.4 fork, exec 和 exit 对 IPC 对象的影响 9
- 1.5 错误处理：封装函数 11
- 1.6 Unix 标准 13
- 1.7 文中 IPC 示例路线图 15
- 1.8 总结 16

## 第 2 章 Posix IPC 19
- 2.1 引言 19
- 2.2 IPC 名称 19
- 2.3 创建和打开 IPC 通道 22
- 2.4 IPC 权限 25
- 2.5 总结 26

vii

# System V IPC

## 第 3 章 System V IPC 27
- 3.1 引言 27
- 3.2 Keys 和 flock 函数 28
- 3.3 ipcrm 结构 30
- 3.4 创建和打开 IPC 通道 30
- 3.5 IPC 权限 32
- 3.6 标识符重用 34
- 3.7 pipes 和 ipcrm 程序 36
- 3.8 内核限制 56
- 3.9 总结 38

- 4.1 引言 43
- 4.2 简单的客户端-服务器示例 43
- 4.3 管道 44
- 4.4 全双工 50
- 4.5 popen 和 pclose 函数 52
- 4.6 FIFO 54
- 4.7 管道与 FIFO 的附加属性 58
- 4.8 一个服务器，多个客户端 60
- 4.9 迭代并发服务器 66
- 4.10 流与消息 67
- 4.11 管道与 FIFO 限制 72
- 4.12 总结 75

- 5.1 引言 75
- 5.2 mq_open, mq_close 和 mq_unlink 函数 76
- 5.3 mq_getattr 和 mq_setattr 函数 79
- 5.4 mq_send 和 mq_receive 函数 82
- 5.5 消息队列限制 86
- 5.6 mq_notify 函数 87
- 5.7 Posix 实时信号 98
- 5.8 使用内存映射 I/O 的实现 106
- 5.9 总结 126

- 6.1 引言 129
- 6.2 msgget 函数 130
- 6.3 msgrnd 函数 131
- 6.4 msgrcv 函数 132
- 6.5 msgsctl 函数 134
- 6.6 简单程序 135
- 6.7 客户端-服务器示例 140
- 6.8 消息复用 142
- 6.9 使用 select 和 poll 的消息队列 151
- 6.10 消息队列限制 152
- 6.11 总结 155

# 第 3 部分 同步 157

## 第 7 章 互斥与与条件 159
- 7.1 引言 159
- 7.2 互斥锁：锁定与解锁 159
- 7.3 生产者-消费者问题 161
- 7.4 锁定与等待 165
- 7.5 条件变量：等待与信号 167
- 7.6 条件变量：定时等待与广播 171
- 7.7 互斥锁与条件变量属性 172
- 7.8 总结 174

- 8.1 引言 177
- 8.2 获取和释放读写锁 178
- 8.3 读写锁属性 179
- 8.4 使用互斥锁与条件变量的实现 179
- 8.5 线程取消 187
- 8.6 总结 192

## 第 9 章 记录锁 193
- 9.1 引言 193
- 9.2 记录锁与文件锁 197
- 9.3 fcnt 记录锁 199
- 9.4 建议性锁 203
- 9.5 强制锁 204
- 9.6 读者与写者的优先级 207
- 9.7 守护进程启动 213
- 9.8 锁文件 214
- 9.10 总结 216

- 10.1 引言 219
- 10.2 sem_open, sem_close 和 sem_unlock 225
- 10.3 sem_wait 和 sem_trywait 226
- 10.4 sem_post 和 sem_getvalue 227
- 10.5 简单程序 228
- 10.6 生产者-消费者问题 233
- 10.7 文件锁 238
- 10.8 sem_init 和 sem_destroy 238
- 10.9 多个生产者，一个消费者 242
- 10.10 多个生产者，多个消费者 245
- 10.11 多个缓冲区 249
- 10.12 进程间的信号量 256
- 10.13 信号量限制 257
- 10.14 使用 FIFO 的实现 257
- 10.15 使用内存映射 I/O 的实现 262
- 10.16 使用系统信号量的实现 271
- 10.17 总结 278

- 11.1 引言 281
- 11.2 semget 函数 282
- 11.3 semop 函数 285
- 11.4 shmctl 函数 287
- 11.5 简单程序 289
- 11.6 文件锁 294
- 11.7 信号量限制 296
- 11.8 总结 300

- 12.1 引言 303
- 12.2 mmap, munmap 和 sync 函数 307
- 12.3 内存映射文件中的计数器 311
- 12.4 BBSD 匿名内存映射 315
- 12.5 SV4/dev/zero 内存映射 316
- 12.6 引用内存映射对象 317
- 12.7 总结 322

- 13.1 引言 325
- 13.2 shm_open 和 shm_unlink 函数 326
- 13.3 ftruncate 和 fstat 函数 327
- 13.4 简单程序 328
- 13.5 增加共享计数器 333
