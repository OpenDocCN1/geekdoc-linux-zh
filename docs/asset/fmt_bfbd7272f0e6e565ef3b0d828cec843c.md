
3. 当提示时，输入密钥文件的密码短语。这样做后，你应该会收到身份已添加的提示。示例如下：

```text
rtracy@ws1:~$ ssh-agent bash
rtracy@ws1:~$ ssh-add ~/.ssh/id_rsa
Enter passphrase for /home/rtracy/.ssh/id_rsa:
Identity added: /home/rtracy/.ssh/id_rsa (/home/rtracy/.ssh/id_rsa)
rtracy@ws1:~>
```

完成后，`ssh-agent` 进程将密码短语存储在内存中。然后它会监听 SSH 请求，并在请求时自动为你提供密钥密码短语。让我们在下面的练习中实践配置 SSH 使用公钥认证：

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_771_0.png)

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_771_1.png)

### 练习 18-3：配置公钥认证

**视频** 欲了解更多信息，请观看练习 18-3 的视频。

在本练习中，你将生成一对 RSA 密钥，并将公钥复制到 SSH 服务器，以启用公钥认证。请完成以下操作：

1. 在你的客户端系统上生成一对 RSA 密钥，步骤如下：
    - a. 以标准用户身份登录到你的客户端系统。
    - b. 打开一个终端会话。
    - c. 在 shell 提示符下，输入 `ssh-keygen -t rsa`。
    - d. 当提示选择保存私钥的文件时，按 `ENTER` 键使用默认文件名 `~/ssh/id_rsa`。
    - e. 当提示输入时，为该密钥输入一个口令短语。

2. 配置服务器系统以使用公钥认证，步骤如下：
    - a. 通过输入 `scp ~/ssh/id_rsa.pub user_name@address_of_SSH_server:mykeyfile`，将你刚刚创建的公钥复制到你的 SSH 服务器系统。
    - b. 当提示输入时，输入远程用户的密码。
    - c. 使用以下命令与远程系统建立 SSH 会话，身份为你打算进行公钥认证的用户：`ssh -l user_name address_of_SSH_server`。
    - d. 当提示输入时，输入远程用户的密码。
    - e. 在远程系统的 shell 提示符下，通过输入 `ls -la` 检查 `.ssh` 隐藏目录是否已存在。如果 `.ssh` 目录不存在，请使用 `mkdir ~/.ssh` 命令创建它。否则，请继续下一步。
    - f. 在远程系统的 shell 提示符下，输入 `cat mykeyfile >> ~/.ssh/authorized_keys`。
    - g. 在 shell 提示符下输入 `exit` 以关闭 SSH 会话。

3. 通过以下步骤测试新配置：
    - a. 在你的客户端系统的 shell 提示符下，输入 `ssh -l user_name address_of_SSH_server`。
    - b. 当提示输入时，输入你分配给 RSA 私钥的口令短语。此时，你应该能够自动通过 SSH 服务器的认证。
    - c. 在 shell 提示符下输入 `exit` 以关闭会话。

4. 配置 `ssh-agent` 以记住你的私钥口令短语，步骤如下：
    - a. 在你的客户端系统的 shell 提示符下，输入 `ssh-agent bash`。
    - b. 在 shell 提示符下，输入 `ssh-add ~/.ssh/id_rsa`。
    - c. 当提示输入时，输入密钥文件的口令短语。执行此操作后，系统应提示身份已添加。
    - d. 在你的客户端系统的 shell 提示符下，输入 `ssh -l user_name address_of_SSH_server`。你应该能够自动通过 SSH 服务器的认证，而无需被提示输入私钥口令短语。

做得好！你现在是一名 SSH 专家了！在结束本章之前，我们还需要讨论另一个与加密相关的话题：加密文件。让我们接下来做这个。

### 加密 Linux 文件

正如你可以使用 OpenSSH 加密 Linux 系统之间的网络传输一样，你也可以使用加密来保护 Linux 文件系统中的文件。你可以使用各种工具来做到这一点。有些是开源的，有些则是专有的。为了应对你的 Linux+/LPIC-1 考试，你需要知道如何使用开源的 GNU Privacy Guard (`GPG`) 实用工具来加密文件。因此，我们将在此处使用这个工具。我们将讨论以下内容：

- `GPG` 的工作原理

- 使用 `GPG` 加密文件

让我们首先讨论 `GPG` 是如何工作的。

#### GPG 的工作原理

Gnu Privacy Guard (`GPG`) 是 OpenPGP 标准（RFC 4880）的一个开源实现。它允许你加密并对你数据和通信进行数字签名。例如，你可以加密 Linux 文件系统中的文件。你还可以加密和数字签名电子邮件消息。

`GPG` 提供了一个加密引擎，可以直接从 shell 提示符使用 `gpg` 命令行实用工具调用。它也可以从系统上运行的 shell 脚本或其他程序中调用。例如，`GPG` 支持已集成到几个流行的 Linux 电子邮件客户端中，如 `Evolution` 和 `KMail`。它也集成到了即时通讯应用程序中，如 `Psi`。

还有各种图形前端可供 `GPG` 使用。一些较流行的前端包括 `KGPG` 和 `Seahorse`。然而，为了应对你的 Linux+/LPIC-1 考试，你需要知道如何从 shell 提示符使用 `GPG`，因此本章我们将重点关注这一点。

接收者的公钥与使用对称密钥加密的消息一起发送。当接收者收到消息时，`GPG` 首先使用用户的私钥解密对称密钥。然后，`GPG` 使用解密后的对称密钥来解密消息的其余部分。

`GPG` 支持许多加密算法，包括以下内容：

- 对称加密：
    - `AES`
    - `3DES`
    - `Blowfish`

- 非对称加密：
    - `Elgamal`
    - `RSA`

- 哈希：
    - `MD5`
    - `SHA-1` 和 `SHA-2`
    - `RIPEMD-160`

- 数字签名：
    - `DSA`
    - `RSA`

现在你了解了 `GPG` 是如何工作的，让我们回顾一下如何使用 `GPG` 来加密文件。

#### 使用 GPG 加密文件

要使用 `GPG` 加密文件，请执行以下操作：

1. 使用 `GPG` 生成你的密钥。为此，请在 shell 提示符下输入 `gpg --gen-key`。下面是一个示例：

    ```text
    rtracey@WS3:~-> gpg --gen-key
    gpg (GnuPG) 1.4.2; Copyright (C) 2005 Free Software Foundation, Inc.
    This program comes with ABSOLUTELY NO WARRANTY.
    This is free software, and you are welcome to redistribute it
    under certain conditions. See the file COPYING for details.

    gpg: directory '/home/rtracey/.gnupg' created
    gpg: new configuration file '/home/rtracey/.gnupg/gpg.conf' created
    gpg: WARNING: options in '/home/rtracey/.gnupg/gpg.conf' are not yet
    active during this run
    gpg: keyring '/home/rtracey/.gnupg/secring.gpg' created
    gpg: keyring '/home/rtracey/.gnupg/pubring.gpg' created
    Please select what kind of key you want:
       (1) DSA and Elgamal (default)
       (2) DSA (sign only)
       (5) RSA (sign only)
    Your selection?
    ```

2. 选择你要创建的密钥类型。通常你使用默认选项（1），它使用 `DSA` 和 `Elgamal`。系统会提示你指定密钥的大小，如下所示：

    ```
    DSA keypair will have 1024 bits.

    ELG-E keys may be between 2024 and 4096 bits long.

    What keysize do you want? (2048)
    ```

3. 指定你要创建的密钥大小。使用默认大小 2048 位通常就足够了。系统会提示你配置密钥有效期，如下所示：
