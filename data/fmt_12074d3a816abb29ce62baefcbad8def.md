
与`/etc/passwd`文件一样，条目由冒号分隔。从左到右，条目分别是：

- 用户名
- 加密密码
- 密码修改日期（自 1970 年 1 月 1 日起的数，标记可以更改密码的日期）
- 可以更改密码的天数
- 必须更改密码的天数
- 密码过期前警告用户的天数
- 密码过期后禁用账户的天数
- 账户禁用日期（自 1970 年 1 月 1 日起的数，标记账户禁用的日期）
- 系统预留数据

由于`/etc/shadow`文件仅`root`用户可读，除非`root`用户账户被破解，否则系统上的加密密码无法破解。

# 技巧 10.3.8：启用影子密码时编辑 passwd 文件

在启用影子密码的情况下，你仍然可以用未使用影子密码时的方式编辑`/etc/passwd`文件，可以更改用户名或密码以外的任何条目。但请记住，当系统或另一个应用程序（如`passwd`程序）尝试更改文件内容时，你不应该编辑该文件。为了解决这个问题，Linux 使用`vipw`程序，它可以让你安全地编辑`/etc/passwd`文件。为了确保编辑过程的安全，`vipw`程序会创建密码文件的副本并让你编辑该副本。当你完成编辑后，它会将你的更改更新到真实的`/etc/passwd`文件。

# 让 LINUX 运行起来：核心技巧与技术

Linux-PAM 网站地址为`http://www.kernel.org/pub/linux/libs/pam/index.html`。

## 技巧 13.10：添加新的 PAM 模块

安装 PAM 模块的方法因模块而异，取决于你是需要下载源代码并编译模块，还是接收预编译好的版本。一旦编译完成，模块将以共享对象文件的形式存在，其名称带有`pam_`前缀并以`.so`扩展。

通常，模块存储在`/lib/security`中。例如，以下目录列出了 RedHat Linux 7 中`/lib/security`目录的内容：

```
$ ls /lib/security/<ENTER>

pam_access.so          pam_lastlog.so       pam_radius.so

pam_unix_acct.so

pam_console.so        pam_limits.so        pam_rosths_auth.so

pam_unix_auth.so

pam_cracklib.so       pam_listfile.so     pam_rootok.so

pam_unix_passwd.so

pam_denyl.so          pam_localuser.so    pam_securetty.so

pam_unix_session.so

pam_env.so           pam_mail.so         pam_shells.so

pam_userdb.so

pam_filter           pam_mkhomedir.so    pam_stack.so

pam_warn.so

pam_filter.so        pam_motd.so          pam_stress.so

pam_wheel.so

pam_ftp.so           pam_nologin.so      pam_tally.so

pam_xauth.so

pam_group.so         pam_permit.so       pam_time.so

pam_issue.so         pam_pwdb.so         pam_unix.so
```

要安装新模块，请下载模块并根据需要进行编译。接下来，将共享对象文件拷贝到`/lib/security`目录：

```
# cp <shared object file name> /lib/security<ENTER>
```

## 10：管理 Linux 系统

### 技巧 10.3.11：编辑 /etc/pam.d 中的 PAM 配置文件

PAM 配置信息以两种方式之一存储：存储在一个名为`/etc/pam.conf`的单个文件中，或者存储在`/etc/pam.d/`目录下的独立文件中。RedHat Linux 7 采用了后者方法，而这也是本技巧中将讨论的方法。

`/etc/pam.d/`目录包含一系列文件。每个文件以一个使用 PAM 进行身份验证的服务命名，并包含 PAM 在为该特定服务提供身份验证时应使用的配置信息。例如，RedHat Linux 7 标准`/etc/pam.d/`目录包含以下内容：

```
chfn            kbdrate         other               rlogin

update

chsh            kde             rp3-config

update-config

ftp             kppp            poweroff        rsh                xdm

gdm             linuxconf      ppp                samba

screensaver

gnorpm-auth     linuxconf-auth reboot  sshd

xxver

halt            linuxconf-pair  rexec              su

isdn-config     login           rhn_register   system-auth
```

例如，`login`文件告诉 PAM 如何处理来自登录服务的身份验证：

```
##PAM-1.0

auth required      /lib/security/pam_securetty.so

auth required      /lib/security/pam_stack.so

service=system-auth

auth required      /lib/security/pam_nologin.so

account required    /lib/security/pam_stack.so

service=system-auth

password required   /lib/security/pam_stack.so

service=system-auth
```

```
session required /lib/security/pam.so

session=system-auth
```

```
session optional /lib/security/pam_console.so
```

此`login`文件包含一系列 PAM 配置指令，每行一个，它们告诉 PAM 如何为登录服务执行身份验证。每个条目的格式如下：

```
<module type> <control flag> <module path> <arguments>
```
