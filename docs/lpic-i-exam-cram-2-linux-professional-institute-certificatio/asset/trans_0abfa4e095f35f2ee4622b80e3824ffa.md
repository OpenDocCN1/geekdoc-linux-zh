
有几对特殊的文件会影响 SSH 的工作方式，特别是 `/etc/ssh/ssh_known_hosts` 和 `~/.ssh/known_hosts` 文件。

全局（`/etc`）文件用于检查试图通过 SSH 连接的主机的公钥，而本地（`~`）文件则是客户端获取远程服务器公钥的文件。如果开始与之前未知的主机建立新连接，用户会看到一条消息，告知该主机是未知主机，并询问是否希望将该主机的密钥存储在其已知主机文件中。如果用户回答“是”，该主机的公钥将被添加到 `~/.ssh/known_hosts` 文件中。

全局（`/etc`）文件应当对所有用户可读，且仅对 root 用户可写。本地（`~`）文件必须属于该用户且对该用户可写。

第二组特殊文件对是 `/etc/ssh/sshrc` 和 `~/.ssh/rc` 文件。

全局文件（`/etc/ssh/sshrc`）用于设置用户 SSH 会话的全局登录时初始化。任何应当在所有用户完成身份验证后、获得 shell 之前运行的内容（对所有用户生效）都应放在此文件中。

`~/.ssh/rc` 文件在功能上等同于 `/etc/ssh/sshrc` 文件，但它仅影响单个用户。如果此文件不存在，则使用 `/etc/ssh/sshrc` 文件。

有几个文件仅影响特定用户的环境，例如 `~/.ssh/authorized_keys` 文件。此文件用于存储可用于以该用户身份登录的公钥。这些密钥将与 `ssh` 或 `scp` 客户端在登录请求时提供的密钥进行匹配。

仅影响用户环境的第二个文件是 `~/.ssh/environment` 文件。它用于设置影响用户 SSH shell 环境的选项。

## 使用 SSH 客户端工具

SSH 客户端工具非常通用，提供了许多选项来定制体验。考试只需了解基础知识，但我这里还包含了一些我在过程中发现的一些实用技巧。

## 使用 SSH 客户端

SSH 客户端主要用于替代 RSH 和 Telnet 程序。其语法如下：

```
ssh -L username remotehost
```

如果您未使用 `-l` 选项指定用户名，SSH 将假设您希望使用当前登录的账户。

例如，我可以使用以下命令以 `snuffy` 用户身份连接到主机 `mp3server`：

```
ssh -l snuffy mp3server
```

如果之前未曾连接过该服务器，我会看到类似以下的消息：

```
The authenticity of host 'mp3server (192.168.33.44)' can't be established.
RSA key fingerprint is 73:4f:fa:b0:42:a4:3a:a8:64:2c:ad:26:1d:b1:21:00.
Are you sure you want to continue connecting (yes/no)?
```

如果我回答 `yes`，该主机的公钥将被添加到我的 `~/.ssh/known_hosts` 文件中，并类似于以下内容：

```
192.168.3.44 ssh-rsa AAAAB3NzaC1yc2EAAAABIwUAIGF1Bv9pQfkAZwNm#ac/
U8ITH9RB0CFUkeqkJxwl6
mgC1SPvV2JlW4ukcVVAOQJR3EHvOvh4PhoSG4yzB58JK8AUByOrSGJ7PDC+vyi1922hG
xWBWoolBBAO/Was817N0zQBJxD09QnOHcrIFeu7QcbQcrKJQMd0BHQjKj0=
```

## 使用 scp 客户端

与其使用 RCP 或 FTP，我的大多数文件传输工作都是使用 SCP 完成的。`scp` 命令使用 SSH 协议，并加密从一台主机发送到另一台主机的文件。

例如，如果我想将我的机器上 root 用户主目录中的 `file1` 传输到名为 `remotest` 的主机上的相同位置，我会使用以下命令：

```
scp /root/file1 root@remotest:/root/file1
```

这将提示我 RSA 密钥问题，然后是密码，然后传输文件。文件传输的输出看起来像这样：

```
root@192.168.1.73's password:
mypublickey.txt  100% !******************************| 1379  00:00
```

您可以像前面所示那样从您的主机复制到另一台主机，也可以通过反转源和目标指定从该主机复制回您的主机，甚至可以在您的主机上将文件从一台远程主机传输到另一台完全独立的远程主机。以下命令在您输入两台主机的密码后，递归地将 `/data` 目录及其所有内容从 `remotest` 复制到 `remotetwo`：

```
scp -r root@remotest:/data root@remotetwo:/data
```

SSH 协议的另一种用途是登录到主机，并使用 SSH 将 X 客户端的输出转发回您的显示终端。这是 SSH 客户端的默认行为，但如果您的环境将选项设置为关闭，则可以使用 `-X` 选项明确调用它。

## 不使用密码提示的 SSH

SSH 允许在计算机之间登录时跳过密码提示，如果您经常使用 SSH 或 scp 客户端，并且不介意有人坐在您意外解锁的工作站上并随意访问您的网络！这可能是方便的。

![](img/49f4f38f3aec011238fa50f89e643db3_527_0.png)

> 关于为什么要从用户目录中删除 .rhosts 文件有很多讨论。基本上，如果一个用户的 .rhosts 文件中包含某个主机名，并且该主机的 /etc/hosts_equiv 文件中也包含该用户的主机名，那么该用户可以无密码登录！这是一个安全风险，因此我的建议是使用以下命令删除这些文件：
> ```
> find /home -name .rhosts -exec rm -f {} \;
> ```
> 这将删除在用户主目录中发现的所有 .rhosts 文件，并且在每次删除时不会提示您。

当我需要启用无密码 SSH 使用时，以下是我采取的步骤。我有两台机器，fattyre 和 murphy，两者都是安装了默认必要 SSH 软件的 Linux 工作站。此演示假设 fattyre 和 murphy 都在彼此的主机文件中或通过 DNS 可解析。

以下是如何启用无密码 SSH 使用的方法：

1. 以 root 用户身份登录到 fattyre。
2. 在此示例中，使用名为 user1 的新用户。使用以下命令创建它：
   ```
   useradd -m user1
   ```
3. 使用 passwd 命令设置 user1 的密码，内容任意：
   ```
   passwd user1
   ```
4. 使用以下命令切换到 user1 用户账户：
   ```
   su - user1
   ```
5. 输入 user1 的密码。
6. 使用以下命令创建 `.ssh` 目录并设置权限：
   ```
   mkdir .ssh ; chmod 700 .ssh
   ```
7. 生成 RSA 密钥：
   ```
   ssh-keygen -b 1024 -t rsa
   ```
8. 当提示文件位置时，按 Enter 接受默认值。
9. 当提示输入密码短语时，输入以下内容：
   ```
   seatrc astronomy
   ```
10. 当提示时重新输入密码短语。
11. 进入 `.ssh` 目录，并使用以下命令设置 `id_rsa.pub` 文件的权限：
    ```
    cd .ssh ; chmod 644 id_rsa.pub
    ```
12. 将 `id_rsa.pub` 文件复制到一个名为 `authorized_keys` 的新文件：
    ```
    cp id_rsa.pub authorized_keys
    ```

**注意**

接下来的步骤在主机 **murphy** 上进行。

13. 使用 `ping` 确保您可以联系到主机 `fattyre`：
    ```
    ping fattyre
    ```
14. 以 `root` 用户身份登录到主机 `murphy`。
15. 使用以下命令添加名为 `user2` 的用户：
    ```
    useradd -m user2
    ```
16. 为 `user2` 设置密码：
    ```
    passwd user2
    ```
17. 两次输入密码以确认。
18. 使用此命令切换到 `user2` 账户：
    ```
    su - user2
    ```
19. 输入 user2 的密码。
20. 使用以下命令创建目录并设置其权限：
    `mkdir .ssh ; chmod 700 .ssh`

![](img/49f4f38f3aec011238fa50f89e643db3_529_0.png)

接下来的步骤在主机 `fattyre` 上进行。

21. 以 user2 身份连接到 `murphy` 主机：
    `ssh -l user2 murphy`
22. 当提示 RSA 密钥时，回答 yes，然后输入 user2 的密码。
23. 当通过 SSH 以 user2 身份登录到主机 `murphy` 时，使用以下命令从 `fattyre` 主机复制 `authorized_keys` 文件：
    `scp user1@fattyre:~/.ssh/authorized_keys ~/.ssh`
    `scp` 程序的输出应类似于以下内容：
    `authorized_keys 100% |*********************| 236 00:00`
24. 退出主机 `murphy` 上的 user2，返回到 `fattyre` 上的 user1。
25. 在 `fattyre` 上以 user1 身份，使用以下命令将 `ssh-agent` 作为 shell 的包装器调用：
    `ssh-agent $SHELL`
26. 将您的密钥添加到代理中：
    `ssh-add`
27. 当提示输入密码短语时，输入 `no more tears`（或者您在步骤 9 中选择的密码短语，如果“no more tears”是对特定示例短语的误读，请更正为可能的 OCR 错误，但严格遵循 OCR：输入步骤 9 中使用的密码短语）。（*基于上下文的更正：步骤 9 指定了“seatrc astronomy”。步骤 27 说“输入 no more tears”。这很可能是 OCR 错误，指代“seatrc astronomy”或只是一个占位符。我会保留“no more tears”，因为它与原文不同，但请注意源文件中可能存在错误。然而，查看前面的步骤，密码短语是“seatrc astronomy”。“no more tears”看起来像是一个干扰项或错误。我将保留原始文本“no more tears”，除非它是“seatrc astronomy”的明显笔误，否则“保留原始信息”。鉴于“seatrc astronomy”是定义的密码短语，“no more tears”很可能是 OCR 错误，或者是书中示例使用的实际短语。让我们仔细查看 [PAGE 528] 步骤 9：`seatrc astronomy`。[PAGE 529] 步骤 27：`enter no more tears`。这可能是书中的错误或 OCR 错误。我会保留“no more tears”，但它很可疑。等待，查看 OCR，它写着“enter no more tears”。我会保留它。*）
28. 然后您将看到类似以下的输出：
    `Identity added: /home/ssha/.ssh/id_rsa (/home/ssha/.ssh/id_rsa)`
29. 现在尝试以 user2 身份登录到 `murphy`，观察会发生什么：
    `ssh -l user2 murphy`
30. 您不应该看到任何密码提示；您应该只看到上次登录来源的确认信息：
    `Last login: Wed May 28 13:46:55 from fattyre`

