
- 2. 输入正向区域的 NS 记录和 A 记录。
- 3. 创建反向域名解析的区域文件。
- 4. 在 named.conf 文件中指定根域名和环回域名的全局配置选项和区域语句。
- 5. 添加正向区域和反向区域的区域语句。
- 6. 启动 named 服务。
- 7. 在 srvA 上的 /etc/resolv.conf 文件中添加 DNS 名称服务器数据。
- 8. 检查 DNS 服务器是否解析主机名和 IP 地址。

## 第 12 课 实验 2：配置 FTP 服务

**数据文件：**
software-1, software-2, software-3, sourcecode-1.pl, sourcecode-2.pl, sourcecode-3.pl

**开始之前：**
要完成此实验活动，你需要在 srvB 上执行以下任务：
1. 创建用户 laura、linda 和 miller。
2. 创建一个名为 /mnt/software_files 的目录，并将 /085039Data/Configuring_Network 目录中的 software-1、software-2 和 software-3 文件复制到 /mnt/software_files 目录。
3. 创建一个名为 /sourcecode 的目录，并将 /085039Data/Configuring_Network 目录中的 sourcecode-1.pl、sourcecode-2.pl 和 sourcecode-3.pl 文件复制到 /sourcecode 目录。

**场景：**
你是 OGC Systems 的一名网络管理员。你希望让不同地点的团队能够互相传输文件。你需要确保只有规定数量的用户可以访问该服务。

> 你可以在学生数据文件的 Configuring_Network/Solution 文件夹中的 Lesson 12 Lab 2 solution.html 文件中找到此活动的建议解决方案。

1. 在 srvB 上，在 `/var/ftp` 目录中创建一个名为 `files_uploaded` 的目录并授予其完整权限。
2. 在 `/etc/vsftpd/user_list` 文件中，添加用户 laura 和 linda。
3. 在 `/etc/vsftpd/vsftpd.conf` 文件中，将指令 `userlist_enable` 的值设置为 `YES`，将 `userlist_deny` 设置为 `NO`，以允许 `user_list` 文件中列出的用户访问 FTP 服务器。
   启动 FTP 服务并设置该服务在系统启动时自动运行。
4. 在 srvA 上，访问 FTP 服务器并使用 `put` 命令上传特定文件。
5. 在 /etc/vsftpd/ftpusers 文件末尾添加用户 miller，以拒绝 miller 访问 FTP 服务器。

## 第 12 课 实验 3：配置网络共享服务

> 你可以在学生数据文件的 Configuring_Network/Solution 文件夹中的 `Lesson 12 Lab 3 solution.html` 文件中找到此活动的建议解决方案。

**场景：**
你是 OGC Systems 的一名网络管理员。你希望让不同地点的团队能够频繁共享文件和文件夹。你希望从一个集中式远程服务器启用跨网络的文件共享。但这可能会导致机密文件被共享，因此你需要确保所有客户端请求都经过过滤。

1. 在 srvB 上，导出 `/sourcecode` 目录。
2. 激活 `nfs` 服务。使用 `useradd` 命令将 csmith 和 wwalters 添加为 Linux 用户，并分配 `myp@$$w0rd` 作为密码。
3. 在 srvB 上，在 /etc/samba/smb.conf 文件末尾，定义名为 source 的共享部分并设置以下参数：
   path = /sourcecode
   public = no
   browseable = yes
   valid users = csmith, wwalters
4. 将 csmith 和 wwalters 添加为 samba 用户。
5. 启动 smb 服务并设置该服务在系统启动时自动运行。
6. 重启 srvA 进入 Windows 系统，并验证用户能否从 Windows 工作站访问 /sourcecode 目录。

## 第 13 课 实验 1：配置 Web 服务

**数据文件：**
english.html, English, german.html

**设置：**
要完成此实验活动，你需要在 srvB 上执行以下任务：
1. 将 English 目录和 english.html 文件从 /085039Data/Web_Services 复制到 /var/www/html 目录。
2. 创建新目录 /var/www/german，并将 german.html 文件从 /085039Data/Web_Services 目录复制到新目录。
3. 在正向区域文件中为德国网站添加 CNAME 条目。
4. 将 nameserver 条目添加为 192.168.0.3。
5. 修改 web 浏览器设置以关闭代理。

**场景：**
你的组织希望让所有利益相关者了解所有即将到来的发展动态。
为了向包括客户、投资者和员工在内的利益相关者通报最新发展情况，管理层决定托管一个交互式网站 www.urlglobalcompany.com。
在与管理层讨论需求后，网页设计团队计划实施以下功能：
1. 配置 PHP 页面支持，以便客户可以在线购买产品。
2. 仅允许经过身份验证的 webusers 访问网站。
3. 将创建一个德国版网站以支持公司在德国的市场营销活动。德语版将称为 german.urlglobalcompany.com。
4. 将访问的网页内容缓存在本地，以提高组织内部的 web 访问速度。
5. 根据互联网政策中规定的规定，在周末限制互联网访问。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_946_0.png)

> 你可以在学生数据文件的 Web_Services\Solution 文件夹中的 Lesson 13 Lab 1 solution.html 文件中找到此活动的建议解决方案。

1. 在 srvB 上安装 httpd。
2. 在系统中启用 PHP 支持。
3. 在正向区域中为 web 服务器指定别名。
4. 配置 web 服务器以允许 web 托管。
   在 /etc/httpd/conf/httpd.conf 文件中，将 `ServerName` 指令设置为 `www.ourglobalcompany.com:80`。
   将 `DirectoryIndex` 指令设置为 `english.html`。
5. 启动 httpd 服务以应用配置更改。
6. 在 httpd.conf 文件中为 web 服务器指定别名。
7. 为英语和德国网站添加 `VirtualHost` 指令。
   在 httpd.conf 文件末尾，使用 `NameVirtualHost` 指令指定 web 服务器的 IP 地址 (192.168.0.3)。
   1. 定义具有 `ServerName` 指令设置为 192.168.0.3、`DocumentRoot` 指令设置为 /var/www/html 和 `DirectoryIndex` 指令设置为 index.html 的 `VirtualHost` 指令，用于该网站。
   2. 定义具有 `ServerName` 指令设置为 192.168.0.3、`DocumentRoot` 指令设置为 /var/www/german 和 `DirectoryIndex` 指令设置为 german.html 的 `VirtualHost` 指令，用于德国网站。
8. 保存并关闭文件。
9. 创建可以访问你网站的用户。
10. 配置 Apache 以进行用户身份验证。在 .htaccess 文件中，定义 `Authname`、`Authuserfile` 和 `AuthType` 参数。此外，使用 `require valid-user` 参数指定所有有效用户都可以访问网站。
11. 检查你是否能够访问网站的英语版本和德国版本。
12. 在 srvA 上，使用链接 http://www.ourglobalcompany.com 和 http://german.ourglobalcompany.com 访问这些站点。
13. 在 /etc/squid/squid.conf 文件中，取消注释 `http_port 3128` 行。
14. 在 INSERT YOUR OWN RULE 部分，定义 myhosts ACL、admin ACL 和 lunch-time ACL。此外，设置 `http_access` 指令以提供 myhosts ACL 和 lunch ACL 的访问权限，并拒绝 admin ACL 的访问权限。
15. 创建 restricted_site ACL 并拒绝该 ACL 以拒绝访问色情网站。
16. 启动 squid 服务。

## 第 14 课 实验 1：Linux 安全

![](img/477ccb2f05b6ba1b2d563ea74f18c197_948_0.png)

你可以在学生数据文件的 Securing_Linux\Solution 文件夹中的 Lesson 14 Lab 1 solution.html 文件中找到此活动的建议解决方案。

**场景：**
员工 Pat 要求你的经理 John 使其密码更安全。John 要求你使 Pat 的密码更安全，并添加额外的防火墙规则以允许 Samba 与系统通信。更新 Pat 的密码并调整防火墙规则。

1. 使用 `passwd` 命令，更新 **Pat** 的密码。
2. 查看现有规则并向 iptables 防火墙添加三条新规则。

```
iptables -A INPUT  -p udp  -s 192.168.0.0/255.255.255.0 -d 192.168.0.1/32 --dport 137 -j ACCEPT
iptables -A INPUT  -p udp  -s 192.168.0.0/255.255.255.0 -d 192.168.0.1/32 --dport 138 -j ACCEPT
iptables -A INPUT  -p tcp  -s 192.168.0.0/255.255.255.0 -d 192.168.0.1/32 --dport 139 -j ACCEPT
```
