
上文使用的 `rm` 命令将删除我们用于编译和安装 GnuPG 的所有源文件。它还将删除来自 `/var/tmp/` 目录的 GnuPG 压缩包。

# 命令

下面列出的命令是我们经常使用的一些，但还有更多。请查看该页面以获取更多细节和信息。

# 创建密钥

首先，如果这是首次使用 GnuPG 软件，我们必须创建一个新的密钥对（公钥和私钥），以便使用其加密功能。

### 第一步

要创建新的密钥对，请使用以下命令：

```bash
[root@deep]## gpg --gen-key
```

```
gpg (GnuPG 1.0.1): Copyright (C) 1999 Free Software Foundation, Inc.

本程序不带任何绝对的保证。

这是一项免费软件，欢迎在某些条件下重新分发。详情请查看 COPYING 文件。

gpg: /root/gnpg/ directory created

gpg: /root/gnpg/options: new options file created

gpg: 你必须重新启动 gpg，以便它能读取新的选项文件
```

它会询问一些问题然后开始生成密钥。

### 第二步

我们使用以下命令再次启动 GnuPG：

```bash
[root@deep]## gpg --gen-key
```

```
gpg (GnuPG 1.0.1): Copyright (C) 1999 Free Software Foundation, Inc.

本程序不带任何绝对的保证。

这是一项免费软件，欢迎在某些条件下重新分发。详情请查看 COPYING 文件。

gpg: /root/gnpg/secring.gpg: keyring created

gpg: /root/gnpg/pubring.gpg: keyring created

请选择你想要的密钥类型：

(1) DSA and ElGamal (默认)

(2) DSA (仅限签名)

(4) ElGamal (签名和加密)

你的选择是？1

DSA 密钥对将具有 1024 位。

生成新的 ELG- 密钥。最小密钥长度为 768 位

默认密钥长度为 1024 位

建议的最大密钥长度为 2048 位

你想要的密钥长度是多少？(1024) 2048

你真的需要大长度吗？y

请求的密钥长度为 2048 位

请指定密钥的有效期。

- 0 = 密钥永不过

- <exp> = 密钥在 n 天后过期

- <w> = 密钥在 n 周后过期

- <m> = 密钥在 n 个月后过期

密钥有效期为？(d) 0

正确吗？(y)? y

你需要 User-ID 来标识你的密钥；软件根据真实姓名、注释和电子邮件地址按如下格式构建用户 ID：

"Heinrich Heine (Der Dichter) <heinrich@duelseldorf.de>"

真实姓名：Gerhard Mourani

电子邮件地址：gmourani@videotron.ca

注释：[按回车]

你选择了此 USER-ID：

"Gerhard Mourani <gmourani@videotron.ca>

更改 (N)、(C)邮箱或 (O)确定/(Q)退出？ 

你需要一个密码语来保护你的机密。

我们正在生成大量的随机字节。在生成质数期间执行其他操作（在键盘上打字、移动鼠标、使用磁盘）是一个好主意；这让随机数生成器有更好的机会获得足够的熵。

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

+

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++<++++......

++++++++AAAA

公钥和私钥已创建并签名。

一个新的密钥对（私钥和公钥）在“root”主目录 (~root) 中创建。
```

# 导入密钥

一旦我们的密钥对创建完成，我们就可以开始将受信任第三方提供的所有密钥放入我们的公钥数据库中，以便在未来的加密和认证通信中使用他/她的密钥。

要为你的密钥库导入公钥，请使用以下命令：

```bash
[root]@deep $ gpg --import <file>
```

```
例如：
[root]@deep $ gpg --import redhat2
gpg: DB42A60E: public key imported
gpg:/root/gnupg/trlusdb created
gpg: 已处理总数: 1
已导入: 1
```

上述命令会将新密钥添加到你的密钥数据库中并更新所有已存在的密钥。需要注意的是，GnuPG 不导入非自签名的密钥。

# 密钥签名

一旦我们的密钥对创建完成，我们就可以开始将受信任第三方提供的所有密钥放入我们的公钥数据库中，以便在未来的加密和认证通信中使用他/她的密钥。

要为你的密钥库导入公钥，请使用以下命令：

```
[root]@deep $ gpg --import <file>
```

```
例如：
[root]@deep $ gpg --import redhat2
gpg: DB42A60E: public key imported
gpg:/root/gnupg/trlusdb created
gpg: 已处理总数: 1
已导入: 1
```

上述命令会将新密钥添加到你的密钥数据库中并更新所有已存在的密钥。需要注意的是，GnuPG 不导入非自签名的密钥。

# 密钥签名

一旦我们的密钥对创建完成，我们就可以开始将受信任第三方提供的所有密钥放入我们的公钥数据库中，以便在未来的加密和认证通信中使用他/她的密钥。

要为你的密钥库导入公钥，请使用以下命令：

```
[root]@deep $ gpg --import <file>
```

```
例如：
[root]@deep $ gpg --import redhat2
gpg: DB42A60E: public key imported
gpg:/root/gnupg/trlusdb created
gpg: 已处理总数: 1
已导入: 1
```

上述命令会将新密钥添加到你的密钥数据库中并更新所有已存在的密钥。需要注意的是，GnuPG 不导入非自签名的密钥。

# 密钥签名

一旦我们的密钥对创建完成，我们就可以开始将受信任第三方提供的所有密钥放入我们的公钥数据库中，以便在未来的加密和认证通信中使用他/她的密钥。

要为你的密钥库导入公钥，请使用以下命令：

```
[root]@deep $ gpg --import <file>
```

```
例如：
[root]@deep $ gpg --import redhat2
gpg: DB42A60E: public key imported
gpg:/root/gnupg/trlusdb created
gpg: 已处理总数: 1
已导入: 1
```

上述命令会将新密钥添加到你的密钥数据库中并更新所有已存在的密钥。需要注意的是，GnuPG 不导入非自签名的密钥。

# 密钥签名

一旦我们的密钥对创建完成，我们就可以开始将受信任第三方提供的所有密钥放入我们的公钥数据库中，以便在未来的加密和认证通信中使用他/她的密钥。

要为你的密钥库导入公钥，请使用以下命令：

```
[root]@deep $ gpg --import <file>
```

```
例如：
[root]@deep $ gpg --import redhat2
gpg: DB42A60E: public key imported
gpg:/root/gnupg/trlusdb created
gpg: 已处理总数: 1
已导入: 1
```

上述命令会将新密钥添加到你的密钥数据库中并更新所有已存在的密钥。需要注意的是，GnuPG 不导入非自签名的密钥。

# 密钥签名

一旦我们的密钥对创建完成，我们就可以开始将受信任第三方提供的所有密钥放入我们的公钥数据库中，以便在未来的加密和认证通信中使用他/她的密钥。

要为你的密钥库导入公钥，请使用以下命令：

```
[root]@deep $ gpg --import <file>
```

```
例如：
[root]@deep $ gpg --import redhat2
gpg: DB42A60E: public key imported
gpg:/root/gnupg/trlusdb created
gpg: 已处理总数: 1
已导入: 1
```

上述命令会将新密钥添加到你的密钥数据库中并更新所有已存在的密钥。需要注意的是，GnuPG 不导入非自签名的密钥。

# 密钥签名
