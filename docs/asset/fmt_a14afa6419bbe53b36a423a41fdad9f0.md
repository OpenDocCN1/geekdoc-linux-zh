
```c
if (msgsnd(id_file, (struct msgbuf *)&data2, sizeof(data_t), 0) == -1) {

    my_error("msgsnd 2", "msgsnd");

}

}
```

`printf("Server : 数据到消息队列传输完成\n");`

`printf("Server : 等待客户端完成读取\n");`

```c
struct msgbuf rec;

while ((end1) || (end2)) {

    if (msgrcv(id_file, &rec, sizeof(struct msgbuf), TYPE_END1, IPC_NOWAIT) != -1) {

        end1 = 0;

    }

    if (msgrcv(id_file, &rec, sizeof(struct msgbuf), TYPE_END2, IPC_NOWAIT) != -1) {

        end2 = 0;

    }

}
```

`printf("Server : 两个子进程已断开\n");`

`close_all(id_file, fd1, fd2);`

}

### CopyClient.c

```c
#include <stdio.h>

#include <stdlib.h>

#include <fcntl.h>

#include <errno.h>

#include <unistd.h>

#include <sys/stat.h>

#include <sys/types.h>

#include <sys/ipc.h>

#include <sys/msg.h>

#include "Copy.h"

static void usage(char *prog)

{

    printf("使用消息队列的应用示例\n");

    printf("用法: %s <file1> <file2>\n", prog);

    exit (1);

}

static void my_error(char *msg, char *call)

{

    fprintf(stderr, "Error %s: %d\n", msg, errno);

    perror(call);

    exit (1);

}

static void disconnection(int id_file, int no_client)

{

    struct msgbuf disconnection_msg;

    if (no_client == 1)

        disconnection_msg.mtype = TYPE_END1;

    else

        disconnection_msg.mtype = TYPE_END2;

    msgsnd(id_file, &disconnection_msg, sizeof(struct msgbuf), 0);

}

static void close_all(int id_file, int fd1, int fd2)

{

    msgctl(id_file, IPC_RMID, NULL);

    close(fd1);

    close(fd2);

}

void main (int argc, char **argv)

{

    int fd;

    int id_file;

    key_t key;

    data_t data;

    int no_client;

    if (argc != 3)

        usage(argv[0]);

    /* 获取客户端编号 */

    no_client = atoi(argv[1]);

    if (no_client != 1 && no_client != 2)

        usage(argv[0]);

    /* 连接到消息队列 */

    printf("Client%d 连接到消息队列\n", no_client);

    /* 键值生成 */

    if ((key = ftok(FILE_KEY, PROJ_OK)) == -1) {

        my_error("ftok", "ftok");

    }

    /* 连接消息队列 */

    if ((id_file = msgget(key, 0666)) == -1) {

        my_error("msgget", "msgget");

    }

    /* 打开文件 */

    if ((fd = open(argv[2], O_WRONLY | O_CREAT | 0666)) == -1) {

        my_error("open", "open");

    }

    printf("Client%d 打开了文件 %s\n", no_client, argv[2]);

    /* 读取循环 */

    while (1) {

        if (msgrcv(id_file, (struct msgbuf *)&data, sizeof(data_t), no_client, 0) == -1) {

            my_error("msgrcv", "msgrcv");

        }

        if (data.data_sz == 0) /* 结束 */

            break;

        int ret = write(fd, data.buf, data.data_sz * sizeof(char));

        if (ret == -1) {

            close_all(id_file, fd, -1);

            my_error("write", "write");

        }

    }

    close(fd);

    printf("Client%d : 断开\n", no_client);

    disconnection(id_file, no_client);

}
```
