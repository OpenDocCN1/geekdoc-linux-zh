
设置 `Agroforestry Electronic Medical Normal tools` 的权限。

(7) 修改各个板块自己目录的权限。

```bash
[root@dianzi /]# chown Eladmin:Electronic
[root@dianzi /]# chown Ecadmin:Ecadmin Economic
[root@dianzi /]# chown Noadmin:Noadmin Normal
[root@dianzi /]# chown Agadmin:Agroforestry
[root@dianzi /]# chown Meadmin:Meadmin Medical
[root@dianzi /]# chown admin:admin share/
```

(8) 修改目录下的权限。

```bash
[root@dianzi /]# cd share
[root@dianzi share]# chown Eladmin:Eladmin Electronic
```

## 学习情境二 部署 Linux 网络服务

```bash
[root@dianzi share]# chown Meadmin:Meadmin Medical
[root@dianzi share]# chown Agadmin:Agadmin Agroforestry
[root@dianzi share]# chown Noadmin:Noadmin Normal
[root@dianzi share]# chown Ecadmin:Ecadmin Economic
[root@dianzi share]# chown admin:admin tools
[root@dianzi share]# ll
drwrx-xr-x. 2 Agadmin Agadmin 6 1月 29 03:33 Agroforestry
drwrx-xr-x. 2 Ecadmin Ecadmin 6 1月 29 03:33 Economic
drwrx-xr-x. 2 Eladmin Eladmin 6 1月 29 03:33 Electronic
drwrx-xr-x. 2 Meadmin Meadmin 6 1月 29 03:33 Medical
drwrx-xr-x. 2 Noadmin Noadmin 6 1月 29 03:33 Normal
drwrx-xr-x. 2 admin admin 6 1月 29 03:33 tools
```

(9) 在文件 `/etc/samba/smb.conf` 中设置用户映射。

```bash
[root@dianzi samba]# vim smbusers
Eladmin=user1
Ecadmin=user2
Noadmin=user3
Agadmin=user4
Meadmin=user5
```

(10) 修改配置文件 `/etc/samba/smb.conf`。（以下是修改部分内容，其余内容保持默认）

```ini
[root@dianzi samba]# vim /etc/samba/smb.conf
[global]
workgroup = MYGROUP
security = user
username map = /etc/samba/smbusers
[Electronic]
comment = Electronic directory.
path = /Electronic
public = no
admin users = Eladmin
valid users = @Eladmin
writable mask = 750
directory mask = 750
[Economic]
comment = Economic directory.
path = /Economic
public = no
admin users = Ecadmin
valid users = @Ecadmin
writable = yes
create mask = 750
directory mask = 750
[Normal]
comment = Normal directory.
path = /Normal
public = no
admin users = Noadmin
valid users = @Noadmin
writable = yes
create mask = 750
directory mask = 750
[Agroforestry]
comment = Agroforestry directory.
path = /Agroforestry
public = no
admin users = Agadmin
valid users = @Agadmin
writable = yes
create mask = 750
directory mask = 750
[Medical]
comment = Medical directory.
path = /Medical
public = no
admin users = Meadmin
valid users = @Meadmin
writable = yes
create mask = 750
directory mask = 750
[share]
comment = share directory.
path = /share
public = no
valid users = admin, @Eladmin, @Ecadmin, @Noadmin, @Agadmin, @Meadmin
writable = yes
create mask = 755
```

(11) 重启 `Samba` 服务。

```bash
[root@dianzi]# systemctl restart smb
```

(12) 客户端下载服务器上的文件。

```bash
[root@dianzi]# smbclient -L //172.168.1.29 -U Eladmin
```

在 `Windows` 下访问 `Samba` 服务。在浏览器中输入 `172.168.1.29`（如图10所示），需要用户和密码。

## 4. 项目总结

- (1) 注意目录权限的设置。
- (2) 能使用 `smstatus` 查看 `Samba` 情况。
- (3) 能使用 `testparam` 检查 `smb.conf` 配置的正确性。

通过学习，了解 `Samba` 服务的工作原理、软件安装及常用配置，能够针对不同的用户设置权限。为了服务器的安全，根据实际情况设置用户映射，并解决这些问题，能够熟练通过 `Linux` 和 `Windows` 访问共享。

## 练习题

### 一、选择题

1. 以下关于 `Samba` 的描述中，不正确的是( )。
    - A. `Samba` 采用 `SMB` 协议。
    - B. `Samba` 支持 `WINS` 名字解析。
    - C. `Samba Linux` 客户端提供文件和打印共享。
    - D. `Samba` 不支持 `Windows` 的域管理。

2. 在 `Linux` 上安装 `Samba` 服务器，可以使（）。
    - A. `Windows` 访问 `Linux` 上共享的资源
    - B. `Linux` 访问 `Windows` 主机上的资源
    - C. `Windows` 主机访问 `Windows` 服务器的资源
    - D. 以上都对

3. 在 `Samba` 配置文件 `/etc/samba/smb.conf` 中，参数 `security` 在默认情况下使用 ）等级。
    - A. `user`
    - B. `share`
    - C. `server`
    - D. `domain`

4. `Samba` 服务器的主配置文件是（）。
    - A. `httpd.conf`
    - B. `inetd.conf`
    - C. `rc.samba`
    - D. `smb.conf`

### 二、填空题

1. 查询 `Linux` 系统是否安装了 `Samba` 服务器的命令是（ ）
2. 添加 `Samba` 用户的命令是（ ）
3. 启动 `Samba` 服务器的命令是（ ）
4. `Samba` 配置文件修改后，使用（ ）测试该文件的。
5. `Samba` 服务器共有 4 种安全等级。使用（ ）等级不需要账号和密码就可以 `Samba` 服务。

### 三、面试题

1. `Linux` 作为服务器，IP 地址是 `192.168.4.10`，服务器上有一个目录 `/home/lupa`，其中有一个文件。现在实现 `lupa` 用户无密码的共享。分别通过 `Windows` 和 `Linux` 客户端访问 `lupa` 目录。

2. 配置 `Samba`，共享 `/home/sharefile` 目录，要求只有 `192.168.0.0/24`、`192.168.1.0/24` 和 `127.0.0.1` 可以访问，共享的 `[share]`，用户不能看到，只有 `student` 才能写的权限。同时，要把 `student` 组的每个学生的家目录也共享，同时设置 `Netbios name = GUEST245`。

3. 小型企业内部局域网环境，要求：
    - (1) 所有的员工能够在公司流动办公，但不在电脑工作，都要把自己的数据保存在 `Samba` 文件服务器上。
    - (2) 市场部和技术部各有自己的目录，同一个部门的人共同有一个共享目录，其他部门的人只能访问服务器中的自己的家目录。
    - (3) 所有的用户都不允许服务器上的 `Shell`。

## 学习情境二 部署 Linux 网络服务

## 项目 1.1 部署FTP 服务

### 引入
