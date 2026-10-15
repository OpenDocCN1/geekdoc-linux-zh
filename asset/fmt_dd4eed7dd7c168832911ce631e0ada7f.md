
## 附录 A 函数原型 857

```
int fstat(int fd, struct stat *buf);
<sys/stat.h>
返回: 成功返回 0，错误时返回 -1
```

```
int fstat(int fd, const char *restrict path, struct stat *restrict buf, int flag);
<sys/stat.h>
flag: AT_SYMLINK_NOFOLLOW
返回: 成功返回 0，错误时返回 -1
```

```
int fsync(int fd);
<stdio.h>
返回: 成功返回 0，错误时返回 -1
```

```
long ftell(FILE *fp);
<stdio.h>
返回: 成功返回当前文件位置指示，错误时返回 -1
```

```
off_t ftello(FILE *fp);
<stdio.h>
返回: 成功返回当前文件位置指示，错误时返回 (off_t)-1
```

```
key_t ftok(const char *path, int id);
<sys/ipc.h>
返回: 成功返回 0，错误时返回 key_t-1
```

```
int ftruncate(int fd, off_t length);
<stdio.h>
返回: 成功返回 0，错误时返回 -1
```

```
int ftrylockfile(FILE *fp);
<stdio.h>
返回: 成功返回 0，如果获取锁则返回非零
```

```
void flock(FILE *fp);
<stdio.h>
```

```
int futimens(int fd, struct timespec times[2]);
<sys/stat.h>
```

```
int fwide(FILE *fp);
<stdio.h>
```

```
char *getcwd(char *buf, size_t size);
<unistd.h>
返回: 成功返回 buf，错误时返回 NULL
```

```
gid_t getegid(void);
<unistd.h>
返回: 调用进程的有效组 ID
```

```
char *getenv(const char *name);
<stdlib.h>
返回: 与名称关联值的指针，未找到返回 NULL
```

```
uid_t geteuid(void);
<unistd.h>
返回: 调用进程的有效用户 ID
```

```
gid_t getgid(void);
<unistd.h>
返回: 调用进程的真实组 ID
```

```
struct group *getent(void);
<grp.h>
返回: 成功返回指针，错误或文件结束返回 NULL
```

```
struct group *getgrgid(gid_t gid);
<grp.h>
返回: 成功返回指针，错误时返回 NULL
```

```
struct group *getgrnam(const char *name);
<grp.h>
返回: 成功返回指针，错误时返回 NULL
```

```
int getgroups(int getsetsize, gid_t grouplist[]);
<unistd.h>
返回: 成功返回补充组 ID 的数量，错误返回 -1
```

```
struct hostent *getostent(void);
<netdb.h>
返回: 成功返回指针，错误时返回 NULL
```

```
int getostname(char *name, int namelen);
<unistd.h>
返回: 成功返回 0，错误时返回 -1
```

### 858 函数原型附录 A

`getnameinfo(const struct sockaddr *restrict addr, socklen_t alen, char *restrict host, socklen_t hostlen, char *restrict service, socklen_t servlen, unsigned int flags);`

`<sys/socket.h>`

`<netdb.h>`

`flags: NI_DGRAM, NI_NAMEREQD, NI_NOFOQD, NI_NUMERICHOST, NI_NUMERIC_SCOPE, NI_NUMERICSERV`

`返回值: 成功返回 0，错误返回非零值`

`struct netent *getnamebyaddr(uint32_t net, int type);`

`<netdb.h>`

`返回值: 成功返回指针，错误返回 NULL`

`struct netent *getgetbyname(const char *name);`

`<netdb.h>`

`返回值: 成功返回指针，错误返回 NULL`

`struct netent *getgetent(void);`

`<netdb.h>`

`返回值: 成功返回指针，错误返回 NULL`

`int getopt(int argc, char * argv[], const char *options);`

`<fcntl.h>`

`extern int optterr, optind, optopt;`

`extern char *optarg;`

`返回值: 下一个选项字符，当全部处理完毕时返回 -1`

`int getpeername(int struct sockaddr *restrict addr, socklen_t *restrict alemp);`

`<sys/socket.h>`

`返回值: 成功返回 0，错误返回 -1`

`pid_t getpgid(pid_t pid);`

`<unistd.h>`

`返回值: 成功返回进程组 ID，错误返回 -1`

`pid_t getpgrp(void);`

`<unistd.h>`

`返回值: 调用进程的进程组 ID`

### 附录 A 函数原型 859

```
pid_t    getpid(void);
<unistd.h>
返回值: 调用进程的进程 ID
```

```
pid_t    getppid(void);
<unistd.h>
返回值: 调用进程的父进程 ID
```

```
int      getpriority(int which, id_t who);
<sys/resource.h>
which: PRIO_PROCESS, PRIO_PORITY, PRIO_USER
返回值: 成功返回 -NZERO 到 NZERO 之间的值，
错误返回 -1
```

```
struct
protent *getprotobname(const char *name);
<netdb.h>
返回值: 成功返回指针，错误返回 NULL
```

```
struct
protent *getprotobumber(int proto);
<netdb.h>
返回值: 成功返回指针，错误返回 NULL
```

```
struct
protent *getprotent(void);
<netdb.h>
返回值: 成功返回指针，错误返回 NULL
```

```
struct
passwd  *getpwent(void);
<pwd.h>
返回值: 成功返回指针，错误返回 NULL 或文件末尾
```

```
struct
passwd  *getpwnam(const char *name);
<pwd.h>
返回值: 成功返回指针，错误返回 NULL
```

```
struct
passwd  *getpwuid(uid_t uid);
<pwd.h>
返回值: 成功返回指针，错误返回 NULL
```

`![](img/5dc46842acde5fbcadfab4612cdecbbc_892_0.png)`

### 860 函数原型 附录 A

`int getrlimit(int resource, struct rlimit *rlptr);` `220`

```
<sys/resource.h>
resource: RLIMIT_CORE, RLIMIT_CPU,
IMIT_DATA, RLIMIT_NOFILE, RLIMIT_STACK,
RLIMIT_AS (FreeBSD 8.0, Linux 3.2.0, Mac OS 10.6,8),
RLIMIT_MEMLOCK (FreeBSD 8.0, Linux 3.2.0, Mac OS 10.6,8),
RLIMIT_MSQUEUE (Linux 3.2.0),
RLIMIT_NICE (Linux 3.2.0),
RLIMIT_PROC (FreeBSD 8.0, Linux 3.2.0, Mac OS 10.6,8),
RLIMIT_NPTS (FreeBSD 8.0),
RLIMIT_RSS (FreeBSD 8.0, Linux 3.2.0, Mac OS 10.6,8),
RLIMIT_SIZE (FreeBSD 8.0),
RLIMIT_SIGPEND (Linux 3.2.0),
RLIMIT_SWAP (FreeBSD 8.0),
RLIMIT_VMEM (Solaris 10)
```

`返回值: 成功返回 0，错误返回 -1`

`char *gets(char *buf);` `152`

```
<stdio.h>
返回值: 成功返回 buf，错误或文件末尾
```

```
struct servant *getbyname(const char *name, const char *proto); 599
<netdb.h>
返回值: 成功返回指针，错误返回 NULL
```

```
struct servant *getbyport(int port, const char *proto); 599
<netdb.h>
返回值: 成功返回指针，错误返回 NULL
```

```
struct servant *getservent(void); 599
<netdb.h>
返回值: 成功返回指针，错误返回 NULL
```

`pid_t getsid(pid_t pid);` `296`

```
<unistd.h>
返回值: 成功返回会话 ID，错误返回 -1
```

```
int getsockname(int sockfd, struct sockaddr *restrict addr, socklen_t *alebp); 605
<socket.h>
返回值: 成功返回 0，错误返回 -1
```

### 附录 A 函数原型 861

```
int getsockopt(int sockfd, int level, int option, void *optval, socklen_t *lenp);
<sys/socket.h>
返回值: 成功返回 0，错误返回 -1
```

`624`

```
struct spwd *getspwd(void);
<shadow.h>
返回值: 成功返回指针，错误返回 NULL
平台: Linux 3.2.0, Solaris 10
```

`182`

```
struct spwd *getspnam(const char *name);
<shadow.h>
返回值: 成功返回指针，错误返回 NULL
平台: Linux 3.2.0, Solaris 10
```

`182`

```
int gettimeofday(struct timeval *tp, void *tz);
<sys/time.h>
返回值: 始终返回 0
```

`190`

```
uid_t getuid(void);
<unistd.h>
返回值: 调用进程的真实用户 ID
```

`228`

```
struct tm *gmtime(const time_t *calptr);
<time.h>
返回值: 拆后的时间指针，错误返回 NULL
```

`192`

```
int getopt(int fd);
<stdlib.h>
返回值: 成功返回 0，错误返回 -1
```

`723`

```
uint32_t htonl(uint32_t host);
<arpa/inet.h>
返回值: 网络字节序的 32 位整数
```

`594`

```
uint16_t htons(uint16_t host);
<arpa/inet.h>
返回值: 网络字节序的 16 位整数
```

`594`

`img/5dc46842acde5fbcadfab4612decbbc_894_0.png`

### 862 函数原型 附录 A

```
const *inet_ntop(int domain, const void *addr, char *restrict str, socklen_t size);
<arpa/inet.h>
返回值: 成功返回地址字符串指针，错误返回 NULL
```

```
inet_pton(int domain, const char *restrict str, void *restrict addr);
<arpa/inet.h>
返回值: 成功返回 1，格式无效返回 0，错误返回 -1
```

```
initgroups(const char *username, gid_t base);
<grp.h> /* Linux & Solaris */
<grp.h> /* FreeBSD & Mac OS */
返回值: 成功返回 0，错误返回 -1
```

```
ioctl(int fd, int request, ...);
<sys/ioctl.h> /* System V */
<sys/ioctl.h> /* BSD and Linux */
返回值: 错误返回 -1，成功返回其他值
```

```
isatty(int fd);
<unistd.h>
返回值: 终端设备返回 1 (true)，否则返回 0 (false)
```

```
kill(pid_t pid, int sign);
<signal.h>
返回值: 成功返回 0，错误返回 -1
```

```
chown(const char *path, uid_t owner, gid_t group);
<unistd.h>
返回值: 成功返回 0，错误返回 -1
```

```
link(const char *existingpath, const char *newpath);
<unistd.h>
返回值: 成功返回 0，错误返回 -1
```

```
linkat(int cfd, const char *existingpath, int nfd, const char *newpath, int flag);
<unistd.h>
flag: AT_SYMLINK_FOLLOW
返回值: 成功返回 0，错误返回 -1
```

### 863 函数原型

```
int
io_list(int mode, struct aiocb *list[], long_t next, struct sigevent *siggev);
<aio.h>
mode: LIO_NOWAIT
返回值: 成功返回 0，错误返回 -1
```

`15`

```
listen(int sockfd, int backlog);
<sys/socket.h>
返回值: 成功返回 0，错误返回 -1
```

`60`

```
struct tm *localtime(const time_t *calptr);
<time.h>
返回值: 拆解后的时间指针，错误返回 NULL
```

`192`

```
off_t lseek(int fd, off_t offset, int whence);
<unistd.h>
whence: SEEK_SET, SEEK_CUR, SEEK_END
返回值: 成功返回偏移量，错误返回 -1
```

`67`

```
int lstat(const char *path, struct stat *buf);
<sys/stat.h>
返回值: 成功返回 0，错误时返回 -1
```

`93`

```
void*malloc(size_t size);
<stdlib.h>
返回值: 成功返回非空指针，错误返回 NULL
```

`207`

```
int mkdir(const char *path, mode_t mode);
<sys/stat.h>
mode: S_IGUD, S_ISVT,
S_WX | GRP | OTH
返回值: 成功返回 0，错误返回 -1
```

`129`

```
int mkdirat(int cfd, const char *path, mode_t mode);
<sys/stat.h>
mode: S_IGUD, S_ISVT,
S_WX | GRP | OTH
返回值: 成功返回 0，错误返回 -1
```

`129`

```
char*mkdtemp(char *template);
<stdlib.h>
返回值: 成功返回目录名指针，错误返回 NULL
```

`169`

```
char*mktemp(char *template);
<stdlib.h>
返回值: 成功返回文件描述符，错误返回 -1
```

`553`

```
time_t mtime(struct tm *imptr);
<time.h>
返回值: 成功返回日历时间，错误返回 -1
```

`192`

### 附录 A 函数原型 865

```
size_t      msgrcv(int msqid, void *ptr, size_t nbytes, long type, int flag);
<sys/msg.h>
    flag: IPC_NOWAIT, MSG_NOERROR
    返回: 如果 OK 返回消息数据部分的大小，错误返回 -1
```
