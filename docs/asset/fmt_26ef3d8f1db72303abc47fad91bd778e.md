
`be_dc(todc, fromdc);`

`wait(NULL);` /* 等待子进程 */

}

}

`void be_dc(int in[2], int out[2])` {

/*

设置 stdin 和 stdout，然后 execcl dc

*/

/* 从管道设置 stdin */

if ( `dup2(in[0],0)` == -1 ) /* 将读端复制到 0 * */
    `oops("dc: cannot redirect stdin",3);`
`close(in[0]);` /* 移动到 fd 0 */
`close(in[1]);` /* 不在此处写入 */

```c
    /* 设置 stdout 到管道out */
    if ( dup2(out[1], 1) == -1 )      /* 将写端复制到 1 */
        oops("dc: cannot redirect stdout",4);
    close(out[1]);                          /* 移动到 fd 1 */
close(out[0]);                          /* 不在此处读取 */
```

```c
be_bc(int todc[2], int fmdc[2])
```

```c
/*
    从 stdin 读取并转换为逆波兰表达式 (RPN)，发送管道
    然后从另一个管道读取并打印给用户
    使用 fdopen() 将文件描述符转换为流
*/
```

```c
{
    int    num1, num2;
    char   operation[BUFSIZ], message[BUFSIZ], *fgets;
    FILE   *fput, *fpin, *fdopen();
```

```c
    /* 设置 */
    close(toc[0]);                          /* 不从管道读取到 dc * */
    close(fmdc[1]);                          /* 不向 dc 写入管道 * */
```

```c
    fput = fdopen(toc[1], "w" );          /* 管道转换为流 * */
    fpin = fdopen(fmdc[0], "r" );          /* 描述符转换为流 * */
    if (fput == NULL || fpin == NULL)
        fatal("Error converting pipes to streams");
```

```c
        /* 解析输入 */
        if ( scanf(message, "%d%+]*%d", &num1, operation,
            &num2)!=3) {
```

```c
            printf("syntax error\n");
            continue;
        }
```

```c
            fflush(fput);
            if (fgets(message, BUFSIZ, fpin) == NULL )
                break;
            printf("%d %c %d = %s", num1, operation, num2, message);
```

```c
    } fclose(fput);                          /* 关闭管道 * */
```

```c
```c

fclose(fpin);      /* dc 将看到 EOF */

}

fatal(char mess[])

{

    fprintf(stderr, "Error: %s\n", mess);

    exit(1);

}

```

这里我们介绍 tinybc 的运行：

```bash
$ cc tinybc.c -o tinybc ; ./tinybc
tinybc: 2+2
2 + 2 = 4
tinybc: 5^5
5 ^ 5 =312475
tinybc:
```

仔细观察此输出，识别哪些部分来自程序。`tinybc` 生成提示符和算术表达式。计算结果是由 `dc` 生成的字符串；`tinybc` 只从管道读取该字符串并将其包含在输出中。

### 11.3.2 关于协程的说明

哪些 Unix 工具可以作为协程？`sort` 工具可以作为程序的协程吗？不能。`sort` 会读取所有数据直到文件结束。通过管道发送结束的唯一方法是关闭写端。一旦你关闭写端，另一端就会处理数据和命令。交互是简单且可预测的。当你要求 `dc` 打印一个值时，得到一行文本。当你告诉 `dc` 推入一个值时，没有响应。程序要成为客户端-服务器协程的一部分，必须有明确的方式指示消息的结束，并且程序必须使用简单、可预测的请求和回复。

## 3 fdopen：让文件描述符像文件

在 `tinybc` 中，我们引入了库函数 `fdopen`。`fdopen` 的工作方式类似于 `fopen`，返回一个 `FILE *`，但它接受文件描述符作为参数。使用 `fopen` 通过文件名打开内容。`fdopen` 也可以打开设备以及普通的磁盘文件。当你有一个文件描述符但没有文件名（例如管道的情况），使用 `fdopen`，这样就可以使用标准的缓冲 I/O 操作。注意 `tinybc` 如何使用 `fprintf` 和 `fgets` 通过管道获取数据。

## 11 连接远端进程：服务器和套接字

### 1.4 popen：让进程像文件

在这一节中，我们继续研究程序如何通过连接另一个进程来获取服务。我们检查 `popen` 库函数。查看 `popen` 做了以及如何工作，并编写我们的版本。

#### 1.4.1 popen 做了什么

`popen` 打开一个文件的缓冲连接：

```c
FILE *fp;                          /* 结构指针 */
fp = fopen("file", "r");      /* 参数是文件名、连接类型 */
c = getc(fp);                            /* 逐字符读取 */
gets(buf, len, fp);                       /* 按行读取 */
scanf(buf, "%d%s", &x, &y);          /* 逐标记读取 */
close(fp);                               /* 完成后关闭 */
```

`popen` 接受两个字符串参数：文件名和连接类型（例如 `"r"`, `"w"`, `"a"`）。`popen` 看起来和工作方式非常像 `fopen`。`popen` 打开到进程的缓冲连接：

```c
FILE *fp;                          /* 相同类型的结构 */
fp = fopen("ls", "r");               /* 参数是程序名、连接类型 */
gets(buf, len, fp);                       /* 完全相同的函数 */
close(fp);                               /* 完成后关闭 */
```

图 11.5 显示了 `popen` 和 `fopen` 之间的相似之处。两个函数都返回相同的语法，并且都返回相同类型的值。第一个参数是要需要打开的命令名称：可以是任何 shell 命令。第二个参数可以是 `"r"` 或 `"w"`，但永远不会是 `"a"`。

![](img/9983708330d437de319a559fa6cda7_0.png)

`popen` 示例
以下程序中，`sort` 命令是数据源，使用 `popen` 获取当前用户的排序列表：

- `popendemo.c`
  - 演示了如何为标准 i/o 打开一个程序
  - 重要要点：
    - `popen()` 返回一个 `FILE *`，就像 `fopen` 一样

## 11.4 popen：让进程像文件

```c
/*
2. 它返回的 FILE 可以使用所有标准函数进行读写
3. 完成后需要使用 pclose()
*/
#include <stdio.h>
#include <stdlib.h>
int main()
{
    FILE *fp;
    char buf[100];
    int i = 0;
    fp = popen("who|sort", "r"); /* 打开命令 *
    while (fgets(buf, 100, fp) != NULL) { /* 从命令读取 */
