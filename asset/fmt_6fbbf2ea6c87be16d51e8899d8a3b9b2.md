
`/home rw`

这表示你希望 `/home` 目录在任何具有读写权限的远程系统上都可以进行 NFS 挂载。

在其他每个（NFS 客户端）节点上，向 `/etc/fstab` 文件添加以下行：

```
alpha:/home  home nfs rw 0 0
```

这表示你希望通过 NFS 将 `alpha` 的 `/home` 目录挂载到本地，路径为 `/home`，并具有读写权限，或者更准确地说，挂载在你的本地 `/home` 目录上，因为为了让此挂载成功，你需要在本地有一个 `/home` 目录。这个过程被称为挂载远程文件系统。

NFS 服务器首先启动，它的进程发现本地的 `/home` 子目录已提供给任何请求它的其他节点导出。当其他节点启动时，NFS 进程处理每个来自 `alpha` 的可用 `/home` 目录的请求。该文件系统现在似乎位于本地节点的硬盘上。当你登录到节点 `gamma`（或 `beta` 或 `delta`）时，你的主目录将对你可用，以及你所有的文件。

## 远程访问安全

书中的简单集群系统假设已享有完全的物理访问安全。也就是说，你和你受信任的同伴是被允许靠近任何节点并登录的人，且没有任何节点可以从该物理边界之外的任何网络访问。如果你想把任何人排除在境外，配置将变得复杂得多！本书的重点是帮助你让集群运行起来。如果你允许公众通过 Internet 访问它，你将不得不进行一些更改来加固安全性。在这里，我们感兴趣的是降低安全性以方便自己进行远程访问，从而节省时间。

在你登录 `alpha` 后，为了节省时间方便自己远程访问，可以通过 `telnet` 命令访问机器：

- `telnet beta`

该命令会向你请求用户 ID 和密码，前提是你已经在 `beta` 已经设置了这些信息。同样，你可以执行 `rlogin`（远程登录）命令，它假设你的用户 ID 和密码：

- `rlogin beta`

该命令与 `telnet` 相同，但它通过用户 ID 允许你登录，从而节省更多时间。`rsh`（远程 shell）命令与 `rlogin` 相同，但输入更短、更快：

- `rsh delta`

它会将你登录到名为 `delta` 的机器，就像 `rlogin` 命令一样。这是最快最简单的登录方法，但会产生安全风险。

## 可选添加 /home/chief/.hosts 文件

即使在物理安全的系统中，软件检查也可以阻止你直接登录。为了利用这种终极的时间节省工具，你可以在主目录创建一个文件，让系统假设你的密码以及你的用户 ID。创建一个名为 `.hosts`（开头必须有一个点）的文件，位于 `/home/chief`，即你的主目录。

每个主机名后面跟着受信任的用户 ID。在这种情况下，你只有一个用户，所以你主目录下的 `.hosts` 文件将方便你从集群的任何节点登录到另一个节点。虽然你可以建立从 `alpha` 到 `gamma` 再到 `delta` 的远程登录链，但你应该养成在登录另一台远程机器之前登出当前机器的习惯，以保持简单。

每当你从网络上的某个节点尝试登录时，该文件都会被远程登录过程检查。注意，网络上的每个节点都会拥有此文件，因为你主目录中的所有文件都通过之前配置的网络文件系统变为可用。`NFS` 是一个非常有用的功能。

通过指定网络上的所有节点以及你的用户 ID，你允许从任何节点访问任何其他节点，而无需密码检查。

## 可选对 /etc/passwd 文件的更改

如果你经常以用户 `chief` 的身份登录并以 `root` 的身份进行系统配置，你可能想要消除对这些密码的需求。这无疑是一个安全风险，但它会节省大量时间。如果你的系统位于安全区域，且你（以及你信任 `root` 密码的人）永远不会靠近这些系统，你可以物理地从你的用户 ID 和 `/etc/passwd` 中的 `root` 条目删除密码。

```
root:c6752ffa:0:0:root:/bin/bash

chief:4456aab:500:500:Chief User:/home/chief:/bin/csh
```

# 第 5 章 配置相关的操作系统文件

密码文件中的每一行条目包含多个字段，每个字段之间用冒号（`:`）隔开以提高可读性。在 Unix 系统中，可读性通常意味着机器可读性，但有时会对人类带来挑战。你可以编辑此文件（以 `root` 为例），并重写字段的内容：

```c
root::0:0:root:/bin/bash

chief::500:500:Chief User:/home/chief:/bin/csh
```

注意，`::` 代表条目中的一个条目或空（null）字段。`root` 用户或你的个人用户 ID 不再需要密码。除非你隐含地信任可能访问这些系统的其他人，否则不要执行此操作！你必须在你的每个节点的 `/etc/passwd` 文件中进行这些更改。

## 注意事项

你可能会发现，后后发布的 Linux 版本更改了密码文件的意义，甚至可能已经替换了它。在这些情况下，其他其他方法消除输入密码的必要性。请参考安装包中附的 Linux 文档。

## 远程引用命令

在第 3 章中，你检查了 `fork/exec` 子进程的几种变体，并得到了一对进程：一个是本地客户端，另一个是远程服务。列表 3.9a 和列表 3.9c 中的 TCP 示例对可以转换为远程引用和远程守护进程对。在列表 5.1a 和列表 5.1b 中实现了一个远程文件列出服务。

> 注意
> 不熟悉 Linux 下 C 程序编译的读者可能想直接跳到第 6 章“为软件开发配置用户环境”。

### 列表 5.1A 远程-cat 命令：列出远程位置文件的内容

```c
/*
** Listing5.1a.c - rcat: 列出远程文件的内容
*/
#include <netinet/in.h>
#include <sys/socket.h>
#include <string.h>
```

### 列表 5.1A 续

```c
#include <netdb.h>
#include <stdio.h>
#define BUFLEN 8192
#define PORT 6789
int main(int argc, char *argv[])
{
    struct sockaddr_in sock;
    struct hostent *hp;
    int port = PORT;
    int fd, ii;
    char buffer[BUFLEN];
    char *p;
    /* argv[] */
    if(argc < 2)
    {
        printf("\nUsage: %s <IP_Addr>:<file_name\n\n", argv[0]);
        exit(-1);
    }
    /* 隔离远程主机 */
    p = strchr(argv[1], ':');
    *p = '\0';
    p++; /* 重置到文件 */
    /* 获取有关远程服务器的关键信息 */
    strncpy(buffer, argv[1], sizeof(buffer));
    if((hp = gethostbyname(buffer)) == NULL)
    {
        perror("Listing5.1a: gethostbyname()");
        exit(-1);
    }
    /* 初始化 TCP 流套接字结构 */
    if((fd = socket(AF_INET, SOCK_STREAM, 0)) < 0)
    {
        perror("Listing5.1a: socket()");
```

### 列表 5.1A 续

```c
        exit(-1);
    }
    memset((char *) &sock, 0, sizeof(sock));
    memcpy(&sock.sin_addr, hp->h_addr, hp->h_length);
    sock.sin_family = hp->h_addrtype;
    sock.sin_port = htons(port);
```

```c
/* 连接到远程服务器 */
if(connect(fd, (struct sockaddr *)&sock, sizeof(sock)) < 0)
{
    perror("Listing5.1a: connect()");
    exit(-1);
}
```

```c
/* 将文件名发送到服务 */
strncpy(buffer, p, sizeof(buffer));
if(send(fd, buffer, strlen(buffer)+1, 0) < 0)
{
    perror("Listing5.1a: send()");
    exit(-1);
}
```

```c
/*
** 将远程文件内容打印到屏幕
*/
while(1)
{
```
