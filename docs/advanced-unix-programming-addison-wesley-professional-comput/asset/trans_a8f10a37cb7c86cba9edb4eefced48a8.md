
保持。如果变量尚不存在，它将被添加到环境中，并且 `overwrite` 的值无关紧要。

`unsetenv` 是随 `setenv` 一起提供的，它用于从环境中移除变量及其值。如果系统没有 `unsetenv`，从环境中移除变量的最佳办法是将其值设置为空字符串，根据应用程序的不同，这种方式可能可接受，也可能不可接受。（某些系统，如 Linux、FreeBSD 和 Darwin，将 `unsetenv` 定义为 `void` 函数，因此没有错误返回值。）

虽然这些函数的接口是标准化的，但它们的实际存在并非强制要求。FreeBSD、Linux 和 Solaris 都有 `putenv`，前两者则有全部三个函数。SUS3 要求具备 `setenv` 和 `unsetenv`，但截至本文写作时，尚无任何 SUS3 系统，因此没有简单、可移植的方法来判定哪些函数存在。`setenv` 和 `unsetenv` 源自 BSD，应当存在于所有由其衍生出的系统中，包括 FreeBSD；`putenv` 源自 System V，应当存在于所有由其衍生出的系统中，包括 Solaris。鉴于 SUS 推荐使用 `setenv` 和 `unsetenv`，也许最佳做法是使用这两个函数进行编码，并为那些尚未提供它们的系统自行包含实现版本。

如果不关心内存泄漏，实现 `setenv` 和 `unsetenv` 很容易。问题在于它们可能需要分配内存，或者在 `unsetenv` 的情况下产生孤立内存，但由于无法假设最初的内存是如何分配的，因此它们无法释放这些内存。尽管存在这一缺陷，以下是我们版本的 `setenv`：

```c
int setenv(const char *var, const char *val, int overwrite)
{
    int i;
    size_t varlen;
    char **e;

    if (var == NULL || val == NULL || var[0] == '\0' ||
        strchr(var, '=') != NULL) {
        errno = EINVAL;
        return -1;
    }
    varlen = strlen(var);
    for (i = 0; environ[i] != NULL; i++)
        if (strncmp(environ[i], var, varlen) == 0 &&
            environ[i][varlen] == '=')
            break;

    if (environ[i] == NULL) {
        if ((e = malloc((i + 2) * sizeof(char *))) == NULL)
            return -1;
        memcpy(e, environ, i * sizeof(char *));
        /* 旧的指针数组可能存在内存泄漏 */
        environ = e;
        environ[i + 1] = NULL;
        return setnew(i, var, val);
    } else {
        if (overwrite) {
            if (strlen(&environ[i][varlen + 1]) >= strlen(val)) {
                strncpy(&environ[i][varlen + 1], val, strlen(val));
                return 0;
            }
            return setnew(i, var, val);
        }
        return 0;
    }
}
```

关于此函数的说明：

-   我们首先做的是检查参数，这是 SUS 要求的。
-   接下来我们搜索环境，查看该变量是否已经定义。请注意，我们必须查找以该名称开头后跟等号（=）的字符串。
-   如果找到该变量，且 *overwrite* 参数为假，则退出。否则有两种情况：新值能容纳，此时我们直接复制进去；或者容纳不下，此时我们调用函数 *setnew*（如下所示）将其放入。
-   如果未找到该变量，我们需要扩展数组。正如我们所说，我们不能使用 *realloc*，因为我们无法假设旧内存是如何分配的。因此，我们使用 *malloc* 并自行复制旧内容。然后，我们用 *NULL* 指针终结新数组，并调用 *setnew* 放入新条目。

以下是 *setnew*，它分配空间用于名称、等号和值，并将其存储在数组中：

```c
static int setnew(int i, const char *var, const char *val)
{
    char *s;

    if ((s = malloc(strlen(var) + 1 + strlen(val) + 1)) == NULL)
        return -1;
    strncpy(s, var, strlen(var) + 1);
    strcat(s, "=");
    strcat(s, val);
    /* environ[i] 的旧值可能导致内存泄漏 */
    environ[i] = s;
    return 0;
}
```

最后，我们有 `unsetenv`，它检查参数，查找变量，如果存在，则将数组其余部分向下滑动，从而有效地将其移除。这也会产生可能的内存泄漏，因为我们无法假设被取消设置的变量的内存可以被释放。

```c
int unsetenv(const char *var)
{
    int i, found = -1;
    size_t varlen;
    size_t t;

    if (var == NULL || var[0] == '\0' || strchr(var, '=') != NULL) {
        errno = EINVAL;
        return -1;
    }

    varlen = strlen(var);
    for (i = 0; environ[i] != NULL; i++)
        if (strncmp(environ[i], var, varlen) == 0 &&
            environ[i][varlen] == '=')
            found = i;
    if (found != -1) {
        /* environ[found] 的旧值可能导致内存泄漏 */
        /* 计算包括 NULL 终止符在内的指针总数 */
        t = i + 1; 
        /* i 是最后一个有效条目的索引加 1（即 NULL 的索引），
           因此需要移动的元件数量为 i - found */
        /* 注意：原始代码中的 't' 在此处范围内未定义，
           假设 't' 意指剩余元件的数量。
           在移动内存的上下文中，我们从 found+1 移动到末尾。
           要移动的数量是（总元件数 - found - 1）个指针，
           加上 NULL 终止符？
           实际上，memmove 是复制。我们需要覆盖 environ[found]。
           源是 environ[found+1]。
           目标是 environ[found]。
           要移动的元件数量是从索引 found+1 到 NULL 终止符。
           假设 environ 中的指针总数为 N。
           我们要移动从 N-found-1 个元件吗？不，我们要移动从 found+1 到末尾的数组。
           原始代码使用了 't'。查看上面的循环，'i' 在 NULL 索引处结束。
           因此，指针总数是 'i'。
           要移动的元件数量是 i - found。
           但我们还需要确保 NULL 终止符被移动。
           如果 environ[i] 是 NULL，且我们从 found+1 开始移动，我们移动 i-found 个元件？
           让我们看看原始代码：memmove(&environ[found], &environ[found + 1], (t - found) * sizeof(char *));
           这里 't' 可能是 NULL 终止符的索引（即上面循环中的 'i'，但 'i' 在循环作用域内？不，'i' 在外部声明）。
           等等，在上一段中：
           for (i = 0; environ[i] != NULL; i++) ...
           所以 'i' 保存了 NULL 指针的索引。
           因此，指针总数是 'i'（0 到 i-1 是有效的，i 是 NULL）。
           我们要移除索引 'found'。
           我们需要移动从 found+1 到 i（包含 NULL）的指针。
           数量是 i - found。
           原始代码说 (t - found)。如果 t == i，那么它是正确的。
           假设 't' 是保存总数或 NULL 索引的变量。
           在提供的 OCR 中：
           for (i = 0; environ[i] != NULL; i++) ...
           ...
           memmove(..., (t - found) * sizeof(char *));
           
           由于 't' 未在所提供的 unsetenv 函数范围的直接作用域中定义，
           但 'i' 已定义。极有可能是 't' 是 'i' 的拼写错误，或者是一个
           计算总大小的变量。鉴于循环在 environ[i]==NULL 处结束，
           'i' 是指针的数量。
           我们将 't' 更正为 'i'，因为它是唯一可能保存总长度索引的合理变量。
        */
        memmove(&environ[found], &environ[found + 1],
                (i - found) * sizeof(char *));
    }
    return 0;
}
```

请注意，我们使用 `memmove` 而不是 `memcpy`，因为前者保证在源和目标内存区域重叠时也能正常工作，而这种情况在此处必然发生。

你可能想知道为什么我们在这些函数中没有使用我们的“ec”错误检查宏。原因是我们希望它们的行为尽可能接近标准函数。

修正 `setenv` 和 `unsetenv` 中的内存泄漏问题相当直接；参见练习 5.1。

## 5.3 exec 系统调用

如果不完全理解进程与程序之间的区别，就不可能理解 *exec* 或 *fork* 系统调用。如果这些术语对你来说是新的，你可能想要回头复习第 1.1.2 节。如果你准备继续，我们将用一句话总结这种区别：进程是一个执行环境，由指令、用户数据和系统数据段组成，以及运行时获取的大量其他资源；而程序是一个包含指令和数据的文件，用于初始化进程的指令段和用户数据段。

*exec* 系统调用使用指定的程序重新初始化一个进程；程序改变，但进程保持不变。另一方面，*fork* 系统调用（第 5.5 节的主题）通过仅仅复制指令、用户数据和系统数据段来创建一个新进程，该进程是现有进程的克隆；新进程不是由程序初始化的，因此新旧进程执行相同的指令。

单独来看，*fork* 和 *exec* 的用途有限——大多数情况下，它们是配合使用的。在我分别介绍它们时请记住这一点，不要因为你认为它们*无用*而惊慌——只需试着理解它们的作用。在第 5.4 节中，当我们联合使用它们时，你会发现它们是一对强有力的工具。

除了启动 UNIX 内核本身之外，*exec* 是 UNIX 上执行程序的唯一方式。不仅 shell 使用 *exec* 来执行程序，shell 及其祖先是同样由 *exec* 调用的。而 *fork* 是创建新进程的唯一方式。

实际上，并没有名为“*exec*”的系统调用。所谓的“*exec*”系统调用是一组六个，名称形式为 *execAB*，其中 *A* 是 *l* 或 *v*，取决于参数是在调用中直接给出（列表）还是在数组中（向量），*B* 是 *absent*、表示应使用 *PATH* 环境变量搜索程序的 *p*，或表示使用特定环境的 *e*。（奇怪的是，你无法在同一个调用中同时获得 *p* 和 *e* 功能。）因此，六个名称是 *execl*、*execv*、*execlp*、*execvp*、*execl e* 和 *execve*。² 我们将从 *execl* 开始，然后处理其他五个。

> 2. 相同的特性可以在两个系统调用中轻松提供，而不是六个，但现在改变为时已晚。参见练习 5.6。

### exec—使用参数列表执行文件

```c
#include <unistd.h>
int execl(
    const char *path, /* 程序路径名 */
    const char *arg0, /* 第一个参数（文件名） */
    const char *arg1, /* 第二个参数（如果需要） */
    ... /* 其余参数（如果需要） */
    (char *)NULL /* 参数列表终止符 */
);
/* 出错时返回 -1（设置 errno） */
```

参数 `path` 必须指定一个可执行文件，该文件必须能被有效用户 ID 执行（例如模式 755），且具有可执行程序的正确内容。进程的指令段被程序的指令覆盖，进程的用户数据段被程序的数据覆盖，并重新初始化栈。然后进程从顶部执行新程序（即调用其 `main` 函数）。

成功的 `execl` 无法返回，因为返回地址已丢失。不成功的 `execl` 会返回，值为 -1，但无需测试该值，因为不可能有其他值。不成功的 `execl` 最常见的原因是 `path` 不存在或不可执行。

`execl` 中跟随在 `path` 后面的参数被收集到一个字符指针数组中；最后一个参数必须是 `NULL`，它停止收集并终止数组。按照惯例，第一个参数是程序文件的名称（而不是完整路径）。新程序可以通过 `main` 的熟悉参数 `argc` 和 `argv` 访问这些参数。由 `environ` 指向的环境也会被传递过去，并且可以通过新程序的 `environ` 指针或 `getenv` 访问，如上一节所述。

由于进程继续存在，且其系统数据段基本上未受扰动，进程的大多数属性保持不变，包括进程 ID、父进程 ID、进程组 ID、会话 ID、控制终端、实际用户 ID 和组 ID、当前和根目录、优先级、累计执行时间，以及通常打开的文件描述符。列出那些确实发生变化的主要属性更简单，且都有充分理由：

