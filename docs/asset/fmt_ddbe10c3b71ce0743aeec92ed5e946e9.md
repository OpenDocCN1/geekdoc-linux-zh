
`close(fd[1]);`

示例 7.5 中的父进程将标准输出重定向到第二个管道（它原本来自第一个管道）。子进程将标准输入重定向自第二个管道，而不是第一个管道。图 7.5–7.8 展示了这种连接机制。

# 图 7.5. 执行第二次 `pipe(fd)` 调用后，示例 7.5 中父进程的连接。

![](img/74e4d4cf6f07ca029fcde95b6b423fe7_281_0.png)

图 7.5 显示了父进程 A 创建新管道后的文件描述符表。
图 7.6 显示了进程 A `fork` 出子进程 B 后的情况。此时，第二次 `pipe` 调用之后的任何 `dup2` 函数尚未执行。

# 图 7.6. fork 后示例 7.5 中进程的连接。进程 A 是父进程，进程 B 是子进程。

![](img/74e4d4cf6f07ca029fcde95b6b423fe7_282_0.png)

图 7.7 显示了父进程和子进程各执行完最后一个 `dup2` 后的情况。
进程 A 已重定向其标准输出以写入管道 b，进程 B 已重定向其标准输入从管道 b 读取。最后，图 7.8 显示了所有不必要的描述符已关闭并形成双进程环后的文件描述符状态。

**图 7.7. 执行 `if` 语句后示例 7.5 中进程的连接。进程 A 是父进程，进程 B 是子进程。**

![](img/74e4d4cf6f07ca029fcde95b6b423fe7_283_0.png)

图 7.8. 整个代码段执行后示例 7.5 中进程的连接。进程 A 是父进程，进程 B 是子进程。

| 进程 A | 文件描述符表 |
| :--- | :--- |
| [0] | 管道读 |
| [1] | 管道 b 写 |
| [2] | 标准错误 |

| 进程 B | 文件描述符表 |
| :--- | :--- |
| [0] | 管道 b 读 |
| [1] | 管道 a 写 |
| [2] | 标准错误 |

## 练习 7.6

如果在练习 7.5 之后插入练习 7.2 的代码会发生什么？

### 答案：

新代码由两个进程执行。每个进程向管道写入 10 个整数并读取另一个进程写入的整数。进程无法运行太远，因为每个进程在写入下一个值之前需要从另一个进程读取。你会看到 0 的行，等。

示例 7.5 的代码可以很容易扩展到任意大小。值 `n` 通过命令行传递并转换为变量 `ncs`。注意，程序需要一个大小为 `n` 的数组来持有描述符。在创建双进程环后，父进程退出并再次 `fork`（尝试写入你自己的代码）。

# 程序 7.1 ring.c

一个创建双进程环的程序。

```c
#include <errno.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
int main(int argc, char *argv[]) {
    /* 表示进程应该产生另一个 */
    pid_t childpid;      /* dup2 调用的返回值 */
    int error;
    int fd[2];            /* pipe 返回的文件描述符 */
    int i;                /* 从 1 开始的进程数 */
    int nprocs;           /*环中的总进程数 */
    /* 检查命令行有效进程数 */
    if (argc != 2 || (nprocs = atoi(argv[1])) <= 0) {
        fprintf(stderr, "Usage: %s\n", argv[0]);
        return 1;
    }
    if (pipe(fd) == -1) { /* 通过管道连接 stdin 到 stdout */
        perror("Failed to create pipe");
        return 1;
    }
    if (dup2(fd[0], STDIN_FILENO) == -1 ||
        dup2(fd[1], STDOUT_FILENO) == -1) { /* 连接管道 */
        perror("Failed to connect pipe");
        return 1;
    }
    if ((close(fd[0]) == -1 || (close(fd[1])) == -1)) {
        perror("Failed to create extra descriptors");
        return 1;
    }
    for (i = 1; i < nprocs; i++) { /* 创建剩余的进程 */
        if (pipe(fd) == -1) {
            fprintf(stderr, "[%ld]: failed to create pipe: %s\n",
                (long)getpid(), i, strerror(errno));
            return 1;
        }
        if ((childpid = fork()) == -1) {
            fprintf(stderr, "[%ld]: failed to create child %d: %s\n",
                (long)getpid(), i, strerror(errno));
            return 1;
        }
        if (childpid > 0) { /* 父进程，重分配 stdout */
            error = dup2(fd[1], STDOUT_FILENO);
        } else /* 子进程，重分配 stdin */
            error = dup2(fd[0], STDIN_FILENO);
        if (error == -1) {
            fprintf(stderr, "[%ld]: failed to dup pipes for iteration %d: %s\n",
                (long)getpid(), i, strerror(errno));
            return 1;
        }
        if ((close(fd[0]) == -1 || (close(fd[1])) == -1)) {
            fprintf(stderr, "[%ld]: failed to create extra descriptors %d: %s\n",
                (long)getpid(), i, strerror(errno));
            return 1;
        }
        if (childpid)
            break;
    }
    /** 向世界问好 */
    fprintf(stderr, "This process is %d with ID %ld and parent id %ld\n",
        i, (long)getpid(), (long)getppid());
    return 0;
}
```

### 7.3 环探索

以下练习测试并修改程序 7.1。你可以通过编译 `ring` 代码或使用 `fork-pipe` 模拟器来尝试这些。网页上会出现模拟器的链接。对于每次修改，我们都会创建程序的副本。新可执行文件的建议名称在括号中。

- 1. 运行程序 7.1 中的程序 (`ring`)。
- 2. 创建一个包含编译和 `lint` 程序描述的 `Makefile`。使用 `make` 编译程序。为该项目的其他部分添加目标。（如果不熟悉 `make` 工具，请参考 A.3 节）。
- 3. 进行任何修正以消除所有反映程序问题的错误和警告消息。（如果不熟悉 `lint` 工具，请参考 A.4 节）。
- 4. 使用多个命令行参数运行 `ring`，并观察环中进程数量从 1 到 20 变化时发生了什么。
- 5. 在最后的 `printf (ring)` 之前加上一个 `wait` 调用来修改原始 `ring`。这如何影响程序的输出？
- 6. 在最后的 `printf (ring2)` 之后加上一个 `wait` 调用来修改原始 `ring`。这如何影响程序的输出？

这只是浪费了一些 CPU 时间。变量 `dummy` 被声明为 `volatile`，以确保 `for` 循环的操作不被优化。使用 `ptrstr` 将字符串输出到标准错误。将 `ptrstr` 使用的 `n` 的值作为可选命令行参数传递给 `ring3`。使用 `0` 作为该参数的默认值。（一次处理一个字符可以让环进程有更多机会在输出时与变量 `n` 进行交替执行，这可能会在字符输出之间产生微小但几乎难以察觉的延迟。）

- 8. 如果执行以下操作，对比修改后的 `ring3` 的结果：
  - 在调用 `ptrstr` 之前插入 `wait`（`ring4`）。
  - 在调用 `ptrstr` 之后插入 `wait`（`ring5`）。
- 9. 按照如下方式修改 `ring1`（`ringtopology`）。
  - 在 `wait` 之前，每个进程分配一个包含 `nprocs` 个元素的数组，用于存储环形上所有进程的 ID。该进程将自己的 ID 放在数组的元素零中，并将变量 `next_ID` 设置为自己的进程 ID。
  - 对 `k` 从 `1` 到 `nprocs-1` 执行以下操作：
    - 将 `next_ID` 输出到标准输出。
    - 从标准输入读取 `next_ID`。
    - 将 `next_ID` 插入到 ID 数组的位置 `k`。
  - 将 `wait` 之后的 `fprintf` 替换为循环，以可读的行格式将 ID 数组的内容到标准标准。此输出测试了环的连通性，因为 ID 数组包含了从给定进程开始出现的进程顺序。
- 10. 通过让子进程而非父进程跳出循环来修改 `ringtopology`（`childbreak`）。我们现在正在进程而不是链。确定这如何影响拓扑。我们仍然拥有环吗？如果使用模拟器，如果你不需要向环发送任何内容来确定拓扑，你可以直接修改 `ring`。
- 11. 通过让两个进程都不跳出循环来修改 `ringtopology`（`ringbreak`）。我们现在正在创建一个进程树而不是链。确定这如何影响拓扑。我们仍然拥有环吗？进程的数量大于 `nprocs`。进程的数量如何依赖 `nprocs`？你将需要调整绕环发送进程 ID 的循环。
- 12. 修改 `ring1` 为双向环（信息可以在环上的相邻节点之间以任一方向流动）。标准输入和输出用于一个方向的流动。文件描述符 3 和 4 用于另一个方向的流动。通过累积每个方向的 ID 数组来测试连接（`biring`）。
- 修改 `ring1` 以创建进程的双向环面。累积 ID 数组以测试连通性。环面具有二维结构。它类似于网格结构，但末尾的进程是连接在一起的。$n^2$ 个进程在每个维度上排列成 $n$ 个环（环面）。每个进程有四个连接（北、南、东、西）。

使用书籍网站上链接的环模拟器来探索此问题的各个方面。修改环模拟器示例以阐明第 4 到第 6 项的效果。将打印设为原子性以说明第 7 项和第 8 项。像第 9 项那样在环上传递数据，并为第 10 项构建一个双向环。

### 7.4 简单通信

第 7.2 节建立了进程环的连接。本节开发了一个简单的应用程序，其中进程在环上生成一个斐波那契数序列。斐波那契序列中的下一个数是序列中两个数字之和。

在这个项目中，进程以字符字符串格式传递信息。原始父进程向标准输出输出代表前两个数字的字符串 `"1 1"`，并将该字符串发送给下一个进程。其他进程从标准输入读取字符串，解码字符串，计算下一个斐波那契数，并写入标准输出，以表示前一个斐波那契数和刚刚计算出的那个。每个进程然后将其计算结果字符串写入标准错误并退出。原始父进程在接收字符串并显示数字后退出。

从程序 7.1 的原始环函数开始，替换 `fprintf` 代码，以下面描述的字符串格式从父进程读取两个整数，计算斐波那契序列中的下一个整数，并将结果写入标准输出。

- 1. 每个字符串都是由单个空格分隔的两个整数的 ASCII 表示。
- 2. 原始父进程写入字符串 `"1 1"` 代表两个 1，然后读取一个字符串。确保发送字符串终止符。
- 3. 所有其他进程读取字符串并写入一个字符串。
- 4. 斐波那契数满足公式 $x_{n+1} = x_n + x_{n-1}$。每个进程接收两个数字（例如 a 后接 b），计算 `c = a + b` 并将 `b` 后接 `c` 写入一个空终止的字符串。`b` 和 `c` 值应以单个空格分隔的字符串形式写入。
- 5. 向标准输出发送消息后，进程以以下格式向标准错误写入单行消息。

```
Process i with PID x and parent PID y received a b and sent c.
```
