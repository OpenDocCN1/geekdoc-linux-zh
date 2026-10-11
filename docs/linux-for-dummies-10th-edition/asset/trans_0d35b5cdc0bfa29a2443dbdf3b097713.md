
![](img/577d3bff979ee86b07f9836e0df274ce_366_0.png)

在过去，人们会使用 telnet 程序远程连接到系统，但我恳求你不要再这样做了。再次强调，不要在安全工具中打开 Telnet 端口，也不要使用 telnet 程序。它会在互联网上以原始的明文形式传输信息，任何人都可以窃听。现在，你可以使用 SSH 协议交互式地登录你的系统，或者使用 scp 程序来回复制文件。

## 运行 Linux SSH 服务器

首先，你需要确保 Linux 系统中已安装 SSH，SSH 服务器正在运行，并且在防火墙中启用了 SSH。（有关第三个问题，请参阅本章前面的“控制和调整防火墙”部分。）

openSUSE 发行版默认安装 SSH 软件，但不会自动启动 SSH 服务器服务。要启动它，你可以使用 systemctl 命令：

```
$ sudo systemctl enable ssh
Created symlink /etc/systemd/system/multi-user.target.wants/sshd.service -> /usr/lib/systemd/system/sshd.service.
$ sudo systemctl start sshd
```

如果你已经在前一节中在防火墙中打开了 SSH 端口，那么你就准备好从远程客户端连接到你的 Linux 系统了！

Ubuntu 工作站发行版默认不安装 SSH 服务器，但你可以使用 apt-get 命令行工具安装 OpenSSH 服务器软件包：

```
$ sudo apt-get install openssh-server
```

安装软件包后，你可以使用 systemctl 命令检查它是否正在运行：

```
$ systemctl list-units --all | grep ssh
ssh.service
loaded active running OpenBSD Secure Shell server
$
```

如果你选择在 Linux 电脑上保持 SSH 服务器运行，你可以使用任何 SSH 客户端软件从远程电脑连接到该 Linux 电脑。你需要使用的软件取决于你从哪种类型的电脑发起连接。

## 安装 Windows SSH 程序

如果你想从 Windows 电脑连接到你的启用 SSH 的 Linux 机器——或者实际上，连接到任何配置为接受 SSH 连接的电脑，而不仅仅是 Linux 机器——你有几个优秀的软件包可供选择。

在 Windows 世界中，一个流行的 SSH 客户端软件包是 PuTTY。这是一个在 MIT 许可证下发布的免费软件包——与大多数 Linux 发行版使用的 GNU GPL 许可证类似——因此你可以随心所欲地使用它，而无需支付一分钱。

PuTTY 的主页（www.chiark.greenend.org.uk/~sgtatham/putty/）提供了一个指向下载区域的 Download 链接。在这里，你可以选择使用哪个版本的 PuTTY（如果你愿意，甚至可以下载程序源代码并自己把玩一番）。在 Windows PC 上让 PuTTY 运行的最简单方法是选择 putty.exe Windows 二进制文件进行下载。这是完整的 PuTTY 程序，包含在一个简单的文件中。

下载 putty.exe 文件后，使用文件管理器程序找到你下载它的位置，然后双击它。主 PuTTY 窗口将出现，如 图 18-3 所示。

![](img/577d3bff979ee86b07f9836e0df274ce_367_0.png)

仅此而已：PuTTY 不需要任何安装设置。现在你准备好使用 SSH 连接到远程电脑了！

## 在 Windows 中设置并建立 SSH 连接

使用 PuTTY 几乎和下载它一样简单。从主 PuTTY 窗口：

- 1. 点击左侧菜单中的 Session 以显示会话选项。参见 图 18-3。
- 2. 在窗口顶部的文本框中输入你想连接的远程电脑的主机名或 IP 地址。
  - 如果你不确定 Linux 系统的地址，打开终端提示符并输入命令 `ip addr`。你应该能看到分配给以太网端口的 IP 地址。
- 3. 确保地址下方的 SSH 单选按钮已选中（这默认应该已经选中）。
- 4. 如果你想保存连接设置，请在 Save Sessions 文本框中输入一个名称，然后点击 Save。
  - 你可以从列表框中选择已保存的会话。PuTTY 会恢复所有配置设置到你保存时的状态。
- 5. 点击 Open 按钮以启动 SSH 会话。

第一次连接到你的 Linux 系统时，PuTTY 会提示你是否要保存服务器的指纹密钥。这可以确保网络上的另一台服务器不会窃取你服务器的 IP 地址并劫持你的连接。只需点击 Yes 接受该密钥即可。

PuTTY 在呈现远程系统的命令行时模拟控制台终端。你可以通过点击主 PuTTY 窗口 Window 部分下的 Appearance 条目来更改终端窗口的外观，如 图 18-4 所示。

![](img/577d3bff979ee86b07f9836e0df274ce_368_0.png)

如果你使用虚拟化软件将你的 Linux 工作站作为虚拟机运行（参见第 20 章），请确保选择创建桥接网络连接，而不是 NAT 网络连接。NAT 网络连接会为你的 Linux 工作站分配一个不在本地网络上的 IP 地址，你将无法从远程客户端连接到它。

然后，终端模拟窗口将出现，要求你输入用于连接的 userid 和密码。输入你的登录信息后，你应该会看到远程电脑的命令行提示符，如 图 18-5 所示。

![](img/577d3bff979ee86b07f9836e0df274ce_369_0.png)

**图 18-4：** PuTTY 窗口外观配置。

![](img/577d3bff979ee86b07f9836e0df274ce_369_1.png)

**图 18-5：** 从 Windows PC 连接到远程 Ubuntu 电脑。

现在你可以像在 Terminal 或 Konsole 程序中那样输入 Linux 命令了！SSH 确保你所有的会话数据在通过网络发送之前都得到安全加密。当你完成后，在命令行输入 **exit**，你的会话就会关闭。

## 使用 SSH 从另一个 Linux 机器连接到你的 Linux 机器

是的，你也可以从另一个 Linux 机器进行连接。这个任务稍微简单一些。打开一个终端窗口（参见第 7 章）并遵循以下步骤：

- 1. **输入** `ssh username@IPaddress` 或 `ssh username@machinefullname` **以打开连接。**
  - 例如，输入 `ssh rich@192.168.1.76` 或 `ssh rich@computer.example.com`。执行此步骤后，会出现以下文本：
    ```
    The authenticity of host '192.168.1.76 (192.168.1.76)' can't be established.
    RSA key fingerprint is ed:68:0f:e3:78:56:c9:b3:d6:6e:25:86:77:52:a7:66.
    Are you sure you want to continue connecting (yes/no)?
    ```
- 2. **输入 yes 并按下 Enter。**
  - 你现在会看到以下行：
    ```
    Warning: Permanently added '192.168.1.76' (RSA) to the list of known hosts.
    rich@192.168.1.76's password:
    ```
- 3. **输入你的登录密码并按下 Enter。现在你进来了！**
  - 通过注销账户（输入 `logout`）来关闭连接。

## 使用 SSH 从运行 OS X 的 Macintosh 连接到你的 Linux 机器

从 Macintosh 进行的过程与在 Linux 下类似。转到 Applications→Utilities→Terminal.app，它会为你打开一个命令行窗口。然后输入

```
ssh IPaddress
```

以访问远程机器上的相同用户账户（同样，你可以使用电脑的全名而不是 IP 地址），或者输入

```
ssh login@IPaddress
```

如果你想访问 `login` 账户，而不是在 Mac 上使用的相同账户。

## 软件漏洞

当有人已经侵入你的系统——无论他们是否被允许在那里——你还有额外的安全问题需要考虑。其中一个涉及机器上安装了什么软件。信不信由你，每个软件都是一个潜在的安全漏洞。如果某人能让程序以正确的方式崩溃，他们就能获得比你本应允许的更大的系统访问权限。这是非常糟糕的事情！

关闭软件漏洞的一种方法是删除所有你不需要的程序。如果需要，你可以随时稍后添加它们。大多数 Linux 发行版（包括 Ubuntu 和 openSUSE）都提供图形工具来添加和删除软件包（参见第 15 章），因此你可以轻松地从电脑上删除任何不必要的软件。

如果事实证明，由于依赖关系，你丢失了其他想要保留的软件，请确保取消删除。

## 使用系统日志查看器关注日志文件

你可能需要考虑的另一个安全问题涉及日志文件。你的网络程序、内核和其他程序都运行日志文件，其中包含系统上正在发生什么记录。你会惊讶于其中包含的信息量之多！它们主要位于 /var/log；有空时去看看。

幸运的是，有工具可以帮助普通人筛选有用信息，以发现 bug 和入侵者的踪迹。Ubuntu 和 openSUSE 都提供图形日志查看器工具，允许你轻松扫描电脑上的主要日志文件。

在 Ubuntu 中，打开应用程序启动器并查找 Logs 应用程序。点击图标启动它。主窗口将出现，如 图 18-6 所示。

Logs 程序将日志数据分为六个类别以便查看：

- **Important：** 所有日志文件中的致命错误
- **All：** 所有日志文件中的所有条目
- **Applications：** 应用程序生成的日志条目
- **System：** 操作系统生成的日志条目
- **Security：** 由安全事件（如登录或注销系统）生成的日志条目
- **Hardware：** 由硬件设备生成的日志条目

