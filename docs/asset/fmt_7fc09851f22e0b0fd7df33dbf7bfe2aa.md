
第三，当你引用 Windows 2000 域或域控制器时，请使用其旧式的 NetBIOS 名称进行引用。例如，如果你的 Windows 2000 域名为 `acme.com`，那么该域可能有一个名为 `ACME` 的“低级”名称。如果域控制器名为 `bigdog.acme.com`，那么它的低级名称就是 `\BIGDOG`。

# 使用 NT/2000 域验证 Linux 用户：winbind

随着 Samba 2.2 出现了一个非常有用的功能：使用 NT 4.0 或 Active Directory 域账户登录 Linux 机器的能力。你已经在第 6 章中读到，可以将 Linux 机器变成一个 NIS 服务器，在其中你可以存储一组集中的用户和组账户，使你无需为每台 Linux 机器上的每个用户重新构建用户账户。但这意味着你仍然需要维护两套集中的用户账户：NIS 账户和微软域。`winbind` 告诉 Linux，“当有人想要登录时，去某某域中的 Microsoft NT 或 AD 域控制器处验证该用户。”

`winbind` 需要几个部分：

- 当然，需要 Samba 程序（`smbd` 必须运行）。
- `nmbd` 必须在运行。
- 需要一个名为 `winbind` 的守护进程在运行。
- 你必须通过 `netjoin` 命令让 Linux 加入域。
- 你必须使用 PAM（可插拔模块）来实现。

为了让 Samba 工作，我们将一个一个地设置。设置，我们将假设在 Linux 机器上。

# 设置 `smb.conf` 的具体示例

为了简单起见，让我们假设我们仍在旧的 REALM 域示例中工作。这是该域的 `smb.conf` 可能的如下：

```
[global]
wins server = 130.10.20.5
workgroup = REALM
server string = Test Samba Server
netbios name = LINUXBOX
security = domain
password server = *
encrypt passwords = yes
username map = /etc/linixtont
[public]
path = /publicstuff
guest ok = yes
writeable = no
write list = gerry
[private]
path = /privatestuff
guest ok = no
valid users = @managers
write list = @managers
```

`/etc/linixtont` 文件将有一条记录：

```
managers = @managers
```

在第一个共享中，我使用了 `guest ok` 而没有使用 `valid users` 语句，因为我并不在乎谁访问它，但 `writeable = no` 确保了没有人可以修改它——除了 `gerry` 之外。在第二个共享中，禁用访客并显式地仅将 `managers` 组的成员设为 `valid users`，可以将其他人全部排除在外。

# 让 Samba 自动启动

我们之前做过这个，但为了保持示例的自包含性，让我们看看如何让 Linux 在运行级别 3 下自动启动 Samba。你可以通过在 `/etc/rc.d/rc3.d` 目录中创建一个符号链接，指向 `/etc/rc.d/init.d/samba` 中的脚本来实现：

```
ln -s /etc/rc.d/init.d/samba /etc/rc.d/rc3.d/S91smb
```

# 创建 unexpected.td

和之前一样，Samba 需要看到一个名为 `/var/cache/samba/unexpected.td` 的文件：

```
touch /var/cache/samba/unexpected.td
```

# 启动 Samba

下次你重启时，Samba 就会启动，但嘿，这可是 Linux；可能要等好几年才会重启——所以让我们手动启动 Samba：

```
/etc/rc.d/init.d/samba start
```

你应该看到类似下面的响应：

```
Starting SMB services:      [ OK ]
Starting SMB services:      [ OK ]
```

# 检查 BIOS 名称解析

无论是讨论 Windows 客户端还是 Linux 客户端，登录失败最令人头疼的原因之一就是简单的计算机名解析方法。NT、2000、XP 和 .NET 缺乏一个简单的工具来检查此项，但 Samba 在 `nmblookup` 中提供了一个非常有用的工具。`nmblookup` 可以通过广播和查询 WINS 服务器来为你查找 NetBIOS 名称，我们将尝试这两种方法。命令看起来如下：

```
nmblookup netbiosname
```

这会真正尝试通过广播解析 NetBIOS 名称，以及：

```
nmblookup -R -U wins-server-address netbiosname
```

为了让后续很多代码能够正常运行，你 Linux 机器上的 Samba 服务必须能够解析你域的 PDC。假设你的 NT 或 Active Directory 域的 PDC（或者在 Active Directory 的情况下，是 DC 模拟器）的 NetBIOS 名称为 `DC1`，IP 地址为 `10.10.10.70`。假设你的 WINS 服务器的 IP 地址是 `10.10.10.50`。你通过以下命令告诉 Samba 广播尝试寻找 `DC1`：

```
nmblookup dc1
```

## 第 9 章 Linux/Microsoft 操作系统互操作性

如果成功，你会看到类似下面的输出：

```
querying dc1 on 10.10.10.0
10.10.10.70 dc1<0>
```

然后像这样告诉它查询 WINS 服务器：

```
nmblookup -R -U 10.10.10.50 dc1
```

你将得到一个类似下面的响应：

```
querying dc1 on 10.10.10.50
10.10.10.70 dc1<0>
```

# 将 Linux PC 加入域

一旦你确定 Linux 机器可以至少找到一个 DC，你就可以准备加入域了。使用这个命令（你之前看到的同一个命令）：

```
smbpasswd -j <domain name> -r <pdc name> -U <domain admin%password>
```

如果我有一个域管理员 Susan，她的密码是 blueSky，在一个名为 bigfirm 的域中，PDC 名为 DC1，我会输入：

```
smbpasswd -j bigfirm -r dc1 -U Susan%blueSky
```

如果 Susan 确实拥有 bigfirm 域的域管理员权限，并且 bigfirm 的密码是 blueSky，且 bigfirm 的 PDC 名为 DC1，那么你会看到类似下面的输出：

```
Joined domain BIGFIRM.
```

# 编辑 nswitch.conf

你可能还记得我们在讨论 NIS 时提到，Linux 使用一个名为 `nswitch.conf` 的文件来确定搜索密码和组信息的顺序——本地文件、NIS 服务器等。这在这里也适用：我们将告诉这台 Linux 机器，期望同时找到密码和组信息：不仅在本地文件中，还包括从 `winbind` 服务获取。

用文本编辑器打开 `/etc/nswitch.conf`。一旦你跳过开头的注释行（记住第一列的井号 `#` 表示注释），你将看到类似下面的三行内容：

```
passwd: files nisplus
shadow: files nisplus
group: files nisplus
```

## 使用 NT/2000 域验证 Linux 用户：winbind 463

将 `passwd` 和 `group` 的 `nisplus` 改为 `winbind`，使行看起来像如下：

```
passwd      files winbind
shadow      files nisplus
group      files winbind
```

# 让 winbind 自动启动

和 Samba 一样，我们希望 `winbind` 自动启动。由于 `winbind` 需要 Samba 作为一个服务 91 启动，我们将 `winbind` 作为服务 92 启动：

```
ln -s /etc/rc.d/init.d/winbind /etc/rc.d/rc3/S92winbind
```

# 为 winbind 分配一个域帐户
