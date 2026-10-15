
`sudo`（清单 5.1）是一个 `set-user-id` 程序，以 `root` 身份运行，允许授权用户执行其获批准的命令。`sudo` 最初由 SUNY-Buffalo 的 Cliff Spencer 编写，并发表在 Evi Nemeth 的《UNIX 系统管理手册》中。`sudo` 最初编写时用于在 BSD UNIX 下运行。

原始的 `sudo` 遗留了一些未完成的工作。这些包括能够从像 `vi` 这样的程序中 `shell` 出来，使用 `root` 的路径，必须完全限定要执行的命令，必须指定可以执行的全部命令而不能指定不可执行的命令，以及能够指定“所有”命令，从而允许用户自由操作。用户也可以 `sudo` 一个 `shell`，从而绕过日志记录机制。

原始的 `sudo` 使用 `root` 的完整环境，包括 `root` 的 `shell` 和路径。我添加了 `putenv` 命令将 `shell` 设置为 `/bin/false`，并为 `sudo` 可以运行的命令分配了一个路径。重新分配 `shell` 变量可防止像 `vi` 这样的程序生成子 `shell`。分配路径限制了可以用 `sudo` 执行的命令范围。它还消除了为命令完全限定路径名的需要。我在配置文件中添加了 `not` 选项，允许你将某人配置为运行除所列命令之外的所有命令。

### Listing 5.1 The revised sudo.c

```
/*
** sudo.c
*/

/*
** Configurable constants
*/

#define SECURE_PATH "/bin:/usr/bin:/etc"
#define USERFILE "/usr/local/adm/sudoers"
#define LOGFILE "/usr/local/adm/sudolog"
#define TIMEDIR "/usr/local/adm/sudocheck/"
#define TIME 5 /* minutes */
#define SUDO_COP "root@localhost"

/*
** To install create the directories in the SECURE_PATH
** and TIMEDIR and the files USERFILE and LOGFILE.
** Set the owner of these files to root and the permissions
** to og-rw. Change the owner to root for the sudo program
** and set the permissions to 4111 (-s--x--x).
*/

#define BUFSIZE 256
#define SUCCESS 1
#define FAILED -1

#define CONFIG_ERR "Configuration error. Contact your security manager."
#define CONFIG_SUB "Invalid sudo configuration!"
#define SUID_ERR "Set UID bit not set."
#define STAT_ERR "Couldn't stat user file"
#define OWNER_ERR "User file not owned by root"
#define PERM_ERR "Invalid permissions on user file"
#define OPEN_ERR "Couldn't open user file"

#define USER_ERR "You are not set up to execute sudo on this machine."
#define USER_SUB "SECURITY** Invalid sudo user!"

#include <ctype.h>
#include <fcntl.h>
#include <pwd.h>
#include <signal.h>
#include <stdio.h>
#include <string.h>
#include <sys/file.h>
#include <sys/param.h>
#include <sys/stat.h>
#include <sys/time.h>
#include <sys/types.h>
```

### Listing 5.1 (continued)

```
char *getpass();
char *crypt();

FILE *check_config(user)
char *user;
{
    struct stat statb;
    FILE *fp;

    if ((setuid(0)) < 0)                        /* no setuid */
        mail(CONFIG_SUB,user,SUID_ERR,CONFIG_ERR);
    if (stat(USERFILE, &statb))                 /* couldn't stat */
        mail(CONFIG_SUB,user,STAT_ERR,CONFIG_ERR);
    if (statb.st_uid != 0)                      /* must be owned by root */
        mail(CONFIG_SUB,user,OWNER_ERR,CONFIG_ERR);
    if ((statb.st_mode & 044)                   /* should be og-rw */
        mail(CONFIG_SUB,user,PERM_ERR,CONFIG_ERR);
    if ((fp = fopen(USERFILE, "r")) == 0)      /* open err */
        mail(CONFIG_SUB,user,OPEN_ERR,CONFIG_ERR);

    return(fp);
}

char *get_command_list(fp, name, password)
FILE *fp;
char *name;
char *password;
{
    char buffer[BUFSIZ];

    while ((fgets(buffer,BUFSIZ,fp)) != NULL)
    {
        if(buffer[0] == '#') continue;          /* skip remarks */
        if((strncmp(buffer,name,strlen(name))) == 0)
        {
            if (get_password(name,password))   /* valid user */
                return(buffer);
            else
                return(NULL);                   /* invalid password */
        }
    }

    return(NULL);                               /* invalid user */
}
```

## 安全问题

向普通用户授予某些超级用户权限并依赖其登录密码进行安全保护很可能会导致安全问题。如果拥有 `sudo` 权限的用户密码强度不足、共享密码或密码被盗，那么授予该用户的超级用户权限也将被攻破。以下文本列出了您可以采取的若干措施来限制这种风险。

- 要求用户使用良好的密码。
- 仅向真正需要 `sudo` 权限的用户授予该权限。
- 仅向用户授予其所需的命令的 `sudo` 访问权限。
- 监控日志文件以查看用户正在做什么。

某些命令不应授予 `sudo` 用户。例如，某些命令会绕过日志记录程序。这些命令会生成交互式 `shell` 或用另一个进程替换 `sudo` 进程。其中包括 `sh`、`ksh`、`csh`、`rsh`（受限 `shell`）和 `exec`。其他命令会增加对其他系统的风险，尤其是在可信计算机基座中。这些是 `rlogin` 和 `remsh`（远程 `shell`，某些系统上的 `rsh`）。这些程序允许您在无需密码的情况下登录另一台计算机。还有其他命令，例如 `chmod` 和 `chown`，可用于强行获取额外权限，并可用于创建可在 `sudo` 之外执行的 `set-UID` `shell`。

## 安全措施

配置文件、日志文件和时间目录的位置应仅为安全管理员所知。任何知道这些文件位置的用户都可以操纵它们以向配置文件添加用户或命令、向安全路径中添加通过 `sudo` 执行的命令，或篡改日志文件。隐藏这些文件位置的一种方法是将其放在隐藏目录中，即目录名以句点开头、任何人都无读取或写入权限且属主为 `root` 的目录。实际上，使用无法键入的目录名会更好。仅应将要执行的命令放在此目录中，并且这些命令的权限应为仅执行，无读取或写入权限。
