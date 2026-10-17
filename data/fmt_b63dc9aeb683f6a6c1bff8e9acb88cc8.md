
在该版本块内部，每个程序（或函数）都有一个唯一的编号。程序号从 0 开始 - 但程序 0 被保留为 NULL 或“ping”程序。它由 `rpc` 编译器自动生成，不需要任何参数，且不返回任何内容。然而，它对于确保远程服务器正在运行是有用的。

`DVD_OPEN_DB` 的程序号为 1，它不接受任何参数并返回一个 `int`（状态）。`DVD_CLOSE_DB` 也是如此，程序号为 3，它也不接受任何参数并返回状态。

# 远程过程调用

不用担心程序号不连续的事。我们在 `dvd_store.x` 中根据它们在 `dvd.h` 中出现的顺序实现了这些函数。完成后的 `dvd_store.x` 包含了所有函数。

运行 `rpcgen` [参见图表] 会生成以下文件：

- `dvd_store_clint.c` - 客户端存根
- `dvd_store_svc.c` - 服务器端存根
- `dvd_store_xdr.c` - XDR 例程
- `dvd_store.h` - 该协议的通用 RPC 头文件

存根文件中的例程会替你处理整个网络编程。将数据序列化为一种网络可传输的格式，并反序列化为对端的原生类型。我们现在需要将对 `dvd.h` API 的实现以及 API 的用户连接到这些存根程序。这是通过使用客户端和服务器存根实现的。这是通过 `dvd.h` 描述的封装器完成的。以下是服务器端的代码示例：

```
/*
dvd_server.c
#include <stdio.h>
#include <stdlib.h>
#include <rpc/rpc.h>
#include "dvd.h"
#include "dvd_store.h"

int dvd_open_db_1(void *dummy_ptr, struct svc_req *svc_req) {
	int result;
	int status = DVD_OPEN_DB;

	/*
	 * 此处实现打开数据库的逻辑
	 */

	result = 0; // 成功
	svc_req->r_reply = &result;
	return status;
}

int dvd_close_db_1(void *dummy_ptr, struct svc_req *svc_req) {
	int result;
	int status = DVD_CLOSE_DB;

	/*
	 * 此处实现关闭数据库的逻辑
	 */

	result = 0; // 成功
	svc_req->r_reply = &result;
	return status;
}
```

以下是对应的客户端代码：

```
/*
dvd_client.c
#include <stdio.h>
#include <stdlib.h>
#include <rpc/rpc.h>
#include "dvd.h"
#include "dvd_store.h"

static char *server_host_name = "localhost";
static CLIENT client = 0;

static void dvd_rpc_client_init(void);
static void dvd_rpc_client_shutdown(void);

int dvd_open_db(void) {
	int *result;
	int status = DVD_ERR_BAD_DATABASE;

	if (0 == client) {
		/* 如果客户端句柄不存在，尝试创建一个 */
		dvd_rpc_client_init();

		result = dvd_open_db_1(NULL, client);
	}

	if (NULL != result) {
    status = *result;
    } else {
    client_pcreateerror(server_host_name);
    }

	return (status);
}

int dvd_close_db(void) {
    int *result;
    int status = DVD_ERR_BAD_DATABASE;

    if (0 != client) {
		result = dvd_close_db_1(NULL, client);
		dvd_rpc_client_shutdown();
    } else {
    /*
     * 看起来某些东西在我们关闭 RPC 连接之前抢先了
     * dvd_close_db 是否在调用 dvd_open_db 或 dvd_open_db_login 之前被调用了
     */
#ifdef RPC_DEBUG
    fprintf(stderr,
        "RPC_CLIENT - dvd_close_db: 句柄为空位于 %s:%d\n",
        __FILE__, __LINE__);
#endif

    status = DVD_ERR_BAD_DATABASE;
    }

    if (NULL != result) {
        status = *result;
    } else {
        client_pcreateerror(server_host_name);
    }
    return (status);
}
```

# 第 18 章

```c
* 无法与服务器建立连接
* 因此打印错误信息并停止

clnt_pcreateerror(server_host_name);
exit(1);
}

* 在调用 dvd_close_db 时拆毁 RPC 连接

static void dvd_rpc_client_shutdown(void) {
  if (0 != client) {
    clnt_destroy(client);
    client = 0;
  }
}
```

你可能已经猜到了，客户端的实现比服务器端要复杂得多！

- `dvd_rpc_client_init` 负责创建到 RPC 服务器的连接。通常它在数据库会话启动时执行，即在调用 `dvd_open_db` 时。它通过调用以下函数创建到服务器的连接：

`CLIENT clnt_create(const char *host, const u_long programm, const u_long versnum, const char *netype);`

并传递服务器主机名、程序号（来自 `dvd_store.x` 中的该程序）、协议版本以及要使用的网络协议 - 在这里是 TCP/IP 协议族中的传输控制协议。

`clnt_create` 返回一个指向名为 `CLIENT` 的 RPC 结构体的指针 - 这是客户端指向 RPC 服务器的句柄。客户端在与服务器通信时使用此句柄。

如果返回值为 NULL 指针，则说明 `clnt_create` 调用由于某种原因失败。在这种情况下，我们使用：

```c
void clnt_pcreateerror(const char *s);
```

将相应的错误信息打印到标准错误输出，并终止客户端的执行。

你可能会注意到服务器主机名被硬编码为 `localhost`。如果你计划在同一机器上运行服务器和客户端，可以保持不变 - 或者你也可以将其更改为不同的服务器名称。理想情况下，这类资源应该从配置文件中输入，或者使用其他机制（如广播）。

调用 `dvd_rpc_client_shutdown` 是为了释放指向 RPC 服务器的句柄 - 这在调用 `dvd_close_db` 结束数据库会话时间接触发。它通过以下函数释放连接：

```c
void client_destroy(CLIENT *clint);
```

将客户端句柄作为唯一参数传递给 RPC 服务器。

现在应该很清楚为什么 `dvd_open_db` 和 `dvd_close_db` 同时被添加到 RPC 接口中，尽管它们都是简单的函数。`dvd_open_db` 创建到 RPC 服务器的连接，而 `dvd_close_db` 释放它。

现在我们需要将这些文件与 `rpcgen` 生成的文件以及我们的应用程序实现链接，以便我们能够通过 RPC 测试至少两个函数（`dvd_open_db` 和 `dvd_close_db`）。在此之前，我们需要在客户端准备一个简短的测试文件 - 我们可以使用服务器上的 `flatfile.c`：

- `dvd_test_client.c`

```c
#include <stdio.h>
#include "dvd.h" /* 注意此测试文件对 RPC 一无所知
 * - 仅包含标准的 DVD API */

int main(int argc, char *argv[]) {
    int status;
************************************************************************************
```

- 测试 1 - 在没有设置 RPC 连接的情况下测试 `dvd_close_db`

- 这向客户端控制台打印错误，因为
