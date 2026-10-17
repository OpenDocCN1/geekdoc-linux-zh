
```bash
[root@localhost conf.d]# curl 172.16.43.249
this is default web
```

然后，在 Windows 和 Linux 分别打开浏览器，在地址栏输入`http://172.16.43.253:8888`，页面自动跳转到`ceshi1.html`；在地址栏输入`http://172.16.43.253:6666`，页面自动跳转到`ceshi2.html`；在地址栏输入`http://172.16.43.249:80`，页面自动跳转到`index.html`，如图 13-6 和图 13-7 所示。

![](img/ec0e037f26e46c767b8ae4c4c4a36e86_275_0.png)

### 例 3 在 IP 地址为 172.16.43.253 的 Apache 服务器上基于域名的网站

网络规划如表 13-2 所示。

**表 13-2 基于域名的虚拟机的网络规划**

| 虚拟机 | IP 地址 | 端口 | 目录 | 主页 |
| :--- | :--- | :--- | :--- | :--- |
| `www.zhiyuan.com` | 172.16.43.253 | 8888 | `/home` | `ceshi.html` |
| `xy.zhiyuan.com` | 172.16.43.253 | 6666 | `/var/www` | `ceshi.html` |
| `index_ip` | 172.16.43.249 | 80 | `/var/www/html` | `index.html` |

具体配置过程：

- ① 配置 DNS 服务器，添加解析、反向区域。

```bash
[root@dns ~]# vi /etc/named.conf
listen 53 { any };
```

- ② 修改配置文件`named.rfc12.zones`，定义区域，内容如下：

```bash
root@dns ~]# vim /etc/named.rfc12.zones
在末尾添加：
zone "zhiyuan.com" {
  type master;
  file "zhiyuan.conf";
  allow-update none;
};

zone "253.43.16.172.in-addr.arpa" {
  type master;
  file "zhiyuan.fan";
  allow-update none;
};
```

- ③ 编辑正向解析文件`zhiyuan.conf`，如图 13-9 所示。

```bash
root@localhost:~# vim /var/named/zhiyuan.conf
```

| 文件(F) | 编辑(E) | 查看(V) | 搜索(S) | 终端(T) | 帮助(H) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TTL 1D | IN SOA zhiyuan.com. root.zhiyuan.com. | : serial | | | |
| | | 0 : refresh | | | |
| | | 1D : retry | | | |
| | | IW : expire | | | |
| | | 3H : minimum | | | |
| | | IN NS zhiyuan.com. | | | |
| | | IN MX 5 mail.zhiyuan.com. | | | |
| | | IN A 172.16.43.253 | | | |
| | | IN A 172.16.43.253 | | | |
| | | IN A 172.16.43.254 | | | |
| | | IN A 172.16.43.252 | | | |
| | | IN CNAME zhiyuan.com. | | | |

编辑反向解析文件`zhiyuan.fan`，如图 13-10 所示。

```bash
root@localhost:~# vim /var/named/zhiyuan.fan
```

| 文件(F) | 编辑(E) | 查看(V) | 搜索(S) | 终端(T) | 帮助(H) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TTL 1D | IN SOA zhiyuan.com. root.zhiyuan.com. | : serial | | | |
| | | 0 : refresh | | | |
| | | 1D : retry | | | |
| | | IW : expire | | | |
| | | 3H : minimum | | | |

## 学习情境二 部署 Linux 网络服务

```bash
<Directory>
<VirtualHost>
[root@localhost.conf#] vim oa.conf
[root@localhost.conf#] cat oa.conf
<VirtualHost 172.16.43.253:80>
DocumentRoot "/var/www/html"
</VirtualHost>
```

- ⑦ 重启`httpd`服务。
- ⑧ 测试。

```bash
[root@localhost.conf#] curl zhiuyuan.com
this is first web
[root@localhost.conf#] curl xy.zhiuyuan.com
this is second web
[root@localhost.conf#] curl oa.zhiuyuan.com
this is default web
```

可以在 Windows 和 Linux 分别打开浏览器，在地址栏分别输入`http://www.zhiuyuan.com`、`http://xy.zhiuyuan.com` 及 `http://oa.zhiuyuan.com`，结果如图 13-11 所示。

![](img/ec0e037f26e46c767b8ae4cc4a36e86_279_0.png)

图 13-11 基于不同域名的虚拟主机

## 13.2.7 访问控制

Apache 对访问控制权限的设置有两种方式：一种是在配置文件`httpd.conf`中直接进行，另一种是使用`<Directory></Directory>`容器设置或在`.htaccess`文件中设置。两种方式都可以用于控制浏览器的访问，但是使用`httpd.conf`配置文件，每次改动都需要重启服务器才能生效，灵活性较差；而使用`.htaccess`文件设置具体的目录访问控制较为灵活。

在 Apache 2.2 版本中，访问控制是基于客户端的主机、IP 地址以及客户端请求中的其他特征，使用`Order`（排序）、`Allow`（允许）、`Deny`（拒绝）指令来实现。在 Apache 2.4 版本中使用`mod_auth_host`这个新的模块来实现访问控制和模块的授权控制。原来在 Apache 2.4 版本下实现网站访问控制的`Order`、`Allow`和`Deny`指令，需要替换为新的访问控制指令。

## 项目 13 部署 Web 服务

### 1. 目录的访问控制

- 例 1 所有请求都被拒绝，命令如下：

```apache
Require all denied
```

- 例 2 所有请求都被允许，命令如下：

```apache
Require all granted
```

- 例 3 `zhiyuan`域内所有请求都被允许，其他拒绝，命令如下：

```apache
Require host zhiyuan.com
```

- 例 4 拒绝 IP 地址为 192.168.1.26 和`test.net`的客户端访问，其他客户端都可以正常访问，命令如下：

```apache
Require not ip 192.168.1.26
Require not host test.net
```

- 例 5 允许 192.168.0.24 网段、IP 为 172.16.43.254 的客户端访问，但其中 192.168.0.100 不能访问，命令如下：

```apache
Require ip 192.168.0 172.16.43.254
Require not ip 192.168.0.100
```

`Options`是 Apache 配置文件中一个常见重要的指令，`Options`指可以在 Apache 服务器核心配置（Server Config）、虚拟主机（Virtual Host）、特定目录配置（Directory）及`.htaccess`文件中使用。

`Options`指令用于控制特定目录启用哪些服务器特性。常见的配置示例如下：

```apache
<Directory>/var/www/html/> #指定目录“允许” Indexes、FollowSymLinks 两种特性
AllowOverride None
Require all granted
</Directory>
```

选项（`Options`）可以出现在配置文件容器内，或`.htaccess`文件中。

```apache
Options [+]|[-Option1] [+]|[-Option2]
```

- 选项前添加加号(`+`) 添加此特性。
- 选项前添加减号(`-`) 表示移除此特性。
