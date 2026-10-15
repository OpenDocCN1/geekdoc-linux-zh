
`tar -xvf filename.tar`

`tar` 文件解包后，将创建一个包含所有源文件的新文件夹。通常，下一步是使用命令编译程序：

```
make
```

下一步是安装程序。要执行这一点，输入命令：

```
make install
```

安装完成后，你应该验证是否创建了 `/etc/openldap` 和 `/usr/share/openldap/migration` 文件夹。

## rpm 文件的安装
这种安装相对简单。下载文件后，运行命令：

```
rpm -Uvh filename.rpm
```

你将获得安装在服务器计算机系统上的 OpenLDAP。类似，你可能需要在客户端计算机系统上安装 OpenLDAP 客户端。

# 118 Chao

要配置 LDAP 服务器，假设你已经安装了 Fedora 或 Red Hat Linux 作为服务器操作系统。下一个任务是配置 `slapd.conf` 文件，输入与你的在线/学习系统创建的域名相同的后缀 `suffix` 和根节点 `rootdn`。继续后续，下一个任务是使用命令为网络管理员创建一个加密密码：

```
/usr/sbin/slappasswd
```

将加密密码复制到 `slapd.conf` 文件中，并将其放置在 `rootpow` 条目之后。你还需要配置控制对 LDAP 服务器访问的权限。例如，你可以允许网络管理员读取和写入目录内容，但仅允许其他人读取目录中的内容。保存配置并使用命令启动 LDAP 服务器：

```
service ldap start
```

在 LDAP 服务器安装并配置后，你可以填充目录。将数据插入目录的一种方法是将用户从现有系统移动到目录。你可以在 `/usr/share/openldap/migration` 文件夹中找到一些工具来完成这项工作。在 `migrate_common` 文件中，设置 `$DEFAULT_BASE` 以匹配在线/学习系统的域名。用户信息信息存储在 `base.pl`、`passwd.pl` 和 `group.pl` 中。你可以使用迁移工具 `./migrate` 将数据从 `.pl` 文件到 `.ldif`，可以通过以下命令由 LDAP 服务器：

```
./migrate.pl > filename.ldif
```

将 `.ldif` 文件的内容添加到目录，使用命令：

```
ldapadd -D "cn=Manager,dc=tu,dc=edu" -x -W -f filename.ldif
```
