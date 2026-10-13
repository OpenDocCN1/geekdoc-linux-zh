
```
Host work
    HostName 35.194.18.119
    IdentityFile ~/.ssh/id_work
    User neilsmyth
```

```
Host home
    HostName 192.168.0.21
    IdentityFile ~/.ssh/id_home
```

在设置配置文件之前，用户将使用以下命令连接到 `work` 系统：

```
$ ssh -l neilsmyth -i ~/.ssh/id_work 35.194.18.119
```

现在，命令可以缩短如下：

```
$ ssh work
```

可以通过运行以下命令找到配置文件的完整选项列表：

```
$ man ssh_config
```

### 15.7 从 Windows 客户端进行 SSH 基于密钥的身份验证

Windows 的最新版本作为 Windows PowerShell 的一部分包含了大多数 Linux 和 macOS 系统使用的 OpenSSH 实现的子集。这允许使用与上面为 Linux 和 macOS 概述的类似步骤从 Windows 客户端设置 SSH 基于密钥的身份验证。

在 Windows 上，搜索 Windows PowerShell 并从结果中选择它。运行后，PowerShell 窗口将如下图 15-1 所示出现：

![](img/be1f159c3cc937d7b264dc5b134856dc_133_0.png)

图 15-1

如果您已从其他客户端系统拥有私钥，请将 `id_rsa` 文件复制到 Windows 系统上的名为 `.ssh` 的文件夹中。文件就位后，按如下方式在 PowerShell 窗口中测试身份验证：

```
$ ssh -l <username>@<hostname>
```

例如：

```
PS C:\Users\neil> ssh -l neil 192.168.1.101
Enter passphrase for key 'C:\Users\neil\.ssh\id_rsa':
```

在提示时输入密码短语并完成身份验证过程。

如果私钥尚不存在，请使用 `ssh-keygen` 实用程序在 PowerShell 窗口中生成新的私钥和公钥对，使用为 Linux 和 macOS 概述的相同步骤。生成密钥后，它们将再次位于当前用户主文件夹的 `.ssh` 目录中，并且公钥文件 `id_rsa.pub` 需要安装在远程 RHEL 9 系统上。不幸的是，Windows PowerShell 不包含 `ssh-copy-id` 实用程序，因此此任务必须手动执行。

在 PowerShell 窗口中，切换到 `.ssh` 子目录并显示公钥 `id_rsa.pub` 文件的内容：

```
PS C:\Users\neil> cd .ssh
PS C:\Users\neil\.ssh> type id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDFgx1vzu591116/uQw7FbmKV... neil@DESKTOP-S8P8D3N
```

突出显示文件内容并使用 Ctrl-C 键盘快捷键复制它。

仍在 PowerShell 窗口中，使用密码身份验证登录远程系统：

```
PS C:\Users\neil\.ssh> ssh -l <username> <hostname>
```

登录后，检查 `.ssh` 子目录是否存在。如果不存在，按如下方式创建它：

```
$ mkdir .ssh
```

进入 `.ssh` 目录并检查是否已存在名为 `authorized_keys` 的文件。如果不存在，请创建它并将 Windows 系统上公钥文件的内容粘贴到其中。

如果 `authorized_keys` 文件已存在，它可能包含其他密钥。如果是这种情况，请编辑文件并将新公钥粘贴到文件末尾。例如，以下文件包含两个密钥：

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCzRWH27Xs8ZA5rIbZXK... neil@localhost.localdomain
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDFgx1vzu591116/... neil@DESKTOP-S8P8D3N
36Rm6Ii3roUCoGCzGR8mn95JvRB3VtCyDdzTWSi8JBpK5gV5oOxNTNPsew1LzouB1CT1qW3CKwEiIwu8S
9MTL7m3nrcaNeLewTTHevvHw4QDwzPQ+B0PDg96fzsYoTXVhzyHSWyo6H0qgrft7aK+gILBtEIhWTkSVE
MAzy1piKtCr1IYTmVK6engv0aoGtMUq6FnOeGp5FjvKkF4aQkh1QR28r  neil@DESKTOP-S8P8D3N
```

公钥安装到服务器后，通过从 PowerShell 窗口登录服务器来测试身份验证，例如：

```
PS C:\Users\neil\.ssh> ssh -l neil 192.168.1.100
Enter passphrase for key 'C:\Users\neil\.ssh\id_rsa':
```

当为所有账户设置并验证基于密钥的身份验证后，请按照上一节末尾所述在 RHEL 9 系统上禁用密码身份验证。

### 15.8 使用 PuTTY 进行 SSH 基于密钥的身份验证

对于没有 OpenSSH 可用或作为使用 PowerShell 的更灵活替代方案的 Windows 系统，PuTTY 工具是一个广泛使用的替代方案。使用 PuTTY 的第一步是在需要 SSH 客户端的任何 Windows 系统上下载并安装它。PuTTY 是一个免费实用程序，可以使用以下链接下载：

https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html

下载与您的 Windows 系统匹配的 Windows 安装程序可执行文件（有 32 位和 64 位版本），然后执行安装程序完成安装。

如果私钥已存在于另一系统上，请在当前用户的主文件夹中创建 `.ssh` 文件夹并将私钥 `id_rsa` 复制到其中。

接下来，需要使用 PuTTYgen 工具将私钥文件转换为 PuTTY 私钥格式文件。通过在 Windows 开始菜单的搜索栏中输入“PuTTY Key Generator”找到此实用程序并启动它：

![](img/be1f159c3cc937d7b264dc5b134856dc_135_0.png)

图 15-2

启动后，单击操作部分中的 Load 按钮并导航到之前复制到 `.ssh` 文件夹的私钥文件（注意可能需要更改文件类型

## 在 RHEL 9 上配置基于 SSH 密钥的身份验证

过滤为所有文件 (*.*) 以使密钥文件可见)。找到后，选择该文件并将其加载到 PuTTYgen 中。系统提示时，输入最初用于加密文件的密码短语。导入私钥后，通过单击“保存私钥”按钮将其保存为 PuTTY 密钥文件。为保持一致性，将密钥文件保存到 `.ssh` 文件夹中，但使用不同的名称以将其与原始密钥文件区分开。

从“开始”菜单启动 PuTTY，并在主屏幕中输入远程服务器的 IP 地址或主机名，然后在左侧面板中选择 Connection -> SSH -> Auth -> Credentials 类别，如图 15-3 所示：

![](img/be1f159c3cc937d7b264dc5b134856dc_136_0.png)

图 15-3

单击“用于身份验证的私钥”字段旁边的“浏览”按钮，然后导航到并选择之前保存的 PuTTY 私钥文件。然后，可选地，滚动到左侧面板顶部，选择“会话”条目，并在“已保存会话”字段中输入会话名称，然后单击“保存”按钮。这将保存会话配置以供将来使用，而无需每次重新输入设置。

最后，单击“打开”按钮以建立与远程服务器的连接，系统提示时输入用户名和密码短语以完成身份验证。

### 15.9 使用 PuTTYgen 生成私钥

前一节介绍了在使用 PuTTY 时使用现有私钥和公钥的情况。如果不存在密钥，可以使用 PuTTYgen 工具创建密钥，该工具包含在主 PuTTY 安装中。

要创建新密钥，请启动 PuTTYgen 并单击图 15-4 中突出显示的“生成”按钮：

![](img/be1f159c3cc937d7b264dc5b134856dc_137_0.png)

图 15-4

按说明移动鼠标指针以生成随机数据，然后输入可选的密码短语以加密私钥。生成密钥后，使用“保存公钥”和“保存私钥”按钮将文件保存到合适的<|message|>位置。如前一节所述，私钥可与 PuTTY 一起使用。要将公钥安装到远程服务器上，请使用 Windows 上 PowerShell 中 SSH 部分介绍的步骤。

### 15.10 摘要
