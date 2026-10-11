

在 **示例 7.3.1** 中，机器名称设置为 **GANDALF**，工作组设置为本地工作组的名称（**MIDEARTH**），以便该机器能与用户熟悉的系统一起出现。唯一需要的密码后端是“**guest**”后端，以允许使用默认的非特权账户名。由于该网络上有一个 WINS 服务器，我们当然会加以利用。

美国空军上校曾有一句名言：“更好是足够好的敌人！”避免复杂性以及避免技术上的完美解决方案，通常都有充分的理由。不幸的是，许多网络管理员仍需学会做好恰到好处的事情以免惹麻烦的艺术。

### 7.3.2 中央打印服务

如果你在系统中拥有所有合适的工具，配置一个简单的打印服务器非常容易。

- **假设条件**
  1. 打印服务器必须不需要管理。
  2. 我们打印服务器上的打印排队和处理系统将是 CUPS。（请参见第 21 章“CUPS 打印支持”以获取更多信息）。
  3. 打印服务器仅服务网络打印机。网络管理员将正确配置 CUPS 环境以支持这些打印机。
  4. 所有工作站将仅使用 PostScript 驱动程序。首选的打印机驱动程序是随 Windows 操作系统附带的 Apple Color LaserWriter 驱动程序。

在这个示例中，我们的打印服务器将把所有传入的打印作业暂存到 */var/spool/samba*，直到作业准备好由 Samba 提交给 CUPS 打印处理器。由于所有传入的连接都将是匿名用户，需要做到两点以启用匿名打印。

- **启用匿名打印**
  - UNIX/Linux 系统必须有一个 **guest** 账户。此账户的默认名称通常是 **nobody**。要找到适用于你的 Samba 版本使用的正确名称，请执行以下操作：

```bash
$ testparm -s -v | grep "guest account"
```

确保此账户存在于你的系统密码数据库中（*/etc/passwd*）。一个好主意是给此账户设置密码，或者锁定它以防 UNIX 使用。假设 guest 账户名为 **pcguest**，可以通过执行以下命令锁定：

```bash
root# passwd -l pcguest
```

确切命令可能会因你的 UNIX/Linux 发行版而异。

  - Samba 将暂存文件的目录必须对 guest 账户有写入访问权限。以下命令将确保该目录可用：

```bash
root# mkdir /var/spool/samba
root# chown nobody.nobody /var/spool/samba
root# chmod a+rw /var/spool/samba
```

**smb.conf** 文件的内容如示例 7.3.2 所示。

**示例 7.3.2** *用于匿名打印的 smb.conf*

```ini
# Global parameters
[global]
workgroup = MIDEARTH
netbios name = GANDALF
security = SHARE
passdb backend = guest
printing = cups
printcap name = cups
[printers]
comment = All Printers
path = /var/spool/samba
printer admin = root
guest ok = Yes
printable = Yes
use client driver = Yes
browseable = No
```

> **注意**
> 在启用了 CUPS 的系统中，有一种机制可以直接将原始数据传递给打印机，而无需通过 CUPS 打印过滤器进行中间处理。若希望使用此运行模式，需要配置一个原始打印设备。此外，还需要在 /etc/mime.conv 和 /etc/mime.types 文件中启用原始 mime 处理器。参见第 21 章“CUPS 打印支持”，第 21.3.4 节。

示例 7.3.2 使用 CUPS 通过 CUPS 库 API 进行直接打印。这意味着所有打印机都将暴露给 Windows 用户，而无需配置 printcap 文件。如果只需要暴露部分打印机，或定义特殊类型的打印机（例如 PDF 过滤器），则可以将 **printcap name = cups** 替换为条目 **printcap name = /etc/samba/mymprintcap**。在这种情况下，指定文件应包含要暴露给 Windows 网络用户的打印机名称列表。

## 7.4 常见错误

所犯的最大错误常常是使网络配置过于复杂。使用能满足当下需求的最简单方案是值得的。

## MS WINDOWS 网络配置指南

### 8.1 功能和优势

偶尔，网络管理员会报告难以使 Microsoft Windows 客户端与 Samba 服务器正确互操作。似乎有些人就是无法接受这样一个事实：配置 MS Windows 网络客户端的正确方式，正是使用 MS Windows NT4 或 200x 服务器时所做的那样。然而，反复提供详细的 Windows 客户端配置说明的需求依然存在。

本章的目的是形象地说明这种配置中最常见和关键方面的 MS Windows 客户端配置。经验丰富的网络管理员可能对本章的细节不感兴趣。

### 8.2 技术细节

本章讨论当今常用平台的 TCP/IP 协议配置以及网络成员资格。这些平台包括：

- Microsoft Windows XP Professional
- Windows 2000 Professional
- Windows Millennium 版 (Me)

#### 8.2.1 TCP/IP 配置

房屋建造者必须确保所有施工都建立在坚实的基础上。对于基于 TCP/IP 的网络系统建造者来说也是如此。基础网络配置问题将困扰所有网络用户，直到它们得到解决。

MS Windows 工作站和服务器可以配置为使用固定 IP 地址，或通过 DHCP 配置。以下示例演示了 DHCP 的使用，并仅简要提及可以进行固定 IP 配置设置的那些情况。

可以使用快捷方式或缩写按键组合到达特定的配置屏幕。本章决定所有示例都基于使用 **Start** 按钮。

##### 8.2.1.1 MS Windows XP Professional

有两条路径可到达 Windows XP TCP/IP 配置面板。请选择你偏好的访问方式：

- 点击 **Start -> Control Panel -> Network Connections**。
- *或者*，点击 **Start ->**，右键点击 **My Network Places**，然后选择 **Properties**。

以下步骤指导完成 Windows XP Professional TCP/IP 配置过程：

1. 在某些安装中，该接口被称为 **Local Area Connection**，在其他安装中则被称为 **Network Bridge**。在我们的系统中，它被称为 **Network Bridge**。右键点击 **Bridge -> Properties**。参见图 8.1。

![](img/86d74c6cc862465e3a42e6dc3c90935a_153_0.png)

2. 网络桥接配置（Network Bridge Configuration）或本地连接（Local Area Connection）面板用于设置 TCP/IP 协议设置。在 **此连接使用下列项目：** 框中，点击 **Internet Protocol (TCP/IP)**，然后点击 **Properties**。默认设置是启用 DHCP 操作（即，“自动获得 IP 地址”）。参见图 8.2。

许多网络管理员希望使用 DHCP 来配置所有客户端 TCP/IP 协议栈设置。（有关如何为 Windows 客户端支持配置 ISC DHCP 服务器的信息，请参见第 46.2.2 节。如果需要提供固定 IP 地址，请点击“使用下列 IP 地址”，并在提供的框中输入 IP 地址、子网掩码和默认网关地址。

图 8.2 Internet Protocol (TCP/IP) 属性。

![](img/86d74c6cc862465e3a42e6dc3c90935a_154_0.png)

3. 点击“高级”按钮以继续 TCP/IP 配置。这将打开一个面板，可以在其中为该接口创建额外的 IP 地址。这些额外地址的技术名称是 $IP\ aliases$，此外，该面板还允许设置更多的默认网关（路由器）。在大多数使用 DHCP 的情况下，不需要创建额外的设置。参见图 8.3 以查看此面板的外观。

   如果 DNS 和 WINS 设置未通过 DHCP 自动提供，则可能需要为它们设置固定值。

4. 点击 DNS 选项卡以添加 DNS 服务器设置。示例系统使用手动配置的 DNS 设置。完成更改后，点击“确定”以提交设置。参见图 8.4。

5. 点击 WINS 选项卡以添加手动 WINS 服务器条目。此步骤演示了一个使用手动配置 WINS 设置的示例系统。完成更改后，点击“确定”以提交设置。参见图 8.5。

##### 8.2.1.2 MS Windows 2000

有两条路径可到达 Windows 2000 Professional TCP/IP 配置面板。请选择你偏好的访问方式：

