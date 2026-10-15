
当 X 服务终止时，`ssh-agent` 也会随关闭。密码永远不会存储在文件中，而是由 `ssh-agent` 存储在内存中，直到用户注销为止。

# 练习 10-1 使用 OpenSSH 管理远程连接

在本次练习中，你将执行以下操作：

- 第一部分：使用 SSH 工具
- 第二部分：在服务器之间建立信任连接

## 第一部分：使用 SSH 工具

在练习的这一部分，你需要与伙伴配合，练习使用 SSH 工具套件。

执行以下操作：

- 1. 从 KDE 桌面打开终端窗口，并使用密码 切换到 root 用户（`su -`），密码为 `novel`。

在练习 9-3 期间，你修改了 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件，允许除你的伙伴以外的所有用户通过 Telnet 访问你的服务器。

为了执行此练习，你需要确保 `/etc/hosts.deny` 文件中的 `ALL :ALL ...` 已注释掉。

a. 输入 `vim /etc/hosts.deny` 在 vi 中编辑该文件。

b. 确保文件底部的以下行已被删除或注释（`#`）：

`ALL : ALL: twist (echo "This service is not accessible from %a!")`

c. 输入 `:wq` 保存文件并退出 vi。

### 使用 OpenSSH 提供安全的远程访问

- 2. 从终端窗口以 `geeko` 身份登录你伙伴的电脑：

a. 在命令行输入以下内容：

```
sh -l geeko partner_server_IP_address
```

b. （条件性的）如果收到关于远程主机真实性的警告，继续输入 `yes` 并继续操作。

c. 输入密码 `N0v3II`。你现在已以 `geeko` 身份登录到伙伴的服务器。

d. 输入 `exit` 退出。

3. 输入以下内容（密码为 `novelli`）来检查谁登录了你伙伴的系统：

```
ssh -l root partner_server_IP_address ps aux
```

系统将显示你伙伴服务器上当前运行的所有进程列表。

4. 输入以下内容（密码为 `N0v3II`），将你的 `/etc/hosts` 文件复制到你的 `/tmp` 目录：

```
scp geeko@partner_server_IP_address:/etc/hosts /tmp/
```

5. 输入以下内容（密码为 `N0v3II`），将你的 `/etc/hosts` 文件复制到伙伴服务器上的目录中：

```
scp /etc/hosts geeko@partner_server_IP_address:/tmp/
```

6. 输入以下内容使用 `sftp` 以 `geeko` 身份连接你伙伴的电脑：

```
sftp geeko@partner_server_IP_address
```

7. 输入以下内容将程序 `/bin/date` 复制到 `geeko` 的目录：

```
cp /bin/date /home/geeko/
```

8. 输入 `exit` 退出 `sftp`。

9. 输入以下内容创建 `/etc/hosts` 文件：

`touch /etc/hosts`

10. 让你的伙伴尝试以 `geeko` 身份通过 Telnet 访问服务器：

`partner_server_IP_address`

11. 输入以下内容删除 `/etc/hosts` 文件：

`rm /etc/hosts`

## 第二部分：在服务器之间建立信任连接

在练习的这一部分，你将在服务器之间建立信任连接。

为了防止意外覆盖，你需要对伙伴的服务器进行操作。当 X 服务终止时，`ssh-agent` 也会关闭。密码永远不会存储在文件中，而是由 `ssh-agent` 存储在内存中，直到用户注销为止。

你可以使用 YaST 模块配置 SSH 密钥。执行以下操作：

- 1. 生成一对 RSA 密钥：

a. 在终端窗口输入：

`ssh-keygen -t rsa`

b. 接受默认位置 `/root/.ssh/rsa`。

c. 输入密码 `novel`。

2. 将 RSA 公钥复制到伙伴服务器（密码为 `N0v3II`）：

`scp .ssh/id_rsa.pub geeko@partner_server_IP_address:/root`

3. （注意：根据上下文，后续步骤涉及密钥交换和测试）

## 使用 YaST 启用远程管理

你可以通过 YaST 启用 SUSE Linux 服务器的远程管理。

要实现和使用远程连接，你需要了解以下内容：

### VNC 和 YaST

你可以使用 YaST 远程管理模块配置你的 SUSE Linux 服务器进行远程访问。

当你激活远程管理时，`xinetd` 通过 VNC 导出 X 登录。

远程管理连接的安全性低于 SSH，因为后者会加密所有传输的数据（包括密码）。因此，我们建议仅在需要执行管理任务时使用远程连接。

如需更多关于 VNC 的信息，可以输入 `man vncviewer` 或访问 `www.realvnc.com`。也可以参考 `/etc/xinet.d/vnc` 中的文档，或输入 `netstatant` 查看 Internet 连接列表。

## VNC 和 YaST 远程管理

VNC（虚拟网络计算）是一种客户端/服务器解决方案，允许从任何地方通过轻量级客户端管理 X 服务器。

两台计算机不需要是相同类型。例如，你可以通过 VNC 在 Windows 上查看 Linux 机器。

服务器和客户端适用于多种操作系统，包括 Microsoft Windows、Apple macOS 和 Linux。

你可以使用 YaST 远程管理模块配置你的 SUSE Linux 服务器，以便从任何网络计算机（或互联网）访问。

激活远程管理后，`xinetd` 提供一个通过 VNC 导出 X 登录的连接。

通过 VNC 客户端连接到服务器，例如 `krdc`（连接 `hostname:5901`）、Konqueror 中的 VNC 连接（`vnc://hostname:5901`）或支持 Java 的 Web 浏览器（`http://hostname:5801`）。

`hostname` 参数可以是实际的主机名（例如 `http://suse.linux.com:5801`），也可以是主机 IP 地址（例如 `http://192.168.1.1:5801`）。

## 如何配置服务器进行远程管理

要配置你的 SUSE Linux 服务器进行远程管理，请执行以下操作：

- 1. 从 KDE 桌面通过以下任一方式启动 YaST 远程管理模块：

* 选择 YaST 图标，输入 密码并点击确定；然后选择“网络服务”（Network Services）> “远程管理”（Remote Administration）。
* 或者
* 打开终端窗口并输入 `su -` 以及 root 密码；然后输入 `yast2 remote`。

![](img/667acce1695f6403deb2b60e994760c8_644_0.png)

图 10-3

- 2. 选择“允许远程管理”（Allow Remote Administration）；然后选择“完成”（Finish）。

显示图 10-4 中的消息。

![](img/667acce1695f6403deb2b60e994760c8_644_1.png)

图 10-4

- 你需要重启显示管理器以激活远程管理设置。

3. 选择确定关闭对话框。

4. 关闭已打开的应用程序；然后通过 `Ctrl+Alt+F2` 显示控制台。

5. 使用相应的密码以 root 登录。

## 第 10 管理远程访问

- 6. 输入 `rcxdm` 重启显示管理器。

片刻后，将显示图形登录界面。

7. 以 `root` 或任何其他本地用户登录桌面。

您的 SUSE Linux Enterprise Server 已准备好进行远程访问。

> **注意** 您可以通过遵循相同的步骤但选择不允许远程管理（Do Not Allow Remote Administration）来禁用 SUSE Linux Enterprise Server 上的远程管理。

## 如何远程访问服务器进行管理

要访问配置了远程管理的 SUSE Linux Enterprise Server，您可以使用 VNC 客户端或支持 Java 的 Web 浏览器。

要从 Web 浏览器访问服务器，请执行以下操作：

- 1. 从计算机桌面打开 Web 浏览器；然后输入以下：

`http://hostname:5801`

其中 *hostname* 是服务器的 IP 地址或主机名。

出现图 10-5 中的对话框。

![](img/667acce1695f6403deb2b60e994760c8_645_0.png)

图 10-5

从 VNC 会话窗口的顶部，您可以选择设置会话选项和将项目放入剪贴板等项目。
