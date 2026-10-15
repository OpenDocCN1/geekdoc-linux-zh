
```c
#include "uucp.h"

#define _PATH_SLIPLOGIN "/usr/sbin/slip login"
#define _PATH_PPPD "/usr/sbin/pppd"
/* amount of time we will wait for CONNECT */
extern int maxexpecttime, trycalls;  /* number of times to retry a line */

jmp_buf Sjbuf;  /*needed by uucp routines*/
extern void cleanup();

main(argc, argv)
int argc;
char *argv[];
{
int ret, i, sflag = 0, fflag = 0, fd;
char *name, *pgrm, *string, *shost;
/* for uucp callers, dialers feedback */
Verbose = 1;

shost = NULL;
name = ((name = strchr(argv[0], '/')) == NULL) ? argv[0] : name + 1;
strcpy(Progname, name);
ret = setservice("slip");
ASSERT(ret == 0, CL_OPEN, "Systems", ret);
```

# Listing 13.6 (continued)

```c
trycalls = 1; /* default in uucp is 2 */
while ((i = getopt(argc, argv, "DS:x:ff:R:")) != EOF)
    switch (i) {
    case 'd':
        Debug = 9; /*turns on uucp debugging level 9*/
        break;
    case 'S':
        slhost = optarg;
        break;
    case 'x':
        Debug = atoi (optarg);
        break;
    case 'f':
        fflag++;
        break;
    case 'T':
        maxexpecttime = atoi (optarg);
        break;
    case 'R':
        trycalls = atoi (optarg);
        break;
    case '?':
        goto Usage;
    }

/* XXX: add the ability to specify phone number,
line, etc. like cu */
if (optind < argc && optind > 0) {
    sflag++;
    string = argv[optind];
    if (!verays(string))
        (void) fprintf(stderr, "Is: %s not in Systems file\n", Progname, string);
        cleanup(10);
    }

    strcpy(ProName, string, MAXBASENAME);
    ProName[MAXBASENAME] = '\0';
    if (slhost == NULL)
        slhost = RmtName;

if (!sflag) {
Usage:
    fprintf (stderr, "Usage: %s [-d] [-T seconds] [-R retries]\n", Progname);
    fprintf (stderr, "[-S sliphost] [SystemName]\n", Progname);
    fprintf (stderr, "\twhere:\n");
    fprintf (stderr, "\t'sliphost is the Slip Host keyword in slip.hosts\n");
    fprintf (stderr, "\t'systemName is the dial-out systemname\n");
    exit (1);
}
```

## Administering the SLIP Users

设置 SLIP 用户需要多个管理步骤。完成设置后，用户将能够连接到 SLIP 服务器，并由服务器在预定的号码上回拨用户。然后用户可以使用 Internet 和 LAN 上提供的所有服务。

第一步是在用户将用于登录 SLIP 服务器的用户 ID 下创建该用户 ID，并为新的用户 ID 分配密码。用户 ID 的实际名称并不重要，虽然按惯例所有 SLIP 登录 ID 都以大写 S 开头，后跟用户的姓名首字母（例如 `Sm d`）。用户 ID 必须以 `/usr/sbin/slcallback` 作为登录 shell，并且还必须具有 `remote` 类以便无需 SecureNet 身份验证即可登录。UID 和 GID 并不是很重要，只是 UID 必须在所有 SLIP 登录中唯一。SLIP 用户的 `/etc/passwd` 条目示例如下所示。

```
Srbm::500:9999:remote:0:0:Slip Callback (Rob Mackinnon): /tmp:/usr/sbin/slcallback
```

# Listing 13.6 (continued)

```c
/* fork early so that the lockfile gets our pid */
if (iff lag && fork() > 0)
    exit(0);

fd = conn(Rmtname);
if (fd < 0) {
    delock(Rmtname);
    fprintf(stderr, "%s: FAILED: %s\n", Progname, UERROR TEXT);
    cleanup(101);
}
/* slip login expects the tty on stdin */
(void)dup2(fd, 0);

/* XXX: pick between slip login or pppd */
pgm = *Progname == 's' ? _PATH_SLIPLOGIN : _PATH_PPPD;
name = ((name = strchr(pgm, '/')) != NULL) ? pgm : name + 1;
exec l(pgmname, name, slhost, (char *) 0);
exit (1);
```

下一步是设置 UUCP Systems 文件，以便 `slip login` 可以找到适当的电话号码和聊天脚本。编辑文件 `/etc/uucp/Systems.slip` 并添加类似以下的行，视情况替换用户 ID、电话号码和聊天脚本。对于基于 PC 的用户调用系统，由于 PC 不能允许登录到自身，省略聊天脚本并希望另一端的 PC 真的是你认为的那个人。如果另一端是 UNIX 机器，尝试使用特殊的 SLIP ID 登录该机器，他们必须创建该 ID。示例条目如下。

```
# Slip line entries for callback
# Rob MacKinnon (home, unix)
Srbm Any D_slip1 9600 55544618 in:\r\d-in: Stoppe word: foobar
Srbm Any D_slip2 9600 55544618 in:\r\d-in: Stoppe word: foobar
```

# Listing 13.6 (continued)
