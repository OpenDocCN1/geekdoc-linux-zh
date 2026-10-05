

## 第 4 章 | 安装和更新软件包

```bash
python27 2.7 [d] common [d] Python programming ..., version 2.7
python36 3.6 [d] common [d], build Python programming ..., version 3.6
```
提示: [d]默认, [e]启用, [x]禁用, [i]已安装

### 3.2. 使用 yum module list --installed 命令列出已安装的模块和流（streams）。

```bash
[root@servera ~]# yum module list --installed
Red Hat Enterprise Linux 8.0 AppStream (dvd)
Name Stream Profiles Summary
postgresql 9.6 [e] client, server [d] [i] PostgreSQL server and client ...
```
提示: [d]默认, [e]启用, [x]禁用, [i]已安装

### 3.3. 使用 yum module info 命令检查 python36 模块的详情。

```bash
[root@servera ~]# yum module info python36
Name : python36
Stream : 3.6 [d]
Version : 828010123171828
Context : 17efdbc7
Profiles : common [d], build
Default profiles : common
Repo : rhel-8.0-for-x86_64-appstream-rpm
Summary : Python programming language, version 3.6
...output omitted.
```
提示: [d]默认, [e]启用, [x]禁用, [i]已安装, [a]激活

### 4. 从 3.6 流和 common 配置文件安装 python36 模块。验证该模块的当前状态。

#### 4.1. 使用 yum module install 安装 python36 模块。使用 name:stream/profile 语法从 3.6 流和 common 配置文件安装 python36 模块。

> 注意
你可以省略 /profile 来使用默认配置文件，并省略 :stream 来使用默认流。

```bash
[root@servera ~]# yum module install python36:3.6/common
...output omitted...
Is this ok [y/N]: y
...output omitted...
```

或者，你可以先启用该模块，使其软件包对系统可用而无需安装。然后使用 yum install @python36 命令安装模块内的软件包。

```bash
[root@servera ~]# yum module enable python36:3.6/common
[root@servera ~]# yum install @python36
...output omitted...
Is this ok [y/N]: y
...output omitted...
Complete!
```

### 4.2. 检查 python36 模块的当前状态。

```bash
[root@servera ~]# yum module list python36
Red Hat Linux 8.0 AppStream (dvd)
Name Stream Profiles Summary
python36 3.6 [d][e] common [d] [i], build Python programming ..., version 3.6
```
提示: [default], [e], [disabled], [i]installed

### 5. 将服务器（profile）的 postgresql 模块切换到 10 流。

#### 5.1. 使用 yum module 命令列出 postgresql 模块和流。注意 postgresql:9.6 模块当前已安装。

```bash
[root@servera ~]# yum module list postgresql
Red Hat Enterprise 8.0 AppStream (dvd)
Name Stream Profiles Summary
postgresql 10 [d] client, server [d] PostgreSQL server and client
postgresql 9.6 [e] client, server [d] PostgreSQL server and client
```
提示: [default], [e], [disabled], [i]installed

#### 5.2. 使用 yum module install 切换到 postgresql:10 模块流。

```bash
[root@servera ~]# yum module install postgresql:10
...output omitted...
Is this ok [y/N]: y
...output omitted...
Complete!
```

#### 5.3. 验证 postgresql 模块已切换到 10 流。

```bash
[root@servera ~]# yum module list postgresql
Red Hat Enterprise 8.0 AppStream (dvd)
Name Stream Profiles Summary
postgresql 10 [d][e] client, server [d] [i] PostgreSQL server and client
postgresql 9.6 client, server [d]
```

### 6. 移除并禁用 postgresql/module 流，以及由配置文件安装的所有软件包。

#### 6.1. 使用 yum remove 命令移除 postgresql/module。该命令还会移除从此模块安装的所有软件包。

```bash
[root@servera ~]# yum remove postgresql
...output omitted...
Is this ok [y/N]: y
...output omitted...
Complete!
```

#### 6.2. 禁用 postgresql/module 流。

```bash
[root@servera ~]# yum disable postgresql
...output omitted...
Is this ok [y/N]: y
...output omitted...
Complete!
```

#### 6.3. 验证 postgresql/module 流已移除并禁用。

```bash
[root@servera ~]# yum module list postgresql
Hat Enterprise Linux 8.0 AppStream (dvd)
Name Stream Summary
postgresql 10 [d][x] client, server [d] PostgreSQL server and client ...
postgresql 9.6 [x] client, server [d] PostgreSQL server and client ...
```
提示: [d]默认, [e]启用, [x]禁用, [i]已安装

### 7. 退出 servera。

```bash
[root@servera ~]# exit
logout
[student@servera ~]$ exit
logout
Connection to server closed.
[student@workstation ~]$
```

# 完成

在工作站（workstation）上，运行 lab software-module finish 脚本以完成本次练习。该脚本将移除练习期间在 servera 上安装的所有模块。

```bash
[student@workstation ~]# lab software-module finish
```

引导性练习结束。

