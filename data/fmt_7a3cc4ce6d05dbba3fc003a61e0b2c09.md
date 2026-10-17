
#include <termios.h>

#include <unistd.h>

/* 

列表 62-3：切换终端到 cbreak 和 raw 模式

*/

/* 

将 `fd` 指的终端设置为 cbreak 模式（非规范模式且关闭回显）。此函数假设终端当前处于 cooked 模式。如果 `prevTermios` 为 `NULL`，则使用它指向的缓冲区作为之前的设置。

*/

int `ttySetBreak`(int `fd`, struct `termios` *`prevTermios`) {

    struct `termios` `t`;

    if (`tcgetattr`(`fd`, &`t`) == -1)

        return -1;

    if (`prevTermios` != `NULL`)

        *`prevTermios` = `t`;

    `t.c_lflag` &= ~(ICANON | ECHO);

    `t.c_lflag` |= ISIGN;

    `t.c_iflag` &= ~ICNL;

    `t.c_cc`[VMIN] = 1;

    `t.c_cc`[VTIME] = 0;

    if (`tcsetattr`(`fd`, TCSAUSH, &`t`) == -1) 

/* 

将 `fd` 指的终端设置为 raw 模式（非规范模式且关闭所有输入和处理）。成功返回 0，错误返回 -1。`prevTermios` 为非 `NULL`，使用它指向的缓冲区作为之前的设置。

*/

int `ttyRaw`(int `fd`, struct `termios` *`prevTermios`) {

    struct `termios` `t`;

    if (`tcgetattr`(`fd`, &`t`) == -1)

        return -1;

    if (`prevTermios` != `NULL`)

        *`prevTermios` = `t`;

    `t.c_lflag` &= ~(ICANON | ISIG | IEXTEN | ECHO);

    `t.c_iflag` &= ~(BRKINT | ICNL | IBRK | IGNCR | INLCR | INPCK | ISTRIP | IXON | PARMRK);

    `t.c_oflag` &= ~OPOST;

    `t.c_cc`[VMIN] = 1;

    `t.c_cc`[VTIME] = 0;

    if (`tcsetattr`(`fd`, TCSAUSH, &`t`) == -1)

        return -1;

    return 0;

}

```

`tty/tty_functions.c`

一个以 raw 或 cbreak 模式编写终端的程序必须在终止时小心地将终端返回到可用模式。除其他任务外，它涉及处理所有可能发送给程序的信号，以便

程序不会过早终止。（在 cbreak 模式下，仍然可以从键盘产生作业控制信号。）

列表 62-4 提供了一个如何操作的示例。该程序执行了以下步骤：

- 根据是否提供了命令行参数（任意字符串）⑨，将终端设置为 cbreak 模式 ③ 或原始模式（raw mode） ④。之前的设置保存在全局变量 `userTermios` ⑮ 中。
- 如果终端被置于断点模式（break mode），则可以从终端产生信号。这些信号需要被处理，以确保在终止或挂起程序时，终端保持在用户预期的状态。程序为 `SIGQUIT` 和 `SIGINT` 安装了相同的处理器程序 ⑱。`SIGTSTP` 需要特殊处理，因此为它安装了不同的处理器 ⑒。
- 为 `SIGTERM` 安装处理器程序，以便捕获 `kill` 命令发送的默认信号 ⑓。
- 执行一个循环，从 `stdin` 逐个读取字符并将其回显到标准输出 ⑔。程序在输出字符之前对输入字符进行特殊处理 ⑕：
    - 所有字母在输出前都会转换为小写。
    - 换行符（`\n`）和回车符（`\r`）原样回显。
    - 除换行和回车以外的控制字符以双字符序列的形式回显：脱字符 (`^`)加上对应的大写字母（例如，Control-A 显示为 `^A`）。
    - 所有字符都以星号 (`*`) 回显。
    - 字母 `q` 会导致循环终止⑙
- 退出循环时，将终端恢复到用户上次设置的状态，然后终止 ⑱。

程序为 `SIGQUIT`、`SIGINT` 和 `SIGTERM` 安装了相同的处理器程序。该处理器程序将终端恢复到用户上次设置的状态并终止程序 ⑒。
`SIGTSTP` 信号的处理器程序 ⑓ 按照第 34.7.3 节描述的方式处理信号。注意该处理器程序操作的以下额外细节：

- 进入时，处理器程序保存当前的终端设置（在 `ourTermios` 中） ➐，并将终端重置为程序启动时生效的设置（保存在 `userTermios` 中） ⑤，在实际停止进程之前再次抛出 `SIGTSTP`。
- 在收到 `SIGCONT` 恢复执行后，处理器程序再次将当前终端设置保存到 `userTermios` 中 ➖，因为用户在程序停止期间可能更改了设置（例如，使用 `stty` 命令）。处理器程序将终端恢复到程序所需的状态（`ourTermios`） ➗。

## 列表 62-4: 演示 cbreak 模式和原始模式

```c
① static struct termios; /* 用户定义的终端设置 */

+ ② static void handler(int sig) /* 通用处理器：恢复 tty 设置并退出 */
{
    if (tcsetattr(STDIN_FILENO, TCSAFLUSH, &ourTermios) == -1)
        errExit("tcsetattr");
    _exit(EXIT_SUCCESS);
}

+ ③ tstpHandler(int sig) /* 用于 SIGTSTP 的处理器 */
{
    struct termios ourTermios; /* 用于保存我们的 tty 设置 */
    sigset_t tstmask, prevMask;
    struct sigaction sa;
    int savedErrno;
    savedErrno = errno; /* 我们在这里可能会更改 'errno' */
    /* 保存当前终端设置，恢复到
    程序启动时的状态 */
    if (tcgetattr(STDIN_FILENO, &ourTermios) == -1)
        errExit("tcgetattr");
    if (tcsetattr(STDIN_FILENO, TCSAFLUSH, &ourTermios) == -1)
        errExit("tcsetattr");
    /* 将 SIGSTP 的位置设置为默认值，再次抛出信号，
    然后解锁以便我们真正停止 */
    if (signal(SIGSTP, SIG_DFL) == SIG_ERR)
        errExit("signal");
    raise(SIGSTP);
    sigemptyset(&tstmask);
    sigaddset(&tstmask, SIGSTP);
    if (sigprocmask(SIG_UNBLOCK, &tstmask, &prevMask) == -1)
        errExit("sigprocmask");
    /* 收到 SIGCONT 后在此恢复执行 */
    if (sigprocmask(SIG_SETMASK, &prevMask, NULL) == -1)
        errExit("sigprocmask");
    /* 重新阻塞 SIGSTP */
    sigemptyset(&sa.sa_mask);
    sa.sa_flags = SA_RESTART;
    sa.sa_handler = tstpHandler;
    if (sigaction(SIGTSTP, &sa, NULL) == -1)
        errExit("sigaction");
    /* 在我们停止期间，用户可能更改了终端设置；
    保存设置以便稍后恢复 */
    if (tcgetattr(STDIN_FILENO, &ourTermios) == -1)
        errExit("tcgetattr");
    /* 恢复我们的终端设置 */
    if (tcsetattr(STDIN_FILENO, TCSAUSH, &ourTermios) == -1)
        errExit("tcsetattr");
errno = savedErrno;
int main(int argc, char *argv[]) {
    char ch;
    struct sigaction sa, prev;
    ssize_t n;
    sigemptyset(&sa.sa_mask);
