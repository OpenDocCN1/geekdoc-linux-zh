
传递给 `smi_open` 的消息队列名称必须为服务器和所有客户端所知。如果实现需要在打开之前创建它，这会在 `smi_open` 内部悄悄完成。这个简单接口中没有任何权限设置，这是它被称为“简单”的众多原因之一。消息队列在关闭后是否保留并未作为接口的一部分进行规定，这也取决于实现。

`entity` 参数是 `SMI_SERVER` 或 `SMI_CLIENT`，具体取决于正在执行打开操作的程序类型。只能有一个服务器进程，但客户端的数量是未定义的。

`msgsize` 参数是 `smi_msg` 结构中 `smi_data` 成员的大小，适用于所有消息。如前所述，没有规定消息可以是不同大小的。

对于发送和接收，我们可以将缓冲区地址传递给简单的发送和接收函数，类似 `write` 和 `read`，如下所示（因为没有大小参数，因为它是固定数量）：

```c
ec_false( smi_send(sqp, buffer) )
...
ec_false( smi_receive(sqp, buffer) )
```

但如果这样做，将要求所有实现将每条消息从发送进程复制到内核，然后再从内核复制到接收进程。相反，我们将使用一个稍微复杂的接口，发送使用两次调用，接收也使用两次调用。每对调用的第一次调用仅获取消息的地址，第二次调用则释放对该地址的访问。这样，实现可以将其保留在 `SMIQ` 结构中（这意味着它确实被复制了），或者保留在共享内存中，或者以任何其他方式。调用者只知道它们有一个可以解引用的地址。需要释放函数是因为该地址可能不会永远有效——内存可能必须被释放，或者共享内存段可能需要被重用——而且底层实现需要知道发送者准备好让消息发送出去了。

解释接收比解释发送更容易：

#### `smi_receive_getaddr`—获取接收的 SMI 消息地址

```c
bool smi_receive_getaddr(
    SMIQ *smp,             /* queue */
    void **addr            /* message */
);
/* Returns true on success or false on error (sets errno) */
```

#### `smi_receive_release`—释放接收的 SMI 消息

```c
bool smi_receive_release(
    SMIQ *smp             /* queue */
);
/* Returns true on success or false on error (sets errno) */
```

`addr` 参数是指向 `void` 指针的指针，而不是指向 `struct smi_msg` 指针，因为在实际中，每个应用程序都会定义自己的消息结构，其前两个成员与 `smi_msg` 的前两个成员（`smi_mtype` 和 `smi_client`）匹配。

应用程序使用这两个调用如下：

```c
struct my_msg *msg;
...
ec_false( smi_receive_getaddr(smp, (void **)&msg) )
/* process data in msg->smi_data */
ec_false( smi_receive_release(smp) )
```

从概念上讲，当调用 `smi_receive_getaddr` 时，消息实际上已被接收。请注意，应用程序不为消息分配空间；那是由实现完成的。

发送非常相似，但有一个额外的难点——识别客户端：

#### `smi_send_getaddr`—获取发送的 SMI 消息地址

```c
bool smi_send_getaddr(
    SMIQ *scp,
    struct client_id *client,    /* client identifier */
    void **addr                 /* message */
);
/* Returns true on success or false on error (sets errno) */
```

#### `smi_send_release`—释放并发送 SMI 消息

```c
bool smi_send_release (
    SMIQ *scp                  /* queue */
);
/* Returns true on success or false on error (sets errno) */
```

从概念上讲，实际的发送发生在调用 `smi_send_release` 时。

`smi_send_getaddr` 的第二个参数由服务器用于识别它正在向其发送消息的客户端。它是一个指向接收消息中的 `struct client_id` 的指针。这是可行的，因为服务器在向其发送消息之前，先会收到想要与其进行通信的客户端的消息。发送的客户端不需要识别服务器（这已经在 `smi_open` 中完成了），因此第二个参数为 `NULL`。

然后，服务器会执行类似以下操作：

```c
struct my_msg *msg_in, *msg_out;
...
ec_false( smi_receive_getaddr(scp, (void **) &msg_in ) )
/* code to process data in msg_in->smi_data */
ec_false( smi_send_getaddr(scp, &msg_in->smi_client, (void **) &msg_out ) )
ec_false( smi_receive_release(scp) )
/* code to put data into msg_out->smi_data */
ec_false( smi_send_release(scp) )
```

请注意：

- 服务器使用了两个独立的 `my_msg` 地址（`msg_in` 和 `msg_out`），因为涉及到两个不同的缓冲区。
- `msg_in` 直到调用 `smi_send_getaddr` 之后才释放，因为在此之前需要 `msg_in->smi_client` 结构。以这种方式交错调用调用是可以的；事实上，`smi_receive_release` 甚至可以在调用 `smi_send_release` 之后调用——发送和接收是完全独立的。或者，`client_id` 结构可以已被复制到一个临时变量中，其地址可在调用 `smi_send_getaddr` 时使用。

客户端像这样调用 `smi_send_getaddr` 和 `smi_send_release`（很可能有一个 `msg_in`，但我们没有展示它）：

```c
struct smi_msg *msg_out;
...
ec_false( smi_send_getaddr(sqp, NULL, (void **)&msg_out) )
/* 向 msg_out->smi_data 中填充数据的代码 */
ec_false( smi_send_release(sqp) )
```

下一节包含一个更完整的示例。

### 7.3.2 使用 SMI 的服务器和客户端示例

为了展示如何在应用程序中使用 SMI 函数，下面是第 7.2.2 节示例中的服务器，它被重写以使用 SMI 接口（`#defines` 位于一个由服务器和客户端共同包含的头文件中）：

```c
#define SERVER_NAME "smg_server"
#define DATA_SIZE 200

int main(void)
{
    SMIQ *sqp;
    struct smi_msg *msg_in, *msg_out;
    int i;

    printf("server started\n");
    ec_null( sqp = smi_open(SERVER_NAME, SMI_SERVER, DATA_SIZE) )
    while (true) {
        ec_false( smi_receive_getaddr(sqp, (void **)&msg_in) )
        ec_false( smi_send_getaddr(sqp, msg_in->smi_client,
                                   (void **)&msg_out) )
        for (i = 0; msg_in->smi_data[i] != '\0'; i++)
            msg_out->smi_data[i] = toupper(msg_in->smi_data[i]);
        msg_out->smi_data[i] = '\0';
        ec_false( smi_receive_release(sqp) )
        ec_false( smi_send_release(sqp) )
    }
    /* 实际上永远无法到达此处 */
    ec_false( smi_close(sqp) )
    exit(EXIT_SUCCESS);

    EC_CLEANUP_BGN
        exit(EXIT_FAILURE);
    EC_CLEANUP_END
}
```

以下是客户端代码：

```c
int main(int argc, char *argv[]) {

    SMIQ *sqp;
    struct smi_msg *msg;
    int i;

    char *work[] = {
        "appleSauce",
        "tiger",
        "mountain",
        NULL
    };

    printf("client %ld started\n", (long)getpid());
    ec_null( sqp = smi_open(SERVER_NAME, SMI_CLIENT, DATA_SIZE) )
    for ( i = 0; work[i] != NULL; i++ ) {
        ec_false( smi_send_getaddr(sqp, NULL, (void **) &msg) )
            strcpy(msg->smi_data, work[i]);
        ec_false( smi_send_release(sqp) )
        ec_false( smi_receive_getaddr(sqp, (void **) &msg) )
            printf("client %ld: %s --> %s\n", (long)getpid(),
                work[i], msg->smi_data);
        ec_false( smi_receive_release(sqp) )
    }
    ec_false( smi_close(sqp) )
    printf("Client %ld done\n", (long)getpid());
    exit(EXIT_SUCCESS);

    EC_CLEANUP_BGN
        exit(EXIT_FAILURE);
    EC_CLEANUP_END
}
```

请注意，我们在第 7.2.2 节中看到的保持文件描述符打开以便写入的那些“棘手操作”已不复存在，`FIFO` 名称等细节也是如此。也许说它们被“隐藏”比说它们“消失”更准确，正如我们要即将发现的那样。

### 7.3.3 SMI 的 FIFO 实现

之前从服务器和客户端中移除的所有与 `FIFO` 消息传递相关的复杂性，现在都必须放入 SMI 函数的实现中。此外，服务器实现将尝试跨消息保持客户端-`FIFO` 文件描述符的打开状态，以避免每次打开和关闭带来的开销，就像第 7.2.2 节中的示例所做的那样。

`FIFO` 实现使用形如 `smifcn_fifo` 的函数名，其中 `smifcn` 是 SMI 名称（例如，`smi_send_getaddr_fifo` 是 `smi_send_getaddr` 的实现）。一个小型包装文件实际上翻译了这些名称，通过像下面这样的小函数：

```c
bool smi_send_getaddr(SMIQ *sqp, struct client_id *client, void **addr)
{
    return smi_send_getaddr_fifo(sqp, client, addr);
}
```

使用包装器允许链接两种类型的应用程序：

- 一个实现无关的应用程序，如上一节所示，可以用通用的 SMI 函数（例如，`smi_send_getaddr`）来编写，然后与特定的实现以及适当的包装器链接，以将调用从通用翻译为特定。
- 希望使用几种实现的应用程序可以使用特定的函数名（例如，`smi_send_getaddr_fifo`, `smi_send_getaddr_skt`），绕过未链接的包装器。这样做的一个主要目的是编写测试程序，例如，使用不同方法运行相同的应用程序以比较它们的性能。我正是这样做的，以准备第 7.2 表，该表是本章的结尾。

我将在书中不展示这些包装器，但它们在网站上 [AUP2003] 有。

我们将以内部的消息队列开始 `FIFO` 实现。服务器和客户端使用相同的数据结构，尽管由于它们在不同的进程中，因此各自拥有自己的数据。

```c
#define MAX_CLIENTS 20
typedef struct {
    SMINTITY sq_entity;           /* 实体 */
    int sq_fd_server;             /* 服务器读取及... */
    int sq_fd_server_w;           /* ... 写入文件描述符 */
    char sq_name[SERVER_NAME_MAX];/* 服务器名称 */
    struct {
        int cl_fd;                /* 客户端文件描述符 */
        pid_t cl_pid;             /* 客户端进程 ID */
    } sq_clients[MAX_CLIENTS];
    struct client_id sq_client;   /* 客户端 ID */
    size_t sq_msgsize;            /* 消息大小 */
    struct smi_msg *sq_msg;       /* 消息缓冲区 */
} SMIQ_FIFO;
```

每个服务器只有 20 个客户端的空间。可以使用链表来解除这个限制，但我没有费心去做。服务器端使用 `sq_fd_server` 来操作服务器，并且服务器端还额外使用 `sq_fd_server_w` 保持一个用于写入的文件描述符处于打开状态，如第 7.2.2 节所述。服务器使用 `sq_clients` 数组保存客户端文件描述符，以避免在处理每个传入消息时反复打开和关闭它们。客户端只需其中一个用于读取自己的 `FIFO`，它使用 `sq_clients[0]`。它使用 `sq_clients[1]` 保持第二个文件描述符处于打开状态以用于写入。对于客户端来说，数组的其余部分和 `sq_fd_server_w` 是浪费的空间，但我认为对两者使用相同的队列结构会更简单，因为浪费的空间很小。

由服务器传递给 `smi_send_getaddr_fifo` 的客户端 ID 信息保留在 `sq_client` 成员中，以供后续的 `smi_send_release_fifo` 使用。传递给 `smi_open_fifo` 的大小和指向消息缓冲区的指针位于 `sq_msgsize` 和 `sq_msg` 成员中。（请注意，与消息队列和套接字一样，对于 `FIFO` 而言，从用户空间到内核再回到接收进程的数据复制是不可避免的。）

服务器和客户端都需要初始化 `sq_clients` 数组，使用这个内部函数：

```c
static void clients_bgn(SMIQ_FIFO *p)
{
    int i;

    for (i = 0; i < MAX_CLIENTS; i++)
        p->sq_clients[i].cl_fd = -1;
}
```

最后，它们调用 `clients_end`：

```c
static void clients_end(SMIQ_FIFO *p)
{
    clients_close_all(p);
}

static void clients_close_all(SMIQ_FIFO *p)
{
    int i;

    for (i = 0; i < MAX_CLIENTS; i++)
        if (p->sq_clients[i].cl_fd != -1) {
            (void)close(p->sq_clients[i].cl_fd);
            p->sq_clients[i].cl_fd = -1;
        }
}
```

我们将在 `smi_open_fifo` 和 `smi_close_fifo` 函数中看到这些调用。

当服务器收到消息时，它使用 `clients_find` 来检查是否已经有一个打开到该 `FIFO` 的文件描述符，如果没有，则找到一个可用的槽位：
