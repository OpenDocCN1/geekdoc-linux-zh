

+   1 从标准输入显示 P-1 行（保留最后一行用于提示）
+   2 在行后显示 [more?] 消息。
+   3 等待输入 Enter、Space 或 'q'
+   4 如果输入为 Enter，则推进一行；转到 2
+   5 如果输入为 Space，则转到 1
+   6 如果输入为 'q'，则退出。

我们还必须在此基础上增加从命令行提取文件名的能力，如果存在的话。清单 1.4 包含一个 C 主程序，用于实现一个基于上述逻辑的 more 版本，该版本还会检查是否存在一个或多个命令行参数，如果存在，则使用参数作为要打开的文件名，而不是标准输入。如果没有命令行参数，则使用标准输入。我们现在假设 P=24。

## 清单 1.4：more 主程序的第一个版本。

```
#include <stdio.h>
#define SCREEN_ROWS    23 /* assume 24 lines per screen */
#define LINELEN        512
#define SPACEBAR       1
#define RETURN         2
#define QUIT           3
#define INVALID        4

/** do_more_of()
 * Given a FILE* argument fp, display up to a page of the
 * file fp, and then display a prompt and wait for user input.
 * If user inputs SPACEBAR, display next page.
 * If user inputs RETURN, display one more line.
 * If user inputs QUIT, terminate program.
 */
void do_more_of(FILE *filep);

/** get_user_input()
 * Displays more's status and prompt and waits for user response,
 * Requires that user press return key to receive input
 * Returns one of SPACEBAR, RETURN, or QUIT on valid keypresses
 * and INVALID for invalid keypresses.
 */
int get_user_input();

int main(int argc, char *argv[])
{
    FILE    *fp;
    int     i = 0;
    if (1 == argc)
        do_more_of(stdin);  // no args, read from standard input
    else
        while (++i < argc) {
            fp = fopen(argv[i], "r");
```

```
if ( NULL != fp ) {
    do_more_of( fp );
    fclose( fp );
}
else
    printf ( "Skipping %s\n", argv[i] );
}
return 0;
}
```

如果你不熟悉本程序中使用的某些 C 函数（也在 C++ 中使用），那么请阅读相关资料，要么在手册页中，要么在任何入门 C/C++ 教科书中。特别是你需要了解以下函数和类型，它们都是 ANSI 标准 C 的一部分，并在 <stdio.h> 中定义：

| FILE | 一个文件流 |
| fopen | 打开一个文件并返回一个 FILE* |
| fclose | 关闭一个 FILE 流 |
| fgets | 从 FILE 流中读取一个字符串 |
| fputs | 向 FILE 流中写入一个字符串 |

在上面的代码中需要注意的一点是，它检查 fopen() 函数的返回值是否为 NULL。每次程序调用库函数或系统函数时，都应检查可能的错误条件。未能做到这一点的程序将是一个让用户沮丧的程序。

如果 main 程序签名中的参数列表对你来说也是新的，这里有一个简要说明。在签名

```
int main( int argc , char *argv[] )
```

中，argc 是一个整数参数，指定命令行上的单词数。由于程序名本身就是一个单词，因此 argc 始终至少为 1。如果它正好为 1，则没有命令行参数。第二个参数 argv 是一个字符指针数组。在 C 中，字符指针是指向以 NULL 结尾的字符串的指针，即最后一个字符为 '\0' 的字符串。数组 argv 是一个数组，其字符串是命令行上的单词。argv[0] 是程序名本身，argv[1] 是第一个命令参数，以此类推。参数的名称是任意的。无论 argc 被命名为 rosebud、numargs 还是 ac，它都能工作。shell 负责将命令参数放入第一个和第二个参数预期的内存位置中（它通过进行系统调用并将这些参数传递给调用来实现这一点）。

清单 1.4 未包含 main() 使用的两个函数的定义：do_more_of() 和 get_user_input()，它们包含在清单 1.5 中。其中第一个很容易推断出来，除了你可能以前没有使用过 fgets() 和 fputs()。该函数在变量 num_of_lines 中跟踪可以在屏幕填满之前写入屏幕的行数，该变量初始为 23。第二个函数也相当直接。唯一可能需要解释的部分是 printf() 指令。

