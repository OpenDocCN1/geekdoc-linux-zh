
结构的第一个字段是指向对话函数的指针，该函数必须按照给定的原型进行声明。第二个字段可以是 `NULL`，也可以指向某些任意数据；无论其值为何，都会作为第四个参数原封地传递给对话函数。

每次对对话函数的调用都包含一组消息和期望的响应。消息包含在 `msg` 参数中，消息总数存储在 `num_msg` 参数中。每条消息都应该以适用于应用程序的方式显示给用户（`stdout` 或 `stderr`、用户下方的弹出窗口等）。如果消息类型需要响应，函数应该接受用户的输入并将其存储在指向 `resp` 的 `pam_response` 结构体数组（`num_msg` 个项）中；`resp` 中的项与 `msg` 中的项对应，因此为 `message[n]` 接收到的响应应存储在 `resp[n]` 中。最后，在正常情况下函数应返回 `PAM_SUCCESS`；如果发生错误，函数应返回 `PAM_CONV_ERR` 且不更改 `resp` 中的任何信息。

`pam_message` 和 `pam_response` 结构体的定义如下：

```c
struct pam_message {
  int msg_style;
  const char *msg;
};

struct pam_response {
  char *resp;
  int resp_retcode;
};
```

`pam_message` 结构体的成员是一个指向显示给用户的消息字符串的指针。`pam_response` 结构体的 `resp` 字段指向一个用于填充用户响应的缓冲区；该缓冲区长度为 `PAM_MAX_MSG_SIZE` 字节，因此函数复制到缓冲区的信息不会超过此限制。`msg` 字段的长度也不应超过 `PAM_MAX_MSG_SIZE` 字节；然而，应用程序不应期望这种行为，因为 PAM 并不强制执行。`resp_retcode` 字段应设置为零；它目前未被使用。

这就留下了 `pam_message` 的 `msg_style` 字段。该字段的值决定了它是什么类型的消息，以及是否期望来自用户的响应。它可以被设置为以下值：

| 常量 |  |
| :--- | :--- |
| `PAM_PROMPT_ECHO_OFF` | 应该显示此消息，用户应输入响应。用户输入时对响应的回显应关闭；PAM 对在替代处显示的内容没有要求，因为应用程序可以自由使用任何合适的惯例（无响应、回显星号 * 等）。 |
| `PAM_PROMPT_ECHO_ON` | 应该显示此消息，用户应输入响应。可以开启回显。 |
| `PAM_ERROR_MSG` | 应该以适用于错误消息的方式显示消息。不期望输入。 |
| `PAM_TEXT_INFO` | 不期望输入。应该显示此消息。该消息不是错误，因此可以用任何合适的方式显示。 |

## 第 12 章

`PAM_BINARY_PROMPT` 这种消息类型是 Linux 支持的扩展。它包含一个用于客户端-服务器认证协议的二进制消息，并期望一个响应。在大多数情况下，提示和响应非常依赖于特定的身份验证协议，因此确定是否显示提示或如何接收响应很大程度上取决于应用程序和协议。

`PAM_BINARY_MSG` 这种消息类型与上一种一样，是 Linux 特有的。它也包含一个二进制消息，但对其不期望响应。

现在有许多应用程序通过文本会话进行交互，对输入输出的格式没有特殊需求。对于这些应用程序，`pam_misc` 库提供了 `misc_conv`；此函数是一个完整的工作函数，通过对标准文件流进行简单的读写来执行其所有功能。这节省了编写自定义对话函数的精力，因为所有这些函数都可能实现完全相同的行为。

## 示例

假设有存储敏感文件的需求，只有系统的有效用户才能访问（并在未来可能定义其他可能的限制）。让我们假设对无人值终端存在担忧，因此我们要求用户在访问这些文件之前重新输入密码。

这一目标可以通过编写一个文件查看器来实现，该查看器要求用户在查看文件之前先通过身份验证。然后我们可以创建一个用户，将我们敏感文件的所有者设为该新用户，使其仅对所有者可读，并将我们的文件查看器设置成 `setuid` 为该用户；这确保了读取文件的唯一方法是通过我们的查看器。

首先，我们使用 PAM 来进行身份验证，并将使用 `misc_conv` 对话函数来节省一些工作。所以，算上我们需要做的非 PAM 方面的工作，我们需要以下头文件：

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <pwd.h>
#include <syslog.h>
#include <security/pam_app.h>
#include <security/pam_misc.h>
#include <security/pam_types.h>
```

我们不需要复杂的错误检查；对于已过期的密码之类的错误，我们可以接受它们。因此，我们只需要在每个阶段检查 `PAM_SUCCESS`。我们也不需要任何类似重试机制，因为如果第一次失败，应用程序可以重新运行。为了避免重复进行相同检查的繁琐，让我们创建一个错误测试函数，向用户显示一条通用消息，并将真实错误记录到 `syslog(3)` 中：

```c
void test_pam_error(pam_handle_t *ph, int pam_retrieval) {
    fputs("authpam: auth error\n", stderr);
    syslog(LOG_ERR, pam_strerror(ph, pam_retrieval));
    exit(EXIT_FAILURE);
}
```

接下来，我们初始化 `main`，声明变量并检查命令行参数：

```c
int main(int argc, char *argv[]) {
    int retval;
    struct passwd *myinfo;
    struct pam_conv_t myconv;
    pam_handle_t *pamhandle = NULL;
    FILE *secure_file;
    char buf[256];

    openlog("authcat", LOG_PID, LOG_AUTH);
    if (argc != 2) {
        fputs("authcat: usage authcat <filename>\n", stderr);
        exit(EXIT_FAILURE);
    }

    myinfo = getpwuid(getuid());
    if (myinfo == NULL) {
        fputs("authcat: cannot determine user\n", stderr);
        exit(EXIT_FAILURE);
    }

    myconv.conv = misc_conv;
    myconv.appdata_ptr = NULL;
    retval = pam_start("authcat", myinfo->pw_name, &myconv, &pamhandle);
    test_pam_error(retval, NULL);
```

接下来，我们进行实际身份验证。我们不在凭据或会话管理，因为这是一次性认证，所以我们需要认证和账户服务：

```c
retval = pam_authenticate(pamhandle, 0);
test_pam_error(retval, NULL);
retval = pam_acct_mgmt(pamhandle, 0);
test_pam_error(retval, NULL);
```

如果我们一直走到这里没有被错误函数杀死，说明是合法的。现在我们现在显示文件：

```c
secure_file = fopen(argv[1], "r");
if (secure_file == NULL) {
    fputs("authcat: cannot open file\n", stderr);
    exit(EXIT_FAILURE);
}

while (!feof(secure_file)) {
    if (fgets(buf, 256, secure_file))
        fputs(buf, stdout);
}

fclose(secure_file);
```

现在我们完成了。我们现在关闭 PAM 并正常返回：

```c
retval = pam_end(pamhandle, retval);
test_pam_error(retval, NULL);
return EXIT_SUCCESS;
}
```
