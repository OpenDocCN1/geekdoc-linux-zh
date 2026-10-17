
The SSH tools are listed in Table 18-1. They include several client programs like `scp` and `ssh`, as well as the `ssh` server. The `ssh` server (`sshd`) provides secure connections to anyone from the outside using the `ssh` client to connect. Several configuration utilities are also included, such as `ssh-add`, which adds valid hosts to the authentication agent, and `ssh-keygen`, which generates the keys used for encryption.

On Red Hat, you can start, restart, and stop the `sshd` server with the `service` command or `redhat-config-services` (Services on Server Settings window and menu):

```
service sshd restart
```

For version 2, names of the actual tools have a 2 suffix. Version 1 tools have a 1 as their suffix. During installation, however, links are set for each tool to use only the name with the suffix. For example, if you have installed version 2, there is a link called `scp` to the `scp2` application. You can then use the link to invoke the tool. Using `scp` starts `scp2`. Table 18-1 specifies only the link names, as these are the same for each version. Remember, though, some applications, such as `sftp`, are available only with version 2.

## SSH Setup

Using SSH involves creating your own public and private keys and then distributing your public key to other users you want to access. These can be different users or simply user accounts of your own that you have on remote systems. Often people remotely log in from a local client into an account on a remote server, perhaps from a home computer to a company computer. Your home computer would be your client account, and the account on your company computer would be your server account. On your client account, you would need to generate your public and private keys. Then you would have to place a copy of your

| Application | Description |
|---|---|
| `ssh` | SSH client. |
| `sshd` | SSH server (daemon). |
| `sftp` | SSH FTP client, Secure File Transfer Program. Version 2 only. Use `?` to list `sftp` commands (SFTP protocol). |
| `sftp-server` | SSH FTP server. Version 2 only (SFTP protocol). |
| `scp` | SSH copy command client. |
| `ssh-keygen` | Utility for generating keys. `-h` for help. |
| `ssh-keyscan` | Tool to automatically gather public host keys to generate `ssh_known_hosts` files. |
| `ssh-add` | Adds RSA and DSA identities to the authentication agent. |
| `ssh-agent` | SSH authentication agent that holds private keys for public key authentication (RSA, DSA). |
| `ssh-askpass` | X Window System utility for querying passwords, invoked by `ssh-add` (openssh-askpass). |
| `ssh-askpass-gnome` | GNOME utility for querying passwords, invoked by `ssh-add`. |
| `ssh-signer` | Signs host-based authentication packets. Version 2 only. Must be suid root (performed by installation). |
| `slogin` | Remote login (version 1). |

服务器账户中的公钥。你可以通过简单地通过电子邮件发送密钥文件或从软盘复制文件来完成此操作。一旦你的服务器上的账户拥有了你的客户端用户的公钥副本，你就可以从客户端账户访问服务器账户。你还将被提示输入服务器账户的密码短语。你必须知道它才能访问该账户。图 18-1 说明了允许用户 `george` 访问账户 `cecelia` 的 SSH 设置。

要允许你使用 SSH 访问其他账户，需要以下步骤：

- 在你的账户上创建公钥和私钥以及密码短语。你需要使用此密码短语从另一个账户访问你的账户。
- 将你的公钥分发到你想要访问的其他账户中，将其放置在 `.ssh/authorized_keys` 文件中。
- 其他账户也必须设置公钥和私钥以及密码短语。
- 你还需要知道其他账户的密码短语才能访问它。

### 使用 ssh-keygen 创建 SSH 密钥

你使用 `ssh-keygen` 命令创建公钥和私钥。你需要指定要使用的加密类型。你可以使用 DSA 或 RSA 加密。使用 `-t` 选项并以小写形式指定加密名称（`dsa` 或 `rsa`）。在以下示例中，用户使用 RSA 加密创建了一个密钥：

```
ssh-keygen -t rsa
```

`ssh-keygen` 命令会提示你输入密码短语，它将用作保护你的私钥的密码。密码短语应由多个单词组成。你还将被提示输入密钥的文件名。如果未输入，SSH 将使用其默认值。公钥将获得 `.pub` 扩展名。`ssh-keygen` 命令会生成公钥并将其放置在 `.ssh/id_dsa.pub` 或 `.ssh/id_rsa.pub` 文件中，具体取决于你指定的密钥类型；它将私钥放置在相应的 `.ssh/id_dsa` 或 `.ssh/id_rsa` 文件中。

![](img/6c226e8ba1efd427dec3bf582418d33f_350_0.png)

图 18-1 SSH 设置和访问

> 注意 `.ssh/identity` 文件名在 SSH 版本 1 中使用；在较旧的发行版版本上可能默认安装。SSH 版本 2 使用不同的文件名，`.ssh/id_dsa` 或 `.ssh/id_rsa`，具体取决于使用 RSA 或 DSA 身份验证。

如果需要更改你的密码短语，你可以使用 `ssh-keygen` 命令和 `-p` 选项。每个用户都将在自己的主目录中拥有自己的 SSH 配置目录，称为 `.ssh`。公钥和私钥以及 SSH 配置文件都放在这里。如果你从源代码构建，`make install` 操作将自动运行 `ssh-keygen`。表 18-2 列出了 SSH 配置文件。

## 授权密钥
