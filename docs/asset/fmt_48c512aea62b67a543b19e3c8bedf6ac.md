
The same is true for pipes. The first command (shown next) prints the list of files on the local system’s printer. The standard output is piped to your own line printer. In the second command, the list of files is printed on the remote system’s printer. The pipe is quoted and evaluated by the remote system, piping the standard output to the printer on the remote system.

```
$ ssh violet ls /home/robert | lpr
$ ssh violet ls /home/robert '|' lpr
```

> Note The Kerberos version of the remote commands also let you specify Kerberos realms and credentials.

| Remote Command | Effect |
|---|---|
| `rwho` | Displays all users logged into systems in your network. |
| `ruptime` | Displays information about each system on your network. |
| `rlogin system-name` | Allows you to log in remotely to an account on another system. |
| `-l` | Allows you to specify the login name of the account. |
| `alogin system-name` | Secure login to an account on another system. |
| `rcp sys:name:file1 sys:name:file2` | Allows you to copy a file from an account on one system to an account on another system. With the `-p` option, preserves the modification times and modes of source files. |
| `scp sys:name:file1 sys:name:file2` | Secure copy of a file from an account on one system to an account on another system. |
| `rsh sys-name Linux-command` | Allows you to remotely execute a command on another system. `-l` allows you to specify the login name. `-n` redirects input from the null special device, `/dev/null`. |
| `ssh sys-name Linux-command` | Secure remote execution of a command on another system. |

## TABLE 15-3 Remote Access Commands

## 安全

## PART

- CHAPTER 16
- 加密、完整性检查和签名。GNU Privacy Guard
- CHAPTER 17
- Internet Protocol Security: IPsec
- CHAPTER 18
- Secure Shell and Kerberos
- CHAPTER 19
- Network Firewalls: Netfilter

## 加密、完整性检查和签名：GNU Privacy Guard

你可以使用加密、完整性检查和数字签名来保护通过网络传输的数据。例如，GNU Privacy Guard 加密软件包让你可以加密你要发送的电子邮件或文件，同时也可以用加密的数字签名对其进行签名，以证明该消息确实由你发送。数字签名还包含加密的修改摘要信息，提供完整性检查，使接收者能够验证收到的消息是原始消息，而不是被更改或替换过的。

### 公钥加密、完整性检查和数字签名

加密数据是确保通过网络传输的数据安全的唯一可靠方法。用密钥加密数据，接收者随后可以对其进行解密。为了充分保护通过网络传输的数据，你不仅应对其进行加密，还应检查其是否未被修改，并确认其确实由声称的作者创建。加密的消息仍可能被截获并修改，然后重新加密。诸如修改摘要之类的完整性检查可确保数据未被篡改。虽然加密和完整性检查可以保护数据，但它们并不能对其进行身份验证。你还需要知道声称发送消息的人确实是发送者，而不是冒名顶替者。为了对消息进行身份验证，作者可以使用数字签名对其进行签名。此签名也可以被加密，使接收者能够验证其真实性。数字签名可确保你收到的消息是真实的。

### 公钥加密

加密使用密钥以这样的方式加密数据，即相应的密钥可以对其进行解密。过去，旧的加密形式使用相同的密钥来加密和解密消息。然而，这涉及向接收者提供密钥，从而使任何获得密钥的人都可以解密数据。公钥加密使用两个密钥来加密和解密消息，即私钥和公钥。私钥你始终保留并用于解密收到的消息。公钥你向你要发送消息的人公开。他们随后使用你的公钥来加密他们想要发送给你的任何消息。私钥用于解密消息，公钥用于加密它们。每个用户都有一组私钥和公钥。反过来，如果你想向另一用户发送消息，你将首先获取该用户的公钥并使用它来加密你要发送给该用户的消息。然后用户用自己的私钥解密消息。换句话说，你的公钥由其他人用来加密他们发送给你的消息，而你使用其他用户的公钥来加密你发送给他们的消息。你的 Linux 系统上的每个用户都可以拥有自己的公钥和私钥。他们将使用 `gpg` 程序生成它们并将其私钥保存在自己的目录中。

### 数字签名

数字签名用于同时对消息进行身份验证并提供完整性检查。身份验证保证消息未被修改——它是你发送的原始消息——完整性检查验证其是否未被更改。虽然数字签名通常与加密消息结合使用以提供更高级别的安全性，但也可以将其用于可以明文发送的消息。例如，你会想知道 Red Hat 版本的升级公告是否确实由 Red Hat 发送，而不是由试图制造混乱的人发送。这样的消息仍然需要经过身份验证，检查其是否确实由发送者发送，或者如果由原始发送者发送，是否在传输过程中以某种方式被更改。这种验证可防止冒充发送者的人篡改或替换消息。

### 完整性检查

对消息进行数字签名涉及使用 `MD5` 修改摘要算法等加密算法从消息内容生成校验和值。这是唯一准确表示消息大小和内容的数值。对消息进行任何更改都会生成不同的值。此值提供了一种检查数据完整性的方法。然后用你的私钥对 `MD5` 值本身进行加密。当用户收到你的消息时，他们会用你的公钥解密你的数字签名。然后用户生成收到的消息的 `MD5` 值并将其与你发送的 `MD5` 值进行比较。如果它们相同，则消息经过身份验证——它是你发送的原始消息，而不是冒充你发送的虚假消息。用户可以使用 `GnuPG` 来解密和检查数字签名。

### 结合加密和签名

通常，数字签名与加密结合使用以提供更安全的传输级别。消息将使用接收者的公钥进行加密，数字签名将使用你的私钥进行加密。用户将用自己的私钥解密消息，然后用你的公钥解密签名。然后他们将签名与用户从消息生成的签名进行比较以对其进行身份验证。当 `GnuPG` 解码消息时，它也会自动解码并检查数字签名。图 16-1 显示了加密和数字签名消息的过程。

## GNU隐私卫士

为了保护您通过电子邮件发送的消息，大多数 Linux 发行版提供了 GNU隐私卫士（`GnuPG`）加密和身份验证功能。`GnuPG` 是 GNU 开源软件，其工作原理与良好隐私（`PGP`）加密非常相似。使用 `GnuPG`，您既可以加密消息，也可以对其进行数字签名——从而保护消息并验证其来自您。目前，Evolution 和 KMail 都支持 `GnuPG` 加密和身份验证。在 Evolution 中，您可以从“安全”菜单选择 PGP 加密和签名来使用 `GnuPG`（在 Red Hat Linux 中，PGP 选项即使用 `GnuPG`）。在 KMail 中，您可以在“选项”窗口的“安全”面板中选择要使用的加密方式。
