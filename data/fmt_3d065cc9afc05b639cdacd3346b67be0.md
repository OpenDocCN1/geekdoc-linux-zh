
上述输出解析了依赖项并显示了将移除的软件包列表以及将释放的磁盘空间。确认继续后，删除了标识的软件包。

更多信息请参考 `dnf` 命令手册页的 `remove` 章节。

## 练习 10-3: 操作软件包组

此练习应在 `server1` 上使用 `sudo` 执行。在此练习中，你将对名为 `system tools` 的软件包组进行管理操作。确定该组是否已安装或可用安装。最后，你将移除该组及其依赖项。

### 1. 检查 `system tools` 软件包组是否已安装：

```
[user1@server1 ~]$ dnf group list
Installed Environments: Server
Installed Groups: Desktop
Available Environments:
Available Groups: Base
system
```

输出未显示 `system tools` 已安装。

### 2. 确定 `system tools` 软件包组是否可用安装：

```
[user1@server1 ~]$ dnf group list
Installed Environments: Server
Installed Groups: Desktop
Available Environments:
Available Groups: Base
system
system tools
```

该组可用。

### 3. 显示 `system tools` 组的软件包列表：

```
[user1@server1 ~]$ dnf group info 'system tools'
Group: system tools
Description: 用于系统监控、网络和共享的各种工具集合。
Mandatory Packages:
bash
bash-completion
coreutils
file
linux
mail
psutils
util-linux
Packages in this group:
- bash
- bash-completion
- coreutils
- file
- linux-core
- linux-headers
- linux-tools
- mail
- psutils
- util-linux
```

### 4. 安装 `system tools` 组：

```
[user1@server1 ~]$ sudo dnf -y groupinstall 'system tools'
Dependencies resolved.
==============================================================
Package                 Arch            Version         Repository      Size
==============================================================
Installing group/module packages:
NetworkManager-libreswan  x86_64   1.20-3.el18      AppStream       120 k
libreswan                x86_64   3.27-9.el18      AppStream       3 M
map                      x86_64   2.70-4.el18      AppStream       57 k
tigercnu                  x86_64   1.9-0.el18      AppStream       26 k
cifs-utils               x86_64   6.8-2.el18       AppStream       93 k
openldap-clients         x86_64   2.46-9.el18      AppStream       636 k
samba-client             x86_64   4.9.1.el.18     AppStream       202 k
seterial                  x86_64   2.17-4.el18      AppStream       32 k
tntx                      x86_64   2.7-1.el18       AppStream       17 k
delta                    x86_64   1.10-4.el18      AppStream       96 k
Installing dependencies:
ldns                     x86_64   1.7.0-20.el18   AppStream       575 k
fix                      x86_64   1.2.3-4.el18      AppStream       165 k
mesa-libGL                x86_64   9.0-15.el18      AppStream       185 k
nss-tools                 x86_64   3.41.0-5.el18   AppStream       567 k
tigercnu-icons            noarch           1.9-9.el18      AppStream       46 k
Installing Groups:
system Tools
```

事务摘要

================================================================

安装 15 个软件包

================================================================

总大小: 10 M

安装大小: 39 M

已更新安装产品。

```
Installed:
NetworkManager-libreswan-1.20-3.el18.x86_64
libreswan-3.27-9.el18.x86_64
map-2.70-4.el18.x86_64
tigercnu-1.9-0.el18.x86_64
cifs-utils-6.8-2.el18.x86_64
openldap-clients-2.46-9.el18.x86_64
samba-client-4.9.1.el.18.x86_64
seterial-2.17-4.el18.x86_64
tntx-2.7-1.el18.x86_64
delta-1.10-4.el18.x86_64
ldns-1.7.0-20.el18.x86_64
fix-1.2.3-4.el18.x86_64
mesa-libGL-9.0-15.el18.x86_64
nss-tools-3.41.0-5.el18.x86_64
tigercnu-icons-1.9-9.el18.noarch
```

完成！

### 5. 移除 `system tools` 组：
