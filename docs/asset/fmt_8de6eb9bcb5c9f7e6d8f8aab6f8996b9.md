
## 安全固 FTP

### tpusers 文件

确保你已经设置了 `/etc/tpusers` 文件非常重要，该文件指定了不允许连接到你的 FTP 服务器的用户。该文件至少应包含以下条目：root, been, daemon, lp, sync, shutdown, halt, mail, news, uuc, operator, games, nobody 以及你的 `/etc/passwd` 文件中存在的所有其他默认供应商提供的账户。

### 匿名 FTP 程序

要禁用 FTP，请从你的密码文件中删除匿名用户 "ftp"，并验证系统上未安装 `anonftp-version.i386.rpm` 包。

- 要从密码文件中删除用户 "ftp"，请使用以下命令：

  `root@deep # userdel ftp`

- 要验证你的 Linux 系统上未安装匿名 FTP 程序的 RPM 包，请使用以下命令：

  `root@deep # rpm -q anonftp`

  package anonftp is not installed

### upload 命令

默认情况下，Wu-ftpd 服务器会向所有用户授予上传权限。`upload` 参数允许远程客户端下载并将文件放置在 FTP 服务器上。为了获得最佳安全性，你不希望用户能够上传到 `/home/ftp` 目录下的 "bin"、etc"、dev" 和 "lib" 子目录。在你的 `/etc/ftpasswd` 文件中，我们已经创建了 root 用户对应的 `/home/ftp`，他们无法访问该目录结构之外的文件系统的任何部分，但万一这些权限出现意外，你应该拒绝进入这些区域的上传权限（`/home/ftp/home/ftp/bin`、`/home/ftp/etc`、`/home/ftp/dev`、`/home/ftp/lib`）。

编辑 `ftpasswd` 文件（`/etc/ftpasswd`）并添加以下行以拒绝进入这些区域的上传权限。

- 我们不希望用户能够上传到这些区域。

  `upload/home/ftp/ / no`

  `upload/home/ftp/ /etc no`

  `upload/home/ftp/ /dev no`

  `upload/home/ftp/ /bin no (仅在你没有使用 "--enable-ls" 选项时需要)`

  `upload/home/ftp/ /lib no (仅在你没有使用 "--enable-ls" 选项时需要)`

## 服务器软件（文件共享网络服务） | 第一章

上述行指定了拒绝进入 chroot 的 `/home/ftp/` 目录下的 "/etc"、"/dev"、"/bin" 和 "/lib" 目录。

### 特殊文件 .notar

无论你对目录进行实时 tar 压缩，都应该确保在所有不允许使用 `upload` 参数的区域，无法使用 tar 命令执行结束操作。

第 1 步

为此，在每个目录以及 FTP 目录中创建特殊文件 `.notar`。

```
[root@$] # touch /home/ftp/notar
[root@$] # touch /home/ftp/etc
[root@$] # touch /home/ftp/dev
[root@$] # touch /home/ftp/bin/notar (仅在你没有使用 "-enable-ls" 选项时需要)
[root@$] # touch /home/ftp/lib/notar (仅在你没有使用 "-enable-ls" 选项时需要)
[root@$] # chmod 060 /home/ftp/notar
[root@$] # chmod 0 /home/ftp/etc/notar
[root@$] # chmod 0 /home/ftp/dev/notar
[root@$] # chmod 0 /home/ftp/bin/notar (仅在你没有使用 "-enable-ls" 选项时需要)
[root@$] # chmod 0 /home/ftp/lib/notar (仅在你没有使用 "-enable-ls" 选项时需要)
```

第 2 步

不可检索的 .notar

### notretrieve 命令

```
# 我们将使用 notretrieve 防止下载。
notretrieve /home/ftp/etc
notretrieve /home/ftp/dev
notretrieve /home/ftp/bin (仅在你没有使用 "-enable-ls" 选项时需要)
notretrieve /home/ftp/lib (仅在你没有使用 "-enable-ls" 选项时需要)
```

## 安装文件

| | |

| :--- | :--- |

| /etc/pam.d/ftp | /usr/man/man5/ftpconversions.5 |

| /etc/logograte.d/ftpd | /usr/man/man5/xferlog.5 |

| /etc/tpaccess | /usr/man/man8/ftpd.8 |

| /etc/ftpconversions | /usr/man/man8/ftpshut.8 |

| /etc/ftpgroups | /usr/man/man8/ftpstart.8 |

| /etc/ftpasswd | /usr/sbin/ftpd |

| /home/ftp | /usr/sbin/xferlog |

| /etc/tpusers | /usr/sbin/config |

# 使用 tar 进行备份

通过六张磁带，你可以每天进行备份。操作步骤是：使用磁带 1 进行第一次全量备份（周五 1），使用磁带 2 到 5 进行增量备份（周一至周四）。然后，在磁带 6 上进行新的全量备份（第二个周五），并再次开始从磁带 2 到 5 开始进行增量备份。在获取通过磁带 6 获得的新备份之前，保持磁带 1 的状态至关重要。在接下来的示例中，我们假设将备份写入 SCSI 磁带驱动器 (`/dev/st0`)，并备份系统的主目录 (`/home`)。

首先，我们必须移动到系统的 `/` 分区。在创建归档文件时，“tar”会剥离文件名开头的 `/` 字符。这意味着还原的文件可能不会存储在备份时的相同位置。因此，为了解决这个问题，解决方案是在进行所有备份和还原之前切换到 `/` 根目录。

- 要切换到 `/` 根目录，请使用命令：

```bash
deep# cd /
```

始终从全量备份开始（例如，在周五）是非常重要的，例如：

- （使用磁带 1 进行第一次全量备份）：

```bash
deep# cd /
deep# # tar cpf /dev/st0 --label="full-backup created on date '+%d-%B-%Y'." --directory=/home
```

- 周一，（使用磁带 2 进行增量备份）：

```bash
deep# cd /
deep# # tar cnp /dev/st0 --label="full-backup created on date '+%d-%B-%Y'." --directory=/home
```

- 周二，（使用磁带 3 进行增量备份）：

```bash
deep# cd /
deep# # tar cnp /dev/st0 --label="full-backup created on date '+%d-%B-%Y'." --directory=/home
```

- 周三，（使用磁带 4 进行增量备份）：

```bash
deep# cd /
deep# # tar cnp /dev/st0 --label="full-backup created on date '+%d-%B-%Y'." --directory=/home
```

- 周四，（使用磁带 5 进行增量备份）：

```bash
deep# cd /
deep# # tar cnp /dev/st0 --label="full-backup created on date '+%d-%B-%Y'." --directory=/home
```

- 周五，2，（使用磁带 6 进行新的全量备份）：

```bash
deep# cd /
deep# # tar cpf /dev/st0 --label="full-backup created on date '+%d-%B-%Y'." --directory=/home
```

- 现在，开始使用磁带 2 到 5 进行增量备份，依此类推。

"`c`" 选项指定创建一个归档文件。

"`p`" 选项保留权限；文件信息将被“记住”。

"`N`" 选项创建增量备份，并仅存储比上次更新的文件。

"`T`" 选项指定下一个参数将是写入的归档文件或设备名称。

# 备份与还原步骤

第 2 章
