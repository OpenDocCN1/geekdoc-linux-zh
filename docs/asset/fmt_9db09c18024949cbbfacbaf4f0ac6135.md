
# 终端 Shell 557

```c
951 char name;
952 char* name;
953 int type;
954 
955 {
956 int serverFd, clientFd, serverLen, clientLen;
957 int domain, internet, port;
958 struct sockaddr_un serverUNIXAddress;
959 struct sockaddr_un clientUNIXAddress;
960 struct sockaddr_in serverINETAddress;
961 struct sockaddr_in clientINETAddress;
962 struct sockaddr* serverSockAddrPtr;
963 struct sockaddr* clientSockAddrPtr;
964 
965 /* 准备服务器套 */
966 internet = internetAddress(name); /* 互联网？ */
967 domain = AF_UNIX; /* 选择作用域 */
968 /* 创建服务器套 */
969 serverFd = socket(domain, SOCK_STREAM, DEFAULT_PROTOCOL);
970 
971 if (serverFd == -1)
972 {
973 perror("ish");
974 return (FALSE);
975 }
976 
977 if (internet) /* 互联网套接 */
978 {
979 sscanf(name, "%d", &port); /* 获取端口号 */
980 /* 填充服务器地址字段 */
981 serverLen = sizeof(serverINETAddress);
982 zero ((char*)&serverINETAddress, serverLen);
983 serverINETAddress.sin_family = AF_INET; /* 作用域 */
984 serverINETAddress.sin_addr.s_addr = htonl(INADDR_ANY);
985 serverINETAddress.sin_port = htons(port); /* 端口 */
986 serverSockAddrPtr = (struct sockaddr*)&serverINETAddress;
987 }
988 else /* UNIX 域套接 */
989 {
990 serverUNIXAddress.sun_family = AF_UNIX; /* 作用域 */
991 strcpy(serverUNIXAddress.sun_path, name); /* 文件名 */
992 serverSockAddrPtr = (struct sockaddr*)&serverUNIXAddress;
993 serverLen = sizeof(serverUNIXAddress);
994 unlink(name); /* 如果套接字已存在则删除 */
995 }
996 
997 /* 绑定到套接字地址 */
998 if (bind(serverFd, serverSockAddrPtr, serverLen) == -1)
999 {
1000 perror("ish");
1001      return (FALSE);
1002      }
1003
1004      /* 设置最大等待连接队列长度 */
1005      if (listen(serverFd, DEFAULT_QUEUE_LENGTH) == -1
1006
1007
1008          perror("ish");
1009          return (FALSE);
1010      }
1011
1012      if (internet) /* 互联网套接 */
1013      {
1014          clientLen = sizeof(clientINETAddress);
1015          clientSockAddrPtr = (struct sockaddr*)&clientINETAddress;
1016      }
1017      else /* UNIX 域套接 */
1018      {
1019          clientLen = sizeof(clientUNIXAddress);
1020          clientSockAddrPtr = (struct sockaddr*)&clientUNIXAddress;
1021      }
1023
      /* 接受连接 */
1024      clientFd = accept(serverFd, clientSockAddrPtr, &clientLen);
1025
1026      close(serverFd); /* 关闭原始服务器套接 */
1027
1028      if (clientFd == -1)
1029      {
1030          perror("ish");
1031          return (FALSE);
1032      }
1034
      /* 执行重定向 */
1035      if (type == OUTPUT_SOCKET) dup2 (clientFd, STDOUT);
1036      if (type == INPUT_SOCKET) dup2 (clientFd, STDIN);
1037      close(clientFd); /* 关闭原始客户端套接 */
1038
1039      return (TRUE);
1040  }
```

# 558 第 13 章 系统编程

## 章末总结

## 检查清单

在本章中，我描述了：

- 所有常用的文件管理系统调用
- 用于复制进程、终止和区分进程的系统调用
- 父进程如何等待其子进程
- 孤儿和僵尸线程进程的术语
- 如何捕获和忽略信号
- 杀死进程的方法
- 进程如何挂起和恢复
- IPC 机制：无名管道、共享内存和信号量
- 客户端-服务器范式
- UNIX 域套接字和互联网套接字
- 互联网 Shell 设计与运行

## 测验

1. 如何判断何时到达文件末尾？
2. 什么是文件描述符？
3. 移动到文件末尾的最快方法是什么
4. 描述 shell 实现 I/O 的方式。
5. 什么是孤儿进程？
6. 在两个进程中运行与在线程中运行有什么区别？
7. 在什么情况下僵尸进程会累积？
8. 父进程如何找到其子进程？
9. `exec()` 和 `execv()` 有什么区别？
10. `kill()` 系统调用的误用是什么？
11. 如何保护关键代码？
12. 进程组的作用是什么？
13. 当写入尝试溢出管道时会发生什么？
14. 如何创建命名管道？
15. 描述客户端-服务器范式。
16. 描述客户端和服务器建立连接的阶段。

## 练习题

1. 编写一个程序捕获信号并打印发送了什么信号。`SIGKILL` 与其他信号有什么区别？

2. 编写一个程序从命令行接收一个整数 `n`，创建一个深度为 `n` 的进程树。当树创建时，进程看起来如下：

`$ tree 4`

I am process 1

I am process 2

I am process 3

I am process 4

确保父进程及其子进程通过 `Control-C` 终止。

3.3 编写一个通过管道连接的三个进程程序。第一个进程提示用户输入字符串并发送给第二个进程。第二个进程将字符串转换为大写并发送给第三个进程。第三个进程将字符串反转并传回第一个进程。当第一个进程获取字符串后应终止。示例：

`$ ring`

Please enter a string: hello

Processed string is: HELLO

3.4 使用 C 语言重写第5 节练习。

3.5 编写一个使用 `setuid()` 让用户访问通常无法访问的文件。

## 项目

编写一组并行运行并交互以玩“剪刀石头布”游戏的程序。在这个游戏中，两个玩家秘密地选择剪刀、石头或布。然后他们展示选择。裁判根据以下规则判断胜负：

- 布赢过石头。
- 石头赢过剪刀。
- 剪刀赢过布。
- 选择相同为平局。

胜者得一分。平局不给分。你的程序应该模拟游戏，允许用户选择迭代次数，观察游戏并查看最终得分。示例：

`$ play 3`

Paper, Scissors, Rock: 3 iterations

Player 1: ready

Player 2: ready

Go Players [1]

Player 1: Scissors

Player 2: Rock

Player 2 wins

Go Players [2]

Player 1: Paper

Player 2: Rock

Player 1 wins

Go Players [3]

Player 1: Paper
