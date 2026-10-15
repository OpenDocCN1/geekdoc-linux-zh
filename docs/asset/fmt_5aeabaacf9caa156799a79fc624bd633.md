
```
8     lock.l_whence = whence; /* SEEK_SET, SEEK_CUR, SEEK_END */

9     lock.l_len = len;      /* 字节（0 表示 EOF） */

10    if (fcntl(fd, F_GETLC, &lock) == -1)

11        return (-1); /* 意外错误 */

12    if (lock.l_type == F_UNLCK)

13        return (0); /*假，未被另一个进程锁定 */

14    return true; /* 真，返回所有者的正 PID */
}
```

Posix 记录锁是建议性锁（advisory locking）。这意味着内核维护了每个进程锁定的所有文件的正确信息，但它并不会阻止进程向一个被另一个进程读锁的文件写入。同样，内核也不会阻止进程从一个被另一个进程写锁的文件中读取。假设该进程具有读写该文件的足够权限，进程可以忽略建议性锁并向被读锁的文件写入，或从被写锁的文件中读取。

建议性锁对于协作进程来说是足够的。通过网络编程编写守护进程是协作进程的一个例子——这些访问共享资源（如序列号文件）的程序都受系统管理员控制。只要包含序列号的实际文件对任何进程不可写，某些随机进程在文件被锁定时无法写入该文件。

## 示例：非协作进程

我们可以通过运行两个序列号程序的实例来证明 Posix 记录锁是建议性的：一个 `lockfent.1` 使用图 9.3 所示的函数`lockfent.2` 在增加序列号之前使用图 9.1 所示的函数，而另一个（`locknone`）则不执行任何锁定。

```
solaris % lockfent & locknone &
```

```
lockfent1: pid = 18816, seq# = 1
lockfent1: pid = 18816, seq# = 2
lockfent1: pid = 18816, seq# = 3
```

```
lockcntl: pid = 18816, Seq# = 4
lockcntl: pid = 18816, Seq# = 3
lockcntl: pid = 18816, Seq# = 6
lockcntl: pid = 18816, Seq# = 7
lockcntl: pid = 18816, Seq# = 8
lockcntl: pid = 18816, Seq# = 9
lockone: pid = 18816, Seq# = 10
lockone: pid = 18816, Seq# = 11
lockone: pid = 18817, Seq# = 12 switch processes: error
lockone: pid = 18817, Seq# = 13
lockone: pid = 18817, Seq# = 14
lockone: pid = 18817, Seq# = 15
lockone: pid = 18817, Seq# = 16
lockone: pid = 18817, Seq# = 17
lockcntl: pid = 18816, Seq# = 12 switch processes: error
lockcntl: pid = 18816, Seq# = 13
lockcntl: pid = 18816, Seq# = 14
lockcntl: pid = 18816, Seq# = 15
lockcntl: pid = 18816, Seq# = 16
lockcntl: pid = 18816, Seq# = 17
lockcntl: pid = 18816, Seq# = 18
lockcntl: pid = 18816, Seq# = 19
lockcntl: pid = 18816, Seq# = 20
lockone: pid = 18817, Seq# = 19 switch processes: error
lockone: pid = 18817, Seq# = 20
lockone: pid = 18817, Seq# = 21
lockone: pid = 18817, Seq# = 22
lockone: pid = 18817, Seq# = 23
lockone: pid = 18817, Seq# = 24
lockone: pid = 18817, Seq# = 25
lockone: pid = 18817, Seq# = 26
lockone: pid = 18817, Seq# = 27
lockone: pid = 18817, Seq# = 28
lockone: pid = 18817, Seq# = 29
lockone: pid = 18817, Seq# = 30
```

`lockcntl` 程序首先运行，但在它执行将序列号从 1 增加到 2 的步骤（此时它持有整个文件的锁）时，内核切换进程运行 `lockone` 程序。这个新程序在 `lockcntl` 程序写回文件之前读取了序列号 2。`lockcntl` 持有的建议性锁对 `lockone` 程序没有影响。

## 9.5 强制锁

某些系统提供了另一种记录锁称为强制锁（mandatory locking）。在强制锁下，内核会检查每次读和写请求，以确保操作不会与进程持有的锁冲突。对于阻塞描述符，与强制锁冲突的读写会导致进程睡眠直到锁释放。对于非阻塞描述符，与强制锁冲突的读写会返回 `EAGAIN` 错误。Posix 和 Unix 只定义了建议性锁。然而，许多源自 System V 的实现提供了建议性和强制锁。强制锁随 System V 引入。要对特定文件启用强制锁：

- 用户执行位（user-execute-bit）必须关闭
- 在没有用户位的情况下，组 ID 位（set-group-ID bit）必须开启

注意，在没有用户位的情况下开启组 ID 位是没有意义的，组 ID 位和组执行位也是如此。因此，强制锁是以这种方式添加的而不影响现有软件。在支持强制锁的系统中，`ls` 命令查找这种特殊的位组合并打印强制锁已启用。同样，`chmod` 命令接受指定来启用强制锁。

## 示例

乍看，使用强制锁应该解决非协作进程的问题，因为协作进程对锁定文件的任何读或写将被阻塞直到锁释放。遗憾的是，时序问题更为复杂，我们可以通过将 `seqno` 示例改为强制锁来轻松演示：

```
solaris cat > seqno
solaris ls -l seqno
-rw----- 
solaris chmod +1 seqno
solaris ls -l seqno
-rw-rwx-
```

现在我们在后台启动两个不锁定的程序：`lockcnt1` 和 `lockone`。我们使用命令行参数 `10000` 作为每个程序读取、增加并写入序列号的次数。

```
solaris lockcnt1 10000 & lockone 10000 &
solaris wait
solaris cat seqno
```
