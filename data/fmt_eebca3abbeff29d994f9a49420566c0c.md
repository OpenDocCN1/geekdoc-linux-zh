
这可以通过简单地将用户的密码更改为他们不知道的新值来实现，但如果用户当时已登录，也很重要将其注销并关闭系统上其他账户对该主目录的访问。当账户被挂起时，很可能用户需要立即离开系统——而不是他们想离开的时候。

清单 5-16 中的大部分脚本都围绕着确定用户是否已登录、通知用户将被注销以及将用户踢出系统。

### 代码

```bash
#!/bin/bash

# suspenduser--Suspends a user account for the indefinite future

homedir="/home"     # Home directory for users
secs=10               # Seconds before user is logged out

if [ -z $1 ] ; then
    echo "Usage: $0 account" >&2
    exit 1
elif [ "$(id -un)" != "root" ] ; then
    echo "Error. You must be 'root' to run this command." >&2
    exit 1
fi

echo "Please change the password for account $1 to something new."
passwd $1

# Now let's see if they're logged in and, if so, boot 'em.
if who|grep "$1" > /dev/null ; then

for tty in $(who | grep $1 | awk '{print $2}'); do

cat << "EOF" > /dev/$tty

**************************************************************
URGENT NOTICE FROM THE ADMINISTRATOR:

This account is being suspended, and you are going to be logged out
in $secs seconds. Please immediately shut down any processes you
have running and log out.

If you have any questions, please contact your supervisor or
John Doe, Director of Information Technology.
***************************************************************
EOF
done

echo "(Warned $1, now sleeping $secs seconds)"

sleep $secs
```

```bash
jobs=$(ps -u $1 | cut -d\  -f1)
① kill -s HUP $jobs          # Send hangup sig to their processes.
sleep 1
② kill -s KILL $jobs > /dev/null 2>&1 # and kill anything left.
echo "$1 was logged in. Just logged them out."
fi
# Finally, let’s close off their home directory from prying eyes.
chmod 000 $homedir/$1
echo "Account $1 has been suspended."
exit 0
```

清单 5-16：`suspenduser` 脚本

## 工作原理

此脚本将用户的密码更改为用户不知道的值，然后关闭用户的主目录。如果他们已登录，我们会给出几秒钟的警告，然后通过终止他们运行的所有进程将其注销。

注意脚本如何向每个运行进程发送 `SIGHUP`（`HUP`）挂断信号 ①，然后等待一秒后再发送更强力的 `SIGKILL`（`KILL`）信号 ②。`SIGHUP` 信号会退出正在运行的应用程序——除了并不总是如此，它不会杀死登录 shell。`SIGKILL` 信号则无法被忽略或阻止，因此保证 100% 有效。不过它并不被首选，因为它不会给应用程序任何时间清理临时文件、刷新文件缓冲区以确保更改写入磁盘等。

恢复用户挂起是一个简单的两步过程：重新打开其主目录（使用 `chmod 700`）并将密码重置为已知值（使用 `passwd`）。

## 运行脚本

此脚本必须以 `root` 身份运行，且有一个参数：要挂起的账户名称。

## 结果

事实证明 `snowy` 已经在滥用他的账户。让我们挂起他，如清单 5-17 所示。

```
$ sudo suspenduser snowy
Please change the password for account snowy to something new.
Changing password for user snowy.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```

(Warned snowy, now sleeping 10 seconds)

snowy 已登录。刚刚将其注销。

账户 snowy 已被暂停。

### Listing 5-17: 在用户 snowy 上测试 suspenduser 脚本

由于 `snowy` 在当时已登录，Listing 5-18 显示了他被踢出系统前几秒在屏幕上看到的内容。

```
************************************************************************
URGENT NOTICE FROM THE ADMINISTRATOR:

This account is being suspended, and you are going to be logged out
in 10 seconds. Please immediately shut down any processes you
have running and log out.

If you have any questions, please contact your supervisor or
John Doe, Director of Information Technology.
************************************************************************
```

### Listing 5-18: 在用户被暂停前打印到用户终端的警告

## #42 删除用户账户

删除账户比暂停它要棘手一些，因为脚本需要在从 `/etc/passwd` 和 `/etc/shadow` 中删除账户信息之前检查整个文件系统是否存在用户拥有的文件。Listing 5-19 确保用户及其数据被完全从系统中删除。它期望之前的 `suspenduser` 脚本位于当前 `PATH` 中。

### The Code

```bash
#!/bin/bash

# deleteuser--Deletes a user account without a trace.
# Not for use with OS X.

homedira="/home"
pwfile="/etc/passwd"
shadow="/etc/shadow"
newpwfile="/etc/passwd.new"
newshadow="/etc/shadow.new"
suspenda="$(which suspenduser)"
locker="/etc/passwd.lock"

if [ -z $1 ] ; then
echo "Usage: $0 account" >&2
exit 1
elif [ "$(whoami)" != "root" ] ; then
echo "Error: you must be 'root' to run this command." >&2
exit 1
fi
```

通过创建文件 `/etc/passwd.lock` 实现相对原始的信号量锁定机制。如果锁文件已存在 ①，此脚本将等待另一个程序将其删除；一旦消失，`deleteuser` 会立即创建它并继续进行 ②，并在完成后将其删除 ③。

### Running the Script

此脚本必须以 `root` 身份运行（使用 `sudo`），并且需要作为命令行参数提供要删除的账户名称。Listing 5-20 显示了该脚本在用户 `snowy` 上的运行情况。

> WARNING
>
> 此脚本不可逆且会导致大量文件消失，因此如果你想尝试使用它，请务必小心！

### The Results
