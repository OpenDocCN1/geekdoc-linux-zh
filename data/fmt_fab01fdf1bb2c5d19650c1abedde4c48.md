
```
/usr/local/sbin:/usr/local/bin:/sbin:/usr/sbin:/bin:/usr/bin
```

请注意，`root`的路径中没有任何与`X`窗口相关的程序。然而，两者都共享一些公共目录：`/usr/local/bin`、`/bin`和`/usr/bin`。出于安全原因，`root`在其`PATH`中排除了`X`；`root` `PATH`中的目录越少，`root`账户受到特洛伊木马破坏的可能性就越小。

### 你的常用工具

当一个账户在其`PATH`中定义了某个目录时，它就可以访问该目录中的所有文件（前提是权限设置正确）。例如，许多用户账户在`PATH`中包含了`/usr/local/bin`，如清单 5-2 所示。该目录中的任何可执行文件都可以被用户访问。

**清单 5-2：查看 `/usr/local/bin` 目录**

```bash
$ ls -l /usr/local/bin
total 3604
lrwxrwxrwx 1 root root     21 Jun 20 11:47 make-ssh-known-hosts -> make-ssh-known-hosts1
lrwxrwxrwx 1 root root     21 Jun 20 11:42 make-ssh-known-hosts.old -> make-ssh-known-hosts1
-rw-r-xr-x 1 root root   20564 Jun 20 11:47 make-ssh-known-hosts1
-rwxr-xr-x 1 root root   20564 Jun 20 11:42 make-ssh-known-hosts1.old
lrwxrwxrwx 1 root root       28 Jun 20 03:58 netcape -> /usr/local/netcape/netcape
lrwxrwxrwx 1 root root       4 Jun 20 11:47 scp -> scp1
lrwxrwxrwx 1 root root       4 Jun 20 11:42 scp1.old -> scp1
-rwxr-xr-x 1 root root   86790 Jun 20 11:47 scp1
-rwxr-xr-x 1 root root   86790 Jun 20 11:42 scp1.old
lrwxrwxrwx 1 root root       3 Jun 20 11:47 slogin -> ssh
lrwxrwxrwx 1 root root       4 Jun 20 11:47 ssh -> ssh1
lrwxrwxrwx 1 root root       8 Jun 20 11:47 ssh-add -> ssh-add1
lrwxrwxrwx 1 root root       8 Jun 20 11:42 ssh-add.old -> ssh-add1
lrwxrwxrwx 1 root root    339747 Jun 20 11:47 ssh-add1
-rwxr-xr-x 1 root root    339747 Jun 20 11:42 ssh-add1.old
lrwxrwxrwx 1 root root      10 Jun 20 11:47 ssh-agent -> ssh-agent1
lrwxrwxrwx 1 root root      10 Jun 20 11:42 ssh-agent.old -> ssh-agent1
-rwxr-xr-x 1 root root    346874 Jun 20 11:47 ssh-agent1
-rwxr-xr-x 1 root root    346874 Jun 20 11:42 ssh-agent1.old
lrwxrwxrwx 1 root root      12 Jun 20 11:47 ssh-askpass -> ssh-askpass1
lrwxrwxrwx 1 root root      12 Jun 20 11:42 ssh-askpass.old -> ssh-askpass1
-rwxr-xr-x 1 root root    103417 Jun 20 11:47 ssh-askpass1
-rwxr-xr-x 1 root root    103417 Jun 20 11:42 ssh-askpass1.old
lrwxrwxrwx 1 root root      11 Jun 20 11:47 ssh-keygen -> ssh-keygen1
lrwxrwxrwx 1 root root      11 Jun 20 11:42 ssh-keygen.old -> ssh-keygen1
-rwxr-xr-x 1 root root    330283 Jun 20 11:47 ssh-keygen1
-rwxr-xr-x 1 root root    330283 Jun 20 11:42 ssh-keygen1.old
```

## 118 第二部分：系统管理实战

```
lrwxrwxrwx  1 root     root        4 Jun 20 11:42 ssh.old -> ssh1
-rwxr-xr-x  1 root     root    598476 Jun 20 11:47 ssh1
-rwxr-xr-x  1 root     root    598476 Jun 20 11:42 ssh1.old
lrwxrwxrwx  1 root     root       24 Jun 20 03:58 vreg -> /usr/local/netescape/vreg
```

`/bin` 目录列出了大多数系统二进制文件。这包括用户 shell、基本的文件命令（如`ls`、`mv`和`cp`）、基本邮件命令，以及许多与进程相关的命令（如`ps`）。这些命令供任何需要它们的用户使用，而不仅仅是系统管理员。

列表 5-3 显示了`Slackware` `/bin` 目录的内容，在其他`UNIX`操作系统中可能有所不同。

### 列表 5-3：查看 `/bin` 目录
