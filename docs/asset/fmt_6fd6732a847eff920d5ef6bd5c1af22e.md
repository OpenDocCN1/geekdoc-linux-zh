
`int info = pvm_notify( int EventType, int msgtag, int cnt, int *ids )`

`EventType`选项有`PvmTaskExit`、`PvmHostDelete`和`PvmHostAdd`。对于应用程序希望通知的每种事件类型，必须单独调用一次通知函数。`msag`参数指定了监听事件时将使用的消息标签。`cnt`参数是`ids`数组中请求通知的任务或节点 ID 的数量。

鉴于`pvm_notify`命令的灵活性，应用程序设计为接收 PVM 系统通知的方法有几种。第一种方案是设计一个独立的观察任务（watcher task）。在集群中会生成一个或多个此类观察任务，它们通常还承担管理应用程序恢复阶段的额外责任。这种方法的优点是应用程序代码可以保持更简洁。注意，在 manager/worker 方案中，manager 经常担任观察者的角色。

第二种方案让应用程序任务相互观察。一种常用方法是让每个任务在本地环中观察其邻居。因此，每个任务只需观察一两个其他任务。另一种常见但不特别高效的方法是让每个任务观察所有其他任务。记住，是 PVM 系统在进行监控，而不是应用程序任务。监控开销在所有选项中是共享的。区别在于发生故障时发送的通知消息数量。

恢复很大程度上取决于应用程序中使用的并行算法类型。常用的选项包括从头重新启动、回滚到上一个检查点，或重新分配失败任务的工作。

第一种选项实现最简单，但计算开销最大。许多批系统使用这种选项，因为它不需要了解应用程序的内容。它保证了即使发生故障，应用程序也能完成，尽管不能保证这需要多久。平均而言，时间少于正常运行时间。对于短运行的应用程序，这是最佳选项。

对于运行时间较长的应用程序，检查点（checkpoint）是一种常用选项。使用这种选项，你必须理解应用程序并对其进行修改，以便应用程序从输入数据文件重启。然后你必须修改应用程序定期写入此类数据文件。在发生故障时，只会丢失从上一个检查点开始的计算。应用程序从最后成功写入的数据文件重启。多久写入一次检查点取决于重启文件的大小以及应用程序将运行多久。对于运行数的大型科学应用，通常每几小时执行一次检查点。

## 使用 PVM 构建容错自适应程序

请注意，如果故障是由集群节点丢失引起的，那么在节点被修复或被集群中的另一个节点替换之前，应用程序无法重启。重启文件几乎总是假设重启时可用节点数量相同的情况下写入的。

在基于 manager/worker 方案的特殊情况下，通常可以将发送给失败 worker 的作业分配给另一个 worker，或者生成一个替换的 worker 来占据其位置。manager/worker 是 Beulf 集群中一种非常流行的并行编程方案，这种特殊情况经常发生。下面是一个 manager/worker 程序示例。

- 容错管理器 / 工人示例
- 使用通知和任务生成。
- example1。

```c
#include <stdio.h>
#include <math.h>
#include <pvm3.h>
#define NWORK 4
#define NPROB 10000
#define MSGTAG 121
int main()
{
    double sum = 0.0, result, input;
    int tids[NWORK], probs[NPROB], sent=0, recvd=0, cc=0, i, j, marker, src, numt;
    /* 管理管理器 */
    if ((cc = pvm_parent()) == PvmParent || cc == PvmSet) {
        /* 生成工人任务 */
        numt = pvm_spawn("example1", (char **) NULL, PvmTaskDefault, (char *) NULL, numt, tids);
        /* 为生成的任务设置通知 */
        pvm_notify(PvmTaskExit, MSGTAG, numt, tids);
        /* 向生成的工人发送问题 */
        for(i=0; i < NPROB; i++) probs[i] = -1;
        for(i=0; i < numt; i++) {
            pvm_pkint(&i, 1, 1); /* 有效问题标记 */
            input = (double) (i + 1);
            pvm_pkdouble(&input, 1, 1);
            pvm_send( tids[i], MSGTAG );
            probs[i] = i; sent++; /* 问题 */
        }
        /* 收集结果 / 处理故障 */
        do {
            /* 接收结果 */
            bufid = pvm_recv(-1, MSGTAG);
            pvm_upint(&marker, 1, 1);
            /* 处理通知 */
            if ( marker > 0 ) {
                /* 查找失败任务索引 */
                for ( i=0, next = -1; i < numt; i++ )
                    if ( tids[i] == marker ) {
                        /* 查找发送给任务的问题 */
                        for ( j=(sent-1); j > 0; j--)
                            if ( probs[j] == i ) {
                                /* 生成替换任务 */
                                if ( pvm_spawn("example1", (char **) NULL,
PvmTaskDefault, (char *) NULL, 1,
                                &tids[i]) == 1 ) {
                                    pvm_notify( PvmTaskExit, MSGTAG, 1,
                                    &tids[i] );
                                    next = i; sent--;
                             }
                            }
                        }
                        probs[j] = -1; /* 插入问题 */
                        break;
                    }
            } else {
                /* 获取源任务并累加解 */
                pvm_updouble(&result, 1, 1);
                sum += result;
                recvd++;
            }
            /* 获取任务索引 */
            pvm_bufinfo(bufid, (int *) NULL, &src);
            for ( i = 0; i < numt; i++ )
                if ( tids[i] == src ) next = i;
        } while (recvd < numt);
    }
    return 0;
}
```

# 基于 PVM 的容错自适应程序

```c
if ( next >= 0 ) {
    for ( i=0, input = -1.0 ; i < NPROB ; i++) {
        if ( probs[i] < 0 ) {
            input = (double) (i + 1);
            probs[i] = next; sent++; /* 下一个问题 */
            break;
        }
        pvm_itsend(PvmDataDefault );
        pvm_pkint(&ok, 1, 1); /* 有效问题标记 */
        pvm_pkdouble(&input, 1, 1);
        pvm_send(tids[next], MSGTAG );
        if ( input < 0.0 ) tids[next] = -1;
    }
}
while ( recvd < sent ) {
    printf("Sum = %lf\n", sum );
}
/* 如果我是一个工作任务 */
else if ( cc > 0 ) {
    /* 通知管理器失效 */
    pvm_notify(PvmTaskExit, MSGTAG, 1, &cc);
    /* Solving问题直到完成 */
    do {
        /* 从主节点获取问题 */
        pvm_recv(-1, MSGTAG );
        pvm_upint(&ok, 1, 1);
        if ( ok > 0 ) /* 主节点死亡 */
            break;
            pvm_updouble(&input, 1, 1);
            if ( input > 0.0 ) {
                /* 计算结果 */
                result = sqrt( 2.0 * input ) - 1.0;
                /* 将结果发送给主节点 */
                pvm_itsend(PvmDataDefault );
                pvm_pkint(&ok, 1, 1); /* 请求更多问题... */
                pvm_pkdouble(&result, 1, 1);
                pvm_send(cc, MSGTAG );
            }
    } else
        done = 1;
} while ( ! done );
}
}
```

```c
pvm_exit();
```

```c
return( 0 );
}
```

这个示例展示了另一个非常有用的函数：`pvm_spawn()`。启动替换机器的能力是容错中的一项强大功能。正如我们在下一节中看到的，它也是自适应程序中的关键函数。

```c
int numt = pvm_spawn( char *task, char **argv, int flag, char *node, int ntasks, int *tids )
```

`pvm_spawn()`例程在虚拟机上启动`ntasks`份可执行任务的副本。假设 PVM 虚拟机运行在 Beowulf 集群上。这里`argv`是指向任务参数数组的指针，数组末尾由`NULL`指定。`flag`参数用于指定选项，它是以下选项的和：

- `PvmTaskDefault`: 让 PVM 选择启动进程的位置
- `PvmTaskHost`: 使用`where`参数指定在特定的宿主机或集群节点上启动
- `PvmTaskArch`: 使用`where`参数指定在何种架构类上启动
- `PvmTaskDebug`: 在调试器下启动这些进程
- `PvmTaskTrace`: 使用 PVM 调用生成跟踪数据
- `PvmMppFront`: 在 MPP 前端/服务节点上启动
- `PvmHostComp`: 在互补宿主机上处理

例如，`flag = PvmTaskHost + PvmHostComp`会在指定节点（例如可能是管理器）的每个节点上启动任务。

返回时，`numt`是成功启动的任务数，如果无法启动任务则返回错误码。如果已启动，`pvm_spawn()`返回一个已启动任务的`tids`向量。如果某些任务无法启动，相应的错误码将放在向量的最后$(ntask - numt)$位置。

在上面的示例中，`pvm_spawn()`用于启动所有工作节点，并替换计算过程中失败的工作节点。这种容错方法对于持续运行且有稳定新工作流进入的应用非常有用，正如我们的两个初始示例那样。两者都使用了上述 PVM 示例代码的变体来实现解决方案。

## 基于 PVM 的容错与自适应程序

### 12.3 自适应程序

在本节中，我们将使用更多的 PVM 虚拟机函数来说明集群程序如何扩展，使其不仅能适应故障，还能适应许多指标和情况。第一个示例演示了一个并行应用程序，它根据应用程序的计算需求，通过添加和释放节点来动态调整虚拟机的大小。在橡树岭国家实验室的一个 128 处理器 Beowulf 集群上，每天都会使用一项由三个研究小组共享的功能。

```c
int numh = pvm_addhosts(char **hosts, int nhost, int *infos)
int numh = pvm_delhosts(char **hosts, int nhost, int *infos)
```

PVM 的`addhosts`和`delhosts`用于添加或删除虚拟机中的一组宿主机。在 Beowulf 集群中，这对应于从计算中添加或删除节点；返回的`numh`是成功添加或删除的数量。参数`infos`是一个长度为`nhost`的数组，包含每个被添加或删除节点的状态码。这允许你检查一组宿主机中的某一个是否导致了问题，而不是尝试重新添加或删除整个主机集。

- “自适应主机分配示例”根据不同的计算阶段动态从计算中添加和移除集群节点

```c
#include <stdio.h>
```

```c
mycxt = pvm_setcontext( oldcxt );
pvm_freecontext( mycxt );
```

```c
return;
```

PVM 内部一直有消息处理程序，它们用于控制虚拟机。在 PVM 3.4 中，定义和删除消息处理程序的能力被提升到了用户级，因此可以编写并行程序，这些程序可以在程序运行时添加新功能。
两个新的消息处理程序函数是：

```c
mhid = pvm_addhmf( src, tag, context, *function );
pvm_delhmf( mhid );
```

一旦任务添加了消息处理程序，每当带有指定的源、消息标签和通信上下文的消息到达该任务时，就会执行指定的函数。该函数将接收到该消息，以便在需要时可以对消息进行解包。PVM 对函数的复杂度没有设置任何限制，函数可以自由地进行系统调用或其他 PVM 调用。添加例程会返回一个消息处理程序 ID，该 ID 将用于删除消息处理程序的例程。

你可以设置的处理器数量没有限制，且每个应用程序任务可以独立地动态地添加和删除处理器。

通过设置消息处理程序，你现在可以编写能够动态更改底层虚拟机特征的程序。例如，可以添加消息处理程序来实现主动消息（active messages）；应用程序随后就可以使用这种通信形式，而不是典型的发送/接收（send/receive）。虚拟机的几乎每个功能都存在类似的机会。

应用程序适应虚拟机特征以满足其当前需求的能力是一项强大的能力，这种能力在 Beowulf 集群中尚未被充分利用。

```c
/* 使用用户定义的消息处理程序
* 适配可用的虚拟机功能。 */
```

```c
#include <stdio.h>
#include <pvm3.h>
```

```c
#define NWORK 4
#define MAIN_MSGTAG 123
#define CNTR_MSGTAG 124
```

int counter = 0;

```c
int handler( int mid ) {
    int ack, incr, src;
    /* 增加计数器 */
    pvm_upint(&incr, 1, 1);
    counter += incr;
    printf("%d\n", counter);
    /* 确认计数器任务 */
    pvm_bufinfo(mid, (*) NULL, (*) NULL, &src);
    pvm_itsend(PvmDataDefault);
    ack = ( counter > 1000 ) ? -1 : 1;
    pvm_pkint(&ack, 1, 1);
    pvm_send(src, CNTR_MSGTAG);
    return( 0 );
}
```

```c
int main( int argc, char **argv) {
    int ack, cc, ctx, bufid, incr=1, iter=1, max, numt, old, value=1, src;
    char *args[2];
```

```c
/* 如果我是管理任务 */
if ( cc = pvm_parent() == PvmNoParent || cc == PvmParentNotSet ) {
/* 为计数器任务消息生成新的消息上下文 */
    ctx = pvm_newcontext();
/* 为独立计数器注册消息处理函数 */
