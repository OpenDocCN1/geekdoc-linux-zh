
如果计算机中的调制解调器未被 Linux 轻松识别，首先要做的是联系调制解调器制造商寻求帮助。一些调制解调器制造商提供在线支持，包括特定 Linux 发行版的连接文档和驱动程序。

有许多类型的调制解调器。可以使用 `lspci` 命令找到 PCI 类型的调制解调器。`lspci` 命令列出连接到计算机系统的 PCI 设备。例如，图 7–21 表明系统安装了 `Conexant HSF 56k Data/Fax/Voice Modem`。

### 图 7-21

`lspci` 命令。

```
[root@localhost dev]# lspci
00:00.0 Host bridge: Intel Corp. 440LX/EX - 82443LX/EX Host bridge (rev 03)
00:01.0 PCI bridge: Intel Corp. 440LX/EX - 82443LX/EX AGP bridge (rev 03)
00:02.0 VGA compatible controller: ATI Technologies Inc 3D Rage II+ 21S7B [Mach 64 GT2] (rev 9a)
00:03.0 Ethernet controller: Intel Corp. 82557/9 [Ethernet Pro 100] (rev 02)
00:07.0 ISA bridge: Intel Corp. 82371AB/EB/MB PIIX4 ISA (rev 01)
00:07.1 IDE interface: Intel Corp. 82371AB/EB/MB PIIX4 IDE (rev 01)
00:07.2 USB Controller: Intel Corp. 82371AB/EB/MB PIIX4 USB (rev 01)
00:07.3 Bridge: Intel Corp. 82371AB/EB/MB PIIX4 ACPI (rev 01)
00:0b.0 Communication controller: Conexant HSF 56k Data/Fax/Voice Modem (rev 01)
[root@localhost dev]#
```

对于每个串行端口，`/dev` 目录中都有一个特殊文件。`/dev/ttyS0` 是串行端口 COM1 的特殊文件。这些特殊设备充当数据的通道。例如，通过键入命令 `cat myfile > /dev/ttyS0`，你可以将文件中的信息直接发送到 com1。S 代表 serial（串行），`tyS0` 用于 COM1，`tyS1` 用于 COM2，以此类推。

### 注意

`tty` 是电传打字机（teletype）的缩写。电传打字机是一种终端类型，其中修改后的打字机旨在从通信线路接受输入，该线路远程操作它。

也可以使用其他设备名称。例如，对于图 7-21 中找到的 HSF 调制解调器，设备名称是 `/dev/ttySHSF0`。要检查设备设置，可以使用命令 `setserial -a <devicename>`。例如，要查看 `/dev/ttySHSF0` 的信息（图 7-22），使用命令 `setserial -a /dev/ttySHSF0`。

### 图 7-22

`setserial` 命令。

![](img/37f079cee226b270f2e09b37a2e4a05d_195_0.png)

通过以下步骤设置 PPP：

1. 添加一个具有唯一 gid 编号的 ppp 组。例如，要添加组 ppp，使用命令 `groupadd ppp`。

2. 将连接到远程服务器的用户添加到 ppp 组。例如，要将 jsmith 添加到 ppp 组，使用命令 `usermod -G ppp jsmith`。

3. 确保 `/usr/sbin/pppd` 命令的所有者是 root（图 7-23）。例如，`chown root /usr/sbin/pppd`。

### 图 7-23

配置 PPP。

![](img/37f079cee226b270f2e09b37a2e4a05d_195_1.png)

4. 确保 `/usr/sbin/pppd` 命令属于 `ppp` 组。例如，执行 `chgrp ppp /usr/sbin/pppd`。

5. 设置 `/usr/sbin/pppd` 命令以 root 权限运行，即使该命令由其他用户执行。例如，执行 `chmod u+s /usr/sbin/pppd`。

6. 将脚本 `ppp-on` 和 `ppp-off` 从目录 `/usr/share/doc/ppp-version/scripts`（其中 `version` 是 `ppp` 程序的版本号）复制到 `/usr/sbin` 目录。例如：

```
cp /usr/share/doc/ppp-2.4.1/scripts/ppp-on /usr/sbin
cp /usr/share/doc/ppp-2.4.1/scripts/ppp-off /usr/sbin
cp /usr/share/doc/ppp-2.4.1/scripts/ppp-on-dialer /usr/sbin
```

7. 将 `ppp-on`、`ppp-off` 和 `ppp-on-dialer` 的所有者更改为 root。例如，执行 `chown root /usr/sbin/ppp-on`。

8. 将 `ppp-on`、`ppp-off` 和 `ppp-on-dialer` 的所属组更改为 `ppp`。例如，执行 `chgrp ppp /usr/sbin/ppp-on`。

9. 将 `ppp-on`、`ppp-off` 和 `ppp-on-dialer` 的权限更改为所有者和所属组可读可执行。例如，执行 `chmod 550 /usr/sbin/ppp-on`。

10. 通过修改以下条目来编辑 `ppp-on` 脚本：

```
TELEPHONE = telephone number to dial
ACCOUNT = your ppp-account
PASSWORD = your password
```

11. 将 `exec /usr/sbin/pppd` 行设置为正确的拨出设备。例如，`ttt0`。

12. 编辑 `/etc/ppp/options` 文件，使其包含以下值：

```
lock
modem
-detach
crtscts
defaultroute
asyncmap 0
mtu 552
mru 552
```

如果你连接的服务器要求 PAP/CHAP，则需要在 `/etc/ppp/pap-secrets` 或 `/etc/ppp/chap-secrets` 文件中配置相关信息。出于安全考虑，这些文件的所有者必须是 root 用户，所属组必须是 root 组，并且文件权限必须设置为 740。PAP 和 CHAP 实际上是对主机计算机进行身份验证，而不是对用户进行验证。然而，ISP（互联网服务提供商）通常会提供用户名和密码供你连接其系统，这些凭据将用于识别你的机器。

`/etc/ppp/pap-secrets` 文件包含以下字段：

```
# Secrets for authentication using PAP
# client      server secret       IP addresses
```

如果你在该 ISP 处的用户名是 `jsmith`，密码是 `Up#39!dn`，则该文件将包含以下内容：

```
# Secrets for authentication using PAP
# client      server secret       IP addresses
jsmith        *         Up#39!dn
```

`server`（服务器）是远程服务器的名称。ISP 通常拥有一个接收单个拨入号码信息的服务器集群。星号（`*`）表示可以连接到任何远程服务器。

IP 地址字段通常为空。出于安全原因，ISP 通常不允许远程系统设置 IP 号。

对于 `/etc/ppp/chap-secrets` 文件，PAP 和 CHAP 配置的唯一区别是增加了远程服务器的身份验证信息。将增加第二行，包含远程服务器的用户名和密码（secret）。

工作完成了。客户端现在应该已经配置完毕。你可以使用 `minicom` 程序来测试调制解调器。使用 `man minicom` 命令查看选项和命令列表。

## ISDN 服务

综合业务数字网 (ISDN) 旨在解决小型办公室或拨入用户在电话拨入服务中面临的带宽问题。ISDN 的开发目的是利用现有的电话布线系统，但提供全数字网络。它的工作方式与标准的电话拨号连接类似，即在需要时拨打电话。

与传统的拨号系统相比，ISDN 具有若干优势。ISDN 可用于传输比传统计算机数据更多的内容。它还可以提供数字视频和电话网络服务（语音）的接入。
