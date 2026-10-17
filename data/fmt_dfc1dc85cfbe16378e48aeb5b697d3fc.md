
一旦获取了 `tar` 包，你就可以解压它，配置软件，然后为你的系统进行编译和安装：

在开始软件构建时，你将获得 `make` 命令的正常输出。构建将耗费几分钟到一小时不等，取决于你的环境。平均而言，完成配置、构建和安装步骤大约需要 15 分钟。

除了安装在 `/usr/lib/mpich-1.2.5.2` 下的基础软件外，在构建和安装完成后，若干软件工具被放置在 `/usr/lib/mpich/bin` 目录下。（你需要修改用户的 `PATH` 环境变量以包含运行 MPI 命令的正确目录。这可以被视为 MPICH 软件所需配置的一部分。）这些工具包括 `mpirun` 命令，以及用于将 C++ (`mpicc`)、C (`mpicc`) 和 FORTRAN (`mpif77` 和 `mpif90`) 与相应库链接的工具。我没有在书中涵盖开发、编译和链接 MPI 命令的细节；有几本很好的书籍可以参考。你可以通过浏览器打开 `/usr/lib/mpich-1.2.5.2/index.html` 或使用 `mpiman` 命令获取 HTML 格式的简单编程手册。

我们可以使用位于 `/usr/lib/mpich-1.2.5.2/examples` 中的示例程序在当前机器上测试编译和安装。让我们编译 `cpi` 示例（它可以计算 pi 的值），以非零 root 身份登录，并在本地系统上使用 `mpirun` 执行程序：

```bash
# cd /usr/lib/mpich-1.2.5.2/examples

# make cpi

# su - rob

# cd /usr/lib/mpich-1.2.5.2/examples

[rob@cs01 examples]$ /mpirun -np 1 cpi

Process 0 on cs01.cluster.local

pi is approximately 3.1416009869231254, Error is
0.0000083333333323
wall clock time = 0.000418
```

关于参与 MPICH 可执行程序的系统信息需要输入 `/usr/lib/mpich-1.2.5.2/share/machines.<ARCH>` 中。该文件在我的系统中名为 `machines.LINUX`，包含了主机名行，或者主机名后跟对于带有多个 CPU 的 SMP 机器的 `<number_of_cpus>`。

### 15.2.3 使用 mpirun

使用 `mpirun` 是测试 MPICH 软件安装的一种有效方法。然而通常情况下，你的集群可能会使用 OpenPBS 或 Platform Computing 的 LSF 等批处理队列软件的其他执行设施。在集群上运行一些测试以验证功能并查看设置测试所需的某些步骤是一个好主意。关于许多选项的更多信息可以在 MPICH 文档中找到。

如前所述，`mpirun` 命令假设有一个底层的远程访问服务来启动并行应用程序组件。显然，使用标准的 BSD R 服务是不安全且不受欢迎的选项。这意味着你应该使用 Kerberos 版本的 R 服务或 SSH 作为远程访问 shell。这些服务的配置之前已经介绍过。让我们使用 SSH，因为它在环境中已经存在。

`tmachines` 程序通常要求集群中的系统能够访问共享文件系统、具有一致的用户标识和权限，并且在相同位置拥有 `/usr/lib/mpich-1.2.5.2/share/machines.LINUX` 文件列出的机器。实际上，这个“程序”是一个 shell 脚本，你可以通过运行 `tmachines -v` 或查看脚本中的命令来观察其测试。

启用测试所需的步骤如下：

- 在所有切片上安装 MPICH。
- 配置 `/usr/lib/mpich-1.2.5.2/share/machines.LINUX` 文件，包含参与测试的机器列表。
- 以用户登录并假设主目录（此步骤假设该目录在所有系统中都是可用的）。
- 为用户生成 `${HOME}/ssh/authorized_keys` 并确保它包含每个主机的密钥（如果你对密钥使用了密码，那么配置 `ssh-agent` 将非常节省时间）。
- 将 `MPIRUNCOMMAND` 环境变量设置为 `ssh` 以使用该服务。
- 运行 `/usr/lib/mpich-1.2.5.2/sbin/tstmachines` 来测试一致性。

现在我们可以使用 MPICH 示例之一的刚刚编译的 `cpi` 对配置进行更通用的测试。在安装了 MPICH 的每台机器上，执行：

```bash
# cd /usr/lib/mpich-1.2.5.2/examples

# make cpi
```

这将所有客户端的相同位置创建一个该可执行文件。此外，你可以编译该执行文件并将其推送到计算切片。例如，SystemImager 允许你只更新“黄金客户端”中的可执行文件，然后将其推送到关联客户端。

一旦在测试的所有计算切片上编译并安装了可执行文件，我们就可以继续。我们将通过运行刚刚编译的 `cpi` 对 MPICH 安装进行简单的测试，以计算 pi 的近似值：

- 该示例是一个相当简单的程序，它是 MPI 编程环境的良好介绍。其准确性随着进行计算的并行组件数量的增加而提高。

# MPICH 库

```bash
# cd /usr/lib/mpich-1.2.5.2/examples

$ cd .

$ ./mpirun -np <N> cpi
```

四节点运行的示例输出如下：

```bash
$ cd /usr/lib/mpich-1.2.5.2/examples

[rob@cs01 examples]$ ./mpirun -np 4 cpi

Process 0 on cs01.cluster.local
Process 1 on cs02.cluster.local
Process 2 on cs03.cluster.local
Process 3 on cs04.cluster.local

pi is approximately 3.1416009869231245, Error is
0.000008333333314
wall clock time = 0.007258
```

通过这样的测试，我们已经验证了目标节点上 MPICH 软件的安装。应用程序运行完成这一事实说明我们的操作是正确的。

`mpirun` 命令用于管理远程调度组件的远程登录。这些登录必须通过在每个远程客户端上查找适当的信息来验证用户的 ID 或凭据。在用户主目录中对登录过程和启动文件进行正确配置，是使用 `mpirun` 成功启动并行作业的前提。例如，如果 SSH 启用了 X11 转发，登录过程可能会产生关于 X11 授权失败的冗余消息。远程访问应该经过正确配置，以处理交互式和非交互式连接。

MPICH 为 `ch_p4` 设备提供了另一种名为“安全守护进程（secure daemons）”的调度机制。这些守护进程使用 BSD `userRouter` 来检查用户是否允许访问系统，如果安全性是你的环境中问题，这种访问可能是不允许的。此外，安全守护进程仅适用于 `ch_p4` 设备和底层 TCP/IP 协议。

这种调度方法既不是通用的安全方案，但它通过从 `mpirun` 直接访问守护进程，对远程系统的单个 RSH 访问进行跨时间的调度。守护进程必须在目标系统上启动，可以是手动启动，也可以使用提供的脚本：`/usr/lib/mpich-1.2.5.2/sbin/chp4_servs`。一旦启动了守护进程，就可以告诉 `mpirun` 命令使用安全访问，既可以通过指定指向守护进程端口的命令选项，也可以通过两个环境变量：

```bash
$ mpirun -p4ssport <port-number> -np 4 cpi

$ export MPI_USEPASSPORTPORT=yes

$ export MPI_P4SSPORT=<port-number>

$ mpirun -np 4 cpi
```
