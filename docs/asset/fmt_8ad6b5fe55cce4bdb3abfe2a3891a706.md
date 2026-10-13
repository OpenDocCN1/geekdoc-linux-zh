
**************************************************

URGENT NOTICE FROM THE ADMINISTRATOR:

This account is being suspended by the request of management.

You are going to be logged out in 10 seconds. Please shut down any processes you have running immediately.

If you have any questions, please contact your supervisor or Jane Mansmith, director of information technology.

**************************************************

And, sure enough, ten seconds later testdude would be logged out and unable to log back in.

![](img/5ced0c78d748bd190e9027e5549a3622_127_0.png)

Compatibility-wise, the third field of the `ps` output on BSD systems is the parent process ID (`PPID`) rather than the session ID. The good news is that it'll work just as well for this task, so the script works across platforms, with but one small change necessary: `homedir` must be defined as appropriate for each server.

### 4. 在挂起后重新启用账户足够简单，我将只展示执行此操作的 shell 脚本（`unsuspend`）片段：

```
passwd $1   # change their password back to a known value
chmod 750 $homedir/$1  # and open their home directory back up
```

There are other ways to suspend accounts on some Unix systems that are worth mentioning. If you're running Linux, for example, there's `usermod`, which lets root change the status of a user account. With the `-L` flag, it locks the account, disabling the password by prefixing the encrypted password string with a `!`, and with `-U` it removes that `!` and enables the account again.

Solaris uses the `passwd` command to enable suspension: `passwd -l acct` will lock the specified account (specifying a new password with the standard `passwd acct` will unlock the account again).

On BSD systems, it's a bit more tricky, because there isn't a command as accessible as `usermod` by default. That's why it's easier just to change the user's password to something else, as shown in the script.

#### Deleting User Accounts

Suspending accounts is helpful, but often you'll need to completely remove the account from the system, including deleting all the files. Another relatively simple task, but if you want to do everything properly, you might find that there are more nuances than initially expected.

##### Task 6.2: Deleting User Accounts

The most important step in deleting a user account is to remove the entry from the `/etc/passwd` file. With that done, the user ceases to exist as far as the Unix system is concerned. However, the user still has files in the system, a home directory, and perhaps also e-mail coming into the system and more. But let's take one step at a time.

- 1. 一旦确定某人不再需要，并且永远不再需要访问系统，就该删除账户了。这最简单的方法是从 `/etc/passwd` 文件（或 NetInfo 数据库）中删除用户的条目，然后使用 `rm` 命令的危险 `'-rf'` 标志强制递归删除用户主目录内的所有文件和文件夹。

Deleting a line from the password file is superficially easy within a script:

```
grep -vE "$1": /etc/passwd > /tmp/newpasswd
mv /tmp/newpasswd /etc/passwd
chmod 655 /etc/passwd
```

![](img/5ced0c78d748bd190e9027e5549a3622_128_0.png)

> The problem with this solution is that you need to prevent any other system administrator from touching or changing the `/etc/passwd` file while you're doing this. In Unix terms, it's called locking the file, and there's no easy solution to this dilemma overall.

> On some Unix systems—including RHL7.2—there's a user-level command `lockfile`, but although it will help ensure that two accounts aren't deleted at the same time, it only works for scripts that you've written. The danger, however, is with all the other commands that might alter the file (including the `passwd` command on a non-shadow password system).

> A better solution is to use `vipw`, a special file-locking version front end to `vi` that locks the password file, lets you edit it, then unlocks it when done. Fortunately, `vipw` is available on Red Hat Linux, Solaris, and Darwin.

- 2. 所需的第二步是在脚本中删除用户的主目录及其所有内容，假设 `$1` 是用户的账户名：

```
rm -rf $homedir/$1
```

There's a nuance to this, however, because the user might very well have files elsewhere on the system.
