

所接收到的。如果没有响应，则不会产生任何输出。
如果给定了可选的计数，则只发送指定数量的请求。往返时间（Round-trip times）和数据包丢失统计信息将被计算。当所有响应都接收到或命令超时（如果指定了 count 选项），或者命令通过 SIGINT 终止时，将显示一个简要的摘要。

此命令旨在用于测试、管理和测量网络性能。它应主要用于隔离网络故障。由于其可能对网络造成的负载，在正常运行期间或从自动化脚本中不必要地使用 ping 被认为是不礼貌的。

## 作者

ping 是在公有领域中开发的。

## 文件

/etc/hosts

## 参见

gethostbyname(3N), inet(3N).

# rcp

**rcp** - 将一个系统的文件和目录复制到另一个系统。

![](img/75f39fc91296b889c0653851accdfd46_564_0.png)

rcp(1)

## 名称

rcp - 远程文件复制

## 概要

- 复制单个文件：
  `rcp [-p] source_file dest_file`
- 复制多个文件：
  `rcp [-p] source_file1 [source_file2]... dest_dir`
- 复制一个或多个目录子树：
  `rcp [-p] -r source_dir1 [source_dir2]... dest_dir`
- 复制文件和目录子树：
  `rcp [-p] -r file_or_dir1 [file_or_dir2]... dest_dir`

## 描述

rcp 命令将一个或多个系统中的文件、目录子树或文件与目录子树的组合复制到另一个系统。在许多方面，它类似于 cp 命令（参见 cp(1)）。

要使用 rcp，必须具有对正在复制文件的读取权限，以及对目录路径中所有目录的读取和搜索（执行）权限。

### 选项和参数

rcp 识别以下选项和参数：

- **source_file**：位于本地或远程机器上，您要复制到指定目的地的现有文件或目录的名称。源文件和目录名称按以下方式构建：
  `user_name@hostname:pathname/filename`
  或
  `user_name@hostname:pathname/dirname`
  
  文件和目录名称的组件部分在下方描述。如果指定了多个现有文件和/或目录子树（*source_file1*、*source_file2*、... 等），目的地必须是一个目录。在本地和远程系统中都允许 Shell 文件名扩展。可以通过单个命令将一个或多个系统中的多个文件和目录子树复制到单个目的地目录。

- **dest_file**：目的地文件的名称。如果未指定主机名和路径名，则现有文件将被复制到本地系统当前目录中名为 *dest_file* 的文件中。如果 *dest_file* 已经存在且可写，则现有文件将被覆盖。目的地文件名的构建方式与源文件相同，只是不能使用文件名扩展字符。

- **dest_dir**：目的地目录的名称。如果未指定主机名和路径名，则现有文件将被复制到本地系统当前目录中名为 *dest_dir* 的目录中。如果 *dest_dir* 已经存在于指定的目录路径中（如果未指定则为当前目录），则在名为 *dest_dir* 的现有目录下方创建一个新的名为 *dest_dir* 的目录。目的地目录名的构建方式与源目录树名称相同，只是不能使用文件名扩展字符。

- **file_or_dir**：如果为复制指定了文件和目录的组合（无论是显式指定还是通过文件名扩展），除非指定了 *-r* 选项，否则只复制文件。如果存在 *-r* 选项，则所有名称与指定 *file_or_dir* 名称匹配的文件和目录子树都会被复制。

- **-P**：保留（复制）源文件的修改时间和模式（权限），忽略当前 *umask* 文件创建模式掩码的设置。如果指定了此选项，*rcp* 仅当目标用户是超级用户时保留粘滞位。

如果未指定 *-p* 选项，如果 *dest_file* 已经存在，*rcp* 将保留 *dest_file* 的模式和所有者；否则 *rcp* 使用经过目的地主机上 *umask* 修改后的源文件模式。目的地文件的修改时间和访问时间被设置为复制发生时的时间。

- **-R**：递归地复制以源目录名为根的目录子树。如果要复制任何目录子树，*rcp* 将递归地将每个以指定源目录名为根的子树复制到目录 *dest_dir*。如果 *source_dir* 正在被复制到同名的现有目录中，*rcp* 会在 *dest_dir* 内创建一个新的 *source_dir* 目录，并将以 *source_dir* 为根的子树复制到 *dest_dir/source_dir*。如果 *dest_dir* 不存在，*rcp* 将创建它，并将以 *source_dir* 为根的子树复制到 *dest_dir*。

### 构建文件和目录名称

如上所述，文件和目录名称包含一个、两个或四个组件部分：

- **user_name**：用于访问远程系统上的目录和文件的登录名。
- **hostname**：目录和文件所在的远程系统的主机名。
- **pathname**：绝对目录路径名或相对于用户 *user_name* 登录目录的目录路径名。
- **filename**：源或目的地文件的实际名称。允许在源文件名上进行文件名扩展。
- **dirname**：源或目的地目录子树的实际名称。允许在源目录名上进行文件名扩展。

每个文件或目录参数要么是形式为 *hostname:path* 的远程文件名，要么是本地文件名（任何冒号 (:) 前都有斜杠 (/)）。Hostname 可以是正式主机名或别名（参见 hosts(4)）。如果 hostname 的形式为 *ruser@host*，则在远程主机上使用 *ruser* 而不是当前用户名。未指定的路径（即 *hostname:*）指的是远程用户的登录目录。如果路径不以 / 开头，则相对于 *hostname* 上远程用户的登录目录进行解释。远程路径中的 Shell 元字符可以用反斜杠 (\)、单引号 ('') 或双引号 (") 进行引用，以便它们在远程被解释。

rcp 程序不会提示输入密码。当前的本地用户名或通过 *ruser* 指定的任何用户名必须存在于 *rhost* 上，并允许通过 remsh(1) 和 rcmd(3) 执行远程命令。remshd(1M) 必须在远程主机上可执行。

形式的第三方传输：

```bash
rcp ruser1@rhost1:path1 ruser2@rhost2:path2
```

执行方式如下：

```bash
remsh rhost1 -l ruser1 rcp path1 ruser2@rhost2:path2
```

因此，为了使这种传输成功，*rhost2* 上的 *ruser2* 必须允许来自 *rhost1* 的 *ruser1* 访问（参见 hosts.equiv(4)）。

## 警告

rcp 程序会被远程主机上 .cshrc 文件中命令产生的任何输出弄糊涂（参见 csh(1)）。

将文件复制到其本身，例如：

```bash
rcp path 'hostname:path'
```

可能会导致不一致的结果。当前 HP-UX 版本的 rcp 只是将文件覆盖到其本身。然而，某些 rcp 的实现，包括某些早期 HP-UX 实现，会损坏文件。此外，同一文件可能通过多种方式引用，例如通过硬链接、符号链接或 NFS。不能保证 rcp 在所有情况下都能正确地将文件覆盖到其本身。

基于 4.2BSD 版本的 rcp 实现（包括 HP-UX 7.0 之前的 rcp 实现）要求将远程用户指定为 *rhost.ruser*。如果在第三方传输（以下示例中的 *rhost1*）中指定的第一个远程主机使用这种旧语法，则命令必须具有以下形式：

```bash
rcp ruser1@rhost1:path1 rhost2.ruser2:path2
```

因为目标由 *rhost1* 解释。经常遇到的一个常见问题是，当两个远程文件要复制到指定远程用户的远程目标时。如果两个远程源系统 *rhost1* 和 *rhost2* 各自期望不同的远程目标形式，则命令：

```bash
rcp rhost1:path1 rhost2:path2 rhost3.ruser3:path3
```

肯定会在其中一个源系统上失败。使用两个单独的命令来执行此类传输。

## 作者

rcp 由加利福尼亚大学伯克利分校开发。

## 参见

cp(1), ftp(1), remsh(1), remsh(1M), rcmd(3), hosts(4), hosts.equiv(4).

《使用 Internet 服务》中的 ftp 章节。

# rcp(1) 使用 Kerberos 认证的安全 Internet 服务

## 名称

rcp - 远程文件复制

## 概要

- 复制单个文件：
  `rcp [-k realm] [-P] [-p] source_file1 dest_file`
- 复制多个文件：
  `rcp [-k realm] [-P] [-p] source_file1 [source_file2]... dest_dir`
- 复制一个或多个目录子树：
  `rcp [-k realm] [-P] [-p] -r source_dir1 [source_dir2]... dest_dir`
- 复制文件和目录子树：
  `rcp [-k realm] [-P] [-p] -r file_or_dir1 [file_or_dir2]... dest_dir`

## 描述

rcp 命令将一个或多个系统中的文件、目录子树或文件与目录子树的组合复制到另一个系统。在许多方面，它类似于 cp 命令（参见 cp(1)）。

要使用 rcp，必须具有对正在复制文件的读取权限，以及对目录路径中所有目录的读取和搜索（执行）权限。

在 Kerberos V5 网络认证环境中，rcp 在启动与远程主机的连接时使用 Kerberos V5 协议。授权机制取决于用于在远程主机上调用 remsh 的命令行选项（即 -K、-R、-r 或 -k）。Kerberos 认证和授权规则在安全 Internet 服务手册页 sis(5) 中描述。

尽管可能应用 Kerberos 认证和授权，但在复制文件时不应用 Kerberos 机制。文件仍然以明文形式通过网络传输。

### 选项和参数

rcp 识别以下选项和参数：

- **source_file**：位于本地或远程机器上，您要复制到指定目的地的现有文件或目录的名称。源文件和目录名称按以下方式构建：
  `user_name@hostname:pathname/filename`
  或
  `user_name@hostname:pathname/dirname`

