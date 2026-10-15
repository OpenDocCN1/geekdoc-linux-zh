

logintimes 此用户的登录次数。语法与 /etc/security/login.cfg 中的相同。

pwdwarntime 提示消息中指示需要更改密码的天数。

pwdchecks 定义本地密码验证程序（清单 9.1）。

dictlist 用于密码检查的密码字典文件名。该文件每行包含一个单词。如果新密码在此文件中找到，则密码将被拒绝。

loginretries 在账户被禁用之前失败的登录次数。

histexpire 密码可被重用的时间（以周为单位）。

histsize 用户不能重用的以前密码的数量。

## 图 9.3 一个示例 /etc/security/user 文件。

```
default:

  ttys = ALL
  auth1 = SYSTEM
  auth2 = NONE
  SYSTEM = "compat"
  pwdwarntime = 3
  pwdchecks = /usr/local2/adm/checkpwd
  dictlist = /usr/local2/adm/pwddictionary
  loginretries = 3
  histexpire = 52
  histsize = 25
  minalpha = 1
  minother = 1
  mindiff = 1
  maxrepeats = 2
  minlen = 6
  maxage = 8
  minage = 1

richter:

  logintimes = 10
```

第二个部分的示例

minalpha 密码中字母字符的最小数量。

minother 密码中非字母字符的最小数量。

mindiff 旧密码和新密码之间必须不同的字符的最小数量。

maxrepeats 字符在密码中可以出现的最大次数。

minlen 密码的最小长度。

maxage 密码有效的最大周数。

minage 密码可以被更改前的最小周数。

## 清单 9.1 checkpwd.c 是一个用于扩展密码验证的本地程序。

```
/*
** Password extension function.
**
** Function must have the interface
**   char *user - User name for which invoked
**   char *new - New password in clear text
**   char *old - Old password in clear text
**   char **message - Error Message, must be allocated from heap.
**                 Caller will call free().
**
** Compile with
**   cc -e checkpwd -o checkpwd checkpwd
**
** Return false when password contains userid, otherwise return true.
*/

#include <string.h>

int checkpwd(char *user, char *new, char *old, char **message)
{
    char *error = "Userid must not be part of password\n";

    *message = NULL;
    if( strstr(new, user) != NULL )
        return 0;
    *message = strdup(error);
    return 1;
}
```

图 9.3 中的默认配置要求用户每八周更改一次密码。密码必须至少包含一个字母字符和一个非字母字符，并且每个字符最多可重复一次。新的密码会与字典文件 /usr/local/adm/pwdict/dictionary 进行检查，并使用位于 /usr/local/adm/checkpwd 的本地开发的可加载模块进行验证。密码在一年内不能被重用，并且每个新密码必须与之前的 25 个密码不同。密码到期前三天，用户在登录时会收到提醒。周日的登录被禁用。

密码历史已启用；编码后的密码、更改时间以及所属的用户 ID 存储在 /etc/security/pwdhist.dir 中。Root 拥有此文件，并且是唯一具有读写权限的用户。

## 日志记录

文件 /etc/security/lastlog 和 /etc/security/failedlogin 记录每个用户的失败登录尝试。记录包括时间、日期、终端、用户 ID、远程主机，以及自上次成功登录以来不成功的尝试次数（有关 AIX v3 登录配置的详细描述以及用于自动化登录监控的工具，请参阅第 8 章）。如果不成功的登录尝试次数超过 loginretries 值，则账户会被记录，并在用户尝试登录时发出警告消息。

/etc/security/portlog 为每个端口包含失败登录发生的时间以及端口被锁定的时间。两者在端口重新启用时都会被重置。不成功的登录时间和次数与 logininterval 和 logindisable 的值进行比较，以确定端口是否应被锁定。

## 扩展密码验证

正如我前面所述，您可以为 AIX v4 的密码验证函数编写自己的扩展。扩展密码验证需要您编写一个 C 程序，例如 checkpwd.c（清单 9.1）并创建动态可加载对象文件 [6]。编译示例代码时使用 -e checkpwd 选项。这会导致编译器使用 checkpwd() 作为入口点而不是 main()。

您可以使用除 main() 之外的任何函数名。登录过程使用 "load system" 调用加载 pwdchecks 属性中列出的文件。系统调用返回使用 -e 选项指定的函数的地址，然后调用该函数。函数的返回值表示成功（0）或失败（任何其他值）。返回的错误消息的内存必须从堆中分配；登录过程将释放它。

