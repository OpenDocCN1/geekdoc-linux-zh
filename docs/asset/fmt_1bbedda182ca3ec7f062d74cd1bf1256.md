
安装 MPI 建议使用分发版（因为由于对其他包的依赖，编译过程极其复杂）。Debian 在 `mpich-package` 中包含了 `Mpich 1.2.7-(itch)` 版本（`mpich` 软件包已过时），还包含了 `mpich-bin`（一个包含对可扩展进程、管理和控制支持的多用途守护进程版本）。`mpich-bin` 实现了 MPI 1.2 标准和 MPI 2 的部分内容（例如，并行输入/输出）。此外，它还包含了另一个名为 LAM 的 MPI 实现（在 `lam*` 包和文档中）。从 MPI 的角度来看，这两种实现是等价，但管理方式不同。关于 MPI 的所有信息（在安装 `mpich*` 包后）可以在 `/usr/share/doc/mpi`（或 `/usr/doc/mpi`）中找到。MPI 需要 `rsh` 在其他机器上执行，这意味着我们必须在 `~/.hosts` 文件中插入用户目录，格式如下：`host username` 允许用户名无需密码进入主机（与 PVM 相同）。请记住，我们必须在所有机器上安装 `rshserver` 包，如果 `/etc/inetd.conf` 中的 `rsh.d` 中有 `tcpd`，我们必须在 `/etc/hosts.allow` 中启用 hosts。此外，我们必须在所有机器上通过 NFS 监控用户目录，并且 `/etc/mpich/machines.LINUX` 文件必须包含组成集群的所有主机名（默认每行一个，如 `localhost`）。此外，用户必须将 Csh 作为默认 shell。

在 Debian 上，我们可以安装 `update-cluster` 包来帮助管理。在 Debian 上安装 Mpich 出于安全考虑使用了 `ssh` 替 `rs=>ssh` 的链接，但区别在于我们使用 `ssh` 认证机制通过相应文件进行无密码连接。否则，对于每个执行的进程，我们都必须在执行前输入密码。为了允许通过 `ssh` 使用密码进行机器连接，我们必须遵循上一节提到的步骤。要检查这一点，我们可以运行 `ssh localhost`，然后我们应该能够无密码登录。请记住，如果我们安装了 Mpich 和 LAM-MPI，`mpirun` 将会被调用为 `mpirun.mpich`，而 `mpirun` 将是 LAM-MPI 的。重要的是，LAM 的 `mpirun` 将使用

`lamboot` 守护进程的设计使得用户可以在没有 root 权限的情况下执行程序（它还允许在虚拟机 VM 中在不调用 MPI 的情况下执行程序）。由于此原因，要执行 `mpirun`，我们将以非 root 身份执行并先执行 `lamboot`。我们使用 `/etc/lam` 中的配置文件进行节点的默认定义（参见 `bhost`）；请参阅文档获取更多信息（`http://www.lam-mpi.org/`）。[Lam]

要编译 MPI 程序，我们使用 `mpicc` 命令（例如 `mpicc -o test.c.`），它接受 `gcc` 的所有选项，尽管建议（通过修改）位于 `/usr/doc/mpich/examples` 文件中的某些 makefiles。也可以使用 `mpireconfig Makefile`，它使用 `Makefile.in` 作为入口来生成 makefile，并且更易修改。之后，我们可以运行：

```
mpirun -np 8 programme
```

或者：

```
mpirun.mpich -np 8 programme
```

其中 `np` 是程序执行运行的处理器或进程数量（在这种情况下为 8）。我们可以输入任何喜欢的数字，因为 Mpich 将尝试在 `/etc/mpich/machines.LINUX` 的所有机器之间平衡分布进程。如果进程多于处理器，Mpich 将使用 GNU/Linux 的交换特性来模拟并行执行。在 Debian 的目录 `/usr/doc/mpich-doc`（指向 `/usr/share/doc/mpich-doc` 的链接）中，我们可以找到所有不同格式的文档（命令、MPI API 等）。

编译 MPI：`mpicc -O -o output output.c`

执行 MPI：`mpirun.mpich -n N output`

现在我们将看到两个示例（包含在分发 `/usr/doc/mpich/examples` 中）。`pi` 是一个用于分布式形式计算 PI 值的简单程序。

点对点通信：`pi.c`

编译：`mpicc -O pi.c`

执行 MPI：`mpirun -np N output`

执行 LAM：`mpirun -np N`（如果我们无法通过 `ssh` 直接访问，则必须使用 root 以外的其他用户）

```c
#include "mpi.h"
#include <stdio.h>
#define BUFFEN 512

main(int argc, char *argv[]) {
    int myid, numprocs;
    char buffer[BUFFER], processor_name[MPI_MAX_PROCESS_NAME];
    MPI_Status status;

    /* 必须放在 MPI 调用之前，始终如此 */
    MPI_Init(&argc,&argv);
    MPI_Comm_size(MPI_COMM_WORLD, &numprocs);
    /* 表示组中的进程数 */
    MPI_Comm_rank(MPI_COMM_WORLD, &myid);
    /* 进程的 ID */
    MPI_Get_processor_name(processor_name, &namelen);
    /* 进程名称 */
    fprintf(stderr, "Process %d at %s\n", myid, processor_name);
    strcpy(buffer, "Hello!");
    if (myid != numprocs)
        next = 0;
    else
        next = 1;

    if (myid == 0) { /* 如果是第一个... */
        if (n== 0) n = 100; else n = 0;
        starttime = MPI_Wtime();} /* 时钟 */
        MPI_Bcast(&n, 1, MPI_INT, 0, MPI_COMM_WORLD); /*广播到其余部分*/
        /*从第4个参数发送到
        组中的进程。所有不是0的进程
        将从参数4或参数-进程0拷贝缓冲区-*/1.*:buffer*/
        printf("%d received '%s\n", myid, buffer)
    } else {
        printf("%d receiving \n", myid);
        MPI_Recv(buffer, BUFFEN, MPI_CHAR, MPI_ANY_SOURCE, 99, MPI_COMM_WORLD, &status);
        /* 阻塞式接收, 1:buffer, 2:size, 3:type, 4:source, 5:tag, 6:context, 7:status */
        printf("%d received '%s\n", myid, buffer);
        MPI_Send(buffer, strlen(buffer)+1, MPI_CHAR, next, 99, MPI_COMM_WORLD);
        printf("%d sent '%s\n", myid, buffer);
    }
    MPI_Barrier(MPI_COMM_WORLD); /* 同步所有进程 */
    MPI_Finalize(); /* 释放资源并结束 */
    return (0);
}
```

# 分布式进程计算：pi

```cpp
2nd :size, 3rd :type, 5th :group */
if (n == 0) done; else {
    h = 1.0 / (double) n;
    sum = 0.0;
    for (i = myid + 1; i < n; i += numprocs) {
        x = h * (double)i - 0.5); sum += f(x);
    }
    mypi = h; sum;
```

`MPI_Reduce(mypi, &pi, MPI_DOUBLE, MPI_SUM, 0,`

`MPI_COMM_WORLD);`

/* 使用 `MPI_SUM` 操作合并组中每个进程的发送缓冲区（Send Buffer）元素，并将结果返回到接收缓冲区（Recv Buffer）。它必须由组中的所有进程调用，使用相同的参数列表/*

sendbuffer, 2nd

recvbuffer, 3rd :size, 4th :type, 5th :oper, 6th :root, 7th

:context*/
