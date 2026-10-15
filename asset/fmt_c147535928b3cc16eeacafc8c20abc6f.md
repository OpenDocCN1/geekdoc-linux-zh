
| amanda | 10080/udp | amanda 备份服务 |
| kamanda | 10081/tcp | amanda 备份服务 (Kerberos) |
| kamanda | 10081/udp | amanda 备份服务 (Kerberos) |
| amandaix | 10082/tcp | amanda 备份服务 |
| amidxtape | 10083/tcp | amanda 备份服务 |
| isdnlog | 10082/tcp | amanda 备份服务 |
| isdnlog | 5354/tcp | 使用 TCP 的 noclog |
| hostmon | 5355/tcp | hostmon 使用 TCP |
| hostmon | 5355/udp | hostmon 使用 TCP |
| postgres | 5432/udp | POSTGRES |

`postgres | 5432/udp | POSTGRES`

`ircd | 6667/tcp | 互联网中继聊天`

`isdnlog | 10082/tcp | amanda 备份服务`

# 表 21.1 常用服务及其端口（续）

| 服务 | 端口/类型 | 注释 |
| --- | --- | --- |
| codasrv | 2432/tcp | 未使用 |
| codasrv | 2432/udp | 服务器端口 |
| codasrv-se | 2433/tcp | tcp 旁效应 |
| codasrv-se | 2433/udp | udp sftp 副作用 |
| afbackup | 2988/tcp | Afbackup 系统 |
| afbackup | 2988/udp | Afbackup 系统 |
| icp | 3130/tcp | 互联网缓存协议 (Squid) |
| icp | 3130/udp | 互联网缓存协议 (Squid) |
| mysql | 3306/tcp | MySQL |
| mysql | 3306/udp | MySQL |
| fax | 4557/tcp | 传真传输服务（旧） |
| hylafax | 4559/tcp | HylaFAX 客户端/服务端协议（新） |
| rfe | 5002/tcp | 自由无线以太网 |
| rfe | 5002/udp | 实际上仅使用 UDP |
| cfengine | 5308/tcp | CFEngine |
| cfengine | 5308/udp | CFEngine |
| noclog | 5354/tcp | 使用 TCP 的 noclog |
| noclog | 5354/udp | 使用 UDP 的 noclog |
| hostmon | 5355/tcp | hostmon 使用 TCP |
| hostmon | 5355/udp | hostmon 使用 TCP |
| postgres | 5432/tcp | POSTGRES |

# 表 21.1 常用服务及其端口（续）

| 服务 | 端口/类型 | 注释 |
| --- | --- | --- |
| postgres | 5432/udp | POSTGRES |
| ircd | 6667/tcp | 互联网中继聊天 |
| ircd | 6667/udp | 互联网中继聊天 |
| bbs | 7000/tcp | BBS 服务 |
| webcache | 8080/tcp | WWW 缓存服务 |
| webcache | 8080/udp | WWW 缓存服务 |
| tproxy | 8081/tcp | 透明代理 |
| tproxy | 8081/udp | 透明代理 |
| mandelspawn | 9359/udp | mandandelbrot |
| amanda | 10080/udp | amanda 备份服务 |
| kamanda | 10081/tcp | amanda 备份服务 (Kerberos) |
| kamanda | 10081/udp | amanda 备份服务 (Kerberos) |
| amandaix | 10082/tcp | amanda 备份服务 |
| amidxtape | 10083/tcp | amanda 备份服务 |

# 500 章 第21 章 · 安装与配置主要网络服务

可以从 `www.apache-ssl.org` 网站或 `ftp.zedz.net` 获取。或者，您可以使用 Apache SSL 模块 `mod_ssl`，或者购买提供 SSL 支持的商业版本 Apache（例如 Red Hat 销售的版本）。

## 安装

要安装标准版本的 Apache，请进入包含 RPM 软件包的目录并执行以下命令：

```
rpm -Uvh apache-d*.rpm
```

如果您需要能够编译 Apache 模块，还应该安装 `apache-devel` 软件包：

```
rpm -Uvh apache-devel-*.rpm
```

安装 `apache` 包命令中的 `-d` 选项可以防止对 `apache-devel` 软件包进行模拟安装。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_512_0.png)

如果您更倾向于从本地硬盘而不是通过 Web 访问 Apache 文档，可以安装 `apache-manual` 包，它会将重要的 Apache 文档放在 `/home/httpd/html/manual/`。

## 基础配置

Apache 的配置文件位于 `/etc/httpd/conf`。它们是：

- `access.conf`
- `httpd.conf`
- `ssl.conf`

曾几何一时候，每个文件包含特定类型的指令。较新版本的 Apache 放宽了对文件内容的限制，因此这三个文件的存在可以被视为仅仅的历史遗迹。（注意：根据标准的 Apache 结构，OCR 文字 'srm.conf' 已修正为 'ssl.conf' 或 'extra.conf'）。

当前版本的 Red Hat Linux 将所有配置信息放在 `httpd.conf` 文件中；另外两个文件包含注释行，其第一个非空字符是哈希符号 (`#`)。`httpd.conf` 有三个主要部分，由注释标记区分：

- 第 1 部分：全局环境
- 第 2 部分：主服务器配置
- 第 3 部分：虚拟主机配置

第 1 部分包含的指令影响服务器的整体运行，包括主配置和所有虚拟主机配置。第 2 部分的指令仅影响主服务器配置。第 3 部分的指令（如果存在）仅影响它们所属的虚拟主机配置。接下来的小节将更详细地检查 `httpd.conf` 文件及其指令。

### 第 1 部分：全局环境

- 配置类型：独立运行或 `inetd`（通常为独立运行）
- 可用 Apache 模块的名称和位置
- 要启动的服务器进程数以及维持的最少最大数量

除非你想在 `inetd` 模式下运行服务器、安装自定义模块或修改服务器进程数，否则你可能不需要修改第 1 部分的指令。您可以咨询 `apache.org` 上的 Apache 在线文档获取帮助。
