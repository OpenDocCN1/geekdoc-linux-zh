
如果你需要从源码编译 SSL，请遵循软件包自带的说明。通常，你必须运行 `configure` 脚本，然后运行 `make` 和 `make install`。

> 提示 我遇到过与 Samba 配合得不好的 二进制文件。在 Samba 配置阶段，配置脚本报错说无法创建摘要。将其替换为 OpenSSL 二进制文件或在同一系统中从源码编译的 SSLay 版本解决了这个问题。如果你在编译 SSL 的 Samba 时遇到困难，请尝试将 SSL 软件包替换另一个。

## 基础 SSL 配置

基础 SSL 配置涉及告诉 SSL 在何处找到密钥文件，并设置程序以便其轻松运行。请以 root 身份执行以下配置步骤：

1. 设置二进制文件使其可以在你的路径中访问。如果你是从 RPM 或 Debian 软件包安装的程序，你可能需要将二进制文件路径添加到 `PATH` 环境变量中。你可以通过编辑 `/etc/profile` 来调整此系统级设置。或者，你可以在路径上的某个目录（如 `/usr/local/bin/`）中创建一个名为 `sslay` 的链接，指向你特定目录中的二进制文件（`sslay` 或 `openssl`）。
2. SSL 依赖随机数来实现安全性。为了给 SSL 的随机生成器初始化，你需要创建一个包含随机字符的文件。为此，输入命令：

```bash
# cat > /tmp/private.txt
```

然后随机输入字符一分钟或以上。完成后，按 `Ctrl+D` 停止输入。结果将是一个名为 `/tmp/private.txt` 的文件。
3. 将你创建的 `/tmp/private.txt` 文件转换为 SSL 可用的格式。为此，输入命令：

```bash
# sslay genrsa -rand /tmp/private.txt > /dev/null
```

结果是基于 `/tmp/private.txt` 的名为 `.rnd` 的文件。
4. 创建一个 SSL 存储证书的目录。一个良好的选择是 `/etc/certificates`。创建后，务必使用 `chmod` 限制对该目录的访问，如 `chmod 0700 /etc/certificates`。
5. 编辑 `/var/ss1/misc/CA` 文件（如果你构建了 SSL 或使用 OpenSSL，此文件可能位于其他目录）。找到定义 `CATOP` 的行，它名为 `CATOP=./demoCA`。将此行改为 `CATOP=/etc/certificates`。
6. 编辑 `/var/ss1/misc.cnf` 文件。找到 `dirs = ./demoCA` 条目并将其改为 `dir = /etc/certificates`。

这些步骤为下文创建证书奠定了基础。这些证书有助于计算机之间进行身份验证，但它们不能取代通常的密码机制。

## 创建证书

通常，SSL 与由证书颁发机构 `CA` 发的证书一起。CA 的“批准章”保证了某个 Web 零售商例如确实是它所声称的实体，而不是冒充者。在大多数 SSL 配置中，你不需要外部 CA 来提供这种保证；你可以生成自己的证书并充当自己的 CA。这种安排对于 Samba 和 SSL 的内部使用是足够了。如果你运行安全网站，你可能会注册 CA。你可以在基于 SSL 的 Samba 上这些注册。

### 创建 CA 配置

创建证书的第一步是运行证书设置脚本 `CA.sh`。如果你是从 OpenSSL RPM 文件安装的 SSL，此脚本位于 `/var/ss1/misc` 目录。列表 14.1 显示运行此脚本的结果。你将被要求输入识别你和你组织的信息。你输入的口令类似于密码，但应该比典型的密码长得多。

### 列表 14.1 运行证书颁发机构脚本的结果

```
# /var/ssl/misc/CA.sh -newca
mkdir: cannot make directory '/etc/certificates': File exists
CA certificate filename (or enter to create)
```

正在 CA 证书 ...
正在使用配置 `/var/ssl/openssl.cnf`
正在生成 1024 位 RSA 私钥

...... 正在写入新私钥 `/etc/certificates/private/.cakey.pem`
Enter PEM pass phrase:
Verifying password - Enter PEM pass phrase:

你即将输入的信息将被整合到
你的证书请求中。
你即将输入的内容被称为 Distinguished名称（Distinguished Name，简称 DN）。
有几个字段你可以留空。
某些字段会有默认值，
如果你输入 '.'，则该字段将留空。

- 国家名称（2位代码） [AU]:US
- 州或省名称（全称） [Some-State]:Massachusetts
- 所在地名称（例如，城市） [:Malden
- 组织名称（例如，公司） [Internet Widgets Pty Ltd]:The Panther School
- 组织单位名称（例如，部门） [:None
- 通用名称（例如，你的名字） [:clouseau.panther.edu
- 电子邮件地址 [:]:jacques@panther.edu

你输入的大部分细节（如组织名称）并不重要。默认情况下，客户端和服务器必须包含国家代码、州和组织名称名称。（接下来的章节“创建客户端证书”将描述客户端证书的这些信息）。

正如 `CA.sh` 输出早期所示所示，该脚本会创建一个文件 `/etc/certificates/private/cakey.pem`。这是一个高度敏感的私钥文件，因此不要将其复制到其他系统上。

### 创建客户端证书

下一步是为客户端创建证书文件。如果你不打算使用客户端证书，可以跳过此步骤。尽管如此，客户端证书可以提供额外的安全组件，我建议你使用它们。假设你要通过 SSL 连接到服务器的客户端名为 `SIMONE`。为了避免混淆，你可以根据客户端名称创建证书的文件名。首先，你使用 `openssl` 程序创建一个名为 `simone.key` 的文件：

```
# openssl genrsa -des3 1024 >simone.key
```

正在生成 RSA 私钥，模数长度 1024 位

+++++
....................
+++++

e is 65537 (0x10001)

Enter PEM pass phrase:
Verifying password - Enter PEM pass phrase:

注意，创建 `simone.key` 文件需要你输入短语，就像你创建 `cakey.pem` 文件时一样。此短语不应与用于服务器的短语相同。

你现在必须创建一个临时客户端文件，如下：

```
# openssl req -new -key simone.key -out simone-csr
```

正在使用配置 `/var/ssl/openssl.cnf`

Enter PEM pass phrase:
你输入的短语是给客户端的，而不是服务器的。你只需要输入一次，因为它是用于身份验证的，而不是为了更改或最初创建该短语。此时，你必须再次输入列表 14.1 中的组织信息，但这次，你应该以适合客户端的方式进行回答。

你现在必须使用你的 CA 配置来“签名”客户端证书。这将允许服务器验证客户端已批准连接到服务器。要此此，你使用 `openssl`：

```
# openssl ca -days 1000 -infiles simone-csr >simone.pem
```

正在使用配置 `/var/ssl/openssl.cnf`

Enter PEM pass phrase:
Checking request certificate with signature
Signature ok

要对客户端证书签名，你需要输入服务器的短语。与其他短语输入一样，这些信息不会回显到屏幕上。程序将继续显示你输入的关于客户端证书的信息。如果一切顺利，程序会询问你是否要对证书签名。输入 `y` 响应。在提交更改到服务器证书数据库（位于 `/etc/certificates` 中）之前，程序会再次请求确认。再次响应 `y`。程序最后通过确认已写入更改来结束。

如果程序不是请求这些确认，反而是抱怨数据不匹配（例如，如果客户端和服务器的州不匹配），那么你应该检查你的服务器配置并根据需要进行更改。

> **注意** 你在创建证书时指定了证书的有效天数。在上一个示例中，它是 `-days 1000` 参数。在该时间结束时，你需要生成一个新证书。

此证书创建过程的结果如下：

- 在服务器的 SSL 数据库（位于 `/etc/certificates` 目录）中创建了一个条目。你不需要担心此条目的细节，除非为了确保它免受损坏、篡改或未经授权的访问。
- 创建了两个文件（示例中的 `smb.key` 和 `smb.pen`），你最终将它们传输到服务器。这些文件非常敏感；有了它们，客户端就能通过验证，不法之徒可能会访问你的服务器。因此，你应该以最安全的方式传输这些文件——例如通过软盘交付。

我建议你为服务器生成客户端证书。这将允许你使用 `smbcclient` 连接本地计算机来测试服务器配置。

有了这些证书，你现在将配置 Samba 使用 SSL，并在你的系统上设置 SSL。

## 配置 Samba 使用 SSL

在使用 Samba 之前，你必须配置启用 SSL 的服务器版本。遗憾的是，许多 Linux 发行版的 Samba 并不支持 SSL。（Red Hat 7.0 是例外，未来可能会更多例外）。一旦你带有 SSL 支持重新编译 Samba（并安装了 SSL 软件包），基本的 SSL 功能只需在 `smb.conf` 中设置参数。然后你可以使用 `smbcclient` 连接自身来测试基本功能。

### 创建启用 SSL 的 Samba

你可能需要编译一个启用了 SSL 支持的 Samba 副本。如果你不确定此要求，请跳到“设置 Samba 的”

### Samba 的 SSL

#### SSL 参数

Samba 包含了大量的 SSL 相关参数。你可以使用其中几个参数来配置基本的启用 SSL 的服务器，包括以下：

- `ssl` 此布尔参数启用或禁用 SSL 支持。默认值为 No，因此你必须将此参数设置为 Yes 以允许 SSL 连接。
- `ssl server cert` 此参数接受 SSL 证书文件的完整路径。如果你使用 `/etc/certificates` 作为 SSL 证书目录，那么你应该使用 `ssl server cert = /etc/certificates/cacert.pem`。没有默认值。
- `ssl server key` 你在此目录中指定服务器自己的密钥文件的位置。如果你按照本章指定的配置了服务器，那么相应的设置为 `ssl server key = /etc/certificates/private/cakey.pem`。此参数没有默认值。

上述三个参数足以启用基本的 SSL 服务器配置，但这种配置仅支持加密而不证书。要使用证书，你必须设置以下附加选项：

- `ssl ca certfile` 此参数指定所有受信任 CA 证书的位置。在小型服务器上，此文件可能只包含一个 CA 的信息。要使用证书，你必须使用此参数或 `ssl ca certdir` 参数（但两者不同具备）。如果你已经按照前面“基础 SSL 配置”中的描述配置了 SSL，则应将此参数指向 `/etc/certificates/cacert.pem`。该参数没有默认值。

`ssl ca certdir` 此参数指定 SSL CA 证书目录的位置。该目录的作用类似于 SSL 证书文件，但每个 CA 在目录中都有其独立的文件。虽然如果你只有几个 CA，设置起来工作量会稍大一些，但如果你使用大量的 CA，这种方式可能更合适。该参数没有默认值。

`ssl client cert` 此参数指定 SSL 客户端证书文件的位置，例如前面在“创建客户端证书”中描述的 `smbclient` 文件。`smbcclient` 在连接到启用 SSL 的服务器时会使用此文件。该文件必须位于任何使用 `smbcclient` 的用户可读的目录中。如果你想作为客户端使用证书，必须设置此选项。

**警告** 尽管客户端证书文件可能被任何使用 SSL 连接的用户读取，但该文件仍然具有敏感性，因此你应该根据其可用性对其进行保护。你可能想要创建一个可以读取该文件的 SSL 用户组，以限制其他用户的访问。

`ssl client key` 此参数指定 SSL 客户端密钥文件的位置，例如“创建客户端证书”中描述的 `smbclient`。如果你想将计算机作为带有证书的客户端，则需要此选项。此密钥应通过将其放置在仅 root 可读的目录中来保护。

`ssl require clientcert` 此布尔参数决定 Samba 作为服务器时是否接受缺少证书的客户端连接。默认值为 No（否），这意味着服务器不需要客户端证书。此类连接是加密的，但仍有可能来自未经授权源的风险。

`ssl servercert` 此布尔参数决定 `smbcclient` 是否连接到没有认证的服务器。在启用 `ssl require clientcert` 的情况下，默认值为 No（否），这开启了连接的加密，但并不能保证服务器的身份。

Samba 支持许多额外的 SSL 特性，其中一些需要配置。你可能希望使用以下一个或选项来扩展和精调你的配置：

`ssl hosts` 此参数允许你指定必须使用 SSL 连接服务器的客户端。它接受计算机名称或 IP 地址列表作为值，使用本章开头“限制计算机访问”中描述的 `allow` 和 `deny` 参数。如果使用了 `hosts` 参数且 `ssl hosts = Yes`，Samba 要求所有连接都通过 SSL 进行。

`hosts` 此参数是 `hosts` 的反反；它指定不使用 SSL 连接服务器的客户端列表。如果你只要求通过路由器到达的连接，可以设置此参数。你可以指定本地网络的 IP 地址以免它们使用 SSL。

`ssl ciphers` 你可以指定 Samba 在协商时使用的加密算法（即加密方案）。可能的值有 `DEFAULT`、`DES-CFB-NULL`、`DES-RC4`、`EXP-RC4`、`EXP-DES-CBC`、`IDEA-DES-CBC`、`DES-CBC-SHA`、`DES-CBC-SHA-RC4`。除非你是 SSL 专家，否则我建议不要调整此参数。

`ssl version` 此参数指定 Samba 尝试使用的 SSL 协议版本。默认值为 `ssl23`，表示接受 2 和 3。如有，你可以将此参数设置为 `tls`、`tls1.2` 或 `tls1.3`。

`ssl compatibility` 此参数配置 Samba 使用旧版本的 SSL 实现。默认值为 `no`（否），你不需要更改它。

如果你的服务器接受 SSL 加密和未加密的连接，你可能需要设置 `hosts` 或 `hosts` 参数。后者更安全，因为它对某些连接设置了异常，而不是要求所有连接都使用 SSL。这些参数的其余部分是你可能不需要调整的。

## 测试 Samba SSL 功能

测试 Samba SSL 功能的最简单方法是根据“设置 Samba”中描述的三个必要参数加上你的 SSL 配置参数来配置 SSL。然后你必须重启 Samba 守护进程。当你启动 `samba` 时，输入服务器密码。如果没有被要求输入密码，说明你没有使用 SSL 版本的 Samba。

一旦 Samba 运行，使用 Samba 包中的 `smbclient` 程序连接本地计算机。例如，如果 Samba 运行在 `clousse` 上，你可能会输入 `smbclient //clouseau/shares`。如果一切顺利，`smbclient` 会提示客户端密码。之后，`smbclient` 会提示你的用户密码。在此过程中，Samba 组件会报告了哪种 SSL 加密方法（或算法）。

> 警告 如果 SSL 报告使用 `NULL`，意味着你的数据没有加密。你应该检查你的设置，特别是 `ssl cipher` 参数。

如果 SSL 报错，请检查你的设置。

## 配置客户端使用 SSL

在“设置 Samba”中讨论的一些选项控制客户端。如果你使用的是 Windows，实现该功能要困难得多。有两种方法：运行单独的代理，或者在客户端本身上运行代理。SSL Proxy 提供的 Windows 二进制文件包含单独的 `.EXE` 和 `.DLL` 文件。

> 警告 SSL Proxy 的 Windows 二进制文件包含单独的 `.EXE` 和 `.DLL` 文件。遗憾的是，Windows 在下载时会损坏 `.DLL` 文件。

## 使用代理服务器

正如我所描述的，代理占用 TCP 端口 `139`，该端口通常由 `smbd` 和 Windows 的 SMB/CIFS 实现。这意味着在代理服务器服务器使用普通的 SMB/CIFS 工具。如果你必须在 Linux 服务器上运行 Samba，可以在代理服务器上运行不带 `smbd` 的 `nmbd` 来解决这个问题。

## Samba over SSL

多个代理服务器支持 SMB/CIFS。流行的选择有 SSL Proxy (`http://obdev.at/sslproxy.html`) 和 Stunnel (`http://www.stunnel.org/`)。这两个包适用于 Windows 和 Unix。对于 Linux，你可以编译源码。

例如，考虑 SSL Proxy。一旦你有了二进制文件和客户端文件，可以如下运行它：

```
# sslproxy -l 139 -R server -r 139 -n -c cert.pem -k cert.key
```
