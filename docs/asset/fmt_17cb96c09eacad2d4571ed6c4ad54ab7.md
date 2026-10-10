
```c
int del_cdc_entry(const char *cd_catalog_ptr) {
    message_db_t mess_send;
    message_db_t mess_ret;

    mess_send.client_pid = mypid;
    mess_send.request = s_del_cdc_entry;
    strncpy(mess_send.cdc_entry_data.catalog, cd_catalog_ptr);

    if (send_mess_to_server(mess_send)) {
        if (read_one_response(&mess_ret)) {
            if (mess_ret.response == r_success) {
                return(1);
            } else {
                fprintf(stderr, "%s", mess_ret.error_text);
            }
        } else {
            fprintf(stderr, "Server failed to respond\n");
        }
    } else {
        fprintf(stderr, "Server not accepting requests\n");
    }
    return(0);
}

int del_cdt_entry(const char *cd_catalog_ptr, int track_no) {
    message_db_t mess_send;
    message_db_t mess_ret;

    mess_send.client_pid = mypid;
    mess_send.request = s_del_cdt_entry;
    strncpy(mess_send.cdt_entry_data.catalog, cd_catalog_ptr);
    mess_send.cdt_entry_data.track_no = track_no;

    if (send_mess_to_server(mess_send)) {
        if (read_one_response(&mess_ret)) {
            if (mess_ret.response == r_success) {
                return(1);
            } else {
                fprintf(stderr, "%s", mess_ret.error_text);
            }
        } else {
            fprintf(stderr, "Server failed to respond\n");
        }
    } else {
        fprintf(stderr, "Server not accepting requests\n");
    }
    return(0);
}
```

## 搜索数据库

对 CD 的搜索函数更为复杂。该函数的用户期望调用它一次来启动搜索。我们在第 7 章中满足了这一预期：在第一次调用时将 `first_call_ptr` 设为 `true`，并让函数返回第一个匹配。后续对搜索函数的调用中，`first_call_ptr` 为 `false`，每次返回一个匹配项。

我们可以更改搜索的方式，或者像我们在这里选择的，在接口运行时处理复杂度。我们做的目的是安排服务器返回所有可能的匹配并将其存储在临时文件中，直到客户端请求它们。

### 尝试一下——搜索

1. 这个函数看起来比实际上复杂，因为它调用了下一节中看到的三个函数：`send_mess_to_server`、`start_resp_from_server` 和 `read_resp_from_server`。

```c
cdc_entry search_cdc_entry(const char *cd_catalog_ptr, int *first_call_ptr) {
    message_db_t mess_send;
    message_db_t mess_ret;
    static FILE *work_file = (FILE *)0;
    static int entries_matching = 0;
    cdc_entry ret_val;
    ret_val.catalog[0] = '\0';
    if (!work_file && (*first_call_ptr == 0)) return(ret_val);
}
```

2. 这里是第一次搜索调用，即 `first_call_ptr` 设为 `true`。我们将其设为 `false` 并忘记。创建一个工作文件并初始化客户端消息结构。

```c
if (*first_call_ptr) {
    *first_call_ptr = 0;
    if (work_file) fclose(work_file);
    work_file = tmpfile();
    if (!work_file) return(ret_val);
}

mess_send.client_pid = mypid;
mess_send.request = s_find_cdc_entry;
strncpy(mess_send.cdc_entry_data.catalog, cd_catalog_ptr);
```

3. 接下来，这里有一个三层条件测试，它调用了 `pipe_imp.c` 中的函数。如果消息成功发送到服务器，客户端等待服务器的响应。当从服务器读取成功时，搜索匹配项被返回客户端的 `work_file`，并增加 `entries_matching` 计数器。

```c
if (send_mess_to_server(&mess_send)) {
    if (start_resp_from_server()) {
        while (read_resp_from_server(&mess_ret)) {
            if (mess_ret.response == r_success) {
                fwrite(mess_ret.cdc_entry_data, sizeof(cdc_entry), 1, work_file);
                entries_matching++;
            } else {
                break;
            }
        } /* while */
    } else {
        fprintf(stderr, "Server not responding\n");
    }
} else {
    fprintf(stderr, "Server not accepting requests\n");
}
```

## 第 13 章

4. 下一个测试检查搜索是否有任何结果。然后，`fseek` 调用将 `work_file` 设置为写入数据的下一个位置。

```c
if (entries_matching == 0) {
    fclose(work_file);
    work_file = (FILE *)0;
    return (ret_val);
}

(void)fseek(work_file, 0, SEEK_SET);
```

5. 如果这不是第一次使用此特定搜索词调用搜索函数，代码将检查是否还有剩余的匹配项。最后，将下一个匹配项读入 `ret_val` 结构体中。之前的检查保证了存在一个匹配项。

```c
else {
    /* *first_call_ptr */
    if (entries_matching == 0) {
        fclose(work_file);
        work_file = (FILE *)0;
        return (ret_val);
    }
}

read(&ret_val, sizeof(cdc_entry), work_file);
entries_matching--;

return (ret_val);
```

# 服务器接口

正如客户端有一个指向 `app_ui.c` 程序的接口，服务器端也需要一个程序来控制（重命名后的）`cd_access.c`，现在是 `cd_dbm.c`。服务器的主函数列在此处。

# 尝试——`server.c`

1. 我们首先声明一些全局变量、`process_command` 函数的原型，以及一个信号处理单元 `unistd.h` 以确保干净退出。

```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <fcntl.h>
#include <limits.h>
#include <signal.h>
#include <string.h>
#include <errno.h>
#include <sys/types.h>
#include <sys/stat.h>

#include "cd_data.h"

#include "cliserv.h"

int save_errno;

static int server_running = 1;

static void process_command(const message_db_t mess_command);

void catch_signals() {

    server_running = 0;

}
```

2. 现在我们进入主函数。在检查信号处理程序是否正确后，程序会检查你是否在命令行上传递了 `-i`。如果是，它将创建一个数据库。如果调用 `cd_dbm.c` 中的 `database_initialize` 例程失败，将显示错误消息。如果服务器运行，则一切正常，来自客户端的任何请求将由 `process_command` 函数处理，稍后我们将向你展示它。

```c
int main(int argc, char *argv[]) {

    struct sigaction new_action, old_action;

    message_db_t mess_command;

    int database_init_type = 0;

    new_action.sa_handler = catch_signals;

    sigemptyset(&new_action.sa_mask);

    new_action.sa_flags = 0;

    if ((sigaction(SIGINT, &new_action, &old_action) != 0) ||
        (sigaction(SIGHUP, &new_action, &old_action) != 0) ||
        (sigaction(SIGTERM, &new_action, &old_action) != 0)) {

        fprintf(stderr, "Server startup error, signal catching failed\n");

        exit(EXIT_FAILURE);

    }

    if (argc > 1) {

        argc++;

        if (strncmp("-i", argv, 2) == 0) database_init_type = 1;

    }

    if (!database_initialize(database_init_type)) {

        fprintf(stderr, "Server error:-\n            could not initialize database\n");

        exit(EXIT_FAILURE);

    }

    if (!server_starting()) exit(EXIT_FAILURE);

    while (server_running) {

        if (read_request_from_client(&mess_command)) {

            process_command(mess_command);

        } else {

            if (server_running) fprintf(stderr, "Server ended - can not \
                read pipe\n");

        }

    }

    server_running = 0;

    /* while */

    server_ending();

    exit (EXIT_SUCCESS);

}
```

3. 任何客户端消息都会传递给 `process_command`，在那里它们被输入到一个 `switch` 语句，该语句对 `cd_dbm.c` 进行相应的调用。

```c
static void process_command(const message_db_t comm)
{
    message_db_t resp;
    int first_time = 1;

    resp = comm; /* 复制命令，然后根据需要更改 resp */

    if (!start_resp_to_client(resp)) {
        fprintf(stderr, "Server Warning: \
            start_resp_to_client %d failed!\n", resp.client_pid);
        return;
    }

    resp.response = r_success;
    memset(resp.error_text, '\0', sizeof(resp.error_text));
    save_errno = 0;

    switch(resp.request) {
        case s_create_new_database:
            if (!database_initialize(1)) resp.response = r_failure;
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;

        case s_get_cdc_entry:
            resp.cdc_entry_data = get_cdc_entry();
            break;
    }
}
```
