
然而，通过将游戏程序 `setuid` 为你自己，运行游戏的用户将你的 UID 作为他们的有效 UID。游戏程序就可以根据需要打开并更新文件，但任意用户无法来编辑它。（你同时也让自己暴露在 `setuid` 编程的大部分风险中；例如，如果游戏程序存在可以被利用产生以你身份运行的 `shell` 的漏洞，那么你所有的文件都可以被删除或更改。这是一个令人恐惧的想法。）

同样的逻辑也适用于 `setgid` 程序，尽管在实践中 `setgid` 程序远少于 `setuid` 程序。

获取 UID 和 GID 的逻辑是相同的。从系统获取 UID 和 GID 非常简单。函数如下：

```c
#include <unistd.h>

uid_t getuid();
uid_t geteuid();

gid_t getgid();
gid_t getegid();

int getgroups(int size, gid_t list[]);
```

- `getuid()`：返回真实 UID。
- `geteuid()`：返回有效 UID。
- `getgid()`：返回真实 GID。
- `getegid()`：返回有效 GID。
- `getgroups(int size, gid_t list[])`：从组集中填充最多 `size` 个元素。返回填充的数量，如果出错返回 `-1`。是否包含 EID 取决于实现。

在符合 POSIX 标准的系统中，你可以传递零；在这种情况下，`getgroups()` 返回组集中的数量。然后你可以根据该值动态分配足够的数组。

在非 POSIX 系统上，常量 `NGROUPS_MAX` 定义了列表的最大大小。该常量可以在现代系统的 `<limits.h>` 中找到，旧系统在 `<sys/param.h>`。我们将给出示例。

你可能注意到没有获取设置用户 ID 或设置组 ID 的调用。这些是有效 UID 和有效 GID 的原始值。因此，你可以在程序启动时使用如下代码获取这六个值：

```c
uid_t ruid, eid, saved_uid;
gid_t rgid, egid, saved_gid;

int main(int argc, char **argv)
{
  ruid = getuid();
  eid = saved_uid = getuid();

  rgid = getgid();
  egid = saved_gid = getegid();

  ... 程序其余部分 ...
}
```

这是一个获取组集的示例。作为扩展，`gawk` 提供了 `awk` 级访问真实和有效 UID、GID 值以及补充组集的权限。为了实现这一点，它必须检索组集。以下函数来自 `gawk` 3.1.3 分发版的 `main.c`：

```c
/* init_groupset -- 初始化组集 */
static void
init_groupset()
{
  #if defined(HAVE_GETGROUPS) && defined(NGROUPS_MAX) && NGROUPS_MAX > 0
    #ifdef GETGROUPS_NOT_STANDARD
    /* 对于不符合标准的系统，使用旧方法。 */
    ngroups = NGROUPS_MAX;
```

## 11.2 获取用户 ID 和组 ID

组相关变量是全局的，此处未显示它们的声明。`GETROUPS_T` 宏（第 1102 行）是用于第二个参数的类型；在 POSIX 系统上它是 `gid_t`，否则为 `int`。

第 1085 行和 1107 行括定了整个函数体；对于完全没有组集的古老系统，该函数的体体为空。

第 1086–1094 行处理非 POSIX 系统；`GETROUPS_NOT_STANDARD` 在程序编译前由配置机制定义。在这种情况下，代码如前文所述使用 `GROUUPS_MAX`。（尽管直到 2004 年，这类系统仍然存在并在使用；但幸运的是，它们的数量正在减少。）

第 1089–1094 行用于 POSIX 系统，通过使用大小参数 `0` 来检索组的数量。

最后，第 1102 行使用 `malloc()`（通过一个错误检查包装宏，见第 3.2.1.8 节，“示例：读取任意长度的行”，第 67 页）分配一个足够大的数组。第 1104 行填充该数组。

## 11.3 以真实用户身份检查：`access()`

在大多数情况下，有效和真实的 UID 以及 GID 值是相同的。因此，文件权限检查是针对有效 ID 而非真实用户，这并不重要。

然而，在编写 `setuid` 或 `setgid` 应用程序时，你可能想要检查一个对于有效 UID 和 GID 合法的操作，对于真实 UID 和 GID 是否也有效。这就是 `access()` 函数的任务：

```c
#include <unistd.h>

int access(const char *path, int amode);
```

`path` 参数是要检查检查真实 UID 和 GID 的文件路径。`amode` 是以下一个或多个值的按位或运算结果：

- `R_OK`: 真实 UID/GID 可以读取该文件。
- `W_OK`: 真实 UID/GID 可以写入该文件。
- `X_OK`: 真实 UID/GID 可以执行该文件，或者如果是目录，则可以搜索该目录。
- `F_OK`: 检查文件是否存在。

路径中的每个组件都会被检查。在某些实现中，当检查 `root` 用户时，如果文件权限中没有设置执行位，`access()` 的行为可能就像 `X_OK` 为真。（这很奇怪，但在这种情况下，有患胜于未患。）`Linux` 并没有这个问题。

如果操作对真实 UID 和 GID 允许，则返回 `0`，否则返回 `-1`。如果 `access()` 返回 `-1`，`setuid` 程序可以拒绝访问一个有效 UID/GID 能够操作的文件：

```c
if (access("/some/special/file", R_OK|W_OK) < 0) {
  fprintf(stderr,"Sorry: /some/special/file: %s\n", strerror(errno));
  exit(1);
}
```

至少在 2.4 系列 `Linux` 内核中，当 `X_OK` 测试应用于一个使用 `noexec` 选项挂载的文件系统时（见第 8.2.1 节，“使用挂载选项”，第 239 页），如果文件的权限指示执行权限，则测试将通过。尽管尝试执行该文件将失败。买自小心（Caveat emptor）。

> 注意：虽然在打开文件之前使用 `access()` 是正确的做法，但存在竞态条件：在 `access()` 检查和调用 `open()` 之间，打开的文件可能会被替换。需要严谨的编程，例如在调用 `access()` 和 `open()` 之前或之后使用 `stat()` 和 `fstat()` 检查所有者和权限。

例如，`pathchk` 程序检查路径的有效性。GNU 版本使用 `access()` 来检查给定路径的目录组件是否有效。参考 `Coreutils` 中的 `pathchk.c`：

```c
/* 如果 PATH 是可用的起始目录，返回 1；如果不是返回 0；
   不存在则返回 2。 */
static int
    dir_ok(const char *path)
{
    struct stat stats;
    if (stat(path, &stats)) // 非零返回 = 失败
        return 2;
    if (IS_ISDIR(stats.st_mode))
    {
        error(0, 0, "%s is not a directory", path);
        return 0;
    }
    /* 使用 access 测试搜索权限，因为 st_mode 的权限位在新的访问控制机制可能会失效。
       当然，如果你正在运行 setuid，access 会失效。*/
    if (access(path, X_OK) != 0)
    {
        if (errno == EACCES)
            error(0, 0, "%s is not searchable", path);
        else
            error(0, 0, "%s", path);
        return 0;
    }
    return 1;
}
```

代码逻辑直观。第 252–253 行检查文件是否存在。如果 `stat()` 失败，则文件不存在。第 255–259 行验证该文件确实是一个目录。第 261–264 行的注释解释了 `access()` 的用法。检查 `st_mode` 位在新的访问控制机制可能会失效。当然，如果你正在运行 `setuid`，`access` 会失效。

## 11.5 新文件的默认组
