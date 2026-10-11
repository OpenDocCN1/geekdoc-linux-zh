
```c
/*
 * insertw - 调用 insertw_1 的客户端接口例程 */
int insertw(char *word)
{
    char **arg; /* 参数指针 */
    arg = &word;
    ret = insertw_1(arg, handle);
    return ret == 0 : *ret;
}

/*
 * deletew - 调用 deletew_1 的客户端接口例程 */
int deletew(char *word)
{
    char **arg; /* 参数指针 */
    arg = &word;
    ret = deletew_1(arg, handle);
    return ret == 0 : *ret;
}

/*
 * lookupw - 调用 lookupw_1 的客户端接口例程 */
int lookupw(char *word)
{
    char **arg; /* 参数指针 */
    arg = &word;
    ret = lookupw_1(arg, handle);
    return ret == 0 : *ret;
}
```

## 22.13.2 服务端接口例程

在服务器端，接口例程接收来自 RPC 生成存根的调用，并将控制传递给实现该调的过程。与客户端不同，服务端接口例程将 rpc 选择的参数类型转换为调用过程使用的参数类型。在大多数情况下，区别在于额外的间接————传递的是对象的指针而不是对象本身。为了转换参数，接口只需要应用 C 间接运算符（`*`）。`rdict_svc.cpp` 展示了这一概念。它包含了字典程序的服务端接口例程。

```c
/* rdict_svc.cpp - initw_1, insertw_1, deletew_1, lookup_1 */
#include <rpc/rpc.h>
#define RPC_SVC
#include "rdict.h"

/* 手写的端端存根例程 */
static int retcode;

int initw(void), insertw(char *), deletew(char *), lookupw(char *);

/*------------------------------------------------------
 * insertw_1 - 远程过程 insertw 的服务端接口 */
int insertw_1(void *w, struct svc_req *rqstp)
{
    retcode = insertw((char **)w);
    return retcode;
}

/*------------------------------------------------------
 * initw_1 - 远程过程 initw 的服务端接口 */
int initw_1(void *w, struct svc_req *rqstp)
{
    retcode = initw();
    return retcode;
}

305
/*
 * deletew_1 - 远程过程 deletew 的服务端接口 */
int deletew_1(void *w, struct svc_req *rqstp)
{
    retcode = deletew((char **)w);
    return retcode;
}

/*
 * lookuppw_1 - 远程过程 lookuppw 的服务端接口 */
int lookuppw_1(void *w, struct svc_req *rqstp)
{
    retcode = lookuppw((char **)w);
    return retcode;
}
```

## 22.14 第 6 步：编译并链接客户端程序

一旦客户端接口例程编写完成并放置在源文件中，就可以对其进行编译。例如，`rdict_client.cpp` 文件包含了字典示例的所有客户端接口例程。编译器将产生目标文件 `rdict_client.obj`。为了完成客户端，程序员需要在主程序中添加一些细节。由于新版本使用了 RPC，它需要包含 RPC 声明的 C语言头文件。它还需要包含 `rdict.h`，因为该文件包含了客户端和服务器使用的常量定义。

客户端程序还需要声明并初始化句柄，供 RPC 通信例程与服务器进行通信。大多数客户端使用定义的类型 `CLIENT` 声明句柄，并通过调用 RPC 库例程 `clnt_create` 来初始化句柄。`rdict.cpp` 显示了必要的代码示例：

```c
/* rdict.cpp - main, nextin */
#include <rpc/rpc.h>
#include <stdlib.h>
#include <stdio.h>
#include <ctype.h>
#include <rdict.h>

#define WSVERS                 MAKEWORD(2, 0)
#define MAXWORDLEN             50              /* 命令或单词的最大长度 */
#define RMACHINE               localhost      /* 远程机器名称 */
CLIENT                 *handle;        /* 远程过程句柄 */

int    nextin(char *, char *), initw(void), insertw(char *);
int    deletew(char *), lookupw(char);

/*----------------------------------------------------------------*/
* main - 在字典中插入、删除或查找单词
/*----------------------------------------------------------------*/
main(int argc, char *argv[]) {
    char    word[MAXWORDLEN+1]; /*用于存储输入行单词的空间*/
    char    cmd;
    int     wrdlen;         /* 输入单词的长度 */
    WSADATA wsdata;

    if (WSastartup(WSVERS, &wsdata) < 0) {
        fprintf(stderr, "WSastartup failed\n");
        exit(1);
    }
    /* 设置远程过程调用连接 */

    handle = clnt_create(RMACHINE, RDICTPROG, RDICTVERS, *top);
    if (handle == NULL) {
        printf("Could not contact remote program.\n");
        exit(1);
    }
}
```

## 第 22.14 第 6 步：编译并链接客户端程序 307
