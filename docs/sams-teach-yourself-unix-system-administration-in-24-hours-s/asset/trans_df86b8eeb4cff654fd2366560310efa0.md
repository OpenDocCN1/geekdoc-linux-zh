
```
if [ "$1" = "" ] ; then
echo Usage: 'basename $0' account
exit 0
fi
if [ "`whoami`" != "root" ] ; then
echo `basename $0`: Error. You must be 'root' to run this command.
exit 0
fi

passwd $1

# Now, let's see if they're logged in, and if so, boot 'em

if [ "`who` | grep $1`" != "" ] ; then
tty=`who | grep $1 | tail -1 | awk '{print $2}'`
cat << "EOF" > /dev/$tty
**************************************************
URGENT NOTICE FROM THE ADMINISTRATOR:
This account is being suspended by the request of management.
You are going to be logged out in $secs seconds. Please shut down
any processes you have running immediately.

If you have any questions, please contact your supervisor or
Jane Mansmith, director of information technology.
**************************************************
EOF

echo "(Warned $1, now sleeping $secs seconds)"
sleep $secs

sid=`ps -u $1 | awk '{print $3}' | tail -1`
kill -HUP $sid
echo "$1 was logged in. Just logged $1 out."
fi

# Finally, let's close off their home directory from prying eyes:
chmod 000 $homedir/$1

echo "Account $1 has been suspended."
exit 0
```

- 4. 当我们准备将 testdude 从其账户中踢出时，现在很容易了：
- $ suspend testdude
- 正在更改用户 testdude 的密码

New password:
Retype new password:
passwd: all authentication tokens updated successfully
(Warned testdude, now sleeping 10 seconds)
testdude was logged in. Just logged testdude out.
Account testdude has been suspended.

The user testdude would have seen the following pop up on his screen:
**************************************************
URGENT NOTICE FROM THE ADMINISTRATOR:

This account is being suspended by the request of management.
You are going to be logged out in 10 seconds. Please shut down
any processes you have running immediately.

If you have any questions, please contact your supervisor or
Jane Mansmith, director of information technology.
**************************************************

And, sure enough, ten seconds later testdude would be logged out and unable to log back in.

![](img/5ced0c78d748bd190e9027e5549a3622_127_0.png)

Compatibility-wise, the third field of the ps output on BSD systems is the parent process ID (PPID) rather than the session ID. The good news is that it'll work just as well for this task, so the script works across platforms, with but one small change necessary: homedir must be defined as appropriate for each server.

- 4. 在挂起后重新启用账户足够简单，我将只展示执行此操作的 shell 脚本（unsuspend）片段：

```
passwd $1   # change their password back to a known value
chmod 750 $homedir/$1  # and open their home directory back up
```

There are other ways to suspend accounts on some Unix systems that are worth mentioning. If you're running Linux, for example, there's usermod, which lets root change the status of a user account. With the -L flag, it locks the account, disabling the password by prefixing the encrypted password string with a !, and with -U it removes that ! and enables the account again.

Solaris uses the passwd command to enable suspension: passwd -l acct will lock the specified account (specifying a new password with the standard passwd acct will unlock the account again).

On BSD systems, it's a bit more tricky, because there isn't a command as accessible as usermod by default. That's why it's easier just to change the user's password to something else, as shown in the script.

## Deleting User Accounts

Suspending accounts is helpful, but often you'll need to completely remove the account from the system, including deleting all the files. Another relatively simple task, but if you want to do everything properly, you might find that there are more nuances than initially expected.

### Task 6.2: Deleting User Accounts

The most important step in deleting a user account is to remove the entry from the /etc/passwd file. With that done, the user ceases to exist as far as the Unix system is concerned. However, the user still has files in the system, a home directory, and perhaps also e-mail coming into the system and more. But let's take one step at a time.

- 1. 一旦确定某人不再需要，并且永远不再需要访问系统，就该删除账户了。这最简单的方法是从 /etc/passwd 文件（或 NetInfo 数据库）中删除用户的条目，然后使用 rm 命令的危险 '-rf' 标志强制递归删除用户主目录内的所有文件和文件夹。

Deleting a line from the password file is superficially easy within a script:

```
grep -vE "$1": /etc/passwd > /tmp/newpasswd
mv /tmp/newpasswd /etc/passwd
chmod 655 /etc/passwd
```

![](img/5ced0c78d748bd190e9027e5549a3622_128_0.png)

> The problem with this solution is that you need to prevent any other system administrator from touching or changing the /etc/passwd file while you're doing this. In Unix terms, it's called locking the file, and there's no easy solution to this dilemma overall.
> 
> On some Unix systems—including RHL7.2—there's a user-level command lockfile, but although it will help ensure that two accounts aren't deleted at the same time, it only works for scripts that you've written. The danger, however, is with all the other commands that might alter the file (including the passwd command on a non-shadow password system).
> 
> A better solution is to use vipw, a special file-locking version front end to vi that locks the password file, lets you edit it, then unlocks it when done. Fortunately, vipw is available on Red Hat Linux, Solaris, and Darwin.

- 2. 所需的第二步是在脚本中删除用户的主目录及其所有内容，假设 $1 是用户的账户名：

```
rm -rf $homedir/$1
```

There's a nuance to this, however, because the user might very well have files elsewhere on the system.

- 3. 查找这些散落的文件是 find 命令的工作，它将在整个文件系统中搜索用户拥有的任何剩余文件或目录。

For example:

```
$ find / -uid 501 -print
```

/var/spool/mail/mdella

In this case, you can see that though you've stripped all the files in the /home directory, there was still an e-mail mailbox lingering in the spool directory.

One ramification of adding this check for files outside the user's home directory is that you need to grab the UID of the account before deleting it. This is done with the line

```
uid="`egrep "^$1:" /etc/passwd | cut -d: -f3`"
```

- 4. 以下是完整的脚本，除了从 shadow 文件中删除账户信息之外。请注意，第一步是调用 suspend 脚本以确保用户无法登录，并在需要时注销。没有理由在这里重复该代码！

```
#!/bin/sh

## Delete - delete a user account without a trace...

homedir="/home"

if [ "$1" = "" ] ; then
 echo Usage: `basename $0` account; exit 0
fi
if [ "`whoami`" != "root" ] ; then
 echo `basename $0`: Error. You must be 'root' to run this command.
 exit 0
fi

suspend $1  # suspend their account while we do the dirty work

uid=`egrep "^$1:" /etc/passwd | cut -d: -f3`

egrep -v "^$1:" /etc/passwd > /tmp/newpasswd
mv /tmp/newpasswd /etc/passwd
chmod 655 /etc/passwd

rm -rf $homedir/$1
```

```
echo "Files still left to remove (if any):"
find / -uid $uid -print

echo "Account $1 (uid $uid) has been deleted, and their /home *"
echo "directory has been removed."
exit 0
```

- 5. 反思一下，更明智的做法是将用户的主目录移动到不同的临时暂存区，以防第二天有人请求某些文件。为此，请将 rm -rf 调用替换为

```
mv $homedir/$1 $holdingarea
```

The variable $holdingarea should be somewhere secure, with minimal access. A good location would be /home/root/pending_deletion or someplace similar.

- 6. deleteuser 的 Darwin 版本有点不同，因为您无需从 /etc/passwd 文件中提取行，而是可以使用更安全的 niutil 命令：

```
niutil -destroy ./users/$1
```

One significant advantage to the Darwin version is that there's no worry about the potential danger from not using a file locking protocol—NetInfo itself automatically ensures that commands don't step on each other.

![](img/5ced0c78d748bd190e9027e5549a3622_130_0.png)

> It would be wise to include a test in the deleteuser script to flag and refuse to delete the root account. If you accidentally deleted that account, the results would be very bad. It's recoverable (boot in single-user mode and fix the password file or NetInfo database), but very, very bad.

Deleting accounts proves to be more than just deleting a line from the /etc/passwd file. Indeed, there's an additional step necessary for a deleted account that we won't address until Hour 18, "Running Your Own Name Server"—setting up an automatic e-mail response informing people that the user is no longer accessible through this system.

Rather than fall too far into the trap of the "not invented here syndrome," however, let's spend the rest of this hour looking at some of the platform-specific account management tools available in Linux, Solaris, and Darwin.

## Linux Account Management Tools

Lurking under the hood of the simple passwd command in Linux (and Solaris, for that matter) is a powerful set of options that can significantly simplify your administrative tasks. They're different on each platform, alas, but if you're in a relatively homogeneous
