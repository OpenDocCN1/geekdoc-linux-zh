
一旦上传到服务器，任何人都可以免费下载用户的公钥。

假设两个 GPG 用户 `wduffee` 和 `bcbrown` 想要交换一个加密文件。`wduffee` 持有新创建的密钥；`bcbrown` 将能够使用 `wduffee` 的公钥加密发送给 `wduffee` 的数据。

# 第 5 章

## 172

`bcrown` 可以从密钥服务器下载 `wduffee` 的公钥，或者 `wduffee` 可以将其公钥导出到 `wduffee` 的文件中并相应进行分发。将属于 `userID` 的公钥导出到文件 `key.asc`，可以使用的命令是：

```bash
gpg --output key.asc wduffee
```

`key.asc` 是要导出的文件名，`wduffee` 是创建密钥的 `userID`。这将创建一个 `key.asc` 文件，该文件可以通过 FTP 或电子邮件发送给 `bcbrown`。一旦 `bcbrown` 获得了该文件，他可以使用以下命令将其内容提取到自己的公钥环中：

```bash
gpg --import key.asc
```

`wduffee` 的密钥将进入 `bcbrown` 的公钥环，现在 `bcbrown` 就可以加密数据并发送给 `wduffee`。当然，`wduffee` 也需要获取 `bcbrown` 的公钥，以便解密 `bcbrown` 发送的消息，或向 `bcbrown` 发送加密消息。

为了让 `bcbrown` 加密指定给 `wduffee` 的文件（在本例中名为 `fileToEncrypt`），`bcrown` 应该执行以下命令：

```bash
gpg -se -r wduffee fileToEncrypt
```

在这里，文件 `fileToEncrypt` 正为 `wduffee` 进行加密。在这种情况下，`-s` 选项指示 `gpg` 使用原始者的 `userID` `bbrown` 对文件进行签名；`-e` 选项指示程序加密文件；`-r` 选项接受参数 `wduffee` 以指定 `wduffee` 为接收者。输入此命令后，`bcrown` 必须通过输入密码来验证自己的身份。只有这样 `gpg` 才会执行命令。这将创建一个名为 `fileToEncrypt.gpg` 的文件，该文件只能通过 `wduffee` 的私钥解密。

一旦 `wduffee` 获得了 `fileToEncrypt.gpg`，他必须使用自己的私钥对其解密才能读取。可以使用以下命令完成：

```bash
gpg fileToEncrypt.gpg
```

`wduffee` 将被提示输入他的密码，之后 GPG 将创建一个名为 `fileEncrypt` 的新文件，该文件是 `brown` 意图给 `wduffee` 的原始文件的解密副本。

这是 `gpg` 许多用途之一的示例。另一个用途是为特定用户发送邮件。有许多为 `gpg` 提供 GTK+ 前端的 GUI 程序。以下两个将在后续章节中进行讨论。

### gpg 的 GUI

Gnome PGP (`gpgp`) 是一个提供密钥管理的前端，而 `tkpg` 是一个 TCL/Tk 前端，为 `gpg` 的加密和解密提供了更多选项。

### 应用 173

| 文件 编辑工具 帮助 | | | | | | | | |
|---|---|---|---|---|---|---|---|---|
| 复制 文件 粘贴 全选 撤销 签名 Gpg 加密 解密 检查剪切 | | | | | | | | |
| 编辑器 secring gpg 签名 gpg 活动 | | | | | | | | |
| 新建 属性 删除 导出 | | | | | | | | |
| 类型 | 名称 | 用户 ID | | | | | | | |
| 公钥 | 2000-10-03 | Wesley <wpg1@ra.msstate.edu> | | | | | | | |

图 5.8 `gpgp` 截图。

### gpgp

`gpgp` 可以从 `www.geocities.com/SiliconValley/Chip/3708/gpgp/gpgprintintro.html` 下载。图 5.8 显示了 `gpgp` 的截图。

四个标签页代表 `gpgp` 为操作提供的不同屏幕。`pubring.gpg` 和 `secring.gpg` 标签页调出用户的公钥环和私钥环。每个密钥环都可以通过 `gpgp` 进行添加、删除、导出或修改（假设密钥权限正确）。编辑器屏幕允许输入文本（通过打字或剪切粘贴），然后使用 `gpgp` 动作按钮进行签名和/或加密。

### tkpgp

`tkpgp` 是另一个图形界面，但使用 `gpgp` 时，它提供了不同的功能（见图 5.9）。

通过 `tkpgp`，用户可以指定使用 PGP 或 GPG 加密、使用二进制或 ASCII 文本，以及要执行的各种操作。`tkpgp` 可以读取和写入文件以签名、加密或解密这些文件。在设置（Settings）按钮下可以设置许多选项，如图 5.10 所示。

GnuPG 是专用 PGP 程序的强替代品，允许用户以安全可靠的方式交换数据。更多选项可以在 GnuPG 的 `man 1` 手页中找到，通常位于 `/usr/man/man1/gpg.1.gz`。

# Web 服务器安全

Web 服务器支持的功能和服务数量巨大，极大地促进了互联网的增长和普及。然而，这些功能也为 Web 服务器安全受到破坏提供了可能。对于管理员来说，理解这些 Web 服务器安全被破坏的可能性，并采取适当措施防止此类攻击的发生，以及在此类攻击成功时限制后果是非常重要的。

## 174 第 5 章

![](img/6942796f6e22033d0f94b498c190e5cc_195_0.png)

ASCII 编辑器 ☐ 传统加密 ☐ 替代字体 ◆ GnuPG 自动添加密钥 ■ 加密到默认密钥 ☐ 禁用编辑器 ☐ VPG

图 5.9 `tkpg` 截图。

## 安全

Web 服务器支持的功能和服务数量巨大，极大地促进了互联网的增长和普及。然而，这些功能也为 Web 服务器安全受到破坏提供了可能。对于管理员来说，理解这些 Web 服务器安全被破坏的可能性，并采取适当措施防止此类攻击的发生，以及在此类攻击成功时限制后果是非常重要的。

| 二进制文件 | gpg |
|---|---|
| 列 | gpg |
| 密钥 | gpg |
| Shell | gpg |
| 系统 | gpg |
| 文本 | gpg |
| 应用 | gpg |
| 关闭 | gpg |

图 5.10 `tkpg` 截图。

### 应用 175

Web 服务器支持的功能和服务数量巨大，极大地促进了互联网的增长和普及。然而，这些功能也为 Web 服务器安全受到破坏提供了可能。对于管理员来说，理解这些 Web 服务器安全被破坏的可能性，并采取适当措施防止此类攻击的发生，以及在此类攻击成功时限制后果是非常重要的。

### 安全

Apache 使用 `access.conf` 文件提供了基于主机的访问控制。可以根据该文件的配置允许或拒绝对某些目录、CGI 和其他服务的访问。

#### access.conf

以下是 `access.conf` 文件的可能示例：

```
# access.conf: 全局访问配置
# 默认规则非常严格：
<Directory>
Options None
AllowOverride None
</Directory>
# 功能必须显式允许，因为默认
# 规则不允许任何选项。
# 以下规则可能需要更改，以反映
# 所设置的 DocumentRoot。
<Directory /home/httpd/html>
Options None
AllowOverride None
order allow, deny
allow from all
# #所有人允许查看根 html 目录。
</Directory>
```

```
# 如果位置发生变化，则为脚本别名的 CGI 目录。
<Directory>/usr/local/etc/http/cgi-bin
AllowOverride None
#Options None
Options ExecCGI
</Directory>
```

`access.conf` 配置由多个规则组成，从根目录的默认规则开始。每个单独的规则以 `<Directory [directory]>` 开始，以 `</Directory>` 结束，并可能包含针对该目录及其子目录的特定访问控制指令。此外，某些选项（例如执行 CGI 的能力）可能被允许或拒绝。

#### 访问控制指令

管理员可能希望更改 Web 服务器的默认访问控制指令。表 5.3 列出了可以在目录结构中使用的访问控制指令。

如果管理员想访问除 `lucasdigital.com` 以外的所有地方，指令将显示如下：

```
order deny, allow
allow from all
deny from lucasdigital.com
```
