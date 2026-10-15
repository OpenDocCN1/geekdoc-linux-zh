
```
rsync -rv "//cygdrive/c/Documents and Settings/%USERNAME%/My Documents/" \
'user@server:My\ Documents/'
```

### 自动备份

使用批处理文件来自动化备份并将文件添加到计划任务中（程序 -> 附件 -> 系统工具 -> 计划任务）。例如创建文件 `backup.bat` 并替换 `user@server`。

```
@ECHO OFF
REM rsync the directory My Documents
SETLOCAL
SET CWRSYNCHOME=C:\PROGRAM FILES\CWRSYNC
SET CYGWIN=nontsec
SET CWOLDPATH=%PATH%
REM uncomment the next line when using cygwin
SET PATH=%CWRSYNCHOME%\BIN;%PATH%
echo Press Control-C to abort
rsync -av "//cygdrive/c/Documents and Settings/%USERNAME%/My Documents/" \
'user@server:My\ Documents/'
pause
```

## 8 SUDO

`Sudo` 是一种标准方法，可在不泄露 root 密码的情况下授予用户部分管理权限。在多用户环境且同时存在服务器和工作站的情况下，`Sudo` 非常有用。只需使用 `sudo` 调用命令：

```
# sudo /etc/init.d/dhcpd restart          # Run the rc script as root
# sudo -u sysadmin whoami                 # Run cmd as an other user
```

### 8.1 配置

`Sudo` 在 `/etc/sudoers` 中进行配置，且只能使用 `visudo` 进行编辑。基本语法是（列表以逗号分隔）：

```
user hosts = (runas) commands          # In /etc/sudoers
```

- `users` 一个或多个用户或 `%组`（如 `%wheel`）以获得权限

- `hosts` 主机列表（或 `ALL`）

- `runas` 命令规则可以作为其运行的用户列表（或 `ALL`）。它用 `( )` 括起来！

- `commands` 将作为 `root` 或作为 `(runas)` 运行的命令列表（或 `ALL`）

此外，这些关键字可以定义为别名，它们称为 `User_Alias`、`Host_Alias`、`Runas_Alias` 和 `Cmdn_Alias`。这对于大型设置很有用。下面是一个 `sudoers` 示例：

```
# cat /etc/sudoers
# Host aliases are subnets or hostnames.
Host_Alias  DMZ    = 212.118.81.40/28
Host_Alias  DESKTOP = work1, work2

# User aliases are a list of users which can have the same rights
User_Alias  ADMINS = colin, luca, admin
User_Alias  DEVEL  = joe, jack, julia
Runas_Alias DBA   = oracle, pgsql

# Command aliases define the full path of a list of commands
Cmd_Alias   SYSTEM = /sbin/reboot,/usr/bin/kill,/sbin/halt,/sbin/shutdown,/etc/init.d/
Cmd_Alias   PW     = /usr/bin/passwd [A-Z]*, !/usr/bin/passwd root # Not root pwd!
Cmd_Alias   DEBUG  = /usr/bin/tcpdump,/usr/bin/wireshark,/usr/bin/nmap

# The actual rules
root,ADMINS ALL = (ALL) NOPASSWD: ALL    # ADMINS can do anything w/o a password.
DEVEL   DESKTOP = (ALL) NOPASSWD: ALL    # Developers have full right on desktops
DEVEL   DMZ     = (ALL) NOPASSWD: DEBUG  # Developers can debug the DMZ servers.

# User sysadmin can mess around in the DMZ servers with some commands.
sysadmin DMZ    = (ALL) NOPASSWD: SYSTEM,PW,DEBUG
sysadmin ALL,!DMZ = (ALL) NOPASSWD: ALL  # Can do anything outside the DMZ.
%db a    ALL    = (DBA) ALL             # Group dba can run as database user.

# anyone can mount/unmount a cd-rom on the desktop machines
ALL     DESKTOP = NOPASSWD: /sbin/mount /cdrom,/sbin/umount /cdrom
```

## 9 加密文件

### 9.1 OpenSSL

#### 单个文件

加密和解密：

```
# openssl aes-128-cbc -salt -in file -out file.aes
# openssl aes-128-cbc -d -salt -in file.aes -out file
```

请注意，文件当然可以是 `tar` 归档。

#### tar 并加密整个目录

```
# tar -cf - directory | openssl aes-128-cbc -salt -out directory.tar.aes    # Encrypt
# openssl aes-128-cbc -d -salt -in directory.tar.aes | tar -x -f -          # Decrypt
```

#### tar zip 并加密整个目录

```
# tar -zcf - directory | openssl aes-128-cbc -salt -out directory.tar.gz.aes   # Encrypt
# openssl aes-128-cbc -d -salt -in directory.tar.gz.aes | tar -xz -f -         # Decrypt
```

- `-` 在 `aes-128-cbc` 后使用 `-k mysecretpassword` 可避免交互式密码请求。然而请注意，这非常不安全。

- `-` 使用 `aes-256-cbc` 代替 `aes-128-cbc` 可获得更强的加密。这也会使用更多 CPU。

### 9.2 GPG

`GnuPG` 以加密和签名电子邮件或任何数据而闻名。此外 `gpg` 还提供了一个高级密钥管理系统。本节仅涵盖文件加密，不涉及电子邮件使用、签名或 Web-Of-Trust。

最简单的加密是使用对称密码。在这种情况下，文件使用密码加密，任何知道密码的人都可以解密它，因此不需要密钥。`Gpg` 会在加密的文件名后添加扩展名 `".gpg"`。

```
# gpg -c file                         # Encrypt file with password
# gpg file.gpg                        # Decrypt file (optionally -o otherfile)
```

#### 使用密钥

更多细节请参阅 `GPG Quick Start`¹⁴ 和 `GPG/PGP Basics`¹⁵ 以及 `gnupg` 文档¹⁶ 等。

私钥和公钥是非对称加密的核心。需要记住的重要事项：

- `-` 你的公钥由他人用于加密文件，只有你作为接收者可以解密（甚至加密该文件的人也无法解密）。因此公钥旨在分发。

- `-` 你的私钥使用你的密码短语加密，并用于解密用你的公钥加密的文件。私钥必须保密。此外，如果密钥或密码短语丢失，则所有用你的公钥加密的文件也将丢失。

- `-` 密钥文件称为 `keyrings`，因为它们可以包含多个密钥。

首先生成一个密钥对。默认值即可，不过你至少需要输入你的全名和电子邮件，可选地输入注释。注释对于使用相同姓名和电子邮件创建多个密钥很有用。此外你应该使用“密码短语”，而不是简单的密码。

```
# gpg --gen-key                         # This can take a long time
```
