

- **max_allowed_packet**
  服务器与客户端之间通信使用的缓冲区最大尺寸。默认值为 24MB，最大值为 1GB。

- **max_buffer_length**
  服务器与客户端之间通信使用的缓冲区初始尺寸。此缓冲区可以扩展到 *max_allowed_packet* 字节。默认值略小于 1MB。

## F.16 mysqlhotcopy

*mysqlhotcopy* 可高效地备份数据库和表。它仅适用于 MyISAM 和 ARCHIVE 表。*mysqlhotcopy* 是一个 Perl 脚本。它要求您已安装 DBI 支持（考虑到它最初由 DBI 的创建者之一 Tim Bunce 编写，这并不令人惊讶）。*mysqlhotcopy* 适用于 Unix 和 NetWare，但不适用于 Windows。

*mysqlhotcopy* 连接到本地主机上的服务器。它针对每个要复制的表向服务器发送表刷新和锁定语句，然后将表文件复制到另一个位置以创建备份。这确保了未完成的表修改已刷新到磁盘，并且在表被复制期间服务器不会尝试进一步修改该表。（本质上，*mysqlhotcopy* 实现了第 14.1 节“在服务器运行时执行数据库维护”中描述的协议。该协议的作用是告知服务器在您直接操作表文件时不要操作指定的表。）

该程序可以通过多种方式调用。一般的调用语法如下：

```
mysqlhotcopy [options] db_name[,/regex/] [new_db_name | dir_name]
```

例如，要在数据目录中创建名为 *db_name_copy* 的数据库 *db_name* 的副本，请使用此命令：

```
% mysqlhotcopy [options] db_name
```

若要改为将 *db_name* 数据库复制到 /tmp 目录下名为 *db_name* 的目录中，请执行以下操作：

```
% mysqlhotcopy [options] db_name /tmp
```

在线文档中提供了更多示例，可以通过此命令获取：

```
% perldoc mysqlhotcopy
```

### F.16.1 mysqlhotcopy 支持的标准选项

`--debug` `--host` `--port` `--user` `--help` `--password` `--socket`

`--host` 选项（如果提供）*仅*用于指定本地主机名称。通常，*mysqlhotcopy* 尝试使用 Unix 套接字文件连接到本地服务器。如果使用 `--host` 选项指定服务器的实际主机名或 IP 号，则它改为通过 TCP/IP 连接。在这种情况下，可以使用 `--port` 选项来指定除默认值以外的端口号。对于 `--password`，密码值不是可选的。

### F.16.2 mysqlhotcopy 特有的选项

- `--addtodest`
  如果目标目录已存在，则不重命名它，而是直接将备份文件添加到该目录中。

- `--allowold`
  如果目标目录已存在，则通过添加后缀 `_old` 重命名该目录。如果复制失败，重命名的目录将恢复为原始名称。如果复制操作成功，除非同时给出 `--keepold` 选项，否则将删除重命名的目录。

- `--checkpoint=db_name.tbl_name`
  将检查点记录写入给定的表，该表应预先按照以下结构创建：

  ```sql
  CREATE TABLE tbl_name
  (
    time_stamp TIMESTAMP NOT NULL,
    src VARCHAR(32),
    dest VARCHAR(60),
    msg VARCHAR(255)
  );
  ```

  `src` 是源数据库名称，`dest` 是目标目录路径名，`msg` 指示复制操作的成功或失败。

- `--chroot=dir_name`
  当 *mysql* 在 *chroot*  jails 中运行时使用此选项。目录名是该 jail 的基础目录。

- `--dryrun`，`-n`
  “不执行”模式。*mysqlhotcopy* 报告它将执行哪些操作来执行该命令，而实际上并不执行。这对于检查 *mysqlhotcopy* 是否会按您的预期进行操作非常有用，尤其是在您学习如何使用它时。

- `--flushlog`
  在所有表锁定之后且在复制之前刷新日志。这会将它们检查点化到复制操作的时间点。

- `--keepold`
  如果之前的目标目录存在，则在创建新副本之前通过添加后缀 _old 重命名该目录。此选项隐含着 `--allowold`。

- `--method=copy_method`
  复制文件的方法。值为 cp 使用 cp 程序。也提供了对 scp 方法的实验性支持。在这种情况下，`copy_method` 值应该是要使用的完整 scp 命令，并且目标目录必须已经存在。由于通过网络复制文件所需额外时间，scp 方法可能会导致表被锁定的时间比本地复制长得多。为避免此问题，请先在本地创建备份，然后在 mysqldump 完成后将其复制到远程主机。

- `--noindexes`
  导致不复制索引文件。（如果您稍后需要使用备份文件来恢复表，可以使用 `myisamchk --recover` 配合文件重新创建 MyISAM 表的索引。）

- `--quiet`，`-q`
  使程序除在发生错误时外不产生任何输出。

- `--record-log_pos=db_name.tbl_name`
  在复制表之前，导致 mysqldump 发出 SHOW MASTER STATUS 和 SHOW SLAVE STATUS 语句，并将结果记录在给定的表中，该表应预先按照以下结构创建：

  ```sql
  CREATE TABLE tbl_name
  (
    host             VARCHAR(60) NOT NULL,
    time_stamp       TIMESTAMP NOT NULL,
    log_file         VARCHAR(32) NULL,
    log_pos          INT NULL,
    master_host      VARCHAR(60) NULL,
    master_log_file  VARCHAR(32) NULL,
    master_log_pos   INT NULL,
    PRIMARY KEY (host)
  );
  ```

  SHOW MASTER STATUS 的结果记录在 `log_file` 和 `log_pos` 列中。此信息提供了二进制日志的复制坐标；如果备份主机是复制主服务器，且从备份文件初始化为该主服务器的从库，则从库应从这些坐标开始复制。SHOW SLAVE STATUS 的结果记录在 `master_host`、`master_log_file` 和 `master_log_pos` 列中；如果备份主机是复制从服务器，且您希望从备份文件初始化同一主服务器的另一个从库，则可以使用这些结果。

- `--regexp=pattern`
  复制所有名称匹配给定正则表达式的数据库。命令的最终参数应该是您希望复制数据库的目录。

- `--resetmaster`
  在所有表锁定之后且在复制之前发出 RESET MASTER 语句，从而重置二进制日志。

- `--resetslave`
  在所有表锁定之后且在复制之前发出 RESET SLAVE 语句，从而重置 master.info 文件中的信息。

- `--suffix=str`
  此选项用于将数据库复制到数据库目录时。每个新的数据库目录名称与原始名称相同，但附加了给定的后缀。

- `--tmpdir=dir_name`
  创建临时文件的目录路径名。默认是使用 TMPDIR 环境变量指定的目录，如果该变量未设置，则使用 /tmp。

## F.17 mysqlimport

*mysqlimport* 客户端程序是一个批量加载器，用于将文本文件的内容读取到现有表中。它作为 LOAD DATA SQL 语句的命令行接口，是向表中输入行的高效方式：

```
mysqlimport [options] db_name file_name . . .
```

*db_name* 参数指定包含要加载数据的目标表的数据库。要加载的表由文件名参数确定。对于每个文件名，名称中第一个句号后的扩展名会被去除，剩余的基名用作应加载该文件的表名。例如，*mysqlimport* 将名为 president.txt 文件的内容加载到 president 表中。

*mysqlimport* 仅读取数据文件。它不用于读取由 mysqldump 生成的 SQL 格式转储文件。请改用 *mysql* 来读取此类文件。

