
程序 `cdparanoia` 可以保存音频轨道（FreeBSD 端口在 `audio/cdparanoia/`），`oggenc` 可以编码为 Ogg Vorbis 格式，`lame` 转换为 mp3。

```
# cdparanoia -B                # Copy the tracks to wav files in current dir
# lame -b 256 in.wav out.mp3    # Encode in mp3 256 kb/s
# for i in *.wav; do lame -b 256 $i `basename $i .wav`.mp3; done
# oggenc in.wav -b 256 out.ogg  # Encode in Ogg Vorbis 256 kb/s
```

## 17 打印

### 17.1 使用 lpr 打印

```
# lpr unixtoolbox.ps            # Print on default printer
# export PRINTER=hp4600          # Change the default printer
# lpr -P hp4500 #2 unixtoolbox.ps # Use printer hp4500 and print 2 copies
# lpr -o Duplex=DuplexNoTumble ... # Print duplex along the long side
# lpr -o PageSize=A4,Duplex=DuplexNoTumble ...
```

```
# lpq                          # Check the queue on default printer
# lpq -l -P hp4500              # Queue on printer hp4500 with verbose
# lprm -                        # Remove all users jobs on default printer
# lprm -P hp4500 3186            # Remove job 3186. Find job nbr with lpq
# lpc status                     # List all available printers
# lpc status hp4500              # Check if printer is online and queue length
```

一些设备不是 PostScript 设备，用 pdf 文件喂给它们时会打印乱码。这可能通过以下方式解决：

```
# gs -dSAFER -dNOPAUSE -sDEVICE=deskjet -sOutputFile=\|lpr file.pdf
```

即使应用程序不支持，也可打印到 PDF 文件。在打印命令中使用 `gs` 代替 `lpr`。

```
# gs -q -sPAPERSIZE=a4 -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -sOutputFile=/path/file.pdf
```

## 18 数据库

### 18.1 PostgreSQL

#### 修改 root 或用户名密码

```
> psql -d template1 -U pgsql
> alter user pgsql with password 'pgsql_password';  # Use username instead of "pgsql"
```

#### 创建用户和数据库

命令 `createuser`、`dropuser`、`createdb` 和 `dropdb` 是方便的快捷方式，等同于 SQL 命令。新建用户为 `bob`，数据库为 `bobdb`；使用 `root` 以 `psql` 登录数据库超级用户：

```
# createuser -U pgsql -P bob          # -P will ask for password
# createdb -U pgsql -O bob bobdb       # new bobdb is owned by bob
# dropdb bobdb                         # Delete database bobdb
# dropuser bob                         # Delete user bob
```

通用数据库认证机制在 `pg_hba.conf` 中配置

#### 授予远程访问

文件 `$PGSQL_DATA_D/postgresql.conf` 指定绑定地址。通常 `listen_addresses = '*'` 用于 Postgres 8.x。

文件 `$PGSQL_DATA_D/pg_hba.conf` 定义访问控制。示例：

```
# TYPE  DATABASE  USER    IP-ADDRESS      IP-MASK         METHOD
host    bobdb     bob     212.117.81.42   255.255.255.255 password
host    all       all     0.0.0.0/0                   password
```

#### 备份和恢复

备份和恢复使用用户 `pgsql` 或 `postgres`。备份和恢复单个数据库：

```
# pg_dump --clean dbname > dbname_sql.dump
# psql dbname < dbname_sql.dump
```

备份和恢复所有数据库（包括用户）：

```
# pg_dumpall --clean > full.dump
# psql -f full.dump postgres
```

在这种情况下，恢复从数据库 `postgres` 开始，在重新加载空集群时更好。

### 18.2 MySQL

#### 修改 mysql root 或用户名密码

方法 1

```
# /etc/init.d/mysql stop
or
# killall mysqld
# mysqld --skip-grant-tables
# mysqladmin -u root password 'newpasswd'
# /etc/init.d/mysql start
```

#### 方法 2

```
# mysql -u root mysql
mysql> UPDATE USER SET PASSWORD=PASSWORD("newpassword") where user='root';
mysql> FLUSH PRIVILEGES;    # Use username instead of "root"
mysql> quit
```

#### 创建用户和数据库（参见 MySQL 文档²⁶）

```
# mysql -u root mysql
mysql> CREATE USER 'bob'@'localhost' IDENTIFIED BY 'pwd';  # create only a user
mysql> CREATE DATABASE bobdb;
mysql> GRANT ALL ON *.* TO 'bob'@'%' IDENTIFIED BY 'pwd';  # Use localhost instead of %
# to restrict the network access
mysql> DROP DATABASE bobdb;                  # Delete database
mysql> DROP USER bob;                        # Delete user
mysql> DELETE FROM mysql.user WHERE user='bob and host='hostname';  # Alt. command
mysql> FLUSH PRIVILEGES;
```

#### 授予远程访问

远程访问通常允许用于某个数据库，而非所有数据库。文件 `/etc/my.cnf` 包含绑定 IP 地址。通常注释掉行 `bind-address = out`。

```
# mysql -u root mysql
mysql> GRANT ALL ON bobdb.* TO bob@'xxx.xxx.xxx.xxx' IDENTIFIED BY 'PASSWORD';
mysql> REVOKE GRANT OPTION ON foo.* FROM bar@'xxx.xxx.xxx.xxx';
mysql> FLUSH PRIVILEGES;                    # Use 'hostname' or also '%' for full access
```

#### 备份和恢复

备份和恢复单个数据库：
