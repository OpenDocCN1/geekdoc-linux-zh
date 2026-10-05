

# 引导练习

## 启用 YUM 软件仓库

在本次练习中，你将配置服务器以从远程 Yum 仓库获取软件包，然后从该仓库更新或安装软件包。

### 预期结果

你应当能够配置系统从教室服务器获取软件更新，并更新系统以使用最新软件包。

### 准备工作

在工作站上以学生用户身份登录，密码为 `student`。

在工作站上运行 `lab software-repo start` 命令。该命令运行一个启动脚本，用于判断主机服务器 servera 是否可以在网络上访问。该脚本还会确保已安装 `yum` 软件包。

```
[student@workstation -]$ lab software-repo start
```

- 1. 使用 `ssh` 命令以 `student` 用户身份登录到 servera。

```
[student@workstation -]$ ssh student@servera
[student@servera -]$
```

- 2. 使用 `su -` 在 shell 提示符下切换到 root。

```
[student@servera -]$ su -
Password: redhat
[root@servera -]$
```

- 3. 在 servera 上配置软件仓库，以便从以下 URL 获取自定义软件包和更新：

  - 自定义软件包提供的地址：http://content.example.com/rhel8.0/x86_64/rhsa-practice/rht
  - 自定义软件包的更新位于：http://content.example.com/rhel8.0/x86_64/rhsa-practice/errata

3.1. 使用 `yum-config-manager` 添加自定义软件包仓库。

```
[root@servera -]$ yum-config-manager \
> --add-repo "http://content.example.com/rhel8.0/x86_64/rhsa-practice/rht"
Adding repo from: http://content.example.com/rhel8.0/x86_64/rhsa-practice/rht
```

# 第 14 章 | 安装和更新软件包

3.2. 检查 `/etc/yum.repos.d` 中由上命令创建的软件仓库。使用 `vim` 命令编辑文件并添加 `gpgcheck=0` 以禁用该仓库的 GPG 密钥检查。

```
[root@server#]# vim
> /etc/yum.repos.d/content.example.com.rhel8.0_x86_64.rhsa-practice_rht.repo
[content.example.com.rhel8.0_x86_64.rhsa-practice_rht]
name=created by dnf config-manager from http://content.example.com/rhel8.0/x86_64/rhsa-practice/rht
baseurl=http://content.example.com/rhel8.0/x86_64/rhsa-practice/rht
enabled=1
gpgcheck=0
```

3.3. 创建 `/etc/yum.repos.d/errata.repo` 文件，并以下内容启用更新仓库：

```
[rht-updates]
name=rht updates
baseurl=http://content.example.com/rhel8.0/x86_64/rhsa-practice/errata
enabled=1
gpgcheck=0
```

3.4. 使用 `yum reposolist -a` 列出系统上的所有仓库：

```
[root@server -]# yum reposolist all
repo id repo name status
content.example.com.rhel8.0_x86_64.rhsa-practice_rht created by .... enabled: 2
rht-updates rht updates enabled: 2
...output omitted...
```

- 4. 禁用 `rht-updates` 软件仓库并安装 `rht-system` 软件包。

4.1. 使用 `yum-config-manager --disable` 禁用 `rht-updates` 仓库。

```
[root@server -]# yum-config-manager --disable rht-updates
```

4.2. 列出并安装 `rht-system` 软件包：

```
[root@server -]# yum list rht-system
Available Packages
rht-system.noarch 1.0.0-1 content.example.com.rhel8.0_x86_64-rhsa-practice-rht
[root@server -]# yum install rht-system
Dependencies resolved.

=======================================================================
Package Arch Version Repository Size
=======================================================================
Installing:
rht-system noarch 1.0.0-1 content...._rht 3.7 k
...output omitted... 
Is this ok [y/N]: y
```

![](img/59afb92e10b67a9cecc358a2c65e93b5_525_0.png)

```
...output omitted...
Installed:
rht-system-1.0.0-1.noarch
Complete!
```

4.3. 验证 `rht-system` 软件包已安装，并记录该软件包的版本号。

```
[root@servera ~]# yum list rht-system
Installed Packages
rht-system.noarch 1.0.0-1@content.example.com_rhel8.0_x86_64_rhca-practice_rht
```

- 5. 启用 `rht-updates` 仓库并更新所有软件包。

5.1. 使用 `yum-config-manager --enable` 启用 `rht-updates` 仓库。

```
[root@servera ~]# yum-config-manager --enable rht-updates
```

5.2. 使用 `update` 命令更新所有软件包。

```
[root@servera ~]# yum update
Dependencies resolved.

=======================================================================
Package Arch Version Repository Size
=======================================================================
Updating:
rht-system noarch 1.0.0-1 content...._rht 3.7 k
...output omitted...
Is this ok [y/N]: y
...output omitted...
Complete!
```

5.3. 验证 `rht-system` 软件包已安装并更新。

```
[root@servera ~]# yum list rht-system
Installed Packages
rht-system.noarch 1.0.0-1@content.example.com_rhel8.0_x86_64_rhca-practice_rht
```

- 6. 退出会。

```
[root@servera ~]# exit
[student@servera -]# exit
[student@workstation -]# exit
```

