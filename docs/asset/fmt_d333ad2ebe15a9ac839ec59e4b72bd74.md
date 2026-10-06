
| 拒绝服务 (DoS) 攻击 | 攻击者或攻击者小组通过向目标主机（服务器、路由器或工作站）发送未经授权的数据包，对组织的网络或服务器资源进行攻击。这导致资源无法供合法用户使用。 | 美国报告的最严重的 DoS 案例发生在 2000 年。几个高流量的商业和政府网站由于受到协同 ping 洪流攻击而无法使用，该攻击使用了几个具有高带宽连接的被攻破系统作为僵尸，或重定向的广播节点。源包通常是伪造的（以及重发的），使得难以调查攻击的真实来源。使用 `iptables` 的入站过滤技术（IETF rfc2267）以及网络入侵检测系统（如 `snort`）进展有助于管理员追踪和防止分布式 DoS 攻击。 |

# 第 2 章：在安装期间保护 RHEL 安全

安全工作在您开始安装 Red Hat Enterprise Linux 之前就开始了。从一开始就安全地配置系统，将有利于以后实施额外的安全设置。

## 2.1. BIOS 和 UEFI 安全

对 BIOS（或等效 BIOS）和引导加载程序的密码保护，可以防止具有物理访问系统的未授权用户使用可移动介质启动，或通过单用户模式获取权限。为了防止此类攻击，您应该采取的安全措施取决于工作站上信息的敏感程度以及机器所在的位置。

例如，如果机器被用于贸易展且不包含任何敏感信息，那么防止此类攻击可能并不至关重要。然而，如果员工带有公司网络私有未加密 SSH 密钥的笔记本电脑被遗留在同一家商店里，可能会导致重大安全漏洞，并对整个公司产生影响。

然而，如果工作站位于授权或信任人员可以访问的地方，则加固 BIOS 或引导加载程序可能不是必要的。

### 2.1.1. BIOS 密码

更改 BIOS 设置的主要原因如下——如果入侵者访问了 BIOS，他们可以将其设置为：

- 防止更改 BIOS 设置——如果入侵者访问了 BIOS，他们可以将其设置为从 CD-ROM 或闪存驱动器启动。这使得他们能够进入救援模式或单用户模式，从而允许他们在系统上启动任意进程或复制敏感数据。

- 防止系统启动——某些 BIOS 允许对启动过程进行密码保护。当激活后时，攻击者将被强制在 BIOS 启动引导加载程序之前输入密码。

由于不同计算机设置 BIOS 密码的方法不同，请参阅计算机说明书以获取特定指令。

如果您忘记了 BIOS 密码，可以通过主板上的跳线帽（jumpers）或断开 CMOS 电池来重置。因此，如果可能，锁定机箱是一个良好的习惯。但在尝试断开 CMOS 电池之前，请先查阅计算机或主板的说明书。

#### 2.1.1.1. 基于非 BIOS 的系统安全

其他系统和架构使用不同的程序来执行底层任务，这些任务大致等于 x86 系统上的 BIOS。例如，统一扩展固件接口 (`UEFI`) shell。关于类似 BIOS 类程序密码保护的指令，请参阅制造商的说明。

## 2.2. 磁盘分区

Red Hat 建议为 `/boot`、`/`、`/home`、`/tmp` 和 `/var/tmp/` 目录创建分区。每个分区的原因不同，我们将分别讨论。

### /boot

此分区是系统启动期间读取的第一个分区。引导系统进入 Red Hat Linux 8 的引导加载程序和内核镜像存储在此分区中。此分区不应加密。如果此分区包含在 `/` 中且该分区变为加密或不可用，您的系统将无法启动。

### /home

当用户数据（`/home`）未单独分区存储时，分区可能会满导致操作系统变得不稳定。此外，当您的系统升级到 Red Hat Linux 8 的下一个版本时，您可以稍后保留 `/home` 分区中的数据，它在安装期间不会被覆盖。如果根分区（`/`）损坏，您的数据可能会永久丢失。通过使用独立分区，可以稍微增加防止数据丢失的。您还可以针对此分区进行频繁备份。

### /tmp 和 /var/tmp

`/tmp` 和 `/var/tmp` 目录都用于存储不需要长期保存的数据。然而，如果大量数据涌入其中一个目录，将耗尽存储空间。如果这些目录存储在 `/` 中，您的系统可能会不稳定并崩溃。因此，将这些目录移动到分区是一个好主意。

#### 注意

在安装过程中，有一个加密区的选项。您必须提供密码。该密码将作为解锁块加密的密钥。

## 2.3. 安装期间限制网络连接

在安装 Red Hat Linux 8 时，安装介质代表的是特定时间的系统快照。由于由于，它可能没有包含最新的安全修复，并可能存在某些介质发布后才修复的问题。

在安装可能存在漏洞的操作系统时，始终将暴露限制在必要的网络区域。最安全的选择是“无网络”，这意味着在安装期间保持断开。在某些情况下，局域网或内网连接就足够，而互联网连接风险最高。为了遵循最佳安全实践，在从网络安装 Red Hat Linux 8 时选择选择您的存储库区域。

## 2.4. 安装所需的最小软件包

只安装您将使用的软件包是一种良好的做法，因为计算机上的每种软件都可能包含漏洞。如果您是从 DVD 介质安装，请利用此机会精确选择您想要安装的包。如果您需要其他包，可以稍后添加到系统中。

## 2.5. 安装后步骤

以下是在安装 Red Hat Enterprise Linux 之后应立即执行的安全相关步骤。

1. 更新您的系统。输入以下命令：

```bash
# yum update
```

2. 虽然防火墙服务 `firewalld` 在安装 Red Hat Enterprise Linux 时会自动启用，但在某些情况下可能会显式禁用，例如在 kickstart 配置中。在这种情况下，建议重新启用防火墙。要启动 `firewalld`，请 root 执行以下命令：

```bash
# systemctl start firewalld
# systemctl enable firewalld
```

3. 为了增强安全性，禁用不需要的服务。例如，如果您的计算机上没有安装打印机，使用以下命令禁用 `cups` 服务：

```bash
# systemctl disable cups
```

要查看正在运行的服务，请输入以下命令：

```bash
$ systemctl list-units | grep service
```

[1] 由于不同制造商的系统 BIOS 不同，某些可能不支持任何类型的密码保护，而某些可能只支持一种而不不支持另一种。

# 第 3 章. 使用系统级加密策略

加密策略是一个用于配置核心加密子系统的系统，涵盖了 TLS、IPC、SSH、DNSSec 和 Kerberos 协议。它提供了一小组策略，管理员可以从中进行选择。

## 3.1. 系统级加密策略

一旦设置了系统级策略，RHEL 中的应用程序将遵循该策略，并拒绝使用不符合策略的算法和协议，除非你显式地请求应用程序这样做。这意味着，该策略适用于在带有系统提供的配置运行时应用程序的默认行为，但在需要时，你可以对其进行覆盖。

Red Hat Linux 8 包含以下策略级别：

| 策略 | 描述 |

| :--- | :--- |

| DEFAULT | 默认系统级加密策略为当前的威胁模型提供了安全设置。它允许使用 TLS 1.2 和 1.3 协议，以及 IKE2 和 SSH2 协议。如果 RSA 密钥和 Diffie-Hellman 参数长度至少为 2048 位，则会被接受。 |

| LEGACY | 此策略确保与 Red Hat Enterprise Linux 5 及更早版本具有最大的兼容性；由于攻击面增加，其安全性较低。除了 DEFAULT 级别的算法和协议外，它还包含了对 TLS 1.0 和 1.1 协议的支持。排除了 DSA、3DES 和 RC4 算法，如果 RSA 密钥和 Diffie-Hellman 参数长度至少为 1023 位，则会被接受。 |

| FUTURE | 一种保守的安全级别，能够抵御任何近期的未来攻击。该级别不允许在签名算法中使用 SHA-1。如果 RSA 密钥和 Diffie-Hellman 参数长度至少为 3072 位，则会被接受。 |

| FIPS | 符合 FIPS140-2 要求的策略级别。这由 `fips-mode-setup` 工具在内部使用，该工具会将 RHEL 系统切换到 FIPS 模式。 |

> 重要

由于 Customer Portal API 上的证书所使用的加密密钥不符合 FUTURE 系统级加密策略的要求，`redhat-support-tool` 实用目前无法在此策略级别工作。

为了解决这个问题，在连接到 Customer Portal API 时请使用 `DEFAULT` 加密策略。

> 注意

策略级别中描述的特定算法和密码仅在应用程序支持它们时才可用。

### 管理加密策略的工具

要查看或更改当前系统级加密策略，请使用 `update-crypto-policies` 工具，例如：

```
$ update-crypto-policies --show
DEFAULT
# update-crypto-policies --set FUTURE
Setting system policy to FUTURE
```

要确保加密策略的更改生效，请重启系统。

### 通过移除不安全的密码套件和协议来实现强加密默认

以下列表包含了从 RHEL 8 核心加密库中移除的密码套件和协议。它们不存在于源码中，或者其支持在构建期间被禁用，因此应用程序无法使用它们。

- DES（自 RHEL 7 起）

- 所有导出级密码套件（自 RHEL 7 起）

- 签名中的 MD5（自 RHEL 7 起）

- SSLv2（自 RHEL 7 起）

- SSLv3（自 RHEL 8 起）

- 所有小于 224 位的 ECC 曲线（自 RHEL 6 起）

- 所有二进制域 ECC 曲线（自 RHEL 6 起）

## 在所有策略级别中禁用的密码套件和协议

以下密码套件和协议在所有加密策略级别中均禁用。只有通过显式配置单个协议才能启用。

- 参数小于 1024 位的 DH

- 密钥大小小于 1024 位的 RSA

- Camellia

- ARIA

- SEED

- IDEA

- 仅完整性密码套件

- 使用 SHA-384 HMAC 的 TLS CBC 模式密码套件

- AES-CCM8

- 所有与 TLS 1.3 不兼容的 ECC 曲线，包括 secp256k

- Ikev1（自 RHEL 8 起）

## 在加密策略级别中启用的密码套件和协议

下表显示了四个加密策略级别中启用的密码套件和协议。

### Red Hat Enterprise Linux 8 安全加固

| | LEGACY | DEFAULT | FIPS | FUTURE |

| :--- | :--- | :--- | :--- | :--- |

| IKEv1 | no | no | no | no |

| 3DES | yes | no | no | no |

| RC4 | yes | no | no | no |

| DH | 至少 1024-位 | 至少 2048-位 | 至少 2048-位 | 至少 3072-位 |

| RSA | 至少 1024-位 | 至少 2048-位 | 至少 2048-位 | 至少 3072-位 |

| DSA | yes | no | no | no |

| TLS v1.0 | yes | no | no | no |

| TLS v1.1 | yes | no | no | no |

| 数字签名中的 SHA-1 | yes | yes | no | no |

| CBC 模式密码 | yes | yes | yes | no |

| 小于 256 位的对称密码 | yes | yes | no | no |

| 证书中的 SHA-1 | yes | yes | no | no |

## 3.2. 切换到兼容早期版本的系统级加密策略

RHEL 8 中的系统级策略允许与早期版本兼容，提供了 `LEGACY` 策略级别。

> 警告

> 切换到 `LEGACY` 策略会导致安全性降低。

### 步骤

1. 要切换到 `LEGACY` 策略，输入以下命令：

```bash
# update-crypto-policies --set LEGACY
Setting system policy to LEGACY
```

## 3.3. 将系统切换到 FIPS 模式

系统级策略包含一个策略级别，根据联邦信息处理（FIPS）出版物 140-2 启用模块自检。

### 步骤

1. 在 RHEL 中启用 FIPS 模式：

```bash
# fips-mode-setup --enable
Setting system policy to FIPS
FIPS mode will be enabled.
```

2. 重启系统使设置生效：

```bash
# reboot
```

### 验证步骤

1. 重启后，可以检查 FIPS 模式状态：

```bash
# fips-mode-setup --check
FIPS mode is enabled.
```

## 3.4. 在容器中启用 FIPS 模式

在容器中根据联邦信息标准（FIPS）出版物 140-2 模块自检：

### 前提条件

- 主机系统必须先切换到 FIPS 模式。

### 步骤

1. 从主机将系统 fips 文件挂载到容器中。

2. 在容器内设置策略级别：

```
$ update-crypto-policies --set FIPS
```

RHEL 8.2 引入了切换容器 FIPS 模式的替代方法。容器内需要以下命令：

```
# mount --bind /usr/share/crypto-policies/back-ends/FIPS /etc/crypto-policies/back-ends
```

> 注意

在 RHEL 8 中，`fips-setup` 命令在容器中无法正常工作，无法用其启用或检查 FIPS 模式。

## 3.5. 将应用程序排除在系统级加密策略之外

最好通过在应用程序中配置支持的密码套件和协议来自定义加密设置。

你也可以从 `/etc/crypto-policies/back-ends` 目录删除应用程序的符号链接，并将其替换为自定义的加密设置。此配置防止应用程序使用系统级加密策略。

### 3.5.1. 退出系统级加密策略的示例

wget

要自定义 `wget` 下载器使用的加密设置，请使用 `--secure-protocol` 和 `--ciphers`。例如：

```
$ wget --secure-protocol=TLSv1_1 --ciphers="SECURE128" https://example.com
```

欲更多信息请参考 wget(1) 手页中的 HTTPS (SSL/TLS) 选项。

curl

要指定加密算法，请使用 curl 工具的 `--ciphers` 选项并提供用冒号分隔的加密算法列表作为值。例如：

```
$ curl https://example.com --ciphers DES-CBC3-SHA:RSA-DES-CBC3-SHA
```

更多信息请参阅 curl(1)。

### Firefox

尽管在 Firefox Web 浏览器中无法退出系统级加密策略，但你可以在 Firefox 的配置编辑器中进一步限制支持的加密算法和 TLS 版本。在地址栏中输入 `about:config` 并根据需要更改 `security.tls.version.min` 选项的值。将 `security.tls.version.min` 设置为 1 允许 TLS 1.0 作为最低要求，security.tls.version.min 2 启用 TLS 1.1，以此类推。

### OpenSSH

要为 OpenSSH 服务器退出系统级加密策略，请取消 `/etc/sysconfig/sshd` 文件中 `CRYPTO_POLICY=` 变量行的注释。更改后，你在 `/etc/ssh/sshd_config` 文件的 Ciphers、MACs、KexAlgorithms 和 GSSAPIKexAlgorithms 部分指定的值将不再被覆盖。更多信息请参阅 ssh_config(5)。

### Libreswan

要允许 Libreswan IPSec 使用 IKE1 协议，请注释 `/etc/ipsec.conf` 中的以下行：

```
# include /etc/crypto-policies/back-ends/libreswan.config
```

然后在你的连接配置中添加 `ikev2=never` 选项。更多信息请参阅 ipsec.conf(5) 手页。

### 其他资源

- 详情请参考 update-crypto-policies(8) 手页。

## 3.6. 使用策略修改符自定义系统级加密策略

使用此过程调整任何系统级加密策略级别或完整自定义策略的算法或协议。![](img/ce77567a90cabeaf166ca2952.png)

> 注意

RHEL 8 提供了系统级加密策略的自定义。

### 步骤

- 1. 创建包含你的调整的策略模块，例如：

```
# cat /etc/crypto-policies/modules/MYCRYPTO.mod
```

sha1_in_certs = 0

min_rsa_size = 3072

cipher = -256-GCM -256-CBC -128-GCM -128-CBC

### 重要

在策略模块文件名中使用大写字母。

- 2. 将你的策略应用于 DEFAULT 系统级加密策略级别：

```
# update-crypto-policies --set DEFAULT:MYCRYPTO
```

- 3. 使你的加密设置对于已运行的服务生效，请重启系统：

```
# reboot
```

### 其他资源

- 详情请参考 update-crypto-policies(8) 手页中的 Custom Policies 部分以及 update-crypto-policies(8) 手页中的 Crypto Policy Format 部分。

- RHEL 8 提供了自定义系统级加密策略的示例。

## 3.7. 创建并设置系统级加密策略

以下步骤演示了如何通过策略文件自定义系统级加密策略。

### 注意

RHEL 8 提供了系统级加密策略的自定义。

### 步骤
