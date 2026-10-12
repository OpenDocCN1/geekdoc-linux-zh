

Tang 是一个将数据绑定到网络存在状态的服务器。当系统绑定到某个安全网络时，Tang 使包含数据的系统可用。Tang 是无状态的，不需要 TLS 或身份验证。与基于托管的方案不同（在这些方案中，服务器存储所有加密密钥并了解每一个曾使用过的密钥），Tang 从不与任何客户端密钥交互，因此它永远不会从客户端获取任何识别信息。

Clevis 是一个用于自动解密的插拔式框架。在 NBDE 中，Clevis 提供 LUKS 卷的自动解锁功能。clevis 软件包提供该功能的客户端部分。

Clevis Pin 是 Clevis 框架的一个插件。其中一个 PIN 是实现与 NBDE 服务器 – Tang 交互的插件。

Clevis 和 Tang 是通用的客户端和服务器组件，提供网络绑定加密。在 Red Hat Enterprise Linux 7 中，它们与 LUKS 配合使用，通过加密和解密根及非根存储卷来实现网络绑定磁盘加密。

客户端和服务器端组件均使用 José 库来执行加密和解密操作。

当您开始配置 NBDE 时，Tang 服务器的 Clevis Pin 会获取 Tang 服务器广播的非对称密钥列表。或者，由于密钥是非对称的，Tang 的公钥列表可以通过带外分发，以便客户端无需访问 Tang 服务器即可操作。此模式称为离线配置。

Tang 的 Clevis Pin 使用其中一个公钥生成一个唯一的、密码强度高的加密密钥。数据使用此密钥加密后，该密钥即被丢弃。Clevis 客户端应在此配置操作产生的状态存储在方便的位置。此加密数据的过程是配置步骤。NBDE 的配置状态存储在 LUKS 头中，利用 luksmeta 软件包实现。

当客户端准备访问其数据时，它加载配置步骤产生的元数据，并响应以恢复加密密钥。此过程是恢复步骤。

在 NBDE 中，Clevis 使用 PIN 绑定 LUKS 卷，以便它可以被自动解锁。成功完成绑定过程后，可以使用提供的 Dracut 解锁器解锁磁盘。

## 4.10.1. 部署 Tang 服务器

要安装 tang 软件包及其依赖项，请以 root 身份输入以下命令：

```
~]# yum install tang
```

使用 systemd 启用并启动 tangd 服务：

```
~]# systemctl enable tangd.socket --now
Created symlink from /etc/systemd/system/multi-user.target.wants/tangd.socket to /usr/lib/systemd/system/tangd.socket.
```

由于 tangd 使用 systemd 套接字激活机制，服务器会在第一个连接进来时立即启动。在首次启动时会自动生成一组新的密码学密钥。

要执行诸如手动生成密钥等密码学操作，请使用 jose 工具。输入 `jose -h` 命令或参阅 `jose(1)` 手册页以获取更多信息。

### 示例 4.4. 轮换 Tang 密钥

定期轮换密钥非常重要。您应该轮换密钥的具体间隔取决于您的应用、密钥大小以及机构策略。关于一些常见的建议，请参阅密码学密钥长度建议页面。

要轮换密钥，请从在密钥数据库目录（通常是 `/var/db/tang`）中生成新密钥开始。例如，您可以使用以下命令创建新的签名密钥和交换密钥：

```
~]# DB=/var/db/tang
~]# jose jwk gen -i '{"alg":"ES512"}' -o $DB/new_sig.jwk
~]# jose jwk gen -i '{"alg":"ECC"}' -o $DB/new_exc.jwk
```

将旧密钥重命名为以 `.` 开头，以将其从广播中隐藏。请注意，以下示例中的文件名与密钥数据库目录中真实且唯一的文件名不同。

```
~]# mv $DB/old_sig.jwk $DB/.old_sig.jwk
~]# mv $DB/old_exc.jwk $DB/.old_exc.jwk
```

Tang 立即获取所有更改。无需重启。

此时，新的客户端绑定会获取新密钥，而旧客户端可以继续利用旧密钥。当您确信所有旧客户端都使用新密钥时，您可以删除旧密钥。

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_121_0.png)

> **警告**
>
> 请注意，当客户端仍在使用旧密钥时删除旧密钥可能会导致数据丢失。

Tang 使用 80 端口进行通信。此端口也广泛用于 Web 服务器。要更改 Tang 的端口号，请使用标准的 systemd 机制覆盖 `tangd.socket` 单元文件。更多信息请参阅 *Red Hat Enterprise Linux 7 System Administrator's Guide: Creating and Modifying systemd Unit Files*。

### 4.10.1.1. 部署高可用性系统

Tang 提供两种构建高可用性部署的方法：

- 1. **客户端冗余（推荐）**

客户端应配置为能够绑定到多个 Tang 服务器。在此设置中，每个 Tang 服务器都有自己的密钥，客户端能够通过联系这些服务器的一个子集来进行解密。Clevis 已经通过其 `sss` 插件支持此工作流程。

有关此设置的更多信息，请参阅以下手册页：

- `tang(8)`，高可用性部分
- `clevis(1)`，Shamir 的秘密共享部分
- `clevis-encrypt-sss(1)`

Red Hat 推荐此方法用于高可用性部署。

- 2. **密钥共享**

为了冗余目的，可以部署多个 Tang 实例。要设置第二个或后续实例，请安装 tang 软件包，并使用通过 SSH 的 `rsync` 将密钥目录复制到新主机。请注意，Red Hat 不推荐此方法，因为共享密钥会增加密钥泄露的风险，并且需要额外的自动化基础设施。

## 4.10.2. 部署加密客户端

要在具有加密卷的机器（客户端）上安装 Clevis 插拔式框架及其 PIN，请以 root 身份输入以下命令：

```bash
~# yum install clevis
```

要使用 Tang PIN 将明文数据加密为 JSON Web Encryption (JWE) 密文对象，请使用 `clevis encrypt tang` 命令，例如：

```bash
~$ clevis encrypt tang '{"url":"http://tang.srv"}' < PLAINTEXT > JWE
The advertisement contains the following signing keys:
_OsIk0T-E2l6qjfDdIwVm1doZjA
Do you wish to trust these keys? [y/nY] y
```

将前面示例中的 `http://tang.srv` URL 更改为安装了 tang 的服务器 URL。JWE 输出文件包含您的加密密文。此密文从 PLAINTEXT 输入文件中读取。

要解密数据，请使用 `clevis decrypt` 命令并提供密文 (JWE)：

```bash
~]$ clevis decrypt < JWE > PLAINTEXT
```

要了解更多信息，请参阅 **clevis-encrypt-tang(1)** 手册页或使用内置的 CLI 帮助：

```bash
~]$ clevis
Usage: clevis COMMAND [OPTIONS]

clevis decrypt   Decrypts using the policy defined at encryption time
clevis encrypt http Encrypts using a REST HTTP escrow server policy
clevis encrypt sss Encrypts using a Shamir's Secret Sharing policy
clevis encrypt tang Encrypts using a Tang binding server policy
clevis luks bind   Binds a LUKSv1 device using the specified policy
clevis luks unlock  Unlocks a LUKSv1 volume

~]$ clevis decrypt
Usage: clevis decrypt < JWE > PLAINTEXT

Decrypts using the policy defined at encryption time

~]$ clevis encrypt tang
Usage: clevis encrypt tang CONFIG < PLAINTEXT > JWE

Encrypts using a Tang binding server policy

This command uses the following configuration properties:

    url: <string>    The base URL of the Tang server (REQUIRED)

    thp: <string>    The thumbprint of a trusted signing key

    adv: <string>    A filename containing a trusted advertisement
    adv: <object>    A trusted advertisement (raw JSON)

Obtaining the thumbprint of a trusted signing key is easy. If you
have access to the Tang server's database directory, simply do:

    $ jose jwk thp -i $DBDIR/$SIG.jwk

Alternatively, if you have certainty that your network connection
is not compromised (not likely), you can download the advertisement
yourself using:

    $ curl -f $URL/adv > adv.jws
```

## 4.10.3. 配置根卷的手动注册

要自动解锁现有的 LUKS 加密根卷，请安装 **clevis-luks** 子软件包，并使用 **clevis luks bind** 命令将卷绑定到 Tang 服务器：

```bash
~]# yum install clevis-luks
```

```bash
~]# clevis luks bind -d /dev/sda tang '{"url":"http://tang.srv"}'
The advertisement contains the following signing keys:
```

