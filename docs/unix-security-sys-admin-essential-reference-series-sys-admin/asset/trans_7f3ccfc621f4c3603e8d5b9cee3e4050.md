

## 关于 SecureNet Key

SecureNet Key（SNK）是一种挑战/响应个人身份识别令牌，外形类似于小型口袋计算器。SNK 最初是为 Digital Pathway 的 SecureNet 门禁设备系列而设计的，但现在已作为独立产品提供。

SNK 具有一个电子芯片，实现了使用 DES 作为加密方案的公钥加密算法。（公钥密码学由 Whitfield Diffie 和 Martin Hellman 于 1976 年发明 [1]，以解决密钥管理问题。）每个参与者都有一对密钥：公钥和私钥。每个参与者的公钥都会公布，而私钥则保密。发送方和接收方无需共享秘密信息的需求被消除了：所有通信仅涉及公钥，且私钥永远不会被传输或共享。

在使用 SNK 之前，系统管理员必须用公钥对 SNK 进行初始化。公钥是一个 24 位随机数，每个 SNK 都是唯一的。在 SNK 用公钥初始化后，它会被交给用户，用户随后通过输入私钥——即四位个人识别号码（PIN）——来完成 SNK 的编程。在完成此步骤之前，SNK 无法使用。一旦初始化并准备就绪，只有被发放 SNK 的用户才能通过使用 PIN 来解锁设备以供使用。

在使用时，计算机将基于公钥计算一个挑战字符串。计算出的挑战始终是唯一的。用户将使用 PIN “打开” SNK 并输入挑战号码。SNK 将使用挑战号码和公钥来计算响应字符串。计算机也使用挑战号码和公钥来计算其期望的响应。如果用户对挑战字符串输入的响应与计算机计算出的响应相匹配，计算机则允许访问。

如需了解 SNK 的信息，请联系

Digital Pathways Inc.
201 Ravenloft Drive
Mountain View, CA
USA

或

Digital Pathways Inc.
5 Campbell Court
Campbell Rd
Bramley, Basingstoke
Hants RG26 5EG
(44)256-882191

## 参考文献

[1] Diffie, W. and M.E. Hellman. “New directions in Cryptography.” *IEEE Transactions on Information Theory*, IT-22:644-654, 1976.

包装程序，`snklogin`（清单 13.1 和 13.2），接受用户的 SNK 用户 ID，该 ID 存储在 `/etc/keyfile` 中（只要在 13.3 中列出）。与此 SNK 用户 ID 关联的 24 位共享密钥号码也存储在此文件中。在根据提供的 SNK 用户 ID 选择共享密钥后，`snklogin` 会提示用户输入从共享密钥计算出的挑战字符串并等待响应。如果 `snklogin` 计算出的响应与用户输入的不匹配

```
/* snklogin.c - front end to standard login program which first authenticates the
 * user using the SecureNet encryption key. Mark Dapaz Wed Dec 2 15:41:47 MET 1992
 */

#include <stdio.h>
#include <stdlib.h>
#include <strings.h>
#include <ctype.h>
#include <signal.h>
#include <setjmp.h>
#include <syslog.h>
#include <pwd.h>
#include "snk.h"
#include "pathname.h"
#include "des.h"

char snkey[8];
int flgason, oflg=0, hflg=0;
char *from_host = "unknown host";
char *from_ip = "location unknown";
char *user = NULL;

jmp_buf env;

main(argc, argv)
int argc;
char **argv;
{
    char challenge[9], response[9], snkey[8], reply[16];
    char md[16], in_id[9], to, message[1024];
    unsigned int oct1, oct2, oct3, oct4, oct5, oct6, oct7, oct8, cksum;
    register int ch;
    int i;
    int secured=0;
    extern char *optarg;
    extern int optind;
    FILE *in_file;
    extern int timeout();
    char *real_ipinfo;
    char *auth_class=NULL;
    int quit();

    /* list of hostnames that we allow through */
    char *hosts_allow[] = {"viceroy.bsc.no", "viceroy.bsc.no", "overlord.bsc.no", NULL };

    /* list of ip addresses that we allow through */
    char *ip_addr_allow[] = {"129.177.80.6", "129.177.80.64", "129.177.80.64", NULL };
```
