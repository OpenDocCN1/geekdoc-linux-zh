
# 第 14 章 GNU/Linux 进程模型 217

```c
#include <sys/types.h>
#include <sys/unistd.h>
int socket(int domain, int type, int protocol);
int bind(int sock, struct sockaddr *addr, int *addrLen);
int listen(int sock, int backlog);
int accept(int sock, struct sockaddr *addr, int *addrLen);
int connect(int sock, struct sockaddr *servaddr, int addrLen);
int send(int sock, const void *msg, int len, unsigned int flags);
int recv(int sock, void *buf, int len, unsigned int flags);
int sendto(int sock, const void *msg, int len,
unsigned int flags,
struct sockaddr *to, int tolen);
int recvfrom(int sock, void *buf, int len,
unsigned int flags,
struct sockaddr *from, int *fromlen);
int getsockopt(int sock, int level, int optname,
void *optval, socklen_t *optlen);
int setsockopt(int sock, int level, int optname,
const void *optval, socklen_t *optlen);
int close(int sock);
```

```c
#include <sys/types.h>
#include <sys/unistd.h>
int socket(int domain, int type, int protocol);
int bind(int sock, struct sockaddr *addr, int *addrLen);
int listen(int sock, int backlog);
int accept(int sock, struct sockaddr *addr, int *addrLen);
int connect(int sock, struct sockaddr *servaddr, int addrLen);
int send(int sock, const void *msg, int len, unsigned int flags);
int recv(int sock, void *buf, int len, unsigned int flags);
int sendto(int sock, const void *msg, int len,
unsigned int flags,
struct sockaddr *to, int tolen);
int recvfrom(int sock, void *buf, int len,
unsigned int flags,
struct sockaddr *from, int *fromlen);
int getsockopt(int sock, int level, int optname,
void *optval, socklen_t *optlen);
int setsockopt(int sock, int level, int optname,
const void *optval, socklen_t *optlen);
int close(int sock);
```

```c
#include <sys/types.h>
#include <sys/unistd.h>
int socket(int domain, int type, int protocol);
int bind(int sock, struct sockaddr *addr, int *addrLen);
int listen(int sock, int backlog);
int accept(int sock, struct sockaddr *addr, int *addrLen);
int connect(int sock, struct sockaddr *servaddr, int addrLen);
int send(int sock, const void *msg, int len, unsigned int flags);
int recv(int sock, void *buf, int len, unsigned int flags);
int sendto(int sock, const void *msg, int len,
unsigned int flags,
struct sockaddr *to, int tolen);
int recvfrom(int sock, void *buf, int len,
unsigned int flags,
struct sockaddr *from, int *fromlen);
int getsockopt(int sock, int level, int optname,
void *optval, socklen_t *optlen);
int setsockopt(int sock, int level, int optname,
const void *optval, socklen_t *optlen);
int close(int sock);
```

```c
#include <sys/types.h>
#include <sys/unistd.h>
int socket(int domain, int type, int protocol);
int bind(int sock, struct sockaddr *addr, int *addrLen);
int listen(int sock, int backlog);
int accept(int sock, struct sockaddr *addr, int *addrLen);
int connect(int sock, struct sockaddr *servaddr, int addrLen);
int send(int sock, const void *msg, int len, unsigned int flags);
int recv(int sock, void *buf, int len, unsigned int flags);
int sendto(int sock, const void *msg, int len,
unsigned int flags,
struct sockaddr *to, int tolen);
int recvfrom(int sock, void *buf, int len,
unsigned int flags,
struct sockaddr *from, int *fromlen);
int getsockopt(int sock, int level, int optname,
void *optval, socklen_t *optlen);
int setsockopt(int sock, int level, int optname,
const void *optval, socklen_t *optlen);
int close(int sock);
```

```c
13:   myParentPid = getppid();
14:   myGid = getgid();
15:   myUid = getuid();
16:
17:   printf("my process is %d\n", myPid);
18:
19:   printf("my parent's process id is %d\n", myParentPid);
20:
21:   printf("my group id is %d\n", myGid);
22:
23:   printf("my user id is %d\n", myUid);
24:
25:   return 0;
26:   }
```

GNU/Linux 中的每一个进程都有一个唯一的标识符，称为进程 ID (`pid`)。每个进程都有一个父进程（`init` 进程除外）。在列表 14.1 中，你使用 `getpid()` 函数获取当前进程 ID，使用 `getppid()` 函数获取进程的父 ID。然后你使用 `getuid()` 和 `getgid()` 获取组 ID 和用户 ID。如果你编译并执行此应用程序，你将看到以下内容：
