
### 创建 TCP 套接字，建立连接

68–71 通过我们的 `tcp-connect` 函数创建 TCP 套接字并建立连接。套接字是普通的阻塞套接字，因此线程会在 `connect` 调用中阻塞直到连接建立。

### 向服务器写入请求

72 `write_get_cmd` 构建 HTTP GET 命令并发送到服务器。我们没有显示此函数，因为它与图 16.18 的区别在于线程版本没有调用 `FD_SET` 也没有使用 `maxfd`。

## 26.7 互斥锁 (Mutex)

注意图 26.14，当线程终止时，主循环会递减 `nconn` 和 `nleft`。我们本可以将这两个递减操作放在 `do_get_read` 函数中，让每个线程在线程终止前立即递减这两个计数器。但这将是一个微妙但重大的并发编程错误。

将代码放在每个线程执行的函数中存在的问题在于，这些变量是全局的，而不是线程特有的。如果一个线程在递减变量的过程中被挂起，另一个线程执行并递减了同一个变量，就会导致错误。例如，假设编译器将运算符转换为：从内存加载到寄存器、递减寄存器、以及从寄存器存储到内存。考虑以下可能发生的场景：

- 1. 线程 A 正在运行，它将 `nconn` 的值加载到 (3) 寄存器中。
- 2. 系统将线程从 A 切换到 B。保存 A 的寄存器，并恢复 B 的寄存器。
- 3. 线程 B 执行与 C 语言表达式 `nconn--` 对应的三条指令，存储了新值 2。
- 4. 稍后，系统将线程从 B 切换到 A。恢复 A 的寄存器，A 从它离开的地方继续执行，即三条指令序列中的第二条。寄存器的值从 3 递减为 2，并将值 2 存储在 `nconn` 中。

最终结果是当 `nconn` 应该为 1 时却为 2。这是错误的。

这类编程错误由于许多原因而很难发现。首先，错误及其发生的概率极低。尽管如此，它仍然是一个错误，并且会失败（墨菲定律）。由于它取决于许多事件的非确定性本质，因此很难复现。最后，在某些系统上，内存中的硬件指令不是原子的；因此，可能存在一条硬件指令来增加内存中的整数（而不是三条指令序列），且硬件在执行该指令期间无法被中断。但并非所有系统都能保证这一点，因此代码在某个系统上可以工作，在另一个系统上却不行。

我们将线程访问相同变量的行为称为并发编程或并行编程。虽然所讨论的错误场景假设的是单 CPU 系统，但如果线程 A 和 B 同时在多处理器系统的不同 CPU 上运行，产生错误的可能性仍然存在。在普通的 Unix 编程中，我们不会遇到这些并发编程问题，因为使用 `fork` 时，父子进程之间除了描述符外没有任何共享。然而，当我们讨论进程间的共享内存时，将会遇到这类问题。

我们可以很容易用线程来演示这个问题。图 26.17 是一个简单的程序，它创建了两个线程，然后每个线程将一个全局变量加 5,000 次。

通过获取计数器的当前值、打印新值然后存储新值，我们加剧了问题的可能性。如果我们运行这个程序，将得到如图 26.16 所示的输出。

#### 图 26.16. 程序图 26.17 的输出。

```
4: 1

4: 2

4: 3

4: 4

4: 517

4: 518

5: 518

5: 519

5: 520

5: 926

5: 927

4: 519

4: 520
```
随着线程 4 执行继续

线程 5 现在执行

随着线程 5 执行继续

线程 4 现在执行；存储的值是错误的

#### 图 26.17 两个错误增加全局变量的线程。

```c
threads/example01.c

#include "unthread.h"

#define NLOOP 5000

int counter;                /* 被线程递增 */

void *doit(void *);

int main(int argc, char **argv)

{

    pthread_t tidA, tidB;

    pthread_create(&tidA, NULL, &doit, NULL);

    pthread_create(&tidB, NULL, &doit, NULL);

    /* 等待两个线程终止 */

    pthread_join(tidA, NULL);

    pthread_join(tidB, NULL);

    exit(0);

}

void *doit(void *vptr)

{

    int i, val;

    /*

     * 每个线程执行 NLOOP 次获取、打印并增加计数器。

     * 计数器的值应该单调递增。

     */

    for (i = 0; i < NLOOP; i++) {

        val = counter;

        printf("%d: %d\n", pthread_self(), val + 1);

        counter = val + 1;

    }

    return NULL;

}
```

注意系统第一次从线程 4 切换到线程 5 时的错误：值 518 被每个线程存储了。这在 10,000 行输出中发生了多次。

这种问题的非确定性在我们在我们运行几次程序时也显而易见：每次运行的最终结果都与上一次运行不同。如果我们将输出重定向到磁盘文件，有时错误不会发生，因为程序运行得更快，提供了更多线程间切换的机会。当我们交互式运行程序并将输出写入到终端时，错误发生的次数最多。

我们刚刚讨论的“多个线程更新共享变量”的问题是最简单的。解决方案是使用互斥锁（mutex）来保护共享变量。在 pthreads 术语中，mutex 代表“互斥（mutual exclusion）”。我们使用以下函数：

```c
#include <pthread.h>

int pthread_mutex_lock(pthread_mutex_t *mptr);

int pthread_mutex_unlock(pthread_mutex_t *mptr);

int pthread_mutex_init(pthread_mutex_t *mptr, int attr);

int pthread_mutex_destroy(pthread_mutex_t *mptr);
```

我们定义了一个名为 `counter_mutex` 的互斥锁。当我们运行这个程序时，输出总是正确的：计数器单调递增，最终打印的值为10,000。

互斥锁涉及多少开销？我们将图 26.17 和 26.18 中的程序更改为循环 50,000 次，并在输出定向 `/dev/null` 时进行计时。无互斥锁错误版本与使用互斥锁正确版本的 CPU 时间差异为 10%。这告诉我们互斥锁的开销。

## 26.8 条件变量

互斥锁是为了防止同时访问共享变量，但我们需要其他机制让我们在等待条件发生时进入睡眠。让我们用一个例子来演示。回到 26.6 中的 Web 客户端，将 Solaris 的 `thr_join` 替换为 `pthread_join`。但在确定线程已终止之前，我们不能调用该 pthread 函数。我们首先声明一个计算终止线程数的全局变量，并用互斥锁保护它。

```c
int ndone;               /* 终止线程数 */
pthread_mutex_t ndone_mutex = PTHREAD_MUTEX_INITIALIZER;
```

我们要求每个线程在终止时增加此计数器，并注意使用关联互斥锁。

```c
void *read *vptr
do_get_read (void *vptr)
{
    pthread_mutex_lock(&ndone_mutex);
    ndone++;
    pthread_mutex_unlock(&ndone_mutex);
    return (fptr);       /* 终止线程 */
}
```

这样做很好，但主循环如何编写呢？它需要不断加锁并检查是否有线程已终止。

```c
while (nleftottore > 0) {
    while (nconn < maxconn && nlefttocann > 0) {
        /* 寻找要读取的文件 */
        ...
    }
    /* 查看是否有线程已完成 */
    pthread_mutex_lock(&ndone_mutex);
    if (ndone > 0) {
```

```c
for (i = 0; i < nfiles; i++) {
  if (file[i].f_flags & F_DONE) {
    pthread_join(file[i].f_tid, (void **)&fptr);
  }
  /* update file[i] for terminated thread */
  ...
  }
  pthread_mutex_unlock(&ndone_mutex);
}
```
