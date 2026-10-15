
```c
case 'd': remove_queue(msgqueue_id); break; 

case 'm': change_queue_mode(msgqueue_id, argv[2]); break;

default: usage();

}

return(0);

}
```

```c
void send_message(int qid, struct mymsgbuf *qbuf, long type, char *text) {

    /* 向队列发送消息 */

    printf("Sending a message ...\n");

    qbuf->mtype = type;

    strcpy(qbuf->mtext, text);

    if((msgsnd(qid, qbuf, strlen(qbuf->mtext)+1, 0) == -1) {

        perror("msgsnd");

        exit(1);

    }

}
```

```c
void read_message(int qid, struct mymsgbuf *qbuf, long type) {

    /* 从队列读取消息 */

    printf("Reading a message ...\n");

    qbuf->mtype = type;

    msgrcv(qid, qbuf, MAX_SEND_SIZE, type, 0);

    printf("Type: %ld %s\n", qbuf->mtype, qbuf->mtext);

}
```

```c
void remove_queue(int qid) {

    /* 删除队列 */

    msgctl(qid, IPC_RMID, 0);

}
```

```c
void change_queue_mode(int qid, char *mode) {

    struct mqid_ds myqueue_ds;

    /* 获取当前信息 */

    msgctl(qid, IPC_STAT, &myqueue_ds);

    /* 转换并加载模式 */

    sscanf(mode, "%hu", &myqueue_ds.msg_perm_mode);

    /* 更新模式 */

    msgctl(qid, IPC_SET, &myqueue_ds);

}
```

```c
void usage(void) {

    fprintf(stderr, "msgtool - A utility for tinkering with msg queues\n");

    fprintf(stderr, "\nUSAGE: msgtool (s)end <type> <messagetext>\n");

    fprintf(stderr, "         (r)ecv <type> <textize>\n");

    fprintf(stderr, "         (d)elete\n");

    fprintf(stderr, "         (m)ode <octal mode>\n");

}
```

### 6.4.3 信号量

### 基础概念

信号量可以描述为计数器，用于控制多个进程对共享资源的访问。它们最常被用作一种锁定机制，防止在一个进程正在对特定资源进行操作时，另一个进程访问该资源。在三种 System V IPC 对象中，信号量通常被认为是最难理解的。为了完全理解信号量，我们将在任何系统调用和操作理论之前对它们进行讨论。

`Semaphore` 这个名字实际上是一个古老的铁路术语，指的是防止车辆在交叉路口穿越轨道的“信号臂”。简单的信号量集 `semaphore set` 也是如此。如果信号量处于开启（信号臂升起），则资源是可用的（车辆可以通过轨道）。然而，如果信号量处于关闭状态（信号臂落下），则资源不可用（车辆必须等待）。

虽然这个简单的例子可以用来引入概念，但重要的是，信号量实际上是实现为集合的，而不是单个实体。当然，一个给定的信号量集可能只包含一个信号量，正如我们的铁路示例那样。

理解信号量概念的另一种方法是将其视为资源计数器。让我们把这个概念应用于另一个现实场景。考虑一个打印池处理程序，它可以处理多台打印机，而每台打印机又处理多个打印请求。
