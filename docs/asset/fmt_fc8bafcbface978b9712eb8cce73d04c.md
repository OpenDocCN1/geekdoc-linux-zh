
```c
/* dict.cpp - main, nextin */

#include <stdlib.h>
#include <stdio.h>
#include <ctype.h>

#define MAXWORDLEN 50    /* 命令或单词的最大长度 */

int   nextin(char *, char *), initw(void), insertw(char *),
       deletew(char *), lookup(char *);
----------------------------------------------------------------------
/*
 * main - 按指定在字典中插入、删除或查找单词
----------------------------------------------------------------------
*/
main(int argc, char *argv[]) {
    char   word[MAXWORDLEN+1];    /* 用于存放输入行单词的空间 */
    char   cmd;
    int    wrdenlen;               /* 输入单词的长度 */

    while (1) {
        wrdenlen = nextin(cmd, word);
        if (wrdenlen < 0) {
            exit(0);
        }
        switch (cmd) {
            case 'I':                   /* 初始化 */
                initw();
                printf("Dictionary initialized to empty.\n");
                break;
            case 'i':                  /* 插入 */
                insertw(word);
                printf("%s inserted.\n", word);
                break;
```

## Sec. 22.6 第 2 步：将程序分为两部分

```c
case 'd':
    /* 删除 */
    if (deletew(word))
        printf("%s deleted.\n",word);
    else
        printf("%s not found.\n",word);
    break;
case 'l':
    /* 查找 */
    if (lookup(word))
        printf("%s found.\n",word);
    else
        printf("%s not found.\n",word);
    break;
case 'q':
    /* 退出 */
    exit(0);
default:
    /* 无效输入 */
    printf("invalid command %c\n",cmd);
    break;
        }
    }
    return 0;
}

/* ---------------------------------------------------------------------
 * nextin - 从输入行读取命令并可能读取单词
--------------------------------------------------------------------- */
int nextin(char *cmd, char *word) {
    int i = 0, ch;
    while ((ch = getchar()) != EOF) {
        if (isspace(ch)) {
            if (i > 0) {
                word[i] = '\0';
                cmd = word;
                return i;
            }
        } else {
            if (i < MAXWORDLEN) {
                word[i++] = ch;
            } else {
                printf("word too long.\n");
                return -1;
            }
        }
    }
    return -1;
}
```

`dict2.cpp` 包含了原始应用程序中将成为远程程序的部分。此外，它包含了过程共享的全局数据的声明。此时，该文件不包含完整的程序——剩余代码将添加。

```c
/* dict2.cpp - initw, insertw, deletew, lookupw */

#include <string.h>

#define MAXWORDLEN 50 /* 命令或单词的最大长度 */
#define DICTSZ 100 /* 最大条数 */
char dict[DICTSZ][MAXWORDLEN+1];/* 字典存储 */
int nwords = 0; /* 字典中的单词数 */

/*- initw - 初始化字典为空 *-
*/
initw() {
    nwords = 0;
    return 1;
}

/*- insertw - 在字典中插入单词 *-
*/
int
insertw(char *word) {
  strcpy(dict[nwords], word);
  nwords++;
  return nwords;
}
```

```c
/*
 * delete - 从字典中删除单词
 */
int
deletew(char *word) {
  int i;
  for (i=0; i<nwords; i++) {
    if (strcmp(word, dict[i]) == 0) {
      nwords--;
      strcpy(dict[i], dict[nwords]);
      return 1;
    }
  }
  return 0;
}
```

```c
/*
 * lookupw - 在字典中查找单词
 */
int
lookupw(char *word) {
  int i;
  for (i=0 ; i<nwords; i++)
    if (strcmp(word, dict[i]) == 0)
      return 1;
  return 0;
}
```

292 分布式程序生成 (`Rpcgen` 示例) 第22 章

从实践角度来看，将应用程序分为两个部分使得单独编译客户端和服务器成为可能。编译器检查两部分都引用的符号常量等问题，而链接器则检查所有数据结构是否已与引用它们的过程被收集在一起。

尽管编译器似乎是一步之读取源程序并生成可执行的二进制文件，但大多数编译器至少有两个内部步骤。在第一步中，计算机检查语法并生成中间对象文件（后缀为 `.obj` 的文件）。在第二步中，编译器调用链接编辑器将对象文件合并为可执行的二进制文件。在这一步，程序员通常会请求编译器为这两个组件生成对象文件（而不是完整的程序）。这些组件必须链接在一起以生成可执行程序，但并并不是编译它们的直接原因：编译器会检查两个文件在语法上都是正确的。

在考虑让编译器检查代码的用处时，请记住，大多数分布式程序比我们简单的示例要复杂得多。编译可能会在大型程序中发现程序员忽略的问题。在插入额外代码之前捕获这些问题将使它们更容易修复。

## 22.7 第 3 步：创建 Rpcgen 规范

一旦程序员选择了分布式程序的结构，他或她就可以准备一个 `rpc` 规范。从本质上说，`rpc` 规范文件包含了远程程序的声明，包括它所使用的数据结构。

规范文件包含常量、类型定义以及客户端和服务器程序的声明。更准确地说，规范文件包含：

- 客户端或（更常见的是）服务器（远程程序）中使用的常量声明，
- 使用的数据类型声明（特别是在远程过程的参数中），
- 远程程序的声明、每个程序中包含的过程以及其参数的类型。

记住，RPC 使用数字来识别远程程序及其内部远程过程。规范文件中的程序声明定义了详细信息，如程序的 RPC 数字、版本号以及分配给程序内每个过程的编号。

所有规范必须用 RPC 编程语言编写，而不是 C 语言。虽然差异很小，但它们可能会令人感到沮丧。例如，RPC 语言使用关键字 `string` 来表示以空字符结尾的字符字符串，而 C 使用 `char *`。甚至*链接器* 也经常被缩写。

经验丰富的程序员可能需要多次迭代才能产生正确的规范。

文件 `dict.x` 展示了一个 `rpc` 规范。它包含了字典程序 RPC 版本的示例声明。
