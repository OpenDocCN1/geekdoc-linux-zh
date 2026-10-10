
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
