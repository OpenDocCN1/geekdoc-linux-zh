
`filename[3][0]` = "graph4";

```c

deltalt[0] = 5.0e-1;

deltalt[1] = 5.0e-3;

deltalt[2] = 5.0e-6;

deltalt[3] = 5.0e-9;

```

```c

/* 加入 pvm */

mytid = pvm_mytid();

```

```c

/* 启动从任务 */

info = pvm_spawn(SLAVENAME, char **)PvmTaskDefault, NPROC, task_id);

/* 创建初始数据集 */

for (i = 0; i < SIZE; i++)

  init[i] = sin(M_PI * (double)i / (double)(SIZE-1));

init[0] = 0.0;

init[SIZE-1] = 0.0;

```

```c

/* 为不同的 delta t 值运行问题 4 次 */

for (l = 0; l < 4; l++) {

    delta2 = (delta[l]/pow(1.0/(double)SIZE,2.0));

    /* 为本次运行开始计时 */

    time(&t0);

    time = t0;

    /* 将初始数据发送给从进程 */

    /* 包含交换边界数据的邻居信息 */

    for (i = 0; i < NPROC; i++) {

        pvm_insend(PvmDataDefault);

        left = (i == 0) ? 0 : task_ids[i-1];

        pvm_pkint(&left, 1, 1);

        right = (i == (NPROC-1)) ? 0 : task_ids[i+1];

        pvm_pkint(&right, 1, 1);

        pvm_pkint(&step, 1, 1);

        pvm_pkdouble(&delta2, 1, 1);

        pvm_pkint(&num_data, 1, 1);

        pvm_pkdouble(&init[num_data*i], num_data, 1);

        pvm_send(task_ids[i], 4);

    }

    /* 等待结果 */

}

```

```c

for (i = 0; i < NPROC; i++) {

    pvm_recv(task_ids[i]);

}

```

`heats` 程序执行导线热扩散的实际计算。工作程序由一个无限循环组成，从主机接收初始数据集，根据该数据集迭代计算解（在每次迭代中与邻居交换边界信息），并将生成的部分解发送回主程序。

```c

int wh(x, y) {

    int x, y;

    return(x*num_data+y);

}

```

# 使用 PVM 进行并行编程

```c

master = pvm_parent();

```

```c

/* 从主程序接收我的数据 */

while(1) {

    pvm_recv(master, 4);

    pvm_upint(&left, 1, 1);

    pvm_upint(&right, 1, 1);

    pvm_upint(&timestep, 1, 1);

    pvm_upkdouble(&delta, 1, 1);

    pvm_upkdouble(&num_data, 1, 1);

    init = (double *) malloc(num_data*sizeof(double));

    pvm_upkdouble(init, num_data, 1);

```

```c

/* 将初始数据拷贝到我的工作数组中 */

A = (double *) malloc(num_data * timestep * sizeof(double));

for (i = 0; i < num_data; i++) A[i] = init[i];

```

```c

/* 执行计算 */

for (i = 0; i < timestep-1; i++) {

    /* 与邻居交换边界信息 */

    /* 发送、接收右 */

    if (left != 0) {

        pvm_initend(PvmDataDefault);

        pvm_pkdouble(&A[wh(i,0)],1,1);

        pvm_send(left, 5);

    }

    if (right != 0) {

        pvm_recv(right, 5);

        pvm_upkdouble(&rightdata, 1, 1);

        /* 发送、接收左 */

        pvm_initend(PvmDataDefault);

        pvm_pkdouble(&A[wh(i,num_data-1)],1,1);

        pvm_send(right, 6);

    }

    if (left != 0) {

        pvm_recv(left, 6);

        pvm_upkdouble(&leftdata,1,1);

    }

```

```c

/* 执行本次迭代的计算 */

for (j = 0; j < num_data; j++) {

```

```c

leftside = (j == 0) ? leftdata : A[wh(i,j-1)];

rightside = (j == (num_data-1)) ? rightdata : A[wh(i,j+1)];

if ((j==0)&&(left==0))

    A[wh(i,j)] = 0.0;

else if ((j==num_data-1)&&right==0))

    A[wh(i+1,j)] = 0.0;

else

    A[wh(i+1,j)]=

        A[wh(i,j)]+delta*(rightside-2*A[wh(i,j)]+leftside);

```

```c

/* 仅为了万一 */

pvm_exit();

```

```c

int wh(x, y)

{

    return(x*num_data+y);

}

```

在本节中，我们提供了多种用 Fortran 和 C 编写的示例程序。这些示例演示了编写 PVM 程序的不同方法。一些示例将应用程序分为两个独立的程序，而另一些则使用单个程序并通过条件判断来处理扩展和计算阶段。这些示例展示了工作任务之间以及主任务之间不同的通信风格。在某些情况下，消息被用于同步，而在另一些情况下，主进程在不再需要时直接杀死工作进程。我们希望这些示例能帮助你理解如何编写更好的 PVM 程序，并评估涉及的设计权衡。

## 11.7 使用 PVM

本节描述了如何设置 PVM 软件软件包、如何配置简单的虚拟机，以及如何编译和运行 PVM 提供的示例程序。第一部分描述了 PVM 的直接用法以及在设置和运行 PVM 时最常见的问题。后半部分描述了一些用于自定义 PVM 环境的更高级选项。

### 11.7.1 设置 PVM

PVM 受欢迎的原因之一是它设置和使用非常简单。安装 PVM 不需要特殊权限。任何在主机上拥有有效登录权限的人都可以进行安装。此外，一个机构内只需要一个人获取并安装 PVM，该机构的所有员都可以使用它。

PVM 在启动和运行期间使用环境变量。每个 PVM 用户都需要为 PVM 设置这两个变量。第一个变量是 `PVM_ROOT`。第二个变量是 `PVM_ARCH`，它告诉 PVM 当前主机的架构，从而从 `PVM_ROOT` 目录中选择哪些可执行文件。

简单的方法是在你的 .cshrc 文件中设置这两个变量（假设你正在使用 csh）。以下是设置 PVM_ROOT 的示例：

```csh

setenv PVM_ROOT /home/username/pvm3

```

设置 `PVM_ARCH` 的推荐方法是将 `PVM_ROOT/lib/cshrc` 文件追加到你的 .cshrc 中。该存根（stub）应该放置在 PATH 和 `PVM_ROOT` 定义之后。该存根会自动确定此主机主机的 `PVM_ARCH`，并且当用户在不同架构之间共享公共文件系统（如 NFS）时特别有用。

如果 PVM 已经安装在你的站点上，你可以直接跳到“启动 PVM”。PVM 源码带有目录和 Makefile。

### 安装总结
- 在 .cshrc 中设置 `PVM_ROOT` 和 `PVM_ARCH`。
- 使用 `PVM_ROOT/lib/cshrc` 存根自动确定 `PVM_ARCH`。
- 使用主机文件（hostfile）一次配置多个主机。

### 11.7.2 启动 PVM

在我们介绍如何编译和运行程序之前，你应该先确保 PVM 已经启动。在安装了 PVM 的任何主机上，你可以输入：

```bash

% pvm

```

然后你会收到“PVM running”的消息。向虚拟机添加主机，输入：

```bash

pvm add

```

删除已在虚拟机中的主机，输入：

```bash

pvm delete

```

查看正在运行的任务，输入：

```bash

pvm ps

```

查看虚拟机的配置，输入：

```bash

pvm conf

```

如果你不想每次都输入大量的主机名，可以使用主机文件选项。你可以每行列出一个主机名并输入：

```bash

% pvm hostfile

```

PVM 会在控制台出现之前添加列出的主机。可以在主机文件中按主机指定某些选项。

停止 PVM 并关闭虚拟机，输入：

```bash

pvm halt

```

# 使用 PVM 进行并行编程

该命令杀死 PVM 任务，关闭虚拟机并退出控制台。

XPVM 中名为“hosts”的菜单会弹出一个主机列表。通过点击主机名，它就会被添加并在虚拟机的动画中显示图标。如果你点击已在虚拟机中的主机，它会被删除。XPVM 在启动时会读取 `$HOME/xpvm.hosts` 文件，该文件是显示在此菜单中的主机列表。如果不加载 "&”，它们将在启动时一次性添加。

退出和停止按钮的作用与 PVM 控制台类似。如果你退出 XPVM 并重启它，XPVM 将自动显示运行中的虚拟机。练习使用 XPVM 启动和添加主机。

### 11.7.3 运行 PVM 程序

在本节中，你将学习如何编译和运行 PVM 软件提供的示例程序。这些示例程序为你编写 PVM 程序提供了非常有用的模板。

第一步是将示例程序拷贝到你的区域：

```bash

% cp -r $PVM_ROOT/examples $HOME/pvm3/examples

% cd $HOME/pvm3/examples

```

`examples` 目录包含一个 `Makefile.aimk` 和 `Readme` 文件，描述了如何构建这些示例。PVM 提供了一个与架构无关的 make 工具——`aimk`，它可以确定 `PVM_ARCH` 并将任何特定系统的库链接到你的应用程序。当你将 `cshrc.stub` 放入 `.cshrc` 时，`aimk` 会自动添加到你的 `$PATH` 中。使用 `aimk` 允许你可以在跨架构编译时保持源代码和 makefile 不变。

主/工作节点（master/worker）编程模型是集群计算中最常用的模型。要编译主/从 C 语言示例，输入：

% aimk slave

如果你更倾向于使用 Fortran，可以使用以下命令编译 Fortran 版本：

% aimk fmaster slave

取决于 `PVM_ROOT` 的位置，Fortran 示例顶部的 `INCLUDE` 语句可能需要修改。如果 `PVM_ROOT` 不是 `$HOME/pvm3`，则需要将包含路径指向 `$PVM_ROOT/include/fpvm3.h`。注意，PVM_ROOT 在 Fortran 内部不会被展开，因此你必须插入实际路径。

`myfile` 将可执行文件生成到 `$HOME/pvm3/bin/PVM_ARCH`，这是 PVM 在所有主机上查找的默认位置。如果文件系统在所有 PVM 主机之间不是共享的，你需要在所有 PVM 主机上构建或拷贝（取决于架构）这些可执行文件。

在一个窗口中启动 PVM 并配置一些主机。这些示例设计为运行在任意数量的主机上（包括一台）。在另一个窗口中，进入 PVM 可执行文件所在的目录并输入：

% master

程序会询问任务数量。这个数字不需要与示例中的主机数量匹配。尝试几种组合。

第一个示例说明了从虚拟机中任何主机的提示符运行 PVM 程序的能力。这就是你如何在工作站上运行串行输出程序的方法。下一个示例（一个名为 `hitc` 的主/从模型）展示了如何从 PVM 控制台以及 XPVM 产生 PVM 任务。

`hitc` 演示了使用任务池范式的动态负载均衡。在这一范式中，主程序管理任务队列，始终向空闲的从节点程序发送更多工作，直到队列为空。当主机计算能力差异很大时，这种范式非常有效，因为负载最轻或更强大的主机会承担更多工作，所有主机在问题结束前保持忙碌。编译 `hitc`，输入：

## 使用 PVM 进行并行编程

% aimk hitc hitc_slave

由于 `hitc` 不需要任何用户输入，它可以可以直接从 PVM 控制台产生。启动 PVM 控制台并添加几个主机。在 PVM 控制台提示符下，输入：

```
pvm> spawn -> hitc
```

"-> spawn" 选项会导致 `hitc` 和从节点中的所有打印语句出现在控制台窗口中。这在你调试第一个 PVM 程序时可能是一个非常有用的功能。你可能希望通过在 `hitc.f` 和 `hitc_slave.f` 中放置打印语句并重新编译来尝试此选项。

为了了解 XPVM 的实时动画能力，你可以再次使用 `hitc`。启动 XPVM 并构建一个具有四台主机的虚拟机。点击“tasks”，从菜单中选择“spawn”。在 XPVM 询问命令的地方输入 "hitc"，并点击“start”。你会看到 `hitc` 在被产生时亮起，并且所有在时空显示器中任务之间传输的消息都会显示。从“-> XPVM views”菜单中还可以选择其他几种视图。“task output”视图等同于 PVM 控制台中的 "->" 选项。它使所有任务的标准输出出现在弹出的窗口中。

从 XPVM（以及 PVM 控制台）产生的程序受限于一性限制：它们不能包含任何交互式输入，例如询问要启动多少个从节点或要解决多大的问题。这类信息可以从文件或命令行参数读取，但目前没有机制可以从键盘向潜在的远程任务获取用户输入。

## 11.8 PVM 控制台详情

PVM 控制台（称为 `pvm`）是一个独立的 PVM 任务，允许你交互式地查询和修改虚拟机。可以在虚拟机中的任何主机上多次启动和停止控制台，而不会影响 PVM 或任何可能正在运行的应用程序。

当控制台启动时，`pvm` 会确定 PVM 是否已经在运行，如果没有，则自动在主机上执行 `pvmd`，并向 `pvm` 传递命令行选项和主机文件。因此，PVM 不需要运行即可启动控制台。

```
pvm [-n<hostname>] [hostfile]
```

`-n` 选项用于为主节点 `pvmd` 指定另一个名称（以防主机名与所需的 IP 地址不匹配）。此功能在 Beowulf 集群中变得非常有用，因为集群节点有时位于自己的网络上。在这种情况下，前端节点将有两个主机名：一个用于集群，一个用于外部网络。`-n` 选项允许你在 PVM 启动期间直接指定集群名称。

一旦启动，控制台会打印提示符：

```
pvm>
```

并从标准输入中接受命令。可用命令如下：

-   **add** 后跟跟一个或多个主机名，将这些主机添加到虚拟机。
-   **alias** 定义或列出命令别名。
-   **conf** 列出虚拟机的配置，包括主机名、pvm 任务 ID、架构类型和相对速度评分。
-   **delete** 从虚拟机中删除主机名。
-   **echo** 回显消息。
-   **halt** 关闭控制台。
-   **help** 显示可用命令的信息。
-   **id** 打印控制台的 ID。
-   **jobs** 列出正在运行的任务。
-   **kill** 终止进程。
-   **mstat** 显示主机的状态。
-   **ps -a** 列出所有进程。
-   **quit** 退出控制台。
-   **setenv** 设置环境变量。
-   **sig** 发送信号。
-   **version** 打印 PVM 的版本。

## 使用 PVM 进行并行编程

主机文件（hostfile）允许用户指定参与虚拟机的主机。主机文件可以是主机名的简单列表，也可以包含每个主机的更多选项。

主机文件中可用选项：

-   **lo**: 为主机指定另一个登录名。
-   **so**: 导致 PVM 在此主机上提示密码。
-   **dx**: 指定 pvm 默认位置以外的路径。
-   **ep**: 指定搜索用户可执行文件的路径。
-   **sp**: 指定主机的相对计算速度。

```
alias help
alias j
setenv PVM_EXPORT
id
```

PVM 支持使用多个控制台。可以在同一台机器上运行多个控制台。

**bx= 调试器位置** 指定了在 spawn 过程中如果请求调试时，在此主机上调用哪个调试器脚本。请注意，也可以设置环境变量 `PVM_DEBUGGER`。默认调试器为 `pvm3/lib/debugger`。

**wd= 工作目录** 指定了在该主机上执行的所有派生任务将运行的工作目录。默认值为 `$HOME`。

**so=ms** 指定在该主机上手动启动一个从机 pmd。如果 `rsh` 和 `rexec` 网络服务被禁用但存在 IP 连通性，则这样做非常有用。使用此项时，你将在 pvm3 的 `tty` 中看到以下内容：
