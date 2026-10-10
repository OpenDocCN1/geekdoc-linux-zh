

# 第 5 章：访问和运行应用程序

**提示：** 在大多数情况下，主机名是 TCP/IP 名称。对于本地网络中的计算机，该名称可能位于你的 /etc/hosts 文件中，或者通过域名系统 (DNS) 服务确定。你也可以使用完整域名，例如 hatbox.handsonhistory.com。X 也支持其他类型的传输，尽管除 TCP/IP 以外的传输现在使用得并不多。

在运行远程 X 应用程序时，你大部分时间都会使用这种形式的显示名称。然而，在某些情况下，信息可能不同。如果你的计算机有多个 X 显示（键盘、鼠标和显示器），除了 :0 之外，你可能还有其他数字（如 :1、:2 等）。也可能出现一个键盘和鼠标控制多个显示器的情况，在这种情况下，你可以像这样向地址添加屏幕编号：

```
whatever:0.1
```

此地址标识第一个显示（:0）上的第二个屏幕（.1）。第一个屏幕标识为 .0（这是默认值，因为大多数显示只有一个屏幕）。但是，除非你有多个物理屏幕，否则可以忽略屏幕标识符。

有两种方法将显示名称标识给远程 X 应用程序：

- **DISPLAY shell 变量** — 可以将 DISPLAY shell 变量设置为标识你显示系统的名称和编号。完成此操作后，从该 shell 运行的任何 X 应用程序的输出都将显示在指定的显示上。例如，要将 DISPLAY 变量设置为 whatever 上的第一个显示，请输入以下命令之一：

```
export DISPLAY=whatever:0
```

或

```
setenv DISPLAY whatever:0
```

第一个示例展示了如何在 bash 或 ksh shell 上设置 DISPLAY 变量。第二个示例适用于 csh shell。

- **-display 选项** — 标识远程显示的另一种方法是在运行 X 应用程序时，在命令行中添加 -display 选项。这会覆盖 DISPLAY 变量。例如，要在远程系统上打开 xterm 窗口，使其显示在 whatever 的第一个显示上，请输入以下内容：

```
xterm -display whatever:0
```

你可能需要先使用 yum 安装 xterm 包。有了这些信息，你应该能够在你可以从本地计算机访问的任何计算机上运行 X 应用程序。以下各节描述了如何利用此信息启动远程 X 应用程序。

## 启动远程 X 应用程序

假设你想在局域网中一台名为 remote1 的计算机上运行应用程序（在你相同的域中）。你的本地计算机是 local1，远程计算机是 remote1。以下步骤展示了如何从 remote1 在你的 local1 的 X 显示上运行 X 应用程序。

**注意：** 此操作假设未实施特殊的安全程序。这是默认情况，旨在让本地网络上的受信任计算机（通常是单用户工作站）共享应用程序。此方法本质上是不安全的，要求你信任你允许访问的所有计算机上的用户。如果你需要更安全的机制，请参阅本章后面的“使用 SSH 运行远程 X 应用程序”部分。

你可能需要启用你的 X 服务器以支持网络连接。要查看是否需要启用网络连接，请运行以下命令：

```
$ ps aux | grep Xorg
root      1941  0.0  2.1  54276 44972 tty1   Ss+  11:14   0:04
/usr/bin/Xorg :0 -nr -verbose -auth /var/run/gdm/auth-for-gdm-D98Kms/database vt1 -nolisten tcp
ericfj    6034  0.0  0.0   4212   724 pts/0  R+   12:21   0:00 grep Xorg
```

如果在 Xorg 命令中看到 -nolisten tcp，你需要启用网络连接。为此，如果你使用的是 GNOME 显示管理器（Fedora 的默认设置），请编辑 /etc/gdm/gdm.schemas 文件。在此 XML 文件中查找以下块：

```
<schema>
    <key>security/DisallowTCP</key>
    <signature>bx</signature>
    <default>true</default>
</schema>
```

将此设置更改为以下内容：

```
<schema>
    <key>security/DisallowTCP</key>
    <signature>bx</signature>
    <default>false</default>
</schema>
```

此后，重新启动你的系统。登录并确保 -nolisten tcp 参数不再存在：

```
$ ps aux | grep Xorg
root      2141  0.0  2.1  54276 44972 tty1   Ss+  12:04   0:04
/usr/bin/Xorg :0 -nr -verbose -auth /var/run/gdm/auth-for-gdm-e2VZ7d/database vt1
```

完成后，按照以下步骤允许远程应用程序连接到你的桌面：

1. 在本地计算机上打开一个终端窗口。
2. 通过在终端窗口中输入以下内容，允许远程计算机（例如，`remote1`）访问本地 X 显示：

```
$ xhost +remote1
remote1 being added to access control list
```

3. 使用任何远程登录命令登录到远程计算机。例如，如果你想以用户 `joe` 的身份登录到远程计算机，可以使用以下命令：

```
$ ssh joe@remote1
joe@remote1's password:
```

你会被提示输入密码。
4. 输入远程用户登录的密码。（你现在已在终端窗口中以远程用户身份登录。）
5. 将远程计算机上的 `DISPLAY` 变量设置为你的本地计算机。例如，如果你的计算机在本地域中名为 pine，命令可以是：

```
$ export DISPLAY=pine:0
```

（如果你正在远程系统上使用 csh shell，可能需要输入 `setenv DISPLAY pine:0`。）
6. 此时，你从远程系统的此 shell 运行的任何 X 应用程序都将显示在本地显示上。例如，要运行远程终端窗口使其本地显示，请输入：

```
$ xterm
```

终端窗口显示在本地显示上。

你需要记住关于显示在你的屏幕上的远程应用程序的几件事：

- 如果你仅使用登录来运行远程应用程序，你可以将导出 `DISPLAY` 变量的行添加到远程系统上的用户配置文件中（如果你使用 `bash` shell，则为 `.bashrc`）。之后，你运行的任何应用程序都将指向你的本地显示。
- 尽管应用程序看起来像是在本地运行，但所有工作都是在远程系统上完成的。例如，如果你远程运行了一个文字处理程序，它将使用远程 CPU，并且当你保存文件时，它会被保存到远程文件系统。

**注意：** 不要忘记当远程 shell 或文件编辑器在你的桌面上打开时。有时人们会忘记某个窗口是远程的，并错误地编辑远程系统上的一些重要配置文件（例如 `/etc/fstab` 文件）。这种错误可能会损坏远程系统。

## 使用基于用户的安全

正如你刚才看到的，xhost 允许来自远程主机的所有用户连接到你的显示。这可能很危险，因为该系统上的任何用户都可以进行屏幕截图、记录按键，甚至控制你的桌面。因此，使用 xhost 可能不是一个好主意。你可以使用命令 `xhost -remote1` 禁用 xhost：

```
$ xhost -remote1
```

在启用 X 服务器监听 TCP 后，你可以使用 xauth 命令，该命令使用共享密钥来允许只有拥有你的共享密钥的特定用户连接到你的显示。要在你的 X 服务器上查看共享密钥，请运行以下命令：

```
$ xauth list
pine/unix:0   MIT-MAGIC-COOKIE-1   2e6461766964a75666665792e636fd
```

此共享密钥允许你在本地运行的 X 应用程序通过你的显示的 unix 套接字进行通信。你需要添加一行额外的内容以允许通过 TCP 连接。你可以通过复制和粘贴相关部分来完成，但省略 /unix，并运行 xauth add，使用你希望授予访问权限的系统名称，在此情况下是名为 pine 的系统：

```
$ xauth add pine:0   MIT-MAGIC-COOKIE-1
2e6461766964a75666665792e636fd
```

现在，你需要启用你的 remote1 客户端以能够与在 pine 上运行的 X 服务器通信。通过添加 pine 到 DISPLAY 变量，然后运行 xauth 在 remote1 上添加共享密钥来实现：

```
$ export DISPLAY=pine:0
$ xauth add pine:0   MIT-MAGIC-COOKIE-1   2e6461766964a75666665792e636fd
```

现在，你以该用户身份从 remote1 运行的任何命令都将显示在 pine:0 上。由于你没有使用 xhost，除非其他用户能够访问该用户的 ~/.Xauthority 文件，否则 remote1 上的其他用户将无法连接到 pine 的显示。

**注意：** 虽然 xauth 提供身份验证，但 xhost 和 xauth 都不提供加密，任何嗅探网络的人都可能捕获你的 X 活动和按键。

## 使用 SSH 运行远程 X 应用程序

ssh 命令不仅提供了登录到远程系统的安全机制，还提供了安全运行远程 X 应用程序的方法。在启用 X11 转发的情况下，你在 ssh 会话期间从远程位置运行的任何 X 应用程序都将显示在你的本地桌面上。

在使用 ssh 登录到远程计算机后，你可以使用该安全通道将 X 应用程序转发回你的本地显示。以下是一个示例：

