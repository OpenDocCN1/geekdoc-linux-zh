
```c
/* tmpnam2.c */
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <errno.h>

int main(int argc, char *argv[]) {
    char pathname[256];
    FILE *tmp;

    /* 临时路径 */
    if (!(tmp = tmpnam(pathname))) {
        fprintf(stderr, "%s\n", strerror(errno));
        abort();
    }
    /* 临时文件 */
    printf("Using temp file: %s\n", pathname);
}
```

![](img/84b5d55e12f9f19712b0bb181eee905f_174_0.png)

# 高级 UNIX 编程

接上页

```c
11: int
12: main(int argc,char *argv[]) {
13:     char tf_path[64];    /* 临时文件路径 */
14:     int tfd = -1;         /* 文件描述符 */
15:     FILE *tmp = 0;       /* 打开的临时 FILE */
16:
17:     /*
18:     * 初始化临时文件模板：

19:     */
20:     strcpy(tf_path,"/var/tmp/tmp.XXXXX");
21:
22:     /*
23:     * 生成临时文件名，创建并打开
24:     * 在文件 tfd 上的临时文件
25:     */
26:     if ((tfd = mkstemp(tf_path)) < 0) {
27:         fprintf(stderr,"%s: 生成临时文件名。\n",
28:             return(errno);
29:         abort());
30:     }
31:
32:     printf("Using temp file: %s\n",tf_path);
33:
34:     /*
35:     * 在临时文件上使用标准 I/O：
36:     */
37:     
38:     tmpf = fdopen(tfd,"+w");
39:     printf("Written by PID=%ld\n",(long)getpid());
40:     close(tmpf);
41:
42:     unlink(tf_path);      /* 释放临时文件 */
43:
44:     return 0;
45: }
```

列表 8.3 中的程序在第 20 行初始化模板，并在第 26 行创建并打开了临时文件，其中调用了 `mkstemp(3)`。为了允许使用标准 I/O 程，在第 37 行调用了函数 `fdopen(3)` 并传入文件描述符 `tfd`。在第 38 行使用 `printf(3)` 对临时文件进行写入。

在 FreeBSD 下使用以下结果编译并运行该程序：

```
$ make mkstemp
cc -c -D_POSIX_C_SOURCE=19939L -D_POSIX_SOURCE -Wall mkstemp.c
cc mkstemp.o -o mkstemp
./mkstemp
Using temp file: /var/tmp/tmp.m4798
```

本次运行生成并使用的临时文件是 `/var/tmp/tmp.m4798`，这与程序第 20 行中使用的模板一致。

列表 8.3 中的程序使用了临时文件名，如下所示：

```c
strcpy(tf_path,"/var/tmp/tmp.XXXXX");
```

## 第 8 章 • 临时文件与进程清理

Xs 之前的字符可以被修改，以允许在程序中使用多个临时文件。例如，第一个和第二个临时文件可以使用以下模板代替：

```c
strcpy(template01,/var/tmp/01-XXXXX");
strcpy(template02,/var/tmp/02-XXXXX");
```

这种技术对于使用多个临时文件并非绝对必要，但在调试程序时会很有帮助。当你看到 `/var/tmp` 目录下以这种方式命名的临时文件时，你就会知道以 `01-` 开头的临时文件是你创建的第一个临时文件，而 `02-` 表示第二个。

### 使用 mkstemp(3) 函数

FreeBSD 支持 `mkstemp(3)` 函数，它允许在临时文件末尾添加后缀。在其他所有方面，它与 `mkstemp(3)` 相似。它的原型如下：

```c
#include <unistd.h>
```

```c
int mkstemp(char *template, int suffixlen);
```

`template` 参数与 `mkstemp(3)` 的参数相同，不同之处 `X` 字符不再需要位于字符串的末尾。参数 `suffixlen` 表示字符串末尾有多少个字符代表后缀。以下代码说明：

```c
char template[256];          /* 存放模板的缓冲区 */
int tmpf;                               /* 打开的临时文件描述符 */
```

```c
strcpy(template,/var/tmp/XXXX.tmp");
tmpf = mkstemp(template,4);           /* 创建并打开临时文件 */
```

在此示例中，最后四个字符格式化为后缀。`X` 字符现在可以位于临时文件基础名的开头或中间。

> 警告
>
> 函数 `mkstemp(3)` 并非到处可用。出于这个原因，不建议将其用于移植性代码。

### 使用 tmpfile(3) 函数

`tmpfile(3)` 函数创建并打开一个临时文件，返回一个 `FILE` 流指针而不是文件描述符。以下是它的原型：

```c
#include <stdio.h>
```

```c
FILE *tmpfile(void);
```

列表 8.4 显示了一个短程序，它创建一个临时文件，向其写入一行，然后从中读回一行。

#### 列表 8.4 tmpfile.c—使用 tmpfile(3) 函数的程序

```c
1:    /* tmpfile.c */
2:
3:    #include <stdio.h>
4:    #include <unistd.h>
5:    #include <string.h>
6:    #include <errno.h>
7:
8:
9:    int
10:   main(int argc,char *argv[]) {
11:       FILE *tmp = 0;           /* 打开临时文件 */
12:       char buf[128];          /* 输入缓冲区 */
13:
14:       if ((tmp = tmpfile()) == NULL) {
15:           fprintf(stderr,"%s: 生成临时文件。\n",
16:               strerror(errno));
17:           exit(1);
18:       }
19:       printf("PID %ld was here.\n", (long)getpid());
20:       fflush(tmp);
21:
22:       rewind(tmp);
23:       fgets(buf, sizeof(buf), tmp);
24:
25:       printf("%s", buf);
26:
27:       fclose(tmp);
28:
29:       return 0;
30:   }
```

在 FreeBSD 下编译该程序：

```
$ make tmpfile
cc -c -D_POSIX_C_SOURCE=19939L -D_POSIX_SOURCE -Wall tmpfile.c
cc tmpfile.o -o tmpfile
./tmpfile
PID 1234 was here.
```

注意，`tmpfile()` 并不调用 `unlink(2)` 来删除文件。磁盘空间在 `tmp` 关闭时会自动回收。

### 使用 tempnam(3) 函数

本章的最后一个函数是 `tempnam(3)`。它的原型如下：

```c
#include <stdio.h>
```

```c
char *tempnam(char *dir, char *prefix);
```

`tempnam` 接受两个参数。第二个参数 `prefix` 是可选的，可以传入空指针；或者指向一个可以作为临时文件名前缀的 C 字符串。

第一个参数 `dir` 比较复杂。以下步骤决定了最终目录：

1. 尝试获取环境变量 `TMPDIR`。如果它已定义且指向一个进程可写入的目录，则使用该目录。实际上，`TMPDIR` 变量允许程序选择目录。
2. 当步骤 1 失败时，检查 `tempnam(3)` 的 `dir` 参数。如果参数不是空指针，且指定的目录存在，则使用。
3. 当步骤 2 不满足时，尝试 `stdio.h` 宏 `P_tmpdir`。
4. 作为最后的手段，将使用目录 `/tmp`。

通常情况下，步骤 1 或 2 指定目录。步骤 3 和 4 是备用目录。返回的指针是一个动态分配的路径字符串，如果失败则返回空指针。在程序结束该路径后，务必释放此返回的指针。注意 `tempnam` 不创建文件，只创建路径。

列表 8.5 显示了一个使用 `tempnam(3)` 函数的程序。

#### 列表 8.5 tempnam.c—使用 tempnam(3) 函数的程序

```c
1:    /* tempnam.c */
2:
3:    #include <stdio.h>
4:    #include <stdlib.h>
5:    #include <unistd.h>
6:    #include <string.h>
7:    #include <errno.h>
8:
9:    extern char *tempnam(char *dir, char *prefix);
10:   int
11:   main(int argc,char *argv[]) {
12:       char *name;
13:
14:       if (name = tempnam(NULL, "tmp-XXXXXX")) {
15:           printf("Temp. file name is %s\n", name);
16:           free(name);
17:       } else {
18:           fprintf(stderr, "error: 生成临时文件名。\n");
19:           exit(1);
20:       }
21:       return 0;
22:   }
```

## 第 8 章 临时文件与进程清理 161

在这种情况下，`fopen(3)` 调用失败了，因为子目录 `./my_tmp` 不存在。如果你创建了它并重复测试，你将获得以下结果：

```
$ mkdir ./my_tmp
 ./tempnam
Temp. file name is ./my_tmp-a50061
$
```

这一次，程序 `./tempnam` 成功地在子目录 `./my_tmp` 中创建了一个临时文件。这源于列表 8.5 中第 16 行的规范。

如果你删除了 `./my_tmp` 目录的权限，你可以测试 `tempnam(3)` 的回退方案：

```
$ chmod 000 my_tmp
 ./tempnam
Temp. file name is /var/tmp-w50063
ls -1 _my_tmp
ls: my_tmp: Permission denied
$
```

`chmod(1)` 命令从子目录 `my_tmp` 中剥夺了所有权限。当程序运行运行时，将使用 `/var/tmp` 目录作为临时文件名。这与 FreeBSD 的 `P_tmpdir` 宏值一致。

### 使文件临时化

一旦创建了临时文件，程序在完成后必须释放它。否则，临时文件目录将随着时间的推移充满许多遗弃的文件。调用 `unlink(2)` 是很简单的，但确保在程序意外退出时执行该操作则更具挑战性。

#### 使用 unlink(2) 使文件临时化

一种确保临时文件在创建并打开后立即释放的方法是。对于 UNIX 初学者来说，这看起来似乎是不合逻辑的：只要文件保持打开状态，UNIX 文件在被解除链接（unlinked）后仍然存在。当文件的最后一个打开的文件描述符关闭时，磁盘空间会被 UNIX 内核回收。

回想函数 `tempfile(3)`，它会创建没有路径名的临时文件。它使用了这种通用过程：

- 生成一个唯一文件名。
- 创建并打开文件。
- 对临时文件名调用 `unlink(2)`。这实际上使文件变得无名，但只要文件保持打开状态，文件本身就存在。
- 调用 `fdopen(3)` 打开一个 `FILE` 流，使用第 2 步中打开的文件描述符。
- 将 `FILE` 指针返回给调用者。

#### 高级 UNIX 编程

这种无名临时文件有两个优势：不需要清理临时文件。

- 文件已经被释放了。
- 随后其他进程无法打开并篡改该临时文件。这同时也提供了一种隐私保护。

第二点仍然存在一个机会窗口，因为文件必须先被创建并传递给 `unlink(2)`。然而，这里提出的主要优势是，无论你的程序如何退出或终止，临时文件都不会被留在目录中，因为它已经取消了链接。

##### 退出清理

在某些情况下，`unlink(2)` 方法并不方便。如果文件必须关闭并重新打开，那么你别选择，必须保留一个与临时文件关联的名称。由于这个原因，C 程序员必须依赖其他方法，例如 `atexit(3)` 函数。

### 使用 atexit(3) 函数

C 库函数 `atexit(3)` 允许程序注册一个可以用于所有类型清理的函数。这里主要感兴趣的是删除临时文件。`atexit(3)` 的语法如下：

```c
#include <stdlib.h>
```

```c
int atexit(void (*func)(void));
```

传递给 `atexit(3)` 的参数仅仅是指向函数的指针，其声明如下：

```c
void func(void) {
    /* 我的清理代码。 */
}
```

函数 `atexit(3)` 在成功注册函数时返回 0，在失败时返回非零。当 `atexit(3)` 失败时，FreeBSD 返回 -1 并在 `errno` 中返回错误代码，但请务必阅读本节中关于它的警告。为了最大的可移植性，最好测试是否返回 0 以判断 `atexit(3)` 是否成功。

由 `atexit(3)` 注册的函数按照它们注册的相反顺序被调用。

> FreeBSD 和 UniWare 7 文说明至少可以注册 32 个函数。额外的条目仅限于内存。Linux 似乎支持只要剩余内存允许的任何注册数量。

HPUX 11 和 IBM 的 AIX 4.3 规定 `atexit(3)` 函数限制为最多 AEXIT_MAX 个注册函数。对于 HUX，这由 `include <limits.h>` 定义；对于 AIX，它

Solaris 8 的限制由 `sysconfig(3)` 使用参数 `_SC_ATE_MAX` 定义。

## 第 8 章 临时文件与进程清理 163

### 警告

FreeBSD 文说明 `atexit(3)` 在返回 -1 时会设置 `errno`（ENOMEM 是一个记录的返回错误）。Linux (Red Hat 6.0) 文档说明 `atexit(3)` 如果失败则返回 -1，且不设置 `errno`。

SGI IRIX 6.5、UniWare 和 HPUX 11 文说明它们在失败时返回“非零”。没有返回错误代码。由于这些原因，请始终测试 `atexit(3)` 的成功返回以获得最大的可移植性。除非考虑到特定平台，否则应忽略 `errno`。列表 8.6 中的程序展示了一个调用 `atexit(3)` 函数的示例。这会导致在终止时调用一个清理函数。

#### 列表 8.6—使用 atexit(3) 函数的程序
