
```c
printf("Mail file is empty or does not exist.\n");
} else {
/*
 * loop continue till end of file because you want the
 * most recent address
 * IP 192.68. is the domain of your ISP, change to you...
 */
while(!feof(mail)) /* until reaching EOF, do this * */ {
fgets(location, 80, mail); /* Grab a line, from mail */
sscanf(location, "198.68.%%s", bob); /* look for domain */
strncpy(location, "198.68.", "");
strcat(location, bob);
printf("The IP Address of your computer is: %s\n",location);
}
printf("</BODY></HTML>\n");
}
}
```

# 8.2 pppdm.c

- `pppdm.c` 由 Ryan R. Klems (`rklems@primenet.com`) 创建
- 作者免费发布，供
- 使用/修改/复制/重新分
- 我唯一的请求是请使用它..给我发邮件
- 并让我知道（使用情况） =
- 此程序保持你的线路连接到 ISP 并发送
- 最新的 IP 地址。对于具有
- 动态分配 IP 地址的人来说非常有用
- 使用以下内容...
- `/root/ip` : 将 IP 输出到此文件
- `/root/log` : 如果定义了日志
- `/root/ppchat` : 为聊天设置的聊天文件。
- 我的聊天文件看起来像：
- `ATDT7917777 CONNECT "* "login:" \`
- `"rklems" 'asword:" "<password"`
- `<password>` 显然是你的密码
- （就像我不会把我的给你一样）
- `"NOTE"` 用于静音拨出的 ATMTDT
- 编译中...

# Hacks #6-8: 各种技巧

- `gcc pppdm -o pdm`
- 注意* 不要调用类似 `pppd` 的命令，因为
- 它会寻找 `pppd`，可能会意外自杀掉；
- */

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <signal.h>
#include <time.h>
#define DOLOG
void main(void)
{
FILE *fin, /* multiuse file pointer */
*popen();/* proto of popen() */
#ifdef DOLOG
FILE *log; /* log file pointer */
#endif
char line[80],/* a line of a file */
bah[80],/* just stuff, also used for holding IP addr */
crap[],/* just stuff */
bob; /* single char placeholder, not used for anything */
int j, /* flag for a link if for this is a new link */
pid; /* pid of pppd process to kill off */
#ifdef DOLOG
time_t now; /* thing for time logging */
#endif
for(:); /* Loop forever... */
{
/* look out IP addr */
if ((fin = popen('ifconfig', 'r')) != NULL)
while (fgets(line, 80, fin) != NULL)
if (sscanf(line, "ppp0 %s", bah))
{
fgets(line, 80, fin);
sscanf(line, " inet addr:%15s", bah);
j=1;
}
fclose(fin);
if (!j) /* no link */
{
if ((fin = popen('ps -a -x', 'r')) == NULL)
{
fprintf(stderr, "PPPD error: cannot open file.\n");
exit(1);
}
/* scan through processes & kill off any zombie */
pppd processes /* */
while (fgets(line, 80, fin) != NULL)
if (sscanf(line, "%d %%c %s pppd%%s", &pid, &bob, crap, bah) == 4)
kill(pid, SIGKILL);
```

# 1674 LX. "DYNAMIC-IP-HACKS-HOWTO VERSION 2.0.7" BY MICHAEL DRISCOLL

```c
fclose(fin);
k=0; /* new dial attempt */
/* try again */
system('*pppd connect chat -v -f /root/ppcpchat');
#ifdef DLOG
now = time(NULL);
if ((log = fopen("/root/log", "a")) == NULL)
{
fprintf(stderr, "Error in opening log.\n");
exit(1);
}
fprintf(log, "Initiating ppp-link. %s\n", ctime(&now));
fclose(log);
#endif
sleep(60); /* wait 1 min and check again */
if(j && !k) /* first time with address */
{
if ((fin = fopen("/root/ip", "w")) == NULL)
{
fprintf(stderr, "Error in opening file.\n");
exit(1);
}
fprintf(fin, "%s\n", bah); /* write out addr */
fclose(fin);
/* mail it to yourself */
system("mail -s joker@your.com < /root/ip");
k=1;
}
else /* take a nap and check again when wake up */
{
j = 0;
sleep(300); /* wait 5 minutes to check again */
}
```

### 8.3 portmsg.c

- `Portmsg.c` 由 Ryan R. Klems (`klems@prenet.com`) 编写
- 版权所有96， 作者免费发布，允许复制和修改，只要保留原始版权声明。
- 我要求你使用这个程序。
- 就这样。
- 此程序在服务器上设置一个端口以接受。
- 接收 telnet 后，程序输出消息然后关闭连接。
- 消息地址为 xxx.xxx.xxx，xxxx 是 IP 号，并在程序内设置。

# Hacks #6-8: 各种技巧

```c
#include <stdlib.h>
#include <stdio.h>
#include <sys/types.h>
#include <socket.h>
#include <sys/io.h>
#include <errno.h>
#include <netinet/in.h>
#include <strings.h>
#include <netdb.h>
#include <unistd.h>
#define HOSTNAME "ares" /* hostname of computer */
#define PORT 3000 /* tcp port to bind */
#define GETHOSTNAME
void get_location(void); /* proto of reading function */
char location[80]; /* The IP address */
void main(void) {
struct in_addr host_ip_number;
struct sockaddr_in host_addr;
struct sockaddr_in addr;
char host_name[100];
struct hostent *hp;
int s, new_sock;
int tmp, length;
/* 我写的这个服务器没有获取主机名，所以我加了个小修复... */
#ifdef GETHOSTNAME
gethostname(host_name, sizeof(host_name));
#else
strcpy(host_name, HOSTNAME);
#endif
hp = gethostbyname(host_name);
memcpy((char *)&host_addr.sin_addr, hp->h_addr, sizeof(host_addr));
host_addr.sin_family = hp->h_type;
host_ip_number = host_addr.sin_addr;
host_addr.sin_port = htons(PORT);
host_addr.sin_addr.s_addr = INADDR_ANY;
/* open a socket s */
s = socket(host_addr.family, SOCK_STREAM, 0);
if ((int)s==-1)
{
fprintf(stderr, "Error in opening socket.\n");
exit(1);
}
tmp = 1;
if(setsockopt(tmp, SOL_SOCKET, SO_REUSEADDR, (char *) &tmp, sizeof(tmp))<0)
{
fprintf(stderr, 'Error in setsockopt.\n');
exit(1);
}
/* bind the socket to the server */
if (bind(s, (struct sockaddr *)&host_addr, sizeof(host_addr)) == -1)
{
if (errno == EADDRINUSE)
{
fprintf(stderr, 'Socket already bound!\n');
exit(1);
}
else
{
fprintf(stderr, 'Other error binding socket.\n');
exit(1);
}
}
/* tell the server to listen to the port */
if (listen(s, 1) == -1)
/* 1 is the maximum size of the connection queue */
{
fprintf(stderr, 'Error in listen.\n');
exit(1);
}
while(1) /* just keep looping */
{
length = sizeof(addr);
/*
* port 已经通过 socket() 打开，通过 bind() 绑定，
* 并通过 listen() 设置为激活状态，现在 accept() 监控端口
* 连接，它将在这里等待直到有连接到来...
* new_sock 是新 socket 的文件描述符
*/
new_sock = accept(s, (struct sockaddr *)&addr, &length);
}
/*
* get_location() 函数和 send() 调用是我为了
* 符合我的需求而做的。
*/
get_location();
/* 发送长度为 length(foo) 的字符串 foo */
send(new_sock, 'Location:\n', 11, 0);
send(new_sock, location, strlen(location), 0);
close(new_sock);
}
void get_location(void)
{
FILE *mail; /* file pointer for mail file */
char a[80]; /* char array for holding ip addr most recent IP */
}
```

# 动态 DNS记录

如果你正在设置涉及动态 DNS 记录（当 IP 地址更改时更改以指向你的计算机的 DNS 记录），你可能想检查这些 URL：

- 1. `http://cfneu.asn.au/mathew/virtual.html`
看看这个，Matthew 让它运行了，并请求其他人尝试它的细节。对于已经拥有静态 IP 控制 DNS 的情况。
- 2. `ftp://ietf.org/internet-drafts/draft-dns-dyn-DYNS-11.txt`
IETF 是互联网工程任务组，是基本上制定未来互联网使用的协议和系统的人。这个 URL 是 IETF 关于动态 DNS 的草案，任何可能考虑此方向的人都应该阅读。

## 10 个实用技巧 #9：更新你的 .plan 文件

作者：Matthew Nuckolls <mnuck@umr.edu>

这对脚本允许用户将当前的 IP 地址存入远程服务器上的 `.plan` 文件中。这样朋友和家人就可以看到你是否已拨入，并看到 ytalk 请求了什么内容。

在你的 `ppp-off` 脚本中，将如下内容

```bash
/etc/ppp/putip "None, the link is down"
```
```

作为第一行。

你需要一个有效的 `$HOME/netrc` 文件才能让 `putip` 正常工作。我的文件看起来像这样：

```
machine rocket
login mnuck
password <password>
```

并且权限设置为 `chmod 600`

```bash
ip-up:
#!/bin/sh
# 确保此文件的权限为 711，因为你的密码是以
# 明文存储的
```

```bash
PLANLOC = /home/mnuck/.plan
REMOTE_USER_NAME = mnuck
REMOTE_PASSWORD =
REMOTE_PLANLOC = /afs/umr.edu/users/mnuck/pub/.plan
REMOTE_SERVER = rocket
```

```bash
echo ' My dynamic IP is: $4 ' /tmp/ip.myip
cat $PLANLOC /tmp/ip.myip > /tmp/plan
echo $REMOTE_USER_NAME > /tmp/ip.script
echo $REMOTE_PASSWORD >> /tmp/ip.script
echo 'put /tmp/plan' $REMOTE_PLANLOC >> /tmp/ip.script
echo 'quit' >> /tmp/ip.script
```

```bash
ftp $REMOTE_SERVER < /tmp/ip.script & /dev/null
rm -f /tmp/ip.myip
rm -f /tmp/ip.script
rm -f /tmp/plan
```

putip:

```bash
#!/#!/bin/sh
# 此脚本依赖于一个有效的 .netrc 文件
# - 详情参阅 ftp 手页
```

```bash
PLANLOC = /home/mnuck/.plan
REMOTE_PLANLOC = /afs/umr.edu/users/mnuck/pub/.plan
REMOTE_SERVER = rocket
```
