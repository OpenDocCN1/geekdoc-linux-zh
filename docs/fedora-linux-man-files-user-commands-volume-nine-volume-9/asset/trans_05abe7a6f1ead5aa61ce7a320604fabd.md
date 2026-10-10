
## requests.

unlock \<filenum\> \<hex-start\> \<hex-len\>

此命令依赖于服务器支持 CIFS UNIX 扩展，如果服务器不支持则将会失败。尝试解锁给定范围内的 POSIX fcntl 锁。用于 Samba 内部测试目的。

volu

打印当前共享卷的名称。

vuid \<number\>

将协议中当前使用的 vuid 更改为给定的任意数字。如果没有参数，则打印当前使用的 vuid。用于 Samba 内部测试目的。

tcon \<sharename\>

建立新的树连接（到共享的连接）。替换当前的树连接。打印新的 tid（树 ID）。用于 Samba 内部测试目的。

tdis

关闭当前的共享连接（树断开连接）。用于 Samba 内部测试目的。

tid \<number\>

将协议中当前的树 ID（tid）更改为一个新的任意数字。如果没有参数，则打印当前使用的 tid。用于 Samba 内部测试目的。

## 注意事项

某些服务器对于提供的用户名、密码、共享名称（又称服务名称）和机器名称的大小写比较挑剔。如果连接失败，请尝试将所有参数以大写字母提供。当连接某些类型的服务器时，通常需要使用 -n 选项。例如，OS/2 LanManager 坚持要求使用有效的 NetBIOS 名称，因此你需要提供一个服务器已知晓的有效名称。

smbclient 支持长文件名，前提是服务器支持 LANMAN2 协议或更高版本。

## 环境变量

变量 **USER** 可能包含使用客户端的用户的用户名。只有当协议级别足够高以支持会话级密码时，才会使用此信息。

变量 **PASSWD** 可能包含使用客户端的用户的密码。只有当协议级别足够高以支持会话级密码时，才会使用此信息。

变量 **LIBSMB_PROG** 可能包含通过 system() 执行的路径，客户端将连接到此路径而不是连接到服务器。此功能主要作为开发辅助工具，在使用 LMHOSTS 文件时效果最佳。

## 安装

客户端程序的位置由各个系统管理员自行决定。因此，以下内容仅为建议。

建议将 smbclient 软件安装在 /usr/local/samba/bin/ 或 /usr/samba/bin/ 目录中，该目录应可被所有用户读取，但仅允许 root 用户写入。客户端程序本身应允许所有用户执行。客户端**不**应设置为 setuid 或 setgid！

客户端日志文件应放在仅可由该用户读写 的目录中。

要测试客户端，你需要知道一个正在运行的 SMB/CIFS 服务器的名称。作为普通用户运行 smbd(8) 是可行的 - 将该服务器作为守护进程在用户可访问的端口（通常是 1024 以上的任何端口号）上运行，将提供一个合适的测试服务器。

## 诊断

客户端发出的大多数诊断信息记录在指定的日志文件中。日志文件名称在编译时指定，但可以在命令行上覆盖。

可用的诊断信息的数量和性质取决于客户端使用的调试级别。如果你遇到问题，请将调试级别设置为 3 并查看日志文件。

## 版本

此 man 页适用于 Samba 套件的 3.2 版本。

## 作者

最初的 Samba 软件和相关工具由 Andrew Tridgell 创建。Samba 现在由 Samba 团队作为一个开源项目进行开发，其开发方式类似于 Linux 内核。

最初的 Samba man 页由 Karl Auer 撰写。man 页源码被转换为 YODL 格式（另一种优秀的开源软件，可在 [link missing] 获取），并由 Jeremy Allison 为 Samba 2.0 版本进行更新。Samba 2.2 版本转换为 DocBook 的工作由 Gerald Carter 完成。Samba 3.0 版本转换为 DocBook XML 4.2 的工作由 Alexander Bokovoy 完成。

# SMBGET

## 名称

smbget - 用于通过 SMB 下载文件的类似 wget 的工具

## 概要

```
smbget [-a, --guest] [-r, --resume] [-R, --recursive] [-u, --username=STRING] [-p, --password=STRING] [-w, --workgroup=STRING] [-n, --nonprompt] [-d, --debuglevel=INT] [-D, --dots] [-P, --keep-permissions] [-o, --outfile] [-f, --rcfile] [-q, --quiet] [-v, --verbose] [-b, --blocksize] [-O, --stdout] [-U, --update] [-?, --help] [--usage] { [url]... }
```

## 描述

此工具是 smbclient(7) 套件的一部分。

smbget 是一个具有类似 wget 语义的简单工具，可以从 SMB 服务器下载文件。你可以在命令行中指定想要下载的文件。

文件应遵循 smb-URL 标准，例如，对于 UNC 路径 \\HOST\SHARE\file，请使用 smb://HOST/SHARE/file。

## 选项

- -a, --guest
  以 guest 用户身份工作

- -r, --resume
  自动恢复中断的文件

- -R, --recursive
  递归下载文件

- -u, --username=STRING
  要使用的用户名

- -p, --password=STRING
  要使用的密码

- -w, --workgroup=STRING
  要使用的工作组（可选）

- -n, --nonprompt
  不询问任何问题（非交互式）

- -d, --debuglevel=INT
  要使用的调试级别

- -D, --dots
  显示点作为进度指示

- -P, --keep-permissions
  在本地文件上设置与远程文件上设置的 samba 权限相同。

- -o, --outfile
  将正在下载的文件写入指定的文件。不能与 -R 一起使用。

- -O, --stdout
  将正在下载的文件写入标准输出。

- -f, --rcfile
  使用指定的 rcfile。它将按指定顺序加载 - 例如，如果你在此选项之前指定任何选项，它们可能会被 rcfile 的内容覆盖。

- -q, --quiet
  保持安静

- -v, --verbose
  详细显示

- -b, --blocksize
  块中下载的字节数。默认为 64000。

- -?, --help
  显示帮助信息

- --usage
  显示简短的使用信息

- -U, --update
  仅当远程文件比本地文件新或本地文件缺失时下载。

- -e, --encrypt
  此命令行参数要求远程服务器支持 UNIX 扩展或已选择 SMB3 协议。请求加密连接。使用 SMB3 或通过 GSSAPI 使用 POSIX 扩展进行 SMB 加密协商。使用给定的凭据进行加密协商（如果提供了域/用户名/密码三元组，则使用 kerberos 或 NTLMv1/v2）。如果无法协商加密，则连接失败。

## SMB URLs

SMB URL 应按以下格式指定：

`smb://<server>/*`

`<server>`: 名称，如果名称是工作组，则是此工作组中的所有服务器；或者如果名称是服务器，则是此服务器上的所有共享。

## 示例

- 递归下载 'src' 目录： `smbget -R smb://server/share/src`
- 下载 FreeBSD ISO 并启用恢复： `smbget -r smb://server/share/FreeBSD-iso`
- 递归下载所有 ISO： `smbget -Rr smb://server/share/*iso`
- 备份 rthonwyn 上的我的数据： `smbget -Rr smb://rthonwyn/share`

## 缺陷

在某些情况下，当错误原因未知时（例如非法格式化的 smb: url 或未开启 -R 选项却试图获取目录），会返回权限拒绝。

## 版本

此 man 页适用于 Samba 套件的 3 版本。

## 作者

最初的 Samba 软件和相关工具由 Andrew Tridgell 创建。Samba 现在由 Samba 团队作为一个开源项目进行开发，其开发方式类似于 Linux 内核。

smbget man 页由 Jelmer Vernooij 撰写。

# SMIME

## 名称

openssl smime - S/MIME 工具

## 概要

```
openssl smime [-encrypt] [-decrypt] [-sign] [-resign] [-verify] [-pk7out] [-cipher] [-in file] [-CAfile file] [-CApath dir] [-trusted_first] [-no_alt_chains] [-certfile file] [-signer file] [-recip file] [-inform SMIME|PEM|DER] [-passin arg] [-inkey file] [-out file] [-outform SMIME|PEM|DER] [-content file] [-to addr] [-from addr] [-subject s] [-text] [-indef] [-noindir] [-stream] [-rand file(s)] [-md digest] [cert.pem],...
```

## 描述

**smime** 命令处理 S/MIME 邮件。它可以加密、解密、签名和验证 S/MIME 消息。

