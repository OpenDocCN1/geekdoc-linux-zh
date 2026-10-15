
为使用 `LDAP` 身份验证的每个服务修改 `/etc/pam.d` 配置。示例 7-5 说明了用于 `Telnet` 登录的配置文件。

### 示例 7-5 用于 `LDAP` 身份验证的 `/etc/pam.d/login` 文件

```
#PAM-1.0
auth        required pam_nlogin.so
auth        sufficient pam_unix_auth.so
auth        required pam_ldap.so        try_first_pass
account     required pam_localuser.so
account     required pam_ldap.so
password    required pam_pwcheck.so      nullock
password    required pam_ldap.so        use_first_pass use_authok
password    required pam_unix.so        nullock use_first_pass use_authtok
session     required pam_unix_session.so
session     required pam_limits.so
session     required pam_env.so
session     optional pam_mail.so
```

这些更改包括：

1. `pam_unix_auth.so` 模块实现了 `auth` 类型用户身份验证，并能够支持 `NSS`。`sufficient` 控制标志确保在本地定义的（`/etc/passwd` 文件）通过验证时操作成功。
2. 如果对本地的 `auth` 类型身份验证失败，所需的 `pam_ldap.so` 模块尝试使用 `LDAP` 进行身份验证。
3. `pam_localuser.so` 模块为本地用户执行账户身份验证。`sufficient` 控制标志在本地用户通过验证时确保操作成功。
4. 如果对本地用户的 `account` 类型身份验证再次失败，`pam_ldap.so` 模块通过 `LDAP` 进行身份验证。
5. `pam_ldap.so` 模块能够对 `LDAP` 目录执行密码更新。

> **提示**：虽然可以将所有用户信息维护在远程 `LDAP` 目录中，但在本地至少定义一个具有超级权限的用户是好的。这在 `LDAP` 不可用时允许访问主机。

`Linux` 用户通常在定义用户 ID 时创建其主目录（通常为 `/home/userid`）。当使用 `LDAP` 身份验证时，用户是远程定义的（没有在本地创建主目录 `host`）。为了避免为每个定义的 `LDAP` 用户手动创建主目录，有两种方法：

*   用户主目录可以位于网络文件服务器上（例如，`NFS` 挂载的文件系统）。
*   主目录可以在用户首次登录时自动创建：
    *   对于除 `SSH` 以外的登录服务，请向该服务的 `PAM` 配置文件（`/etc/pam.d/login`）添加 `pam_mkhomdir.so` 模块（例如）：

```
session required pam_mkhomdir.so skel=/etc/skel umask=0077
```

    *   如果通过验证且不存在主目录，则会在 `/home` 中创建主目录。`umask=0077` 参数将目录设置为 `700`。主目录由 `/etc/skel` 目录中的骨架文件构建。
    *   从 `OpenSSH` 版本 3.3 开始，由于 `SSH` 的安全修改，不再支持使用 `pam_mkhomdir.so` 自动创建主目录。你可以使用 `home_dir` 包替换 `pam_mkhomdir.so`。`make_home_dir` 包可在以下地址获取：

http://www.trustsec.de/soft/oss

## 配置 `NSS`

为了完成此过程，我们配置 `NSS` 使用 `LDAP` 进行用户和组验证。我们修改 `/etc/nsswitch` 配置文件，如示例 7-6 所示。

### 示例 7-6 用于 `LDAP` 认证的 `/etc/nsswitch` 文件

```
passwd: ldap compat
group: ldap compat
shadow: ldap compat
```

接下来，我们创建 `/etc/nss_ldap.conf` 文件，如示例 7-7 所示。

### 示例 7-7 用于 `LDAP` 认证的 `/etc/nss_ldap.conf` 文件

```
#  LDAP 服务器。必须在不使用 LDAP 的情况下解析。
host 9.12.6.16:3389
# 搜索基的区分名称
base=itso
uri ldaps://9.12.6.16:3389
ldap_version 3
```

`base` 参数使用 `z/OS` `LDAP` 服务器定义的后缀。`uri` 参数指向运行在 `z/OS` 上的 `LDAP` 服务器。

## 7.4 `IBM Tivoli Access Manager WebSEAL`

`IBM Tivoli Access Manager WebSEAL` 是用于 Web 资源的安全管理器。`WebSEAL` 是一种高性能、多线程的 Web 服务器，它对受保护的 Web 对象空间应用细粒度的安全策略。`WebSEAL` 可以提供单点登录解决方案，并将后端 Web 服务器资源整合到其安全策略中。

除了验证 `Linux` 用户外，我们还可以结合 `z/OS` 使用 `WebSEAL` 来保护 Web 基础资源。此场景如图 7-3 所示。

![](img/a2760634ecd5eb26c25e81867e88d740_162_0.png)

**图 7-3** 对 `z/OS RACF` 数据库验证用户

在这种场景中，我们使用单个 `Tivoli Access Manager` 实例。为了扩展性和高可用性，需要多个 `Tivoli Access Manager`/`Linux` 实例。

请求分发机制将负载分布到所有实例（例如，轮询 `DNS` 或使用 `LVS` 的 `Linux` 集群）。

### 7.4.1 配置 `WebSEAL`

要配置 `WebSEAL`：

1. 首先，使用命令从 `Tivoli Access Manager` 安装 `PDWeb-PD-4.1.0-2.s390.rpm` 包：

```
rpm -ivh PDWeb-PD-4.1.0-2.s390.rpm
```

2. 使用 `pdconfig` 命令配置 `WebSEAL`。`e-business` 的 `Access Manager` 设置菜单如示例 7-8 所示。

#### 示例 7-8 `Access Manager` 设置菜单

```
Access Manager for e-business Setup Menu 

1. Configure Package

2. Unconfigure Package

3. Display Configuration Status

x. Exit

请选择菜单项 [x]: 1
```

3. 选择选项 1 以导航到示例 7-9 所示的 `Access Manager` 配置菜单。

#### 示例 7-9 `Access Manager` 配置菜单

```
Access Manager for e-business Configuration Menu

1. Access Manager WebSEAL Configuration

x. Return to Access Manager for e-business Setup Menu

请选择菜单项 [x]: 1
```

4. 选择选项 1 以导航到示例 7-10 所示的 `Access Manager WebSEAL` 设置菜单。

#### 示例 7-10 `Access Manager WebSEAL` 设置菜单

```
Access Manager WebSEAL for e-business Setup Menu

1. Configure

2. Display Configuration Status

x. Exit

请选择菜单项 [x]: 1
```

5. 选择选项 1。系统提示输入 `Tivoli Access Manager` 管理员 (`sec_master`) 密码。我们使用密码 `secret`。

**注意**：如果反复输入错误密码，可能会收到错误：

```
Error: This account has been temporarily locked out due to too many failed login attempts.
```

获取正确的密码，等待五分钟解锁锁定，然后重启 `pdconfig` 命令。

6. 系统提示启用 `WebSEAL` 服务器与 `LDAP` 服务器之间的 `SSL` 通信。输入 `y`（是）或 `n`（否）以启用 `Access Manager` 服务器与 `LDAP` 服务器之间的 `SSL` 通信：

```
Do you want to enable SSL communication between the Access Manager server and the LDAP server (y/n) [Yes]?
```
