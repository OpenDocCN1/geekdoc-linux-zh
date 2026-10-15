
```cpp
char * Client::getResponseFromServer(char * str) {

  if ((socket_descriptor = socket(AF_INET, SOCK_STREAM, 0)) == -1) {
    perror("Error opening socket\n");
    exit(1);
  }

  if (connect(socket_descriptor, (const sockaddr *)&pin, sizeof(pin)) == -1) {
    perror("Error connecting to socket\n");
    exit(1);
  }

  cout << "Sending message '" << str << "' to server...\n";

  if (send(socket_descriptor, str, strlen(str)) == -1) {
    perror("Error in send\n");
    exit(1);
  }

  if (recv(socket_descriptor, buf, 8192, 0) == -1) {
    perror("Error in receiving response from server\n");
    exit(1);
  }

  close(socket_descriptor);

  cout << "\nResponse from server:\n" << buf << "\n";
  return buf;
}
```

系统调用 `socket`、`connect`、`send`、`recv` 和 `close` 在第 19 章中描述过。

## 实现服务器

`Server` 类的构造函数的特殊之处在于，构造函数不会返回到调用程序。构造函数设置了一个处理循环并无限运行。`Server` 类构造函数的实现与第 19 章中看到的 `server.c` 示例相似：

```cpp
Server::Server(void (*a_work_func)(char *, char *, int) , int my_port) {
    work_func = a_work_func;
    port = my_port;
    int address_size;
    int i, len;
    char buf[4000]; // 用于接收来自客户端的数据

    temp_buf = new char[16384]; // 用于返回数据的空间
    sock_descriptor = socket(AF_INET, SOCK_STREAM, 0);
    if (sock_descriptor == -1) {
        perror("call to socket");
        exit(1);
    }

    bzero(&sin, sizeof(sin));
    sin.sin_family = AF_INET;
    sin.sin_addr.s_addr = INADDR_ANY;
    sin.sin_port = htons(port);

    if (bind(sock_descriptor, (struct sockaddr*)&sin, sizeof(sin)) == -1) {
        perror("call to bind");
        exit(1);
    }

    if (listen(sock_descriptor, 20) == -1) {
        perror("call to listen");
        exit(1);
    }
    while(1) {
        temp_sock_descriptor = accept(sock_descriptor, (struct sockaddr*)&pin, &address_size);
        if (temp_sock_descriptor == -1) {
            perror("call to accept");
            exit(1);
        }

        if (recv(temp_sock_descriptor, buf, 4000, 0) == -1) {
            perror("call to recv");
            exit(1);
        }

        // 这调用了传递给
        // 类构造函数的函数：
        work_func(buf, temp_buf, 16384);

        // 虚函数 doWork 填充了
        // 返回给客户端的数据 'temp_buf'：

        len = strlen(temp_buf);

        if (send(temp_sock_descriptor, temp_buf, len, 0) == -1) {
            perror("call to send");
            exit(1);
        }
    }
}
```

`Server` 类构造函数使用 `socket`、`bind`、`listen`、`accept` 和 `recv` 调用来建立与远程客户端对象的连接。构造函数中的主处理循环对每个新的服务请求调用 `my_work` 函数，等待 `my_work` 在 `temp_buf` 缓冲区返回数据，然后将数据返回给客户端对象。下一节包含编写工作函数、创建服务器对象以及处理客户端请求的示例。

# 用于 TCP 套接字的 C++ 类库

## 第23 章

## 测试 C++ 客户端/服务器类

`Server` 类包含一个指向工作函数的私有指针，该函数被调用处理每个客户端请求。下面的简单程序定义了一个简单的工作函数，向客户端返回消息，并创建一个服务器对象来处理客户端请求。

```cpp
#include <iostream>
#include "Server.h"

void my_work_func(char *command, char *return_buffer, int return_size) {
    cout << "entering my_work_func(" << command << ")\n";
    sprintf(return_buffer, "my_work_func: %s", command);
}

void main() {
    Server * server = new Server(my_work_func); // 默认端口=8080
}
```

在这个示例中，你也可以直接创建服务器，而不是使用 `new` 运算符：

```cpp
Server(my_work_func);
```

接这个短程序可以用于测试 `Client` 类：

```cpp
#include <iostream>
#include "Client.h"

void main() {
    // 默认主机="127.0.0.1", 端口=8080
    // 在构造函数中：
    Client * client = new Client("127.0.0.1", 8080);
    // 关闭套接字
    delete client;
}
```

# 使用库

## 第 24 章

- 数学库经过了修正，并在许多情况下提高了速度。
- 标准合规性

然而，这些增强和改进的代价是在 `lib5` 和 `lib6` 之间引入了根本性的不兼容性。在 Linux 发行版迁移到 `lib6` 之前，Linux 用户必须意识到并处理这种不兼容性。发行版构建者（如 Caldera 和 Red Hat）必须提供兼容性库，以便使用户能够运行依赖于这两个库版本中任一的程序，同时又让发行版基于另一个库进行构建。更糟糕的是，由于 C 语言库在任何 Linux（或 UNIX）系统中都是无处不在且基础性的，从 `lib5` 升级到 `lib6` 是一项艰巨的任务，如果操作不当或疏大意，可能会导致系统无法使用。

“你想表达什么？”如果你正在寻找新的 Linux 发行版，你可以使用基于 `lib6` 的发行版来解决整个问题。其次，如果你是一个开发者，你必须决定是支持 `lib5`、`lib6` 还是两者都支持。最后，整个讨论为软件开发提供了一个极佳的教训，凸显了良好设计的重要性以及核心软件组件变更的深远影响。这个教训很简单：深思熟虑的软件设计将尽可能提供通用、可扩展的公共接口，并最大限度地减少引入核心不兼容变更的需求。

# 库工具

在进入库的创建和使用之前，本节将快速介绍你创建、维护和管理编程库所需的工具。更详细的信息可以在后续节讨论的每个命令和程序的帮助页以及 `info` 文档中找到。

## 理解 `nm` 命令
