
## 11.7 使用 PVM

本节描述了如何设置 PVM 软件包，如何配置一个简单的虚拟机，以及如何编译和运行随 PVM 提供的示例程序。第一部分描述了 PVM 的简单用法以及在设置和运行 PVM 过程中最常见的问题。后一部分描述了可用于自定义 PVM 环境的一些更高级选项。

### 11.7.1 设置 PVM

PVM 受欢迎的原因之一是其设置和使用简单。

PVM 必须由具有管理员访问权限的用户安装。随后，只要管理员未限制对任何 PVM 安装文件的访问权限，它就可以供机器上的所有用户使用。

PVM 的 Windows 版本以 WinZip 文件形式分发，其中包含一个 **InstallShield** 自解压可执行文件。由于 PVM 安装过程将确认编译器的位置和配置，因此用于配合 PVM 的编译器应已安装。基于此基本信息，用户只需在安装过程中始终点击 *Next*（下一步）即可成功安装 PVM。Windows 安装过程中的一个选项会询问这是服务器安装还是客户端安装。对于基于 Windows 的集群，必须至少进行一次 PVM 服务器安装。这是因为服务器安装包含所有 PVM 源代码和库，而客户端安装则指向一个服务器安装，从中可以访问相应的 PVM 程序。当然，也可以为集群的所有节点执行服务器安装，从而避免在运行时客户端通过网络访问程序的需求及相关成本。

默认情况下，安装会将 PVM 系统放在目录 `C:\Program Files\PVM3.4` 中。（不过，如果您希望指定其他位置，可以使用 *Browse*（浏览）按钮。）选择 *Next* 继续，以选择 PVM 用于临时运行时文件的位置。最常见的位置是 `C:\TEMP`。输入此位置，按 *Next* 继续进入设置类型屏幕。选择 *Typical*（典型）安装可确保执行完整安装。按 *Next* 继续进入 C 编译器指定屏幕。从屏幕中选择 C 编译器选项，按 *Next* 继续。如果选择 *None*（无），下一个将是 Fortran 编译器指定屏幕。如果选择了已安装的编译器，接下来出现的目标屏幕将包含编译器 `include` 和 `lib` 目录的正确位置。按 *Next* 继续进入 Fortran 编译器指定屏幕。如果选择了未安装的编译器，您将收到警告消息，并被要求输入编译器 `include` 和 `lib` 目录所在的位置。输入此信息，按 Next 继续进入 Fortran 编译器指定屏幕。

Fortran 编译器指定与上述 C 选择类似。安装过程会在适当的程序文件夹中添加程序图标。只需接受默认值 PVM 3.4，按 Next 继续。屏幕显示刚刚选择的当前设置。当您按下 Next 时，InstallShield 过程开始复制文件，并在状态栏上显示进度。根据系统性能，这可能需要一两分钟。文件复制完成后，您将收到通知，告知 PVM 注册表值将被添加到系统中。按 OK 继续。如果没有足够空间来构建 PVM，系统将询问是否增加 `CONFIG.SYS` 中的环境空间。按 Yes 继续。下一个屏幕说明设置已完成，并提供查看 ReadMe 和帮助文件的选项以及在此机器上启动 PVM 守护进程选项。这些现在可以跳过，因为稍后都可以执行。按 Finish 进入最终设置屏幕。机器必须重新启动后 PVM 才能就绪使用。

#### Windows 网络文件

**LMHOSTS** 和 **HOSTS** 都是微软 TCP/IP for Windows 使用的文件。这两个文件包含集群节点名称和 IP 信息，以便 Windows 网络能够本地解析机器和主机名。这两个文件都位于 `C:\WINNT\system32\drivers\etc` 目录中。构建 Windows 系统时会在该位置放置示例文件。示例文件包含有关指令选项的额外信息。这里只讨论 PVM 安装所必需的那些内容。

**LMHOSTS** 包含 IP 地址到计算机名称的映射。每个条目占一行，IP 地址后跟相应的计算机名称，然后是 `#PRE`，这会使该条目预加载到名称缓存中。每行上的每个条目之间必须至少有一个空格。

```
# Filename: LMHOSTS
134.123.10.30    node1    #PRE
134.123.10.31    node2    #PRE
134.123.10.32    node3    #PRE
134.123.10.33    node4    #PRE
```

**HOSTS** 包含 IP 地址到主机名的映射。每个条目占一行，第一列是 IP 地址，后跟相应的主机名。每行上的每个条目之间必须至少有一个空格。

```
# Filename: HOSTS
```

在本节中，我们提供了用 Fortran 和 C 编写的各种示例程序。这些示例展示了编写 PVM 程序的各种方式。有些将应用程序划分为两个独立的程序，而有些则使用单个程序并通过条件语句来处理生成和计算阶段。这些示例展示了不同的通信风格，既包括工作进程之间的通信，也包括工作进程和主进程之间的通信。在某些情况下，消息用于同步，而在其他情况下，主进程在不再需要工作进程时简单地将其终止。我们希望这些示例能帮助您更好地理解如何编写更好的 PVM 程序并评估其中涉及的设计权衡。

工作进程基于数据集迭代计算解（每次迭代都与邻居交换边界信息），并将产生的部分解发回给主进程。作为在工作进程中使用无限循环的替代方案，我们可以向从节点发送一条特殊消息，指示其退出。相反，我们简单地在工作进程中使用无限循环，并从主程序终止它们。第三种选择是让工作进程只执行一次，在处理完来自主程序的单个数据集后退出。这需要将主程序的生成调用放入 **heat.c** 的主 **for** 循环内。虽然此选项可行，但它会给整体计算带来不必要的开销。

在每个时间步和每个计算阶段之前，温度矩阵的边界值会被交换。左手边界元素先发送给左邻居任务并从右邻居任务接收。对称地，右手边界元素发送给右邻居然后从左邻居接收。检查邻居的任务 ID，以确保不会尝试向不存在的任务发送或接收消息。

```c
/*
    heatslv.c

    The slaves receive the initial data from the host,
    exchange boundary information with neighbors,
    and calculate the heat change in the wire.
    This is done for a number of iterations, sent by the master.

*/
#include "pvm3.h"
#include <stdio.h>

int num_data;

main()
{
    int mytid, left, right, i, j, master;
    int timestep;

    double *init, *A;
    double leftdata, rightdata, delta, leftside, rightside;
    /* enroll in pvm */
    mytid = pvm_mytid();
    master = pvm_parent();

    /* receive my data from the master program */
    while(1) {
        pvm_recv(master, 4);
        pvm_upkin(&left, 1, 1);
        pvm_upkin(&right, 1, 1);
        pvm_upkin(&timestep, 1, 1);
        pvm_upkdouble(&delta, 1, 1);
        pvm_upkin(&num_data, 1, 1);
        init = (double *) malloc(num_data*sizeof(double));
        pvm_upkdouble(init, num_data, 1);

        /* copy the initial data into my working array */

        A = (double *) malloc(num_data * timestep * sizeof(double));
        for (i = 0; i < num_data; i++) A[i] = init[i];

        /* perform the calculation */

        for (i = 0; i < timestep-1; i++) {
            /* trade boundary info with my neighbors */
            /* send left, receive right */
            if (left != 0) {
                pvm_initsend(PvmDataDefault);
                pvm_pkdouble(&A[wh(i,0)],1,1);
                pvm_send(left, 5);
            }
            if (right != 0) {
                pvm_recv(right, 5);
                pvm_upkdouble(&rightdata, 1, 1);
                /* send right, receive left */
                pvm_initsend(PvmDataDefault);
                pvm_pkdouble(&A[wh(i,num_data-1)],1,1);
                pvm_send(right, 6);
            }
            if (left != 0) {
                pvm_recv(left, 6);
                pvm_upkdouble(&leftdata,1,1);
            }

            /* do the calculations for this iteration */

            for (j = 0; j < num_data; j++) {
                leftside = (j == 0) ? leftdata : A[wh(i,j-1)];
                rightside = (j == (num_data-1)) ? rightdata : A[wh(i,j+1)];
                if ((j==0)&&(left==0))
                    A[wh(i+1,j)] = 0.0;
                else if ((j==(num_data-1))&&(right==0))
                    A[wh(i+1,j)] = 0.0;
                else
                    A[wh(i+1,j)] =
                        A[wh(i,j)]+delta*(rightside-2*A[wh(i,j)]+leftside);
            }
        }

        /* send the results back to the master program */

        pvm_initsend(PvmDataDefault);
        pvm_pkdouble(&A[0],num_data*timestep,1);
        pvm_send(master,7);
    }
    /* just for good measure */
    pvm_exit();
}

int wh(x, y)
int x, y;
{
    return(x*num_data+y);
}
```
