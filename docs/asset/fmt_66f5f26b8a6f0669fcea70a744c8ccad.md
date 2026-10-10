
```
# The directory to which anonymous FTP user will chroot to.
# Note: if you change this (add,rm)ftpuser may stop
# functioning.
#/anonymous-root /home/ftp
```

当有人以匿名用户身份登录时，本节会验证登录情况，以确保用作密码的电子邮件符合 `rfc822` 标准。这并不意味着该密码是一个有效的、可用的密码。

```
# Password verification for the anonymous FTP user.
# <none|trivial|rfc822> [<enforce|warn]
password-check rfc822 enforce
```

限制匿名连接的长度也可以帮助我们减少攻击。通常，这会给合法用户带来不便，因此不要设置得太短。

```
# Maximum connection time in minutes
#limit-time anonymous 30
```

此区域设置了匿名连接对匿名 FTP 区域的权限。权限越少越好。我建议你保留此处所示的默认设置，除非你了解这些更改带来的后果。

```
# Some permissions for the anonymous FTP user.
# All the following default to "yes" for everybody
rename no anonymous # rename permission?
delete no anonymous # delete permission?
overwrite no anonymous # overwrite permission?
chmod anonymous # chmod permission?
umask no anonymous # umask permission?
```

我建议对这一部分进行一些更改。这里是你设置上传区域的地方。如果你允许匿名用户向你的系统放置文件，可以保持此设置；否则，将第二行上传的 `yes` 改为 `no`。这可以防止任何人上传到此区域。

## 第 22 章 FTP 服务器 471

### 匿名 FTP 目录上传设置

```
# anon-ftp-root path allow? Owner group mode dirs?
# Upload /home/incoming* no
# Upload /home/ftp/pub/incoming yes ftp daemon 0666 nodirs
```

```
# What can a filename content (this /etc is under the
anonymous-ftp root)
path-filter anonymous /etc/passwd \^-[A-Za-z0-9_]*$ ^\.\\nalias
```

```
# Shortcuts for anonymous FTP incoming (note: the ':': isn't obligatory)
alias coming: /pub/incoming
cdpath /pub/incoming
```

> 默认情况下，`wu-ftpd` FTP 服务器未配置为匿名服务器。

## ftpconversions

`ftpconversions` 配置文件也是 `wu-ftpd` 的一个特殊功能，它在传输文件之前在服务器上提供客户端文件转换能力。如果客户端在下载后没有可用的软件来转换文件，这将非常有用。例如，如果客户端是 Windows 机器，它可能没有 `gzip` 工具来解压下载后的文件。因此，通过使用 `wu-ftpd` 的此功能，你可以在服务器上解压文件。显然，在 DOS 机器上解压二进制可执行文件是没有用的；并不是所有压缩的二进制文件都是二进制文件。

安装 `wu-ftpd` 时自带的配置文件包含了大多数 UNIX 压缩方案，你可能不需要对此文件进行更改。如果你需要进行更改，请记住使用冒号（`:`）来分隔每个字段。以下代码显示了文件中转换行的格式，表 22-1 解释了每一项。

```
1 : 2 : 3 : 4 : 5 : 6 : 7 : 8
```

| 表 22-1 |
| ftpconversion 字段说明 |
| 描述 | 描述 |
| 1 | 删除文件名开头的前缀 |
| 2 | 删除文件名末尾的后缀 |
| 3 | 传输时在文件末尾插入附加前缀字符串 |
| 4 | 传输时在文件开头附加后缀 |
| 5 | 外部命令，用于识别传输期间动态执行的程序 |
| 表 22-1（续） |
| 字段 | 描述 |
| 6 | 可操作的文件类型：`T_REG`、`T_ASCII` 和/或 `T_DIR`。用管道符号 `()` 分隔多个类型。 |
| 7 | 指定由 `0_COMPRESS`、`0_UNCOMPRESS` 和/或 `0_TAR` 使用的转换类型。用管道符号 `()` 分隔多个类型。 |
| 8 | 描述正在发生的转换类型 |

你在主 `ftppass` 文件中控制此功能的使用。如果没有启用 `compress` 和 `tar` 选项，则不会使用此配置文件。

## ftpservers

此配置允许使用多个配置文件。如果你根据连接到系统的机器需要多个配置，可以为每个 IP 地址创建单独的配置文件。这些配置文件基于 `/etc/wu-ftpd` 目录中的所有文件。`ftpservers` 中列出的每个 IP 地址都有自己的路径。

## /etc/inetd

文件的开头设置了服务器名称，无论是独立运行还是 `inetd`。如果服务器类型是 `inetd`，则你必须在 `inetd.conf` 文件中添加条目。

## /etc/inetd.conf

接下来的 `message` 部分设置了消息名称。第一个在用户登录系统后显示。第二个在进入目录时显示，最后的选项表示 Is 是默认 -选项。

## 日志文件

`timeout` 部分识别了可能导致连接超时的三种情况。第一个是空闲连接。当达到以下三个限制（以秒为单位）中的任何一个时，将释放连接。这是你查找系统出现什么问题的地方。

### proftpd 服务器

专业 FTP 服务器 `proftpd` 是一个健壮、安全的服务器，当用时是一个极佳的选择。该服务器在重型 FTP 站点中越来越受欢迎。你可以在此处找到源码。

## proftpd.conf

`proftpd` FTP 服务器只有一个配置文件。该文件位于 `/etc` 目录，包含了使 `proftpd` 顺畅运行的所有信息。本章所示的配置文件随 Debian 安装提供。

此选项设置了服务器运行时的所有者。在正常情况下，您应该保持这些设置不变：

- # 设置服务器通常运行的用户和用户组。
  `User root`
  `Group root`

匿名部分默认是被注释掉的；因此它是不可用的。要启用此部分，请通过删除该部分中的双双井号（`##`）来编辑配置文件。此部分假设您的服务器上有一个 `ftp` 用户和 `nogroup` 组。如果您的机器上没有这些项，则该部分将无法工作。

当您启用此配置的匿名部分时，上传功能将不可用，因为该部分默认也被标记为注释。

```
# 基础匿名配置，不包含上传目录。
## <Anonymous~ftp>
## User ftp
## Group nogroup
## # 我们希望客户端能够使用 "anonymous"
## 也可以使用 "ftp" 登录
## UserAlias anonymous ftp
## RequireValidShell off
## # 限制匿名登录的最大数量
## MaxClients 10
## # 等，我在源文中看到一个拼写错误：MaxClients 10
## # 我们希望在登录时显示 'welcome.msg'，
## 在每个新进入的目录显示 '.message'
## DisplayLogin welcome.msg
## DisplayFirstChdir .message
## # 限制匿名根目录下的所有写入权限
## <Directory *>
## <Limit WRITE>
## DenyAll
## </Limit>
## </Directory>
## # <Directory incoming>
## <Limit READ WRITE>
## DenyAll
## </Limit>
## <Limit STOR>
## AllowAll
## </Limit>
## </Directory>
## </Anonymous>
```

## 第 22 章 ✦ FTP 服务器 475

配置文件未列出同时运行的服务器最大实例数量。设置最大值有助于防止任何拒绝服务攻击。有关此类攻击的更多信息，请查看安全章节（第19章）。要进行此更改，请向配置文件添加此行：

```
MaxInstances      30
```

这限制了服务器可以启动实例数量。如果您发现需要运行更多实例，可以调整此值。

## 日志文件

`proptpd` 服务器的日志文件存放在 `/var/log/xferlog`。再次强调，查看您的日志文件有助于发现滥用、攻击和任何其他问题。日志文件是您的朋友——我确定您已经听腻了。

## 管理 FTP 服务器
