
`mysqldump` 是一个用于 MySQL 和 MariaDB 数据库系统的简单备份工具。该命令返回长长的 SQL 命令列表，可以从这些列表中精确恢复数据库。`mysqldump` 知晓三种语法变体，取决于保存一个数据库、多个列出的数据库还是由 MySQL 管理的所有数据库。只有第一种变体允许备份限制在单个表。

为了让 `mysqldump` 建立到数据库服务器的连接，必须使用 `mysql` 命令中描述的连接选项，即 `-u`、`-p`、`-h` 等。其他许多选项控制备份的细节。

### 选项

- `--add-locks`
  在第一个 `INSERT` 命令之前插入 `LOCK TABLE`，在最后一个 `INSERT` 命令之后解锁。这加快了 MyISAM 表的重新加载。然而，此选项不适用于 InnoDB 表。

- `--create-options`
  在 `CREATE TABLE` 中包含 MySQL 特有的选项。

- `--disable-keys`
  在重新加载数据期间禁用索引更新。索引直到过程结束时才会更新，这样速度更快。

- `--extended-insert`
  创建较大的 `INSERT` 命令，同时插入多个数据记录。

- `--lock-all-tables`
  对整个数据库运行 `LOCK READ`。这确保在备份期间没有表被更改。此选项仅适用于 MyISAM 表。对于 InnoDB 表，最好使用 `--single-transaction`。

- `--lock-tables`
  在备份期间对每个表运行 `TABLE READ`。

- `--no-create-info`
  只保存数据，不保存结构。生成的备份中有 `INSERT` 命令，但没有 `CREATE TABLE`。

- `--no-data`
  只保存数据库的结构（模式），但不包含数据。

- `--no-tablespaces`
  防止 `mysqldump` 包含 `CREATEFILE GROUP` 或 `CREATE TABLESPACE` 命令。如果你以没有 Process 权限的用户运行命令，在当前的 MySQL 版本中必须使用此选项。否则会发生拒绝访问的错误。

- `--opt`
  以下选项的简写：`--add-drop-table`、`--add-locks`、`--create-options`、`--disable-keys`、`--extended-insert`、`--lock-tables`、`--quick` 和 `--set-charset`。由于历史原因，`--opt` 默认启用。然而，只有当你执行 MyISAM 表的备份时，生成的设置才是优的（因此有了该选项名称）。

- `--quick`
  直接输出要保存的数据记录，不在内存中进行中间存储。

- `--routines`
  还保存存储过程的代码。

- `--set-charset`
  在 `mysqldump` 输出开始更改活动字符集，并在结束时恢复之前的字符集。

- `--single-transaction`
  确保整个备份作为单个事务的一部分执行。这对于 InnoDB 表很有用，并防止单个表在备份期间被更改。这确保了整体的一致性。

- `--skip-opt`
  禁用默认启用的 `--opt` 选项。

- `--triggers`
  还保存触发器的代码。

## 示例

备份带有 MyISAM 表的数据库只需要几个选项。如果你想防止单个表在备份期间被更改，则需要在命令中添加 `--lock-all-tables` 选项。

```
user$ mysqldump -u user -p dbname > backup.sql
Enter password: ********
```

如果你想保存一个压缩后的备份，应该按照以下步骤操作：

```
user$ mysqldump -u user -p dbname | gzip -c > backup.sql.gz
```

对 InnoDB 表执行优化备份需要多得选项，因为 `mysqldump` 的默认设置并没有针对此类情况进行优化：

```
user$ mysqldump -u user -p --skip-opt --single-transaction \
--create-options --quick --extended-insert \
--disable-keys --add-drop-table dbname > backup.sql
```

如果你使用 `cron` 任务（`cron job`）自动运行备份，你必须将 `-u user -p` 替换为以下选项，并在仅 root 访问的文件 `/root/.my.cnf` 中输入连接参数：

> # 在备份脚本中，`--defaults-extra-file` 必须是第一个选项
`mysqldump --defaults-extra-file=/root/.my.cnf ...`

要稍后恢复备份，你必须运行以下命令：

```
user$ mysqladmin -u user -p create dbname
user$ mysql -u user -p --default-character-set=utf8 dbname < nbackup.sql
```

# `namei`

## `namei [options] file`

`namei` 显示形成指定文件路径的所有目录的权限：

```
user namei -l ~/.ssh
f: /home/kofler/.ssh
drwxr-xr-x root root      /
drwxr-xr-x root root home
drwxr-xr-x kofler kofler kofler
drwx------ kofler .ssh
```

# `nc`

## `nc [options] [hostname/ip-address] [port]`

`nc` 命令更广为人知的 Netcat。它将 TCP/UDP 端口重定向到标准输入/输出，并提供许多其他功能。你可以使用该命令类似于 `telnet` 地交互式测试 HTTP 或 SMTP 等网络协议。通过 `nc`，你还可以通过任何网络端口复制文件、实现聊天，或者设置一个通过端口接收并执行命令的简单后门程序。因此，`nc` 在黑客和渗透测试人员中极其流行并不意外。

在某些 Linux 发行版中，`nc` 命令包含在同名的软件包中；在其他发行版中，你必须安装 `netcat`。注意 Netcat 有不同的实现版本。例如，Debian 和 Ubuntu 使用 `netcat-traditional`，而 RHEL 提供了来自 mmap 开发者的变体（https://nmap.org/ncat）。在实践中，这不会产生任何差异，但根据版本，单个选项的实现方式可能不同（或完全没有实现）。

### 选项

- `-4 -6`
  仅使用 IPv4 或 IPv6。

- `-l`
  等待指定的端口建立连接（监听）。

- `-p portnr`
  定义本地端口（源端口）。通常在 `nc` 命令末尾指定的端口是目标端口。

- `-x proxyadr:portnr`
  使用指定的代理地址和相应的端口。

`man nc` 中描述了许多其他选项。`nc` 的一个可能的替代方案是 `socat` 命令，本书未涵盖它。它还支持 SCTP，可以通过代理服务器工作，操作串口接口，并对传输数据进行加密：

# Examples（示例）

要从主机 1 向主机 2 通过任意端口（这里是 1234）复制文件，你首先在主机 2（右侧列）启动接收端，然后向主机 1 发起传输（左侧列）：

```
host2$ nc -l 1234 > file
host1$ nc host2 1234 < file
```

进行聊天同样简单。你只需要与对方约定一个端口即可。聊天在计算机上通过 `nc -l`（左侧列）启动。通过这样，`nc` 监控指定的端口 1234 并等待建立连接。

在第二个主机上，启动 `nc` 时不带选项以连接到第一个主机。没有可见的确认显示连接已建立，但只要双方中的一方输入文本（标准输入）并按回车键确认，文本就会出现在另一方的终端上（标准输出）。

```
host1$ nc -l 1234
host2$ nc host1 1234
how are you?
how are you?
good
```
```
good
<Ctrl+><
```

第三个示例展示了 Netcat 的潜在危险：在这里，主机 1 上的 `nc` 设置为将从端口 1234 接收的所有输入传递给 `bash` shell。它们的输出会被传回给发送者。现在可以从第二个主机在主机 1 上运行 shell 命令。因此，`ls` 显示的是位于主机 1 上的文件！

```
host1$ nc -l 1234 -e /bin/bash
host2$ nc host1 1234
ls
file1
file2
file3
```
