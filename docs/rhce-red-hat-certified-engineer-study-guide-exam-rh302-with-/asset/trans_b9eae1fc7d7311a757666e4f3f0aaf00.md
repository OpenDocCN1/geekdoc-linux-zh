

# 500 章 第21 章 · 安装与配置主要网络服务

可以从 www.apache-ssl.org 网站或 ftp.zedz.net 获取。或者，您可以使用 Apache SSL 模块 mod_ssl，或者购买提供 SSL 支持的商业版本 Apache（例如 Red Hat 销售的版本）。

## 安装

要安装标准版本的 Apache，请进入包含 RPM 软件包的目录并执行以下命令：

```
rpm -Uvh apache-d*.rpm
```

如果您需要能够编译 Apache 模块，还应该安装 apache-devel 软件包：

```
rpm -Uvh apache-devel-*.rpm
```

安装 apache 包命令中的 `-d` 选项可以防止对 apache-devel 软件包进行模拟安装。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_512_0.png)

如果您更倾向于从本地硬盘而不是通过 Web 访问 Apache 文档，可以安装 apache-manual 包，它会将重要的 Apache 文档放在 /home/httpd/html/manual/。

## 基础配置

Apache 的配置文件位于 /etc/httpd/conf。它们是：

- access.conf
- httpd.conf
- ssl.conf

曾几何一时候，每个文件包含特定类型的指令。较新版本的 Apache 放宽了对文件内容的限制，因此这三个文件的存在可以被视为仅仅的历史遗迹。（注意：根据标准的 Apache 结构，OCR 文字 'srm.conf' 已修正为 'ssl.conf' 或 'extra.conf'）。

当前版本的 Red Hat Linux 将所有配置信息放在 httpd.conf 文件中；另外两个文件包含注释行，其第一个非空字符是哈希符号 (#)。httpd.conf 有三个主要部分，由注释标记区分：

- 第 1 部分：全局环境
- 第 2 部分：主服务器配置
- 第 3 部分：虚拟主机配置

第 1 部分包含的指令影响服务器的整体运行，包括主配置和所有虚拟主机配置。第 2 部分的指令仅影响主服务器配置。第 3 部分的指令（如果存在）仅影响它们所属的虚拟主机配置。接下来的小节将更详细地检查 `httpd.conf` 文件及其指令。

### 第 1 部分：全局环境

- 配置类型：独立运行或 `inetd`（通常为独立运行）
- 可用 Apache 模块的名称和位置
- 要启动的服务器进程数以及维持的最少最大数量

除非你想在 `inetd` 模式下运行服务器、安装自定义模块或修改服务器进程数，否则你可能不需要修改第 1 部分的指令。您可以咨询 apache.org 上的 Apache 在线文档获取帮助。

### 第 2 部分：主配置

`httpd.conf` 的第 2 部分包含仅影响服务器主配置的指令；不影响任何虚拟主机（如果配置）。主要配置项包括：

- 服务器的主机
- 服务器监听的端口号（通常为 80）
- 守护进程运行的用户和组 ID（通常为 `nobody`）
- 日志记录类型：按 IP 地址或主机名（通常按 IP 地址记录效率更高）
- 根目录的位置（通常为 `/home/httpd/html`）
- 用户 HTML 子目录的名称（通常为 `~/public_html` 或 `~/www`）
- CGI 脚本所在的路径
- 格式目录索引时使用的图标位置
- 特殊内容处理配置选项

通常，您应该修改 ServerName 指令（指定与服务器关联的主机名）和 ServerAdmin 指令（指定服务器管理员的电子邮件）。根据需要，您可能需要更改其他指令。

### 第 3 部分：虚拟主机配置

虚拟主机（也称为多宿主）是 Apache 的一项重要功能，允许单个 Web 服务器响应多个 IP 地址或主机名。例如，可以配置一个 Apache 实例响应指向 www.able.com 和 www.baker.com 的查询。虚拟主机允许两个或组织共享一个 Web 服务器。如果您想配置 Apache 支持虚拟主机，必须修改 httpd.conf 文件第 3 部分的指令。您应该指定：

- 虚拟主机的 IP 地址或地址
- 每个虚拟主机管理员的电子邮件
- 每个虚拟主机的主机名
- 与每个虚拟主机相关的日志文件名
- 每个虚拟主机的文档根目录和 CGI 目录

以下是两个主机——www.firsthost.com 和 www.secondhost.com 的典型虚拟主机配置，它们都分配了 IP 地址 192.169.100.1：

```
NameVirtualHost 192.169.100.1
<VirtualHost firsthost.com>
ServerAdmin webmaster@firsthost.com
DocumentRoot /home/httpd/html
</VirtualHost>

<VirtualHost secondhost.com>
ServerAdmin webmaster@secondhost.com
DocumentRoot /home/httpd/html
</VirtualHost>
```

