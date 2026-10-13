
# 第 2 章：建立简单网络

img/1fa05dc2b61f40be78509e4d8bfc1fe6_80_0.png

img/1fa05dc2b61f40be78509e4d8bfc1fe6_82_0.png

图 2-11：网络邻域

## Samba 加密配置

Samba 加密可以如下所示配置：

1. 以 `root` 身份登录。
2. 编辑 `/etc/smb.conf` 文件。如果你不熟悉编辑 Linux 文本文件，请参阅附录 A“介绍 vi”。`Vi` 是一种几乎在每台 Linux 和 UNIX 计算机上都能找到文本编辑器。
3. 找到以下两行
   - `encrypt passwords = yes`
   - `smb passwd file = /etc/smbpasswd`
4. 行首的分号 (`;`) 意味着 Samba 将它们视为注释。删除分号后，这些参数将生效。它们看起来应该像下面这样

```
encrypt passwords = yes
smb passwd file = /etc/smbpasswd
```

5. 通过输入以下命令创建 `/etc/smbpasswd` 文件：

```
cat /etc/passwd | mksmbpasswd.sh > /etc/smbpasswd
```

6. 运行 `smbpasswd` 命令为 `root` 创建密码。系统会提示你输入密码。请输入你在第 1 章安装 Red Hat Linux 时使用的相同密码。为了让 Windows 能够访问 Linux 服务器上的 `root` 用户，这两个密码必须匹配。

> 注意，我们正在为 `root` 用户创建密码，因为那是 Red Hat Linux 安装过程中自动创建的唯一用户。第 6 章描述了如何创建 Linux 用户账户。在此之前，将使用 `root` 用户进行这些演示。

![](img/1fa05dc2b61f40be78509e4d8bfc1fe6_80_0.png)

## 测试 Samba

如果你运行了局域网（LAN）并已经连接了你的 Windows 95 和 Linux-Samba 机器，你可以直接进入“网络邻域”并开始浏览。如果这种方法不起作用，输入以下命令来查看 Samba 导出的资源：

```
smbstatus
```

如果你已经加入了服务器，将显示公共共享。否则，你只会看到带有版本号的页头。然而，这个工具非常有用，因为它显示了客户端正在访问哪些服务（打印机和文件）。

Red Hat 提供了一个随 RPM 软件包提供的 Samba 配置文件。它位于 `/etc/smb.conf`。`smbd` 进程在启动时会读取此文件。此默认配置允许你挂载 Linux 用户的家目录，该用户名称需与“配置 Windows 95 用于网络操作”节中所描述的 Windows 95 计算机名称相匹配。这项功能非常重要，因为如果你的 Windows 95 TCP/IP 计算机名称与用户名匹配，你将能够自动浏览并使用 Samba 服务，而无需修改 `smb.conf`。

如果你想自定义 `smb.conf`，请查看附录“介绍 vi”，然后按照以下指令操作：

1. 输入以下命令将 `smb.conf` 保存为 `rc/smb.conf.bak`：

```
cp /etc/smb.conf /etc/smb.conf.bak
```

2. 输入以下命令查看手册页（称为 man page）：

```
/bin/man smb.conf
```

请密切注意示例。

3. 使用 `vi` 打开 `smb.conf`：

```
/bin/vi /etc/smb.conf
```

我把实验留给你自己，因为我将在稍后的第 6 章更详细地介绍 `smb.conf`。

4. Samba 必须重新读取 `smb.conf`。输入以下命令运行 Samba 启动和停止脚本：

```
/etc/rc.d/init.d/smb stop
/etc/rc.d/init.d/smb start
```

## 成功了！

等一下。你现在处于冲刺阶段！看看你能否从 Windows 浏览你的 Linux 服务器。

Red Hat Samba 配置指定了用户安全。要访问 Samba 资源，Linux 用户名必须与 Samba 共享名匹配。我还没有配置任何你可以匹配的普通 Linux 用户。但是，你已经配置了 `root` 用户。因此，你需要注销 Windows 95 系统，然后以 Root 用户身份重新登录。当你以 Root 身份登录 Windows 95 机器后，你在 Linux 机器上也将显示为 Root：

1. 点击桌面左下角的“开始”按钮退出你的 Windows 机器。选择“关闭所有程序”并以另一个用户登录，选择“是”。系统将关闭所有打开的程序并提示你输入名称和密码。
2. 登录你的 Windows 机器。第一个对话框要求你作为用户登录。它默认是上次登录的用户名。按 Shift+Tab 跳到用户名框并输入名称 `root`。按 Tab 键到密码，输入你在 Samba 配置中为 `root` 使用的相同密码。
3. 假设你从未登录过 `root`，Windows 将提示你两次输入刚刚输入的密码。在两个框中都重新输入密码。系统将创建以后可以使用的 `root` 用户。
4. 对话框看起来很诡异但并非如此。系统认为它必须找到服务器，但在大多数情况下这是没有必要的，对于本例也是如此。当你的电脑重启后，使用以下步骤查看你的新 Linux-Samba 服务器：
5. 双击“网络邻域”图标（通常在屏幕右上角）打开图 2-11 所示的“网络邻域”窗口

![](img/1fa05dc2b61f40be78509e4d8bfc1fe6_82_0.png)

图 2-11：网络邻域

6. 从 Windows 浏览你的 Linux 服务器。Red Hat Samba 配置指定了用户安全。要访问 Samba 资源，Linux 用户名必须与 Samba 共享名匹配。我还没有配置任何你可以匹配的普通 Linux 用户。但是，你已经配置了 `root` 用户。因此，你需要注销 Windows 95 系统，然后以 Root 用户身份重新登录。当你以 Root 身份登录 Windows 95 机器后，你在 Linux 机器上也将显示为 Root。
