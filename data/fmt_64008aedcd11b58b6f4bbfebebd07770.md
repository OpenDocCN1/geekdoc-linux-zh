
嗯，也许吧，如果你真的不介意骇客的话。

# 转移更新后的密码文件

在所有这些情况下，更新后的密码文件会被存放在一个“安全”的位置（一个空间充足的分区），然后一个脚本会将其复制到`/etc/passwd`，并进行适当的安全检查。该脚本可以像以下伪代码示例一样简单。

```
if [! -f /etc/ptmp ]; then
cp /some/safe/place/in/root /etc/ptmp
mv /etc/ptmp /etc/passwd
fi
```

这几乎就是我所做的，但没有竞态条件。代码位于客户端密码更新脚本中（清单 15.3）。

## 清单 15.3 客户端密码更新脚本将更新后的密码文件存放在一个空间充足的分区中，然后将其复制到`/etc/passwd`并进行适当的安全检查。

```
#!/bin/sh
#
# passwd-update -- update /etc/passwd from a copy of the master.
# Spends most of its time checking to see if it succeeded.
#
SAFEPLACE=/usr/local/etc/passwd # Place where the master puts it.
SAFEMINIMUM=25 # Smallest allowable /etc/passwd file size, in lines.

if ccopy $SAFEPLACE /etc/ptmp; then
: It was ok.
else
echo "$0: /etc/ptmp exists, therefore the /etc/passwd file"
echo " is locked. Try again later, please."
exit 0
fi
```

## 清单 15.4 客户端`ccopy`程序用于客户端密码更新脚本。

```
/*
 * ccopy - copy only if the target file does not exist. Used
 * to avoid race conditions. This is a classical unix
 * lock file creation mechanism: it's an atomic action.
 */
#include 
#include  /* For open(2). */
#include  /* For umask and fstat(2). */
#include 
#include  /* For error reporting. */
extern int sys_nerr;
extern char *sys_errlist[];

#define USERRR 1  /* Parameters messed up or missing. */
#define EXISTS 2  /* File exists, try again later. */
#define REALERR 3  /* Something bad happened. */
#define ERR (-1)  /* System's normal error value. */

char *ProgName = NULL; /* Name (ie, ccopy) for error reports. */
main(argc, argv) int argc; char *argv[]; {
    ProgName = argv[0];
    if (argc != 3) {
        (void) fprintf(stderr, "%s: Error - you must supply
        exactly two filenames.\n", ProgName);
        (void) fprintf(stderr, "%s - copy one file to another
        IFF the second doesn't exist\n", ProgName);
        (void) fprintf(stderr, "Usage: %s infile outfile\n",
        ProgName);
        exit(USERRR);
    }
    exit(ccopy(argv[1],argv[2]));
    /*NOTREACHED*/
}
```

## 但它安全吗？

安全性在这里在两个方面抬头：服务器上的安全性和传输通道的安全性。在服务器上，你面临提供一个无密码的特权账户或一个无密码的特权程序。这听起来很可怕，但事实上，这组程序的组合安全性与`/bin/passwd`的安全性完全一样。新增的程序仅验证一个人的身份，然后运行`/bin/passwd`。很容易阅读程序并确信它只做了它声称的事情。阅读`/bin/passwd`就更难了，你可能有也可能没有它的源代码。

```
oldUmask = umask((mode_t)0);
if ((outFd = open(outFile,O_CREAT|O_EXCL | O_WRONLY | O_TRUNC,
    status.st_mode)) == ERR) {
    switch (errno) {
    case EEXIST:
        rc = EXISTS;
        sayExists(outFile);
        break;
    default:
        rc = REALERR;
        sayOpenError(outFile,O_WRONLY,errno);
        break;
    }
    (void) umask(oldUmask);
    return rc;
}
while ((nread = read(inFd,buf,sizeof(buf))) != 0) {
    if (write(outFd,buf,nread) != nread) {
        rc = REALERR;
        sayWriteError(outFile,errno);
        break;
    }
}

(void) umask(oldUmask);

(void) close(inFd);
if (close(outFd) == ERR) {
    sayWriteError(outFile,errno);
    rc = REALERR;
}
return 0;
```

SUID root 程序存在一个额外的风险。因为它们通常从用户的账户开始运行，所以它们必须非常小心地设置其`$PATH`、共享库搜索路径等等。在我们的例子中，我们总是从系统管理员控制下的账户运行，因此我们只需要使环境与 root 相同。出于这个原因，`passwd`是该账户的 shell，且环境非常精简。

```
/*
 * error reporters -- for open, existence and write errors.
 */
sayExists(outFile) char *outFile; {
    (void) fprintf(stderr, "%s: Error - file %s already exists,\n"
                   "    try again later.\n", ProgName,outFile);
    return;
}

sayOpenError(name,readWriteOrStat,errno) char *name;
    int readWriteOrStat, errno;
    char *operation;
{
    switch (readWriteOrStat) {
    case R_OK:
        operation = "stat input";
        break;
    case O_RDONLY:
        operation = "read input";
        break;
    case O_WRONLY:
        operation = "create output";
        break;
    }
    (void) fprintf(stderr, "%s: can't %s file \"%s\", %s (errno %d).\n"
                   "    halting.\n", ProgName, operation, name,
                   (errno < sys_nerr) ? sys_errlist[errno] :
                   "Unknown error", errno);
    return;
}
```

## 网络安全
