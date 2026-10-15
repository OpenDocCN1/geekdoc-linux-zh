
当浏览器提示你时，输入 root 用户名和密码。出现 SWAT 窗口（见图 27-2）。

图 27-2

从你的浏览器中使用 SWAT 管理你的 Samba 配置。

![](img/a90dc0c1392c27f587fa6c88e9865199_769_0.png)

欢迎使用 SWAT！

请通过上方按钮选择一个配置操作

# Samba 文档

- 守护进程
  - `smbd` - SMB 守护进程
  - `nmbd` - NetBIOS 守护进程
  - `winbind` - winbind 守护进程
- 
  - `samba.conf` - 主配置文件
  - `hosts` - NetBIOS hosts

> TIP 在使用 SWAT 之前，为你的 `samba.conf` 文件创建一个备份。要允许 localhost 以外的计算机访问服务，请修改 `only_from = 127.0.0.1` 行自 `/etc/xinetd.d/swat` 并重启服务。

- 以下章节解释了如何使用 `samba.conf`。

# 第五部分 运行

> 注意：每次使用 GUI 创建更改时，请为 `/etc/samba/smb.conf` 创建备份。

# 在 SWAT 中创建全局设置

一组全局设置影响文件和打印方式。这些设置出现在 `/etc/samba/smb.conf` 的 `[global]` 标题下。查看并编辑全局属性，点击 GLOBALS 按钮。

有七种类型的选项：基础、安全、日志、打印、浏览和 wins。

> 注意每个选项对应 `smb.conf` 中的参数。你可以参考该页面获取更多信息。

## Base Options

以下选项涉及基本信息：

- Workgroup — Samba 组的名称。默认值为 WORKGROUP。
- Realm — 如果你使用 Kerberos 认证，此值指示要使用的 Kerberos realm。即提供服务的的主机名。
- NetBIOS name — 分配给此 Samba 服务器的名称。你可以使用与 DNS 主机名相同的名称，或者留空，将自动使用 DNS 主机名。默认填充了你的 DNS 主机名。
- NetBIOS alias — 允许设置与 TCP/IP 名称不同的计算机引用方式（别名）。
- Server string — 标识服务器的字符串。此名称出现在注释框等地方。默认为 Samba 和版本号。
- Interfaces — 允许设置多个网络接口并让 Samba 浏览不同的子网络。此字段的格式为 IP 地址/子网掩码。或者，识别网络接口（例如电脑网卡的 eth0）。例如，一个 C 类网络地址可能显示为：

```
192.168.24.11/255.255.255.0
```
