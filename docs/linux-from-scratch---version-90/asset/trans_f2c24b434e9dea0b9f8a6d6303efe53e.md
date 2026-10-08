

## 6.19. MPC-1.1.0

MPC 软件包包含一个用于任意高精度复数算术以及结果正确舍入的库。

**预计编译时间：** 0.3 SBU
**所需磁盘空间：** 22 MB

### 6.19.1. 安装 MPC

为编译准备 MPC 准备：

```
./configure --prefix=/usr \
--disable-static \
--dodecdir=/usr/share/doc/mpc-1.1.0
```

编译程序包并生成 HTML 文档：

```
make
make html
```

测试结果，请执行：

```
make check
```

安装程序包及其文档：

```
make install
make install-html
```

### 6.19.2. MPC 内容

**已安装的库：** libmpc.so
**已安装的目录：** /usr/share/doc/mpc-1.1.0

# 概要说明

- **libmpc** 包含复数数学函数

## 6.20. Shadow-4.7

Shadow 软件包包含用于安全方式处理密码的程序。

**预计编译时间：** 0.2 SBU
所需磁盘空间： 46 MB

### 6.20.1. 安装 Shadow

> 如果你想强制使用强密码，请参阅 http://www.linuxfromscratch.org/blfs/view/9.0posts/cracklib.html，在构建 Shadow 之前安装 CrackLib。然后在在下面的 configure 命令中添加 --with-libcrack。

禁用 **groups** 程序及其 man 手册的安装，因为 Coreutils 提供了更好的版本。防止安装已在第 6.8 节“Man-pages-5.02”中安装过的手动帮助页：

```
sed -i 's/groups$(EXEEXT)/' src/Makefile.in
find man -name Makefile.in -exec sed -i 's/groups/.1 /' - {} \;
find man -name Makefile.in -exec sed -i 's/getpasswd/.3 /' - {} \;
find man -name Makefile.in -exec sed -i 's/password/.5 /' - {} \;
```
不要使用 crypt 方法，而是使用更安全的 SHA512 方法密码加密，它允许超过 8 个字符的密码。也有必要更改 Shadow 默认使用的旧 /var/spool/mail/ 目录，当前：

```
sed -i 's@#ENCRYPT_METHOD DES@SHA512@' s@/var/spool/mail/'etc/login.defs
```
> 如果你选择带有 Cracklib 支持构建 Shadow，请运行：

```
sed -i 's@DICTPATH.*$DICTPATH@lib/cracklib/' etc/login.defs
```
将 useradd 生成的第一个组号更改为 1000：

```
sed -i 's/1000/999/' etc/useradd
```

为编译准备 Shadow：

```
./configure --sysconfdir=/ --with-group-name-max-length=32
```

configure 选项的含义：

```
--with-group-name-max-length=32
```
用户名最大 32 个字符。组名也是。

编译程序包：

```
make
```

Linux From Scratch - 版本 9.0

此软件包不带测试套件。

安装程序包：

```
make install
```

将位置错误的程序移动到正确位置：

```
mv -v /usr/bin/passwd /bin
```

## 6.20. 配置 Shadow

此软件包包含添加、修改和删除用户及组；设置和更改密码以及执行其他管理任务的实用。关于密码管理的完整解释，请查看树中的 HOWTO 文件。如果支持 Shadow，请记住需要验证密码的程序（显示管理器、FTP 程序、pop3 守护进程等）必须符合 Shadow。

启用密码，运行以下命令：

```
pwconv
```

启用影子组密码，运行：

```
grpconv
```

Shadow 对 useradd 工具的配置有一些需要说明的地方。useradd 工具的默认操作是创建一个与用户同名的组。默认情况下，用户 ID (UID) 和组 ID (GID) 数字为 1000。这意味着如果你不向 useradd 传递参数，每个用户将是系统中唯一组的成员。如果这种行为不受希望，你需要向 useradd 传递 -g 参数。默认参数存储在 /etc/default/useradd 文件中。你可能需要根据特定需求修改该文件中的两个参数。

/etc/default/useradd 参数说明

```
GROUP=1000
```
此参数设置 /etc/group 文件中使用的数字起始。你可以根据需要修改它。注意 useradd 永远不会重用 UID 或 GID。参数中指定的数字已被使用，之后将使用下一个可用数字。另外，如果你第一次在使用 useradd 时没有 -g 参数，终端会显示：useradd: unknown GID 1000。你可以忽略此信息和组号 1000。

```
CREATE_MAIL_S=yes
```
此参数导致 useradd 为新用户创建一个邮箱文件。useradd 将此文件的组所有设置为 mail ，权限为 0660。如果你希望 useradd 不创建这些邮箱文件，请使用以下命令：

```
sed -i 's/yes/no/' /etc/default/useradd
```

## 6.20.3. 设置 root 密码

为 root 用户选择并设置密码：

```
passwd root
```

### 6.20.4. Shadow 内容

已安装程序：

chage, chfn, chpassword, chsh, expiry, faillog, gpassword, groupadd, groupdel, groupmems, groupdp, grpk, grpcv, grpunv, lastlog, login, newgidmap, newgrp, newuidmap, news, passwd, pw, pwconv, su, userdel, usermod, vigr

已安装目录：

/etc/shadow

# 概要说明

- **chage**: 用于更改更改之间的最大天数。
- **chfn**: 用于更改用户的全名和其他信息。
- **chpassword**: 用于批量模式更新组密码。
- **chpasswd**: 用于批量模式更新用户密码。
- **chsh**: 用于更改用户的默认 shell。
- **expiry**: 检查并强制当前密码过期。
- **faillog**: 用于检查登录日志，在账户被锁定之前设置最大失败次数。
- **gpassword**: 用于向组添加和删除成员。
- **groupadd**: 创建指定名称的组。
- **groupdel**: 删除指定名称的组。
- **groupmems**: 允许用户管理/其组成员关系。
- **groupmod**: 用于修改组名或 ID。
- **grpck**: 验证组文件 /etc/group 和 /etc/shadow 的完整性。
- **grpcn**: 从密码文件创建或更新 shadow 文件。
- **grpunv**: 更新 /etc/group 并后者。
- **lastlog**: 报告所有用户或指定用户的最近登录情况。
- **login**: 系统用于让用户登录。
- **logout**: 是一个用于限制登录时间和端口的守护进程。
- **newgidmap**: 用于设置命名空间的 gid 映射。
- **newgrp**: 用于在登录会期间更改当前 GID。
- **newuidmap**: 用于设置命名空间的 uid 映射。
- **news**: 用于创建或更新一系列用户账户。
- **nologin**: 显示账户不可用的消息；被设计为被禁用账户的默认 shell。
- **passwd**: 用于更改用户或组账户的密码。
- **pwck**: 验证密码文件 /etc/passwd 和 /etc/shadow 的完整性。
- **pwconv**: 从密码文件创建或更新 shadow 密码。
- **su**: 以替换用户和组 ID 运行 shell。
- **useradd**: 创建指定名称的新用户，或更新默认新用户信息。
- **userdel**: 删除指定的用户账户。
- **usermod**: 用于修改给定用户的登录名、用户标识 (UID)、shell、初始组、主目录等。
- **vigr**: 编辑 /etc/group 或 /etc/gshadow 文件。

