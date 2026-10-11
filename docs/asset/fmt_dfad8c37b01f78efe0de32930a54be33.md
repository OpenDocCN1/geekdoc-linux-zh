
因此，要设置文件的权限为 `rwxr-xr-x`，可以这样使用 `chmod` 命令：

```
chmod 755 perm
```

若要添加 `setuid` 权限，请在结果值中加上 `4000`。若要设置 `setgid` 权限，请加上 `2000`。若要同时设置 `setuid` 和 `setgid` 权限，请加上 `6000`。例如，要在文件所有者拥有读和写权限的同时设置 `setuid` 权限，请这样执行 `chmod`：

```
chmod 4600 perm
```

## 全局可读文件

定期审计全局可读文件是个好习惯。恶意用户常常寻找包含关键信息的全局可读文件，这些信息可能有助于他们进行权限提升。

使用 `find` 命令搜索全局可读文件：

```
find /etc -type f -perm -4 -print 2> /dev/null
```

## 全局可写文件

全局可写文件可能被恶意用户利用以获取 `root` 权限。考虑一个被设置为所有人可写的 `setuid` 可执行脚本。恶意用户可以编辑此类脚本，以 `root` 身份执行任何命令。

使用 `find` 命令搜索全局可写文件：

```
find / -type f -perm -2 -print 2> /dev/null
```

## 由 bin 和 sys 拥有的文件

某些发行版错误地将可执行文件的属主设置为非 `root` 用户，如 `bin` 和 `sys`。

例如，假设 `/usr/bin/in.telnnet` 由用户 `bin` 拥有且可写。如果攻击者成功以用户 `bin` 的权限挂载服务器的 NFS `/usr/bin` 共享目录，他或她就可以用特洛伊木马替换 `/usr/bin/in.telnetd`，该木马将在每次收到传入 `telnet` 连接时由 `inetd` 或 `xinetd` 以 `root` 权限执行。

要检查 `bin` 拥有的文件，运行以下命令：

```
find / -user bin -print 2> /dev/null
```

类似地，使用以下命令检查 `sys` 拥有的文件：

```
find / -user sys -print 2> /dev/null
```

## umask 值

每当创建新文件或目录时，会根据 `umask` 值赋予默认权限。使用 `umask` 命令查看当前用户的 `umask` 值：

```
[bash]$ umask -p umask 0002
```

`umask` 的值是通过将文件权限八进制值与文件对应的 `666` 或目录对应的 `777` 进行异或 `XOR` 运算确定的。对于文件，请注意 `umask` 值不允许设置执行 `x` 权限。

`XOR` 代表“异或”。以下是 `XOR` 的真值表：

| XOR | 0 | 1 |
|---|---|---|
| 0 | 0 | 1 |
| 1 | 1 | 0 |

假设我们希望 `umask` 值指示文件所有者拥有读写权限，而组或其他用户没有任何权限。此外，假设我们希望目录的 `umask` 包含执行 `x` 权限。如果目录没有执行 `x` 权限，则无法 `cd`（更改目录）进入该目录。这种设置的文件权限值为 `700`，分解为八进制表示为：

```
111 000 000
```

使用上面的表，让我们将此值与 `777` 异或，以获得合适的 `umask` 值：

```
111 000 000 : 700
111 111 111 : 777
XOR: 000 111 111 : 077
```

使用 `umask` 命令设置新的 `umask` 值：

```
umask 077
```

推荐的 `umask` 值是 `077`。这使得每个新创建的文件或目录只能由其所有者读写。

请注意，`umask` 值由三组八进制位组成，即三组八位。编译器创建的文件通常遵循 `umask` 值（除了 `x` 位）。

## 重要文件

确保以下文件已分配正确的权限：

| 文件名 | 用户 | 组 | 权限 |
| :--- | :--- | :--- | :--- |
| `/bin` | root | root | drwxr-xr-x |
| `/etc` | root | root | drwxr-xr-x |
| `/etc/aliases` | root | root | -rw-r--r-- |
| `/etc/default/login` | root | root | -rw------- |
| `/etc/exports` | root | root | -rw-r--r-- |
| `/etc/hosts` | root | root | -rw-r--r-- |
| `/etc/hosts.allow` | root | root | -rw------- |
| `/etc/hosts.deny` | root | root | -rw------- |
| `/etc/hosts.equiv` | root | root | -rw------- |
| `/etc/hosts.lpd` | root | root | -rw------- |
| `/etc/inetd.conf` | root | root | -rw------- |
| `/etc/issue` | root | root | -rw-r--r-- |
| `/etc/login.access` | root | root | -rw------- |
| `/etc/login.conf` | root | root | -rw------- |
| `/etc/login.defs` | root | root | -rw------- |
| `/etc/motd` | root | root | -rw-r--r-- |
| `/etc/mtab` | root | root | -rw-r--r-- |
| `/etc/netgroup` | root | root | -rw------- |
| `/etc/passwd` | root | root | -rw-r--r-- |
| `/etc/rc.d` | root | root | drwx------ |
| `/etc/rc.local` | root | root | -rw------- |
| `/etc/rc.sysinit` | root | root | -rw------- |
| `/etc/security` | root | root | -rw------- |
| `/etc/services` | root | root | -rw-r--r-- |
| `/etc/shadow` | root | root | -r------- |
| `/etc/ssh/ssh_host_key` | root | root | -rw------- |
| `/etc/ssh/sshd_config` | root | root | -rw------- |
| `/etc/ssh/ssh_host_dsa_key` | root | root | -rw------- |
| `/etc/ssh/ssh_host_key` | root | root | -rw------- |
| `/etc/ssh/ssh_host_rsa_key` | root | root | -rw------- |
| `/etc/ttys` | root | root | -rw------- |
| `/root` | root | root | drwx------ |
| `/sbin` | root | root | drwxr-xr-x |
| `/tmp` | root | root | drwxrwxrwt |
| `/usr/bin` | root | root | drwxr-xr-x |
| `/usr/etc` | root | root | drwxr-xr-x |
| `/usr/sbin` | root | root | drwxr-xr-x |
| `/var/log` | root | root | drwxr-xr-x |
| `/var/log/authlog*` | root | root | -rw------- |
| `/var/log/boot*` | root | root | -rw------- |
| `/var/log/cron*` | root | root | -rw------- |
| `/var/log/dmesg` | root | root | -rw------- |
| `/var/log/lastlog` | root | root | -rw------- |
| `/var/log/mailog*` | root | root | -rw------- |
| `/var/log/messages*` | root | root | -rw------- |
| `/var/log/secure*` | root | root | -rw--- |
| `/var/log/spooler*` | root | root | -rw--- |
| `/var/log/syslog*` | root | root | -rw--- |
