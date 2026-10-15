
```
# mysqldump -u root -psecret --add-drop-database dbname > dbname_sql.dump
# mysql -u root -psecret -D dbname < dbname_sql.dump
```

备份和恢复所有数据库：

```
# mysqldump -u root -psecret --add-drop-database --all-databases > full.dump
# mysql -u root -psecret < full.dump
```

这里的 `secret` 是 `mysql` `root` 密码，`-p` 后没有空格。当单独使用 `-p` 选项（无密码）时，密码会在命令行提示输入。

### 18.3 SQLite

`SQLite`²⁷ 是一个小型强大、独立、免服务器、零配置的 SQL 数据库。

#### 转储和恢复

转储和恢复 SQLite 数据库可能很有用。例如你可以编辑转储文件以更改列属性或类型，然后恢复数据库。这比处理 SQL 命令更容易。使用命令 `sqlite3` 用于 3.x 数据库。

```
# sqlite database.db .dump > dump.sql                # dump
# sqlite database.db < dump.sql                       # restore
```

#### 转换 2.x 到 3.x 数据库

```
sqlite database_v2.db .dump | sqlite3 database_v3.db
```

## 19 磁盘配额

磁盘配额允许限制用户或（或组成员）可使用的磁盘空间量和/或文件数量。配额按文件系统分配，由内核强制执行。

### 19.1 Linux 设置

通常需要安装配额工具包，它包含命令行工具。在 `fstab` 中激活用户配额并重新挂载分区。如果分区繁忙，则必须关闭所有被锁定的文件，或必须重新启动系统。将 `usrquota` 添加到 `fstab` 挂载选项中，例如：

```
/dev/sda2   /home   reiserfs   rw,acl,user_xattr,usrquota 1 1
# mount -o remount /home
# mount                 # 检查 usrquota 是否激活，否则重启
```

使用 `quotacheck` 初始化 `quota.user` 文件。

```
# quotacheck -vum /home
# chmod 644 /home/aquota.user   # 让用户自行检查其配额
```

使用提供的脚本（例如 SuSE 上的 `/etc/init.d/quotad`）或使用 `quotaon` 激活配额：

```
quotaon -vu /home
```

使用以下命令检查配额是否激活：

```
quota -v
```

### 19.2 FreeBSD 设置

配额工具是基本系统的一部分，然而内核需要选项 `quota`。如果没有，则添加它并重新编译内核。

```
options QUOTA
```

与 Linux 相同，将配额添加到 `fstab` 选项中（`userquota`，而不是 `usrquota`）：

```
/dev/ad0s1d   /home   ufs   rw,noatime,userquota   2   2
# mount /home              # 重新挂载分区
```

在 `/etc/rc.conf` 中启用磁盘配额并启动配额。

```
# grep quotas /etc/rc.conf
enable_quotas="YES"        # 启动时打开配额（或 NO）。
check_quotas="YES"         # 启动时检查配额（或 NO）。
# /etc/rc.d/quota start
```

### 19.3 分配配额限制

默认情况下配额不受限制（设为 0）。限制使用 `edquota` 为单个用户设置。配额也可以复制给多个用户。不同配额实现的文件结构不同，但原理相同：块和 inode 的值可以受限。只更改 `soft` 和 `hard` 的值。如果未指定，块为 1k。宽限期使用 `edquota -t` 设置。例如：

```
# edquota -u colin
```

#### Linux

用户 `colin`（`uid` 1007）的磁盘配额：

Filesystem   blocks   soft   hard   inodes   soft   hard

`/dev/sda8`    108      1000   2000   1        0      0

#### FreeBSD

```
Quotas for user colin:
/home: kbytes in use: 504184, limits (soft = 700000, hard = 800000)
    inodes in use: 1792, limits (soft = 0, hard = 0)
```

#### 多用户

命令 `edquota -p` 用于将配额复制给其他用户。例如将参考配额复制给所有用户：

```
# edquota -p refuser `awk -F: '$3 > 499 {print $1}' /etc/passwd`
# edquota -p refuser user1 user2   # 复制给 2 个用户
```

#### 检查

用户只需输入 `quota` 即可检查其配额（`quota.user` 文件必须可读）。`root` 可以检查所有配额。

```
# quota -u colin                # 检查用户的配额
# repquota /home                # 分区的完整报告，针对所有用户
```

## 20 Shell

大多数 Linux 发行版使用 `bash` shell，而 BSD 使用 `tcsh`，`bourne shell` 仅用于脚本。过滤器非常有用，可以通过管道连接：

- `grep` 模式匹配

- `sed` 搜索并替换字符串或字符

- `cut` 从标记打印特定列

- `sort` 按字母或数字排序

- `uniq` 从文件中删除重复行

例如一次性全部使用：

```
# ifconfig | sed 's/ / /g' | cut -d" " -f1 | uniq | grep -E "[a-z0-9]+" | sort -r
# ifconfig | sed '/inet addr:/!d;s/.*//.*/'|sort -t. -k1,1n -k2,2n -k3,3n -k4,4n
```

`sed` 模式中的第一个字符是一个制表符。要在控制台上写入制表符，请使用 `ctrl-v ctrl-tab`。

### 20.1 bash

`bash` 和 `sh` 的重定向和管道：

```
# cmd1 > file                 # 将 stdout 重定向到文件。
# cmd2 > file                 # 将 stderr 重定向到文件。
# cmd1 >> file                # 将 stdout 重定向并追加到文件。
# cmd1 <> file                # 将 stdout 和 stderr 都重定向到文件。
# cmd1 >file 2>&1             # 将 stderr 重定向到 stdout，然后重定向到文件。
# cmd1 | cmd2                 # 将 stdout 管道传输到 cmd2
# cmd1 2>&1 | cmd2            # 将 stdout 和 stderr 管道传输到 cmd2
```

在 `~/.bashrc` 中修改你的配置（也可以是 `~/.bash_profile`）。以下条目很有用，使用 `". ~/.bashrc"` 重新加载。使用 `cygwin` 时使用 `~/.bash_profile`；使用 `rxvt` 时使用 `shift + 左键` 粘贴。
