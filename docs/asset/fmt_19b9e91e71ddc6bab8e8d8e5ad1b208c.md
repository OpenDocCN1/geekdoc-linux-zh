
# 第 13 章：安全的 Linux 才是快乐的 Linux

![](img/d01c7c9abe7acbcb8b5f8f79e6511f25_280_0.png)

8. 点击“连接”（Connect）建立与你的 Linux 机器的连接。

第一次以此方式连接时会“未找到主机密钥”（Host Key Not Found）对话框。点击“连接”（Connect）并保存主机密钥。你不需要在此 Windows 机器上再次执行此步骤。查看图 13-5 可以看到 Windows 机器上的 Linux 命令行窗口！（我不确定为什么这个默认字体看起来这么像“手写”；你可以通过选择格式（Format）>更改字体（Change Font）来更改所有会话，或者在首选项（Preferences）菜单的连接配置文件（Connection Profile）中选择配置文件并点击外观（Appearance）选项卡。）

![](img/d01c7c9abe7acbcb8b5f8f79e6511f25_280_1.png)

# 第三部分：快速上手 Linux

完成后，在命令行输入 `exit`，连接就会关闭。

## 使用 SSH 从另一个 Linux 盒子连接到你的 Linux Box

是的，你也可以从另一个 Linux 盒子连接。这个任务稍微简单一点。打开终端窗口（见第 14 章）并按照以下步骤操作：

- 1. 输入 `ssh username@ipaddress` 或 `ssh username@machinefull` 来建立连接。

例如，输入 `ssh dee@192.168.1.6` 或 `ssh dee@computer.example`。执行此步骤后，会出现以下文本：

> 无法建立 '192.168.1.6' (192.168.1.6) 的真实性。
RSA 密钥指纹为：
SHA256:68:0fe3:78:56:c9:b3:d6:e2:25:86:77:52:a7:6
确定要继续连接吗 (yes/no)?

- 2. 输入 `yes` 并按回车键。

你现在看到这几行：

> 警告：已将 '192.168.1.6' (RSA) 添加到已知主机列表。
dee@192.168.1.6 的密码：

- 3. 输入你的登录密码并按回车键。现在你进入了！

通过注销账户（输入 `logout`）来关闭连接。

## 使用 SSH 从运行 OS X 的 Macintosh 连接到你的 Linux Box

在 Macintosh 上的操作过程与 Linux 下类似。前往“应用程序：实用工具：`Terminal.app`”，这将为你打开一个命令行窗口。然后输入

```
ssh IPAddress
```

以访问远程机器上的同一个用户账户（再次，你可以使用计算机全名而不是 IP 地址），或者输入

```
ssh login@IPAddress
```
