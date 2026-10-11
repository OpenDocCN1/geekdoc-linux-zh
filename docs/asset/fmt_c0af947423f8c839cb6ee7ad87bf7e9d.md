
```
[Shreya@localhost]$ chmod 600 SSH2-Shreya
[Shreya@localhost]$ chmod 600 SSH2-Shreya.pub
```

5. 一旦你创建了密钥对，将公钥文件上传到相应的主目录，在授权文件中添加了条目，并在标识文件中添加了条目，你现在应该能够使用公钥登录。务必使用 `-i` 选项配合标识文件，而不是私钥文件；否则你会收到“No further authentication methods available”（没有可用的进一步身份验证方法）错误。以下示例语法：

```
[Shreya@localhost]$ ssh2 SSH-Server -i identification
```

### 如何在 VShell SSH 服务器上使用 OpenSSH 密钥

将 OpenSSH 客户端密钥用于 VShell SSH 服务器比上一节更加直接。由于 VShell SSH 服务器接受 OpenSSH 密钥格式，因此无需将 OpenSSH 密钥转换为其他格式，这节省了宝贵的时间和许多潜在的麻烦！既然你有一个 OpenSSH 客户端密钥，我将演示如何在 VShell SSH 服务器上使用 OpenSSH 密钥。

1. 将 OpenSSH 公钥文件复制到远程 VShell SSH 服务器，特别是位于 `C:\Program Files\VShell\PublicKey\%USER%` 的公钥文件夹中。

2. 确保远程 VShell SSH 服务器已启用公钥身份验证。

3. 从客户端机器，使用以下语法连接到 VShell SSH 服务器：

```
ssh <VShell Server> -P 22 -i OpenSSHPrivateKey -l <username on VShell server>
```

使用前面的示例，以 Shreya 作为 OpenSSH 私钥，身份验证过程的示例如下：

```
ssh VshellServer -p 22 -i Shreya -l shreya

Enter passphrase for key 'Shreya':

Authenticated with partial success

Shreya@VshellServer's password:

C:\\
```

请注意，在密钥身份验证成功后，VShell 会要求在 VShell 服务器上输入密码。这只在 VShell 服务器上同时要求密码和公钥复选框的情况下发生。如果公钥是唯一需要的身份验证方法，就不会出现密码提示；然而，这是强制实施双因素身份验证的一种很好的方法，管理目的上应该要求这一点。

### 使用 SSH Communications 的 SSH 客户端创建密钥（Unix 和 Windows 命令行）

要在 Windows 或 Unix 上使用 SSH Communications 的 SSH 客户端创建密钥，请完成以下步骤。

1. 更改目录至 `ssh-keygen` 二进制文件所在的位置：

```
cd /usr/local/bin
C:\cd "Program Files\SSH Secure Shell\bin"
```

2. 创建 DSA 密钥对：

```
ssh-keygen2
Generating 2048-bit dsa key pair
2 Ooo.o0o.ooo.
```

3. 密钥生成后，输入口令，并确认口令：

```
Key generated.
2048-bit dsa, kusum@localhost.com, Fri Aug 15 2003 11:17:00
Passphrase :
Again :
Private key saved to /home/kusum/.ssh2/id_dsa_2048_a
Public key saved to /home/kusum/.ssh2/id_dsa_2048_a.pub
```

4. 确认口令后，公钥和私钥都应该已生成。在这种情况下，公钥文件的名称将是 `id_dsa_2048_a.pub`，私钥文件的名称将是 `id_dsa_2048_a`。密钥应自动保存到 Unix 用户主目录中的 `.ssh2` 文件夹（`/home/<username>/.ssh2/`）以及 Windows 用户的主文件夹（Documents and Settings/`<username>`/Application Data/SSH/UserKeys。Windows 下的位置如下所示：

```
Private key saved to C:\Documents and Settings\Administrator\Application Data\SSH\UserKeys\id_dsa_2048_a
Public key saved to C:\Documents and Settings\Administrator\Application Data\SSH\UserKeys\id_dsa_2048_a.pub
```

5. SSH Communications 的 SSH 客户端密钥已生成！

创建过程完成后，将 SSH 公钥复制到 SSH 服务器。以下部分演示如何在 SSH Communications 的 SSH 服务器、OpenSSH 服务器和 VanDyke VShell SSH 服务器上使用 SSH 客户端密钥。

### 如何在 SSH Communications 的 SSH 服务器上使用 SSH 客户端密钥

在将您的公钥（例如，`id_dsa_2048_a.pub`）安全上传到 SSH 服务器（通常位于用户的主目录，Unix 为 `/home/<username>/.ssh2`，Windows 为 Documents and Settings\`<username>`\.ssh2）后，还需要在用户主目录中的授权文件中添加公钥条目，该文件标记为 `Authorization`。语法如下：

```
Key id_dsa_2048_a.pub
```

在 SSH 服务器上创建授权文件后，需要在 SSH 客户端上创建识别文件，通常位于用户主目录中的 `ssh2` 文件夹内（Unix 为 `/home/<username>/.ssh2`，Windows 为 Documents and Settings\`<username>`\.ssh2）。SSH 客户端使用 `-i` 标志使用该文件来指示用于认证的私钥。务必在 SSH 客户端上使用 `-i` 选项配合此文件。创建此文件的语法如下：

```
echo "idkey id_dsa_2048_a" >> identification
```

完成密钥对创建、将公钥文件上传到相应的主目录、在授权文件中添加条目以及在识别文件中添加条目后，您应该能够通过公钥登录。以下是对语法的演示：

```
ssh2 <SSH server IP address> -i identification
```

### 如何在 OpenSSH 服务器上使用 SSH 客户端密钥

若要在 OpenSSH 服务器上使用 SSH Communications 的 SSH 客户端公钥和私钥对，请完成以下步骤。

- 确保您的密钥对不包含密码短语。虽然在转换过程中移除密码短语很重要，但请务必在转换过程完成后为旧密钥和新转换的密钥都添加密码短语。若要更改密钥的密码短语，请使用 `-e` 开关。

```
ssh-keygen2 -e id_dsa_2048_a
```

- 移除密码短语后，我们需要使用以下命令将 SSH Communications 的 SSH 密钥转换为 OpenSSH 兼容格式：

```
[Shreya@localhost]$ssh-keygen2 -i id_dsa_2048_a.pub > id_dsa_2048_a_Open.pub
[Shreya@localhost]$ssh-keygen2 -i id_dsa_2048_a > id_dsa_2048_a_Open
```

- 一旦您将公钥复制到 SSH 服务器（使用 SFTP 或某种替代的安全方法，没有自动化工具来执行此操作），请在 OpenSSH 服务器上输入以下命令，将新转换的公钥添加到位于 OpenSSH 服务器上用户主目录中的授权密钥文件。

```
[Shreya@OpenSSHserver]$cat id_dsa_2048_a_Open.pub >> /home/Shreya/.ssh/authorized_keys
```

- 在 SSH 客户端上，公钥和私钥对的权限需要受到保护才能使用。对生成的密钥文件设置以下权限：

```
[Shreya@localhost]$chmod 600 id_dsa_2048_a_Open.pub
[Shreya@localhost]$chmod 600 id_dsa_2048_a_Open
```
