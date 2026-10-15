
```c
typedef struct {
    pid_t client_pid;
    client_request_e request;
    server_response_e response;
    cdc_entry entry_data;
    cdt_entry cdt_data;
    char error_text[TEXT_LEN];
} message_db_t;
```

最后，我们获取执行传输的接口函数，实现在 `pipe_imp.c` 中。这些分别分为第一个和第二个块中的服务器端和客户端函数：

```c
int server_starting(void);
void server_ending(void);
int read_request_from_client(message_db_t *rec_ptr);
int send_resp_to_client(const message_db_t mess_to_send);
int send_resp_to_client(const message_db_t mess_to_send);
void end_resp_to_client(void);

int client_starting(void);
void client_ending(void);
int send_mess_to_server(message_db_t mess_to_send);
int start_resp_from_server(void);
int read_resp_from_server(message_db_t *rec_ptr);
void end_resp_from_server(void);
```

我们将剩下的讨论分为客户端接口函数以及 `pipe_imp.c` 中的服务器端和客户端函数细节，并在需要查看源代码。

### 客户端接口函数

我们现在来看 `client_if.c`。它提供了数据访问例程的“伪”实现。这些例程将请求封装在 `message_db` 结构中，并使用 `pipe_imp.c` 中的例程将请求传输到服务器。这允许我们对原始的 `app_ui.c` 进行最小修改。

> 尝试——客户端解释器

该文件实现了 `cd_data.h` 中定义的函数。它通过向服务器发送请求并将服务器响应从函数返回来实现，充当中间件。

```c
#define POSIX_SOURCE

#include "cd_data.h"
#include <cliserv.h>
```

静态变量 `mypid` 减少了原本需要调用 `getpid` 的次数。我们使用本地函数 `read_one_response` 来消除重复代码：

```c
static pid_t mypid;
static int read_one_response(message_db_t *rec_ptr);
```

### `database_initialize` 和 `close` 例程

`database_initialize` 和 `close` 例程仍然被调用，但现在分别用于初始化管道接口的客户端，以及在客户端退出时移除冗余的命名管道。

```c
int database_initialize(const int new_database)
{
    if (!client_starting()) return(0);
    mypid = getpid();
    return(1);
}
/* database_initialize */
void database_close(void) {
    client_ending();
}
```

调用 `get_cdc_entry` 例程以根据指定的 CD 目录标题从数据库获取目录条目。在这里，我们将请求编码在 `message_db_t` 结构中并将其传递给服务器。然后，我们将响应读回另一个不同的 `message_db_t` 结构中。如果找到了条目，它将作为 `cdc_entry_structure` 包含在 `message_db_t` 结构中，因此我们返回该结构的适当响应：

```c
cdc_entry get_cdc_entry(const char *cd_catalog_ptr)
{
    cdc_entry ret_val;
    message_db_t mess_send;
    message_db_t mess_ret;

    ret_val.catalog[0] = '\0';
    mess_send.client_pid = mypid;
    mess_send.request = s_get_cdc_entry;
    strcpy(mess_send.cdc_entry_data.catalog, cd_catalog_ptr);

    if (send_mess_to_server(mess_send)) {
        if (read_response(mess_ret) == r_success) {
            ret_val = mess_ret.cdc_entry_data;
        } else {
            fprintf(stderr, "%s", mess_ret.error_text);
        }
    } else {
        fprintf(stderr, "Server failed to respond\n");
    }
    return(ret_val);
}
```

这里是我们使用的 `read_one_response` 函数源代码，用于避免重复代码：

```c
static int read_one_response(message_db_t *rec_ptr)
{
    int return_code = 0;
    if (!rec_ptr) return(0);

    if (start_resp_server()) {
        if (read_resp_from_server(rec_ptr)) {
            return_code = 1;
        }
        end_resp_server();
    }
    return(return_code);
}
```

其他的 `get_xxx`、`del_xxx` 和 `add_xxx` 例程实现与 `get_cdc_entry` 函数类似，为了完整性在此处复制。首先是获取 CD 轨道的函数：

```c
cdt_entry_get_cdt_entry(const char *cd_catalog_ptr, const int track_no) {
    cdt_entry ret_val;
    message_db_t mess_send;
    message_db_t mess_ret;

    ret_val.catalog[0] = '\0';
    mess_send.client_pid = mypid;
    mess_send.request = s_get_cdc_entry;
    strcpy(mess_send.cdc_entry_data.catalog, cd_catalog_ptr);
    mess_send.cdc_entry_data.track_no = track_no;

    if (send_mess_to_server(mess_send)) {
        if (read_one_response(&mess_ret)) {
            if (mess_ret.response == r_success) {
                ret_val = mess_ret.cdt_entry_data;
            } else {
                fprintf(stderr, "%s", mess_ret.error_text);
            }
        } else {
            fprintf(stderr, "Server failed to respond\n");
        }
    } else {
        fprintf(stderr, "Server not accepting requests\n");
    }
    return(ret_val);
}
```

接下来是两个添加数据的函数，首先添加到目录，然后添加到轨道数据库：
