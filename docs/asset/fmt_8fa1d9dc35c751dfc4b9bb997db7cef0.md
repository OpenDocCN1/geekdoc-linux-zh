
- 没有先执行 `dvd_open_db`/`dvd_open_db_login` 来建立
- 到服务器的 RPC 连接

************************************************************************************

{
    printf("TEST 1 - Testing dvd_close_db without");
    // RPC connection setup\n");
    status = dvd_close_db;
    if (DVD_SUCCESS != status) {
        printf(" - passed\n");
    } else {
        printf(" - FAILED!\n");
    }
}

************************************************************************************

- 测试 2 - 在没有预先 RPC 连接的情况下测试 `dvd_today`

************************************************************************************

{
    char *date;
```c
printf(\
TEST 2 - Testing dvd_today without pre-existing"
  * RPC connection\n");
status = dvd_today(&date);

if (DVD_SUCCESS == status) {
  printf("* - Today date is %s [YYYYMMDD]\n", date);
  printf("* - passed\n");
} else {
  printf("* - FAILED!\n");
}
```

********************************
* 测试 3 - 测试 `dvd_open_db`
{
  printf(\
TEST 3 - Testing dvd_open_db\n");
  status = dvd_open_db;

  if (DVD_SUCCESS == status) {
    printf("* - passed\n");
  } else {
    printf("* - FAILED!\n");
  }
}
```

在此阶段，我们已经可以将这些简单的例程编译成准备测试的二进制文件。首先，我们生成存根文件（stub files）：

- `rpcgen dvd_store.x`

现在我们链接服务器所需的文件 - 我们创建的封装文件、`rpcgen` 编译器生成的服务器存根、XDR 存根以及实际的后端实现 - 为了简单起见，我们将使用平文件版本：

```bash
gcc -DRPC_DEBUG -o dvd_rpc_server dvd_store_wrapper.c dvd_store_svc.c
dvd_store.xdr.c flatcfile.c
```

同样，客户端由客户端封装文件、客户端存根、XDR 存根和客户端应用程序构建：

```bash
gcc -DRPC_DEBUG -o dvd_rpc_client dvd_client_wrapper.c dvd_store.c
dvd_store.xdr.c test_client.c
```

到目前为止一切顺利！这种构建过程可以用于构建所有示例，功能通过这种方式添加。为了让你对最终产品有个直观感受，客户端的输出应该是这样的：

```
RPC_CLIENT - dvd_close.db: handle is null at dvd_client_wrapper.c:10
RPC_CLIENT - dvd_today: handle is null at dvd_client_wrapper.c:76
RPC_CLIENT - dvd_today: making RPC connection localhost: Success```

- 测试 1 - 在没有设置 RPC 连接的情况下测试 `dvd_close_db`
- 通过
- 测试 2 - 在没有预先 RPC 连接的情况下测试 `dvd_today`
- 今天日期为 200007-17 [YYYYMMDD]
- 通过
- 测试 3 - 测试 `dvd_open_db`
- 通过
- 测试 4 - 测试 `dvd_today`
- 今天日期为 200007-17 [YYYYMMDD]
- 通过
- 测试 5 - 测试 `dvd_err_text`
- 未知错误: 1 - 通过
- 无错误 - 通过
- 无法打开文件 - 通过
- 等（更多错误代码...)
- 测试 6 - 测试 `dvd_get_genre_list`
- 类型数量 - 7
- 通过
- 等（更多类型...)
- 测试 7 - 测试 `dvd_get_classification_list`
- 类别数量 - 6
- 通过
- 3:12
- 4:15
- 5:18
- 通过
- 测试 8 - 测试 `dvd_member_create`
- 分配的 id 为 5
- 通过
- 测试 X - 测试 `dvd_member_search`
- 数量为 1
- 结果为 5
- 通过
- 等....其他 API 测试...)
- 测试 X - 测试 `dvd_close`
- 通过

服务器测试输出（为了简练）应该是：

```
RPC_SERVER: dvd_today_1_svc called
RPC_SERVER: dvd_open_db_1_svc called
RPC_SERVER: dvd_today_1_svc called
RPC_SERVER: dvd_err_text_1_svc called
RPC_SERVER: dvd_err_text_1_svc called

RPC_SERVER: dvd_get_genre_list_1_svc called
RPC_SERVER: dvd_classification_list_1_svc called
RPC_SERVER: dvd_member_create_1_svc called
RPC_SERVER: dvd_member_search_1_svc called
RPC_SERVER: dvd_member_get_from_number_1_svc called
RPC_SERVER: dvd_title_create_1_svc called
RPC_SERVER: dvd_disk_delete_1_svc called
RPC_SERVER: dvd_title_delete_1_svc called
RPC_SERVER: dvd_member_delete_1_svc called
RPC_SERVER: dvd_close_db_1_svc called
```

下面的图显示了当应用程序调用这些 DVD 函数时的控制流：

![](img/930f7611cac03acd5573f4bb9fd7b9_707_0.png)

# 远程过程调用

客户端封装为应用程序提供了标准的 DVD API，但实际上它为 RPC 存根构建了消息。该消息从客户端进程序列化并传输到服务器进程。在这里，它被服务器存根接收并反序列化（de-marshaled）。然后，过程被分发到服务器封装文件，由它重构标准的 DVD 调用。它获取数据库的响应，并再次跨 RPC 接口返回给客户端进程。

服务器应用程序位于同一机器上还是完全不同的机器上，对客户端代码没有区别。事实上，即使远程机器是不同的 CPU、运行不同的操作系统、具有不同的字节序和字长，只要双方支持 ONC-RPC 协议即可。

# 带有简单参数和简单返回类型的函数

好的，让我们考虑函数带有参数的情况：

```c
int dvd_member_delete(const int member_id);
```

这里比之前的例子并没有复杂。以下是向 `dvd_store.x` 文件添加过程定义所需的额外代码：

```c
int DVD_MEMBER_DELETE(int) = 7;
```

这是该过程的服务器封装代码：

```c
/* dvd_member_delete 的服务器封装函数 */
int dvd_member_delete_1_svc(int *member_ptr, struct svc_req *svc_req_ptr)
    static int result;

#ifdef RPC_SERVER
    puts('RPC_SERVER: dvd_member_delete_1_svc called\n', stderr);
#endif

    result = dvd_member_delete(*member_ptr);
    return (&result);
}
```
