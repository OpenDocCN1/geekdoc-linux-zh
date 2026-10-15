
```c
/* uname.c:
 *
 * Example of uname(2):
 */

#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <errno.h>
#include <string.h>
#include <sys/utsname.h>

int
main(int argc, char **argv) {
    int z;
    struct utsname u_name;
    
    z = uname(&u_name);
    
    if ( z == -1 ) {
        fprintf(stderr, "%s: uname(2)\n",
                strerror(errno));
        exit(1);
    }
    
    printf( " sysname[] = '%s'\n",
            u_name.sysname);
    printf( " nodename[] = '%s'\n",
            u_name.nodename);
    printf( " release[] = '%s'\n",
            u_name.release);
    printf( " version[] = '%s'\n",
            u_name.version);
    printf( " machine[] = '%s'\n",
            u_name.machine);
    printf( " domainname[] = '%s'\n",
            u_name.domainname);
    
    return 0;
}
```

列表 9.1 中使用的步骤如下：

- 分配结构 `u_name` 以接收来自 `uname(2)` 的数据（第 15 行）。
- 在第 17 行调用 `uname(2)`。
- 检查并报告错误（第 19 行到第 23 行）。
- 报告返回的值（第 25 行到第 36 行）。

以下会话输出展示了如何编译和运行该程序。示例系统 `lux` 上程序的输出也作为一个示例包含在内（注意该系统未配置为使用 NIS）：

```sh
@lux
$ make uname
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type uname.c
gcc uname.o -o uname
```

![](img/961a0296fe36074690a9847b79332eff_217_0.png)

对程序进行的小改动是：

- 该程序现在接受命令行上的可选端口号作为第二个参数（第 60 行和第 61 行）。
- 移除了对 `getservbyname(3)` 的调用，因为端口号现在默认为 9999 或在命令行上明确给出。

以下会话展示了如何编译和测试客户端程序，针对一个宽泛地址的服务器：

```sh
@pepper
$ make daytime
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type daytime.c
gcc daytime.o -o daytime
@pepper
$ ./daytime 127.0.0.1 9999
Date & Time is: Sunday Aug 22 22:02:19 1999

@pepper
$ ./daytime 192.168.0.1 9999
Date & Time is: Sunday Aug 22 22:02:30 1999

@pepper
$
```

该会话演示了客户端程序如何成功从主机 `pepper` 上两个可能的 IP 地址调用同一个服务器。如果你的网络中有远程主机，请务必远程尝试该程序。

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
>
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

以下输出会话显示了在假设的系统 `tux` 上对该程序进行编译和运行的过程：

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
