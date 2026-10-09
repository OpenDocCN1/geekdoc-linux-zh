

args[0] = "worker";
nums = pvm_spawn( "example3", args, PvmTaskDefault,
          (char *) NULL, NWORK, (int *) NULL );

/* Increment & Return Worker Values */
do {
    /* Get Value */
    bufid = pvm_recv( -1, MAIN_MSGTAG );
    pvm_upkint( &value, 1, 1 );
    max = ( value > max ) ? value : max;
    printf( "recv'd value = %d\n", value );

    /* Send Reply */
    pvm_bufinfo( bufid, (int *) NULL, (int *) NULL, &src );
    if ( counter < 1000 ) value += iter++;
    else { value = -1; nums--; }   /* Tell Workers to Exit */
    pvm_initsend( PvmDataDefault );
    pvm_pkint( &value, 1, 1 );
    pvm_send( src, MAIN_MSGTAG );
} while ( nums > 0 );

printf( "Max Value = %d\n", max );

/* If I am a Worker Task */
else if ( cc > 0 && !strncmp( argv[1], "worker" ) ) {
/* Grow Values Until Done */
    do {
        /* Send Value to Master */
        value *= 2;
        pvm_initsend( PvmDataDefault );
        pvm_pkint( &value, 1, 1 );
        pvm_send( cc, MAIN_MSGTAG );
        /* Get Incremented Value from Master */
        pvm_recv( cc, MAIN_MSGTAG );
        pvm_upkint( &value, 1, 1 );
    } while ( value > 0 );
}

/* If I am a Counter Task */
else if ( cc > 0 && !strncmp( argv[1], "counter" ) ) {
/* Grow Values Until Done */
    do {
        /* Send Counter Increment to Master */
        pvm_initsend( PvmDataDefault );
        pvm_pkinf( &kin, 1, 1 );
        pvm_send( cc, CNTR_MSGTAG );
        incr += 2;
        /* Check Ack from Master */
        pvm_recv( cc, CNTR_MSGTAG );
        pvm_upkinf( &ack, 1, 1 );
    } while ( ack > 0 );
}

pvm_exit();
return( 0 );
}

在典型的消息传递系统中，消息是瞬态的，重点在于通过降低延迟和增加带宽来尽可能缩短其存在时间。但在当今并行的应用程序中，越来越多的情况下，如果能有一种方式来实现持久化消息，编程将会变得更加容易。这正是 PVM 中*消息盒（Message Box）*功能的目的。消息盒是虚拟机内部的一个元组空间。

消息盒由四个函数组成：

```c
index = pvm_putinfo( name, msgbuf, flag )
pvm_recvinfo( name, index, flag )
pvm_delinfo( name, index, flag )
pvm_getboxinfo( pattern, matching_names, info )
```

任务可以使用常规的 PVM 打包例程创建任意消息，然后使用 `pvm_putinfo()` 将此消息放入消息盒并附加一个关联的名称。任何知道该名称的 PVM 任务都可以检索此消息的副本。如果名称未知或正在动态变化，则可以使用 `pvm_getboxinfo()` 查找消息盒中活动的名称列表。该标志定义了存储消息的属性，例如谁允许删除此消息，此名称是否允许多个消息实例，以及对同一名称的写入是否覆盖消息。

消息盒已被用于许多其他目的。例如，PVM 的组服务器功能完全在新的消息盒函数中实现；Cumnivs 计算控制工具使用消息盒查询如何连接到远程分布式仿真的说明；性能监视器将其发现结果保存在消息盒中供其他工具使用。

在并行计算中实现持久化消息的能力，不仅在高性能计算中，也在协作技术中开启了众多新的应用可能性。

```c
/* Example using persistent messages to adapt to change
 * Monitor tasks are created and killed as needed
 * Information is exchanged between these tasks using persistent messages
 */
#include <stdio.h>
#include <sys/time.h>
#include <pvm3.h>
#define MSGBOX "load_stats"
int main()
{
    int cc, elapsed, i, index, load, num;
    struct timeval start, end;
    double value;

    /* If I am a Manager Task */
    if ((cc == pvm_parent()) == PvmNoParent || cc == PvmParentNotSet) {

        /* Periodically Spawn Load Monitor, Check Current System Load */
        do {
            /* Spawn Load Monitor Task */
            if ((pvm_spawn("example4", (char **) NULL, PvmTaskDefault,
                           (char *) NULL, 1, (int *) NULL) != 1) {
                perror("spawning load monitor");
                break;
            }
            sleep(1);

            /* Check System Load (Microseconds Per Megaflop) */
            for (i = 0, load = 0.0, num = 0; i < 11; ++i)
                if ((pvm_recvinfo(MSGBOX, i, PvmBoxDefault) >= 0)) {
                    pvm_uplink(&elapsed, 1, 1);
                    load += elapsed; num++;
                }
            if (num)
                printf("Load Avg = %lf usec/Mflop\n",
                       (double) load / (double) num);

            sleep(5);

        } while (1);
    }

    /* If I am a Load Monitor Task */
    else if ( cc > 0 ) {
       /* Time Simple Computation */
       gettimeofday( &start, (struct timezone *) NULL );
       for ( i=0, value=1.0 ; i < 1000000 ; i++)
          value *= 1.2345678;

       gettimeofday( &end, (struct timezone *) NULL );
       elapsed = (end.tv_usec - start.tv_usec)
             + 1000000 * (end.tv_sec - start.tv_sec);

       /* Dump Into Next Available Message Mbox */
       pvm_initsnd( PvmDataDefault );
       pvm_pkint( &elapsed, 1, 1 );
       index = pvm_putinfo( MSGBOX, pvm_getsbuf(),
                PvmBoxDefault | PvmBoxPersistent
                | PvmBoxMultiInstance | PvmBoxOverWritable );

       /* Free Next Mbox Index for Next Instance (Only Save 10) */
       pvm_delinfo( MSGBOX, (index + 1) % 11, PvmBoxDefault );
    }

    pvm_exit();

    return( 0 );
}
```

## III 集群管理

# 13 集群工作负载管理

James Patton Jones, David Lifka, Bill Nitzberg 和 Todd Tannenbaum

Beowulf 集群是一个强大（且吸引人）的工具。但管理工作负载可能会带来重大挑战。运行数百甚至数千个作业或在众多用户间共享集群并不罕见。某些作业可能只能在特定节点上运行，因为集群中的节点并不完全相同；例如，某些节点的内存比其他节点多。某些节点可能暂时未正常运行。某些用户可能需要对集群的一部分或全部具有优先访问权。某些作业可能必须在一天中的特定时间运行，或者只能在其他作业完成后运行。即使是最简单的环境，在管理不断增长的优先级网络同时跟踪所有这些活动和资源细节也是一个复杂的问题。工作负载管理软件通过提供一种方法来监控和管理通过系统的工作流，从而解决这一问题，允许根据提供的策略实现集群资源的*最佳利用*。

基本上，工作负载管理软件在满足竞争的用户需求和本地策略限制的前提下，最大化地将资源交付给作业。用户将工作打包成一组作业，而管理员（或系统所有者）描述本地使用策略（例如，Tom 的作业总是优先处理）。软件监控集群状态，调度工作，执行策略，并跟踪使用情况。

关于术语的快速说明：有许多术语用于描述这个管理软件的领域。以下所有主题都与工作负载管理相关：分布式资源管理、批处理队列、作业调度，以及资源和任务调度。

## 13.1 工作负载管理软件的目标

工作负载管理软件的目标是确保提交的作业最终能够根据提供的策略利用集群资源并运行至完成。但为了实现这一目标，工作负载管理系统通常必须执行以下部分或全部活动：

- 队列管理
- 调度
- 监控
- 资源管理
- 记账

用户、资源以及这些工作负载管理活动之间的典型关系如图 13.1 所示。如图所示，工作负载管理软件位于集群用户和集群资源之间。首先，

