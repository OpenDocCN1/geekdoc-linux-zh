
[bob@pcbsd-2823] ~% 

+   - 你已进入！请注销。

```
[bob@pcbsd-2823] ~% logout
$
```

+   - 你回到了原来的 shell 提示符。

+   - 从远程机器，通过 rlogin 或 rsh 登录到你刚刚启用 rlogin 和 rsh 的 PC-BSD 主机。

对于 Solaris 服务器：

+   - 将正确的主机名、IP 地址和用户权限放入你的主目录中的 `.login` 文件以及 `/etc/hosts.equiv` 文件中。有关说明，请参见 rlogin 和 rsh 的手册页。

+   - 使用以下两条命令检查 rlogin 是否已启用并正在运行：

```
bob@solaris:~$ svcadm enable svc://network/login:rlogin
svcadm: svc://network/login:rlogin: is not complete, missing general/complete (see svcs -xv svc://network/login:rlogin for details)
bob@solaris:~$ svcs -xv svc://network/login:rlogin
svc://network/login:rlogin (?)
State: -
Reason: Service is incomplete, defined only by profile /etc/svc/profile/generic.xml. To install this service, identify and install the package which provides the service's primary manifest. Use "pkg search 'svc://network/login\:rlogin'" to identify the package, then "pkg install <pkgs>" to install the indicated package.
Impact: This service is not running.
```

+   - 基于此，以超级用户身份按照 svcs 命令给出的说明进行操作。

```
bob@solaris:~$ su
Password: xxx
```

+   - 执行一次 pkg 搜索。

```
root@solaris:~# pkg search 'svc://network/login\:rlogin'
INDEX            ACTION VALUE            PACKAGE
```

+   - 现在从远程客户端机器对刚刚启用并运行 rlogin 的服务器测试 rlogin 和 rsh。

## 23.3 用户管理

用户管理的两个最重要目标是服务和安全：提供服务以确保用户群体能够访问并充分利用现代 UNIX 系统可提供的资源，以及保护用户群体利用这些资源所需的文件和进程。在本章后面，我们将介绍系统管理员可以部署的一些安全方法，以保持系统安全。在第 25 章中，我们还将展示围绕虚拟化技术（如 Jails、Zones 和 VirtualBox 虚拟机）的安全方法。

传统 UNIX 提供服务和保障安全的方法是通过访问权限实现的，即针对系统中的特定对象（如文件），为单个用户、用户组或系统中的所有其他用户设置访问权限。我们在第 5 章第 5.4 节和第 5.5 节中展示了如何设置文件的访问权限。设计并实现用户组以及用户组的访问权限，是该方法最重要的部分。

当然，用户账户的创建和配置是为用户群体提供最大服务和保障安全的第一步。

在接下来的部分中，我们将重点介绍如何在 PC-BSD 和 Solaris 上管理用户账户和用户组。这些操作通常在 UNIX 系统初始安装完成后的较长时间进行，但这并不意味着不能在系统初始化期间进行。接下来的示例说明了：

+   - 在 PC-BSD 上基于文本的用户账户创建与配置的两个简单案例
+   - PC-BSD 中的 GUI 账户创建与配置
+   - Solaris 中基于文本的账户创建与配置

向 UNIX 系统添加新用户账户通常涉及以下步骤：

+   1. 为用户分配用户名、用户 ID 号和主组，并决定新用户还应属于哪些其他组。将这些数据输入系统用户账户配置文件中。
+   2. 为新账户分配密码。
+   3. 为用户创建主目录。
+   4. 将默认或自定义初始化文件放入用户的主目录中。
+   5. 授予新用户对其主目录和初始化文件的所有权。
+   6. 设置其他对系统有用的用户账户配置细节。这包括磁盘配额和其他资源限制，以及系统特权。
