
## sysidcfg 文件中的关键字适用以下规则：

- 关键字可以按任意顺序排列。
- 关键字不区分大小写。
- 关键字值可以可选地用单引号 (`'`) 括起来。
- 只有关键字的第一个实例有效；如果您多次指定同一关键字，将使用首先指定的关键字。

### 以下是位于名为 `/jumpstart` 的配置目录中的 `sysidcfg` 文件示例：

```
system_locale=en_US
timezone=EST
timeserver=localhost
terminal=vt100
name_service=NONE
security_policy=none
root_password=XbcjeAg18jLeI
network_interface=primary {protocol_ipv6=no netmask=255.255.255.0}
```

## 在名称服务环境中设置 JumpStart

正如前一节所述，您可以使用 `sysidcfg` 文件在安装的初始阶段回答系统识别问题，无论是否使用名称服务。当 `sysidcfg` 文件与 NIS 命名服务一起使用时，识别参数（如区域设置和时区）可以从名称服务中提供。在运行 NIS 名称服务的网络上安装 JumpStart 客户端所需的 `sysidcfg` 文件通常要短得多，并且不需要为每个客户端单独的 `sysidcfg` 文件。

您将使用 `/etc/locale`、`/etc/timezone`、`/etc/hosts/`、`/etc/ethers` 和 `/etc/netmasks` 文件作为创建 NIS 数据库以支持 JumpStart 客户端安装的来源。有关 NIS 的更多信息以及如何创建 NIS 映射，请参阅第 18 章“名称服务”。

## 设置客户端

现在您需要设置通过网络安装的客户端。设置 `/jumpstart` 目录和适当文件后，使用 install 服务器上的 `add_install_client` 命令设置远程工作站以从 install 服务器安装 Solaris。`add_install_client` 命令的语法如下：

```
add_install_client -e <ethernet_addr> -i <ip_addr> -s <install_svr:/dist> -c <config_svr:/config_dir> \
-p <sysidcfg_svr/sysid_config_dir> <client_name> <client_arch>
```

`add_install_client` 选项在表 21.17 中描述。

### 表 21.17

#### ADD_INSTALL_CLIENT 选项

| 选项 | 描述 |
|---|---|
| `-e <ethernet_addr>` | 指定安装客户端的以太网地址，如果客户端未在名称服务中定义，则为必需。 |
| `-i <ip_addr>` | 指定安装客户端的 IP 地址，如果客户端未在名称服务中定义，则为必需。 |
| `-d` | 将客户端指定为 DHCP 客户端。 |
| `-s <install_svr:/dist>` | 指定安装服务器的名称 (`install_svr`) 和 Solaris 8 操作环境发行版的路径 (`/dist`)。如果客户端被添加到启动服务器，则此选项为必需。 |
| `-p <sysidcfg_svr/sysid_config_dir>` | 指定配置服务器 (`sysidcfg_svr`) 和 `sysidcfg` 文件的路径 (`sysid_config_dir`)。此选项在 Solaris 8 OS 及更高版本发行版上可用。 |
| `<client_name>` | 安装客户端的主机名。 |
| `-c <config_svr:/config_dir>` | 指定配置服务器 (`config_svr`) 和配置目录的路径 (`/config_dir`)。 |
| `<client_arch>` | 指定使用 `<servername>` 作为安装服务器的系统的平台组。 |

有关 `add_install_client` 命令的更多选项，请参阅 Solaris 在线手册页。

在以下步骤中，我将创建一个 JumpStart 客户端，该客户端将从配置为启动和安装服务器的系统启动。此外，整个 Solaris 8 媒体已复制到本地磁盘。

## 逐步操作

### 21.5 创建 JumpStart 客户端

执行以下步骤设置 JumpStart 客户端：

1. 在安装服务器上，切换到包含已安装的 Solaris 8 操作环境映像的目录，如下所示：

```
cd /export/jumpstart/Solaris_8/Tools
```

2. 使用本地目录中找到的 `add_install_client` 脚本创建 JumpStart 客户端，如下所示：

```
./add_install_client -s ultra5:/export/jumpstart/install \
-c ultra5://jumpstart -p ultra5://jumpstart -e 8:0:20:21:49:25 \
-i 192.168.1.106 client1 sun4u
```

系统响应如下：

```
Adding Ethernet number for client1 to /etc/ethers
Adding "share -F nfs -o ro,anon=0 /export/jumpstart/install" to /etc/dfs/dfstab
making /tftpboot
enabling tftp in /etc/inetd.conf
updating /etc/bootparams
copying inetboot to /tftpboot
```

`add_install_client` 脚本自动在以下文件和目录中创建了条目：

`/etc/ethers`

```
8:0:20:21:49:25  client1
```

`/etc/dfs/dfstab`

```
share -F nfs -o ro,anon=0 /export/jumpstart
```

`/etc/bootparams`

```
client1 root=ultra5:/export/jumpstart/Solaris_8/Tools/Boot install=ultra5:/export/jumpstart boottype= \
:in sysid_config=ultra5://jumpstart install_config=ultra5://jumpstart rootopts::rsize=32768
```

`/tftpboot` directory

```
lrwxrwxrwx 1 root other 26 Jun 19 16:11 C0A8016A -> inetboot.SUN4U.Solaris_8-1
lrwxrwxrwx 1 root other 26 Jun 19 16:11 C0A8016A.SUN4U -> inetboot.SUN4U.Solaris_8-1
-rw-r--r-- 1 root other 158592 Jun 19 16:11 inetboot.SUN4U.Solaris_8-1
-rw-r--r-- 1 root other 317 Jun 19 16:11 rm.192.168.1.106
lrwxrwxrwx 1 root other 1 Jun 19 16:11 tftpboot -> .
```

注意

在以下步骤中，示例中做了以下关联：

Install Server name - `server`

Distribution directory - `/export/jumpstart/install`

Configuration Server name - `server`

Configuration directory - `/export/jumpstart/config`

Boot server name - `server`

Install client - `client1`

Client architecture - `sun4m`

3. 使用 `rm_install_client` 命令按如下方式从引导服务器中删除 JumpStart 客户端的条目和配置信息：

```
./rm_install_client client1
```

系统响应如下：

```
removing client1 from bootparams
removing /etc/bootparams, since it is empty
removing /tftpboot/inetboot.SUN4U.Solaris_8-1
removing /tftpboot
disabling tftp in /etc/inetd.conf
```

## 一个 JumpStart 安装示例

以下示例展示了如何为一个虚构站点设置自定义 JumpStart 安装。网络由一台 Enterprise 3000 服务器和五台 Sparc10 工作站组成。

## 设置安装服务器
