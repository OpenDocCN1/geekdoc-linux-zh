
教程中的 `malloc,free` 配对说明了一个相关的示例。当执行以下代码并终止时，由于第二个变量 `uidstr` 没有内存关联，因此会发生段错误：

```
char *uidstr = "0";
```

记住这一点极其重要：如果一个用户的 `ID` 值为 `0`，那么它将自动拥有 `root` 权限；因此，`root` 用户使用的不是 `ID` 的名称。以下显示了一个 C 语言程序，它可以查找 `/etc/passwd` 中所有用户 `ID` 为 `0` 的用户：

```c
#include <stdio.h>
#include <string.h>
#define MAXLINESIZE 512
int main(int argc, char **argv) {
    FILE *INPUT;
    char buffer[MAXLINESIZE];

    // 以只读模式打开 /etc/passwd
    INPUT = fopen("/etc/passwd", "r");
    while (fgets(buffer, sizeof(buffer), INPUT) != NULL) {
        // 忽略 /etc/passwd 中的注释
        if (buffer[0] == '#')
            continue;
        // 用户 ID 是第三字段
        char *username = strtok(buffer, ":");
        char *password = strtok(NULL, ":");
        char *uid = strtok(NULL, ":");
        if (strcmp(uid, "0") == 0)
            printf("User %s has root privileges!\n", username);
    }

    fclose(INPUT);
    return 0;
}
```

### 大多数（如果不是全部）程序都有权访问读取或修改文件，这通常在后台完成

这在尝试执行 `-R` 命令（列出所有子目录）时非常有价值。密码文件包含每个用户的条目。该用户的系统文件是：`/etc/passwd`

冒号（`:`）分隔了 `/etc/passwd` 文件中的字段。第一个字段是用户名，第二个字段是用户名的长度。第三字段是用户 `ID`。第四个字段是家目录。请注意，你可以定义家目录的绝对路径而不是字符串，这被用于 Web 服务器等服务的用户。Web 服务器的条目如下：

```
root:x:0:0:root:/root:/bash
```

`bin/nologin` 是出于安全原因而应该禁用的账户的 Shell 替代方案。第三字段是用户 `ID` 的数值值，第四个字段是组 `ID` 的数值值。正如你将看到的，为了让组 `ID` 的数值值具有意义，你必须访问 `/etc/group`。

```
www-data:x:33:33::/bin/nologin
```

## 教程数据文件与信息

读取 `/etc/passwd` 没问题，但不要尝试在没有锁的情况下编辑它。`passwd` 结构在 `passwd.h` 中的定义如下：

```c
struct passwd {
    char *pwname;      /* 用户名 */
    char *pwpassword;  /* 密码 */
    uid_t uid;         /* 用户 ID */
    gid_t gid;         /* 组 ID */
    char *pwge;       /* 用户信息 */
    char *pwhome;      /* 家目录 */
    char *pwshell;     /* shell */
};
```

在 `/etc/passwd` 中，内核只检查用户 `ID` 和组 `ID`。由于只有 `root` 用户是不同用户（例如 `mtsuk`）的组才能访问某个文件，然后服务器进程在尝试执行请求的任务之前，会临时将其有效用户 `ID` 从 `root` 更改为 `mtsuk`。如果 `mtsuk` 不允许访问该文件，将生成错误。在完成 `mtsuk` 服务器要求的所有任务后，服务器进程将将其有效用户 `ID` 改回 `root`。许多服务器进程都是这样工作的。

`usergroup.c` 在 `FileSilo` 资源中提供，它通过访问 `/etc/group` 来打印所有属于命令行参数中指定组的用户。请注意，你提供的是组名或组 `ID`。一个简单的 C 程序执行以下输出：

```
$ UserGroups
Finding information about _116nThe group is stated with ID (116).
The members of this group are:
tsouuk
```

```c
appName = getservport(htons(port), NULL);
if (appName == NULL) {
    printf("unknown application!\n");
} else {
    name = appName->name;
    printf("port number %d is %s\n", port, name);
    return 0;
}
```

如果你想找到你所属的所有组，可以访问 `/etc/group` 的主页，它将返回用户所属的组列表。在该页面内部，你还会找到一个演示如何使用 `getgrouplist()` 的 C 程序。

`getgroup()` 返回有效组 `ID`。

`getgid()` 返回进程的实际组 `ID`。

请注意，你需要使用 `htons()` 函数转换端口号和网络字节序——一个关于网络字节序的快速教程将解释什么是主机序和网络序，以及为什么需要这种转换。

## 关于 Setuid

许多程序通过更改用户 `ID` 来执行在没有这样做的情况下难以完成的任务。示例 `/usr/bin/passwd` 允许普通用户在 `setuid()` 的帮助下写入 `/etc/passwd` 和 `/etc/shadow`。

## `/etc/services`

`services` 文件包含有关互联网的信息。以下行属于 `/etc/services`，并按顺序列出以便更好地理解其格式：

| Service | Port | Description |
|---|---|---|
| http | 80 | #WorldHTTP |
| http | 80 | #HyperText Transfer Protocol |

```bash
$ ls -l /usr/bin/passwd
-rwxrsr-x 1 root root 48512 Jan 21 2014 /usr/bin/passwd
```

下面显示了一个 `getgeteuid()` 的 C 程序，它会显示其有效用户 `ID`。

第一个字段是端口名和使用的协议。`IANA` 的策略为 `TCP` 和 `UDP` 协议分别分配一个已知端口号。即使某个服务不支持其中一种，你也可以看到一条包含注释的行。

```c
#include <sys/types.h>
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <fcntl.h>
```

记住，`FTP` 或 `SSH` 没有默认的服务端口号。然而，你需要在客户端程序中显式声明你想要使用的端口。一个示例是访问 Web 服务器的 `http://www.example.com/`。

## C 结构和 struct

结构是 C 中一种用户定义的数据类型，允许你组合不同类型的数据项，包括结构。你可以使用点运算符 (`.` 访问结构的任何单个成员，该点是结构变量名与要访问的成员之间的分隔符。你也可以使用结构指针，如下代码所示：

你可以使用以下系统调用访问 `/etc/services` 中的信息：`getservname(name)`, `getservport(port, protocol)`, `getservbyname(name, protocol)`。

```c
#include <sys/types.h>
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
```

```c
int value;
list * list;
an_aliz_to_the_list;
```

`getservbyport(port)` 演示了 `getservbyport` 系统调用的结构。

在这里，你创建了一个链表，每个节点都有指向下一个节点的指针。在关闭括号后，你可以使用 `head` 访问链表。

```c
int main(int argc, char **argv) {
    struct servent *appName;
    int port = 80;
    char *name;
```
