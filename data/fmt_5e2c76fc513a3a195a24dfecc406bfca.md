
在服务器端，您需要私钥以及包含公钥的证书。根据应用程序的不同，私钥可以是加密的（例如在配合 `Apache` 使用时），也可以是未加密的（例如在配合 `stunnel` 使用时）。

如果您使用了 `OpenSSL` 命令行界面，您可以在命令行中指定密钥文件。要创建一个私钥的未加密副本，请使用以下命令：

```bash
openssl rsa < private/encrypted_key.pem > unencrypted_key.pem
```

如果您在 `YaST CA` 节点模块中创建了证书，则需要从该模块将证书和私钥导出到文件。`YaST` 将证书和私钥导出到一个单个文件中。在导出对话框中，您可以选择格式以及私钥是否进行加密。在导出用于 `stunnel` 的密钥时，请在不加密私钥的情况下进行导出。使用软磁盘、USB 闪盘（U盘）或 `ssh` 将它们传输到服务器。

由于私钥是未加密的，因此只有 `root` 用户和 `stunnel` 进程能够读取该文件：

```bash
da10~ # cp /media/floppy/pop3servercert.pem /etc/stunnel/stunnel.pem
da10~ # chmod 600 /etc/stunnel/stunnel.pem
```

配置 `/etc/stunnel/stunnel.conf` 需要以下条（注意第 58 行和 59 行前的缺失符号）：

```bash
13 #chroot = /var/lib/stunnel/
14 #setuid = stunnel
15 #setgid = nogroup
...
58 [pop3s]
59 accept = 995
60 # connect = 110
   exec = /usr/sbin/popper
   execargs = popper -s
```

在我们的场景中，上述前三行需要一个注释符号。要在更改根目录监狱（jail）中运行 `stunnel`，需要将额外的文件复制到监狱中，以便它仍然能够调用 POP 服务器。此外，`stunnel` 需要以 `root` 身份调用 `pop` 服务器，以便 POP 服务器能够验证密码。

接下来的几行激活了 `POP3S`。端口 `995` 上的连接将移交给 POP 服务器 `popper`（来自 `qpopper` 软件包）。配置文件中的大部分行已经准备就绪。

启动 `stunnel` 后，`stunnel` 接受端口 `995` 上的加密连接，并将解密后的文本交给 `popper`。

然而，当现在使用 `Kmail` 等邮件客户端连接到服务器时，将会出现错误消息：

图 5-1

![](img/ebd0b66532100449f2a48e48fa2ec8ce_209_0.png)

## 选择详细信息显示 Kmail 无法验证服务器提供的证书的有效性。

图 5-2

![](img/ebd0b66532100449f2a48e48fa2ec8ce_210_0.png)

为了验证有效性（以避免连接到声称是目标服务器的虚假站点），需要认证体系中所有 CA 的证书。这些包括根 CA 证书和任何子 CA 的证书。

再次说明，在哪里找到这些证书取决于您如何创建证书颁发机构。使用 `OpenSSL` 命令行界面时，您在创建根 CA 时在 `openssl` 命令中指定了文件名。使用 `YaST CA` 节点模块时，您必须从该模块导出根 CA 证书。

通过选择“加密配置”，然后选择“SSL 签名者和导入”选项卡，即可将 CA 证书导入 `Kmail`：

### 图 5-3

![](img/ebd0b66532100449f2a48e48fa2ec8ce_211_0.png)

导入后，CA 证书将导入 `Kmail` 中。为了验证有效性（以避免连接到声称是目标服务器的虚假站点），需要认证体系中所有 CA 的证书。这些包括根 CA 证书和任何子 CA 的证书。
