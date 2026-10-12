
```
[root@demo2]# openssl req -x509 -new -nodes -utf8 -sha512 -days 3650 -batch -config /etc/ssl/x509.conf -form DER -out /etc/ssl/certs/pubkey.der -keyout /etc/ssl/certs/priv.key
Generating RSA private key
****
****
writing new private key to '/etc/ssl/certs/priv.key'
[root@demo2]#
```

此签名证书有效期为 10 年（3650 天）。确保密钥得到充分保护。可以通过将密钥离开服务器并存储在安全位置来实现。将密钥放在 U 盘并放在抽屉里并不是安全位置。锁锁的位置，例如保险箱。

```
[root@demo2]# openssl x509 -inform DER -in /etc/ssl/certs/pubkey.der -out /etc/ssl/certs/pubkey.pem
[root@demo2]#
```

## 签名模块

`sign-file` 实用工具确保模块对内核进行了正确签名。该工具位于内核源码内部。以下指令假设你正在为当前运行的内核签名模块。如果你打算为不同的内核签名模块，必须提供正确内核版本源码中 `sign-file` 实用工具的路径。如果你不使用正确的工具，模块的签名类型可能与预期的签名类型不匹配。

要签名模块，请运行当前运行内核的 `sign-file` 实用工具，并提供你为签名模块创建的私钥和公钥路径（例如，我使用名为 `hello` 的模块）：

```
[root@demo2]# sudo /usr/src/kernels/$(uname -r)/scripts/sign-file sha512 /etc/ssl/certs/priv.key /etc/ssl/certs/pubkey.der /lib/modules/$(uname -r)/extra/hello.ko
```

注意模块应该安装到 `/lib/modules/`，你需要提供模块的正确路径。

## 更新所有者密钥数据库

机器所有者密钥 `MOK` 是一种安全功能，旨在保护计算机系统的启动过程免受未经的修改或攻击。它通常用于支持 UEFI 和安全启动的系统，这些系统要求所有引导加载程序和内核模块都由受信任实体签名。

`MOK` 数据库存储在系统固件内的非易失性内存位置，包含允许对引导加载程序和内核模块签名的密钥列表。`MOK` 数据库中的每个密钥都与唯一标识符关联，并用于验证引导加载程序和内核模块的数字签名。如果数字签名无效，启动将继续但软件不会加载；启动将停止且系统不会启动。

要注册 `MOK` 密钥，你必须在每个目标系统上使用 UEFI 系统控制台手动进行。

由于你创建的密钥未包含在 UEFI 安全启动数据库中，你需要使用 `mokutil` 命令在 shim 中向 `MOK` 数据库注册：

`mokutil --import /etc/ssl/certs/pubkey.der`

上一个命令会提示你输入一个一次性密码，你将在重启系统后，`MOK` 管理服务注册密钥时使用该密码。

## 重启系统

- 1. UEFI 应该在启动时自动启动 shim UEFI 密钥管理器，如下图所示。如果你在 10 秒内没有按下任何键，你将无法注册你的 `MOK` 密钥：

![](img/110fa0d6324f0893fff03cee6394144d_111_0.png)

图 3.11 - Shim 实用程序

按任意键继续。

- 2. 随后，你将看到 shim 主菜单。从菜单中选择 Enroll MOK（注册 MOK）。

![](img/110fa0d6324f0893fff03cee6394144d_111_1.png)

图 3.12 – Shim 主菜单

这将允许你继续注册密钥或查看密钥。

- 3. 从菜单中选择 View key 0（查看密钥 0）（如下所示）以显示密钥详情。

![](img/110fa0d6324f0893fff03cee6394144d_112_0.png)

图 3.13 – 查看密钥

- 4. 随后将显示密钥详情。验证所展示的值是否与你用于签名模块并插入内核映像的密钥相匹配：

图 3.14 – 密钥详情

然后按任意键返回 Enroll MOK 菜单。

- 5. 从菜单中选择 Continue（继续）。

- 6. 将显示 Enroll the key(s)?（注册密钥？）屏幕，你现在可以从菜单中选择 Yes（是）（如下图所示）。

![](img/110fa0d6324f0893fff03cee6394144d_113_0.png)

图 3.15 – 注册密钥

选择 Yes 以注册密钥。

- 7. 系统将提示你输入密码。输入你使用 `mokutil` 命令导入密钥时使用的密码。

密钥已注册到 UEFI Secure Boot 密钥数据库。

- 8. 你现在被重定向到主菜单。从菜单中选择 Reboot（重启）。

![](img/110fa0d6324f0893fff03cee6394144d_113_1.png)

图 3.16 – 完成后重启

# 工作原理

启动系统后，你可以验证某个密钥是否包含在相应的内核密钥环（keyringing）中。验证取决于你正在运行的内核版本。此外，你需要检查的密钥名称也所不同，因为实现方式随着内核版本的变化而变化。

如果为自定义模块生成的密钥列在正确的密钥环中，你就可以可以在 Secure Boot（安全启动）模式下加载由该密钥签名的模块。

对于 Oracle Linux 8 上的 RHCK 以及 UEK R6 或更高版本的内核，`built_trusted_keys` 密钥环和 `platform` 密钥环中的密钥对于模块签名和 kexec 文本都是受信任的，这意味着我们可以按照标准程序为密钥环中的密钥对在 `MOK` 数据库中签名模块，并且它会被自动信任。

由于密钥被加载到 `builtin_trusted_keys` 密钥环中，你应该同时检查两个密钥环的模块签名。以下是一个示例：

```
[root@demos2 ~]# keyctl show %:builtin_trusted_keys
Keyring
718980521--swrv 0 0 keyring: .builtin_trusted_keys
895270521--swrv 0 0 asymmetric: Oracle CA Server
235653a3b7ec77a9b0526a411c5a5a5d7
643918572--swrv 0 0 asymmetric: Oracle IMA signing CA:
a2ef2897a05948027f1d4904ae1e8e46e4651
668b1900--swrv 0 0 asymmetric: Oracle America, Inc.: Ksplice Kernel Module Key: 09901d06f5a4f5c5b2ef251e8277b5ee4c
35441076--swrv 0 0 asymmetric: Oracle Linux Signing Key: 3b55241296a269a3f5be026173de8e53f
[root@demos2 ~]# keyctl show %:platform
85804605--swrv 0 0 keyring: .platform
88615021--swrv 0 0 asymmetric: Oracle America, Inc.: 43c0d551c25357b8c44edcf5d49263
69874825--swrv 0 0 asymmetric: Oracle America, Inc.: 2e7c7201d5cd5f254c93deca7ae5f96c0f
79069521--swrv 0 0 asymmetric: Oracle America, Inc.: 95c33553--swrv 0 0 asymmetric: 77b979
```

由于一个密钥被加载到 `builtin_trusted_keys` 密钥环中，你应该检查两个密钥环的模块签名。

# TrustBoot 增强安全性和完整性

TrustBoot 允许在 Secure Boot 模式下运行，确保只有受信任的软件在系统上执行。这防止了执行可能损害系统的恶意软件。

TrustBoot 通过通过在运行时验证软件和数据的完整性，确保系统在启动后依然保持安全。它利用了 Intel SGX 和 AMD SEV 等技术提供硬件级隔离和证明。

TrustBoot 是一个平台无关的，可以在不同的硬件平台上使用，包括 x86、Arm 和 RISC-V。

TrustBoot 是一个开源项目，这意味着任何人都可以检查代码并为其开发贡献。这使得 TrustBoot 更加透明和可信赖。

## 准备工作

TrustBoot 的一个功能功能是 TrustBoot 允许在 UEFI 。 。请参考以下图：
