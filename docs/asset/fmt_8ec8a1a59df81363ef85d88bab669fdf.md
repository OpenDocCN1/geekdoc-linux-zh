
## 测试频率最高的状态
测试频率最高的状态是：
* `ESTABLISHED`：数据包是已看到双向数据包的连接的一部分
* `NEW`：数据包是新连接的开始
* `RELATED`：数据包正在启动新的次要连接。这是像 FTP 数据传输或 ICMP 错误这样的协议的常见功能。
* `INVALID`：数据包无法识别。可能是由于系统资源不足，或不匹配现有数据流的 ICMP 错误。

## 262 ▶ 附录 A

6. 这是前一个示例的扩展：

```
iptables -A FORWARD -s 0/0 -i eth0 -d 172.16.1.58 -o eth1 -p TCP \
-sport 1024:65535 -m multiport --dports 80,443 -j ACCEPT

iptables -A FORWARD -d 0/0 -o eth0 -s 172.16.1.58 -i eth1 -p TCP \
-m state --state ESTABLISHED -j ACCEPT
```

此处配置 `iptables` 以允许防火墙在数据包从任何 IP 地址进入接口 `eth0`，且目的地为可通过接口 `eth1` 访问的 IP 地址 `172.16.1.58` 时，接受需要路由的 `TCP` 数据包。源端口范围在 `1024` 到 `65535` 之间，目的端口为 `80` 端口（`www/http`）和 `443`（`https`）。来自 `172.16.1.58` 的回包也允许被接受。不必说明源和目的端口，你可以简单地使用 `-m state` 和 `--state ESTABLISHED` 选项来允许与已建立连接相关的数据包。

## 允许访问防火墙的 DNS

```
iptables -A OUTPUT -p udp -o eth0 --dport 53 -sport 1024:65535 \
-j ACCEPT

iptables -A INPUT -p udp -i eth0 --sport 53 --dport 1024:65535 \
-j ACCEPT
```

## 允许访问防火墙的 WWW 和 SSH

```
iptables -A OUTPUT -o eth0 -m state --state ESTABLISHED,RELATED \
-j ACCEPT

iptables -A INPUT -p tcp -i eth0 --dport 22 --sport 1024:65535 \
-m state --state NEW -j ACCEPT

iptables -A INPUT -p tcp -i eth0 --dport 80 --sport 1024:65535 \
-m state --state NEW -j ACCEPT
```

## 允许防火墙访问互联网

```
iptables -A OUTPUT -j ACCEPT -m state \
--state NEW,ESTABLISHED,RELATED -o eth0 -p tcp \
-m multiport --dports 80,443 --sport 1024:65535

iptables -A INPUT -j ACCEPT -m state --state ESTABLISHED,RELATED \
-i eth0 -p tcp
```

## 允许家庭网络访问防火墙

在此示例中，`eth1` 直接连接到使用 `172.16.1.0` 网络 IP 地址的家庭网络。假设此网络与防火墙之间的所有流量都被简单视为受信任并予以允许。

针对连接到互联网的接口的进一步规则将需要只允许特定端口、连接类型以及可能的远程服务器访问你的防火墙和家庭网络。

```
iptables -A INPUT -j ACCEPT -p all -s 172.16.1.0/24 -i eth1
iptables -A OUTPUT -j ACCEPT -p all -d 172.16.1.0/24 -o eth1
```

# 附录：SELinux 安全策略和上下文

安全增强型 `Linux`（`SELinux`）增强功能由美国联邦国家安全局（`NSA`）开发，自版本 `3` 的 `Fedora Core` 和版本 `4` 的 `Red Hat Enterprise Linux` 开始包含在内。细粒度访问控制架构在 `Linux` 内核中得到支持。既支持“类型”强制，也支持基于角色的访问控制（`RBAC`）。系统进程和文件（包括套接字描述符、`IPC`、设备）各自被分配一组已知为安全上下文的安全属性。

安全目标：

* 保护系统免受用户侵害
* 保护用户之间互不侵犯
* 保护文件免受脚本/程序侵害

以下 `RPM` 软件包构成了 `SELinux`：

* `selinux-policy-strict`
* `selinux-policy-strict-sources`：配置文件
* `selinux-policy-targeted`
* `selinux-policy-targeted-sources`：配置文件
* `libselinux`：提供一组接口的库，供具有安全意识的应用程序获取和设置进程和文件的安全上下文。
* `selinux-doc`

配置文件：`/etc/selinux/config`

```
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#       enforcing - SELinux security policy is enforced.
#       permissive - SELinux prints warnings instead of enforcing.
#       disabled - SELinux is fully disabled.
SELINUX=enforcing
# SELINUXTYPE= type of policy in use. Possible values are:
#       targeted - Only targeted network daemons are protected.
#       strict - Full SELinux protection.
SELINUXTYPE=targeted
```

可以通过设置 `SELINUX=disabled` 来关闭 `SELinux` 功能。（需要重新启动才能读取新配置。）

直接设置强制执行：

* 强制执行：
    * 使用命令：`setenforce 1`（在内核运行时更改 `SELinux` 强制执行状态。）
    * 或者
    * `echo 1 > /selinux/enforce`
    * 在 `/etc/grub.conf` 的 "kernel" 命令行中指定：`enforcing=1`（在启动时设置强制执行。）

* 禁用：
    * 使用命令：`setenforce 0`
    * 或者
    * `echo 0 > /selinux/enforce`
    * 或者
    * 在 `/etc/grub.conf` 的 "kernel" 命令行中指定：`selinux=0`

使用命令查看当前设置：`getenforce`

## 安全上下文

* 查看文件/目录上下文：`ls -Z /var/www`

* 设置文件/目录上下文：`chcon -R -h -t httpd_sys_content_t /home/user1/public_html`
    * 选项：
        * `-R`：递归。当前目录及所有子目录中的文件和目录。
        * `-h`：影响符号链接。
        * `-t`：指定安全上下文的类型。

* 查看运行中进程的安全上下文：`ps -eZ`

* 查看用户的安全上下文：`id`

```
uid=500(user1) gid=500(user1) groups=500(user1)
context=user_u:system_r:unconfined_t
```

新文件的安全上下文默认为父目录的安全上下文。

# 附录：YUM 仓库服务器

## 关于 YUM

`YUM` 或 `Yellowdog Updater Modified`（修改版 `Yellowdog` 更新器）是一个交互式自动更新程序，可用于使用 `rpm` 维护系统。`Yum` 是 `rpm` 系统的自动更新器和软件包安装/卸载器。它自动计算依赖关系，并确定安装软件包时应执行哪些操作。`Yum` 使得维护机器组变得更加容易，无需手动使用 `rpm` 更新每一台机器。

## 关于仓库

仓库是一组 `rpm` 列表的集合。它包含有关 `rpm` 的各种信息，例如其依赖关系等。

## 既然可以使用 rpm 命令安装 RPM，为什么要使用 Yum？

好吧，如果你想要安装 `RPM`，必须确保其依赖项也已安装。但在 `YUM` 的情况下并非如此，你可以直接安装软件包及其依赖项。`YUM` 会处理你所有的安装事务。此外，`rpm` 安装方式不提供更新功能，但 `yum` 提供该功能。

## YUM 的关键特性

* 多个仓库
* 简单的配置文件
* 正确的依赖关系计算
* 快速操作
