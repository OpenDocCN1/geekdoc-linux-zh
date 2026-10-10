
与普通的远程 shell 服务一样，**SSH** 会查看 `/etc/hosts.equiv` 文件和用户的 `.rhosts` 文件，以确定是否应该允许连接。它还会查看 SSH 专用文件 `/etc/ssh/ssh_hosts.equiv` 和 `.shosts`。使用 `ssh_hosts.equiv` 和 `.shosts` 文件更可取，因为这样可以避免向非加密的远程 shell 服务授予访问权限。`/etc/ssh/ssh_hosts.equiv` 和 `.shosts` 文件在功能上等同于传统的 `hosts.equiv` 和 `.rhosts` 文件，因此相同的说明和规则同样适用。你可以通过停用 `.rhosts` 和 `.shosts` 文件的使用来提高安全性。在 `/etc/ssh/sshd_config` 文件中通过取消注释以下行来实现：

```
#IgnoreRhosts  yes
```

（如需更多信息，请运行 **man hosts.equiv** 和 **man ssh** 命令。）

现在你准备好测试 SSH 服务了。从另一台已安装 SSH 的计算机（甚至如果不是这样的情况下，也可以从同一台计算机）输入 `ssh` 命令，后跟一个空格和你要连接的系统名称。例如，要连接到系统 `ratbert.glaci.com`，输入：

```
$ ssh ratbert.glaci.com
```

如果你第一次使用 `ssh` 命令登录到该系统，它会要求你确认是否真的想连接。当出现如下提示时，输入 **yes** 并按 Enter 键：

```
The authenticity of host 'ratbert.glaci.com (199.170.177.18)' can't be
established.
RSA key fingerprint is xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx.
Are you sure you want to continue connecting (yes/no)? yes
```

> **注意：** 如果你第二次看到认证请求，这可能是**中间人**攻击。

如果启动 `ssh` 连接时未指定用户名，SSH 守护程序将假定你希望使用客户端登录的用户名。如果你想以不同的用户名（例如 `chris`）登录，可以输入以下内容：

```
$ ssh chris@ratbert.glaci.com
```

或者

```
$ ssh -l chris ratbert.glaci.com
```

一旦登录成功，就会显示 shell 提示符，你可以开始像使用本地 shell 一样使用远程系统。

`scp` 命令类似于用于在 Linux 系统之间复制文件的 `rcp` 命令。下面是一个使用 `scp` 命令将名为 `jake` 的用户主目录中名为 `memo` 的文件复制到名为 `maple` 的计算机上 `/tmp` 目录的示例：

```
$ scp /home/jake/memo maple:/tmp
jake@maple's password: ******
memo	100%  177KB 101.3KB/s  00:02
```

输入你的用户名密码（如果要求输入密码）。如果密码被接受，远程系统会指示文件已成功复制。

同样，sftp 命令会启动与支持 SSH 连接的 FTP 服务器进行交互式 FTP 会话。许多注重安全的人更喜欢使用 sftp 而不是其他 ftp 客户端，因为它在本地与远程主机之间提供了安全的连接。这里有一个示例：

```
$ sftp ftp.handsont-history.com
Connecting to ftp.handsont-history.com
jake@ftp.handsont-history.com’s password: ******
sftp>
```

此时，你可以开始交互式 FTP 会话。你可以像使用任何 FTP 客户端一样对文件使用 get 和 put 命令，但你可以放心地知道你在安全连接上工作。

> **提示：** 与 ssh 和 scp 一样，sftp 命令要求服务器上必须运行 SSH 服务。如果你无法使用 sftp 连接到 FTP 服务器，可能是因为 SSH 服务不可用。也可能是在服务器的 `/etc/ssh/sshd_config` 文件中禁用了该服务。

## 使用 ssh、scp 和 sftp 而不需要密码

对于经常使用的机器，通常很有帮助的是将它们配置为无需使用密码即可登录。以下程序展示了如何做到这一点。

这些步骤将引导你完成从一台机器到另一台机器的无密码认证设置。在本示例中，本地用户在名为 host1 的计算机上名为 chester。远程用户在名为 host2 的计算机上也名为 chester。

1. 登录到本地计算机（在本示例中，我以 chester 身份登录到 host1）。

   **注意：** 在你的本地工作站上，仅以本地用户身份运行步骤 2 一次。除非你丢失了 ssh 密钥，否则不要再次运行。在配置后续远程服务器时，直接跳到步骤 4。

2. 输入以下内容以生成 ssh 密钥：

   ```
   $ ssh-keygen -t dsa
   Generating public/private dsa key pair.
   Enter file in which to save the key
   (/home/chester/.ssh/id_dsa): <Enter>
   Enter passphrase (empty for no passphrase): <Enter>
   Enter same passphrase again: <Enter>
   Your identification has been saved in /home/chester/.ssh/id_dsa.
   Your public key has been saved in /home/chester/.ssh/id_dsa.pub.
   The key fingerprint is:
   3b:c0:2f:63:a5:65:70:b7:4b:e0:2a:c4:18:24:47:69 chester@host1
   ```

3. 按 Enter 接受默认密钥文件位置。然后再次按 Enter（两次）以分配空白密码短语。（如果你输入密码短语，系统会提示你输入该密码短语，并且没有它就无法登录。）

4. 你必须通过关闭对主目录、.ssh 目录和认证文件的权限来保护认证密钥的权限，如下所示：

   ```
   $ chmod go-w $HOME
   $ chmod 700 $HOME/.ssh
   $ chmod go-rwx $HOME/.ssh/*
   ```

5. 输入以下内容将密钥复制到远程服务器（将 `chester` 替换为远程用户名，将 `host2` 替换为远程主机名）：

   ```
   $ cd -/.ssh
   $ scp id_dsa.pub chester@host2:/tmp
   chester@host2's password: ******
   ```

6. 输入以下内容将 ssh 密钥添加到远程用户的授权密钥中（代码应位于一行，不要换行）：

   ```bash
   $ ssh chester@host2 'cat /tmp/id_dsa.pub >> /home/chester/.ssh/authorized_keys2'
   ```

   > **注意：** 上两步会要求输入密码。这是正常的。此外，你可能希望使用 `chmod` 命令将 `authorized_keys2` 文件的访问权限限制为仅该用户。有关 `chmod` 的更多信息，请参阅第 4 章。

7. 为了让 `sshd` 守护程序接受你创建的 `authorized_keys2` 文件，你的主目录和认证文件必须具有安全的权限。为了保护这些文件和目录，输入以下内容（注意，需要双引号以防止 \* 被本地 shell 解释）：

   ```
   $ ssh chester@host2 chmod go-w $HOME
   $ ssh chester@host2 chmod 700 $HOME/.ssh
   $ ssh chester@host2 "chmod go-rwx $HOME/.ssh/*"
   ```

8. 输入以下内容以从临时目录中删除密钥：

   ```
   $ ssh chester@host2 rm /tmp/id_dsa.pub
   ```

需要注意的是，一旦你成功设置好这种机制，无论本地计算机的 IP 地址如何变化多少次，它都将有效。IP 地址与这种认证方式无关。

## 保护 Linux 服务器

将你的 Fedora 系统作为公共网络上的服务器开放，在安全方面会带来一系列全新的挑战。你的计算机不仅要拒绝几乎所有传入请求，还将被期望响应受支持服务（如 Web、FTP 或邮件服务）的请求，通过提供信息或运行接收数据的脚本来满足这些请求。

整本书都充满了有关如何保护服务器安全的信息。许多依赖 Internet 服务器的企业会指定专职管理员负责监控其服务器的安全。因此，请将本节视为对需要警惕的一些攻击类型以及可用于保护 Fedora 服务器的一些工具的概述。

### 理解攻击技术

对计算系统的攻击因攻击者的目标和资源不同而呈现不同的形式。一些攻击者想要制造破坏，而另一些则想要渗透你的机器并利用其资源用于其不正当目的。还有一些攻击者针对你的数据以获取经济利益或进行勒索。以下是三种主要类型的攻击：

- **拒绝服务（DoS）** — 最容易实施的攻击是拒绝服务攻击。这些攻击的主要目的是通过过载无关数据来扰乱远程站点的活动。DoS 攻击可以简单到每秒向网站发送数千个页面请求。这类攻击容易实施，也容易防御。一旦你掌握到攻击来源，只需给肇事者的 ISP 打个电话就能解决问题。如果 DoS 攻击伪造了返回地址，你可能需要花更多精力来追踪来源。

- **分布式拒绝服务（DDoS）** — 更高级的 DoS 攻击被称为分布式拒绝服务攻击。DDoS 攻击更难实施，且几乎无法阻止。在这种形式的攻击中，攻击者控制成百上千台安全较弱的互联网络计算机。然后攻击者指挥它们统一向单个 Internet 主机发送无关数据流。结果是一位攻击者的威力被放大了数千倍。与常规 DoS 中攻击来自一个方向不同，它来自数千个方向同时发起。防御 DDoS 攻击的最佳方法是联系你的 ISP，看看是否可以在其边界路由器上过滤流量。

很多人使用“我的机器上没有任何人想要的东西”这种借口来逃避考虑安全问题。这种论点的问题在于，攻击者有很多理由使用你的机器。攻击者可以将你的机器转变为代理，以便日后用于 DDoS 攻击。不止一次，当局出现在一脸困惑的计算机用户门口，询问关于源自其计算机的威胁的问题。通过忽视安全，所有者让自己承担了巨大的责任。

> **注意：** 如果你的系统或网页被诸如 slashdot.org 等流行的 Internet 网站提及，你可能会经历看似 DDoS 攻击的情况，但实际上只是一大群人试图访问你的网站。

