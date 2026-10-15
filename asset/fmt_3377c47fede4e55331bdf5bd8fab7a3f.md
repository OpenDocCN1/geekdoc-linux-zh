
# 停止最近运行的进程进程

## 使用 Kali Linux 2.0 进行渗透测试

`Stop-Process -processname calc`

### 列表 953 - 审查脚本

我们在 `system_report.ps1` 文件中发现了一组据。用户名是 'sandboxalex'，密码是 'Ndaw*nRoqC+haZ'。我们似乎还发现了脚本安装的目标机器名称 'Poultry'。考虑到此目录下脚本的类型，并考虑到用户似乎是 'sandbox' 域的一部分，我们可能正在看一台 Windows 计算机。

> 将你发现的脚本下载并保存在你的笔记中是一个好习惯。你永远不知道某些东西何时会被删除，或者客户何时会要求更多证据。

## 24.5.3 创建一个稳定的反向隧道

类似于我们通过 `www-data` 用户获得 Ajla 的无权限 shell 访问时，我们无法为 Zora 使用 mysql 用户进行标准的 ssh 连接，因为该用户默认没有 shell 访问权限。

虽然我们可以创建一个类似于在 Ajla 上使用的 ssh 隧道，但还有另一个选项，我们设置 Zora 运行着最新版本的 Alpine。较新版本的 ssh 客户端允许我们建立一种非常实用的用于动态端口转发的反向隧道。

```bash
ssh -V

OpenSSH_8.1p1, OpenSSH_1.1d1 10 Sep 2019
```

### 列表 954 - 检查 ssh 版本

Zora 运行着 OpenSSH_8.1p1，它应该支持此功能。如果我们能让它工作，我们就可以通过在我们的 Kali 上运行的 SOCKS 代理获得对 10.5.0/24 内部网络的完全网络访问。由于我们只有访问 met，我们需要在 Zora 上创建一个新的 ssh key。首先，让我们在 Zora 上生成一个 ssh key。

```bash
ssh-keygen

Generating public key pair.

Enter file in which to save the key (/var/lib/ssh/id_rsa):

Enter passphrase (empty for no):

Enter passphrase again:

Created key /var/lib/ssh/id_rsa

Public key has been saved in /var/lib/ssh/id_rsa.pub.
```

```bash
ssh-rsa AAAAB3Nzac2EAAAABQQC4c...
```

### 列表 955 - 生成 SSH 密钥

PWK 2.0
Copyright © Offensive Security Ltd. All rights reserved.

## 使用 Kali 进行渗透测试 2.0

通过 `www-data` 用户获得 Ajla 的无权限 shell 访问时，我们无法使用 mysql 用户为 Zora 使用标准的 ssh 连接，因为该用户默认没有 shell 访问权限。

虽然我们可以创建一个类似于在 Ajla 上使用的 ssh 隧道，但还有另一个选项，我们设置 Zora 运行着最新版本的 Alpine。较新版本的 ssh 客户端允许我们建立一种非常实用的用于动态端口转发的反向隧道。

```bash
ssh -V

OpenSSH_8.1p1, OpenSSH_1.1d1 10 Sep 2019
```

### 列表 954 - 检查 ssh 版本

Zora 运行着 OpenSSH_8.1p1，它应该支持此功能。如果我们能让它工作，我们就可以通过在我们的 Kali 上运行的 SOCKS 代理获得对 10.5.0/24 内部网络的完全网络访问。由于我们只有访问 met，我们需要在 Zora 上创建一个新的 ssh key。首先，让我们在 Zora 上生成一个 ssh key。

```bash
ssh-keygen

Generating public key pair.

Enter file in which to save the key (/var/lib/ssh/id_rsa):

Enter passphrase (empty for no):

Enter passphrase again:

Created key /var/lib/ssh/id_rsa

Public key has been saved in /var/lib/ssh/id_rsa.pub.
```

```bash
ssh-rsa AAAAB3Nzac2EAAAABQQC4c...
```

### 列表 955 - 生成 SSH 密钥

PWK 2.0
Copyright © Offensive Security Ltd. All rights reserved.

# 渗透安全
www.offensive-security.com

3389/tcp 开启 ms-tcp-server
5900/tcp 关闭 vnc
8086/tcp 关闭 http-proxy

Nmap 扫描完成：扫描了 1 个 IP 地址（1 个主机）。Nmap 发现端口 135, 139, 445 和 3389 处于开启状态。然而，端口 53 是关闭的，而该端口在域控制器上通常是开启的。这很可能不是我们正在寻找的域控制器，但其他端口仍然表明这是一个 Windows 操作系统。前 20 个端口没有显示任何 HTTP 应用，因此让我们尝试通过发现的凭据通过 RDP 登录来“利用”这台机器。

### 24.6.2 漏洞利用（或仅仅登录）

现在我们有更大的把握确认该主机运行着 Windows，并且发现 RDP 是开启的，我们将使用 `xfreerdp` 连接到它。配合 Nmap，我们必须使用 `proxychains` 命令来准备 `xfreerdp`。我们通过 `/d:sandbox` 和 `/u:alex` 标志提供域名和用户名。为了重定向剪贴板，我们将使用 `+clipboard` 标志，这将允许我们在 Poultry 之间复制和粘贴。最后，我们还将为主机提供 `/v:10.5.5.20`。
