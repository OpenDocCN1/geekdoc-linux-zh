
你的`/dev/mouse`别名应该已经为其使用的端口设置好了。对于串行鼠标，这通常是`COM1`端口`/dev/ttyS0`。如果别名未设置或你需要更改它，可以使用`ln -s`命令。以下示例为第一个串口`/dev/ttyS0`设置了`/dev/mouse`别名：

```bash
ln -s /dev/ttyS0 /dev/mouse
```

## 第6章：安全配置

网络安全的良好基础是设置 Linux 系统作为网络的防火墙运行，保护其免受未经授权的访问。你可以使用防火墙来实现包过滤或代理。包过滤简单来说就是判断防火墙接收到的数据包是否应该进入本地网络的过程。它检查数据包的地址，如果允许，则发送数据包。当前使用的防火墙是`Netfilter`（`iptables`）。较旧的发行版为我们提供了一个名为`ipchains`的早期版本。若要实现防火墙，只需提供一系列规则来管理你想在系统上允许的任何访问。如果该系统是私有网络的网关，系统的防火墙可以有效保护网络免受攻击。

保护系统访问的另一种方法是提供安全的用户身份验证、轻量级目录协议（`LDAP`）和可插拔认证模块（`PAM`）。这些将在第6章中详细讨论。

为了保护来自网络外部主机的远程连接，可以对传输进行加密。对于 Linux 系统，你可以使用`Secure Shell`（`SSH`）软件套件加密任何传输，防止其被他人读取。如果你不使用`SSH`，最好避免使用`telnet`和`rcp`（见第21章）等标准工具通过互联网进行远程访问。外部用户还可能尝试通过任何服务（如网站）获得未经授权的访问。在这种情况下，你可以设置代理来保护你的网站（见第24章）。

### 常用安全工具概览

| 应用 | 描述 | 网站 |
| :--- | :--- | :--- |
| `GNU Privacy Guard` (`GPG`) | 加密和数字签名 (第6章) | www.gnupg.org |
| `Tripwire` | 入侵检测 (第6章) | www.tripwire.org |
| `Netfilter` (`iptables` and `ipchains`) | 防火墙包过滤 (第37章) | www.samba.org |
| `Squid` | Web 代理服务器 (第24章) | www.squid-cache.org |
| `SSH` | 用于远程访问的安全 Shell 加密 (第37章) | www.ssh.org |
| `Kerberos` | 用于远程访问的认证 (第37章) | www.mit.edu |
| `Pluggable Authentication Modules` (`PAM`) | 身份验证 (第27章) | www.kernel.org |
| `Lightweight Directory Protocol` (`LDAP`) | 身份验证 (第27章) | www.ldap.org |
| `Shadow` | 密码 (第27章) | www.linux-security.org |

## GNU Privacy Guard (GPG)：加密与认证

为了保护来自网络外部主机的远程连接，可以对传输进行加密。对于 Linux 系统，你可以使用`Secure Shell`（`SSH`）软件套件加密任何传输，防止其被他人读取。如果你不使用`SSH`，最好避免使用`telnet`和`rcp`（见第21章）等标准工具通过互联网进行远程访问。外部用户还可能尝试通过任何服务（如网站）获得未经授权的访问。在这种情况下，你可以设置代理来保护你的网站（见第24章）。

*(注：原文内容在表格前后存在重复，此处已合并去重)*

![](img/95726952b50a5b7113b49b7e63a39779_129_0.png)

图 6-1. 公钥加密与数字签名

### GPG 命令

#### 常用选项

- `-s`, `--sign`: 对文档进行签名，创建一个签名。可以与`--encrypt`结合。
- `--clearsign`: 创建明文签名。
- `-b`, `--detach-sign`: 创建分离签名。
- `-e`, `--encrypt`: 加密数据。可以与`--sign`结合。

#### 表 6-2. GPG 命令与选项

| GPG 命令 | Description |
|--- | --- |
| `--decrypt` `[file]` | 解密文件（若未指定文件，则使用`stdin`）并将其写入`stdout`（或使用`--output`指定的文件）。如果解密后的文件经过签名，则会验证签名。 |
| `--verify` `[sigfile]` `[signed-files]` | 验证已签名的文件。签名可以包含在文件中，也可以是一个独立的分离签名文件。 |
| `--list-keys` `[names]` | 列出密钥库中的所有密钥或指定的。 |
| `--list-public-keys` `[names]` | 列出公钥库中的所有密钥或指定的。 |
| `--list-secret-keys` `[names]` | 列出你的私钥（秘密密钥）。 |
| `--list-sigs` `[names]` | 列出你的密钥以及它们具有任何签名。 |
| `--check-sigs` `[names]` | 列出密钥及其签名并验证签名。 |
| `--fingerprint` `[names]` | 列出指定密钥的指纹。 |
| `--gen-key` | 生成一组新的私钥和公钥。 |
| `--edit-key` `name` | 编辑你的密钥。使用命令执行大多数密钥操作，如签名密钥或使用`passwd`更改口令。 |
| `--sign-key` `name` | 使用你的私钥对公钥进行签名。等同于`--edit-key`中的`sign`。 |
| `--delete-key` `name` | 从公钥库中移除公钥。 |
| `--delete-secret-key` `name` | 从私钥库和公钥库中同时移除私钥和公钥。 |
| `--gen-revoke` | 为自己的密钥生成撤销证书。 |

#### 表 6-2. GPG 命令与选项（续）

| GPG 命令 | Description |
| --- | --- |
| `--export` `[names]` | 从你的密钥库中导出指定的密钥。不带参数时，导出所有密钥。 |
| `--send-keys` `[names]` | 导出并将指定的密钥发送到密钥服务器。必须使用`--keyserver`选项提供该服务器的名称。 |
| `--import` `[files]` | 将文件中包含的密钥导入你的公钥库。 |

#### GPG 通用选项

| GPG 选项 | Description |
| --- | --- |
| `-a`, `--armor` | 创建 `ASCII` 输出，即加密数据的 `ASCII` 版本。 |
| `-o`, `--output` `file` | 将输出写入指定的文件。 |
| `--default-key` `name` | 指定用于签名的默认私钥。 |
| `--keyserver` `site` | 用于查找不在你密钥库中的公钥的密钥服务器。也可以指定将你的公钥发送到那里。 |
| `-r`, `--recipient` `names` | 使用指定用户的公钥为该用户加密数据。 |
