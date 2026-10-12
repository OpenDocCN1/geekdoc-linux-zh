
### SYSTEM CALL: `pipe()`

**PROTOTYPE**: `int pipe(int fd[2]);`

**RETURNS**:
*   成功返回 `0`
*   错误返回 `-1`
    *   `errno = EMFILE` (无可用描述符)
    *   `EMFILE` (系统文件表已满)
    *   `EFAULT` (`fd` 数组无效)

### 原型定义：`int dup(int oldfd);`

**返回值**：
*   成功时返回新描述符
*   错误时返回 `-1`：
    *   `errno = EBADF` (`oldfd` 不是有效的描述符)
    *   `EBADF` (`newfd` 超出范围)
    *   `EMFILE` (该进程的描述符过多)

**备注**：旧的描述符不会关闭。两者可以互换。

虽然旧的描述符和新创建的描述符可以互换，但通常会先关闭标准流之一。`dup()` 系统调用会使用编号最小且未使用的描述符作为新描述符。

**考虑**：

```c
childpid = fork();

if(childpid == 0) {

    /* 关闭子进程的标准输入 */

    close(0);

    /* 将管道的输入端对复制到 stdin */

    dup(fd[0]);

    execclp("sort", "sort", NULL);

}
```

由于文件描述符 `0` (`stdin`) 已经关闭，`dup` 调用将管道的输入描述符 (`fd0`) 复制到了它的标准输入上。然后我们调用了 `execclp()`，用 `sort` 程序的文本段（代码）覆盖子进程的文本段。由于新 `exec()` 的程序会从其派生进程初始化标准流，它实际上继承了管道的输入端作为它的标准输入！现在，原始父进程发送到管道的任何内容，都会进入该设施。

还有另一个系统调用 `dup2()` 也可以使用。这个特定的调用源于 Unix 第 7 版，并一直延续到 BSD 版本，现在是 POSIX 标准所强制要求的。

### 系统调用：`dup2()`

**原型定义**：`int dup2(int oldfd, int newfd);`

**返回值**：
*   成功时返回新描述符
*   错误时返回 `-1`：
    *   `errno = EBADF` (`oldfd` 不是有效的描述符)
    *   `EBADF` (`newfd` 超出范围)
    *   `EMFILE` (该进程的描述符过多)

#### # 334 页 Linux 程序员指南：第 6 章

**备注**：使用 `dup2()` 会关闭旧的描述符

通过这个特定的调用，我们将关闭操作和实际的描述符复制封装在了一个系统调用中。此外，它保证了原子性，本质意味着它永远不会被到达的信号所中断。整个操作将在返回控制权给内核进行信号分发之前完成。在原始的 `dup()` 系统调用中，程序员必须在调用之前执行 `close()` 操作。这导致了两次系统调用，在它们之间经过的短暂时间内存在细微的脆弱性。如果在那个短暂瞬间到达了信号，描述符的复制就会失败。当然，`dup2()` 为我们解决了这个问题。

**考虑**：

```c
childpid = fork();

if(childpid == 0)

    /* 关闭 stdin，将管道的输入端复制到 stdin */

    dup2(0, fd[0]);

    execclp("sort", "sort", NULL);
```

### 轻松使用管道！

如果以上所有的闲言乱语看起来都是创建和利用管道的一种非常迂回的方法，那么还有另一种替代方案。

#### 库函数：`popen()`

**原型定义**：`FILE *popen(char *command, char *type);`

**返回值**：
*   成功时返回一个新的文件流
*   如果 `fork()` 或 `pipe()` 调用失败，返回 `NULL`

**备注**：创建一个管道，并使用 "command" 执行 `fork`/`exec` 操作。

这个标准库函数通过内部调用 `pipe()` 创建了一个半双工流水线。然后它派生一个子进程，执行 Bourne shell，并在 shell 中执行参数 "command"。数据流的方向由第二个参数 "type" 决定。它可以是 "r" 或 "w"，不能二者兼得！在 Linux 下，管道将按照 "type" 参数第一个字符指定的模式打开。因此，如果你尝试传递 "rw"，它将只会以 "read" 模式打开它。

虽然这个库已经为你处理了大量的脏活工作，使用 `popen()` 创建的管道必须用 `pclose()` 关闭。到这里，你已经意识到 `popen`/`close` 与标准文件流 I/O 函数 `popen()` 和 `fclose()` 具有惊人的相似之处。

#### 库函数：`pclose()`

**原型定义**：`int pclose(FILE *stream);`

**返回值**：
*   `wait4(id)` 用的退出状态
*   如果 "stream" 无效或 `wait4(id)` 失败，则返回 `-1`

**备注**：等待管道进程终止，然后关闭流。

`pclose()` 函数对由 `popen()` 形成的进程执行 `wait4()`。当它返回时，它会销毁管道和文件流。再次，它与正常基于流的 I/O 中的 `fclose()` 是同词。

考虑这个示例，它打开了一个到 `sort` 命令的管道，并对字符串数组进行排序：

```text
********************************************************************************
《Linux 程序员指南 - 第 6 章》节选
(C)opyright 1994-1995, Scott Burkett
********************************************************************************
```

```c
模块：popen.c

********************************************************************************

#include <stdio.h>

#define MAXSTRS 5

int main(void) {

    int cntr;

    FILE *pipe_fp;

    char *strings[MAXSTRS] = {"echo", "bravo", "alpha",
                               "charlie", "delta"};

    /* 通过调用 popen() 创建一条流水线 */

    if ((pipe_fp = popen("sort", "w")) == NULL) {
        perror("popen");
        exit(1);
    }

    /* 处理循环 */

    for(cntr=0; cntr<MAXSTRS; cntr++) {
        fputs(strings[cntr], pipe_fp);
        fputs("\n", pipe_fp);
    }

    /* 关闭管道 */

    pclose(pipe_fp);

    return(0);

}
```

由于 `popen()` 使用 shell 来执行，所有的 shell 扩展字符和元字符都可以可用！此外，重定向和输出管道等高级技术可以使用 `popen()`。考虑以下示例调用：

```c
popen("ls -b", "r");

popen("sort > /tmp/foo", "w");

popen("sort | more", "w");
```

作为 `popen()` 的另一个示例，考虑这个小程序，它打开了两个管道（一个指向 shell，另一个指向 sort）：

```text
********************************************************************************
《Linux 程序员指南 - 第 6 章》节选
(C)opyright 1994-1995, Scott Burkett
********************************************************************************
```

```c
模块：popen2.c

********************************************************************************

#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    FILE *pipe_fp, *infile;
    char readbuf[80];

    if (argc != 3) {
        fprintf(stderr, "USAGE: popen3 [command] [filename]\n");
        exit(1);
    }

    /* 打开输入文件 */
    if ((infile = popen(argv[2], "rt")) == NULL) {
        perror("fopen");
        exit(1);
    }
```
