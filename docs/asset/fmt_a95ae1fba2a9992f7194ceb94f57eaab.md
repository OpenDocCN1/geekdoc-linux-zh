
```c
#include "unipc.h"

int main(int argc, char **argv) {
    int fd1, fd2;
    struct shm *ptr1, *ptr2;
    pid_t childpid;
    struct stat stat;

    if (argc != 2) {
        err_exit("usage: <name>\n", argv[0]);
    }
    shm_unlink(ipc_name(argv[1]));
    fd1 = shm_open(ipc_name(argv[1]), O_RDWR|O_CREAT|O_EXCL, FILE_MODE);
    ftruncate(fd1, sizeof(struct shm));
    fd2 = shm_open("/etc/shm", O_RDONLY);
    stat(fd2, &stat);

    if ((childpid = fork()) == 0) {
        ptr2 = mmap(NULL, stat.st_size, PROT_READ, MAP_SHARED, fd2, 0);
        ptr1 = mmap(NULL, stat.st_size, PROT_READ|PROT_WRITE, MAP_SHARED, fd1, 0);
        printf("child: shm ptr = %p, mptr ptr = %p\n", ptr1, ptr2);
        sleep(5);
        printf("parent: shared memory integer = %d\n", *ptr1);
        exit(0);
    }
    /* parent: 与 child 反向 mmap */
    ptr1 = mmap(NULL, stat.st_size, PROT_READ|PROT_WRITE, MAP_SHARED, fd1, 0);
    ptr2 = mmap(NULL, stat.st_size, PROT_READ, MAP_SHARED, fd2, 0);
    printf("parent: shm ptr = %p, mptr ptr = %p\n", ptr1, ptr2);
    waitpid(childpid, NULL, 0);
    exit(0);
}
```

### 图 13.6 共享内存段可以出现在进程中不同的地址

我们创建一个名为命令行参数的共享内存段，将其大小设置为一个整数的大小，然后打开 `/etc/shm` 文件。父进程和子进程均两次 `mmap`，顺序不同。每个打印内存区域的起始地址。子进程睡眠 5 秒，父进程在共享内存区域存储 777，然后子进程打印此值。

当我们运行这个程序时，我们看到共享内存对象在父进程和子进程中映射到了不同的地址。

```
solaris % test3.data
parent: shm_ptr = eee000, mptr_ptr = eee000
child: shm_ptr = eee000, mptr_ptr = eee300
shared memory integer = 777
```

尽管如此，父进程将 777 存储到 `0xeee`，子进程从中读取该值。父进程和子进程中的指针 `ptr1` 都指向同一个内存段，尽管每个指针在每个进程中是不同的。

## 共享计数器

我们开发了一个类似于 2.3 所示的示例，多个进程增加存储在共享内存中的计数器。我们将计数器存储在共享内存并在并名称进行同步，不再需要父子关系。由于 Posix 共享内存对象和 Posix 信号量通过名称引用，只要每个增加计数器的进程对 IPC 对象（共享内存和信号量）具有足够的权限。

图 13.7 显示了创建共享内存对象、创建并初始化信号量以及终止它们的服务器。

### 创建共享内存对象

13-19 如果共享内存对象已存在，我们调用 `shm_unlink`，然后调用 `shm_open` 创建对象。对象的大小通过 `ftruncate` 设置为 `shm_struct` 的大小，`mmap` 将对象映射到我们的地址空间。关闭描述符。

### 创建并初始化信号量

20-22 如果信号量已存在，我们调用 `sem_unlink`，然后调用 `sem_open` 创建名称并初始化为 1。它将被任何增加共享内存对象中计数器的进程用互斥锁。然后关闭信号量。

### 终止

23 进程终止。由于 Posix 共享内存具有内核持久性，对象将一直直到所有进程关闭（进程终止时没有打开引用）并显式 `unlink`。

我们的程序必须为共享内存对象和信号量使用不同的名称。无法保证实现会在 Posix IPC 名称（消息队列、信号量和共享内存）中添加任何内容。我们看到 Solaris 为这三类名称加上 `.MQ`、`.SEM` 和 `.SHM` 前缀，但 Digital Unix 没有。

## Posix 共享内存

```c
#include <unipc.h>
struct shm {
    /* 存储在共享内存中的结构体 */
    int count;
};
sem_t *mutex;    /* 指向命名信号量 */
int main(int argc, char **argv) {
    int fd;
    struct shm *ptr;
    if (argc != 3) shunlink(argv[1]); /* 如果失败则忽略 */
    err_quit("usage: <shname> <semname>", 1); /* 创建 shm, 设置其大小, 映射, 关闭描述符 */
    fd = shm_open(ipc_name(argv[1]), O_RDWR|O_CREAT|O_EXCL, FILE_MODE);
    ftruncate(fd, sizeof(struct shm));
    ptr = mmap(NULL, sizeof(struct shm), PROT_READ|PROT_WRITE, O_SHARED, fd, 0);
    close(fd);
    sem_unlink(ipc_name(argv[2])); /* 如果失败则忽略 */
    mutex = sem_open(ipc_name(argv[2]), O_CREAT|O_EXCL, FILE_MODE, 1);
    sem_close(mutex);
    exit(0);
}
```

图 13.7 创建并初始化共享内存和信号量的程序。

图 13.8 显示了我们的客户端程序，它多次增加共享内存中的计数器，并在每次增加计数器时获取信号量。

### 打开共享内存

`shm_open` 打开共享内存对象，该对象必须存在（因为没有指定 `O_CREATE`）。`mmap` 将内存映射到进程的地址空间，然后关闭描述符。

### 打开信号量

打开命名信号量。

### 获取信号量并增加计数器

按照命令行指定的次数增加计数器。我们每次都打印计数器的旧值，以及进程 ID，因为我们在同一时间运行了多个该程序的副本。

## 13.5 递增共享计数器 335

```c
#include "unipc.h"

struct shmstruct {    /* 存储在共享内存中的结构体 */
    int      count;
};
sem_t   *mutex;    /* 命名信号量的指针 */

int
main(int argc, char **argv) {
    int      fd, i, nloop;
    pid_t   pid;
    struct shmstruct *ptr;

    if (argc != 4)
        fprintf(stderr, "usage: %s <shname> <semname> <loops\n", argv[0]);
    nloop = atoi(argv[1]);
    fd = Shm_open(Px_ipc_name(argv[2]), O_RDWR, FILE_MODE);
    ptr = (struct shmstruct *)mmap(NULL, sizeof(struct shmstruct), PROT_READ|PROT_WRITE, MAP_SHARED, fd, 0);

    close(fd);

    mutex = Sem_open(Px_ipc_name(argv[3]), 0);

    pid = getpid();
    for (i = 0; i < nloop; i++) {
        Sem_wait(mutex);
        printf("pid %ld: %d\n", (long)pid, ptr->count++);
    }

    exit(0);
}
```

> 图 13.5 递增共享内存中计数器的程序。

我们首先启动服务器，然后在后台运行三个客户端的副本。

`solaris & shm1` 创建并初始化共享内存和信号量
