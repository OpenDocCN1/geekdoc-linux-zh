
## 从密码文件中检索记录

```c
    char *pw_name;      /* 登录名 (用户名) */
    char *pw_password;  /* 加密密码 */
    uid_t pw_uid;      /* 用户 ID */
    gid_t pw_gid;       /* 组 ID */
    char *pw_gecos;      /* 注释 (用户信息) */
    char *pw_dir;       /* 初始工作（家）目录 */
    char *pw_shell;     /* 登录 shell */
};
```

`passwd` 结构的 `pw_gecos` 和 `pw_passwd` 字段在 SUSv3 中未定义，但在 UNIX 实现中可用。只有在启用密码影子功能时，`pw_passwd` 字段才包含有效信息。（在程序中，确定是否启用了密码影子最简单的方法是在成功调用 `getpwnam()` 后紧跟调用上述的 `getpwuid()`，以查看它是否返回了相同用户名的影子密码记录。）某些其他实现在此结构中还提供了额外的非标准字段。

> `pw_gecos` 的名称源于早期的 UNIX 实现，当时该字段包含用于与运行通用电气综合操作系统（GECOS）的机器通信的信息。尽管这种用法早已过时，但该字段名保留了下来，并且该字段被用于记录有关用户的信息。

`getpwuid()` 函数返回与 `getpwnam()` 完全相同的信息，但它是使用参数 `uid` 提供的数值 uid ID 进行查找的。
`getpwnam()` 和 `getpwuid()` 都返回一个指向静态分配结构的指针。在每次调用这两个函数之一（或调用下述的 `getpwent()` 函数）时，该结构都会被覆盖。

由于它们返回的是指向静态分配内存的指针，`getpwnam()` 和 `getpwuid()` 不是重入的。事实上，情况更为复杂，因为返回的结构包含指向其他已分配信息（例如 `pw_name` 字段）的指针。（我们在第 21.1.2 节解释了重入性。）类似的语句适用于 `getgrnam()` 和 `getgid()` 函数（稍后描述）。

SUSv3 提供了一组相应的重入函数——`getpwnam_rl`、`getgrnam_rl` 和 `getgid_rl`，它们接受 `passwd`（或组）结构作为参数和一个用于持有其他结构的缓冲区，指向 `passwd`（或组）结构的字段。此附加缓冲区所需的字节数可以通过 `sysconf(SC_GETPWR_R_SIZE_MAX)` 获取，在组相关函数的情况下可以通过 `sysconf(SC_GETGR_R_SIZE_MAX)` 获取。详细信息请参阅这些函数的手册页。

根据 SUSv3，如果未找到匹配的 `passwd` 记录，`getpwnam()` 和 `getpwuid()` 将返回原始的 `errno`。这意味着我们应该可以使用下面的代码来区分错误和“未找到”的情况：

```c
struct passwd *pwd;
error = 0;
pwd = getpwnam(name);
if (pwd == NULL)
    if (errno == 0)
        /* 未找到 */
    else
        /* 错误 */;
```

然而，许多 UNIX 实现在这一点上不符合 SUSv3。如果未找到匹配的 `passwd` 记录，这些函数返回 `NULL` 并将 `errno` 设置为零值，例如 `ENOENT` 或 `ESRCH`。在 2.7 版本之前，glibc 此这种情况产生 `ENOENT` 错误，但从 2.7 版本开始，glibc 符合 SUSv3 的要求。这些实现之间的这种差异部分是因为 POSIX.1-1990 未要求这些函数设置 `errno`，并允许它们在“未找到”的情况下设置 `errno`。所有这一切的后果是，在使用这些函数时很少能区分错误和“未找到”的情况。

## 从组文件中检索记录

`getgrnam()` 和 `getgrgid()` 从组文件中检索记录。

```c
#include <grp.h>

struct group *getgrnam(const char *name);
struct group *getgrgid(gid_t gid);
```

成功时返回一个指针，失败时返回 `NULL`；请参正文关于“未找到”的描述

`getgrnam()` 函数通过组名查找组信息，`getgrgid()` 函数通过组 ID 进行查找。两个函数都返回指向以下类型结构的指针：

```c
struct group {
    char *gr_name;      /* 组名 */
    char *gr_passwd;    /* 加密密码（如果没有密码影子功能） */
    gid_t gr_gid;       /* 组 ID */
    char **gr_mem;       /* 以 NULL 结尾的指针数组，
                         列出在 /etc/group 中的成员 */
};
```

`group` 结构的 `gr_passwd` 字段在 SUSv3 中未定义，但在 UNIX 实现中可用。只有在启用密码影子功能时，`gr_passwd` 字段才包含有效信息。

`getgrgid()` 函数返回与 `getgrnam()` 完全相同的信息，但它是使用参数 `gid` 提供的数值 gid ID 进行查找的。
`getgrnam()` 和 `getgrgid()` 都返回一个指向静态分配结构的指针。在每次调用这两个函数之一（或调用下述的 `getgrwent()` 函数）时，该结构都会被覆盖。

由于它们返回的是指向静态分配内存的指针，`getgrnam()` 和 `getgrgid()` 不是重入的。事实上，情况更为复杂，因为返回的结构包含指向其他已分配信息（例如 `gr_name` 字段）的指针。（我们在第 21.1.2 节解释了重入性。）类似的语句适用于 `getgrnam()` 和 `getgid()` 函数（稍后描述）。

SUSv3 提供了一组相应的重入函数——`getpwnam_rl`、`getgrnam_rl` 和 `getgid_rl`，它们接受 `passwd`（或组）结构作为参数和一个用于持有其他结构的……[后续文本]

根据 SUSv3，如果未找到匹配的 `passwd` 记录，`getpwnam()` 和 `getpwuid()` 将返回原始的 `errno`。这意味着我们应该可以使用下面的代码来区分错误和“未找到”的情况：

```c
struct passwd *pwd;
error = 0;
pwd = getpwnam(name);
if (pwd == NULL)
    if (errno == 0)
        /* 未找到 */
    else
        /* 错误 */;
```

然而，许多 UNIX 实现在这一点上不符合 SUSv3。如果未找到匹配的 `passwd` 记录，这些函数返回 `NULL` 并将 `errno` 设置为零值，例如 `ENOENT` 或 `ESRCH`。在 2.7 版本之前，glibc 此这种情况产生 `ENOENT` 错误，但从 2.7 版本开始，glibc 符合 SUSv3 的要求。这些实现之间的这种差异部分是因为 POSIX.1-1990 未要求这些函数设置 `errno` 并允许它们在“未找到”的情况下设置 `errno`。所有这一切的后果是，在使用这些函数时很少能区分错误和“未找到”的情况。

## 遍历密码文件

```c
#include <pwd.h>

struct passwd *getpwent(void);

成功时返回指针，在流末尾或出错时返回 NULL

void setpwent(void);
void endpwent(void);
```

`getpwent()` 逐条从密码文件中返回记录，在没有更多记录（或发生错误）时返回 `NULL`。在第一次调用时，`getpwent()` 会自动打开密码文件。当我们完成文件操作后，调用 `endpwent()`将其关闭。

我们可以通过以下代码遍历整个密码文件，并打印用户名和 ID：

```c
struct passwd *pwd;
while ((pwd = getpwent()) != NULL) {
    printf("%-%8s\n", pwd->pw_name, (long)pwd->pw_uid);
}
endpwent();
```
