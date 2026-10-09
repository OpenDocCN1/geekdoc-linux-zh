

EC_CLEANUP_BGN
return T_ERROR;
EC_CLEANUP_END
}
static bool store_char(char *word, size_t maxword, int c, size_t *np)
{
errno = E2BIG;
if (!(*np < maxword))
{
    return false;
}
word[(*np)++] = c;
return true;
EC_CLEANUP_BGN
return false;
EC_CLEANUP_END
}

在编写大型程序时，分块调试非常方便。这不仅提供了早期反馈，还使查找错误变得更加容易，因为需要搜索的代码行数较少。这里是一个用于 `gettoken` 的测试程序：

```c
int main(void)
{
char word[200];
while (1)
switch (gettoken(word, sizeof(word))) {
case T_WORD:
printf("T_WORD <s>\n", word);
break;
case T_BAR:
printf("T_BAR\n");
break;
case T_AMP:
printf("T_AMP\n");
break;
case T_SEMI:
printf("T_SEMI\n");
break;
case T_GT:
printf("T_GT\n");
break;
case T_GGT:
printf("T_GGT\n");
break;
case T_LT:
printf("T_LT\n");
break;
case T_NL:
printf("T_NL\n");
break;
case T_EOF:
printf("T_EOF\n");
exit(EXIT_SUCCESS);
case T_ERROR:
printf("T_ERROR\n");
exit(EXIT_SUCCESS);
}
```

当我们运行这个程序并输入以下行（后跟 EOT）：

```
$ sort <inf | pr -h "Sept. Results" >>out&
```

我们得到了以下输出：

```
T_WORD <sort>
T_LT
T_WORD <inf>
T_BAR
T_WORD <pr>
T_WORD <-h>
T_WORD <Sept. Results>
T_GGT
T_WORD <out&>
T_AMP
T_NL
T_EOF
```

这个测试并没有证明 `gettoken` 是正确的，但它足以鼓励我们继续处理 shell 的其余部分。

下一步是编写一个函数来处理简单命令，该命令由 `|`、`&`、`;` 或换行符终止。我们将把这个函数称为 `command`。参数只是被输入到一个 `argv` 数组中，以便稍后在调用 `execvp` 时使用。标准输入有三种可能性：默认值（`STDIN_FILENO`）、文件（如果存在 `<`），或管道的读取端（如果该简单命令前由 `|` 引导）。标准输出有四种可能性：默认值（`STDOUT_FILENO`）、要创建或截断的文件（如果存在 `>`）、要创建或追加的文件（如果存在 `>>`），或管道的写入端（如果该简单命令后跟随 `|`）。从 `gettoken` 接收的标记告诉我们是哪种情况成立。

当 `command` 处理标记时，它使用这些变量来记录简单命令的标准输入和输出情况：

- `srcfd`：源文件描述符，初始值为 `STDIN_FILENO`。如果输入通过 `<` 重定向，`srcfd` 被设置为 `-1`，并且 `srcfile` 记录文件名。如果输入是管道，`srcfd` 将设置为其他非 `STDIN_FILENO` 的文件描述符号码。
- `srcfile`：源文件，仅当简单命令包含 `<` 时使用。
- `dstfd`：目标文件描述符，初始值为 `STDOUT_FILENO`。如果输出通过 `>` 或 `>>` 重定向，则被设置为 `-1`，并且 `dstfile` 记录文件名。与 `srcfd` 类似，如果输出是管道，它被设置为非 `STDOUT_FILENO` 的文件描述符。
- `dstfile`：输出文件，仅当简单命令包含 `>` 或 `>>` 时使用。
- `append`：这个布尔变量仅在输出通过 `>>` 重定向时设置为 `true`。
- `makepipe`：这是 `command` 的一个参数。如果为 `true`，调用者要求 `command` 创建管道，将读取端用作其标准输入，并将写入端的文件描述符传回给调用者，调用者将其用作其标准输出。这一机制将在稍后解释。

在遍历标记时，`command` 还检查逻辑错误：`<` 或 `>` 出现两次、当简单命令以 `|` 终止时出现 `>`、当简单命令前由 `|` 引导时出现 `<` 等。有趣的是，典型的 UNIX shell 并不检查其中的一些异常情况：你实际上可以运行如下的命令行：
$ who >outf | wc

函数 `command` 返回终止管道的那个标记，因为终止符的类型会影响后续处理：如果终止符是 `&`，最右边的简单命令不会被等待，并且管道中的所有简单命令都会在忽略中断和退出信号的情况下运行。如果最右边的简单命令需要被等待，其进程 ID 也必须通过参数 `wpid` 返回。如果终止符是换行符，则会提示用户输入新命令。

关于 `command` 最微妙的地方在于，当简单命令后跟随 `|` 时，它会递归调用自身。递归调用一直持续，直到遇到其他终止符（`;`、`&` 或换行符）之一。每个递归调用负责实际创建管道（使用 `pipe` 系统调用），因此其参数 `makepipe` 被设置为 `true`。写入端管道的文件描述符通过另一个参数 `pipefdp` 传回。只有在递归调用返回后，简单命令才会实际被调用（使用函数 `invoke`），因为在管道的写入端可用之前无法调用它。此外，如上所述，在调用任何组成简单命令之前，必须知道管道终止符，以便 `invoke` 知道如何处理信号。因此，管道从左到右处理，但简单命令从右到左调用。对于最左边的简单命令有一次调用 `command`，此时 `makepipe` 设置为 `false`；然后对于每个额外的简单命令，再进行一次 `makepipe` 设置为 `true` 的递归调用。当 `command` 调用的栈返回时，简单命令被调用——此时所有需要的信息都已可用。

以下是 `command` 的代码。值得仔细研究。

```c
#define MAXARG  50      /* max args in command */
#define MAXFNAME  500    /* max chars in file name */
#define MAXWORD  500     /* max chars in arg */

static TOKEN command(pid_t *wpid, bool makepipe, int *pipefdp)
{
    TOKEN token, term;
    int argc, srcfd, dstfd, pid, pfd[2] = {-1, -1};
    char *argv[MAXARG], srcfile[MAXFNAME] = "", dstfile[MAXFNAME] = "";
    char word[MAXWORD];
    bool append;

    argc = 0;
    srcfd = STDIN_FILENO;
    dstfd = STDOUT_FILENO;
    while (true) {
        switch (token = gettoken(word, sizeof(word))) {
        case T_WORD:
            if (argc >= MAXARG - 1) {
                fprintf(stderr, "Too many args\n");
                continue;
            }

            if ((argv[argc] = malloc(strlen(word) + 1)) == NULL) {
                fprintf(stderr, "Out of arg memory\n");
                continue;
            }
            strcpy(argv[argc], word);
            argc++;
            continue;
        case T_LT:
            if (makepipe) {
                fprintf(stderr, "Extra <\n");
                break;
            }
            if (gettoken(srcfile, sizeof(srcfile)) != T_WORD) {
                fprintf(stderr, "Illegal <\n");
                break;
            }
            srcfd = -1;
            continue;
        case T_GT:
        case T_GGT:
            if (dstfd != STDOUT_FILENO) {
                fprintf(stderr, "Extra > or >>\n");
                break;
            }
            if (gettoken(dstfile, sizeof(dstfile)) != T_WORD) {
                fprintf(stderr, "Illegal > or >>\n");
                break;
            }
            dstfd = -1;
            append = token == T_GGT;
            continue;
        case T_BAR:
        case T_AMP:
        case T_SEMI:
        case T_NL:
            argv[argc] = NULL;
            if (token == T_BAR) {
                if (dstfd != STDOUT_FILENO) {
                    fprintf(stderr, "> or >> conflicts with |\n");
                    break;
                }
                term = command(wpfd, true, &dstfd);
                if (term == T_ERROR)
                    return T_ERROR;
            }
            else
                term = token;
            if (makepipe) {
                ec_negl(pipe(pfd));
                *pipefdp = pfd[1];
                srcfd = pfd[0];
            }
            ec_negl(pid = invoke(argc, argv, srcfd, srcfile, dstfd,
                dstfile, append, term == T_AMP, pfd[1]));
            if (token != T_BAR)
                *wpid = pid;
            if (argc == 0 && (token != T_NL || srcfd > 1))
                fprintf(stderr, "Missing command\n");
            while (--argc >= 0)
                free(argv[argc]);
            return term;
        case T_EOF:
            exit(EXIT_SUCCESS);
        case T_ERROR:
            return T_ERROR;
        }
    }
    EC_CLEANUP_BGN
    return T_ERROR;
    EC_CLEANUP_END
}
```

一旦 `command` 遇到标记 `T_BAR` 并感知到需要管道，为什么它要求下一次调用 `command` 来创建管道，而不是自己创建然后仅仅传递读取文件描述符？这是为了节省文件描述符。如果在递归调用 `command` 之前而不是之后调用 `pipe` 系统调用，每个递归级别——每个简单命令——都会占用两个管道文件描述符，这些描述符在递归调用返回之前无法关闭。由于在某些系统中文件描述符资源紧缺，管道将被限制为比该数量少一半左右的简单命令。通过让读取端创建管道，我们可以在调用 `invoke` 之前（我们将很快涉及到）调用 `pipe`，如果我们的调用者要求我们创建管道，从而允许管道具有任意长度。

`invoke` 将创建的子进程不需要管道的写入端（`pfd[1]`），因此它作为最后一个参数传递给 `invoke`，以便在子进程中关闭；我们将稍后看到这一点。

以下是创建第一次对 `command` 调用的主程序。它是基于第 5.4 节中单次 shell 的主程序构建的。

```c
int main(void)
{
    pid_t pid;
    TOKEN term = T_NL;

    ignore_sig();
    while (true) {
        if (term == T_NL)
            printf("%s", PROMPT);
        term = command(&pid, false, NULL);
    }
}
```

