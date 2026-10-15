
`alpha % semwait /tmp/test1`      therelafter sem-wait returns

`pid 9702` has semaphore, value = 0  type interrupt key to abort program

`alpha % getvalue /tmp/test1`

and value remains 0

value = 0

```
这个示例展示了我们之前提到的两个特性。第一个，信号量的值是内核持久化的。也就是说，当我们在上一个示例中创建信号量时，信号量的值由内核维护，即使在此期间没有没有程序打开该信号量。第二个，当我们终止持有信号量锁的 `semwait` 程序时，信号量的值不会改变。当持有锁的进程在未释放锁的情况下终止时，它不会被解锁。我们现在展示实现如何使用负信号量值来表示等待信号量解锁的进程数。
```

`alpha % getvalue /tmp/test1`      value is still 0 from previous example

value = 0

`alpha % semwait /tmp/test1`      start in the background [1] 9718 it blocks, waiting for semaphore

`alpha % semwait /tmp/test1`      one process waiting for semaphore

value = -1

`alpha % semwait /tmp/test1`      start another in the background [2] 9727 also blocks, waiting for semaphore

`alpha % semwait /tmp/test1`      two processes waiting for semaphore

value = -2

`alpha % sempost /tmp/test1`      now post to semaphore

value = -1                      value after sem-post returns

`pid 9718` has semaphore, value = -1  output from semwait program

`alpha % sempost /tmp/test1`      post again to semaphore

value = 0                       

`pid 9727` has semaphore, value = 0  output from semwait program

```
## Posix 信号量

当值为 -2 且我们执行程序时，值会增加到 -1，一个在 `semwait` 调用中阻塞的进程会返回。我们现在在 Solaris 2.6 下执行相同的示例以查看差异。
```

```
solaris % semcreate /test2

solaris % ls -l /tmp/.test2

-rw-r-- 48 Nov 13 09:11 /tmp/.test2

-rw-r-- 0 Nov 13 09:11 /tmp/.test2

solaris % getvalue /test2
```

与 Posix 消息队列一样，`/tmp` 目录下会创建包含指定名称作为文件名的文件。我们看到第一个文件的权限对应于调用 `sem_open` 时指定的权限，我们猜测第二个文件是用于锁的。我们现在验证当进程在未释放锁的情况下终止时，内核不会自动对信号量进行同步。

```
solaris % semwait /test2

pid 9733 has semaphore, value = 0  type interrupt key
```

`solaris % getvalue /test2`

value = 0

与之前的 Digital Unix 输出相比，一个不同点在于，当信号量被同步时，该实现如何处理等待信号量的值：

```
solaris % getvalue /test2

value = 0

value is still 0 from previous example

solaris % semwait /test2 & [1] 9757 start in the background blocks, waiting for semaphore

solaris % getvalue /test2

value = 0

this implementation does not use negative values start another in the background

solaris % semwait /test2 & [2] 9763 two processes waiting

solaris % getvalue /test2

value = 0

pid 9757 has semaphore, value = 0  now post to semaphore output from semwait program 0

solaris % sempost /test2

pid 9763 has semaphore, value = 0  output from semwait program

value = 0
```
