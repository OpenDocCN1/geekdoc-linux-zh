
## 获取主机名和域名

函数 `gethostname(2)` 和 `getdomainname(2)` 是另外两个可用于查询当前系统信息的函数。

### 使用 gethostname(2) 函数

`gethostname(2)` 函数可用于确定当前的主机名。其函数原型如下所示：

```c
#include <unistd.h>

int gethostname(char *name, size_t len);
```

此函数接受两个参数：

- 接收缓冲区 `name`，其长度必须为 `len` 字节或更长。
- 接收缓冲区 `name` 的最大长度（`len`，单位为字节）。

如果成功，该函数的返回值为零。如果发生错误，则返回 -1。错误由外部变量 `errno` 描述。

> **提示**
> `gethostname(2)` 的 `len` 参数必须包含要返回的主机名的总长度以及末尾的空字节。

### 使用 getdomainname(2) 函数

`getdomainname(2)` 函数是另一个便利函数，允许程序员查询程序正在执行的宿主机的 NIS 域名。函数原型如下：

```c
#include <unistd.h>

int getdomainname(char *name, size_t len);
```

此函数的用法与 `gethostname(2)` 函数完全相同。这两个参数是：

- 缓冲区 `name`，用于接收域名，且长度至少为 `len` 字节。
- 缓冲区 `name` 的缓冲区长度（`len`，单位为字节）。

同样，函数成功时返回零。发生错误时返回 -1。外部变量 `errno` 包含失败时的错误代码。

Linux 的手册页指出，`getdomainname(2)` 函数内部使用 `uname(2)` 函数来获取并返回 NIS 域名。

### 测试 gethostname(2) 和 getdomainname(2)

这两个函数在清单 9.2 中提供的程序中进行演示。该程序只是调用这些函数并报告其结果。

![](img/961a0296fe36074690a9847b79332eff_225_0.png)

**清单 9.2：gethostn.c——gethostname(2) 和 getdomainname(2) 演示程序**

```c
/* gethostn.c:
 *
 * Example of gethostname(2):
 */
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <errno.h>
#include <string.h>

int
main(int argc, char *argv[]) {
    int z;
    char buf[32];

    z = gethostname(buf, sizeof buf);

    if (z == -1) {
        fprintf(stderr, "%s: gethostname(2)\n",
                strerror(errno));
        exit(1);
    }

    printf("host name = '%s'\n", buf);

    z = getdomainname(buf, sizeof buf);

    if (z == -1) {
        fprintf(stderr, "%s: getdomainname(2)\n",
                strerror(errno));
        exit(1);
    }

    printf("domain name = '%s'\n", buf);

    return 0;
}
```

使用的步骤如下：

1. 定义一个大小合适的缓冲区（第 14 行）。
2. 调用 `gethostname(2)` 将主机名获取到字符数组 `buf[]` 中（第 16 行）。
3. 检查并报告错误（第 18 至 22 行）。
4. 报告主机名（第 24 行）。
5. 调用 `getdomainname(2)` 将 NIS/YP 域名获取到同一个字符数组 `buf[]` 中（第 26 行）。
6. 检查并报告错误（第 28 至 32 行）。
7. 报告域名（第 34 行）。

以下输出会话显示了在假设的系统 tux 上对该程序进行编译和运行的过程：

![](img/961a0296fe36074690a9847b79332eff_226_0.png)

```bash
$ make gethostn
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type gethostn.c
gcc gethostn.o -o gethostn
$ ./gethostn
host name = 'tux'
domain name = ''
```

在这个示例运行中，您可以看到主机和域名的值都已成功报告（尽管由于未配置 NIS 域，域名被报告为空字符串）。您的值将与所示示例有所不同，特别是如果您已经配置了 NIS 域。在了解了如何查询本地系统后，现在是将注意力转向解析远程主机名的时候了。这将是本章剩余部分的重点。

## 解析远程地址

将类似 www.lwn.net 这样的名称转换为 IP 编号的过程相当复杂。它涉及本地系统 /etc 目录中的多个文件，包括诸如 /etc/resolv.conf、/etc/hosts 和 /etc/nsswitch.conf 等文件（仅举几个例子）。根据本地系统的配置情况，其他文件和守护进程也可能发挥作用。例如，在查询这些文件之后，可以查询名称服务器，然后该服务器可以将查询转发给其他名称服务器。所有这些复杂性都是你在编写应用程序时真正不想去考虑的细节。

幸运的是，应用程序编写者可以扮演鸵鸟的角色，把头埋进沙子里。如果系统配置正确，程序员只需要几个系统函数调用即可。接下来介绍的是一组相关函数，它们为您隐藏了远程名称查找的复杂性。

> **注意**
> 本书假设你拥有一个配置正确的 Linux 系统。关于系统管理和网络管理已经写了很多整本书。因此，本书的重点是教你如何使用套接字编程，而不是如何设置域名和名称服务器。

## 错误报告

即将描述的函数使用不同的变量进行错误报告。在普通的 C 库函数中，错误代码报告给变量 `errno`（通过包含 `errno.h` 声明）。然而，本节的函数将其错误报告给变量 `h_errno`。其原型如下所示：

```c
#include <netdb.h>
extern int h_errno;
```

`h_errno` 变量是一个外部整型变量。以下函数将错误发布到 `h_errno`：

- `gethostbyname(3)`
- `gethostbyaddr(3)`

以下函数使用 `h_errno` 的值作为输入：

- `herror(3)`
- `hstrerror(3)`

> **警告**
> 请注意，`h_errno` 值存在一个缺陷，即它不能在同一个进程中的不同线程之间共享。虽然较新的 glibc 库已使 `errno` 线程安全，但 `h_errno` 值不是线程安全的。

## 报告 h_errno 错误

您可能知道，`strerror(3)` 函数方便地将 `errno` 值转换为人类可读的错误消息。同样，存在两种报告 `h_errno` 值的方法：

```c
#include <netdb.h>
extern int h_errno;

void herror(const char *msg);

const char *hstrerror(int err);
```

函数 `herror(3)` 很像 `perror(3)` 函数。`herror(3)` 函数现在被认为是过时的，但您可能在现有的源代码中找到它。它打印消息 `msg`，随后跟随错误文本。这被写入标准错误（`stderr`）输出流。

`hstrerror(3)` 函数镜像了熟悉的 `strerror(3)` 函数的功能。它接受 `h_errno` 输入值作为输入，并返回一个指向描述错误的文本消息的指针。返回的指针仅在下一次调用此函数之前有效。

## 理解错误代码

用于 `h_errno` 变量的 C 宏与 `errno` 值有显著差异。表 9.2 列出了在调用 `gethostbyname(3)` 和 `gethostbyaddr(3)` 时你可能会遇到的错误代码。

