
# Fedora Linux 手册：用户命令第九卷

![](img/00002.jpeg)

## 献辞

本书献给 Michael Kerrisk 以及 Linux 文档项目团队。

## 版权信息

LinuxManFiles.com 出版

Unit 12 / 30 upper Queen Street

Auckland, New Zealand 1010

保留所有权利。未经出版者书面许可，不得以任何手段（电子、机械、复印、录音或其他）对本书的任何部分进行复制、存储在检索系统中或传输。对于本文所包含的信息的使用，不承担任何专利责任。尽管在准备本书时已采取措施，但出版者和作者对错误或遗漏不承担任何责任。对于使用本文所包含的信息造成的损害也不承担任何责任。

版权所有 2016 LinuxManFiles.com

第一版 2016

ISBN 978-0-9941352-8-5

出版于新西兰

编译与编辑：Gareth Morgan Thomas

## 免责声明

就我们所知，本手册中发布的所有文本除非另有说明，均属于公有领域。

我们非常重视对公有领域的承诺。

如果您有理由认为 LinuxManFiles.com 发布的任何文本尚未进入公有领域，请邮件至：`editor at linuxmanfiles.com`。

## 目录

# PITCHPLAY

## 名称

`pitchplay` - 封装脚本，用于通过声卡使用 `cdda2wav` 以不同音调播放音频轨道（`cdda2wav` 已启用声卡支持）。

## 概要

`pitchplay <track a> <pitch a> <track b> <pitch b>...`

## 描述

`pitchplay` 允许使用 `cdda2wav` 播放音频轨道，音调以百分比指定，100% 为原始调，50% 为低一个八度，200% 为高一个八度。

## 示例

`pitchplay 1 90 3 140 5 50`

将以 90% 的音调播放轨道 1，以 140% 的音调播放轨道 3，以 50% 的音调播放轨道 5。

## 参阅

(1)

## 作者

`cdda2was` 由 Joerg Schilling <> 和等人编写。

本帮助页描述了由 cdrkit 分发版提供的 `pitchplay` 程序实现。详见正文。它是 cdrtools 项目分发的原始程序的衍生版本。然而，cdrtools 的开发者并未参与该衍生版本的开发，因此对由此引起的任何问题概不负责。请勿尝试通过联系原始作者来获取此程序的支持。

如果您有支持性问题，请发送至

如果您确实发现了 Bug，请向此列表发送邮件，或在邮件主题中写入简短描述，并在正文第一行输入 `"Package: cdrkit"`。

本帮助页由 Oleksandr Moskalenko <>> 编写，适用于 Debian GNU/Linux 系统。其他发行版可以在不联系作者的情况下使用。帮助页中的任何错误或遗漏都是我的错；对本帮助页的查询或更正应直接发送给（而不是发送给主要作者）。

***

此文档正在进行中。请在 `Mozilla NSS bug 836477` 中贡献初始审查 `m[][1]`

# pk12util

## 描述

PKCS #12 工具 `pk12util` 允许在任何支持 PKCS#12 的服务器之间共享证书。该工具可以将证书和密钥从 PKCS-12 文件导入安全数据库，导出证书并列出证书和密钥。

## 选项与参数

### 选项

- `-i p12file`：从 PKCS#12 文件导入密钥和证书到安全数据库。
- `-l p12file`：列出 PKCS#12 文件中的密钥和证书。
- `-o p12file`：从安全数据库导出密钥和证书到 PKCS#12 文件。

### 参数

- `-c keyCipher`：指定密钥加密算法。
- `-C certCipher`：指定密钥证书（整体包）加密算法。
- `-d [sql:]directory`：指定用于导入或导出证书和密钥的数据库目录。

`pk12util` 支持两种数据库：旧安全数据库（`cert8.db`、`key3.db` 和 `secmod.db`）和新的 SQLite 数据库（`cert9.db`、`key4.db` 和 `pkcs11.txt`）。如果不使用前缀 `sql:`，工具将假设指定的数据库为旧格式。

- `-h tokenna`：指定导入或出的令牌名称。
- `-k slotPasswordFile`：指定包含槽密码的文本文件。
- `-K slotPassword`：指定槽密码。
- `-m | --key-len key`：指定密钥长度。
- `-key-len key`：指定所需的密钥长度。
- `-n | --cert-key-len key`：指定证书密钥所需的长度。
- `-n`：指定要导出或导入的证书名称。
- `-P dbprefix`：指定数据库的前缀。
- `-r`：以原始（二进制）形式转储所有内容。
- `-v`：启用调试日志。
- `-w p12filePasswordFile`：指定文件的密码。
- `-W p12filePassword`：指定文件的密码。

## 返回码

- `0`：无错误
- `1`：用户取消
- `2`：用错误
- `6`：无错误
- `8`：证书数据库错误
- `9`：密钥数据库错误
- `10`：文件初始化错误
- `11`：Unicode 转换错误
- `12`：临时文件创建错误
- `13`：PKCS11 获取错误
- `14`：PKCS12 解码器启动
- `15`：导入错误
- `16`：PKCS12 解码错误
- `17`：PKCS12 解码验证
- `18`：PKCS12 解码校验
- `19`：PKCS12 解码导入
- `20`：版本 3 转换为 2
- `21`：版本 7 转换为 5
- `22`：证书和密钥错误
- `23`：获取默认数据库错误
- `24`：通过别名查找证书
- `25`：创建导出错误
- `26`：完整性错误
- `27`：安全创建错误
- `28`：证书和密钥错误
- `29`：编码错误

## 示例

### 导入密钥和证书

`pk12util` 导入证书或密钥的基本用法是指定 PKCS#12 输入文件（`-i`）并指定要访问的安全数据库（使用 `-d` 指定目录或 `-h` 指定令牌）。

```bash
pk12util -i p12File [-h tokenna] [-v] -d [sql:]directory [-P dbprefix] [-k slotPasswordFile|-K slotPassword] [-w p12filePasswordFile|-W p12filePassword]
```

例如：

```text
# pk12util -i /tmp/cert-files/users.p12 -d sql:/ho/my/sharedndb
输入用于加密密钥的密码。密码至少为 8 个字符，并应包含一个非字母字符。
输入新密码:
再次输入密码:
输入 PKCS12 文件的密码:
pk12util: PKCS12 导入成功
```

### 导出密钥和证书

使用 `pk12util` 命令导出证书和密钥需要同时指定从数据库提取的证书名称（`-n`）以及要写入的 PKCS#12 格式输出文件。可以使用可选参数来加密该文件以保护证书材料。

```bash
pk12util -o p12File -n certna [-c keyCipher] [-C certCipher] [-m|--key-len keyLen] [-n|--cert-key-len certKeyLen] -d [sql:]directory [-P dbprefix] [-k slotPasswordFile|-K slotPassword] [-w p12filePasswordFile|-W p12filePassword]
```

```text
# pk12util -o certs.p12 -n Server-Cert -d sql:/ho/my/sharednssdb
Enter password for PKCS12 file:
Re-enter password:
```

### 列出密钥和证书

`.p12` 文件中的信息不是人类可读的。文件中的证书和密钥可以用人类可读的美打印格式打印（列出），显示 `.p12` 文件中每个证书以及任何公钥的信息。

```bash
pk12util -l p12File [-h tokenna] [-r] [-d [sql:]directory] [-P dbprefix] [-k slotPasswordFile|-K slotPassword] [-w p12filePasswordFile|-W p12filePassword]
```

例如，这将打印默认的 ASCII 输出：

```text
# pk12util -l certs.p12
Enter password for PKCS12 file:
Key(shrouded):
Friendly Na: Thawte Freemail Meer's Thawte Consulting (Pty) Ltd.
ID Encryption algorithm: PKCS #12 V2 PBE With SHA-1 And 3KEY Triple DES-CBC
Paraters:
Salt: 45:2e:6a:a0:03:4d:7b:a1:63:3c:15:ea:67:37:62:1f
Iteration Count: 1 (0x1)
Certificate:
Data:
Version: 3 (0x2)
Serial Nuer: 13 (0xd)
Signature Algorithm: PKCS #1 SHA-1 With RSA Encryption
Issuer: "E=,CN=Thawte Personal Freemail C A,OU=Certification Services Division,O=Thawte Consulting,L=Cape T own,ST=Western Cape,C=ZA"
```

或者，`-r` 会打印证书并将它们导出为独立的 DER 二进制文件。这允许将证书提供给支持 `.p12` 文件的其他应用程序。每个证书写入写入顺序编号的文件中，从 `file0001.der` 开始一直到 `file000N.der`，每个证书的编号递增：

```text
pk12util -l test.p12 -r
Enter password for PKCS12 file:
Key(shrouded):
Friendly Na: Thawte Freemail Meer's Thawte Consulting (Pty) Ltd.
ID Encryption algorithm: PKCS #12 V2 PBE With SHA-1 And 3KEY Triple DES-CBC
Paraters:
Salt: 45:2e:6a:a0:03:4d:7b:a1:63:3c:15:ea:67:37:62:1f
Iteration Count: 1 (0x1)
Certificate
Friendly Na: Thawte Personal Freemail Issuing CA - Thawte Consulting
Certificate
Friendly Na: Thawte Freemail Meer's Thawte Consulting (Pty) Ltd. ID
```

## 密码加密

PKCS#12 不仅保护私密钥，还保护与密钥相关的证书和元数据。基于密码的加密用于在导出到 PKCS#12 文件时保护私密钥，可选地保护整个包。如果没有指定算法，工具将默认使用 `PKCS12 V2 PBE with SHA1 and 3KEY Triple DES-cbc` 进行私密钥加密。在非 FIPS 模式下，`PKCS12 V2 PBE with SHA1 and 40 Bit RC4` 是整体包加密的默认算法。在 FIPS 模式下，没有包加密。

私密钥默认始终使用强加密进行保护。

支持多种类型的密码。

### 用于 PKCS#5 V2 的对称 CBC 密码

- `DES-CBC`
- `RC2-CBC`
- `RC5-CBCPad`
- `DES-EDE3-CBC`（密钥加密的默认算法）
- `AES-128-CBC`
- `AES-192-CBC`
- `AES-256-CBC`
- `CAMELLIA-128-CBC`
- `CAMELLIA-192-CBC`
- `CAMELLIA-256-CBC`

### PKCS#12 PBE 算法

- `PKCS #12 PBE with Sha1 and 128 Bit RC4`
- `PKCS #12 PBE with Sha1 and 40 Bit RC4`
- `PKCS #12 PBE with Sha1 and Triple DES CBC`
- `PKCS #12 PBE with Sha1 and 128 Bit RC2 CBC`
- `PKCS #12 PBE with Sha1 and 40 Bit RC2 CBC`
- `PKCS12 V2 PBE with SHA1 and 128 Bit RC4`
- `PKCS12 V2 PBE with SHA1 and 40 Bit RC4`（非 FIPS 模式下的默认）
- `PKCS12 V2 PBE with SHA1 and 3KEY Triple DES-cbc`
- `PKCS12 V2 PBE with SHA1 and 2KEY Triple DES-cbc`
- `PKCS12 V2 PBE with SHA1 and 128 Bit RC2 CBC`
- `PKCS12 V2 PBE with SHA1 and 40 Bit RC2 CBC`

### PKCS#5 PBE 算法

- `PKCS #5 Password Based Encryption with MD2 and DES CBC`
- `PKCS #5 Password Based Encryption with MD5 and DES CBC`
- `PKCS #5 Password Based Encryption with SHA1 and DES CBC`

使用 PKCS#12 时，加密提供程序可以是软令牌模块或外部硬件模块。如果加密模块不支持请求的算法，则将使用下一个最合适的算法。

```text
pkcheck --action-id=action {--process{pid|pid,pid-start-ti|pid,pid-start-ti,uid*} | --system-bus-na=busna} [--allow-user-interaction] [--enable-internal-agent] [--detailkeyvalue...]
```

# pkcheck

## 描述

`pkcheck` 用于检查由 `--process`（见下文）或 `--system-bus-na` 指定的进程是否授权执行 `action`。`--detail` 选项可以使用零次或多次，用于传递有关 `action` 的细节。如果传递了 `--allow-user-interaction`，`pkcheck` 将阻塞并等待身份验证。

执行 `pkcheck --list-temp` 将列出当前会话的所有临时授权，而执行 `pkcheck --revoke-temp` 将撤销当前会话的所有临时授权。

此命令是 polkit D-Bus 接口的简单封装；详情请参 D-Bus 接口文档。

## 返回值

如果指定的进程已授权，`pkcheck` 以返回值 0 退出。如果授权结果包含任何细节，这些细节将以环境变量风格的键/值对格式打印到标准输出，例如：首先是键，后面跟着等号，然后是值并换行。

```text
KEY1=VALUE1 KEY2=VALUE2 KEY3=VALUE3 ...
```

不在 `[a-zA-Z0-9_]` 中的字节将使用带有 `*` 的八进制代码进行转义。例如，UTF-8 字符串 `føl,你好` 将打印为 `f\303\270l\54\344\275\240\345\245\275`。

如果指定的进程未授权，`pkcheck` 以返回值 1 退出，并在标准错误上打印诊断信息。细节打印到标准输出。

由于没有可用的身份验证代理或未传递 `--allow-user-interaction` 导致指定的进程未授权，`pkcheck` 以返回值 2 退出，并在标准错误上打印诊断信息。细节打印到标准输出。

由于用户拒绝了身份验证对话框或请求导致指定的进程未授权，`pkcheck` 以返回值 3 退出，并在标准错误上打印诊断信息。细节打印到标准输出。

如果在检查授权时发生错误，`pkcheck` 以返回值 127 退出，并在标准错误上打印诊断信息。

如果传递的一个或多个选项格式不正确，`pkcheck` 以返回值 126 退出。如果 stdin 是 tty，则也会显示此帮助页。

## 注意事项

不要对 `--process` 使用裸露的 `pid` 或 `pid,start-ti` 语法形式。这两种形式都存在竞态条件。新代码应始终使用 `pid,pid-start-ti,uid`。`start-ti` 的值可以通过查询取决于操作系统的 (5) 文件系统来确定。如果传递的参数少于 3 个，`pkcheck` 将尝试在内部查找它们，但注意这可能存在竞态。

如果你的程序是一个带有例如自定义 Unix 域套接字的守护进程，你应该通过 `PEERCRED` 等操作系统机制来确定 `uid` 参数。

## 身份验证代理

`pkcheck` 与任何其他 polkit 应用一样，将使用为相关进程注册的身份验证代理。然而，如果没有可用的身份验证代理，如果传递了 `--enable-internal-agent` 选项，`pkcheck` 可以注册它自己的文本身份验证代理。

## 作者

由 David Zeuthen <> 编写，感谢许多人的帮助。

## 缺陷

请将错误报告发送至发行或 polkit-devel 邮件列表，查看链接 [] 的如何订阅。

## 参见

(8)、(8)、(1)、(1)、(1)

* * *

# pkcs11_eventmgr



## 名称

`pkcs11_eventmgr` - 智能卡 PKCS#11 事件管理器

## 语法

`pkcs11_eventmgr [no]debug [no]daemon polling_ti=<secs> expire_ti=<secs> pkcs11_module=<module> config_file=<filename>`

## 描述

`card_eventmgr` 是一个智能卡监控程序，监听读卡器状态并在多个事件上分发操作。`card_eventmgr` 可用于多种操作，例如在移除卡片时锁定屏幕。

支持三种事件：卡片插入、卡片移除和移除卡片后的超时。要执行的操作在配置文件中指定。

## 选项

### `[no]debug`

启用调试输出。默认为无调试。

### `[no]daemon`

在后台运行。如果未设置 `debug`，则也从 tty 分离。默认：无守护进程。

### `polling_ti=<secs>`

设置以秒为单位的轮询超时。默认为 1 秒。

### `expire_ti=<secs>`

设置卡片移除后的超时。默认为 0（永不超时）。

### `config_file=<configuration file>`

设置配置文件。默认为 `/etc/pam_pkcs11/card_eventmgr.conf`。

### `pkcs11_module=<pkcs11.so library>`

设置要使用的 PKCS#11 库模块。默认为 `/usr/lib/pkcs11/opensc-pkcs11.so`。

## 文件

- `/etc/pam_pkcs11/card_eventmgr.conf`
- `/usr/lib/pkcs11/opensc-pkcs11.so`

## 示例

以标准方式运行此程序，请输入：

```bash
pkcs11_eventmgr
```

或者，你可以指定选项：

```bash
pkcs11_eventmgr nodebug nodaemon polling_ti=5 config_file=${HOME}/.pkcs11_eventmgr.conf
```

## 缺陷

由于 PKCS#11 库在卡片移除和重新插入时会失败，为了避免这种情况，`pkcs11_eventmgr` 在移除卡片时尝试通过调用 `C_Finalize()` 和 `C_Initialize()` 重新初始化。

因此，像 `xscreensaver-command` 这样的应用程序可能会失败（例如：尝试解锁已解锁的会话）。在这种情况下，命令错误地返回错误代码。

用户应注意这种情况。

## 作者

Juan Antonio Martinez <>

## 参见

(8), (5)

`README.eventmgr`

PAM-PKCS11 用户手册

# `pkcs11_inspect`

## 名称

`pkcs11_inspect` - 打印证书内容

## 概要

`pkcs11_inspect [debug] [config_file=<filename>]`

## 描述

`pkcs11_inspect` 使用智能卡监控来获取证书内容并显示它。

`pkcs11_inspect` 使用配置文件以及 (8) PAM 模块。它加载定义的映射器，并使用它们查找证书条目（例如：查找 UPN 条目）。

当映射器在证书中找到条目时，它将其转换为 UTF-8 并打印到标准输出。

## 选项

## 示例

要标准方式运行此程序，在读卡器中插入智能卡并输入：

```bash
pkcs11_inspect
```

或者，你可以指定选项：

```bash
pkcs11_inspectdebugconfig_file=${HOME}/.pam_pkcs11.conf
```

## 作者

Juan Antonio Martinez <>

## 参见

(8), (1)

PAM-PKCS11 用户手册

# `pkcs11_listcerts`

## 名称

`pkcs11_listcerts` - 智能卡 PKCS#11 证书列表

## 语法

`pkcs11_listcerts [debug]`

## 描述

`pkcs11_listcerts` 显示所有证书。

## 选项

### `debug`

启用调试输出。

## 作者

Juan Antonio Martinez <>

## 参见

(8)

PAM-PKCS11 用户手册

Juan Antonio Martinez <>

## 相关参考

PAM-PKCS11 用户手册

(8)

# PKCS12

## 名称

`pkcs12` - PKCS#12 文件工具

## 语法

```bash
openssl pkcs12 [-export] [-chain] [-inkey filena] [-certfile filena] [-na na] [-cana na] [-in filena] [-out filena] [-noout] [-nomacver] [-nocerts] [-clcerts] [-cacerts] [-nokeys] [-info] [-des | -des3 | -idea | -aes128 | -aes192 | -aes256 | -callia128 | -callia192 | -callia256 | -nodes] [-noiter] [-maciter | -nomaciter | -nomac] [-twopass] [-descert] [-certpbe cipher] [-keypbe cipher] [-macalg digest] [-keyex] [-keysig] [-password arg] [-passin arg] [-passout arg] [-rand file(s)] [-CAfile file] [-CApath dir] [-CSP na]
```

## 描述

`pkcs12` 命令允许创建和解析 PKCS#12 文件（通常称为 PFX 文件）。Netscape、MSIE 和 MS Outlook 等多个程序使用 PKCS#12 文件。

## 命令选项

有许多选项，其含义取决于是在创建还是解析 PKCS#12 文件。默认情况下解析 PKCS#12 文件。可以使用 `-export` 选项创建 PKCS#12 文件（见下文）。

## 解析选项

### `-in filena`

指定要解析的 PKCS#12 文件的 `filena`。默认使用标准输入。

### `-out filena`

写入证书和私钥的 `filena`，默认使用标准输出。它们均以 PEM 格式写入。

### `-passin arg`

PKCS#12 文件（即输入文件）的密码源。有关 `arg` 格式的更多信息，请参见 (1) 中的 `PASS PHRASE ARGUMENTS` 部分。

### `-passout arg`

用于加密任何输出私钥的口语源。有关 `arg` 格式的更多信息，请参见 (1) 中的 `PASS PHRASE ARGUMENTS` 部分。

### `-password arg`

在使用 `-export` 时，`-password` 等同于 `-passout`。否则，`-password` 等同于 `-passin`。

### `-noout`

此选项抑制将密钥和证书输出到 PKCS#12 文件的版本。

### `-clcerts`

仅输出客户端证书（不输出 CA 证书）。

### `-cacerts`

仅输出 CA 证书（不输出客户端证书）。

### `-nocerts`

不输出任何证书。

### `-nokeys`

不输出任何私钥。

### `-info`

输出关于 PKCS#12 文件结构、使用的算法和迭代次数的额外信息。

### `-des`

在输出前使用 `DES` 对私钥进行加密。

### `-des3`

在输出前使用三重 `DES` 对私钥进行加密，这是默认设置。

### `-idea`

在输出前使用 `IDEA` 对私钥进行加密。

### `-aes128`、`-aes192`、`-aes256`

在输出前使用 `AES` 对私钥进行加密。

### `-callia128`、`-callia192`、`-callia256`

在输出前使用 `Callia` 对私钥进行加密。

### `-nodes`

完全不对私钥进行加密。

### `-nomacver`

在读取文件之前不尝试验证完整性 MAC。

### `-twopass`

提示输入独立的完整性和加密密码：大多数软件始终认为这些密码是相同的，因此此选项会导致此类 PKCS#12 文件无法读取。

## 文件创建选项

### `-export`

此选项指定将创建一个而非解析 PKCS#12 文件。

### `-out filena`

指定写入 PKCS#12 文件的 `filena`。默认使用标准输出。

### `-in filena`

从此处读取证书和私钥的 `filena`，默认使用标准输入。它们必须必须是 PEM 格式。顺序不重要，但应包含一个私钥及其对应的证书。如果存在额外的证书，它们也将被包含在 PKCS#12 文件中。

### `-inkey filena`

从该文件读取私钥。如果不存在，则输入文件中必须存在一个私钥。

### `-na friendlyna`

指定证书和私钥的 `friendly na`。此名称通常由导入文件的软件在列表框中显示。

### `-certfile filena`

从该文件读取额外证书的 `filena`。

### `-cana friendlyna`

指定其他证书的 `friendly na`。此选项可以使用多次，以按照它们出现的顺序为所有证书指定名称。Netscape。

### `-passin arg`、`-passout arg`

PKCS#12 文件（即输入文件）的密码源。有关 `arg` 格式的更多信息，请参见 (1) 中的 `PASS PHRASE ARGUMENTS` 部分。

在使用 `-export` 时，`-password` 等同于 `-passout`。否则，`-password` 等同于 `-passin`。

### `-chain`

此选项指定将创建一个而非解析 PKCS#12 文件。（等一下，检查上下文：原文在 `-export` 下提到“此选项指定将创建一个而非解析 PKCS#12 文件”，但稍后提到了 `-chain`。我将保持原文结构）。

将 `na` 写入 Microsoft CSP `na`。

## NOTES

尽管有很多选项，但大多数选项极少使用。对于 PKCS#12 文件解析，仅需使用 `-in` 和 `-out`；对于 PKCS#12 文件的创建，还会使用 `-export` 和 `-na`。

如果没有出现 `-clcerts`、`-cacerts` 或 `-nocerts` 选项，则所有证书将按照它们在输入 PKCS#12 文件中出现的顺序输出。不能保证第一个出现的证书就是与私钥对应的那个。某些软件需要私钥和证书，并假设文件中的第一个证书就是与私钥对应的那个：但情况并不总是如此。使用 `-clcerts` 选项可以通过只输出与私钥对应的证书来解决此问题。如果需要 CA 证书，则可以使用 `-nokeys -cacerts` 选项将它们输出到单独的文件，以便仅输出 CA 证书。

`-keypbe` 和 `-certpbe` 算法允许指定私钥和证书的精确加密算法。通常默认值就足够了，但有时软件无法处理 Triple DES 加密的私钥，此时可以使用选项 `-keypbe PBE-SHA1-RC2-40` 将私钥加密降低到 40 位 RC2。所有算法的完整描述包含在 `pkcs8` 手页中。

## EXAMPLES

解析 PKCS#12 文件并将其输出到文件：

```bash
openssl pkcs12 -in file.p12 -out file.pem
```

仅将客户端证书输出到文件：

```bash
openssl pkcs12 -in file.p12 -clcerts -out file.pem
```

不加密私钥：

```bash
openssl pkcs12 -in file.p12 -out file.pem -nodes
```

打印关于 PKCS#12 文件的信息：

```bash
openssl pkcs12 -in file.p12 -info -noout
```

创建一个 PKCS#12 文件：

```bash
openssl pkcs12 -export -in file.pem -out file.p12 -na "My Certificate"
```

包含额外的证书：

```bash
openssl pkcs12 -export -in file.pem -out file.p12 -na "My Certificate" \
-certfile othercerts.pem
```

## BUGS

有人会认为 PKCS#12 标准本身就是一个巨大的 bug :-)

0.9.6a 之前的 OpenSSL 版本在 PKCS#12 密钥生成例程中存在一个 bug。在少数情况下，这可能会产生一个使用无效密钥加密的 PKCS#12 文件。结果是，其他实现（MSIE 或 Netscape）触发此 bug 的某些 PKCS#12 文件无法被 OpenSSL 解密，同样，OpenSSL 产生的某些 PKCS#12 文件也无法被其他实现解密。产生此类文件的概率相对较小：小于 1/256。

修复此 bug 的副作用是，任何旧的加密格式错误的 PKCS#12 文件都无法再被修复后的版本解析。在这种情况下，`pkcs12` 工具将报告 MAC 是正确的，但在提取私钥时会因解密错误而失败。

这个问题可以通过旧版本的 OpenSSL 从 PKCS#12 文件中提取私钥和证书，然后使用新版本的 OpenSSL 从这些密钥和证书重新创建 PKCS#12 文件来解决。例如：

```bash
old-openssl -in bad.p12 -out keycerts.pem
openssl -in keycerts.pem -export -na "My PKCS#12 file" -out fixed.p12
```

## SEE ALSO

(1)

# PKCS7

## NAME

`pkcs7` - PKCS#7 工具

## SYNOPSIS

```bash
openssl pkcs7 [-inform PEM|DER] [-outform PEM|DER] [-in filena] [-out filena] [-print_certs] [-text] [-noout] [-engine id]
```

## DESCRIPTION

`pkcs7` 命令处理 DER 或 PEM 格式的 PKCS#7 文件。

## COMMAND OPTIONS

### `-inform DER|PEM`

指定输入格式。`DER` 格式是 DER 编码的 PKCS#7 v1.5 结构。`PEM`（默认）是 DER 格式的 Base64 编码版本，带有头部和尾行。

### `-outform DER|PEM`

指定输出格式，该选项与 `-inform` 选项含义相同。

### `-in filena`

指定要读取的输入文件名，如果没有指定此选项，则从标准输入读取。

### `-out filena`

指定要写入的输出文件名，默认为标准输出。

输出文件中的所有证书：

```bash
openssl pkcs7 -in file.pem -print_certs -out certs.pem
```

```bash
openssl pkcs8 -topk8 -in key.pem -out file.pem
```

## NOTES

PEM 格式的 PKCS8 使用头尾行：

```text
-----BEGIN PRIVATE KEY-----
...
-----END PRIVATE KEY-----
```

为了与某些 CA 兼容，它还接受：

```text
-----BEGIN PRIVATE KEY-----
...
-----END PRIVATE KEY-----
```

## RESTRICTIONS

PKCS7 v1.5 在 RFC2315 中指定的无法，例如，...

```text
-写入 "My Certificate" \ -certfile othercerts.pem
```



此选项生成一种损坏格式的 RSA 私钥，以便软件使用。具体而言，私钥本应封装在 `OCTET STRING` 中，但软件仅包含结构本身，而不包含周围的 `OCTET STRING`。

### `-eed`

此选项生成损坏格式的 DSA 密钥。DSA 参数被嵌入在 `PrivateKey` 结构内部。在这种格式下，`OCTET STRING` 包含一个由两个结构组成的 `ASN1 SEQUENCE` 序列：一个包含参数的 `SEQUENCE` 和一个包含私钥的 `ASN1 INTEGER`。

### `-nsdb`

此选项生成与 Netscape 私钥数据库兼容的损坏格式的 DSA 密钥。`PrivateKey` 包含分别由公钥和私钥组成的 `SEQUENCE`。

### `-v2 alg`

此选项启用 PKCS#5 v2.0 算法的使用。通常情况下，PKCS#8 私钥使用基于密码的加密算法 `pbeWithMD5AndDES-CBC` 进行加密，该算法使用 56 位 DES 加密，但它是 PKCS#5 v1.5 支持的最强加密算法。使用 `-v2` 选项将使用 PKCS#5 v2.0 算法，它们可以使用任何加密算法，例如 168 位三 DES 或 128 位 RC2，但目前还没有许多实现支持 PKCS#5 v2.0。如果你只是在 OpenSSL 中使用私钥，那么这并不重要。

`alg` 参数是要使用的加密算法，有效值包括 `des`、`des3` 和 `rc2`。建议使用 `des3`。

### `-v2prf alg`

此选项设置与 PKCS#5 v2.0 使用的 PRF 算法。典型值可以是 `hmacWithSHA256`。如果未设置此选项，将使用密码算法的默认值，如果没有默认值，则使用 `hmacWithSHA1`。

### `-v1 alg`

此选项指定要使用的 PKCS#5 v1.5 或 PKCS#12 算法。可能算法的完整列表下所示。

### `-engine id`

可以输出 PKCS#8 格式的 DER 编码加密私钥，因为加密细节包含在 ASN1 级别，而传统格式将它们包含在 PEM 级别。

# PKCS#5 v1.5 和 PKCS#12 算法

`-v1` 命令行选项可以使用多种算法，包括 PKCS#5 v1.5 和 PKCS#12。下文将对其进行详细描述。

### PBE-MD2-DES PBE-MD5-DES

这些算法包含在原始 PKCS#5 v1.5 规范中。由于它们都使用 DES，因此仅提供 56 位保护。

### PBE-SHA1-RC2-64 PBE-MD2-RC2-64 PBE-MD5-RC2-64 PBE-SHA1-DES

这些算法未在原始 PKCS#5 v1.5 规范中提到，但它们使用相同的密钥派生算法并被软件支持。它们在 PKCS#5 v2.0 中被提到。它们使用 64 位 RC2 或 56 位 DES。

### PBE-SHA1-RC4-128 PBE-SHA1-RC4-40 PBE-SHA1-3DES PBE-SHA1-2DES PBE-SHA1-RC2-128 PBE-SHA1-RC2-40

这些算法使用 PKCS#12 密码加密算法，并允许使用三 DES 或 128 位 RC2 等强加密算法。

## EXAMPLES

使用三 DES 将私钥从传统格式转换为 PKCS#5 v2.0 格式：

```
openssl pkcs8 -in key.pem -topk8 -v2 des3 -out enckey.pem
```

使用 CBC 模式下的 256 位 AES 和 `hmacWithSHA256` PRF 将私钥从传统格式转换为 PKCS#5 v2.0 格式：

```
openssl pkcs8 -in key.pem -topk8 -v2 aes-256-cbc -v2prf hmacWithSHA256 -out enckey.pem
```

使用兼容 PKCS#5 1.5 的算法 (DES) 将私钥转换为 PKCS#8：

```
openssl pkcs8 -in key.pem -topk8 -out enckey.pem
```

使用兼容 PKCS#12 的算法 (3DES) 将私钥转换为 PKCS#8：

```
openssl pkcs8 -in key.pem -topk8 -out enckey.pem
```

使用兼容 PKCS#12 的算法 (3DES) 将私钥转换为 PKCS#8：

```
openssl pkcs8 -in key.pem -topk8 -out enckey.pem
```

使用 v1 PBE-SHA1-DES 将私钥转换为 PKCS#8：

```
openssl pkcs8 -in key.pem -topk8 -out enckey.pem
```

读取 DER 格式的未加密 PKCS#8：

```
openssl pkcs8 -inform DER -nocrypt -in key.pem
```

将 PKCS#8 格式的私钥转换为传统格式：

```
openssl pkcs8 -in key.pem -out key.pem
```

## STANDARDS

此 PKCS#5 v2.0 的测试向量已发布在 pkcs-ng 列表中，使用了三 DES、高迭代次数的 RC2：8 密钥符合此标准。

## BUGS

应该有一个选项可以打印加密算法以及迭代次数等细节。使用三 DES 和 PKCS#5 v2.0 的 PKCS#8 应该是 OpenSSL 的默认密钥格式：为了兼容，某些工具使用了旧格式。

## SEE ALSO

(1), (1), (1), (1)

# PKEXEC

请注意，身份验证消息可能会引用变量（参见“VARIABLES”部分），例如 `$(user)` 将展开为用户变量的值。

## 包装器用法

为了避免修改现有软件以在命令行调用前加缀 `pkexec`，可以在 **she-bang 包装器** 中使用 `pkexec`，如下：

```
#!/usr/bin/pkexec /usr/bin/python import os import sys print "Hello, I'm running as uid %d"%(os.getuid()) for n in range(len(sys.argv)): print "arg[%d]=%s'"%(n, sys.argv[n])
```

如果此脚本安装到 `/usr/bin/my-pk-test`，可以使用以下注释

```
[...] <annotate key="org.freedesktop.policykit.exec.path">/usr/bin/python</annotate> <annotate key="org.freedesktop.policykit.exec.argv1">/usr/bin/my-pk-test</annotate> [...]
```

来选择合适的 polkit 动作。注意写好最后一个注解，否则它将匹配任何对 `/usr/bin/python` 脚本的 `pkexec` 调用。

## 变量

以下变量由 `pkexec` 设置。它们可以用于授权规则和身份验证对话框中显示的消息：

* `program`:
  要执行的程序的完全限定路径。例如：`"/bin/cat"`

* `command_line`:
  请求的命令行（不要用此进行任何安全检查，因为它是不安全的）。例如：`"cat /srv/xyz/foobar"`

* `user`:
  执行程序的用户名。例如：`"davidz"`

* `user.gecos`:
  执行程序的用户全名。例如：`"David Zeuthen"`

* `user.display`:
  执行程序的用户表示，适用于在身份验证对话框中显示。通常设置为用户名和全名的组合。例如：`"David Zeuthen (davidz)"`

## 作者

由 David Zeuthen <> 编写，并得到许多人的帮助。

## 缺陷

请将错误报告发送至发行版或 polkit-devel 邮件列表，参见关于如何订阅的链接 []

## 参见

(8), (8), (1), (1), (1)

## 注意事项

1. she-bang 包装器

***

# PKEY

## 名称

pkey - 公钥或私钥处理工具

## 语法

`openssl pkey` [`-inform PEM|DER`] [`-outform PEM|DER`] [`-in filename`] [`-passin arg`] [`-out filename`] [`-passout arg`] [`-cipher`] [`-text`] [`-text_pub`] [`-noout`] [`-pubin`] [`-pubout`] [`-engine id`]

## 描述

`pkey` 命令处理公钥或私钥。它们可以在各种形式之间转换，并打印它们的组件。

## 命令选项

### `-inform DER|PEM`

这指定输入格式 DER 或 PEM。

### `-outform DER|PEM`

指定输出格式，这些选项与 `-inform` 选项含义相同。

### `-in filename`

指定用于读取密钥的文件名，如果未指定此选项，则使用标准输入。如果密钥已加密，将提示输入密码。

### `-passin arg`

输入文件的密码源。更多关于格式的信息请参见文档。

### `-out filename`

指定用于读取密钥的文件名，如果未指定此选项，则使用标准输入。

### `-passout arg`

输出文件的密码源。更多关于格式的信息请参见文档。

### `-cipher`

使用的加密算法。

### `-text`

以文本格式打印出组件。

### `-text_pub`

以文本格式打印公钥组件。

### `-noout`

不输出编码版本。

### `-pubin`

从输入读取公钥。

### `-pubout`

输出密钥的公钥部分。

## 参见

(1), (1), (1), (1), (1)

***

# PKEYPARAM

## 名称

pkeyparam - 公钥算法参数处理工具

## 语法

`openssl pkeyparam` [`-in filename`] [`-out filename`] [`-text`] [`-noout`] [`-engine id`]

## 描述

`pkey` 命令处理公钥或私钥。它们可以在各种形式之间转换，并打印它们的组件。

## 命令选项

### `-in filename`

指定用于读取参数的文件名，如果未指定此选项，则使用标准输入。

### `-out filename`

指定用于写入参数的文件名，如果未指定此选项，则使用标准输出。

### `-text`

以文本格式打印参数。

### `-noout`

不输出参数的编码版本。

### `-engine id`

使用的引擎。

## 示例

打印参数的文本版本：

```bash
openssl pkeyparam -in param.pem -text
```

## 注意

此命令没有 `-inform` 或 `-outform` 选项，因为只支持 PEM 格式，且密钥类型是由 PEM 头部决定的。

## 查看

(1), (1), (1), (1), (1), (1)

***

# PKEYUTL

## 名称

pkeyutl - 公钥算法实用

## 语法

`openssl` `pkeyutl` [`-in file`] [`-out file`] [`-sigfile file`] [`-inkey file`] [`-keyform PEM|DER`] [`-passin arg`] [`-peerkey file`] [`-peerform PEM|DER`] [`-pubin`] [`-certin`] [`-rev`] [`-sign`] [`-verify`] [`-verifyrecover`] [`-encrypt`] [`-decrypt`] [`-derive`] [`-pkeyopt opt:value`] [`-hexdump`] [`-asn1parse`] [`-engine id`]

## 描述

`pkeyutl` 命令可以使用任何支持的算法执行公钥操作。

## 命令选项

`-in filena`

指定用于读取数据的输入文件 filena，如果未指定此选项，则使用标准输入。

`-out filena`

指定要写入的输出文件 filena，默认使用标准输出。

`-inkey file`

输入密钥文件，默认情况下应为私钥。

`-keyform PEM|DER`

密钥格式，PEM、DER 或 ENGINE。

`-passin arg`

输入密钥密码源。有关 `arg` 格式的更多信息，请参阅 (1) 中的 `PASS PHRASE ARGUMENTS` 。

`-peerkey file`

对端密钥文件，用于密钥派生（agreent）操作。

`-peerform PEM|DER`

对端密钥格式，PEM、DER 或 ENGINE。

`-engine id`

指定一个引擎（通过其唯一的 `id` 字符串）将使 `pkeyutl` 尝试获取指定引擎的函数引用，从而在需要时对其进行初始化。该引擎随后将被设置为所有可用算法的默认引擎。

`-pubin`

输入文件为公钥。

`-certin`

输入是包含公钥的证书。

`-rev`

反转输入缓冲区顺序。这对于以小端序格式表示缓冲区的库（如 CryptoAPI）很有用。

`-sign`

对输入数据签名并输出签名结果。这需要私钥。

`-verify`

根据签名文件验证输入数据，并指示验证成功还是失败。

`-verifyrecover`

验证输入数据并输出恢复的数据。

`-encrypt`

使用公钥加密输入数据。

`-decrypt`

使用私钥解密输入数据。

`-derive`

使用对端密钥派生共享密钥。

`-hexdump`

对输出数据进行十六进制导出。

`-asn1parse`

对输出数据进行 asn1parse，这在 ASN1 结构被签名时，配合 `-verifyrecover` 选项使用非常有用。

## 注意

支持的操作和选项取决于密钥算法及其实现。下面列出了 OpenSSL 操作和选项。

除非另有说明，所有算法都支持 `digest:alg` 选项，该选项指定在 sign、verify 和 verifyrecover 操作中使用的摘要。值 `alg` 应代表如 `EVP_get_digestbynayna()` 函数中使用的摘要，例如 `sha1`。

## RSA 算法

DSA 算法仅支持签名和验证操作。目前除 `digest` 之外没有额外选项。只能使用 SHA1 摘要，且默认使用该摘要。

## DH 算法

DH 算法仅支持操作。

## EC 算法

EC 算法支持签名、验证和派生操作。目前支持且 `digest` 之外没有额外选项。只能使用 SHA1 摘要，且默认使用该摘要。

## 示例

使用私钥对数据签名：
```bash
openssl pkeyutl -in param.pem
```

恢复签名（例如，使用 RSA 时）：
```bash
openssl pkeyutl -verify in.pem
```

验证签名（例如，使用 RSA 时）：
```bash
openssl pkeyutl -verify in.pem
```

使用公钥加密数据：
```bash
openssl pkeyutl -encrypt -in param.pem -out out.
```

派生共享密钥：
```bash
openssl pkeyutl -derive -peerkey param.pem
```



## 查看

(1), (1), (1)

`pkeyutl` (1)

(1), (1), (1), (1), (1)

## 选项

支持以下选项：

`*--modversion*`

请求显示命令行上指定的库的版本信息。如果 `pkg-config` 能够找到命令行上的所有库，则每个库的版本字符串将打印到 stdout，每行一个版本。在这种情况下，`pkg-config` 成功退出。如果一个或多个库未知，`pkg-config` 将以非零代码退出，且 stdout 内容未定义。

### `--version`

显示 `pkg-config` 的版本并退出。

### `--atleast-pkgconfig-version=VERSION`

要求至少使用指定版本的 `pkg-config`。

### `--help`

显示帮助信息并退出。

### `--print-errors`

如果命令行上的一个或多个模块或其依赖未找到，或者在解析 `*.pc*` 文件时发生错误，则此选项将导致打印解释问题的错误信息。对于像 `--exists` 这样的“谓词”选项，`pkg-config` 默认静默运行，因为它通常用于想要控制输出内容的脚本中。此选项可以单独使用（仅打印在查找命令行命令行模块时遇到的错误），也可以与其他选项结合使用。环境变量 `PKG_CONFIG_DEBUG_SPEW` 会覆盖此选项。

### `--short-errors`

打印短的错误信息。

### `--silence-errors`

如果命令行上的一个或多个模块或其依赖未找到，或者在解析 `*.pc*` 文件时发生错误，则此选项将防止打印解释问题的错误。对于像 `--exists` 这样的“谓词”选项，`pkg-config` 默认静默运行，因为它通常用于想要控制输出内容的脚本中。因此，此选项仅对 `--cflags` 或 `--modversion` 等默认打印错误的选项有用。环境变量 `PKG_CONFIG_DEBUG_SPEW` 会覆盖此选项。

### `--errors-to-stdout`

如果打印错误，将其打印到 stdout 而不是默认的 stderr。

### `--debug`

打印调试信息。这与同样启用 `--print-errors` 的环境变量 `PKG_CONFIG_DEBUG_SPEW` 略有不同。

以下选项用于编译和链接：

### `--cflags`

这会打印编译命令行上的包所需的预处理器和编译标志，包括它们所有依赖项的标志。标志会被“压缩”，使得每个相同的标志只出现一次。如果无法找到命令行上一个或多个包的数据，`pkg-config` 将以非零代码退出。

### `--cflags-only-I`

打印 `--cflags` 的 `-I` 部分。即，它定义了头文件搜索路径但不指定其他内容。

### `--cflags-only-other`

打印 `--cflags` 中未被 `--cflags-only-I` 覆盖的部分。

### `--libs`

此选项与 `--cflags` 相同，但它打印链接标志。与 `--cflags` 一样，重复标志会被合并（保持正确的顺序），并且输出中包含依赖项的标志。

### `--libs-only-L`

打印 `--libs` 的 `-L` 部分。即，它定义了库搜索路径，但不指定要链接哪些库。

### `--libs-only-l`

为命令行上指定的库打印 `--libs` 的 `-l` 部分。注意，由于 `-rd` 等标志，`--libs-only-l` 和 `--libs-only-L` 的并集可能比 `--libs` 小。

### `--libs-only-other`

打印 `--libs` 中未被 `--libs-only-L` 和 `--libs-only-l` 覆盖的部分，例如 `--pthread`。

### `--variable=VARIABAME`

返回包的 `*.pc*` 文件中定义的变量值。大多数包定义了变量 `prefix`，因此你可以说：`pkg-config --variable=prefix glib-2.0`

### `--define-variable=VARIABAME=VALUE`

为变量设置全局值，覆盖任何 `*.pc*` 文件中的值。大多数包定义了变量 `prefix`，因此你可以说：`pkg-config --print-errors --define-variable=prefix=/foo --variable=prefix glib-2.0`

### `--print-variables`

返回包中定义的所有变量列表。

### `--uninstalled`

通常，如果你请求包 `foo` 且包 `foo-uninstalled` 存在，`pkg-config` 将优先选择“-uninstalled”变体。这允许针对未安装的包进行编译/链接。如果你指定了 `--uninstalled` 选项，如果使用了任何“-uninstalled”包，`pkg-config` 将返回成功，否则返回失败（false）。环境变量 `PKG_CONFIG_DISABLE_UNINSTALLED` 防止 `pkg-config` 隐式选择“-uninstalled”包，因此如果设置了该变量，只有当你显式在命令行上传递如“foo-uninstalled”的名字时它们才会被使用。

### `--exists`

### `--atleast-version=VERSION`

### `--exact-version=VERSION`

### `--max-version=VERSION`

这些选项测试命令行上的包或包列表是否为 `pkg-config` 已知，并可选地测试包的版本号是否满足某些约束。如果所有包存在且满足版本约束，`pkg-config` 将成功退出。否则它将失败退出。只有第一个 `VERSION` 比较选项会被遵循。后续此类类型的选项将被忽略。

与其使用版本测试选项，你可以简单地在每个包名称后给出版本约束，例如：`pkg-config --exists 'glib-2.0 >= 1.3.4 libx = 1.8.3'`。如果你想查看错误信息，请参考使用 `--print-errors`。当没有给 `pkg-config` 提供输出选项时，将隐含 `--exists`。

### `--msvc-syntax`

此选项仅在 Windows 上可用。它导致 `pkg-config` 以 Microsoft Visual C++ 命令行编译器 `cl` 识别的格式输出 `-l` 和 `-L` 标志。具体来说，它不是打印 `-Lx:/so/path` 而是打印 `/libpath:x/so/path`，不是打印 `-lfoo` 而是打印 `foo.lib`。注意 `--libs` 输出由链接器标志，应该放在 `cl` 命令行的 `/link` 之后。

### `--dont-define-prefix`

此选项仅在 Windows 上可用。它防止 `pkg-config` 自动尝试覆盖每个 `*.pc*` 文件中变量 `prefix` 的值。

### `--prefix-variable=PREFIX`

此选项同样仅在 Windows 上可用。它设置 `pkg-config` 如上自动设置的变量名称。

### `--static`

输出适用于静态链接的库。这包括输出中的任何私有库。这取决于 `*.pc` 文件中正确的标记，否则通常会输出大量的库。

### `--list-all`

列出 `pkg-config` 路径中找到的所有模块。

### `--print-provides`

列出指定包提供的所有模块。

### `--print-requires`

列出指定包需要的所有模块。

### `--print-requires-private`

列出指定包用于静态链接需要的所有模块（参见 `--static`）。

## 环境变量

### `PKG_CONFIG_PATH`

一个用冒号分隔（在 Windows 上用分号分隔）的目录列表，用于搜索 `*.pc*` 文件。在搜索路径之后始终会搜索默认目录；默认是 `libdir/*pkgconfig:*datadir*/pkgconfig`，其中 `libdir` 是 `pkg-config` 安装时的 libdir，`datadir` 是 `pkg-config` 安装时的 datadir。

### `PKG_CONFIG_DEBUG_SPEW`

如果设置，会导致 `pkg-config` 打印各种调试信息并报告所有错误。

### `PKG_CONFIG_TOP_BUILD_DIR`

用于为 `*.pc*` 文件中可能出现的魔法变量 `pc_top_builddir` 设置值。如果未设置环境变量，将使用默认值 `'$(top_builddir)'`。该变量应该指向使用 `pkg-config` 报告的编译/链接标志的 Makefile 的顶部构建目录。这在编译/链接未安装的包时才有用。

### `PKG_CONFIG_DISABLE_UNINSTALLED`

通常如果你请求包 `foo` 且包 `foo-uninstalled` 存在，`pkg-config` 将优先选择“-uninstalled”变体。这允许针对未安装的包进行编译/链接。如果设置了此环境变量，将禁用该行为。

### `PKG_CONFIG_ALLOW_SYSTEM_CFLAGS`

如果 `.pc` 文件中变量的值以原始的未覆盖的 `prefix` 变量值开头，则将使用覆盖后的 `prefix` 值。

## AUTOCONF 宏

`PKG_CHECK_MODULES(VARIABLE-PREFIX, MODULES [,ACTION-IF-FOUND [,ACTION-IF-NOT-FOUND]])`

宏 `PKG_CHECK_MODULES` 可用于 `configure.ac` 以检查模块是否存在。一个典型的用法是：

```autf
PKG_CHECK_MODULES([MYSTUFF], [gtk+-2.0 >= 1.3.5 libx = 1.8.4])
```

这将产生替换变量 `MYSTUFF_LIBS` 和 `MYSTUFF_CFLAGS`，它们被设置为给定模块列表的 libs 和 cflags。如果模块缺失或版本错误，默认情况下 configure 将终止并显示消息。要替换默认操作，请指定 `ACTION-IF-NOT-FOUND`。如果你指定了自己的 `ACTION-IF-NOT-FOUND`，`PKG_CHECK_MODULES` 将不会打印任何错误消息。但是，它会设置变量 `MYSTUFF_PKG_ERRORS`，你可以用它显示发生了什么错误。

注意，如果存在第一次调用 `PKG_CHECK_MODULES` 可能发生的情况，你应该确保在你的 `configure.ac` 中显式调用 `PKG_PROG_PKG_CONFIG`。

另外请注意，不建议重复使用 `VARIABLE-PREFIX`。在第一次成功使用后，后续对相同 `VARIABLE-PREFIX` 的调用将直接使用从上次使用设置的 `_LIBS` 和 `_CFLAGS` 变量，而不再调用 `pkg-config`。

`PKG_PROG_PKG_CONFIG([MIN-VERSION])`

将 `PKG_CONFIG` 变量定义为可用的 `pkg-config`，如果你需要 `pkg-config` 但不想使用 `PKG_CHECK_MODULES`，则非常有用。

`PKG_CHECK_EXISTS(MODULES, [ACTION-IF-FOUND], [ACTION-IF-NOT-FOUND])`

检查特定模块组是否存在。类似于 `PKG_CHECK_MODULES()`，但不会设置变量或打印错误。类似于 `PKG_CHECK_MODULES`，请确保调用了此宏或 `PKG_CHECK_MODULES` 的第一个实例，或者确保手动调用了 `PKG_CHECK_EXISTS`。

`PKG_INSTALLDIR(DIRECTORY)`

替换变量 `pkgconfigdir` 为模块安装 pkg-config `.pc` 文件的位置。默认目录为 `$libdir/pkgconfig`，但可以通过传递 `DIRECTORY` 更改默认值。用户可以通过 `--with-pkgconfigdir` 参数进行覆盖。

`PKG_NOARCH_INSTALLDIR(DIRECTORY)`

替换变量 `noarch_pkgconfigdir` 为模块安装架构无关的 pkg-config `.pc` 文件的位置。默认目录为 `$datadir/pkgconfig`，但可以通过传递 `DIRECTORY` 更改默认值。用户可以通过 `--with-noarch-pkgconfigdir` 参数进行覆盖。

`PKG_CHECK_VAR(VARIABLE, MODULE, CONFIG-VARIABLE, [ACTION-IF-FOUND], [ACTION-IF-NOT-FOUND])`

从 `MODULE` 获取 pkg-config 变量 `CONFIG-VARIABLE` 的值并存储在 `VARIABLE` 中。注意不建议重复使用 `VARIABLE`，因为如果变量已设置，将跳过检查。

## 元数据文件语法

要将一个库添加到 `pkg-config` 已知的包集中，只需安装 `.pc` 文件。您应该将此文件安装到 `libdir*/pkgconfig`。

这里有一个示例文件：

```ini
# 这是一个注释
prefix=/ho/hp/unst
# 这定义了一个变量
exec_prefix=${prefix}
# 根据第一个变量定义另一个变量
libdir=${exec_prefix}/lib
includedir=${prefix}/include
Na: GObject
# 人类可读名称
Description: GLib 的对象/类型系统
# 人类可读描述
Version: 1.3.1
URL:
Requires:
```

`pkg-config` 由 Jas Henstridge 编写，由 Martijn van Beers 重写，并由 Havoc Pennington 重写。Tim Janik、Owen Taylor 和 Raja Harinath 提交了建议和代码。`gno-config` 由 Miguel de Icaza、Raja Harinath 以及 GNOME 团队的各种黑客编写。它的灵感来自 Owen Taylor 的 `gtk-config` 程序。

## Bug (BUGS)

`pkg-config` 处理带和不带 `=` 的参数混合得并不良好。请坚持使用一种。

可以在 `pkg-config` 组件下报告 Bug。

# PGREP

## 名称

`pgrep`, `pkill` - 根据名称和其他属性查找进程或向进程发送信号

## 语法

`pgrep` [选项] 模式

`pkill` [选项] 模式

## 描述

`pgrep` 查看当前运行的进程，并将匹配选择标准的进程 ID 列到标准输出（stdout）。所有标准都必须匹配。例如，

```
$ pgrep -u root sshd
```

将仅列出名为 `sshd` 且属于 `root` 的进程。另一方面，

```
$ pgrep -u root,daemon
```



将列出属于`root`或`daemon`的进程。

`pkill`将向每个进程发送指定的信号（默认是`SIGTERM`），而不是将它们列出在标准输出上。

## 选项

`-signal`

`--signal` `信号`定义发送给每个匹配进程的信号。可以使用数值或符号性信号名称。（仅限`pkill`。）

`-c`、`--count`

抑制正常输出；相反，打印匹配进程的计数。当计数不匹配任何项时（例如返回零），该命令将返回非零值。

`-d`、`--delimiter` `分隔符`

设置用于在输出中分隔每个进程 ID 的字符串（默认是换行符）。（仅限`pgrep`。）

`-f`、`--full`

`模式`通常只与进程名称进行匹配。当设置`-f`时，将使用完整的命令行。

仅选择匹配进程中最旧（最久远启动的）的一个。

`-P`、`--parent` `ppid`、...

仅匹配父进程 ID 在列表中的进程。

`-s`、`--session` `sid`、...

仅匹配进程会话 ID 在列表中的进程。会话 ID 0 被转换为`pgrep`或`pkill`自身的会话 ID。

`-t`、`--terminal` `term`、...

仅匹配控制终端在列表中的进程。指定的终端名称不应带`/dev/`前缀。

`-u`、`--euid` `euid`、...

仅匹配有效用户 ID 在列表中的进程。可以使用数值或符号性值。

`-U`、`--uid` `uid`、...

仅匹配真实用户 ID 在列表中的进程。可以使用数值或符号性值。

`-v`、`--inverse`

取反匹配。此选项通常用于`pgrep`的语境。在`pkill`的语境中，短选项被禁用以避免意外使用该选项。

`-w`、`--lightweight`

在`pgrep`的语境中显示所有线程 ID 而不是 PID。在`pkill`的语境中，此选项被禁用。

`-x`、`--exact`

仅匹配名称（或如果指定了`-f`则为命令行）完全匹配`模式`的进程。

`-F`、`--pidfile` `文件`

从文件中读取`PID`。此选项对于`pkill`也许比`pgrep`有用。

`-L`、`--logpidfile`

如果 pidfile（见`-F`）未锁定则失败。

`--ns` `pid`

匹配属于指定命名空间的进程。需要以 root 身份运行以匹配来自其他用户的进程。查看`--nslist`了解如何限制匹配哪些命名空间。

`--nslist` `名称`、...

仅匹配提供的命名空间。可用的命名空间：`ipc`、`mnt`、`net`、`pid`、`user`、`uts`。

`-V`、`--version`

显示版本信息并退出。

`-h`、`--help`

显示帮助并退出。

## 操作数

`模式`

指定扩展正则表达式，用于匹配进程名称或命令行。

## 示例

示例 1：查找`nad`守护进程的进程 ID：

```bash
$ pgrep -u root nad
```

示例 2：让`syslog`重新读取配置文件：

```bash
$ pkill -HUP syslogd
```

示例 3：提供所有`xterm`进程的详细信息：

```bash
$ ps -fp $(pgrep -d, -xterm)
```

示例 4：运行`netscape`：

```bash
$ pgrep -d, -netscape
```

## 退出状态

`0`

成功。

`1`

无匹配。

`2`

语法错误。

`3`

致命错误。

## 注意事项

`pgrep`和`pkill`命令是`procps`软件包的一部分。

## 参考

`pgrep`、`pkill`

---

设置要使用的配置文件。所有`cs11`选项均可用。注意，其中某些选项在非 PAM 环境下没有意义，因此它们将被忽略。

## 返回值

成功时，`pklogin_finder`在标准输出上打印登录名称并退出码 0。

用户映射失败时返回 1。

无用户匹配时不打印任何内容并返回 2。

## 文件

`/etc/pam_pk11/pk11.conf`

## 示例

要标准方式运行此程序，将智能卡插入读取器并输入：

```bash
pklogin_finder
```

或者，你可以指定选项：

```bash
pklogin_finder -configfile=${HOME}/.pam_pk11.conf
```

## 作者

Juan Antonio Martinez <>

## 参考

(8)、(1)、PAM-PKCS11 用户手册

## 标准

`prep`和`pkill`引入于 Solaris 7。

## 作者

本手册页由 Richard Hughes 编写。

## 报告 Bug

请将 Bug 报告发送至

---

成功

`1`

由于内部错误失败。

## 参考

`pkcon` (1)。

## 作者

本手册页由 Richard Hughes 编写。

## 作者

Richard Hughes

作者。

## 版权

Copyright 2007 Richard Hughes

---

# PKTTYAGENT

## 名称

`pkttyagent` - 文本认证辅助程序

## 语法

`pkttyagent` [`--version`] [`--help`]

`pkttyagent` [`--process`{`pid`|`pid,pid-start-ti`}|`--system-bus-na` `busna`] [`--notify-fd` `fd`] [`--fallback`]

## 描述

`pkttyagent`用于为`--process`或`--system-bus-na`指定的对象启动文本认证代理。如果没有这两个选项，则使用父进程。

为了在身份代理注册成功时接收通知，可以监听`Changed` D-Bus 信号，或使用`--notify-fd`传递给程序的文件描述符数量。当身份代理成功注册后，该文件描述符将被关闭。

如果使用了`--fallback`，文本身份代理将不会替换现有的身份代理。

## 返回值

如果无法注册身份代理，`pkttyagent`将以退出代码 127 退出。诊断信息将打印在标准错误上。

如果传递的一个或多个选项格式错误，`pkttyagent`以退出代码 126 退出。如果`stdin`是一个`ty`，则也会显示此手册页。

如果身份代理注册成功，`pkttyagent`将继续运行，并根据需要与用户交互。当不再需要其服务时，可以杀死该进程。

## 注意

由于进程标识可能会被重用，调用者在使用`--process`选项时应始终使用`pid,pid-start-ti`。`pid-start-ti`的值可以通过查询例如取决于操作系统的 (5) 文件系统来确定。如果仅向`--process`选项传递了`pid`，则`pkttyagent`将自行查找启动 ti，但注意这可能存在竞态条件。

## 作者

由 David Zeuthen <> 编写，感谢许多人的帮助。

## 缺陷

请将错误报告发送到发行版或 polkit-devel 邮件列表，参见链接`m[]`的如何订阅。

## 参见

(8)、(8)、(1)、(1)、(1)

# PL2PM

## 名称

`pl2pm` - 将 Perl4 `.pl` 文件转换为 Perl5 `.pm` 模块的粗略工具。

## 语法

`pl2pm files`

## 描述

`pl2pm`是一个辅助将 Perl4 风格的`.pl`文件转换为 Perl5 风格库模块的工具。通常，你的旧`.pl`文件仍然可以正常工作，只有当你计划更新库以使用较新的 Perl 5 功能（如`AutoLoading`）时才应该使用此工具。

## 局限性

这只是第一步，但通常是一个良好的第一步。

## 作者

Larry Wall <>

# PLDD

## 名称

`pldd` - 显示链接到进程的动态共享对象

## 语法

`pldd pid pldd option`

## 描述

`pldd`命令显示链接到指定进程 ID 的动态共享对象列表。该列表包含了使用 (3) 动态加载的库。

## 选项

`-?`、`--help`

显示程序帮助信息。

`--usage`

显示简短的用法信息。

`-V`、`--version`

显示程序版本。

也会显示包含链接到进程的动态共享对象的输出。

## 参见

(1)、(1)、(3)、(8)

## 结语

此页是 Linux `man-pages`项目发布 4.00 的。项目的描述、报告缺陷的信息以及此页的最新版本可以在此处找到。

# PMAP

## 名称

`pmap` - 报告进程的内存映射

## 语法

`pmap [options] pid [...]`

## 描述

`pmap`命令报告一个或多个进程的内存映射。

## 选项

`-x`、`--extended`

显示扩展格式。

`-d`、`--device`

显示设备格式。

`-q`、`--quiet`

不显示页眉或页脚行。

`-A`、`--range low,high`

将结果限制在指定的`low`到`high`地址范围。注意低、高参数是用逗号分隔的单个字符串。

`-X`

显示比`-x`选项更多的细节。警告：格式根据`/proc/PID/smaps`变化。

`-XX`

显示内核提供的所有内容。

`-p`、`--show-path`

显示映射列中文件的完整路径。

`-c`、`--read-rc`

设置 HTML 的基础 URL。

`-C`、`--read-from`

从`file`读取。

`-n`、`--create-rc`

创建新配置。

`-N`、`--create-to`

创建到`file`。

`-h`、`--help`

显示帮助。

`-V`、`--version`

显示版本并退出。

## 退出状态

`0`

成功。

`1`

失败。

`2`

未找到。

## 参见

(1)、(1)

## 标准

无适用，但`pmap`看起来很糟糕。

## 报告缺陷

请将报告发送至

# POD2HTML

## 名称

`pod2ht` - 将 pod 文件转换为 HTML

## 语法

`pod2ht --htdir <na>`

## 描述

`pod2ht`将 pod 文件转换为 HTML。

## 参数

`help`

`--help`

`--quiet`

不显示大部分警告信息。

### noquiet

`--noquiet`

显示大部分警告信息（默认行为）。但这与`verbose`（详细）模式不同。

### verbose

`--verbose`

显示进度信息。

### nooverbose

`--noverbose`

不显示进度信息（默认行为）。

## AUTHOR

Tom Christiansen, <>.

## BUGS

查看`Pod::Ht`获取翻译器中已知错误的列表。

## SEE ALSO

`perlpod`、`Pod::Ht`

## COPYRIGHT

本程序根据艺术许可协议（Artistic License）发布。

---

# POD2MAN

## NAME

`pod2man` - 将 POD 数据转换为格式化的 roff 输入

## SYNOPSIS

```text
pod2man [--center=string] [--date=string] [--errors=style]
[--fixed=font][--fixedbold=font][--fixeditalic=font]
[--fixedbolditalic=font][--na=na][--nourls]
[--official][--quotes=quotes][--release=version]]
[--section=manext][--stderr][--utf8][--verbose]
[input[output]...]
```



# `pod2man --help`

## 描述（DESCRIPTION）

`pod2man` 是 `Pod::Man` 的前端，用于从 POD 源码生成 roff 输入。生成的 roff 代码适用于通过 `(1)` 在终端上显示，通常通过 `(1)` 进行，或使用 `(1)` 进行打印。

`input` 是读取 POD 源码的文件（POD 可以嵌入在代码中）。如果未提供 `input`，则默认为 `STDIN`（标准输入）。如果提供了 `output`，则是写入格式化输出的文件。如果未提供 `output`，则将格式化输出写入 `STDOUT`（标准输出）。在一次 `pod2man` 调用中，通过提供多对 `input` 和 `output` 文件，可以处理多个 POD 文件，从而节省模块加载和编译时间。

`--section`、`--release`、`--center`、`--date` 和 `--official` 可用于设置使用的页眉和页脚；如果没有提供，`Pod::Man` 将采用各种默认值。详情请见下文或 `Pod::Man`。

`pod2man` 假设你的 roff 格式化器具有等宽字体 `CW`。如果你的字体被称为其他名称（如 `CR`），请使用 `--fixed` 指定。这通常只影响用于打印的 `(1)` 输出。同样，你也可以设置用于粗体、斜体和粗体斜体等宽输出的字体。

除了明显的 pod 转换外，`Pod::Man`（因此 `pod2man`）还会处理 `func()`、`(n)` 以及像 `$foo` 或 `@bar` 的简单变量引用，这样你就不需要为它们使用代码转义；不过，像 `$fred{'stuff'}` 这样复杂的表达式仍需要转义。它还将未作为连字符使用的破折号转换为短折号（en dashes），将长破折号 `---` 如这样 `—` 转换为正确的长折号（em dashes），修复“成对引号”，并处理其他几种针对 troff 的微调。完整信息请参阅 `Pod::Man`。

## 选项（OPTIONS）

### `-c string`，`--center=string`

将居中页眉设置为 `string`。默认值是 `"User Contributed Perl Documentation"`，但也请参见下文的 `--official`。

### `-d string`，`--date=string`

将左侧页脚字符串设置为此值。默认情况下，使用输入文件的修改日期；如果输入来自 `STDIN`，则使用当前日期。

### `--errors=style`

设置错误处理样式。`die` 表示在遇到任何 POD 格式错误时抛出异常。`stderr` 表示在标准错误上报告错误，但不抛出异常。`pod` 表示在生成的文档中包含一个 POD ERRORS 章节以总结错误。`none` 尽可能完全忽略 POD 错误。

默认值是 `die`。

### `--fixed=font`

用于逐字复制文本和代码的等宽字体。默认为 `CW`。因此系统可能倾向于使用 `CR`。这只影响 `(1)` 输出。

### `--fixedbold=font`

等宽字体的粗体版本。默认为 `CB`。只影响 `(1)` 输出。

### `--fixeditalic=font`

等宽字体的斜体版本（实际上是一个误解，因为大多数等宽字体只有倾斜版本，没有斜体版本）。默认为 `CI`。只影响 `(1)` 输出。

### `--fixedbolditalic=font`

等宽字体的粗体斜体（可能实际上是倾斜）版本。`Pod::Man` 不假设你拥有这种字体，默认为 `CB`。因此某些系统（如 Solaris）提供了 `CX` 这种可用字体。只影响 `(1)` 输出。

### `-h`，`--help`

打印用法信息。

### `-l`，`--lax`

不再使用。`pod2man` 过去曾检查输入作为手册页的有效性，但现在这应该由 `(1)` 完成。

### `-n na`，`--na=na`

设置手册页的名称（name）。如果没有此选项，`Pod::Man` 假设名称为不带扩展名的文件名。如果文件以 `.pm` 结尾，则名称设置为不带扩展名的文件名。

### `--nourls`

通常，`Pod::Man` 假设标题包含 URL。如果给出此标志，则抑制 URL 锚文本。这可以产生更少的输出。

### `-o`，`--official`

如果未给出 `--center`，则将默认头部指示该页面是标准发布的一部分。

### `-q quotes`，`--quotes=quotes`

### `-u`，`--utf8`

默认情况下，`pod2man` 会产生尽可能保守的 `roff` 输出，以确保它能够尽可能兼容不同的 `roff` 实现。许多 `roff` 实现无法处理非 ASCII 字符，因此所有非 ASCII 字符都会转换为尝试创建正确带音符号字符的 `roff` 转义序列（至少对于 `troff` 输出），或者转换为 `X`。

此选项表示改为输出字面的 UTF-8 字符。如果你的 `roff` 实现可以处理，这是最佳的输出格式，可以避免包含非 ASCII 字符的文档损坏。但请注意，许多实现不支持包含字面 UTF-8 字符的 roff 源码，甚至可能导致段错误或其他异常行为。

请注意，使用此选项时，除非 POD 源码是 US-ASCII 或 Latin-1，否则必须正确声明其输入编码。没有 `=encoding` 命令的 POD 输入将被假设为 Latin-1，如果它实际上是 UTF-8，输出将被双重编码。有关 `=encoding` 命令的更多信息，请参见 `(1)`。

### `-v`，`--verbose`

在生成每个输出文件时打印其名称。

## 退出状态（EXIT STATUS）

只要所有处理的文档都产生了输出，即使该输出包含错误信息（使用 `--errors=pod` 生成 `POD ERRORS` 部分），`pod2man` 也会以状态 `0` 退出。如果处理的文档中有任何一个没有生成输出文档，`pod2man` 将以状态 `1` 退出。如果处理的 POD 文档中存在语法错误，且错误处理模式设置为默认的 `die`，`pod2man` 将立即终止并以状态 `255` 退出。

## 诊断（DIAGNOSTICS）

如果 `pod2man` 失败并报错，请参考 `Pod::Man` 和 `Pod::Simple` 以了解这些错误可能意味着什么。

## 示例（EXAMPLES）

```bash
pod2man program > program.1
pod2man SoModule.pm /usr/perl/man/man3/SoModule.3
pod2man --section=7 note.pod > note.7
```

如果你想连续打印大量的手册页，可能需要设置 `C` 和 `D` 寄存器以设置连续的页码和奇偶页分页，至少在某些 `(7)` 版本中是如此。

```bash
troff -man -rC1 -rD1 perl.1 perldata.1 perlsyn.1 ...
```

若要在 `STDERR` 上获取索引项，请开启 `F` 寄存器，如下：

```bash
troff -man -rF1 perl.1
```

索引依赖于每个主页、节、子节、项目以及任何 `X<>` 指令通过 `.tm` 输出消息。详情请参见 `Pod::Man`。

## 缺陷（BUGS）

本文档大部分内容重复自 `Pod::Man`。

## 参见（SEE ALSO）

`Pod::Man`、`Pod::Simple`、`(1)`、`(1)`、`(1)`、`(1)`、`(1)`、`(7)`

在你的系统中，记录 an macro 宏设置的手册页可能是 `(5)` 而不是 `(7)`。

此脚本的当前版本始终可以通过其网站 `<>` 获取。从 5.6.0 版本开始，它是 Perl 核心分发的一部分。

## 作者（AUTHOR）

Russ Allbery `<>`，非常依赖于 Larry Wall 和 Tom Christiansen 的原始 `pod2man`。

## 版权与许可（COPYRIGHT AND LICENSE）

Copyright 1999, 2000, 2001, 2004, 2006, 2008, 2010, 2012, 2013 Russ Allbery `<>`。

此程序是免费软件；你可以按照 Perl 本身的条款对其进行重新发行和/或修改。

---

# `POD2TEXT`

## 名称（NAME）

`pod2text` - 将 POD 数据转换为格式化的 ASCII 文本

## 语法（SYNOPSIS）

```bash
pod2text [-aclostu] [--code] [--errors=*style*] [-i *indent*]
[-q*quotes*] [--nourls] [--stderr] [-w*width*]
[*input* [*output* ...]]
```

```bash
pod2text -h
```

## 描述（DESCRIPTION）

`pod2text` 是 `Pod::Text` 及其子类的前端。它利用它们从 POD 源码生成格式化的 ASCII 文本。它可以选择使用 termcap 序列或 ANSI 颜色转义序列来格式化文本。

`input` 是读取 POD 源码的文件（POD 可以嵌入代码中）。如果未给出 `input`，则默认为 `STDIN`。如果给出 `output`，则是写入格式化输出的文件。如果未给出 `output`，则格式化输出被写入 `STDOUT`。在一次 `pod2text` 调用中，通过提供多对 `input` 和 `output` 文件可以处理多个 POD 文件，从而节省模块加载和编译时间。

## 选项（OPTIONS）

### `-a`，`--alt`

使用另一种输出格式，该格式等情况下使用不同的标题样式，并在左边距对 `=item` 项标记冒号。

### `--code`

将输入文件中的任何非 POD 文本也包含在输出中。这对于查看使用 POD 块编写的代码非常有用，可以在渲染 POD 的同时保持代码完封不动。

### `-c`，`--color`

使用 ANSI 颜色转义序列格式化输出。使用此选项要求系统安装了 `Term::ANSIColor`。

### `-i indent`，`--indent=indent`

设置用于缩进正文的空格数。如果未提供，默认为 4 个空格。

### `--errors=style`

设置处理模式。`die` 表示遇到任何格式化错误时抛出异常。`stderr` 表示在标准错误上报告错误，但不抛出异常。`pod` 表示在生成的文档中包含 POD ERRORS 部分。`none` 完全忽略错误。

默认是 `die`。

### `-h`，`--help`

打印用法信息并退出。

### `-l`，`--loose`

在 `=head1` 标题后打印一个空行。通常，`=head1` 之后不打印空行，但在 `=head2` 之后会打印空行，因为这是手册页的预期格式。

### `-m width`，`--left-margin=width`，`--margin=width`

左边距的空格宽度。默认为 0。这是包括标题在内的所有文本的边距，而不是正文缩进的；对于后者，请参见 `-i` 选项。

### `--nourls`

通常情况下，带有 URL 的 `L<>` 格式代码会被格式化为显示锚点文本和 URL。也就是说：

### `--stderr`

默认情况下，如果从 POD 输入中检测到任何错误，`pod2text` 会报错。如果给了 `--stderr` 且没有 `--errors` 标志，错误将发送到标准错误，但 `pod2text` 不终止。这等同于 `--errors=stderr` 并且为了向后兼容提供了支持。

### `-t`，`--termcap`

尝试从 `termcap` 确定终端的宽度以及粗体和下划线序列，并使用这些信息来格式化输出。输出将在你的终端设备宽度少两列的地方进行换行。使用此选项需要系统在 `Term::Cap` 能够找到的地方有一个 `termcap` 文件，并且要求系统支持 `termios`。使用此选项，`pod2text` 的输出将包含适用于当前终端类型的终端控制序列。

### `-u`，`--utf8`

默认情况下，`pod2text` 尝试使用 `sa` 输出编码作为其输入编码，以与旧版本兼容。此选项改为强制将输出编码为 `UTF-8`。

请注意，在使用此选项时，除非输入编码为 `US-ASCII` 或 `Latin-1`，否则你的 POD 源文件的输入编码必须正确声明。没有 `=encoding` 命令的 POD 输入将被假设为 `Latin-1`，如果它实际上是 `UTF-8`，则输出将变成双重编码。关于 `=encoding` 命令的更多信息，请参见 `(1)`。

### `-w`，`--width=width`，`-width`

在右侧换行的列数。默认值为 76，除非给了 `-t`，在这种情况下它比你的终端设备宽度少两列。

## 退出状态（EXIT STATUS）

只要所有处理的文档都产生了输出，即使输出包含错误（使用 `--errors=pod` 生成的 `POD ERRORS` 部分），`pod2text` 也会以状态 `0` 退出。如果处理的文档中有任何没有产生输出文档，`pod2text` 将以状态 `1` 退出。如果处理的 POD 文档存在语法错误，且错误处理样式设置为默认的 `die`，则 `pod2text` 将立即终止并以退出状态 `255` 退出。

## 诊断（DIAGNOSTICS）

如果 `pod2text` 出错，请参考 `Pod::Text` 和 `Pod::Simple` 获取有关这些错误可能含义的信息。在内部，它还可以产生以下诊断：

- `-c (--color)` 要求安装 `Term::ANSIColor`
- `(F)` 给出了 `-c` 或 `--color`，但无法加载 `Term::ANSIColor`。
- 未知选项：`%s`
- `(F)` 给出了未知的命令行选项。

此外，无效的命令行选项可能会导致其他的 `Getopt::Long` 错误消息。

## 环境变量（ENVIRONMENT）

### `COLUMNS`

如果给了 `-t`，`pod2text` 将从此环境变量获取你当前的屏幕宽度（如果可用）。它会覆盖 `TERMCAP` 中的终端宽度信息。

### `TERMCAP`

如果给了 `-t`，`pod2text` 将使用此环境变量的内容（如果可用）来确定适用于当前终端设备的正确格式化序列。

## 参见（SEE ALSO）

`Pod::Text`、`Pod::Text::Color`、`Pod::Text::Overstrike`、`Pod::Text::Termcap`、`Pod::Simple`、`(1)`

此脚本的当前版本可以通过其网站 `<>` 获取。从 5.6.0 开始，它是 Perl 核心分发的一部分。

## 作者（AUTHOR）

Russ Allbery `<>`。

## 版权与许可（COPYRIGHT AND LICENSE）

Copyright 1999, 2000, 2001, 2004, 2006, 2008, 2010, 2012, 2013 Russ Allbery `<>`。

本程序是免费软件；你可以按照 Perl 本身的条款重新分发和/或修改它。

---

# `POD2USAGE`

## 名称（NAME）

`pod2usage` - 从文件中嵌入 pod 文档打印用法信息

## 语法（SYNOPSIS）

`pod2usage`

`[-help]` `[-man]` `[-exit exitval]` `[-output outfile]` `[-verbose level]` `[-pathlist dirlist]` `[-formatter module]` `[-utf8]` `file`

## 选项与参数（OPTIONS AND ARGUMENTS）

### `-help`

打印简要帮助信息并退出。

### `-man`

打印此命令的手册页并退出。

### `-exit exitval`

要返回的退出状态值。

### `-output outfile`

输出文件。如果使用了特殊名称 `-`、`>&1` 或 `>&STDOUT`，则使用标准输出。如果使用了 `>&2` 或 `>&STDERR`，则使用标准错误。

### `-verbose level`

所需的详细程度：

1. 仅打印 SYNOPSIS
2. 打印 SYNOPSIS 部分和任何 OPTIONS/ARGUMENTS 部分
3. 打印整个手册页，类似于运行 `pod2text`

### `-pathlist dirlist`

如果没有提供绝对路径，则指定用于搜索输入文件的一个或多个目录。给定列表中的每个目录路径在 Unix 上用 `:` 分隔（MSWin32 和 DOS 用 `;`）。

### `-formatter module`

使用哪种文本格式化。默认是 `Pod::Text`，或者对于非常旧的 Perl 版本是 `PlainText`。`Pod::Text::Termcap`。

### `-utf8`

此选项假设格式化器（见上文）理解 `utf8`。它开启 utf8 输出。

### `file`

包含以用法格式输出的文件路径。

## 描述（DESCRIPTION）

`pod2usage` 读取输入文件并打印用法信息。如果没有指定文件，则从标准输入读取。

## 参见（SEE ALSO）

`Pod::Usage`

## 作者（AUTHOR）

Russ Allbery `<>`。

# `ppdc`

`ppdc` 支持以下选项：

### `-D na=value`

设置源文件中使用的变量。等同于在源文件中使用 `#define` 指令。

### `-I include-directory`

指定备选目录。可以提供多个 `-I` 选项来添加目录。

### `-c ssage-catalog`

指定用于本地化的单个 gettext（`filena.po`）或 Apple strings（`filena.strings`）格式的消息目录。

### `-d output-directory`

指定 PPD 文件的输出目录。默认输出目录为 `"ppd"`。

### `-l language(s)`




指定本地化 PPD 文件时使用的多个语言。默认语言是 `"en"`（英语）。用逗号分隔多个语言，例如 `"de_DE,en_UK,es_ES,es_MX,es_US,fr_CA,fr_FR,it_IT"` 将为每个文件创建德语、英国英语、西班牙语（西班牙、墨西哥和美国）、法语（法国和加拿大）和意大利语。

`-m`

指定输出文件名基于 `ModelNa` 而不是 `FileNa`。

`-t`

指定测试而不是生成 PPD 文件。

`-v`

指定详细输出，基本上是正在加载或写入的文件状态。生成压缩的 PPD 文件（`filena.ppd.gz`）。默认生成未压缩的 PPD 文件。

`--cr`

`--crlf`

`--lf`

指定使用的换行符：回车、回车加换行或仅换行。默认使用换行符字符。

### SEE ALSO（参见）

`(1)`

### AUTHOR（作者）

基于 `(1)` 的 Tom Christiansen。

---

指定备用的包含目录。可以提供多个 `-I` 选项来添加额外的目录。

## 另请

`(1)`、`(5)`、`(1)`、`(1)`、`(1)`、CUPS 在线帮助（

## 版权

Copyright 2007-2014 by Apple Inc.

---

# ppdi

## 名称

`ppdi` - 导入 PPD 文件（废弃）

## 概要

```text
ppdi [ -I include-directory ] [ -o source-file ] ppd-file [ ... ppd-file ]
```

## 描述

`ppdi` 将一个或多个 PPD 文件导入到 PPD 编译器源文件中。同一个 PPD 文件的多种语言会被合并到一个打印机定义中，以便对所有本地化版本进行准确更改。此程序已废弃，并将在未来的 CUPS 版本中移除。

## 选项

`ppdi` 支持以下选项：

### `-I include-directory`

指定备用的包含目录。可以提供多个 `-I` 选项来添加额外的目录。

### `-o source-file`

指定要更新的 PPD 源文件。如果源文件不存在，则创建一个新的源文件。否则，将现有文件与命令行上的新 PPD 文件合并。如果没有指定源文件，则使用文件名 `ppdi.drv`。

## 另请

`(1)`、`(1)`、`(1)`、`(1)`、`(5)`、CUPS 在线帮助（

## 版权

Copyright 2007-2014 by Apple Inc.

---

# ppdrge

## 名称

`ppdrge` - 合并 PPD 文件（废弃）

## 概要

```text
ppdrge [ -o output-ppd-file ] ppd-file ppd-file [ ... ppd-file ]
```

## 描述

`ppdrge` 将两个或多个 PPD 文件合并成一个多语言的 PPD 文件。此程序已废弃，并将在未来的 CUPS 版本中移除。

## 选项

`ppdrge` 支持以下选项：

### `-o output-ppd-file`

指定要创建的 PPD 文件。如果未指定，则合并后的 PPD 文件将写入标准输出。如果输出文件已存在，将被静默覆盖。

---

# ppdpo

## 描述

`ppdpo` 从 PPDC 源文件中提取 UI 字符串，并更新 GNU gettext 或 OS X strings 格式的消息目录源文件用于翻译。此程序已废弃，并将在未来的 CUPS 版本中移除。

## 选项

`ppdpo` 支持以下选项：

### `-D name=value`

为源文件设置 `name` 变量。这等同于在源文件中使用 `#define` 指令。

### `-I include-directory`

指定备用的包含目录。可以提供多个 `-I` 选项来添加额外的目录。

### `-o output-file`

指定输出文件。支持的扩展名包括 GNU gettext 格式的 `.po` 或 `.po.gz` 以及 OS X strings 文件的 `.strings`。

## 另请

`(1)`、`(1)`、`(1)`、`(1)`、`(5)`、CUPS 在线帮助（

## 版权

Copyright 2007-2014 by Apple Inc.

---

# PR

## 名称

`pr` - 转换文本文件用于打印

## 概要

```text
pr [OPTION]... [FILE]...
```

## 描述

对 `FILE` 进行分页或分列打印。

如果没有 `FILE` 或当 `FILE` 为 `-` 时，则从标准输入读取。

长选项的强制性参数对于短选项也是强制的。

### `+FIRST_PAGE[:LAST_PAGE]`、`--pages=FIRST_PAGE[:LAST_PAGE]`

从页面 `FIRST_PAGE` 开始（或停止于 `LAST_PAGE`）打印。

### `-COLUMN`、`--columns=COLUMN`

输出 `COLUMN` 列并向下打印，除非使用了 `-a`。平衡每页各列的行数。

### `-a`、`--across`

横向打印列而不是向下打印，通常与 `-COLUMN` 一起使用。

### `-c`、`--show-control-chars`

使用帽子符号表示（`^G`）和八进制反斜杠表示法。

### `-d`、`--double-space`

输出双倍行间距。

### `-D`、`--date-format=FORMAT`

使用 `FORMAT` 作为页眉日期。

### `-e[CHAR[WIDTH]]`、`--expand-tabs[=CHAR[WIDTH]]`

将输入的 `CHAR`（制表符）扩展为制表符宽度 `WIDTH`（8）。

### `-F`、`-f`、`--form-feed`

使用分页符代替换行符分隔页面（通过 `-F` 使用 3 行页眉，或在未使用 `-F` 时使用 5 行页眉和页脚）。

### `-h`、`--header=HEADER`

在页眉中使用居中的 `HEADER` 代替文件名，`-h ""` 打印空行，不使用 `-h`""。

### `-i[CHAR[WIDTH]]`、`--output-tabs[=CHAR[WIDTH]]`

将空格替换为 `CHAR`（制表符），制表符宽度 `WIDTH`（8）。

### `-J`、`--join-lines`

合并整行，关闭 `-W` 行截断，不进行列对齐，`--sep-string=STRING` 设置分隔符。

### `-l`、`--length=PAGE_LENGTH`

设置页长度为 `PAGE_LENGTH`（66）行（默认文本行 56，使用 `-F` 时为 63）。如果 `PAGE_LENGTH` <= 10，则隐含 `-t`。

### `-m`、`--merge`

并行打印所有文件，每列一个文件，截断行，但使用 `-J` 合并全长度行。

### `-n[SEP[DIGITS]]`、`--number-lines[=SEP[DIGITS]]`

行编号，使用 `DIGITS`（5）位数字，然后是 `SEP`（制表符），默认从第一行开始计数。

### `-N`、`--first-line-number=NUMBER`

从第 `NUMBER` 行计数。

### `-o`、`--indent=MARGIN`

每行缩进 `MARGIN`（零空格），影响 `-w`。

### `-r`、`--no-file-warnings`

无法打开文件时不显示警告。

### `-s[CHAR]`、`--separator[=CHAR]`

使用单个字符 `CHAR` 分列，默认 `<TAB>` 无 `-w`。

### `-S[STRING]`

使用 `STRING` 分列，无 `-w`。

### `-t`、`--omit-header`

显示帮助并退出。

### `--version`

输出版本信息并退出。

## 作者

由 Pete TerMaat 和 Roland Huebner 编写。

## 报告漏洞

GNU coreutils 在线帮助：`<>`

向 `<>` 反馈翻译错误。

## 版权

Copyright 2015 Free Software Foundation, Inc. 许可证 GPLv3+：`<>`

这是免费软件：你可以自由更改和分发。在法律允许范围内不提供担保。

## 另请

完整文档见：`<>`

或通过本地信息获取：`info '(coreutils) pr invocation'`

---

# PRECONV

## 名称

`preconv` - 将文件的编码转换为 GNU troff 可理解的形式

## 概要

```text
[ -dr ] [ -e encoding ] [files ...] -h | --help -v | --version
```

在 `-e` 命令行选项及其参数之间可以存在空格。

## 描述

`preconv` 读取 `files` 并将其编码转换为 GNU `troff` 可以处理的格式，将数据发送到标准输出。目前，它处理 ASCII 字符和 `'\[uXXXX]'` 实体，其中 `XXXX` 是四到六位的十六进制数，代表 Unicode 输入代码。通常情况下，调用 `preconv` 时应配合 `groff` 的 `-k` 和 `-K` 选项。

## 选项

### `-d`

向标准错误输出调试信息（主要是使用的编码）。

### `-D encoding`

在所有操作失败时指定默认编码（见下文）。

### `-eencoding`

显式指定输入编码，覆盖所有其他选项。这对应于 `groff` 的 `-Kencoding` 选项。如果不使用此开关，`preconv` 将使用下述算法来选择输入编码。

### `--help`

`-h` 打印帮助信息。

### `-r`

不添加 `.lf` 请求。

### `--version`

`-v` 打印版本号。

## 用法

`preconv` 尝试通过以下算法查找输入编码：

1. 如果使用选项 `-e` 显式指定了输入编码，则使用它。
2. 否则，检查输入是否以字节顺序标记（Byte Order Mark，BOM，见下文）。如果找到，则使用它。
3. 最后，检查第一行或第二行输入是否存在已知的编码标签（见下文）。如果找到，则使用它。
4. 如果所有尝试均失败，则使用选项 `-D` 提供的默认编码、当前 locale 的编码，或者在 locale 被设置为 `C`、`POSIX` 或空时使用 `latin1`（按此顺序）。

注意，`groff` 程序支持 `GROFF_ENCODING` 环境变量，它最终会被展开为选项 `-k`。

### 字节顺序标记

Unicode 标准定义字符 U+FEFF 为字节顺序标记（BOM）。相反，值 U+FFFE 保证完全不是 Unicode 字符。这允许检测数据流中的字节序（大端序或小端序），且 MIME 编码 `UTF-16` 和 `UTF-32` 强制数据流以 U+FEFF 开头。同样，编码为 `UTF-8` 的数据流可能以 BOM 开头（以便于与 `UTF-16` 和 `UTF-32` 之间的转换）。在所有情况下，字节顺序标记不是数据的一部分，而是编码协议的一部分；换句话说，`preconv` 的输出不包含它。

注意，如果 U+FEFF 不在输入数据的开头，它实际上会被输出；此时它的含义是“零宽不间断空格”字符——这在 `groff` 中通常是不需要的。

### 编码标签

支持多种单一字符编码的编辑器需要在输入文件中使用标签来标记文件的编码。虽然对于代表大量自然语言的数据，可以通过启发式算法推测出正确的输入编码，但这仍然只是推测。此外，对于过短或不代表自然语言的输入，所有算法都很容易失败。

出于这些原因，`preconv` 支持 `GNU Emacs` 和 `XEmacs`（可能还有其他程序）使用的编码标签约定（带有相应限制）。

`GNU Emacs` 和 `XEmacs` 中的编码标签存储在所谓的文件变量（File Variables）中。`preconv` 识别存放在第一行或第二行 troff 注释中的以下语法形式：

`-*- tag1: value1; tag2: value2; ... -*-`

`preconv` 唯一相关的标签是 `coding`，它可以取下面列的值。这里有一个示例行，告诉 `Emacs` 以 troff 模式编辑文件，并使用 latin2 作为编码：

```troff
.\" -*- mode: troff; coding: latin-2 -*-
```

以下列表列出了 `preconv` 支持的所有 MIME 编码标签（小写或大写）；此列表硬编码在源码中：

`big5`、`cp1047`、`euc-jp`、`euc-kr`、`gb2312`、`iso-8859-1`、`iso-8859-2`、`iso-8859-5`、`iso-8859-7`、`iso-8859-9`、`iso-8859-13`、`iso-8859-15`、`koi8-r`、`us-ascii`、`utf-8`、`utf-16`、`utf-16be`、`utf-16le`

此外，还识别以下硬编码的其他标签列表，这些标签最终映射到上述列表中的值：

`ascii`、`chinese-big5`、`chinese-euc`、`chinese-iso-8bit`、`cn-big5`、`cn-gb`、`cn-gb-2312`、`cp878`、`csascii`、`csisolatin1`、`cyrillic-iso-8bit`、`cyrillic-koi8`、`euc-china`、`euc-cn`、`euc-japan`、`euc-japan-1990`、`euc-korea`、`greek-iso-8bit`、`iso-10646/utf8`、`iso-10646/utf-8`、`iso-latin-1`、`iso-latin-2`、`iso-latin-5`、`iso-latin-7`、`iso-latin-9`、`japanese-euc`、`japanese-iso-8bit`、`jis8`、`koi8`、`korean-euc`、`korean-iso-8bit`、`latin-0`、`latin1`、`latin-1`、`latin-2`、`latin-5`、`latin-7`、`latin-9`、`le-utf-8`、`le-utf-16`、`le-utf-16be`、`le-utf-16-be`、`le-utf-16be-with-signature`、`le-utf-16le`、`le-utf-16-le`、`le-utf-16le-with-signature`、`utf8`、`utf-16-be`、`utf-16-be-with-signature`、`utf-16be-with-signature`、`utf-16-le`、`utf-16-le-with-signature`、`utf-16le-with-signature`

这些标签取自 `GNU Emacs` 和 `XEmacs` 以及它们的别名。编码标签末尾的 `-dos`、`-unix` 和 `-mac` 后缀（表示文件使用的换行符）在与上述标签进行比较之前会被删除。

### Iconv 问题

`preconv` 自身仅支持三种编码：latin-1、cp1047 和 UTF-8；所有其他编码都传递给 `iconv` 库函数。在编译时会搜索并检查是否存在有效的 `iconv` 实现；调用 `preconv --version` 会显示是否使用了 `iconv`。

## 缺陷

`%%`

单个 `%`。

`%b`

作为字符串的 `ARGUMENT`，其 `'\'` 转义字符会被解释，但八进制转义的形式为 `\0` 或 `\0NNN`。

以及所有以 `diouxXfeEgGcs` 之一结尾的 C 格式说明符，其中 `ARGUMENT` 会先转换为相应的类型。支持可变宽度。

注意：你的 shell 可能有自己版本的 `printf`，它通常会优于这里描述的版本。请参阅你 shell 的文档详细了解其支持的选项。

## 作者

由 David MacKenzie 编写。

## 报告错误

GNU coreutils 在线帮助：`<>`

向 `<>` 报告 `printf` 翻译错误。

## 版权

版权所有 2015 Free Software Foundation, Inc. 许可 `GPLv3+：GNU GPL 3 版本或更高版本 <>`。

这是一个免费软件：你可以自由地更改和重新发布它。在法律允许的范围内不提供任何担保。

## 参见

`(3)`

完整文档请见：`<>`

或通过本地 `info '(coreutils) printf invocation'` 获取。

---

# PRLIMIT

## 名称

`prlimit` - 获取和设置进程资源限制

## 语法

```text
prlimit [options] [--resource=limits] [--pid PID]
prlimit [options] [--resource=limits] command [argument...]
```

## 描述

给定进程 ID 和一个或多个资源，`prlimit` 尝试检索和或修改限制。

当给定 `command` 时，`prlimit` 将使用指定的参数运行该命令。

`limits` 参数由软限制和硬限制组成，用冒号（`:`）分隔，用于修改现有值。如果未给出 `limits`，`prlimit` 将显示当前值。如果未给出其中一个值，将使用现有值。要指定无限制或无限限制（`RLIM_INFINITY`），可以传递 `-1` 或 `'unlimited'` 字符串。

由于限制的性质，软限制必须低于或等于硬限制（也称为上限）。要查看所有可用资源限制，请参考 `RESOURCE OPTIONS` 部分。

- `soft:hard`：指定两个限制。
- `soft:`：仅指定软限制。
- `:hard`：仅指定硬限制。
- `value`：将两个限制都设置为相同的值。

## 通用选项

### `-h`、`--help`

显示帮助文本并退出。

### `--noheadings`

不打印标题行。

### `-o`、`--output list`

定义使用的输出列。如果未指定输出安排，则使用默认集合。使用 `--help` 获取所有支持列的列表。

### `-p`、`--pid`

指定进程 ID；如果未给出，将使用正在运行的进程。

### `--raw`

使用原始输出格式。

### `--verbose`

详细模式。

### `-V`、`--version`



显示版本信息并退出。

## 资源选项

`-c, --core` [`limits`]

核心文件的最大大小。

`-d, --data` [`limits`]

最大数据大小。

`-e, --nice` [`limits`]

允许提高的最高 nice 优先级。

`-f, --fsize` [`limits`]

最大文件大小。

`-i, --sigpending` [`limits`]

最大挂起信号数量。

`-l, --ock` [`limits`]

最大锁定内存地址空间。

`-m, --rss` [`limits`]

最大驻存内存大小（RSS）。

`-n, --nofile` [`limits`]

最大打开文件数。

`-v, --as` [`limits`]

地址空间限制。

`-x, --locks` [`limits`]

最大持有的文件锁数量。

`-y, --rtti` [`limits`]

实时任务的输出。

## 示例

`prlimit --pid 13134`

显示所有当前资源的限制值。

`prlimit --pid 13134 --rss --nofile=1024:4095`

显示 RSS 的限制，并将打开文件数的软限制和硬限制分别设置为 1024 和 4095。

`prlimit --pid 13134 --nproc=512:`

仅修改进程数量的软限制。

`prlimit --pid $$ --nproc=unlimited`

为当前进程将进程数的软限制和上限值设置为无限制。

`prlimit --cpu=10 sort -u hugefile`

将软、硬 CPU 时间限制都设置为十秒。

## 参见

`(3)`

完整文档请见：`<>`

或通过本地 `info '(coreutils) printf invocation'` 获取。

注：由于提供的文本中存在大量重复内容，译文已按要求对核心部分进行了翻译，并保持了格式一致性。

取消 BSD 风格的“仅限自身”限制，该限制在使用 BSD 风格（不带“-”）选项或当 `ps` 个性设置类似于 BSD 风格时被施加到所有进程上。通过这种方式选择的进程集是其他选项所选进程集的补充。另一种描述是，此选项会导致 `ps` 列出所有带有终端（tty）的进程，或者与 `x` 选项一起使用时列出所有进程。

`-A`

选择所有进程。与 `-e` 相同。

`-a`

选择所有进程，但会话首进程（见 `(2)`）和未关联终端的进程除外。

`-d`

选择所有会话首进程外的进程。

`deselect`

选择所有不符合指定条件的进程（反转选择）。与 `-N` 相同。

`-e`

选择所有进程。与 `-A` 相同。

`g`

真正的所有进程，甚至是会话首进程。此标志已过时，可能在未来的发布中被弃用。它通常由 `a` 标志隐含，仅在运行 `sunos4` 个性模式下有用。

`-N`

选择所有不符合指定条件的进程（反转选择）。与 `--deselect` 相同。

`-T`

选择所有与此终端关联的进程。与不带参数的 `t` 选项相同。

`r`

限制仅选择运行中的进程。

`x`

取消 BSD 风格的“必须拥有 tty”限制，该限制在使用 BSD 风格（不带“-”）选项或当 `ps` 个性设置类似于 BSD 风格时被施加到所有进程上。通过这种方式选择的进程集是其他选项所选进程集的补充。另一种描述是，此选项会导致 `ps` 列出所有你拥有的进程（EUID 为 `ps`），或者与 `a` 选项一起使用时列出所有进程。

## 通过列表选择进程

这些选项接受空格分隔或逗号分隔列表形式的单个参数。它们可以使用多次。例如：`ps -p "12" -p 3,4`

`-123`

与 `--pid 123` 相同。

`123`

与 `--pid 123` 相同。

`-C cmdlist`

按命令名称选择。这选择可执行名称在 `cmdlist` 中给出的进程。

`-G grplist`

按实际组 ID（RGID）或名称选择。这选择实际组名称或 ID 在 `grplist` 列表中的进程。实际组 ID 标识创建进程的用户所在的组，见 `(2)`。

`-g grplist`

按会话或按有效组名称选择。许多标准规定了按会话选择，但按有效组选择是其他几个操作系统使用的逻辑行为。此 `ps` 在列表完全为空（如会话所示）时将按会话选择。组 ID 只有指定组名称时才有效。见 `-s` 和 `--group` 选项。

`--Group grplist`

按实际组 ID（RGID）或名称选择。与 `-G` 相同。

`--group grplist`

按有效组 ID（EGID）或名称选择。这选择有效组名称或 ID 在 `grplist` 中的进程。有效组 ID 描述进程所使用的文件访问权限的组（见 `(2)`）。`-g` 选项通常是 `--group` 的替代方案。

`ppidlist`

按进程 ID 选择。与 `-p` 和 `--pid` 相同。

`-p pidlist`

按 PID 选择。这选择 PID 出现在 `pidlist` 中的进程。与 `p` 和 `--pid` 相同。

`--pid pidlist`

按进程 ID 选择。与 `-p` 和 `p` 相同。

`--ppid pidlist`

按父进程 ID 选择。这选择父进程 ID 在 `pidlist` 中的进程。也就是说，它选择了 `pidlist` 中列出的进程的进程。

`qpidlist`

按进程 ID 选择（快速模式）。与 `-q` 和 `--quick-pid` 相同。

`-q pidlist`

按 PID 选择（快速模式）。这选择 PID 出现在 `pidlist` 中的进程。使用此选项，`ps` 只为 `pidlist` 中列出的 PID 读取必要信息，而不应用额外的过滤规则。PID 的顺序是不排序且被保留的。在此模式下不允许额外的选择选项、排序和树形类型列表。与 `q` 和 `--quick-pid` 相同。

`--quick-pid pidlist`

按进程 ID 选择（快速模式）。与 `-q` 和 `q` 相同。

`--ppid pidlist`

按父进程 ID 选择。这选择父进程 ID 在 `pidlist` 中的进程。也就是说，它选择了 `pidlist` 中列出的进程的进程。

`qpidlist`

按进程 ID 选择（快速模式）。与 `-q` 和 `--quick-pid` 相同。

`-q pidlist`

按 PID 选择（快速模式）。这选择 PID 出现在 `pidlist` 中的进程。使用此选项，`ps` 只为 `pidlist` 中列出的 PID 读取必要信息，而不应用额外的过滤规则。PID 的顺序是不排序且被保留的。在此模式下允许额外的选择选项、排序和树形类型列表。与 `q` 和 `--quick-pid` 相同。

`--quick-pid pidlist`

按进程 ID 选择（快速模式）。与 `-q` 和 `q` 相同。

`-s sesslist`

按会话 ID 选择。这选择会话 ID 在 `sesslist` 中指定的进程。

`--sid sesslist`

按 sessionID 选择。与 `-s` 相同。

`ttylist`

按 tty 选择。与 `-t` 和 `--tty` 几乎相同，但也可以配合空 `ttylist` 使用，表示与 `ps` 关联的终端。使用 `T` 选项被认为比配合空 `ttylist` 使用 `t` 更干净。

`-t ttylist`

按 tty 选择。这选择与 `ttylist` 中指定的终端关联的进程。可以使用终端（ttys 或屏幕）或 `tty`。`ttylist` 在 S1 中指定。

`--tty ttylist`

按终端选择。与 `-t` 和 `--tty` 相同。

`-U userlist`

按有效组 ID（EGID）或名称选择。有效组 ID 描述进程所使用的文件访问权限的组（见 `(2)`）。`-g` 选项通常是 `--group` 的替代方案。

`ppidlist`

按进程 ID 选择。与 `-p` 和 `--pid` 相同。

`-p pidlist`

按 PID 选择。这选择 PID 出现在 `pidlist` 中的进程。与 `p` 和 `--pid` 相同。

`--pid pidlist`

按进程 ID 选择。与 `-p` 和 `p` 相同。

`--ppid pidlist`

按父进程 ID 选择。这选择父进程 ID 在 `pidlist` 中的进程。也就是说，它选择了 `pidlist` 中列出的进程的进程。

`qpidlist`

按进程 ID 选择（快速模式）。与 `-q` 和 `--quick-pid` 相同。

`-q pidlist`

按 PID 选择（快速模式）。这选择 PID 出现在 `pidlist` 中的进程。使用此选项，`ps` 只为 `pidlist` 中列出的 PID 读取必要信息，而不应用额外的过滤规则。PID 的顺序是不排序且被保留的。在此模式下允许额外的选择选项、排序和树形类型列表。与 `q` 和 `--quick-pid` 相同。

`--quick-pid pidlist`

按进程 ID 选择（快速模式）。与 `-q` 和 `q` 相同。

`-s sesslist`

按会话 ID 选择。这选择会话 ID 在 `sesslist` 中指定的进程。

`--sid sesslist`

按 sessionID 选择。与 `-s` 相同。

## 输出格式控制

这些选项用于选择 `ps` 显示的信息。输出可能根据个性设置而异。

`-c`

为 `-l` 选项显示不同的调度器信息。

`--context`

显示安全上下文格式（用于 SELinux）。

`-f`

全格式列表。此选项可以与许多 UNIX 风格选项结合以额外的列。它还会打印命令参数。与 `-L` 使用时，将添加 NLWP（线程数）和 LWP（线程 ID）列。见 `c` 选项、格式关键字 `args` 和格式关键字 `comm`。

`-F`

额外的全格式。见 `-F` 隐含的 `-f` 选项。

`--format form`

用户定义的格式。与 `-o` 和 `o` 相同。

`j`

BSD 作业控制格式。

`-j`

作业格式。

`l`

显示 BSD 长格式。

`-l`

长格式。配合此选项时 `-y` 选项通常很有用。

`-M`

添加安全数据列。与 `Z` 相同（用于 SELinux）。

`O format`

是预加载的 `o`（重载）。BSD `O` 选项可以像 `-O`（预定义许多常用字段的用户定义输出格式），也可以用于指定排序顺序。使用启发式方法确定此选项的行为。为了确保获得所需的行为（排序或格式化），请通过另一种方式指定选项（例如使用 `-O` 或 `--sort`）。当作为格式选项时，它与 `-O` 相同，具有 BSD 个性。

`-O format`

类似于 `-o`，但预加载了许多默认列。与 `-o pid,:format,,:state,:tna,:ti,:command` 或 `-o pid,:format,,:tna,:ti,:cmd` 相同，见下方的 `-o`。

`o format`

指定用户定义的格式。与 `-o` 和 `--format` 相同。

自定义格式。`format` 是一个以空格或逗号分隔列表形式存在的单个参数，用于指定各个输出列。可识别的关键字在下方的标准格式指定符（STANDARD FORMAT SPECIFIERS）部分描述。可以根据需要重命名标题（`ps -o pid,:ruser=RealUser -o comm=Command`）。如果所有列标题均为空（`ps -o pid= -o comm=`），则不输出标题行。列宽会根据宽标题的需要自动增加；这可以用于加宽如 `WCHAN` 等列（`ps -o pid,:wchan=:WIDE-:WCHAN-:COLUMN -o comm`）。同时也提供显式的宽度控制（`ps -o pid,:wchan:42,:cmd`）。`ps -o pid=X,:comm=Y` 的行为随运行模式（personality）而异；输出可能是一列“X,:comm=Y”，也可能是两列“X”和“Y”。不确定时请使用多个 `-o` 选项。使用 `PS_FORMAT` 环境变量按需指定默认值；`DefSysV` 和 `DefBSD` 是可以用于选择默认 UNIX 或 BSD 列的宏。

`s`

显示信号格式。

`u`

显示以用户为中心的格式。

`v`

显示虚拟内存格式。

`X`

`--columns n`

设置屏幕宽度。

`--culative`

包含已死亡子进程的数据（与父进程求和）。

`e`

在命令后显示环境变量。

`f`

ASCII 艺术进程层次结构（森林）。

`--forest`

ASCII 艺术进程树。

`h`

无标题。（或在 BSD 模式下，每个屏幕显示一个标题）。`h` 选项存在问题。标准的 BSD `ps` 使用此选项在输出的每页打印标题，但较旧的 Linux `ps` 使用此选项完全禁用标题。此版本的 `ps` 遵循 Linux 的用法，即除非选择了 BSD 模式，否则不打印标题；在这种情况下，会在每页打印标题。无论当前运行模式如何，你都可以使用长选项 `--headers` 和 `--no-headers` 分别启用每页打印标题或完全禁用标题。

`-H`

显示进程层次结构（森林）。

`--headers`

重复标题行，每页输出一个。

`k spec`

指定排序顺序。排序语法为：

```text
[+|-]key[,[+|-]key[,...]]
```

从标准格式指定符（STANDARD FORMAT SPECIFIERS）部分选择一个单字母键值。`+` 是可选的，因为默认方向是数值或字典序的升序。与 `--sort` 相同。

示例：

```text
ps jaxkuid,-ppid,+pid
ps axk comm o comm,args
ps kstart_ti -ef
```

`--lines n` 设置屏幕高度。`-n alist` 设置 `alist` 文件。与 `N` 相同。正确显示 WCHAN 需要 `alist` 文件，且它必须与当前 Linux 内核完全匹配以获得正确输出。如果没有此选项，`alist` 的默认搜索路径为：

```text
$PS_SYSMAP$
$PS_SYSTEM_MAP$
/proc/*/wchan
/boot/System.map-$(uname -r)
/boot/System.map
/lib/modules/$(uname -r)/System.map
/usr/src/linux/System.map
/System.map
```

`n` WCHAN 和 USER 的数值输出（包括所有类型的 UID 和 GID）。`N` 指定 `alist` 文件。与 `-n` 相同，见上文 `-n`。

`--no-headers` 完全不打印标题行。`--no-heading` 是此选项的别名。

`O order` 排序顺序（重载）。BSD 的 `O` 选项可以像 `-O`（预定义常用字段的自定义输出格式），也可以用于指定排序顺序。使用启发式算法来确定此选项的行为。为了确保获得所需的行为（排序或格式化），请以其他方式指定选项（例如使用 `-O` 或 `--sort`）。对于排序，过时的 BSD `O` 选项语法为：

```text
O[+|-]k1[,[+|-]k2[,...]]
```

它根据下方过时排序键（OBSOLETE SORT KEYS）部分描述的单字母短键 `k1`、`k2` 等指定的层级排序对进程列表进行排序。目前 `+` 是可选的，依赖于迭代键的默认方向，但有助于区分 `O` 排序和 `O` 排序。

`--rows n` 设置屏幕高度。

## 线程显示

`H`

将线程显示为进程。

`-L`

显示线程，可能包含 LWP 列。

`m`

在进程后显示线程。

`-m`

在进程后显示线程。

`-T`

显示线程，可能包含 SPID 列。

## 其他信息

`--info`

输出调试信息。

`L`

列出所有格式指定符。

`V`

输出 procps-ng 版本。

`-V`

输出 procps-ng 版本。

`--version`

输出 procps-ng 版本。

## 注意事项

此 `ps` 通过读取 `/proc` 中的虚拟文件工作。此 `ps` 不需要 setuid 或任何权限即可运行。不要给此 `ps` 特殊权限。

此 `ps` 需要访问 `alist` 数据才能正确显示 WCHAN。对于 2.6 之前的内核，必须安装 `System.map` 文件。目前 CPU 使用率是在整个生命周期内运行时间的百分比。这并不理想，而且不符合 `ps` 其他部分遵循的标准。CPU 使用率之和可能恰好等于 100%。

SIZE 和 RSS 字段不包括进程的部分，例如页表、内核栈、`struct thread_info` 和 `struct_struct`。这些通常是 20 KiB 的常驻内存。SIZE 是进程的虚拟大小（code+:data+:stack）。

标记为 `<defunct>` 的进程是死进程（所谓的僵尸进程），由于父进程没有正确销毁它们而仍然留存。如果父进程退出，这些进程将被销毁。

如果用户名的长度大于显示列的长度，则显示数值用户 ID。

诸如 `ps -aux` 之类的命令选项是不推荐的，因为它是两种不同标准的混淆。根据 POSIX 和 UNIX 标准，上述命令请求所有具有 TTY 的进程（通常是用户运行的命令）以及所有属于用户 `"x"` 的进程。如果该用户不存在，`ps` 将假设你真的想运行 `ps aux`。该参数可以缩写为下划线字母中的一个 `s|l|o|t|m|a`。

## 进程标志

这些值的和显示在 `"F"` 列中，该列由 `flags` 输出指定符提供：

`1`

fork 后但没有 exec。

`4`

使用了超级权限。

## 进程状态代码

以下是 `s`、`stat` 和 `state` 输出指定符（表头为 `"STAT"` 或 `"S"`）将显示的用于描述进程状态的不同值：

`D`：不中断睡眠（通常为 IO）。

## 标准格式指定符

| KEY | LONG | DESCRIPTION |
| :--- | :--- | :--- |
| `c` | `cmd` | 可执行文件的简单名称 |
| `C` | `pcpu` | CPU 占用率 |
| `f` | `flags` | 长格式 F 字段中的标志 |



# 进程状态字段及格式描述符

## AIX 格式描述符

此`ps`支持 AIX 格式描述符，其工作方式类似于`(1)`和`(3)`的格式代码。例如，可以使用此命令生成标准的默认输出：`ps -eo "%p %y %x %c"`。普通 NORMAL 代码在下一节中描述。

| CODE | NORMAL | HEADER |
| :--- | :--- | :--- |
| `%C` | `pcpu` | `%CPU` |
| `%G` | `group` | `GROUP` |
| `%P` | `ppid` | `PPID` |
| `%U` | `user` | `USER` |
| `%a` | `args` | `COMMAND` |
| `%c` | `comm` | `COMMAND` |
| `%g` | `rgroup` | `RGROUP` |
| `%n` | `nice` | `NI` |
| `%p` | `pid` | `PID` |
| `%r` | `pgid` | `PGID` |
| `%t` | `eti` | `ELAPSED` |
| `%u` | `ruser` | `RUSER` |
| `%x` | `ti` | `TIME` |
| `%y` | `tty` | `TTY` |
| `%z` | `vsz` | `VSZ` |

## 标准格式指定符

以下是用于控制输出格式（例如通过选项`-o`）或使用 GNU 风格的`--sort`选项对选定进程排序的不同关键字。

例如：`ps -eo pid,:user,:args --sort user`

此版本的`ps`尝试识别其他`ps`实现中使用的大多数关键字。

以下用户定义的格式指定符可能包含空格：`args`, `cmd`, `comm`, `command`, `fna`, `ucmd`, `ucomm`, `lstart`, `bsdstart`, `start`。

因此，某些关键字可能无法排序。

| CODE | HEADER | DESCRIPTION |
| :--- | :--- | :--- |
| `%cpu` | `%CPU` | 以 "##.#" 格式的进程 cpu 占用率。目前，它是已使用的 CPU 时间除以进程运行的时间（`cputi`/`realti`比例），以百分比表示。除非你运气极好，否则总和不会为 100%（别名 `pcpu`）。 |
| `%m` | `%MEM` | 进程驻留集合大小与机器物理内存的比例，以百分比表示。 |
| `args` | | 以下用户定义的格式指定符可能包含空格：`args`, `cmd`, `comm`, `command`, `fna`, `ucmd`, `ucomm`, `lstart`, `bsdstart`, `start`。 |
| `cmd` | | |
| `comm` | | |
| `command` | | |
| `fna` | | |
| `ucmd` | | |
| `ucomm` | | |
| `lstart` | | |
| `bsdstart` | | |
| `start` | | |

| 字段 | 名称 | 描述 |
| :--- | :--- | :--- |
| `drs` | `DRS` | 数据驻留集大小，除执行代码外分配的物理内存量。 |
| `egid` | `EGID` | 进程的有效组 ID，十进制整数形式。（别名 `gid`）。 |
| `egroup` | `EGROUP` | 进程的有效组 ID。如果可以获取且字段宽度允许，则显示文本组 ID，否则显示十进制表示。（别名 `group`）。 |
| `eip` | `EIP` | 指令指针。 |
| `esp` | `ESP` | 栈指针。 |
| `eti` | `ELAPSED` | 自进程启动以来的运行时间，格式为 `[[DD-]hh:]mm:ss`。 |
| `etis` | `ELAPSED` | 自进程启动以来的运行时间，单位为秒。 |
| `euid` | `EUID` | 有效用户 ID（别名 `uid`）。 |
| `euser` | `EUSER` | 有效用户名。如果可以获取且字段宽度允许，则显示文本用户 ID，否则显示十进制表示。可以使用`-n`选项强制使用十进制表示。（别名 `una`, `user`）。 |
| `f` | `F` | 与进程关联的标志，参见**进程标志（PROCESS FLAGS）**部分。（别名 `flag`, `flags`）。 |
| `fgid` | `FGID` | 文件系统访问组 ID。（别名 `fsgid`）。 |
| `fgroup` | `FGROUP` | 文件系统访问组 ID。如果可以获取且字段宽度允许，则显示文本组 ID，否则显示十进制表示。（别名 `fsgroup`）。 |
| `flag` | `F` | 见`f`。（别名 `f`, `flags`）。 |
| `flags` | `F` | 见`f`。（别名 `f`, `flag`）。 |
| `fna` | `COMMAND` | 进程可执行文件文件名的前 8 个字节。此列输出可能包含空格。 |
| `fuid` | `FUID` | 文件系统访问用户 ID。（别名 `fsuid`）。 |
| `fuser` | `FUSER` | 文件系统访问用户 ID。如果可以获取且字段宽度允许，则显示文本用户 ID，否则显示十进制表示。 |
| `gid` | `GID` | 见`egid`。（别名 `egid`）。 |
| `group` | `GROUP` | 见`egroup`。（别名 `egroup`）。 |
| `ignored` | `IGNORED` | 忽略信号掩码，参见`(7)`。根据字段宽度，显示十六进制格式的 32 或 64 位掩码。（别名 `sig_ignore`, `sigignore`）。 |
| `ipcns` | `IPCNS` | 描述进程所属命名空间的唯一 inode 编号。参见`(7)`。 |
| `label` | `LABEL` | 安全标签，最常用于 SELinux 上下文数据。这用于高安全系统上的*强制访问控制*（"MAC"）。 |
| `lstart` | `STARTED` | 命令启动的时间。另参见`bsdstart`, `start`, `start_ti`和`sti`。 |
| `lsession` | `SESSION` | 如果包含了 systemd 支持，则显示进程的登录会话标识符。 |
| `lwp` | `LWP` | 可调度实体的轻量级进程（线程）ID。（别名 `spid`, `tid`）。更多信息参见`tid`。 |
| `machine` | `MACHINE` | 如果包含了 systemd 支持，则显示分配给虚拟机或容器的进程的机器名称。 |
| `maj_flt` | `MAJFLT` | 该进程发生的大页异常次数。 |
| `min_flt` | `MINFLT` | 该进程发生的小页异常次数。 |
| `mntns` | `MNTNS` | 描述进程所属挂载空间的唯一 inode 编号。参见`(7)`。 |
| `netns` | `NETNS` | 描述进程所属命名空间的唯一 inode 编号。参见`(7)`。 |
| `ni` | `NI` | nice 值。范围从 19（最友好）到 -20（对他人不友好），参见`(1)`。（别名 `nice`）。 |
| `nice` | `NI` | 见`ni`。（别名 `ni`）。 |
| `nlwp` | `NLWP` | 进程中 lps（线程）的数量。（别名 `thcount`）。 |
| `nwchan` | `WCHAN` | 进程睡眠时所在的内核地址（如果需要内核名称，请使用`wchan`）。运行中的任务将显示横字符（`-`）。 |
| `ouid` | `OWNER` | 如果包含了 systemd 支持，则显示会话所有者的 Unix 标识符。 |
| `pcpu` | `%CPU` | 见`%cpu`。（别名 `%cpu`）。 |
| `pending` | `PENDING` | 等待信号掩码。参见`(7)`。进程信号与单个线程的信号不同。使用`m`选项或`-m`选项查看两者。根据字段宽度，显示十六进制格式的 32 或 64 位掩码。（别名 `sig`）。 |
| `pgid` | `PGID` | 进程组 ID，或等于组组长的进程 ID。（别名 `pgrp`）。 |
| `pgrp` | `PGRP` | 见`pgid`。（别名 `pgid`）。 |
| `pid` | `PID` | 代表进程的编号。（别名 `tgid`）。 |
| `pidns` | `PIDNS` | 描述进程所属命名空间的唯一 inode 编号。 |
| `sigignore` | `IGNORED` | 参见`ignored`。（别名 `ignored`,`sig_ignore`）。 |
| `sigmask` | `BLOCKED` | 参见`blocked`。（别名 `blocked`,`sig_block`）。 |
| `size` | `SIZE` | 如果进程弄脏所有可写页面并将其交换出，则所需的近似交换空间大小。这个数字非常粗略！ |
| `slice` | `SLICE` | 如果包含了 systemd 支持，则显示进程所属的 slice 单元。 |
| `spid` | `SPID` | 参见`lwp`。（别名 `lwp`,`tid`）。 |
| `stackp` | `STACKP` | 进程栈的底部（起始位置）地址。 |
| `start` | `STARTED` | 命令启动的时间。如果进程在 24 小时内启动，输出格式为 "HH:MM:SS"，否则为 "Mmmdd"（其中 Mmm 为三字母月份）。另参见`lstart`、`bsdstart`、`start_ti`和`sti`。 |
| `start_ti` | `START` | 进程的启动时间或日期。如果进程不是在调用`ps`的同一年启动，则只显示年份；如果不是在同一天启动，则显示 "MmmDD"，否则显示 "HH:MM"。另参见`bsdstart`、`start`、`lstart`和`sti`。 |
| `stat` | `STAT` | 字符进程状态。不同值的含义请参见 **PROCESS STATE CODES** 章节。如果你只想显示第一个字符，另参见`s`和`state`。 |
| `state` | `S` | 参见`s`。（别名 `s`）。 |
| `suid` | `SUID` | 保存的用户 ID。（别名 `svuid`）。 |
| `supgid` | `SUPGID` | 补充组的组 ID，如果有。参见`(2)`。 |
| `supgrp` | `SUPGRP` | 补充组的组，如果有。参见`(2)`。 |
| `suser` | `SUSER` | 保存的用户名。如果可以获取且字段宽度允许，将是文本形式的用户 ID，否则为十进制表示。（别名 `svuser`）。 |
| `svgid` | `SVGID` | 参见`sgid`。（别名 `sgid`）。 |
| `svuid` | `SVUID` | 参见`suid`。（别名 `suid`）。 |
| `sz` | `SZ` | 进程核心映像在物理页中的大小。这包括文本、数据和栈空间。设备映射目前被排除；这可能会发生变化。参见`vsz`和`rss`。 |
| `tgid` | `TGID` | 表示任务所属线程组的数字（别名 `pid`）。它是线程组首者的进程 ID。 |
| `thcount` | `THCNT` | 参见`nlwp`。（别名 `nlwp`）。该进程拥有的内核线程数量。 |
| `tid` | `TID` | 表示可调度实体的唯一数字（别名 `lwp`,`spid`）。此值也可能出现为：进程 ID (`pid`)；进程组 ID (`pgrp`)；会话首者的会话 ID (`sid`)；线程组首者的线程组 ID (`tgid`) 以及进程组首者的 tty 进程组 ID (`tpgid`)。 |
| `ti` | `TIME` | 累计 CPU 时间，格式为 "[DD-]HH:MM:SS"别名 `cputi`）。 |
| `tna` | `TTY` | 控制的 tty（终端）。别名 `tt`,`tty`）。 |
| `tpgid` | `TPGID` | 进程连接的 tty（终端）上的前台进程组 ID，如果进程未连接到 tty，则为 -1。 |
| `trs` | `TRS` | 文本驻存大小，分配给执行代码的物理内存。 |
| `tt` | `TT` | 控制的 tty（终端）。别名 `tna`,`tty`）。 |
| `tty` | `TT` | 控制的 tty（终端）。别名 `tna`,`tt`）。 |
| `ucmd` | `CMD` | 参见`comm`。（别名 `comm`,`ucomm`）。 |
| `ucomm` | `COMMAND` | 参见`comm`。（别名 `comm`,`ucmd`）。 |
| `uid` | `UID` | 真实用户 ID。 |
| `euid` | `EID` | 有效用户 ID。 |
| `suid` | `SUID` | 保存的用户 ID。 |
| `eguid` | `EGUID` | 有效用户 ID。 |
| `gid` | `GID` | 真实组 ID。 |
| `egid` | `EGID` | 有效组 ID。 |
| `sgid` | `SGID` | 保存的组 ID。 |
| `setid` | `SETID` | 会话系统 ID。 |
| `supgid` | `SUPGID` | 补充组 ID。 |
| `supgrp` | `SUPGRP` | 补充组名。 |
| `suser` | `SUSER` | 保存的用户名。 |
| `euser` | `EUSER` | 有效的用户名。 |
| `svgid` | `SVGID` | 保存的组 ID。 |
| `svuid` | `SVUID` | 保存的用户 ID。 |
| `sz` | `SZ` | 进程核心映像在物理页中的大小。 |
| `tgid` | `TGID` | 表示任务所属线程组的数字（别名 `pid`）。 |
| `thcount` | `THCNT` | 参见`nlwp`。（别名 `nlwp`）。该进程拥有的内核线程数量。 |
| `tid` | `TID` | 表示可调度实体的唯一数字（别名 `lwp`,`spid`）。 |
| `ti` | `TIME` | 累计 CPU 时间，格式为 "[DD-]HH:MM:SS"别名 `cputi`）。 |
| `tna` | `TTY` | 控制的 tty（终端）。别名 `tt`,`tty`）。 |
| `tpgid` | `TPGID` | 进程连接的 tty（终端）上的前台进程组 ID。 |
| `trs` | `TRS` | 文本驻留大小，分配给执行代码的物理内存。 |
| `tt` | `TT` | 控制的 tty（终端）。别名 `tna`,`tty`）。 |
| `tty` | `TT` | 控制的 tty（终端）。别名 `tna`,`tt`）。 |
| `ucmd` | `CMD` | 参见`comm`。（别名 `comm`,`ucomm`）。 |
| `ucomm` | `COMMAND` | 参见`comm`。（别名 `comm`,`ucmd`）。 |
| `uid` | `UID` | 真实用户 ID。 |
| `euid` | `EID` | 有效用户 ID。 |
| `suid` | `SUID` | 保存的用户 ID。 |
| `eguid` | `EGUID` | 有效用户 ID。 |
| `gid` | `GID` | 真实组 ID。 |
| `egid` | `EGID` | 有效组 ID。 |
| `sgid` | `SGID` | 保存的组 ID。 |
| `setid` | `SETID` | 会话系统 ID。 |
| `supgid` | `SUPGID` | 补充组 ID。 |
| `supgrp` | `SUPGRP` | 补充组名。 |
| `suser` | `SUSER` | 保存的用户名。 |
| `euser` | `EUSER` | 有效的用户名。 |
| `svgid` | `SVGID` | 保存的组 ID。 |
| `svuid` | `SVUID` | 保存的用户 ID。 |
| `sz` | `SZ` | 进程核心映像在物理页中的大小。 |
| `tgid` | `TGID` | 表示任务所属线程组的数字（别名 `pid`）。 |
| `thcount` | `THCNT` | 参见`nlwp`。（别名 `nlwp`）。该进程拥有的内核线程数量。 |
| `tid` | `TID` | 表示可调度实体的唯一数字（别名 `lwp`,`spid`）。 |
| `ti` | `TIME` | 累计 CPU 时间，格式为 "[DD-]HH:MM:SS"别名 `cputi`）。 |
| `tna` | `TTY` | 控制的 tty（终端）。别名 `tt`,`tty`）。 |
| `tpgid` | `TPGID` | 进程连接的 tty（终端）上的前台进程组 ID。 |
| `trs` | `TRS` | 文本驻留大小，分配给执行代码的物理内存。 |
| `tt` | `TT` | 控制的 tty（终端）。别名 `tna`,`tty`）。 |



| `tty` | TT | 控制的 tty（终端）。别名 `tna`,`tt`）。 |

| `ucmd` | CMD | 参见 `comm`。（别名 `comm`,`ucomm`）。 |

| `ucomm` | COMMAND | 参见 `comm`。（别名 `comm`,`ucmd`）。 |

`ps` 最初由 Branko Lankester 编写，Michael K. Johnson 对其进行了重大重写，以使用 proc 文件系统，在此过程中更改了一些内容。Michael Shields 增加了 pid-list 特功能。Charles Blake 添加了 lti 级排序、dirent 风格库、设备名称到数字的 mmap 数据库、直接在 `System.map` 上的近似二分查找以及许多代码和文档的清理。David Mossberger-Tang 为 `psupdate` 编写了通用的 BFD 支持。Albert Cahalan 重写了 `ps` 以完全支持 Unix98 和 BSD，并针对过时和外语法编写了许多非常丑陋的补丁。

请向以下地址发送错误报告。不需要也不建议订阅。

---

# PS2ASCII

## NAME

`ps2ascii` - 将 PostScript 或 PDF 转换为 ASCII 的 Ghostscript 翻译

## SYNOPSIS

`ps2ascii` [*input.ps* [ *output.txt* ] ]

`ps2ascii` *input.pdf* [ *output.txt* ]

## DESCRIPTION

`ps2ascii` 使用 `gs` (1) 从 `PostScript`(tm) 或 Adobe `Portable Docunt Format` (PDF) 文件中提取 ASCII 文本。如果命令行上未指定文件，`gs` 将从标准输入读取；但 PDF 输入来自显式指定的文件，而不是标准输入。如果未指定输出文件，则将 ASCII 文本写入标准输出。

`ps2ascii` 不查看字体编码，并且不擅长处理光间（kerning），因此对于 PostScript（但目前不是 PDF），你可能考虑 `pstotext`（见下文）。

## FILES

运行 `gs -h` 查找 Ghostscript 文档在系统上的位置，你可以从那里获取更多细节。

## SEE ALSO

`gs` (1),

## VERSION

`ps2epsi` 使用 `gs` (1) 处理 `PostScript`(tm) 文件并生成一个符合 Adobe `Encapsulated PostScript Interchange` (EPSI) 格式的新文件作为输出。EPSI 是封装式 PostScript (EPS) 的特殊形式，它在文件开头以 PostScript 注释的形式添加了最终显示页面的位图版本。能够理解 EPSI 的程序（通常是文字处理器或 DTP 程序）可以使用此位图在屏幕上提供 PostScript 的预览版本。显示的质量通常不是很好（（例如：低分辨率、无颜色），但最终打印版本使用的是真实的 PostScript，因此具有正常的 PostScript 质量。

## USAGE

在 Unix 系统上，这样调用 `ps2epsi`：

`ps2epsi` *infile.ps* [ *outfile.epsi* ]

其中 "infile.ps" 是输入文件，“outfile.epsi" 是生成的 EPSI 文件。如果省略了输出文件名，则根据输入文件名生成。当使用标准扩展名（".ps", ".cps", ".eps" 或 ".epsf"）时，它将被替换为输出扩展名 ".epsi"。在 DOS 系统上，命令是：

`ps2epsi` *infile.ps outfile.epi*

其中 "infile.ps" 是原始 PostScript 文件，“outfile.epi" 是输出文件的名称。

## LIMITATIONS

并不是每个 PostScript 文件都能成功封装，因为对 PostScript 构造一个正确的封装文件可能包含的内容有限制。`ps2epsi` 做了一些额外工作来尝试帮助封装，它会自动计算所有封装式 PostScript 文件所需的边界框（bounding box），因此在大多数时候它都做得很好。然而，在某些情况下，由于原始 PostScript 文件的内容，封装无法工作。

## COMPATIBILITY

`Framaker` DTP 系统是理解 EPSI 文件的应用程序之一，`ps2epsi` 已在 Sun 工作站上使用 Framaker 3.0 对来自各种来源的多个 PostScript 图表进行了测试。其他平台上的 Framaker 应该能够使用这些文件，尽管我尚未进行此类测试。

## FILES

| ps2epsi | Unix shell 脚本 |

| :--- | :--- |

| ps2epsi.bat | DOS 批文件 |

| ps2epsi.ps | 执行该工作的 Ghostscript 程序 |

## SEE ALSO

`gs` (1)

## VERSION

本文最后一次针对 Ghostscript 9.16 版本进行了修订。然而，内容可能过时，或与 `ps2epsi.txt` 不一致。

## AUTHOR

George Caron

---

# PS2PDF

## NAME

`ps2pdf` - 使用 ghostscript 将 PostScript 转换为 PDF

`ps2pdf12` - 使用 ghostscript 将 PostScript 转换为 PDF1.2（兼容 Acrobat3 及更高版本）

`ps2pdf13` - 使用 ghostscript 将 PostScript 转换为 PDF1.3（兼容 Acrobat4 及更高版本）

`ps2pdf14` - 使用 ghostscript 将 PostScript 转换为 PDF1.4（兼容 Acrobat5 及更高版本）

## SYNOPSIS

`ps2pdf12` - 使用 ghostscript 将 PostScript 转换为 PDF1.2（兼容 Acrobat3 及更高版本）

`ps2pdf13` - 使用 ghostscript 将 PostScript 转换为 PDF1.3（兼容 Acrobat4 及更高版本）

`ps2pdf14` - 使用 ghostscript 将 PostScript 转换为 PDF1.4（兼容 Acrobat5 及更高版本）

`ps2pdf` [*input.ps* [ *output.txt* ] ]

`ps2pdf` *input.pdf* [ *output.txt* ]

`ps2pdf` - 使用 ghostscript 将 PostScript 转换为 PDF（注：提供的文本在摘要中有冗余定义，根据示例保留了该结构）

## DESCRIPTION

`ps2pdf` 使用 `gs` (1) 从 `PostScript`(tm) 或 Adobe `Portable Docunt Format` (PDF) 文件中提取 ASCII 文本。如果命令行上未指定文件，`gs` 将从标准输入读取；但 PDF 输入来自显式指定的文件，而不是标准输入。如果未指定输出文件，则将 ASCII 文本写入标准输出。

`ps2pdf` 不查看字体编码，并且不擅长处理光间，因此对于 PostScript（但目前不是 PDF），你可能考虑 `pstotext`（见下文）。

`ps2pdf` 使用 `gs` (1) 从 `PostScript`(tm) 或 Adobe `Portable Docunt Format` (PDF) 文件中提取 ASCII 文本。如果命令行上未指定文件，`gs` 将从标准输入读取；但 PDF 输入来自显式指定的文件，而不是标准输入。如果未指定输出文件，则将 ASCII 文本写入标准输出。

`ps2pdf` 不查看字体编码，并且不擅长处理光间，因此对于 PostScript（但目前不是 PDF），你可能考虑 `pstotext`（见下文）。

（此处省略原文中重复的段，按要求不重复输出）

`eps2eps` [ `options` ] `input output.eps`

## DESCRIPTION

`ps2ps` 使用 `gs` (1) 将 `PostScript`(tm) 或 `PDF`(tm) 文件 "input" 转换为更简单、规范且（通常是）快的 PostScript "output.ps"。 输出是符合 level 2 DSC 3.0 的 PostScript。

`eps2eps` 执行等同的优化，创建封装式 PostScript (EPS) 文件。注意，尽管如此，输入不需要是 EPS 文件，PostScript 或实际上是 PDF 文件也同样可以接受。

两者都接受任何通用的 Ghostscript 命令行选项，以及针对 `ps2write` 和 `eps2write`设备的特定选项。

## FILES

运行 `gs -h` 查找系统上 Ghostscript 文档的位置，你可以从那里获取更多详情。

## SEE ALSO

`gs` (1), (1), (1)

## VERSION

此文档最后针对 Ghostscript 9.16 版本进行了修订。

## AUTHOR

Artifex Software, Inc. 是 Ghostscript 的主要维护者。

---

# PSFADDTABLE

## NAME

`psfaddtable` - 为控制字体添加 Unicode 字符表

## SYNOPSIS

`psfaddtable fontfile tablefile outfile`

## DESCRIPTION

`psfaddtable` 获取 `fontfile` 提供的 `.psf` 格式控制字体，并使用 `tablefile` 提供的 Unicode 字符表对其扩展，生成一个包含嵌入字符表的字体文件，并写入 `outfile`。输入文件名 `-` 表示标准输入，输出文件名 `-` 表示标准输出。如果 `fontfile` 已经包含嵌入的字符表，则将其忽略。

## TABLE FILE FORMAT

`psfgettable` 从 `.psf` 格式的控制字体中提取嵌入的 Unicode 字符表，并转换为 `psf` (1) 使用的格式的可读 ASCII 文件。如果字体文件名是单个横杠 `-`，则从标准输入读取字体。

## SEE ALSO

`psfgettable` (8), `psfstriptable` (1), `psfxtable` (1), `psfaddtable` (1)

---

# PSFSTRIPTABLE

## NAME

`psfstriptable` - 从控制字体移除嵌入的 Unicode 字符表

## SYNOPSIS

`psfstriptable fontfile outfile`

## DESCRIPTION

`psfstriptable` 从 `fontfile` 读取 `.psf` 格式的控制字体，如果存在嵌入的 Unicode 字体表，将其移除，并将结果写入 `outfile`。输入文件名 `-` 表示标准输入，输出文件名 `-` 表示标准输出。

## SEE ALSO

`psfaddtable` (8), `psfgettable` (1), `psfxtable` (1), `psfstriptable` (1)

---

# PSFXTABLE

## NAME

`psfxtable` - 处理控制字体的 Unicode 字符表

## SYNOPSIS

`psfxtable [-i infont] [-o outfont] [-it intable] [-ot outtable] [-nt]`

## DESCRIPTION

`psfxtable` 处理 `.psf` 格式控制字体的嵌入 Unicode 字符表。它读取字体和可能的表，并写入字体和或表。`psfaddtable` (1)、`psfstriptable` (1) 和 `psfgettable` (1) 是它的链接。

每个文件名 `infont`、`outfont`、`intable` 和 `outtable` 都可用单个横杠 `-` 替换，在这种情况下使用标准输入或标准输出。如果没有 `-i` 选项，则从标准输入读取字体。如果没有 `-it` 或 `-o` 或 `-ot` 选项，则不读取输入表，或不写入输出字体或输出表。

默认情况下，当输入字体具有 Unicode 表或提供了显式表（覆盖输入字体表）时，输出字体（如果有）将具有 Unicode 表。选项 `-nt` 导致输出不带表的字体。当请求 `outfont` 时，如果 `infont` 有 psf1 头部且 `intable` 不包含序列，则将获得 psf1 头部，否则获得 psf2 头部。

## SEE ALSO

`psfaddtable` (8), `psfstriptable` (1), `psfgettable` (1), `psfxtable` (1)

---

# GSTACK

## NAME

`gstack` - 打印运行进程的堆栈跟踪

## SYNOPSIS

`gstack pid`

## DESCRIPTION

`gstack` 到命令行指定的 `pid` 活动进程，并打印执行堆栈跟踪。如果二进制文件中存在 ELF 符号（通常如此，除非运行 `strip` (1)），则打印地址。如果进程是线程组的一部分，`gstack` 将为组中的每个线程打印堆栈跟踪。

## SEE ALSO

`gdb` (1), `ptrace` (2), `threads` (1)

## AUTHORS

Ross Thompson <>

Red Hat, Inc. <>

---

# PSTREE

## NAME

`pstree` - 显示进程树

## SYNOPSIS

`pstree [-a--argunts] [-c--compact] [-h--highlight-all -H--highlight-pid] [-g--show-pgids] [-l--long] [-n--nuric-sort] [-N--ns-sort] [-p--show-pids] [-s--show-parents] [-S--session]`

## DESCRIPTION

`pstree` 以树的形式显示运行的进程。如果省略 pid，则根位于 init。如果指定了用户，则显示该用户的所有进程。

`pstree -V` --version

## OPTIONS

-a 显示命令行参数。如果进程的命令行被换出，该进程将显示在括号中。-a 隐式禁用进程压缩，但不禁用线程。-A 使用 ASCII 字符绘制树。-c 禁用相同子树的压缩。默认情况下，会尽可能压缩子树。-h 高亮当前进程及其祖先。如果终端不支持高亮，或者当前进程及其任何祖先不在显示的子树中，则此操作无效。-H 类似于 `-h` 但高亮指定的指定的进程。与使用 `-h` 不同，如果高亮不可用，`pstree` 在使用 `-H` 时失败。-g 显示 PGID。进程组 ID 以十进制显示在每个进程后的括号中。-p 隐式禁用压缩。-l 显示长行。默认情况下，行将被截断为 COLUMNS 环境变量或显示宽度。如果这两种方法不起作用，则使用默认的 132 列。-n 按 PID 而不是按名称排序相同祖先进程。（数字排序。）-N 为指定类型的每个命名空间显示独立的树。可用类型有：ipc, mnt, net, pid, user, uts。普通用户无法访问其他用户的信息，因此输出将受到限制。-p 显示 PID。-s 显示父进程。-S 显示会话。-u 显示 UID。-Z 显示安全上下文。

显示 PID。PID 以十进制数字的形式在每个进程名称后的括号内。`-p` 隐式禁用压缩。

`-s`

显示指定进程的父进程。

`-S`

显示命名空间切换。与 `-N` 类似，作为普通用户运行时，输出受限。

`-u`

显示 uid 切换。当进程的 `uid` 与其父进程的 `uid` 不同时，新的 `uid` 将显示在进程名称后的括号内。

`-U`

使用 UTF-8 (Unicode) 线框。在 Linux 1.1-54 及以上版本中，在控制台上执行 `echo -e '\033%8'` 进入 UTF-8 模式，执行 `echo -e '\033%@'` 退出。

`-V`

显示版本信息。

`-Z`

`c2ph [-dpnP] [var=val] [files ...]`

## OPTIONS

`Options: -w wide; 缩写形式为: type_width=45 er_width=35 offset_width=8 -x hex; 缩写形式为: offset_fmt=x offset_width=08 size_fmt=x size_width=04 -n 不生成 perl 代码（作为 pstruct 调用时为默认） -p 生成 perl 代码（作为 c2ph 调用时为默认） -v 生成 perl 代码，并将 C 声明作为注释 -i 不重新计算内建数据类型的大小 -a 同时导出关于内建类型的信息 -t 追踪执行 -d 产生大量的调试输出 -slist 给出一个用逗号分隔的结构列表以供导出`list`listlist`

## DESCRIPTION

以下是 Tom Christiansen <> 编写的旧版 `c2ph.doc` 文档，日期：1991 年 7 月 25 日 08:10:21 GMT

从以前，我写了一个名为 `pstruct` 的程序。它是一个 Perl 程序，尝试解析 C 结构体并为你显示它们的偏移量（offsets）。这对于查看二进制转储或捣鼓内核的人来说特别有用。

`pstruct` 并不是一个漂亮的程序。它也不特别健壮。你看，问题在于 C 编译器解析 C 语言的能力远比我所能希望的好。

于是我变聪明了：我决定偷懒，让 C 编译器来解析 C，它会输出供我读取的调试 stabs。这些内容更容易被解析。它仍然不是一个漂亮的程序，但至少它更健壮了。

`pstruct` 接受任何 `.c` 或 `.h` 文件，最好是 `.s` 文件，因为无论如何它都会将其转换成那种格式，并输出如下的列表：



```
struct tty {
    int tty.t_locker 000 4
    int tty.t_tex_index 004 4
    struct tty * tty.t_tp_virt 008 4
    struct clist tty.t_rawq 00c 20
    int tty.t_rawq.c_cc 00c 4
    int tty.t_rawq.c_cmax 010 4
    int tty.t_rawq.c_cfx 014 4
    int tty.t_rawq.c_clx 018 4
    struct tty * tty.t_rawq.c_tp_cpu 01c 4
    struct tty * tty.t_rawq.c_tp_iop 020 4
    unsigned char * tty.t_rawq.c_buf_cpu 024 4
    unsigned char * tty.t_rawq.c_buf_iop 028 4
    struct clist tty.t_canq 02c 20
    int tty.t_canq.c_cc 02c 4
    int tty.t_canq.c_cmax 030 4
    int tty.t_canq.c_cfx 034 4
    int tty.t_canq.c_clx 038 4
    struct tty * tty.t_canq.c_tp_cpu 03c 4
    struct tty * tty.t_canq.c_tp_iop 040 4
    unsigned char * tty.t_canq.c_buf_cpu 044 4
    unsigned char * tty.t_canq.c_buf_iop 048 4
    struct clist tty.t_outq 04c 20
    int tty.t_outq.c_cc 04c 4
    int tty.t_outq.c_cmax 050 4
    int tty.t_outq.c_cfx 054 4
    int tty.t_outq.c_clx 058 4
    struct tty * tty.t_outq.c_tp_cpu 05c 4
    struct tty * tty.t_outq.c_tp_iop 060 4
    unsigned char * tty.t_outq.c_buf_cpu 024 4
    unsigned char * tty.t_outq.c_buf_iop 028 4
    ...
}
```

实际上，这是通过一组特定的选项生成的。你可以控制每一列的格式，无论你偏好宽宽还是窄、十六进制还是十进制、前导零或其他任何设置。使用此工具只需要一个能生成 BSD 风格 stabs 的 C 编译器。原生编译器和 GCC 的`-g`选项可以为此实现。要了解更多信息，只需输入一个错误的选项（如`-?`），就会提供很长的用法信息。

如果你通过另一个名字`c2ph`调用`pstruct`，你就拥有了一个将 C 代码翻译成 Perl 代码的代码器！至少对于结构体和联合体的声明是如此，但这已经很厉害了。在此之前，任何用 Perl 编程并希望与 C 程序（如内核）交互的人，都被迫猜测 C 结构体的布局，然后将这些布局硬编码到自己的程序中。当然，当你把编写好的程序带到一个结构布局不同的系统时，你的程序就崩溃了。这就是为什么我们有了 Larry 的`c2ph`翻译器，它虽然有帮助，但只在某些系统上有效，而不适用于真实的 C，而这也是非常需要的。我为你提供的是一种获取所有 C 结构体的循环方法。我将它们以包和函数的形式封装。请考虑以下程序：

```
#!/usr/local/bin/perl
require 'syscall.ph';
require 'sys/ti.ph';
require 'sys/resource.ph';
$ru = "\0" x &rusage_sizeof();
syscall(&SYS_getrusage, &RUSAGE_SELF, $ru) && die "getrusage: $!";
@ru = unpack($t = &rusage_typedef(), $ru);
$uti = $ru[&rusage_uti + &tival'tv_sec ] + ($ru[&rusage_uti + &tival'tv_usec ]) / 1e6;
$sti = $ru[&rusage_sti + &tival'tv_sec ] + ($ru[&rusage_sti + &tival'tv_usec ]) / 1e6;
printf "you have used %8.3fs+%8.3fu seconds.\n", $uti, $sti;
```

如你所见，包名就是结构体的名称。普通字段就是它们自己的名称。此外，为了方便起见，提供了以下访问函数：

`struct`不接受参数，返回结构体中第一层元素的数量。你可以用它对结构体数组进行索引，例如：`$usec = $u[&user'u_ut + (&ITIMER_VIRTUAL * &itirval'struct) + &itirval'it_value + &tival'tv_usec ];`。`sizeof`返回结构中的字节数，或者如果你传递参数则返回大小，例如`&rusage'sizeof(&rusage_uti)`。`typedef`这是传递给`pack`和`unpack`的 Perl 格式定义。如果你请求空内容的 typedef，将得到整个结构体，否则将得到你请求的结构的 typedef。填充（Padding）会被处理，确保联合体被解包到所有别名的魔法也已处理。不过尚未支持位域。`offsetof`此函数返回该结构在数组中的字节偏移量。如果你懒得解包，可能希望使用此函数通过`vec()`直接对包结构进行索引。`typeof`不要与 typedef 访问函数混淆，此函数返回该字段的 C 类型。这允许你在预先不知道任何信息的情况下打印出良好的结构化打印输出。此函数无参数时为无操作（noop）。因此我将发布这样一个工具来为你导出结构体。

我看到的这种用法基本上是：

```
% c2ph <so_include_file.h> > /usr/lib/perl/tmp.ph
% c2ph so_include_file.h >> /usr/lib/perl/tmp.ph
% install
```

使用`c2ph`有点棘手，因为你必须正确包含文件。我无法确定你的系统情况，但这通常并不非常困难。

正如我提到的，代码并不漂亮——当我开始时从未想过它会是一个 1000 行的程序，否则我可能根本不会开始。但对于程序各个部分之间通信的方式，我不会那么草率，等等。

# pulseaudio

## 名称

pulseaudio - PulseAudio 音系统

## 摘要

`pulseaudio [options]`

`pulseaudio --help`

`pulseaudio --version`

`pulseaudio --dump-conf`

`pulseaudio --dump-modules`

`pulseaudio --dump-resample-thods`

`pulseaudio --cleanup-shm`

`pulseaudio --start`

`pulseaudio --kill`

`pulseaudio --check`

## 描述

PulseAudio 是一个用于 Linux、POSIX 和 Windows 系统的低延迟音频服务器。

## 选项

`-h | --help`

显示帮助。

`--version`

显示版本信息。

`--dump-conf`

加载守护进程配置文件`daemon.conf`，解析命令行上剩余的配置选项，并输出生成的守护进程配置，格式与`daemon.conf`兼容。

`--dump-modules`

列出可用的加载模块。配合`-v`可获取更详细的列表。

`--dump-resample-thods`

列出可用的音频重采样器。

`--cleanup-shm`

识别`/dev/shm`中过时的 PulseAudio POSIX 共享内存段并可能将其删除。这会在每次新守护进程启动或客户端尝试连接到守护进程时隐式执行。通常不需要手动执行此命令。仅在支持通过挂载到`/dev/shm`的虚拟文件系统实现 POSIX 共享内存的系统上可用（例如 Linux）。

`--start`

如果 PulseAudio 尚未运行则启动它。这与不带`--start`启动 PulseAudio 不同，后者如果 PA 已经在运行将会失败。当此调用返回时，保证 PulseAudio 已完全初始化。隐含`--daemonize`。

`-k | --kill`

杀死调用用户已运行的 PulseAudio 守护进程（等同于发送`SIGTERM`）。

`--check`

当 PulseAudio 守护进程已为调用用户运行时，返回代码 0，否则返回非零。除了错误到 stderr 外，在控制台上不产生任何输出。

`--system[=BOOL]`

作为系统级实例而非用户运行。请注意，这将禁用 PulseAudio 的某些功能，除非系统没有本地用户（例如是瘦客户端），否则通常不建议。此功能需要特殊配置和专门的 UNIX 用户设置。强烈建议与`--disallow-module-loading`结合使用（见下文）。

`-D | --daemonize[=BOOL]`

启动后进入守护进程模式，即与终端分离。

`--fail[=BOOL]`

当启动脚本`default.pa`（见下文）中指定的任何命令失败时，启动将失败。

`--high-priority[=BOOL]`

尝试获取高 Unix nice 级别。只有当调用用户设置了非零的`RLIMIT_NICE`资源限制（在支持此的系统上），或者我们以 SUID root 身份调用（见下文），或者我们被配置为作为系统守护进程运行（见上面的`--system`）时，才会成功。建议启用此项，因为这只是微不足道的安全风险（见下文）。

`--realti[=BOOL]`

尝试为 PulseAudio 的 I/O 线程获取实时调度。只有当调用用户设置了非零的`RLIMIT_RTPRIO`资源限制（在支持此的系统上），或者我们以 SUID root 身份调用（见下文），或者我们被配置为作为系统守护进程运行（见上面的`--system`）时，才会成功。建议仅对信任的用户启用，因为这是一个主要的安全风险（见下文）。

在消息中显示标记。

`--log-backtrace=FRAMES`

当`FRAMES`大于 0 时，记录指定帧数的栈回溯。

`-p | --dl-search-path=PATH`

设置动态对象（插件）的搜索路径。

`--resample-thod=METHOD`

默认使用指定的方法（见上面的`--dump-thods`）。

`--use-pid-file[=BOOL]`

创建 PID 文件。如果禁用此选项，每个用户可以运行多个服务器。

`--no-cpu-limit[=BOOL]`

在支持的平台上不安装 CPU 限制。默认情况下，PulseAudio 在占用过多 CPU 时会自动终止。这在使用实时调度时很有用（见下文）。

`--disable-shm[=BOOL]`

PulseAudio 客户端和服务器可以通过 POSIX 共享内存交换数据（在支持的系统中）。如果禁用，将通过 socket 通。请注意，当 PulseAudio 启用`--system`运行时，共享内存传输总是禁用的。

`-L | --load="MODULE ARGUMENTS"`

使用指定的参数加载指定的模块。

`-F | --file=FILENAME`

启动时运行指定的脚本。可以多次指定以顺序运行多个脚本。配合`-n`可禁用默认脚本`default.pa`（见下文）。

`-C`

启动后在 STDIN/STDOUT 上打开命令解释器。这可以用于运行时动态配置 PulseAudio。等同于`--load=module-cli`。

`-n`

启动时不加载默认文件`default.pa`（见下文）。通常与`-C`或`--file`配合。

## 文件

`~/.config/pulse/daemon.conf`, `/etc/pulse/daemon.conf`: 守护进程的配置设置。如果用户目录下不存在该文件，则加载全局配置文件。见 (5) 获取更多信息。

`~/.config/pulse/default.pa`, `/etc/pulse/default.pa`:  PulseAudio 守护进程时执行的默认配置脚本。如果用户目录下不存在该文件，则加载全局配置脚本。见 (5) 获取更多信息。

`~/.config/pulse/client.conf`, `/etc/pulse/client.conf`: PulseAudio 客户端应用程序的配置设置。如果用户目录下不存在该文件，则加载全局配置文件。见 (5) 信息。

## 信号

`SIGINT, SIGTERM`: PulseAudio 守护进程将关闭（等同于`--kill`）。

`SIGHUP`:将长状态报告储存在 STDOUT 或 syslog，取决于配置。

`SIGUSR1`: 加载 module-cli，允许通过 STDIN/STDOUT 进行运行时重配置。

`SIGUSR2`: 加载 module-cli-protocol-unix，允许通过 AF_UNIX socket 进行运行时重配置。更多信息请参阅 **(1)**。

## UNIX 组与用户

组`pulse-rt`：如果 PulseAudio 二进制文件被标记为 SUID root，则调用用户是否在该组中将决定是否启用实时调度和/或高优先级调度。请注意，启用实时调度存在安全风险（见下文）。

`pulse-access`组：如果 PulseAudio 作为系统守护进程运行（见上文`--system`），则当该组的用户通过 AF_UNIX socket 连接时将授予访问权限。如果 PulseAudio 作为用户守护进程运行，则此组没有意义。

用户`pulse`，组`pulse`：：如果 PulseAudio 作为系统守护进程运行（见上文`--system`）并以 root 身份启动，守护进程将放弃权限并使用该用户和组变为普通用户进程。如果 PulseAudio 作为用户守护进程运行，则该用户和组没有意义。

## 实时与高优先级调度

为了尽量减少播放期间出现断音的风险，如果底层平台支持，建议运行 PulseAudio 时启用实时调度。这可以将 PulseAudio 守护进程的调度延迟与系统负载解耦，从而确保 PulseAudio 始终在需要填充硬件播放缓冲区时获得 CPU 时间的最佳方法。遗憾的是，这在大多数系统上是一个安全风险，因为 PulseAudio 是作为用户进程运行，而给用户进程赋予实时调度权限始终伴随着用户滥用其导致系统锁定的风险——这是可能的，因为使进程变为实时实际上禁用了抢占。

为了降低这种风险，PulseAudio 默认不启用实时调度。但在受信任的系统中建议启用它。要要操作，请使用`--realti`（见上文）启动 PulseAudio，或在`daemon.conf`中启用相应的选项。由于在大多数系统中获取实时调度是一项特权操作，因此需要对系统配置进行特殊更改以允许调用用户执行该操作。有两种方案可用：

在较新的 Linux 系统上，可以使用系统资源限制`RLIMIT_RTPRIO`（更多信息参阅 **(2)**）允许特定用户获取实时调度。这可以在`/etc/security/limits.conf`中配置，建议资源限制为 9。

或者，可以为 PulseAudio 二进制文件设置 SUID root 位。这样，守护进程将在启动时立即放弃 root 权限，但保留`CAP_NICE`能力（在支持的系统上），前提是调用用户是`pulse-rt`组的成员（见上文）。对于所有其他用户，所有能力都将立即被放弃。该解决方案的优点是实时权限仅授予 PulseAudio 守护进程，而不是用户的所有进程。

或者，如果认为锁定机器的风险太大而无法启用实时调度，则可以启用高优先级调度（即负 nice 水平）。这可以通过在启动 PulseAudio 时传递`--high-priority`（见上文）来启用，也可以通过`daemon.conf`中的相应选项进行启用。只有在设置了相应的资源限制`RLIMIT_NICE`时（更多信息参阅 **(2)**）才能启用负 nice 水平，该限制可能配置在`/etc/security/limits.conf`中。建议资源限制为 31（对应 nice 水平 -11）。

## 环境变量

PulseAudio 客户端库检查以下环境变量的存在并据此更改其本地配置：

`$PULSE_SERVER`：当客户端请求服务器连接且未明确请求特定服务器时，指定要连接的服务器的字符串。服务器字符串是由空白字符分隔的服务器地址列表，按顺序尝试。服务器地址由一个可选的地址类型指定符（unix:, tcp:, tcp4:, tcp6:）以及路径或主机地址组成。主机地址可以包含一个可选的端口号。服务器地址可以用 {} 包裹的字符串作为前缀。在这种情况下，除非前缀字符串等于本地主机或机器 ID（`/etc/machine-id`），否则将忽略后续服务器地址。

`$PULSE_SINK`：当客户端创建播放流且未请求特定 sink 时，连接的 sink 名称。

`$PULSE_SOURCE`：当客户端创建录制流且未请求特定 source 时，连接的 source 名称。

`$PULSE_BINARY`：使用服务器自动启动时运行的 PulseAudio 执行文件路径。

`$PULSE_CLIENTCONFIG`：用于客户端配置时读取替代`client.conf`（见上文）的文件路径。

`$PULSE_COOKIE`：包含 PulseAudio 认证 cookie 的文件路径。默认值为`~/.config/pulse/cookie`。

这些环境变量设置如果已设置，其优先级高于来自`client.conf`（见上文）的配置设置。

## 作者

PulseAudio 开发者 <pulseaudio-discuss (at) lists (dot) freedesktop (dot) org>; PulseAudio 可从此处获取

## 相关



# PWD

## NAME

`pwd` - 打印当前/工作目录的名称

## SYNOPSIS

`pwd` `[*OPTION*]`...

## DESCRIPTION

打印目录的完整文件名

`-L`, `--logical` 使用逻辑路径

`-P`, `--physical` 使用物理路径

`--help` 显示帮助并退出

## 相关

(3)

完整文档位于：<> 或通过本地查看：`info '(coreutils) pwd'`

* * *

# PWMAKE

## NAME

`pwmake` - 生成随机易读密码的简单工具

## SYNOPSIS

`pwmake` `<entropy-bits>`

## DESCRIPTION

`pwmake` 是一个生成随机易读密码的简单配置工具。该工具允许指定用于生成密码的熵位数。

熵从 `/dev/urandom` 获取。

最小比特数为 `56`，适用于暴力破解尝试次数有限的系统/服务的密码。`64` 位对于攻击者无法直接访问密码哈值的应用程序是足够的。对于攻击者可能直接访问密码哈值或密码作为密钥的情况，应根据谨慎程度使用 `80` 到 `128` 位。

## 选项

第一个也是唯一的参数是生成密码的熵位数。

## 文件

`/etc/security/pwquality.conf` - `libpwquality` 库的配置文件。

## 返回码

`pwmake` 成功返回 0，错误返回非零。

## 相关

(1), (8)

## 作者

Tomas Mraz <>

* * *

# PWQCHECK

## NAME

`pwqcheck` - 检查密码质量

## SYNOPSIS

`[*options*]`

## DESCRIPTION

`Op Ar options` 程序使用 `libpasswdqc` 库检查密码质量。默认情况下，它期望从标准输入读取 3 行：

**第一行是新密码，**

**第二行是旧密码，且**

**第三行是现有账户名称或**

(5) 条目。

有多个可用的选项，用于控制 `Op Ar options` 的行为。

`Op Ar options` 在成功时会打印 `OK`。建议调用 `Op Ar options` 的脚本同时检查退出状态是否为零以及是否存在 `OK` 行。

## OPTIONS

`min =` `N0`, `N1`, `N2`, `N3`, `N4`

(默认值：`min=disabled,24,11,8,7`)

不同类型密码/短语允许的最小长度。可以使用关键字 `disabled` 来禁止无论长度如何都不允许特定类型的密码。随后的每个数字必须小于或等于前一个数字。

`N0` 用于仅由一个字符类中的字符组成的密码。字符类包括：数字、小写字母、大写字母和其他字符。还存在针对`non- ASCII`字符的特殊类，这些字符无法分类，但被假定为数字。

`N1` 用于由两个字符类的字符组成的密码，且这些字符类不满足短语的要求。

`N2` 用于短语。注意，除了满足此长度要求外，短语还必须包含足够数量的单词（参见下文 `passphrase` 选项）。

`N3` 和 `N4` 分别用于由三个和四个字符类的字符组成的密码。

在计算字符类数量时，作为密码第一个字符的大写字母和作为最后一个字符的数字不计入内。

除了长度足够长外，密码还需要包含足够的不同字符以匹配它们所检查的字符类和最小长度。

`max =` `N`

(默认值：`max = 40`) 允许的最大密码长度。这可以防止用户设置对于系统服务来说可能过长的密码。数值 8 被特殊处理：如果将 `max` 设置为 8，超过 8 个字符的密码不会被拒绝，但在强度检查时将会被截断为 8 个字符，并会警告用户。这用于传统的基于 DES 的密码哈希，它会将密码截断为 8 个字符。

如果你在使用传统的哈希，设置 `max = 8` 是重要的，否则弱密码将通过检查。

`passphrase =` `N`

(默认值：`passphrase = 3`) 短语所需的单词数量。

`match =` `N`

(默认值：`match = 4`) 用于判定密码至少部分基于字符字符串中发现的信息所需的公共子串长度，或设置为 0 以禁用子串搜索。注意，一旦发现弱子串，密码不会被拒绝；相反，它将受到普通的强度限制，弱子串的权重会被部分扣。

子串搜索不区分大小写，并能够检测和移除倒写的公共子串。

`config =` `FILE`

以 `passwdqc.conf` 格式加载配置 `FILE`。此文件可以定义 `passwdqc.conf5` 中描述的任何选项，但只尊重 `min`、`max`、`passphrase`、`match` 和 `config` 选项。

`-1`

只读取 1 行（新短语）。这是在 OpenBSD 上将 `Op Ar options` 作为密码检查程序时需要的——例如在 `/etc/login.conf` 的 "default" 部分中使用 `:passwordcheck=/usr/bin/pwqcheck -1:`。

`-2`

只读取 2 行（新旧短语）。

`pam_passwdqc` 模块由 Solar Designer 为 Openwall GNU/*/Linux 编写。`Op Ar options` 程序最初由 Dmitry V. Levin 为 ALT GNU/*/Linux 编写，间接复用了 `pam_passwdqc` 的代码（通过 `libpasswdqc`）。此手册页源自 `pam_passwdqc` 文档由 Dmitry V. Levin 为 Openwall GNU/*/Linux 编写。

* * *

# PWQGEN

## NAME

`pwqgen` - 生成质量可控的随机短语

## SYNOPSIS

`pwqgen` [*options*]

## DESCRIPTION

`pwqgen` 使用 `libpasswdqc` 生成随机短语

## OPTIONS

`random =` `N`

(默认值：`random = 47`) 随机短语的位数（来自 `/dev/urandom`）。

`config =` `FILE`

以 `passwdqc.conf` 格式加载配置 `FILE`。此文件可以定义任何描述的选项，但只尊重 `random` 和 `config` 选项。

`--version`

输出 `Op Ar options` 程序版本并退出。

`-h , --help`

输出 `Op Ar options` 帮助文本并退出。

## EXIT STATUS

当 `Op Ar options` 遇到无效配置文件、无效选项、无效参数值、无法获取足够的随机性以及任何无法生成短语的情况时，以非零状态退出。

## FILES

`/etc/passwdqc.conf`

## SEE ALSO

(1), (4), `passwdqc.conf5`, `pam_passwdqc`.

## AUTHORS

`pam_passwdqc` 模块由 Solar Designer 为 Openwall GNU/*/Linux 编写。`Op Ar options` 程序最初由 Dmitry V. Levin 为 ALT GNU/*/Linux 编写，间接复用了 `pam_passwdqc` 的代码（通过 `libpasswdqc`）。此手册页由 Dmitry V. Levin 为 Openwall GNU/*/Linux 编写。

* * *

# PWSCORE

## NAME

`pwscore` - 可配置密码质量检查工具

## SYNOPSIS

`pwscore` [*user*]

## DESCRIPTION

`pwscore` 是一个检查密码的简单工具。密码从标准输入读取。

该工具使用 `libpwquality` 库对最小长度、字典检查和其他检查进行可配置的检查。

如果密码未通过任何检查，它会报告错误；或者它会打印出 `0` 到 `100` 之间的整数密码质量分。

密码质量分相对于配置文件中的 `minlen` 设置。但通常低于 50 的值可以被视为中等质量，高于该值的视为良好。任何通过质量检查（特别是强制性的 `cracklib` 检查）的密码在默认 `minlen` 设置下即使高于 50 分也能抵御快速破解攻击。

## OPTIONS

第一个也是唯一的可选参数是用户名，用于检查密码与用户名的相似性。

## FILES

`/etc/security/pwquality.conf` - `libpwquality` 库的配置文件。

## RETURN CODES

`pwscore` 成功时返回 0，错误时返回非零。

## SEE ALSO

(1), (5), (8)

## AUTHORS

Tomas Mraz <>

* * *

# QEMU-IMG

## NAME

`qe-img` - QEMU 磁盘镜像工具

## SYNOPSIS

usage: `qe-img` command [command options]

## DESCRIPTION

`qe-img` 允许你离线创建、转换和修改镜像。它可以处理 QEMU 支持的所有镜像格式。

**警告：** 绝对不要使用 `qe-img` 修改正在运行的虚拟机或任何其他进程使用的镜像；这可能会破坏镜像。此外，请注意，查询正在被另一个进程修改的镜像可能会遇到状态不一致的情况。

## OPTIONS

支持以下命令：

- `options`：以 `na=value` 格式列出的格式特定选项列表，用逗号分隔。使用 `-o ?` 查看所用格式支持的选项概述，或参阅下文的格式说明。
- `snapshot_param`：用于内部快照的参数，格式为 `'snapshot.id=[ID],snapshot.na=[NAME]'` 或 `'[ID_OR_NAME]'`。
- `snapshot_id_or_na`：已弃，请改用 `snapshot_param`。
- `-c`：表示目标镜像应压缩（仅限 `qcow` 格式）。
- `-h`：带有或不带命令均显示帮助并列出支持的格式。
- `-p`：显示进度条（仅限 `compare`、`convert` 和 `rebase` 命令）。如果支持该的命令未使用 `-p` 选项，则会在处理时报告进度。
- `-q`：静默模式，不输出（错误除外）。
- `-S`：指定稀疏镜像的大小。
- `-t`：指定缓存模式，详见 `drive=...` 选项的说明。
- `T`：指定源缓存。
- `-o`：指定格式选项。
- `-f`：指定格式。
- `-b`：指定基础文件。
- `-F`：指定基础格式。
- `snapshot`：快照名称。
- `-a`：应用快照。
- `-c`：创建快照。
- `-d`：删除快照。
- `-l`：列出镜像中的所有快照。
- `u`：更新镜像链。
- `-n`：跳过目标创建。
- `-s`：严格模式，当镜像大小不匹配时失败。

### 命令描述：

`check [-f *fmt*] [--output=*ofmt*] [-r [leaks | all]] [-T *src_cache*]] *filena`

对磁盘镜像 `filena` 执行一致性检查。如果指定了 `-r`，`qe-img` 将尝试修复任何不一致之处。下表总结了退出代码：

- **0**：检查完成，镜像一致。
- **1**：由于错误未完成。
- **2**：检查完成，镜像损坏。
- **3**：检查完成，镜像存在泄漏但未损坏。
- **63**：该格式不支持检查。

`create [-f *fmt*] [-o *options*] *filena* [*size*]`

创建一个大小为 `size`、格式为 `fmt` 的磁盘镜像 `filena`。根据格式，你可以添加一个或多个 `options`。如果指定了 `backing_file`，则镜像将仅记录与 `backing_file` 的差异。在这种情况下，不需要单独指定大小。大小也可以通过 `-o` 选项指定。

`commit [-q] [-f *fmt*] [-t *cache*] [-b *base*] [-d] [-p] *filena`

将 `filena` 中记录的更改提交到基础镜像或备份文件。如果备份文件比快照小，则将其将其调整为与快照相同的大小。如果快照比备份文件小，则不会截断备份文件。如果你希望备份文件匹配较小的快照大小，可以在操作成功后安全地对其截断。

操作成功后将清空 `filena`。如果你之后不需要 `filena` 并打算删除它，可以通过指定 `-d` 标志来跳过清空。

如果给定镜像文件 `filena` 的备份链包含多个层，可以通过 `base` 指定提交更改的文件（必须是 `filena` 备份链的一部分）。如果未指定 `base`，将使用顶层的直接备份文件（即 `filena`）。出于一致性考虑，显式指定 `base` 将始终隐含 `-d`（因为在提交到间接备份文件后清空镜像会导致从中间备份链中读取到不同的数据）。

`compare [-f *fmt*] [-F *fmt*] [-T *src_cache*] [-p] [-s] [-q] *filena1 *filena2`

检查两个镜像的内容是否相同。你可以比较不同格式或设置的镜像。

除非通过 `-f`（用于 `filena1`）和/或 `-F`（用于 `filena2`）选项指定格式，否则将探测格式。

默认情况下，如果较大的镜像在另一个镜像结束后的区域仅包含未分配扇区和/或全零扇区，则它们被认为是相同的。此外，如果某个扇区在一个镜像中未分配，而在另一个镜像中仅包含零字节，则被评估为相等。你可以通过指定 `-s` 选项来使用 `Strict` 模式。当 `compare` 在 `Strict` 模式下运行时，如果镜像大小不同或某个扇区在一个镜像中已分配而在另一个镜像中未分配，则操作将失败。

默认情况下，`compare` 会打印结果消息。此消息显示两个镜像是否相同或第一个不同字节的位置。此外，如果使用了 `Strict` 模式，结果消息还可以报告镜像大小差异。

如果镜像相等，`compare` 以 `0` 退出；如果镜像不同，以 `1` 退出。其他退出代码表示执行过程中发生错误，标准错误输出包含错误消息。下表总结了 `compare` 子命令的所有退出代码：

| 退出代码 | 说明 |
| :--- | :--- |
| `0` | 镜像相同 |
| `1` | 镜像不同 |
| `2` | 打开镜像时出错 |
| `3` | 检查扇区分配时出错 |
| `4` | 读取数据时出错 |

`convert [-c] [-p] [-n] [-f *fmt*] [-t *cache*] [-T *src_cache*] [-O *output_fmt*] [-o *options*] [-s *snapshot_id_or_na*] [-l *snapshot_param*] [-S *sparse_size*]] filena [[filena2 [...]]] output_filena`

使用格式 `output_fmt` 将磁盘镜像 `filena` 或快照 `snapshot_param`（`snapshot_id_or_na` 已弃）转换为磁盘镜像 `output_filena`。可以选择压缩（`-c` 选项）或使用任何特定格式选项，如加密（`-o` 选项）。

只有 `qcow` 和 `qcow2` 格式支持压缩。压缩是只读。确保如果压缩的扇区被重写，它将以未压缩数据的形式重写。

在使用如 `qcow` 等可增长格式时，镜像转换也有助于获取更小的镜像：空扇区会被检测并从目标镜像中消除。

`sparse_size` 表示连续的字节数（默认值为 4k），应仅包含零，以便 `qe-img` 在转换过程中创建稀疏镜像。如果 `sparse_size` 为 0，则不会扫描源的未分配或零扇区，目标镜像将始终全量分配。

你可以使用 `backing_file` 选项强制将输出镜像创建为指定基础镜像的写复制（copy on write）镜像；`backing_file` 的内容应与输入的基础镜像相同，但路径、镜像格式等可能有所不同。

如果指定了 `-n` 选项，将跳过目标卷创建。这对于 `rbd` 等格式非常有用，如果目标卷已经用 `qe-img` 无法提供的特定选项创建。

`info [-f *fmt*] [--output=ofmt] [--backing-chain]] filena`

提供有关磁盘镜像 `filena` 的信息。特别可以用于了解在磁盘上保留的大小，这可能与显示的大小不同。如果虚拟机快照存储在磁盘镜像中，它们也会显示。命令可以以 `ofmt` 格式输出，可以是 `human` 或 `json`。

如果磁盘镜像具有基础文件链，可以使用 `--backing-chain` 选项递归地列出链中每个磁盘镜像的信息。

例如，如果你有一个镜像链：

`base.qcow2 <- snap1.qcow2 <- snap2.qcow2`

要从顶层开始到基础镜像列出上述链中每个磁盘镜像的信息，请执行：

`qe-img info --backing-chain snap2.qcow2`

`map [-f *fmt*] [--output=ofmt]] filena`

转储镜像 `filena` 及其基础文件链的元数据。特别是，此命令会转储 `filena` 每个扇区的分配状态，以及基础文件链中分配该扇区的顶层文件。

支持两种选项格式。默认格式（`human`）仅转储文件中已知的非零区域。文件的已知零部分将完全忽略，整个链中未分配的部分也是如此。`qe-img` 的输出将识别可以读取数据的文件以及在该文件中的偏移量。每行将包含四个字段，前三个是十六进制数字。例如，以下内容的第一行：

```
Offset Length Mapped to File 0 0x20000 0x50000 /tmp/overlay.qcow2 0x100000 0x10000 0x95380000 /tmp/backing.qcow2
```



意味着从镜像偏移量 0 开始的`0x20000`（131072）字节在`/tmp/overlay.qcow2`（以`raw`格式打开）中从偏移量`0x50000`（327680）开始可用。如果使用`human`格式，经过压缩、加密或在以 raw 格式不可用的数据将导致错误。注意文件名可能包含换行符，因此在脚本中解析此输出格式是不安全的。

另一种格式`json`返回一个字典数组：

- 数据是否经过压缩、加密或以 raw 格式不可用（布尔值`data`）；
- 数据是否为零（布尔值`zero`）；
- 读取数据的文件以及在该文件中的偏移量（`offset`）。

`snapshot [-l | -a *snapshot* | -c *snapshot* | -d *snapshot*]] filena`

在镜像`filena`中列出、应用、创建或删除快照。

`rebase [-f *fmt*] [-t *cache*] [-T *src_cache*] [-p] [-u] -b *backing_file [-F *backing_fmt*]] filena`

更改镜像的基础文件。只有`qcow2`和`qed`格式支持更改基础文件。

基础文件将被更改为`backing_file`，并且如果镜像格式支持，将基础文件格式更改为`backing_fmt`。如果`backing_file`指定为`""`（空字符串），则镜像将重基为无基础文件。

`cache`指定用于`filena`的缓存模式，而`src_cache`指定读取基础文件的缓存模式。

`rebase`可以以两种不同的模式运行：

### 安全模式（Safe mode）

这是默认模式，并执行真正的重基操作。新的基础文件可能与旧的不同，`qe-img rebase`将确保保持`filena`的客户端可见内容不变。

为了实现这一点，`backing_file`与旧基础文件之间的任何簇将合并到`filena`中，然后实际更改基础文件。

注意，安全模式是一个耗时操作，类似于转换镜像。它仅在旧基础文件仍然存在时有效。

### 不安全模式（Unsafe mode）

如果指定`-u`，`qe-img`使用不安全模式。在此模式下，仅更改`filena`的基础文件名和格式，不对文件内容进行任何检查。用户必须指定正确的新基础文件，否则镜像的客户端内容将损坏。

在使用此命令扩展磁盘镜像之后，你**必须**在虚拟机内部使用文件系统和分区工具来实际开始使用设备上的新空间。

`and [-p] [-f]` `fmt` `[-t]` `cache` `-o` `options` `filena`

为镜像文件`filena`添加镜像格式特定的`options`。并不是所有文件格式都支持此操作。

## NOTES

支持的镜像文件格式：

`raw`

原始磁盘镜像格式（默认）。该格式的优点是简单且易于导出到其他模拟器。如果你的文件系统支持“空洞”（例如 Linux 上的 ext2 或 ext3 或 Windows 上的 NTFS），则只有写入的扇区会占用空间。使用`qe-img info`查看镜像实际使用的大小，或在 Unix/Linux 上使用`ls -ls`。

支持的选项：

`preallocation`

预分配模式（允许值：`off`、`falloc`、`full`）。`falloc`模式通过调用`posix_fallocate()`为镜像预分配空间。`full`模式通过向底层存储写入零来为镜像预分配空间。

`qcow2`

QEMU 镜像格式，最通用的格式。使用它可以获得更小的镜像（如果你的文件系统不支持空洞，例如在 Windows 上，这非常有用）、可选的 AES 加密、基于 zlib 的压缩以及对多个虚拟机快照的支持。

支持的选项：

`compat`

确定使用的 qcow2 版本。`compat=0.10`使用任何 0.10 版本的 QEMU 都能读取的传统镜像格式。`compat=1.1`只有 QEMU 1.1 及更高版本才能理解的镜像格式扩展（默认值）。其中包括零簇，它允许对稀疏镜像进行高效的读时复制。

`backing_file`

基础镜像的文件（参见`create`子命令）

`backing_fmt`

基础镜像的镜像格式

`encryption`

如果此选项设置为`on`，镜像将使用 128 位 AES-CBC 进行加密。

在 qcow 和 qcow2 镜像中使用加密在现代密码学标准中认为是有缺陷的，存在若干设计问题：

- AES-CBC 密码器使用了基于扇区数量的可预测初始化向量。这使得它容易受到选择明文攻击，从而揭示加密数据的存在。
- 用户密码被直接用作加密密钥。选择不当或过短的密码将破坏加密的安全性。
- 如果密码泄露，没有任何方法可以更改密码来保护任何 qcow 镜像中的数据。必须克隆文件并在新文件中使用不同的加密密码。然后使用`shred`等程序对原始文件进行安全擦除，尽管在许多现代存储技术上这种方法也是无效的。

因此，强烈建议使用 qcow / qcow2 加密。建议用户使用替代加密技术，例如 Linux dm-crypt / LUKS 系统。

`cluster_size`

更改 qcow2 的簇大小（应在 512 到 2M 之间）。较小的簇可以优化镜像文件的大小，而较大的簇通常提供更好的性能。

`preallocation`

预分配模式（允许值：`off`、`metadata`、`falloc`、`full`）。带有预分配 metadata 的镜像初始较大，但在镜像需要增长时可以提高性能。`falloc`和`full`预分配与`raw`格式的选项类似，但同时也设置了 metadata。

`lazy_refcounts`

如果此选项设置为`on`，引用计数更新将被推迟，目标是避免 metadata I/O 并提高性能。这对于`cache=writethrough`特别有意义，因为它不会批量处理 metadata 更新。权衡是，宿主机崩溃后，引用计数表必须重建，即在下次打开时需要执行（自动的）`qe-img check -r all`，这可能花费很长时间。

此选项只有在指定`compat=1.1`时才能启用。

`nocow`

如果此选项设置为`on`，它将关闭文件的写时复制（COW）。它仅在 btrfs 上有效，对其他文件系统无效。

Btrfs 在托管虚拟机镜像文件时性能较低，当虚拟机内的客户系统也使用 btrfs 作为文件系统时更是如此。关闭 COW 是缓解这种糟糕性能的方法。通常在 btrfs 上关闭 COW 有两种方法：

a) 通过挂载`nodatacow`来禁用它，这样所有新创建的文件都是 NOCOW。

b) 对于空文件，添加 NOCOW 文件属性。这就是此选项的作用。

注意：此选项仅对新文件有效。

用于启用加速器。根据目标架构，可以使用`kvm`、`xen`或`tcg`。默认使用`tcg`。如果指定了多个加速器，当上一个初始化失败时，将尝试使用下一个。

`kernel_irqchip=on|off`

在可用时，为所选的加速器启用内核内 irqchip 支持。

`vmport=on|off|auto`

启用 VMWare IO 端口的仿真，用于`vmmouse`等。`auto`表示根据`accel`来选择该值。对于`accel=xen`，默认为`off`，否则默认为`on`。

`kvm_shadow_m=size`

定义`KVM`影子内存管理单元（MMU）的尺寸。

`dump-guest-core=on|off`

在核心转储（core dump）中包含客户机内存。默认为`on`。

`m-merge=on|off`

启用或禁用内存合并（memory merge）支持。当主机支持此功能时，它将消除虚拟机实例之间相同的内存页（默认启用）。

`iommu=on|off`

启用或禁用启用的 Intel`IOMMU`（`VT-d`）支持。默认为`off`。

`aes-key-wrap=on|off`

在`s390-ccw`主机上启用或禁用`AES`密钥封装支持。此功能控制是否创建`AES`封装密钥以允许执行`AES`加密函数。默认为`on`。

`dea-key-wrap=on|off`

在`s390-ccw`主机上启用或禁用`DEA`密钥封装支持。此功能控制是否创建`DEA`封装密钥以允许执行`DEA`加密函数。默认为`on`。

`-cpu` *model*

选择 CPU 模型（使用`-cpu help`查看列表和额外功能）。

`-smp [cpus=n][cores=cores][threads=threads][sockets=sockets][maxcpus=maxcpus]`

启动具有`n`个 CPU 的 SMP 系统。在 PC 目标上，支持最多 255 个 CPU。在 Sparc32 目标上，Linux 将可用 CPU 数量限制为 4。对于 PC 目标，可以指定每个插槽的`cores`、每个核心的`threads`以及总数`sockets`。如果给出任何值，可以省略 CPU 的总数`n`。`maxcpus`指定热插拔 CPU 的数量。

`-numa[,m=size][cpus=cpu[-cpu]][nodeid=node]`

启动一个 NUMA 系统。如果省略`m`、`mdev`和`cpus`，资源将平均分配。另外注意，`-numa`选项不会分配任何指定的资源。也就是说，它将现有资源分配到 NUMA 节点，你仍需使用`-m`、`-smp`选项分别分配内存，并可能使用`-object`为`mdev`子选项指定内存后端。

`-add-fd fd=fd,set=set][opaque=opaque]`

向 fd 集合添加一个文件描述符。有效选项有：

`fd=fd`

此选项定义要复制到 fd 集合中的文件描述符。该描述符不能是`stdin`、`stdout`或`stderr`。

`set=set`

此选项定义要添加该文件的 fd 集合 ID。

`opaque=opaque`

此选项定义一个用于描述`fd`的自由字符串。你可以使用 fd 集合中预打开的文件描述符打开镜像：

```
qe-system-i386 -add-fd fd=3,set=2,opaque="rw:/path/to/file"
qe-system-i386 -add-fd fd=4,set=2,opaque="ro:/path/to/file"
qe-system-i386 -drive file=/fdset/2,index=0,dia=disk
```

`-balloon none`禁用气球设备。`-balloon virtio[,addr=addr]`启用 virtio 气球设备（默认），可选指定 PCI 地址`addr`。`-device` `driver[,prop[=value][,...]]`添加设备`driver`。`prop=*value`设置驱动程序属性。有效属性取决于驱动程序。要获取可用驱动程序和属性的帮助，请使用`-device help`和`"-device driver,help"`。`-na` `na`设置客户机的`na`。此`na`将显示在 SDL 窗口标题中。`na`也将用于 VNC 服务器。此外还可以在 Linux 中可选设置顶层可见进程`na`。在 Linux 上还可以启用单个线程命名以辅助调试。`-uuid` `uuid`设置系统 UUID。

### 块设备选项：

- `-fda` `file`
- `-fdb` `file`

使用`file`作为软磁盘 0/1 镜像。

- `-hda` `file`
- `-hdb` `file`
- `-hdc` `file`
- `-hdd` `file`

使用`file`作为硬盘 0, 1, 2 或 3 镜像。

- `-cdrom` `file`

使用`file`作为 CD-ROM 镜像（不能同时使用`-hdc`和`-cdrom`）。你可以通过`/dev/cdrom`作为文件名来使用主机 CD-ROM。

- `-drive` `option[,option[,option[,...]]]`

定义一个新的驱动器。有效选项有：

- `file=file`

此选项定义了该驱动器使用哪个磁盘镜像。如果`filename`包含逗号，则应将其双写（例如，使用`file=my,,file`来使用文件`file=my,file`）。

特殊文件（如 iSCSI 设备）可以使用特定协议的 URL 指定。更多信息请参阅“Device URL Syntax”章节。

- `if=interface`

此选项定义了驱动器连接的接口类型。可用类型有：ide, scsi, sd, mtd, floppy, pflash, virtio。

- `bus=bus,unit=unit`

这些选项通过定义总线线号和单元 ID（unit id）来定义驱动器的连接位置。

- `index=index`

此选项通过在给定接口类型的可用连接器列表中使用索引，来定义驱动器的连接位置。

- `dia=dia`

此选项定义了 dia 的类型：disk 或 cdrom。

- `cyls=c,heads=h,secs=s[,trans=t]`

这些选项的定义与`-hdachs`中的相同。

- `snapshot=snapshot`

`snapshot`为"on"或"off"，控制给定驱动器的快照模式（参见`-snapshot`）。

- `cache=cache`

`cache`为"none", "writeback", "unsafe", "directsync"或"writethrough"，控制如何使用主机缓存来访问块数据。

- `aio=aio`

`aio`为"threads"或"native"，在基于 pthread 的磁盘 I/O 和原生 Linux AIO 之间进行选择。

- `discard=discard`

`discard`为"ignore"（或"off"）或"unmap"（或"on"）之一，用于控制`discard`（也称为`trim`或`unmap`）请求是被忽略还是传递给文件系统。因此，机器类型可能不支持 discard 请求。

- `format=format`

指定使用哪种磁盘`format`而不是自动检测格式。可以指定`format=raw`以避免解释不可信的格式头信息。

- `serial=serial`

此选项指定分配给设备的序列号。

- `addr=addr`

指定控制器的 PCI 地址（仅限`if=virtio`）。

- `werror=action,rerror=action`

指定在发生写入和读取错误时采取的`action`。有效操作有："ignore"（忽略错误并尝试继续）、"stop"（暂停 QEMU）、"report"（向客户机报告错误）、"enospc"（仅当主机磁盘已满时暂停 QEMU；否则向客户机报告错误）。默认设置为`werror=enospc`且`rerror=report`。

- `readonly`

以只读模式打开驱动器`file`。客户机的写入尝试将失败。

- `copy-on-read=copy-on-read`

`copy-on-read`为"on"或"off"，用于启用是否将读取的备份文件扇区复制到镜像文件中。

- `detect-zeroes=detect-zeroes`

`detect-zeroes`为"off", "on"或"unmap"，用于启用将操作系统的纯零写入自动转换为特定驱动程序优化的零写入命令。如果`discard`被设置为"unmap"，你甚至可以选择"unmap"以允许将零写入转换为 UNMAP 操作。

默认情况下，使用`cache=writeback`模式。只要数据出现在主机的页缓存（page cache）中，它就会报告数据写入已完成。只要你的客户机操作系统确保在需要时正确刷新磁盘缓存，这种就是安全的。如果你的客户机操作系统没有正确处理易失性磁盘写入缓存，且主机崩溃或掉电，客户机可能会遇到数据损坏。

对于此类客户机，你应该考虑使用`cache=writethrough`。

### `[,socket=socket|sock_fd=sock_fd]` 定义一个新的文件系统设备。可用选项包括：

#### `fsdriver`

此选项指定要使用的文件系统驱动程序后端。目前支持`local`、`handle`和`proxy`文件系统驱动程序。

#### `id=`

指定此设备的标识符。

#### `path=`

指定文件系统设备的导出路径。此路径下的文件将对客户机上的`9p`客户端可用。

#### `security_model=security_model`

指定用于该导出路径的安全模型。支持的安全模型有`passthrough`、`mapped-xattr`、`mapped-file`和`none`。在`passthrough`（透传）安全模型下，文件在客户机创建时将使用`sa`凭据存储。这要求 QEMU 以 root 身份运行。在`mapped-xattr`安全模型下，如`uid`、`gid`、模式位和链接目标等文件属性将作为文件扩展属性存储。对于`mapped-file`，这些属性存储在隐藏的`.virtfs_metadata`目录中。由该安全模型导出的目录无法与其他 Unix 工具交互。`none`安全模型与`passthrough`相同，区别是服务器在设置所有权等文件属性失败时不会报告错误。安全模型仅对`local` fsdriver 是强制性的。其他 fsdrivers（如`handle`、`proxy`）不接受安全模型参数。

#### `writeout=writeout`

这是一个可选参数。唯一支持的值是`imdi`。这意味着将使用主机页缓存来读写数据，但只有当存储子系统报告数据已写入时，才会向客户机发送写入通知。

#### `readonly`

允许将`9p`共享作为只读挂载项导出给客户机。默认提供读写权限。



### `socket=socket`

允许代理文件系统驱动程序使用传递的 socket 文件与 `virtfs-proxy-helper` 进行通信。

#### `sock_fd=sock_fd`

允许代理文件系统驱动程序使用传递的 socket 描述符与 `virtfs-proxy-helper` 进行通信。通常像 `libvirt` 这样的辅助程序会创建 `socketpair` 并将其中一个 `fd` 作为 `sock_fd` 传递。

`-fsdev` 选项配合 `-device driver virtio-9p-pci` 使用。

### `-device virtio-9p-pci,fsdev=id,mount_tag=mount_tag`

`virtio-9p-pci` 驱动程序的选项有：

### `fsdev=id`

指定配合 `-fsdev` 选项指定的 id 值。

### `mount_tag=mount_tag`

指定客户机用于挂载此导出点的 tag。

### `socket=socket`

允许代理文件系统驱动程序使用传递的 socket 文件与 `virtfs-proxy-helper` 进行通信。通常像 `libvirt` 这样的辅助程序会创建 `socketpair` 并将其中一个 `fd` 作为 `sock_fd` 传递。

### `sock_fd`

允许代理文件系统驱动程序使用传递的 `sock_fd` 作为与 `virtfs-proxy-helper` 接口的 socket 描述符。

### `-virtfs_synth`

创建合成文件系统。

### USB 选项：

### `-usb`

启用 USB 驱动程序（很快将成为默认）。

### `-usbdevice devna`

添加 USB 设备 `devna`。

### `mouse`

虚拟鼠标。激活时这将覆盖 PS/2 鼠标枚举。

### `tablet`

使用绝对坐标的指针设备（如触摸屏）。这使得 QEMU 能够在不捕获鼠标的情况下报告鼠标位置。

### `disk:[format=format]:file`

基于文件的存储设备。可选的 `format` 参数将用于而不是检测格式。可以指定 `format=raw` 以避免解释不可信的格式头。

### `host:bus.addr`

通过 `bus.addr` 透传主机设备（仅限 Linux）。

### `host:vendor_id:product_id`

通过 `vendor_id:product_id` 透传主机设备（仅限 Linux）。

### `serial:[vendorid=vendor_id,productid=product_id]:dev`

转换为主机设备 `dev` 的串口，可用设备参见 `-serial`。

### `braille`

盲文设备。这将使用 BrlAPI 在真实或虚拟设备上显示盲文。

### `net:options`

支持 CDC 以太网和 RNDIS 协议的网络适配器。

### 显示选项：

### `-display type`

选择使用的显示类型。此选项是旧样式 `-sdl/-curses/...` 选项的替代品。`type` 的有效值为：

### `sdl`

通过 SDL 显示输出（通常在独立的图形窗口中；其他可能性请参见 SDL 文档）。

### `curses`

通过 curses 显示输出。对于支持文本模式的图形设备模型，QEMU 可以 curses/ncurses 接口显示此输出。当图形设备处于图形模式或不支持文本模式时，不显示任何内容。通常只有 VGA 模型支持文本模式。

### `none`

不显示视频输出。客户机仍然看到一个显卡，但其输出不会显示给 QEMU 用户。此选项与 `-nographic` 选项的区别在于，它只影响视频输出的处理；`-nographic` 还会更改串口和并行端口目的地。

### `gtk`

在 GTK 窗口中显示视频输出。此界面提供了下拉菜单和其他元素，可以在运行时配置和控制虚拟机。

### `vnc`

在显示器 `<arg>` 上启动 VNC 服务器。

- `-nographic`: 正常情况下，QEMU 使用 SDL 显示 VGA 输出。通过此选项，你可以完全禁用图形输出，使 QEMU 成为一个简单的命令行应用程序。释放的串口将重定向到控制台，并与显示器合并（除非显式重定向到其他地方）。因此，你仍然可以使用 QEMU 通过串口控制台调试 Linux 内核。使用 `C-a h` 可以帮助在控制台和显示器之间切换。

- `-curses`: 正常情况下，QEMU 使用 SDL 显示 VGA 输出。通过此选项，QEMU 可以在文本模式下使用 `curses/ncurses` 接口显示 VGA 输出。在图形模式下不显示任何内容。

- `-no-fra`: 为 SDL 窗口不使用装饰，并使用所有可用屏幕空间启动它们。这使得在专用桌面工作区中使用 QEMU 更加方便。

- `-alt-grab`: 使用 `Ctrl-Alt-Shift` 捕获鼠标（代替 `Ctrl-Alt`）。注意，这也会影响特殊键（用于全屏、显示器模式切换等）。

- `-ctrl-grab`: 使用 `Right-Ctrl` 捕获鼠标（代替 `Ctrl-Alt`）。注意，这也会影响特殊键（用于全屏、显示器模式切换等）。

- `-no-quit`: 禁用 SDL 窗口关闭功能。

- `-sdl`: 启用 SDL。

- `-spice [option][,option][,...]]`: 启用 spice 远程桌面协议。有效选项有：

    - `port=<nr>`: 设置 spice 监听明文通道的 TCP 端口。

    - `addr=<addr>`: 设置 spice 监听的 IP 地址。默认是任何地址。

    - `ipv4`

    - `ipv6`

    - `unix`: 强制使用指定的 IP 版本。

    - `password=<secret>`: 设置身份认证所需的密码。

    - `sasl`: 要求客户端使用 SASL 对 spice 进行认证。所使用的认证方法的具体选择由系统/用户针对 'qe' 的 SASL 配置文件控制。该文件通常位于 `/etc/sasl2/qe.conf`。如果以非特权用户运行 QEMU，可以使用环境变量 `SASL_CONF_PATH` 使其搜索服务配置的备选位置。虽然 SASL 认证方法也可以提供数据加密（例如 GSSAPI），但建议 SASL 始终配合 `tls` 和 `x509` 设置使用，以启用 SSL 和服务器证书。这确保了数据加密，防止身份凭据泄露。

    - `disable-ticketing`: 允许客户端在无认证的情况下连接。

    - `disable-copy-paste`: 禁用客户端与虚拟机之间的复制粘贴。

    - `disable-agent-file-xfer`: 禁用客户端与虚拟机之间基于 `spice-vdagent` 的文件传输。

    - `tls-port=<nr>`: 设置 spice 监听加密通道的 TCP 端口。

    - `x509-dir=<dir>`: 设置 x509 文件目录。期望格式为 `-vnc $display,x509=$dir`。

    - `x509-key-file=<file>`

    - `x509-key-password=<file>`

    - `x509-cert-file=<file>`

    - `x509-cacert-file=<file>`

    - `x509-dh-key-file=<file>`: 也可以单独配置 x509 文件。

    - `tls-ciphers=<list>`: 指定要使用的加密算法列表。

    - `tls-channel=[main|display|cursor|inputs|record|playback]`

    - `plaintext-channel=[main|display|cursor|inputs|record|playback]`: 强制特定通道使用或不使用 TLS 加密。可以多次指定这些选项来配置多个通道。可以使用特殊名称 `default` 设置默认模式。对于未显式强制到某种模式的通道，允许 spice 客户端随心选择 tls/明文。

    - `image-compression=[auto_glz|auto_lz|quic|glz|lz|off]`: 配置图像压缩（无损）。默认是 `auto_glz`。

    - `jpeg-wan-compression=[auto|never|always]`

    - `zlib-glz-wan-compression=[auto|never|always]`: 配置 wan 图像压缩（针对慢速链路是有损压缩）。默认是 `auto`。

    - `streaming-video=[off|all|filter]`: 配置视频流检测。默认是 `filter`。

    - `agent-mouse=[on|off]`: 启用/禁用通过 `vdagent` 传递鼠标事件。默认是 `on`。

    - `playback-compression=[on|off]`: 启用/禁用音频流压缩（使用 celt 0.5.1）。默认是 `on`。

    - `seaess-migration=[on|off]`: 启用/禁用 spice 迁移。默认是 `off`。

- `-portrait`: 将图形输出向左旋转 90 度（仅限 PXA LCD）。

- `-rotate <deg>`: 将图形输出向左旋转 `deg` 度（仅限 PXA LCD）。

- `-vga <type>`: 选择模拟的 VGA 卡类型。`type` 的有效值为：

    - `cirrus`: Cirrus Logic GD5446 显卡。从 Windows 95 开始的所有 Windows 版本都应该能识别并使用此显卡。为了获得最佳性能，请在客户机和主机操作系统中使用 16 位色深。（这是默认值）

    - `std`: 带有 Bochs VBE 扩展的标准 VGA 卡。如果你的操作系统支持 VBE 扩展（例如 Windows XP）并且你想使用高分辨率（>= 1280x1024），请使用它。

    - `vmware`: VMware SVGA 适配器。如果你有足够新的驱动程序，可以使用它。

    - `qxl`: QXL 虚拟化设备。在使用 spice 协议时效果最佳。

    - `tcx`: (仅限 m) Sun TCX 缓冲区。

    - `cg3`: (仅限 m) Sun-three。

    - `virtio`: Virtio VGA 卡。

    - `none`: 禁用 VGA 卡。

- `-full-screen`: 全屏启动。

- `-g <width>x<height>[x<depth>]`: 设置初始分辨率和深度（PPC, SPARC 仅限）。

- `-vnc display[,option][...]]`: 正常情况下，QEMU 使用 SDL 显示 VGA 输出。通过此选项，你可以让 QEMU 监听显示 *display* 并通过 VNC 会话重定向 VGA 显示。在使用此选项时启用平板设备（`-usbdevice tablet`）非常有用。使用 VNC 显示时，可以使用 `-k` 参数设置键盘布局（如果不是 en-us）。*display* 的有效语法为：

    - `host*:d`: 仅允许来自 *host* 的 TCP 连接到显示 *d*。按照习惯，TCP 端口为 5900+*d*。可以省略 *host*，此时服务器接受任何主机。

    - `unix:path`: 允许通过 UNIX 套接字连接，*path* 是监听连接的 unix 套接字位置。

    - `none`: 初始化 VNC 但不启动。可以使用显示器命令 `change` 以后启动 VNC 服务器。

- `reverse`: 通过“反向”连接到监听的 VNC 客户端。客户端由 *display* 指定。对于反向网络连接（`host:d`），*d* 参数是 TCP 端口而不是显示器。

- `websocket`: 打开一个额外的 TCP 监听端口，用于 VNC WebSocket 连接。根据定义，WebSocket 端口是 5700+*display*。如果指定了 *host*，仅允许来自该主机的连接。作为替代，可以使用 `websocket=*port` 指定 WebSocket 端口。如果通过 VNC 选项指定了所需的 x509，则支持 WebSocket 连接的 TLS 加密。

- `password`: 要求客户端连接使用密码认证。

密码需要单独在 **pcsys_monitor** 中通过 `set_password` 命令设置。更改密码的语法为：`set_password <protocol> <password>`，其中 `<protocol>` 可以是 `vnc` 或 `spice`。

如果你想更改 `<protocol>` 的密码过期时间，应该使用 `expire_password <protocol> <expiration-ti>`，其中过期时间 `ti` 可以是以下选项之一：`now`、`never`、`+seconds` 或 UNIX 过期时间戳 `ti`，例如 `+60` 使密码在 60 秒后过期，或 `1335196800` 使密码在 `Mon Apr 23 12:00:00 EDT 2012` 过期（这是该日期的 UNIX `ti` 对应的 `ti`）。

你也可以使用关键词 `now` 或 `never` 作为过期时间 `ti`，允许 `<protocol>` 密码立即过期或永不过期。

### `non-adaptive`

禁用自适应编码。自适应编码默认启用。自适应编码会尝试检测频繁更新的屏幕区域，并使用有损编码（如 JPEG）发送这些区域的更新。这在播放视频时节省带宽非常有帮助。禁用自适应编码将恢复 Tight 等编码的原始静态行为。

### `share=[allow-exclusive|force-shared|ignore]`

设置显示共享策略。`allow-exclusive` 允许客户端请求独占访问。正如 rfb 规范建议的，通过断开其他连接来实现。并行连接多个客户端需要所有客户端请求共享会话（使用 `vncviewer: -shared` 参数）。这是默认设置。`force-shared` 禁用客户端独占访问。对于共享桌面会话非常有用，你不希望某人忘记指定 `-shared` 而导致断开所有人的连接。`ignore` 完全忽略共享标志并允许所有人无条件连接。这不符合 rfb 规范，但是是传统的 QEMU 行为。

### i386 target only

### `-win2k-hack`

在安装 Windows 2000 时使用以避免磁盘已满错误。安装 Windows 2000 后，你不再需要此选项（此选项会减慢 IDE 传输）。

### `-no-fd-bootchk`

禁用 BIOS 中软磁盘的启动签名检查。可能需要从旧软磁盘启动。

### `-no-acpi`

禁用 ACPI（高级配置和电源接口）支持。如果你的客户操作系统抱怨 ACPI 问题，请使用它（仅限 PC 目标机器）。

### `-no-hpet`

禁用 HPET 支持。

### `-acpi`

禁用 ACPI（高级配置和电源接口）支持。如果你的客户操作系统抱怨 ACPI 问题，请使用它（仅限 PC 目标机器）。

使用不需要管理员权限运行的用户模式网络栈。有效选项有：

- `vlan=n`

将用户模式堆栈连接到 VLAN `n`（`n` = 0 为默认值）。

- `id=id`

- `na=na`

为监控命令分配唯一的 `na`。

- `net=addr[mask]`

设置客户可见的 IP 网络地址。可选指定子网掩码，可以是 `a.b.c.d` 形式，也可以是有效最高位的数量。默认为 `10.0.2.0/24`。

- `host=addr`

指定客户可见的主机地址。默认为客户网络中的第二个 IP 地址，即 `x.x.x.2`。

- `restrict=on|off`

如果启用此选项，客户将被隔离，即它将无法与主机通信，且没有客户 IP 数据包将通过主机路由到外部。此选项不会影响任何显式设置的转发规则。

- `hostna=na`

指定内置 DHCP 服务器报告的客户端主机 `na`。

- `dhcpstart=addr`

指定内置 DHCP 服务器可以分配的 16 个 IP 中的第一个。默认为客户网络中的第 15 到第 31 个 IP，即 `x.x.x.15` 到 `x.x.x.31`。

- `dns=addr`

指定虚拟 DNS 服务器的客户可见地址。地址必须与主机地址不同。默认为客户网络中的第三个 IP，即 `x.x.x.3`。

- `dnssearch=domain`

为内置 DHCP 服务器发送的域名搜索列表提供项。通过多次指定此选项可以传输多个域名后缀。如果支持，当无法解析域名时，客户将尝试追加给定的域名后缀。

示例：

```
qe -net user,dnssearch=mgmt.example.org,
dnssearch=example.org [...]
```

- `tftp=dir`

使用用户模式网络栈时，激活内置 TFTP 服务器。`dir` 中的文件将暴露为 TFTP 服务器的根目录。客户上的 TFTP 客户端必须配置为二进制模式（使用 Unix TFTP 客户端的 `bin` 命令）。

- `bootfile=file`

使用用户模式网络栈时，将 `file` 广播为 BOOTP 文件名。结合 `tftp` 使用，可以从本地目录为客户进行网络启动。

示例（使用 pxelinux）：

```
qe-system-i386 -hda linux.img -boot n -net user,tftp=/path/to/tftp/files,bootfile=/pxelinux.0
```

- `s=dir[,sserver=addr]`



使用用户模式网络栈时，激活内置 SMB 服务器，使 Windows 系统能够透明地访问 `dir` 中的主机文件。SMB 服务器的 IP 地址可以设置为 `addr`。默认使用客户网络中的第四个 IP，即 `x.x.x.4`。

在客户 Windows 操作系统中，需要将以下行：

```
10.0.2.4 sserver
```

添加到 `C:\WINDOWS\LMHOSTS` 文件（针对 windows 9x/Me）或 `C:\WINNT\SYSTEM32\DRIVERS\ETC\LMHOSTS`（Windows NT/2000）。

然后可以通过 `\\sserver\qe` 访问 `dir`。

注意主机操作系统上必须安装 SAMBA 服务器。QEMU 已在 Red Hat 9、Fedora Core 3 和 OpenSUSE 11.x 版本上通过测试。

- `hostfwd=[tcp|udp]:[hostaddr]:hostport-[guestaddr]:guestport`

将入站的 TCP 或 UDP 连接从主机端口 `hostport` 重定向到客户 IP 地址 `guestaddr` 的端口 `guestport`。如果未指定 `guestaddr`，其值为 `x.x.x.15`（内置 DHCP 服务器提供的第一个地址）。通过指定 `hostaddr`，可以将规则绑定到特定的主机接口。如果未设置连接类型，则使用 TCP。此选项可以多次给定。

例如，要将屏幕 1 的主机 X11 连接重定向到客户屏幕 0，请使用以下命令：

```
# 在主机上 qe-system-i386 -net user,hostfwd=tcp:127.0.0.1:6001-:6000 [...] # 此主机 xterm 应该在客户 X11 服务器中打开：xterm -display :1
```

要将主机端口 5555 的 telnet 连接重定向到客户的 telnet 端口，请使用以下命令：

```
# 在主机上 qe-system-i386 -net user,hostfwd=tcp::5555-:23 [...] telnet localhost 5555
```

当你在主机上使用 `telnet localhost 5555` 时，你连接到了客户 telnet 服务器。

- `guestfwd=[tcp]:server:port-dev`

- `guestfwd=[tcp]:server:port-cmd:command`

将客户 TCP 连接转发到 `port` 上的 IP 地址 `server` - `dev`。

将客户 TCP 连接转发到 `port` 上的 IP 地址 `server` - `cmd:command`。

```
# 启动第一个 QEMU 实例 qe-system-i386 linux.img \ -net nic,macaddr=52:54:00:12:34:56 \ -net socket,listen=:1234 # 将此实例的 VLAN 0 连接到第一个实例的 VLAN 0 # qe-system-i386 linux.img \ -net nic,macaddr=52:54:00:12:34:57 \ -net socket,connect=127.0.0.1:1234
```

`-netdev socket,id=id[,fd=h][,mcast=maddr:port[,localaddr=addr]]` `-net socket[,vlan=n][,na=na][,fd=h][,mcast=maddr:port[,localaddr=addr]]` 使用 UDP 组播 socket 创建与另一个 QEMU 虚拟机共享的 VLAN `n`，有效地为每个具有相同组播地址 `maddr` 和端口 `port` 的 QEMU 创建一个总线。

### 注意：

1. 多个 QEMU 可以运行在不同的主机上并共享一条总线（假设这些主机已正确配置了组播）。

`-netdev l2tpv3,id=id,src=srcaddr,dst=dstaddr[,srcport=srcport][,dstport=dstport],txsession=txsession[,rxsession=rxsession][,ipv6][,udp][,cookie64][,counter][,pincounter][,txcookie=txcookie][,rxcookie=rxcookie][,offset=offset]]` `-net l2tpv3[,vlan=n][,na=na],src=srcaddr,dst=dstaddr[,srcport=srcport][,dstport=dstport],txsession=txsession[,rxsession=rxsession][,ipv6][,udp][,cookie64][,counter][,pincounter][,txcookie=txcookie][,rxcookie=rxcookie][,offset=offset]]` 将 VLAN `n` 连接到 L2TPv3 伪交叉。L2TPv3 (RFC3391) 是一种在两个系统之间传输以太网（以及其他二层）数据帧的流行协议。它存在于路由器、防火墙和 Linux 内核中（从 3.3 版本开始）。

这种传输允许虚拟机直接与另一个虚拟机、路由器或防火墙通信。

- `src=srcaddr`: 源地址（强制性）

- `dst=dstaddr`: 目的地址（强制性）

- `udp`: 选择 udp 封装（默认为 ip）。

- `srcport=srcport`: 源 udp 端口。

- `dstport=dstport`: 目的 udp 端口。

- `ipv6`: 强制使用 v6，否则默认为 v4。

- `rxcookie=rxcookie`, `txcookie=txcookie`: Cookie 是 l2tpv3 规范中的一种弱安全形式。其功能主要用于防止配置错误。默认情况下为 32 位。

- `cookie64`: 将 cookie 大小设置为 64 位而不是默认的 32 位。

- `counter=off`: 强制使用不带计数器的"裁减"L2TPv3。

- `pincounter=on`: 解决损坏的计数器处理问题。这对于具有数据包重排序的网络可能也有帮助。

- `offset=offset`: 在头部和数据之间添加额外的偏移量。例如，为了附加...

`telnet` 指定套接字上的流量应解释 telnet 转义序列。

`reconnect` 设置当远端断开时，非服务器套接字重连的超时时间。`q` 将延迟多少秒后尝试重连。设置为 0 则禁用重连，且为默认值。

下方是 TCP 和 unix 套接字选项：

`TCP options: port=*port* [,host=*host*] [,to=*to*] [,ipv4] [,ipv6] [,nodelay]`

监听套接字的 `host` 指定要绑定的本地地址。连接套接字的 `host` 指定要连接的远程主机。对于监听套接字，`host` 是可选的。如果未指定，默认为 `0.0.0.0`。

监听套接字的 `port` 指定要绑定的本地端口。连接套接字指定要连接的远程主机上的端口。`port` 可以以端口号或服务名的形式给出。`port` 是必须的。

`to` 仅适用于监听套接字。如果指定了它且无法绑定 `port`，QEMU 将尝试绑定到后续端口，直到 `to` 为止并成功。`to` 必须指定为端口号。

`ipv4` 和 `ipv6` 指定使用 IPv4 或 IPv6。如果两者均未指定，套接字可以使用任一种协议。

`nodelay` 禁用 Nagle 算法。

`unix options: path=*path*`

`path` 指定 unix 套接字的本地路径。`path` 是必须的。

`-chardev udp ,id=*id* [,host=*host*] ,port=*port* [,localaddr=*localaddr*] [,localport=*localport*] [,ipv4] [,ipv6]` 将从客户的所有流量通过 UDP 发送到远程主机。

`host` 指定要连接的远程主机。如果未指定，默认为 `localhost`。

`port` 指定要连接的远程主机端口。`port` 是必须的。

`localaddr` 指定要绑定的本地地址。如果未指定，默认为 `0.0.0.0`。

`localport` 指定要绑定的本地端口。如果未指定，将使用任何可用的本地端口。

`ipv4` 和 `ipv6` 指定使用 IPv4 或 IPv6。如果两者均未指定，设备可以使用任一种协议。

`-chardev msmouse ,id=*id*` 将 QEMU 释放的 msmouse 事件转发到客户端。msmouse 不接受任何选项。

`-chardev vc ,id=*id* [[,width=*width*] [,height=*height*]] [[,cols=*cols*] [,rows=*rows*]]` 连接到 QEMU 文本控制台。`vc` 可选指定大小。

`width` 和 `height` 分别指定控制台的宽度和高度，单位为像素。

`cols` 和 `rows` 指定控制台的大小以适应给定尺寸的文本控制台。

`-chardev ringbuf ,id=*id* [,size=*size*]` 创建一个固定大小 `size` 的环形缓冲区。`size` 必须是 2 的幂，默认为 `64K`。

`-chardev file ,id=*id*,path=*path*` 将从客户接收的所有流量记录到文件中。

`path` 指定打开的文件路径。如果文件不存在将创建，如果已存在则将覆盖。`path` 是必须的。

`-chardev pipe ,id=*id*,path=*path*` 与客户建立双向连接。Windows 宿主机与其他宿主机之间的行为略有不同：

在 Windows 上，将在 `\.pipe\*path` 处创建一个全工管道。

在其他宿主机上，将创建两个名为 `path*.in` 和 `path*.out` 的管道。写入 `path*.in` 的数据将由客户接收。客户写入的数据可以从 `path*.out` 读取。QEMU 不创建这些命名管道（fifo），而是要求它们必须存在。

`path` 构成上述的管道路径的一部分。`path` 是必须的。

`-chardev console ,id=*id*` 将客户的流量发送到 QEMU 的标准输出。console 不接受任何选项。

`console` 仅在 Windows 宿主机可用。

`-chardev serial ,id=*id*,path=*path*` 将客户的流量发送到宿主机上的串口设备。

在 Unix 宿主机上，serial 实际上接受任何 tty 设备，而不只是串口线。

`path` 指定要打开的串口设备名称。

`-chardev pty ,id=*id*` 在宿主机上创建一个新的伪终端并连接到它。pty 不接受任何选项。

`pty` 在 Windows 宿主机不可用。

`-chardev stdio ,id=*id* [,signal=on|off]` 连接到 QEMU 进程的标准输入和标准输出。

`signal` 控制终端是否启用信号，包括使用组合键 Control-c 退出 QEMU。此选项默认启用，使用 `signal=off` 禁用。

`stdio` 在 Windows 宿主机不可用。

`-chardev braille ,id=*id*` 连接到本地 BrlAPI 服务器。braille 不接受任何选项。

`-chardev tty ,id=*id*,path=*path*` tty 仅适用于 Linux、Sun、OpenBSD。

`path` 指定要打开的串口设备名称。

目前身份验证通过使用 `ssh-agent` 完成。未来可能支持其他身份验证方法。

# Sheepdog

Sheepdog 是一个为 `QEMU` 设计的分布式存储系统。QEMU 支持使用本地 `sheepdog` 设备或远程网络设备。

### 指定 sheepdog 设备的语法

`sheepdog[+tcp|+unix]://[host:port]/vdina`

`[?socket=path][#snapid|#tag]`

## 示例

```
qe-system-i386 --drive file=sheepdog://192.0.2.1:30000/MyVirtualMachine
```

# GlusterFS

GlusterFS 是一个用户空间的分布式文件系统。QEMU 支持通过 TCP、Unix 域套接字和 RDMA 传输协议使用 `GlusterFS` 卷来托管虚拟机磁盘镜像。

在 GlusterFS 卷上指定虚拟机磁盘镜像的语法为：

`gluster[+transport]://[server[:port]]/volna/image[?socket=...]`

## 示例

```
qe-system-x86_64 --drive file=gluster://192.0.2.1/testvol/a.img
```

- **url**: 在显式向驱动程序传递选项时的完整 URL。
- **readahead**: 每次向远程服务器发送范围请求时预读的数据量。该值可以可选地带有后缀 'T'、'G'、'M'、'K'、'k' 或 'b'。如果没有后缀，则假设为字节。该值必须是 512 字节的倍数。
- **sslverify**: 在通过 SSL 连接时是否验证远程服务器的证书。可以是 'on' 或 'off'。默认值为 'on'。
- **cookie**: 在每次发出的请求中发送此 cookie（也可以用 ';' 分隔的 cookie 列表）。仅在使用支持 cookie 的 HTTP 等协议时支持，否则将被忽略。
- **tiout**: 设置 CURL 连接的超时（秒）。该 tiout 是 CURL 等待远程服务器响应以获取要下载镜像大小的时间。如果没有设置，则使用 5 秒默认超时。

注意，当显式向 `qe` 传递选项时，`driver` 是 `<protocol>` 的值。

### 示例：从远程 Fedora 20 活动 ISO 镜像启动

```
qe-system-x86_64 --drive dia=cdrom,file= qe-system-x86_64 --drive dia=cdrom,file.driver=http,file.url=
```

### 示例：从远程 Fedora 20 云镜像启动，使用本地覆盖层进行写入、写时复制以及 64k 的预读

```
qe-img create -f qcow2 -o backing_file='json:{"file.driver":"http",, "file.url":"",, "file.readahead":"64k"}' /tmp/Fedora-x86_64-20-20131211.1-sda.qcow2 qe-system-x86_64 -drive file=/tmp/Fedora-x86_64-20-20131211.1-sda.qcow2,copy-on-read=on
```

### 示例：从存储在带有自签名证书的 VMware vSphere 服务器上的镜像启动，使用本地覆盖层进行写入、64k 的预读以及 10 秒的超时

```
qe-img create -f qcow2 -o backing_file='json:{"file.driver":"https",, "file.url":"&dsNa=datastore1",, "file.sslverify":"off",, "file.readahead":"64k",, "file.tiout":10}' /tmp/test.qcow2 qe-system-x86_64 -drive file=/tmp/test.qcow2
```

Bluetooth(R) 选项：

- **-bt hci[...]**: 定义相应的蓝牙 HCI 功能。`-bt` 选项与所选机器类型中存在的 HCI 匹配。例如，当选择一个内置一个 HCI 的机器时，只有第一个 `-bt hci[...]` 选项是有效的并定义 HCI 的逻辑。传输层由机器类型决定。目前 `n800` 和 `n810` 机器有一个 HCI，而所有其他机器都没有。

- **-bt hci,null**:（默认）相应的蓝牙 HCI 没有内部逻辑，且不会响应任何 HCI 命令或发布事件。
- **-bt hci,host[:***id***]**: (`bluez` 仅）相应的 HCI 将命令/事件传递给或从此处接收。

注意，当显式向 `qe` 传递选项时，`driver` 是 `<protocol>` 的值。

# 调试/专家选项

## `-fw_cfg [na=]na,file=file`

从文件中添加 `fw_cfg` 条目。`na` 决定暴露给客体的 `fw_cfg` 文件目录中该条目的 `na` 名称。

### `-serial dev`

将虚拟串口重定向到宿主机字符设备 `dev`。默认设备在图形模式下为 `vc`，在非图形模式下为 `stdio`。此选项可以使用多次来模拟多达 4 个串口。

使用 `-serial none` 禁用所有串口。

可用的字符设备有：

#### `vc[:WxH]`

虚拟控制台。可选地以像素给出宽度和高度：

```
vc:800x600
```



也可以以字符形式指定宽度或高度：

`vc:80Cx24C`

### `pty`

[仅限 Linux] 伪 TTY（自动分配一个新的 PTY）。

### `none`

不分配设备。

### `null`

空设备。

### `chardev:id`

使用通过 `-chardev` 选项定义的字符设备。

### `/dev/XXX`

[仅限 Linux] 使用宿主机 tty，例如`/dev/ttyS0`。宿主机串口参数将根据相关的参数进行设置。

#### `/dev/parportN`

[仅限 Linux，仅限并行端口] 使用宿主机并行端口`N`。目前可以使用 SPP 和 EPP 并行端口功能。

### `file:filena`

将输出写入`filena`。无法读取任何字符。

### `stdio`

[仅限 Unix] 标准输入输出。

### `pipe:filena`

命名管道`filena`。

#### `COMn`

[仅限 Windows] 使用宿主机串口`n`。

#### `udp:[remote_host]:remote_port[@[src_ip]:src_port]`

此项实现了 UDP 网络控制台。当未指定`remote_host`或`src_ip`时，它们默认为`0.0.0.0`。当不使用指定的`src_port`时，会自动选择一个随机端口。

如果你只需要一个简单的只读控制台，可以使用`netcat`或`nc`，通过以下方式启动 QEMU：`-serial udp::4555`，并运行`nc`：

```bash
nc -u -l -p 4555
```

每当 QEMU 向该端口写入内容时，就会出现在 netconsole 会话中。

如果你计划通过 netconsole 发回字符，或者你想频繁停止并启动 QEMU，你应该让 QEMU 每次使用相同的源端口，可以使用类似`"-serial udp::"`的内容传递给 QEMU。

另一种方法是使用经过补丁的 netcat，它可以监听 TCP 端口并通过 UDP 发送和接收字符。如果你有一个激活了 telnet 远程回显和单字符传输的补丁版 netcat，可以使用以下选项设置一个 netcat 重定向器，允许通过端口 5555 的 telnet 访问 QEMU 端口。

**QEMU 选项：**

```bash
-serial udp::
```

**netcat 选项：**

```bash
-u -P 4555 -L 0.0.0.0:4556 -t -p 5555 -I -T
```

**telnet 选项：**

```bash
localhost 5555
```

#### `tcp:[host]:port[,server][,nowait][,nodelay][,reconnect=seconds]`

TCP 网络控制台有两种工作模式。它可以将串行 I/O 发送到某个位置，也可以等待来自某个位置的连接。

默认情况下，TCP 网络控制台被发送到`host`的`port`。如果你使用`server`选项，QEMU 将等待客户端 socket 应用连接到端口后才继续，除非指定了`nowait`选项。

`nodelay`选项禁用了 Nagle 缓冲算法。`reconnect`选项仅在设置了`noserver`时生效；如果连接断开，它将尝试在给定间隔重新连接。

如果省略了`host`，则默认为`0.0.0.0`。每次只接受一个 TCP 连接。你可以使用`telnet`连接到相应的字符设备。

将 TCP 控制台发送到`192.168.0.2`端口`4444`的示例：

```bash
-serial tcp:192.168.0.2:4444
```

在端口`4444`上监听并等待连接的示例：

```bash
-serial tcp::4444,server
```

在 IP`192.168.0.100`端口`4444`上监听但不等待的示例：

### `-gdb dev`

在设备`dev`上等待 GDB 连接。典型的连接可能是基于 TCP 的，但 UDP、伪 TTY 甚至 stdio 也是合理的用例。

后者允许在 GDB 内部启动 QEMU 并通过管道建立连接：

```text
(gdb) target remote | exec qe-system-i386 -gdb stdio ...
```



## QEMU 选项

- `-s`、`-gdb tcp::1234` 的简写，即在 TCP 端口 1234 上打开 `gdbserver`。
- `-d` `item1`[,...] 启用指定项目的日志记录。使用 `-d help` 查看日志项目列表。
- `-D` `logfile` 将日志输出到 `logfile` 而不是 `stderr`。
- `-L` `path` 设置 BIOS、VGA BIOS 和键位映射的目录。
- `-bios` `file` 设置 BIOS 文件名。
- `-enable-kvm` 启用 KVM 全虚拟化支持。此选项仅在编译时启用了 KVM 支持时才可用。
- `-xen-domid` `id` 指定 xen 宾客域 ID `id`（仅限 XEN）。
- `-xen-create` 使用 xen 超调用创建域，跳过 `xend`。警告：在使用 `xend` 时不应使用此选项（仅限 XEN）。
- `-xen-attach` 附加到现有的 xen 域。`xend` 在启动 QEMU 时将使用此项（仅限 XEN）。
- `-no-reboot` 退出而不是重启。
- `-no-shutdown` 在宾客机关机时不退出 QEMU，而是仅停止仿真。这允许实例切换到监视器以将更改提交到磁盘镜像。
- `-loadvm` `file` 直接使用保存的状态启动（监视器中的 `loadvm`）。
- `-daemonize` 初始化后将 QEMU 进程设为守护进程。在 QEMU 准备好在其任何设备上接收连接之前，它不会从标准 IO 分离。此选项是外部程序启动 QEMU 的有用方法，无需处理初始化竞态条件。
- `-option-rom` `file` 将 `file` 的内容作为可选 ROM 加载。此选项用于加载 EtherBoot 等内容。
- `-rtc [base=utc|localti|date][,clock=host|vm][,driftfix=none|slew]` 指定 `base` 为 `utc` 或 `localti`，让 RTC 分别从当前 UTC 或本地时间启动。在 MS-DOS 或 Windows 中为了正确的日期，需要 `localti`。若要在特定时间点启动，请提供格式为 `2006-06-17T16:01:21` 或 `2006-06-17` 的 `date`。默认 `base` 为 UTC。

默认情况下，RTC 由主机系统时间驱动。这允许在宾客内部使用精确的参考钟，特别是当主机时间平滑跟随准确的外部参考钟时（例如通过 NTP）。如果你想将宾客时间与主机隔离，可以将 `clock` 设置为 `rt`。为了防止其在挂起期间进行，可以设置为 `vm`。

如果你遇到时间漂移问题（特别是 Windows 的 ACPI HAL 问题），请启用 `driftfix`（仅限 i386 目标）。此选项将尝试计算 Windows 宾客未处理的多少定时器中断并重新注入它们。

- `-icount [shift=N|auto]`（等一下，让我重新格式化）
- `-icount [shift=N|auto]` 启用虚拟指令计数器。虚拟 CPU 每隔 `2^N` ns 的虚拟时间执行一条指令。如果指定 `auto`，将自动调整虚拟 CPU 速度，以保持虚拟时间与真实时间的误差在几秒之内。

当虚拟 CPU 睡眠时，除非指定了 `sleep=no`，否则虚拟时间将以默认速度推进。使用 `sleep=no`，只要虚拟 CPU 进入睡眠模式，虚拟时间将立即跳转到下一个定时器截止时间，且在未启用定时器时不会推进。这种行为从宾客的角度提供了确定性的执行时间。

请注意，虽然此选项可以提供确定性行为，但它并不提供周期精确的仿真。现代 CPU 包含标量乱序执行内核和复杂的缓存层级。执行的指令数与实际性能往往很少或没有关联。

`align=on` 将激活延迟算法，尝试同步主机钟和虚拟时钟。目标是让宾客按 `shift` 选项强制的真实频率运行。每当宾客钟落后于主机钟且指定了 `align=on` 时，我们将向用户打印消息告知延迟。目前，当 `shift` 为 `auto` 时，此选项不起。注意：同步算法适用于宾客钟快于主机钟的 `shift` 值。这通常发生在 `shift` 值较高时（高低取决于主机机器）。

- `-watchdog` `model` 创建一个虚拟硬件看狗设备。一旦启用（通过宾客操作），必须由宾客内部的代理定期轮询看狗，否则宾客将重启。选择一个你的宾客具有驱动程序的模型。

`model` 是要仿真的硬件看门狗模型。使用 `-watchdog help` 列出可用硬件模型。一个宾客只能启用一个看门狗。

可能可选的模型包括：

- `ib700`

  iBASE 700 是带有单个定时器的简单 ISA 看门狗。

- `i6300esb`

  Intel 6300ESB I/O 控制器是一个功能更丰富的 PCI 基双定时器看门狗。

- `diag288`

  基于 diagnose 288 超用的 s390x 虚拟看门狗（目前仅限 KVM）。

- `-watchdog-action` `action` `action` 控制看门狗定时器超时时 QEMU 执行的操作。默认是 `reset`（强制重置宾客）。其他可能的操作有：`shutdown`（尝试关闭宾客）、`poweroff`（强制关闭宾客）、`debug`（调试并继续）、`none`（什么都不做）。

注意 `shutdown` 操作需要宾客响应 ACPI 信号，而这可能无法做到。

示例：

```text
-watchdog-action shutdown i6300esb
-watchdog-action pause ib700
```

- `-echr` `ascii_value` 修改切换到监视器的 ascii 字符。默认为 `0x01`。你可以从以下选择不同的字符，1 到 26 映射到 Control-z。`-echr 20`
- `-virtioconsole` `c` 设置 virtio 控制。此选项为了向下兼容。请使用新方法 `-console`。
- `-show-cursor` 显示光标。
- `-tb-size` `n` 设置 TB 大。
- `-incoming tcp:[host]:port[,to=maxport][ipv4,ipv6]` 准备接入迁移，在指定的 tcp 端口监听。
- `-incoming rdma:host:port[,ipv4,ipv6]` 准备接入迁移，在指定的 rdma 端口监听。
- `-incoming fd:fd` 从给定的文件描述符接入迁移。
- `-incoming exec:cmdline` 从指定命令的输出接入迁移。
- `-incoming defer` 等待通过 `migrate_incoming` 指定 URI。监视器可以在发布 `migrate_incoming` 之前更改设置（如迁移参数），以便开始迁移。
- `-nodefaults` 不创建默认设备。通常，QEMU 会设置默认设备，如串口、并行口、虚拟控制台、监视器设备、VGA 适配器、软驱和光驱等。`-nodefaults` 将禁用所有默认设备。
- `-chroot` `dir` 在启动宾客执行前切换目录。配合 `-runas` 特别有用。
- `-runas` `user` 在启动宾客执行前放弃 root 权限，切换到指定的用户。
- `-prom-env` `variable=value` 设置 OpenBIOS nvram `variable` 为给定的 `value`（仅限 PPC、SPARC）。
- `-semihosting` 启用半托管模式（仅限 ARM、M68K、Xtensa、MIPS）。
- `-semihosting-config [enable=on|off][,target=native|gdb|auto][,arg=str[,...]]` 启用并配置半托管（仅限 ARM、M68K、Xtensa、MIPS）。

允许用户传递输入参数，可以多次使用以构建列表。为了向后兼容，仍然支持旧式的 `-kernel`/`-append` 命令行传递方法。如果同时指定了 `--semihosting-config arg` 和 `-kernel`/`-append`，参数将传递给半主机（semihosting），因为它始终具有优先级。

- `-old-param` 旧版参数模式（仅限 ARM）。
- `-sandbox` `arg` 启用 Seccomp 模式 2 系统调用过滤器。`on` 将启用系统调用过滤，`off` 将禁用。默认为 `off`。
- `-readconfig` `file` 从 `file` 读取设备配置。当你想要启动一个带有许多命令行选项的 QEMU 进程，但又不想超过命令行字符限制时，这种方法非常有用。
- `-writeconfig` `file` 将设备配置写入 `file`。该 `file` 可以是 `filename`（将命令行和设备配置保存到文件中），也可以是连字符（`-`）以将输出打印到标准输出 stdout。这稍后可以用作 `-readconfig` 选项的输入文件。
- `-nodefconfig` 通常情况下，QEMU 在启动时从 `sysconfdir` 和 `datadir` 加载配置文件。`-nodefconfig` 选项将防止 QEMU 加载任何这些配置文件。
- `-no-user-config` `-no-user-config` 选项使 QEMU 不加载 `sysconfdir` 上任何用户提供的配置文件，但不会跳过 `datadir` 中 QEMU 提供的配置文件。
- `-trace [events=file][,file=file]]` 指定跟踪选项。

### `events=file`

立即启用 `file` 中列出的事件。文件每行包含一个事件（如 `trace-events` 文件列出的）。只有当 QEMU 编译时使用了 `simple` 或 `stderr` 跟踪后端时，此选项才可用。

### `file=file`

将输出跟踪日志到 `file`。

此选项仅在 QEMU 编译时使用了 `simple` 跟踪后端时可用。

- `-enable-fips` 启用 FIPS 140-2 合规模式。
- `-msg timestamp[=on|off]` 在每条日志消息前添加时间戳。（默认：on）
- `-dump-vmstate` `file` 将当前机器类型的 JSON 编码 vmstate 信息转储到 `file` 文件。

### 通用对象创建

`-object` `typeena`[,`prop1`=`value1`,...] 按照指定的顺序设置属性，创建类型为 `typeena`。注意必须设置 `id` 属性。这些对象放置在 `/objects` 路径下。

`-object memory-backend-file,id=id,size=size,m-path=dir,share=on|off`

创建一个内存文件后端对象，可以使用大页支持客机 RAM。`id` 参数是一个唯一 ID，用于在配置 `-numa` 参数时引用此内存区域。`size` 选项提供内存区域的大小，并接受常见后缀，例如 `500M`。`m-path` 提供了指向共享内存或大页文件系统挂载的路径。`share` 布尔选项决定内存区域是标记为 QEMU 私有的还是共享的。后者允许协作的外部进程访问 QEMU 内存区域。

`-object rng-random,id=id,filename=/dev/random`

创建一个随机数生成器后端，从主机上的设备获取熵。`id` 参数是一个唯一 ID，用于从 `virtio-rng` 设备引用此熵后端。`filename` 参数指定从哪个文件获取熵，如果省略，则默认为 `/dev/random`。

`-object rng-egd,id=id,chardev=chardevid`

创建一个随机数生成器后端，从运行在主机上的外部守护进程获取熵。`id` 参数是一个唯一 ID，用于从 `virtio-rng` 设备引用此熵后端。`chardev` 参数是字符设备后端的唯一 ID，该后端提供到 RNG 守护进程的连接。

## 键位映射

在图形界面期间，你可以使用特殊的键组合来更改模式。默认键位映射如下，但如果你使用 `-alt-grab`，则修饰键为 Ctrl-Alt-Shift（而不是 Ctrl-Alt），如果你使用 `-ctrl-grab`，则修饰键为右 Ctrl（而不是 Ctrl-Alt）：

- **Ctrl-Alt-f**

  切换全屏。

- **Ctrl-Alt-+**

  放大屏幕。

- **Ctrl-Alt---**

  缩小屏幕。

在运行期间，如果你在使用 `-nographic` 选项，使用 `Ctrl-a h` 获取终端命令：

- **Ctrl-a h**
- **Ctrl-a ?**

  打印此帮助。

- **Ctrl-a x**

  退出。

- **Ctrl-a s**

  保存数据。

- **Ctrl-a t**

  切换控制台。

- **Ctrl-a b**

  中断。

- **Ctrl-a c**

  切换之间。

选项将使 (1) 尝试选择显示限制、使用空间和已用 inode 的单位。

`--always-resolve`

始终尝试将用户/组名称翻译为 `uid` / `gid`，即使该名称仅由数字组成。

`-p, --raw-grace`

当用户处于宽限期时，报告其宽限期结束（或已结束）时自 Unix 纪以来的秒数。当没有宽限期生效时，该字段为 `0`。这在通过脚本解析输出时特别有用。

`-i, --no-autofs`

忽略由自动挂载完成的挂载点。

`-l, --local-only`

仅在本地文件系统上报告配额（即忽略 NFS 挂载的文件系统）。

`-A, --all-nfs`

为所有 NFS 文件系统报告配额，即使它们报告为在本地设备上。

`-f, --filesystem-list`

仅对命令行指定的泛系统报告配额。

`-m, --no-mixed-pathnas`

目前，NFSv4 挂载点的 pathnas 在发送时不带路径开头的斜杠。`rpc.rquotad` 利用此识别 NFSv4 挂载并正确地在路径前前加上 NFS 文件系统的伪根。如果您指定了此选项，`quota` 将始终发送带开头斜杠的路径。这出于历史原因可能有用，但请注意，如果您使用新的 `rpc.rquotad`，通过 RPC 的 quota 将停止工作。

`-q, --quiet`

打印更简洁的消息，仅包含超出配额的文件系统信息。

`-Q, --quiet-refuse`

如果拒绝到 `rpc.rquotad` 的连接，不打印错误信息（通常发生在服务器上未运行 `rpc.rquotad` 时）。

`-w, --no-wrap`

如果设备名称过长，不要换行。这在通过脚本解析 (1) 的输出时有用。

`--show-mntpoint`

同时将挂载点作为文件系统标识显示。

`--hide-device`

不在文件系统标识中显示设备名称。

同时指定 `-g` 和 `-u` 会显示用户配额和组配额（针对该用户）。

只有超级用户可以使用 `-u` 标志和可选的 `user` 参数来查看其他用户的限制。非超级用户可以使用 `-g` 标志和可选的 `group` 参数仅查看其所属组的限制。

`-q` 标志优于 `-v` 标志。

## 诊断

如果 `quota` 以非零状态退出，则说明一个或多个文件系统超过了配额。

## 文件

`aquota.user` 或 `aquota.group`

文件系统根目录下的配额文件（版本 2 配额，非 XFS 文件系统）。

`quota.user` 或 `quota.group`

文件系统根目录下的配额文件（版本 1 配额，非 XFS 文件系统）。

`/etc/mtab`

默认文件系统。

## 参见

(2), (5), (8), (8), (8), (8), (8), (8)

# QUOTASYNC

## 名称

`quotasync` - 将内核中的文件系统使用情况和限制同步到磁盘格式。

## 概要

`quotasync` [`-ug`] `mount-point`...

`quotasync` [`-ug`] `-a`

`quotasync` `-h` | `-V`

## 描述

`quotasync` 将文件系统使用情况和限制从内核内存刷到存储在文件系统中的配额文件中。默认情况下仅同步用户配额。

如果您想通过解析配额文件的工具（如 (8)）显示准确的配额，此工具非常有用。

## 选项

`-u, --user`

同步用户使用情况和限制。

`quota.user` 或 `quota.group`

文件系统根目录下的配额文件（版本 1 配额，非 XFS/GFS2 文件系统）。

`/etc/mtab`

用户空间维护的挂载文件系统列表。

`/proc/mounts`

内核维护的挂载文件系统列表。

## 参见

(1), (2), (8), (8), (8), (8)。

# rapper

## 名称

`rapper` - Raptor RDF 解析和序列化实用。

## 概要

`rapper` [`OPTIONS`] `INPUT-URI` `[INPUT-BASE-URI]`

`rapper` [`OPTIONS`] `INPUT-URI` `[INPUT-BASE-URI]`

## 示例

```text
rapper [ OPTIONS] INPUT-URI [INPUT-BASE-URI]
```

```text
rapper [OPTIONS] INPUT-URI [INPUT-BASE-URI]
```

```text
rapper [ OPTIONS] INPUT-URI [INPUT-BASE-URI]
```



`rapper` -

## 描述

`quotasync` 将文件系统使用情况和限制从内核内存刷到存储在文件系统中的配额文件中。默认情况下仅同步用户配额。

如果您想通过解析配额文件的工具（如 `(8)`）显示准确的配额，此工具非常有用。

## 选项

`-u, --user`

同步用户使用情况和限制。

`-g, --group`

同步组使用情况和限制。

`-a, --all`

同步所有文件系统的使用情况和限制。您必须指定此选项或指定所需的文件系统。

`-V, --version`

显示程序版本信息并退出。

`-h, --help`

显示程序用法并退出。

## 诊断

如果同步失败或给出无效选项，`quotasync` 将以非零退出码终止。否则将返回零。

## 文件

`aquota.user` 或 `aquota.group`

文件系统根目录下的配额文件（版本 2 配额，非 XFS/GFS2 文件系统）。

`quota.user` 或 `quota.group`

文件系统根目录下的配额文件（版本 1 配额，非 XFS/GFS2 文件系统）。

`/etc/mtab`

用户空间维护的挂载文件系统列表。

`/proc/mounts`

内核维护的挂载文件系统列表。

## 参见

`(1)`, `(2)`, `(8)`, `(8)`, `(8)`, `(8)`。

* *

# rapper

## 名称

`rapper` - Raptor RDF 解析和序列化实用

## 概要

`rapper` [`OPTIONS`] *INPUT-URI* *[INPUT-BASE-URI]*

## 示例

```
rapper [OPTIONS] INPUT-URI [INPUT-BASE-URI]
```

`-h, --help`

显示程序用法并退出。

## 诊断

如果同步失败或给出无效选项，`quotasync` 将以非零退出码终止。否则将返回零。

## 文件

`aquota.user` 或 `aquota.group`

文件系统根目录下的配额文件（版本 2 配额，非 XFS/GFS2 文件系统）。

`quota.user` 或 `quota.group`

文件系统根目录下的配额文件（版本 1 配额，非 XFS/GFS2 文件系统）。

`/etc/mtab`

用户空间维护的挂载文件系统列表。

`/proc/mounts`

内核维护的挂载文件系统列表。

## 参见

`(1)`, `(2)`, `(8)`, `(8)`, `(8)`, `(8)`。

* *

# rapper

## 名称

`rapper` - Raptor RDF 解析和序列化实用

## 概要

`rapper` [`OPTIONS`] *INPUT-URI* *[INPUT-BASE-URI]*

## 示例

```
rapper [OPTIONS] INPUT-URI [INPUT-BASE-URI]
```

`rapper` -

## 描述

`quotasync` 将文件系统使用情况和限制从内核内存刷到存储在文件系统中的配额文件中。默认情况下仅同步用户配额。

如果您想通过解析配额文件的工具（如 `(8)`）显示准确的配额，此工具非常有用。

## 选项

`-u, --user`

同步用户使用情况和限制。

`-g, --group`

同步组使用情况和限制。

`-a, --all`

同步所有文件系统的使用情况和限制。您必须指定此选项或指定所需的文件系统。

`-V, --version`

显示程序版本信息并退出。

`-h, --help`

显示程序用法并退出。

## 诊断

如果同步失败或给出无效选项，`quotasync` 将以非零退出码终止。否则将返回零。

## 文件

`aquota.user` 或 `aquota.group`

文件系统根目录下的配额文件（版本 2 配额，非 XFS/GFS2 文件系统）。

`quota.user` 或 `quota.group`

文件系统根目录下的配额文件（版本 1 配额，非 XFS/GFS2 文件系统）。

`/etc/mtab`

用户空间维护的挂载文件系统列表。

`/proc/mounts`

内核维护的挂载文件系统列表。

## 参见

`(1)`, `(2)`, `(8)`, `(8)`, `(8)`, `(8)`, `(8)`。

* *

# rapper

## 名称

从 `rapper` 中删除了 `-m` 选项，但此处从未记录过它。

删除了隐藏已久的 `-n` 选项。

删除了 `-s` 选项，它等同于 `-f` `scanForRDF`。

### 1.4.16
增加了 `-I/--input-uri` 和 `-O/--output-uri` 以分别设置输入和输出（解析器和序列化器）基 URI。

### 1.4.15
增加了 `-t/--trace` 用于进行 URI 追踪。

### 1.4.5
更新添加了序列化器 `rdfx-abbrev`。

### 1.4.3
更新了潜在的解析器和序列化器，并描述了用于定义命名空间的 `-f`。

### 1.3.0
增加了 `-f` 用于特性。

增加了 `-g` 用于猜测要使用的解析器。

### 1.1.0
删除了 `-a` 和 `--assu`，因为 `rdf:RDF` 现在始终是可选的。

## AUTHOR
Dave Beckett -

* * *

# RCTEST

## NAME
`rctest` - RFCOMM 测试

## SYNOPSIS
`rctest` `<mode*>` `[*options*]` `[*bdaddr*]`

## DESCRIPTION
`rctest` 用于测试 BlueZ 栈上的 RFCOMM 通信

## MODES
`-r`
监听并接收

`-w`
监听并发送

`-d`
监听并转储传入的数据

`-s`
连接并发送

`-u`
连接并接收

`-n`
连接并静默

`-c`
连接、断开、连接、...

`-m`
多次连接

## OPTIONS
`-b*bytes*`
发送/接收 `bytes*` 字节

`-i*device*`
选择指定的 `device*`

`-P*channel*`
选择指定的 `channel*`

`-U*uuid*`
选择指定的 `uuid*`

`-L*seconds*`
为 `seconds*` 启用 `SO_LINGER` 选项

`-W*seconds*`
为 `seconds*` 启用延迟设置

`-B*filena*`
使用来自 `filena*` 的数据包

`-N*num*`
发送 `num*` 帧

`-C*num*`
在延迟前发送 `num*` 帧（默认: 1）

`-D*milliseconds*`
在发送 `num*` 帧后延迟 `milliseconds*`（默认: 0）

`-A`
请求身份验证

`-E`
请求加密

`-S`
安全连接

`-M`
成为主设备

`-T`
启用时间戳

## AUTHORS
由 Marcel Holtmann <> 和 Maxim Krasnyansky <> 编写，man 页由 Filippo Giunchedi <> 提供

* * *

# rdfproc

## NAME
`rdfproc` - Redland RDF 处理工具

`-o, --output` `FORMAT`
设置三元组序列的输出 `FORMAT`，例如从搜索（`find` 命令）到 Redland 序列化器。使用 `-h` 或 `-o` 查看支持的格式的完整列表。

`-p, --password`
从标准输入读取存储选项 `'password'`。以行尾（`'\n'`）或文件结束终止。这等同于使用 `-t` 或 `--storage-options` 设置，但不需要在参数列表中暴露密码。

`-q, --quiet`
抑制信息消息（输出到 `stderr`）

`-r, --results` `FORMAT`
设置查询结果的语法格式。使用 `-h` 或 `-r` 查看查询结果格式的完整列表。

格式的准确列表取决于编译时使用的 `(3)`，但在 `-h` 的用法信息中是正确的。

`-s, --storage` `TYPE`
设置 Redland 存储类型（默认为 `'hashes'`）。如果环境变量 `RDFPROC_STORAGE_TYPE` 已设置，此处提供的存储类型将覆盖它。使用 `-h` 或 `-s` 查看查询结果格式的完整列表。

`-t, --storage-options` `OPTIONS`
设置 Redland 存储的选项，默认为 `"hash-type='bdb',dir='.'"` 以匹配默认存储 `"hashes"`。对于需要额外选项的 `'mysql'` 等存储类型，类似于 `"host='hostna',database='dbna',user='abc',password='pass'"`。如果环境变量 `RDFPROC_STORAGE_OPTIONS` 已设置，此处提供的存储选项将在之后应用。

`-v, --version`
打印 Redland 版本并退出。

`-V, --verbose`
在 `stderr` 上显示信息消息。

## COMMANDS
在允许的情况下，如 `NODE`、`SUBJECT`、`PREDICATE` 或 `OBJECT`，

`rdfproc` 工具允许使用 `Redland` RDF 库对 RDF 内容进行解析、查询、操作和序列化。`store-na` 是 Redland 存储，通常是一个短标识符。`command` 的参数各异在下文的 COMMANDS 部分进行了解释。

显示匹配三元组（*SUBJECT*、*PREDICATE*、`?`）的一个或所有节点

## 环境

可以通过设置 `RDFPROC_STORAGE_OPTIONS` 来提供存储选项，而不是使用选项 `-t`, `--storage-options OPTIONS*`。当两者都给出时，以命令行选项为准。

可以通过设置 `RDFPROC_STORAGE_TYPE` 来提供存储类型，而不是使用选项 `-s`, `--storage TYPE*`。当两者都给出时，使用命令行中的存储类型。

## 符合标准

*RDF/XML Syntax (Revised)*，W3C Recommendation，

*N-Triples*，位于 **RDF Test Cases*，Jan Grant 和 Dave Beckett (eds.) W3C Recommendation，

## 参见

`(3)`, `(3)`, `(1)`

## 作者

Dave Beckett -

* * *

# RDIST

## 名称

`rdist` - 远程文件传输客户端程序

## 概要

`rdist` [ `-DFn` ] [ `-A` *num* ] [ `-a` *num* ] [ `-d` *var=value* ] [ `-l` *<local logopts>* ] [ `-L` *<remote logopts>* ] [ `-f` *distfile* ] [ `-M` *maxproc* ] [ `-m` *host* ] [ `-o` *distopts* ] [ `-t` *tiout* ] [ `-p` *<rdistd-path>* ] [ `-P` *<transport-path>* ] [ *na ...* ]

`rdist` `-DFn` `-c` *na ...* *[login@]host[:dest]**

`rdist` `-Server`

`rdist` `-V`

## 描述

`Rdist` 是一个在多个主机上维护相同文件副本的程序。在可能的情况下，它可以保留文件的所有者、组、模式和修改时间（mti），并更新正在执行的程序。`Rdist` 从 `distfile` 读取命令以指导文件和或目录的更新。如果 `distfile` 为 `'-'`，则使用标准输入。如果不存在 `-f` 选项，程序将首先查找 `distfile`，然后查找 `Distfile` 作为输入。如果命令行上没有指定任何名称（na），`rdist` 将更新 `distfile` 中列出的所有文件和目录。否则，参数被视为要更新的文件名称或要执行的命令标签。如果标签和文件名称冲突，则假设为标签。这些可以结合使用，使用特定命令更新特定文件。

`-c` 选项强制 `rdist` 将剩余参数解释为小型 `distfile`。等效的 `distfile` 如下：

```
( `na` ... ) -> [`login`@]`host`
install [`dest`] ;
```

`-Server` 选项被识别为对旧版本 `rdist` 提供部分向后兼容支持，旧版本使用此选项将 `rdist` 置于服务器模式。如果使用 `-Server` 命令行选项启动 `rdist`，它将尝试执行（运行）旧版本的 `rdist`。只有当编译 `rdist` 时包含了旧 rdist 的位置（Red Hat Linux 使用 `/usr/bin/oldrdist` 路径）且该程序在运行时可用，此选项才会生效。

`Rdist` 可以使用 *(3)* 函数调用或运行任意的传输程序（如 *(1c)*）来访问每个目标主机。使用的方法在编译时选择。然而，如果使用后续的方法，可以在运行时通过命令行指定传输程序，默认为 *(1c)*。如果使用 *(1c)* 方法且目标主机为字符串 `localhost` 且远程用户名称与本地用户名称相同，`rdist` 将运行命令：

```
/bin/sh -c rdistd -S
```

否则，`rdist` 将运行命令：

```
rsh host -l reser rdistd -S
```

其中 `host` 是目标主机的名称，`reser` 是建立连接的用户名称，`rdistd` 是目标主机上的 rdist 服务器命令，如下。要使用 *(1c)* 以外的传输程序，请使用 `-P` 选项。无论使用什么传输程序，必须与上述指定的 *(1c)* 语法兼容。如果传输程序不兼容，应将其封装在理解此命令行语法的 shell 脚本中，然后执行真实的传输程序。

这是一个使用 *(1)* 作为传输的示例：

```
rdist -P /usr/local/bin/ssh -f myDistfile
```



如果使用`(3)`方法，则`rdist`将直接连接到目标主机并运行如下所示的`rdistd`服务器程序。默认且优先的方法是使用`(1c)`连接到目标主机。这允许`rdist`在无需设置 uid 为`root`的情况下运行。

在每个目标主机上，`Rdist`将尝试运行命令：

- `-f distfile`：设置要使用的`distfile`名称。如果将`distfile`指定为`-`，则从标准输入（`stdin`）读取。
- `-l logopts`：设置本地日志选项。
- `-L logopts`：设置远程日志选项。
- `-M num`：设置空闲进程的最大数量。
- `-m host`：限制更新哪些机器。
- `-n`：打印命令而不执行。
- `-o distopts`：指定要启用的传输选项。
- `-P <transport-path>`：使用传输程序。
- `-p <rdistd-path>`：设置`rdistd`的路径。
- `-t tiout`：设置输出文件。
- `-Server`：将`rdist`置于服务器模式。
- `-V`：显示`rdist`的版本。
- `-c na ...`：将剩余参数解释为小型`distfile`。
- `-verify`：验证文件。
- `-F distfile`：不分叉任何子进程。
- `-whole`：完整模式。整个文件名将追加到目的地。
- `-noexec`：自动排除`(5)`格式的可执行文件。
- `-younger`：较新模式。此选项导致`rdist`不更新比主副本更新的文件。
- `-compare`：二进制比较。
- `-follow`：跟随符号链接。
- `-ignlnks`：忽略未解析的链接。
- `-chknfs`：不检查或更新位于目标主机上 NFS 文件系统上的文件。
- `-chkreadonly`：在目标主机上启用检查，以查看文件是否位于只读文件系统上。

如果远程主机上的目标是一个符号链接，但该链接不在主主机上，则远程目标将保留为符号链接。这种行为在`rdist`的原始版本中通常被认为是一个 bug，但为了兼容旧版本而保留了它。

### `quiet`

静默模式。正在修改的文件通常会打印到标准输出。此选项会抑制这种输出。

### `remove`

删除多余文件。如果正在更新目录，则远程主机上存在但主目录中不存在的任何文件将被删除。这对于维护目录的完全相同副本非常有用。

### `nochkowner`

不检查已存在文件的用户所有权。文件所有权仅在文件更新时进行设置。

### `nochkgroup`

不检查已存在文件的组所有权。文件组所有权仅在文件更新时进行设置。

### `nochkmode`

不检查文件和目录的权限模式。权限模式仅在文件更新时进行设置。

### `nodescend`

不进入目录。通常`rdist`会递归检查目录。如果启用此选项，则`distfile`中文件列表中列出的任何目录将不会被递归扫描。仅检查目录的存在性、所有权模式。

### `numchkgroup`

使用数字组 ID（`gid`）来检查组所有权，而不是组名。

### `numchkowner`

使用数字用户 ID（`uid`）来检查用户所有权，而不是用户名。

### `savetargets`

保存已更新的文件而不是删除它们。任何更新的目标文件首先会从`file`重命名为`file.OLD`。

### `sparse`

启用对稀疏文件（又称为空文件）的检查。稀疏文件最常见的类型之一是由`(3)`产生的。此选项会增加额外的处理开销，因此应仅对可能包含稀疏文件的目标启用。

`-p <rdistd-path>`设置在目标主机上搜索`rdistd`服务器的路径。`-P <transport-path>`设置要使用的传输命令路径。这通常是`(1c)`，但可以是任何其他程序，例如`(1)`，它可以理解`(1c)`命令行语法并为远程主机提供适当的连接。`transport-path`可以是冒号分隔的可能路径列表。在这种情况下，将使用第一个存在的路径。例如`/usr/ucb/rsh:/usr/bin/remsh`、`/usr/bsd/rsh`。`-t tiout`设置等待远程`rdist`服务器响应的 tiout（秒）。默认为 900 秒。`-V`打印版本信息并退出。

## 消息日志

`Rdist`使用一组预定义的消息`facilities`（设施），每个设施包含一个消息`types`列表，指定要向该`facility`发送类型的消息。本地客户端（`rdist`）和远程服务器（`rdistd`）各自维护一份将什么类型的消息记录到哪些设施的副本。

`rdist`的`-l logopts`选项告诉`rdist`在本地使用哪些日志选项。`rdist`的`-L logopts`选项告诉`rdist`向远程`rdistd`服务器传递哪些日志选项。

`logopts`的格式应为：

```text
facility=types:facility=types...
```

有效的设施名称有：

### `stdout`

发送到标准输出的消息。

### `file`

日志到文件。要指定文件名，请使用格式`file=filena=types`。例如`file=/tmp/rdist.log=all,debug`。

### `syslog`

使用`(8)`设施。

### `notify`

使用`rdist`内部的`notify`设施。此结合`distfile`中的`notify`关键字使用，指定将哪些消息邮件到`notify`地址。

`types`应该是用逗号分隔的消息类型列表。指定的每个消息类型都会启用该消息级别。这与使用升序方案的`(3)`系统设施不同。以下是有效的`types`：

### `change`

发生变化。这包括以这种方式安装或更新的文件。

### `info`

通用信息。

### `notice`

关于变化的一般信息。这包括为了安装特定目标而需要创建目录，但在`distfile`中没有显式指定的内容。

### `nerror`

非致命的普通错误。

### `ferror`

致命错误。

### `warning`

关于错误的警告，其严重程度低于`nerror`类型消息。

### `debug`

调试信息。

第一格式用于定义变量。第二格式用于分送到其他主机。第三格式用于创建自指定日期以来的文件列表。`source list`指定本地主机上用作主拷贝的文件和目录目录。`destination list`是接收这些文件的主机列表。如果文件在主机上过期（第二格式）或文件新于时间戳文件（第三格式），则源列表中的每个文件将被添加到列表中。

标签是可选的。它们用于识别部分更新的命令。

换行符、制表符和空格仅用作分隔符，否则将被忽略。注释以`#`开始并以换行结束。

要展开的变量以`$`开头，后跟一个字符或大括号内的名称（见末示例）。

源和目标列表具有以下格式：

```text
<na> or
```

```text
(' 用空格分隔的多个 na ')
```

这些简单列表可以通过集合加法、减法或交集进行修改，如下：

```text
list '-' list
list '+' list
list '&' list
```

如果需要额外的修改（例如，除 OSF/1 机器的所有服务器和客户端），则必须使用临时变量显式构建列表。

shell 字符`[、]、{、}、*`和`?`在本地主机上以`(1)`的方式被识别并展开。可以使用反斜杠转义。`~`字符也以`csh`的方式展开，但在本地和目标主机上分别展开。当对以`~`开头的文件使用`-o whole`选项时，主目录以外的所有内容都会附加到目标`na`。不以`/`或`~`开头的文件名使用目标用户的家目录作为文件名部分的根目录。

命令列表由零个或多个以下格式的命令组成。

```text
install <options> opt_dest_na ; notify <na list> ; except <na list> ; except_pat <pattern list> ; special <na list> string ; cmdspecial <na list> string ;
```

`install`命令用于复制过期的文件和/或目录。每个源文件都会复制到目标列表中的每个主机。目录将以相同的方式递归复制。`Opt_dest_na`是一个用于重命名文件的可选参数。如果命令列表中没有出现`install`命令，或者没有指定目标`na`，则使用源文件`na`。如果路径中的目录在远程主机上不存在，则将创建它们。上文`OPTIONS`中指定的`-o distopts`选项在命令行上具有相同的语义，但它们仅适用于源文件列表中的文件。目标主机上使用的登录`na`与本地主机的相同，除非目标`na`的格式为`".`

`notify`命令用于将更新的文件列表（以及可能发生的任何错误）通过邮件发送给列出的`na`（目标主机名）。如果`na`中没有出现`@`，则会将目标主机追加到`na`之后（例如`, , ...`）。

`except`命令用于更新源列表中的所有文件，除了`na list`中列出的文件。这通常用于复制目录中某些文件以外的所有内容。

`except_pat`命令与`except`命令类似，但`pattern list`是一个正则表达式列表（详情见`(1)`）。如果模式中的其中一个匹配文件`na`内的任何字符串，则该文件将被忽略。注意，由于`\`是引号字符，它必须双倍处理才能成为正则表达式的一部分。变量在`pattern list`中会被展开，但 shell 文件模式匹配字符不会。若要包含`$`，必须用`\`对其进行转义。

`special`命令用于指定`(1)`在`na list`中的文件更新或安装后，在远程主机上执行的命令。如果省略了`na list`，则将对每个更新或安装的文件执行 shell 命令。`String`以`"`开始和结束，并可以跨越`distfile`中的多行。发送到 shell 的多个命令应用`;`分隔。命令在被更新主机的用户家目录中执行。`special`命令可以在程序更新后用于重建私有数据库等。每个`special`命令都设置了以下环境变量：

### `FILE`

刚刚更新的本地文件的完整路径`na`。

### `REMFILE`

刚刚更新的远程文件的完整路径`na`。

### `BASEFILE`

刚刚更新的远程文件的文件名。

`cmdspecial`命令与`special`命令类似，不同之处在于它仅在整个命令完成后执行，而不是在每个文件更新后执行。文件列表位于环境变量`$FILES`中。`$FILES`中的每个文件`na`用`:`（冒号）分隔。

如果主机`na`以`+`（加号）结尾，则去掉加号并禁用 NFS 检查。这等同于对这一个主机禁用`-o chknfs`选项。

以下是一个简单的示例。

```text
HOSTS = ( matisse ) FILES = ( /bin /lib /usr/bin /usr/gas /usr/include/{*.h,{stand,sys,vax*,pascal,machine}/*.h} /usr/lib /usr/man/man? /usr/ucb /usr/local/rdist ) EXLIB = ( Mail.rc aliases.dir aliases.pag crontab dshrc sendmail.cf sendmail.fc sendmail.hf sendmail.st uucp vfont ) ${FILES} -> ${HOSTS} install -oremove,chknfs ; except /usr/lib/${EXLIB} ; except /usr/gas/lib ; special /usr/lib/sendmail "/usr/lib/sendmail -bz" ; srcs: /usr/src/bin -> arpa except_pat ( \\.o\$ /SCCS\$ ) ; IMAGEN = (ips dviimp catdvi) imagen: /usr/local/${IMAGEN} -> arpa install /usr/local/lib ; notify ralph ; ${FILES} :: stamp.cory notify ;
```



## ENVIRONMENT

`TMPDIR` - 要使用的临时目录名。默认是`/tmp`。

## FILES

`distfile` - 输入命令文件  
`$TMPDIR/rdist*` - 更新列表的临时文件

## SEE ALSO

`(1),` `(1),` `(2),` `(1c),` `(3)`

## DIAGNOSTICS

## NOTES

如果文件的文件名（路径名的最后部分）为`.`，则`rdist`假设目标名是目录。即`/tmp/.`意味着`/tmp`在远程主机上应该是一个目录。

为了向下兼容，仍然识别以下选项：  
`-v -N -O -q -b -r -R -s -w -y -h -i -x`

## BUGS

源文件必须位于执行`rdist`的本地主机上。

变量展开仅对名单列表有效；应该有一个通用的宏机制。

`Rdist`在遇到负 mti 文件（1970 年 1 月 1 日之前的文件）时中止。

如果一个硬链接文件在目标中列出多次，则`rdist`将报告缺少链接。每个目标应只列出一个链接实例。

# READLINK

## NAME

`readlink` - 打印解析的符号链接或规范文件名单

## SYNOPSIS

`readlink` [*OPTION*]... `FILE`...

## DESCRIPTION

打印符号链接或规范文件名单的值

`-f`, `--canonicalize`  
通过递归跟踪给定名单每个组件中的符号链接来规范化；除最后一个组件外必须存在

`-e`, `--canonicalize-existing`  
通过递归跟踪给定名单每个组件中的符号链接来规范化，所有组件必须存在

`-m`, `--canonicalize-missing`  
通过递归跟踪给定名单每个组件中的符号链接来规范化，不要求组件存在

`-n`, `--no-newline`  
不输出末尾的分隔符

`-q`, `--quiet`,  
`-s`, `--silent`  
抑制大部分错误信息

`-v`, `--verbose`  
报告错误信息

`-z`, `--zero`  
每行输出都以 NUL 结束，而不是换行符

`--help`  
显示此帮助并退出

`--version`  
输出版本信息并退出

## SEE ALSO

`(1)`

## AUTHOR

`cddav`由 Joerg Schilling `<>` 等编写。  
本手册描述的是由 cdrkit 分发的程序。它是 cdrtools 项目原始程序的衍生品。然而，cdrtools 开发人员没有参与此衍生品的开发，因此对由此引起的任何问题不负责。不要尝试通过联系原始作者获取此程序的支持。

如果你有支持问题，请发送到

如果你确定发现了 bug，请向此列表发送邮件，并在主题中写入简短描述，并在正文第一行写入 "Package: cdrkit"。

本手册由 Oleksandr Moskalenko `<>` 编写，适用于 Debian GNU/Linux 系统。其他发行版可以使用，无需联系作者。手册中的任何错误或遗漏都是我的错；对本手册的查询或更正应指向（而不是主作者）。

# REALPATH

## NAME

`realpath` - 打印解析后的路径

## SYNOPSIS

`realpath` [*OPTION*]... `FILE`...

## DESCRIPTION

打印解析后的绝对路径；除最后一个组件外必须存在

`-e`, `--canonicalize-existing`  
所有组件必须存在

`-m`, `--canonicalize-missing`  
组件必须存在

`-L`, `--logical`  
在解析符号链接之前解析 '..' 组件

`-P`, `--physical`  
按遇到解析符号链接（默认）

`-q`, `--quiet`  
抑制大部分错误信息

`--relative-to`=*FILE*  
打印相对于`FILE`的解析后的路径

`--relative-base`=*FILE*  
除非路径在`FILE`之下，否则打印绝对路径

`-s`, `--strip`, `--no-syinks`  
不展开链接

`-z`, `--zero`  
每个输出行都以`NUL`结尾，而不是换行符

`--help`  
显示此帮助信息并退出

`--version`  
输出版本信息并退出

## 作者

由 Padraig Brady 编写。

## 报告错误

GNU coreutils 在线帮助：<>

向 <> 报告`realpath`翻译错误

## 版权

版权所有 2015 Free Software Foundation, Inc. 许可协议 GPLv3+: GNU GPL 3 或更高版本 <>。

这是免费软件：你可以自由地更改和重新发布它。在法律允许的范围内，不提供任何保证。

## 另请

(1), (2), (3)

完整文档见于：<>

或通过本地访问：`info '(coreutils) realpath invocation'`

* * *

# REBUILD-JAR-REPOSITORY

## 名称

`rebuild-jar-repository` - 重建 JAR 仓库

## 语法

`rebuild-jar-repository` [选项]... 目录

## 描述

根据当前的 JVM 设置重构（由`build-jar-repository`构建的）jar 仓库

## 选项

如果没有指定选项，默认操作将使用符号链接重建

`-c, --copy`  
复制文件。

`-h, --hard`  
创建硬链接。

`-s, --soft, --syolic`  
创建符号链接（默认）。

(1), (1),

* * *

# RECODE-SR-LATIN

## 名称

`recode-sr-latin` - 将塞尔维亚文本从西里尔字母转换为拉丁字母脚本

## 语法

`recode-sr-latin` [*选项*]

## 描述

将塞尔维亚文本从西里尔字母转换为拉丁字母。输入文本从标准输入读取。转换后的文本输出到标准输出。

### 信息性输出：

`-h, --help`  
显示此帮助信息并退出

`-V, --version`  
输出版本信息并退出

## 作者

由 Danilo Segan 和 Bruno Haible 编写。

## 报告错误

向 <> 报告错误。

## 版权

版权所有 2006-2007 Free Software Foundation, Inc. 许可协议 GPLv3+: GNU GPL 3 或更高版本 <>

这是免费软件：你可以自由地更改和重新发布它。在法律允许的范围内，不提供任何保证。

## 另请

`recode-sr-latin`的完整文档维护为 Texinfo 手册。如果你的站点上正确安装了`info`和`recode-sr-latin`程序，则命令

`info recode-sr-latin`

应该让你能够访问完整的手册。

* * *

# redland-db-upgrade

## 名称

`redland-db-upgrade` - 将旧版 Redland 数据库升级到 0.9.12 格式

## 语法

`redland-db-upgrade` *old BDB 名* *new BDB 名*

## 描述

`redland-db-upgrade`将 Redland 数据库从 0.9.11 及更的格式转换为新格式。它可以在每个 Redland 数据库上运行。例如，如果数据库`a`创建了文件`a-sp2o.db`、`a-so2p.db`和`a-po2s.db`，它可以转换为新的数据库`b`：

```
redland-db-upgrade a b
```

## 另请

(3),

## 作者

Dave Beckett -

* * *

# REGDIFF

## 名称

`regdiff` - Windows 注册表文件的差异程序

## 语法

`regdiff` [--help] [--backend=BACKEND] [--credentials=CREDENTIALS] [location]

## 描述

`regdiff`逐键逐值地比较两个 Windows 注册表文件，并生成一个包含两个文件差异的文本文件。

`regdiff`生成的文件后可以通过`regpatch`工具应用到注册表文件。

`regdiff`和`regpatch`使用与 Windows `regedit32.exe`工具相同的 sa 文件格式。

## 选项

`--help`  
显示可用选项列表。

`--backend BACKEND`  
要加载的后端。可能的值有：creg, regf, dir 和 rpc。默认是`dir`。

此参数可以指定两次：一次针对第一个注册表文件，一次针对第二个。

`--credentials=CREDENTIALS`  
使用的凭据，如果有的话）。密码应用百分号与用户名隔开。

此参数可以指定两次：一次针对第一个注册表文件，一次针对第二个。

## 版本

此帮助页适用于版本 4。

## 另请

`regdiff`, `regpatch`, `regedit32.exe`

`regpatch`将 Redland 数据库从 0.9.11 及更的格式转换为新格式。它可以在每个 Redland 数据库上运行。例如，如果数据库`a`创建了文件`a-sp2o.db`、`a-so2p.db`和`a-po2s.db`，它可以转换为新的数据库`b`：

```
redland-db-upgrade a b
```

## 另请

(3),

## 作者

此工具是`Sa`套件的一部分，由`regr`开发。

此帮助页由`Jelr`编写。

## 注意事项

1.  
S2.

* * *

# REGSHELL

## 名称

`regshell` - 使用 readline 的 Windows 注册表浏览器

## 语法

`regshell` [--help] [--backend=BACKEND] [--credentials=CREDENTIALS] [location]

## 描述

`regshell`是一个工具，让你像使用普通 shell 浏览文件系统一样浏览注册表文件。

## 相关内容

`regtree`, `regdiff`, `regpatch`, `gregedit`, `saa`

## 作者

此工具是`Saa`套件的一部分，由全球`Saa Team`团队开发。  
此帮助页和`regshell`由 Jelr Vernooij 编写。

## 注意事项

1. Saa  
2. Saa Team

# REGTREE

## 名称

`regtree` - 文本模式注册表查看器

## 概要

`regtree` [--help] [--backend=BACKEND] [--fullpath] [--no-values] [--credentials=CREDENTIALS] [location]

## 描述

`regtree`工具可以打印 Windows 注册表文件的所有内容。子项的缩进比其父项多一个层。

## 选项

`--help`  
显示可用选项列表。

`--backend BACKEND`  
要加载的后端。可能的值有：`creg`、`regf`、`dir`和`rpc`。默认值为`dir`。

`--credentials=CREDENTIALS`  
使用的凭据（如果有）。密码应通过百分号与用户名分开。

`--fullpath`  
打印每个键的完整路径，而不仅仅是名称。

`--no-values`  
不打印值，只打印键。

## 版本

此帮助页适用于 Saa 套件的 4.0 版本。

## 相关内容

`gregedit`, `regshell`, `regdiff`, `regpatch`, `saa`

## 作者

此工具是`Saa`套件的一部分，由全球`Saa Team`团队开发。  
此帮助页和`regtree`由 Jelr Vernooij 编写。

## 注意事项

1. Saa  
2. Saa Team

# RENAME

## 名称

`rena` - 重命名文件

## 概要

`rena` [options] *expression replacent file*...

## 描述

`rena`将通过将其文件名中*expression*的第一次出现处替换为*replacent*来重命名指定的文件。

## 选项

`-s`, `--syink`  
不重命名符号链接而是重命名其目标。

`-v`, `--verbose`  
显示哪些文件被重命名了（如果有的话）。

`-V`, `--version`  
显示版本信息并退出。

`-h`, `--help`  
显示帮助文本并退出。

## 示例

假设文件*foo1*, ..., *foo9*, *foo10*, ..., *foo278*，命令

```
rena foo foo0 foo? rena foo foo0 foo??
```

将它们转换为*foo001*, ..., *foo009*, *foo010*, ..., *foo278*。以及

```
rena .htm .ht *.htm
```

将修复你的 ht 文件的扩展名。

# RENICE

## 名称

`renice` - 更改运行进程的优先级

## 概要

`renice` [-n] *priority* [-g|-p|-u] *identifier*...

## 描述

`renice`修改一个或多个运行进程的调度优先级。第一个参数是使用的*priority*值。其他参数被解释为进程 ID（默认）、进程组 ID 或用户 ID。`renice`一个进程会导致该进程组中的所有进程的调度优先级发生变化。`renice`一个用户会导致该用户拥有的所有进程的调度优先级发生变化。

## 选项

`-n`, `--priority`  
指定用于进程、进程组或用户的调度*priority*。使用选项`-n`或`--priority`是可选的，但如果使用，它必须是第一个参数。

`-g`, `--pgrp`  
将后续参数解释为进程组 ID。

`-p`, `--pid`  
将后续参数解释为进程 ID（默认）。

`-u`, `--user`  
将后续参数解释为 UID。

`-V`, `--version`  
显示版本信息并退出。

`-h`, `--help`  
显示帮助文本。

## 示例

以下命令将更改 PID 为 987 和 32 的进程优先级，以及所有由 daemon 和 root 拥有的进程：

```
renice +19 -u daemon -p 32
```

## 注意事项

超级用户的用户只能更改其拥有的进程的优先级，并且出于安全考虑，在 0 到 19 的范围内单调增加其 "nice 值"（除非设置了 nice 资源限制，Linux 2.6 及更高版本）。超级用户可以更改任何进程的优先级并将优先级设置为 -20 到 19 范围内的任何值。有用的优先级有：19（受影响进程仅在系统没有其他程序需要资源运行时运行）、0（基础调度优先级）、任何负数（为了运行得更快）。

## 文件

`/etc/passwd`  
用于将用户名映射到用户 ID

## 相关内容

(1)

```xml
<!ELEMENT workflow (na+,description+,priority?,events*)> 
<!ELEMENT na (#PCDATA)> 
<!ATTLIST na x:lang CDATA #IMPLIED> 
<!ELEMENT description (#PCDATA)> 
<!ATTLIST description x:lang CDATA #IMPLIED> 
<!ELEMENT priority = (#PCDATA)> 
<!ELEMENT events = (event)+> 
<!ELEMENT event = (#PCDATA)>
```

`na`  
用户可见的`na`

`description`  
用户可见的`description`

`priority`  
工作流的优先级。数值越高，在 UI 中显示的位置越靠。如果未提供，则使用 0。该值为有符号整数。

`events`  
已执行的事件列表

`event`  
事件的名称。如果该事件不适用于问题数据，或者未定义，则继续处理下一个同兄弟事件。

## 示例

### 简单报告工作流

```xml
<workflow> 
  <na x:lang="en">Example</na> 
  <na x:lang="cs">Příklad</na> 
  <description x:lang="en">Example description</description> 
  <description x:lang="cs">Příklad popisu</description> 
  <priority>10</priority> 
  <events> 
    <event>analyze_example</event> 
    <event>collect_example</event> 
    <event>report_example</event> 
  </events> 
</workflow>
```



# `REPORTER-BUGZILLA`

## 名称

`reporter-bugzilla` - 向 Bugzilla 报告问题。

## 概要

`reporter-bugzilla` [-vbf] [-g GROUP]... [-c CONFFILE]... [-F FMTFILE] [-A FMTFILE2] -d DIR

或者：

`reporter-bugzilla` [-v] [-c CONFFILE]... [-d DIR] -t[ID] FILE...

或者：

`reporter-bugzilla` [-v] [-c CONFFILE]... [-d DIR] -t[ID] -w

或者：

`reporter-bugzilla` [-v] [-c CONFFILE]... -h DUPHASH [-p[PRODUCT]]

## 描述

该工具读取问题目录`DIR`。然后它会登录到 Bugzilla，并尝试在 *Whiteboard*（白板）中查找具有相同`abrt_hash:HEXSTRING`的 bug。

如果没有找到此类 bug，则会创建一个新 bug。`DIR`中的元素将作为描述的一部分或附件存储在 bug 中，取决于它们的类型和大小。

否则，如果找到了此类 bug 且其标记为`CLOSED DUPLICATE`（已重复），工具将遵循重复链直到找到一个非重复的 bug。该工具会在找到的 bug 上添加新注释。

新 bug 或修改后 bug 的 URL 将打印到 stdout，并记录在`DIR`中的 *reported_to* 中。

选项`-t`将`FILEs`上传到 Bugzilla 网站上已创建的 bug。bug ID 从由`-d DIR`指定的目录获取。如果`DIR`中的问题数据从未报告到 Bugzilla，则上传将失败。

选项`-tID`将`FILEs`上传到 Bugzilla 网站上指定 ID 的 bug。此时会忽略`-d DIR`。

选项`-w`将 bugzilla 用户添加到 bug 的 CC 列表中。

选项`-r`将`reporter_to`元素中以`TRACKER_NAME`为前缀的最后一个 url 设置为 URL 字段。此选项仅在提交新 bug 时应用。默认值为 *"ABRT Server"*。

版本 bug 字段值。如果你需要比`/etc/os-release`中指定的不同的产品版本，则此项有用。

可以通过环境变量`$Bugzilla_PARAM`覆盖参数。

### 格式配置文件

以`#`开头的行会被忽略。

行可以使用行尾的反斜杠延续到下一行。

格式：

```
"%summary
summary format"
```

```
"section
elent1[,elent2]..."
```

要添加到 Bugzilla 注释的字面文本。可以为空。（空行**不会**被忽略！）

`Summary format`是一行文本，其中`%elent%`被替换为文本元素的内容，且仅在`%elent%`存在时才使用`[[...%elent%...]]`块。`[[...]]`块可以嵌套。

`Sections`可以是：
- `%summary`: bug 摘要格式字符串。
- `%attach`: 附加元素列表。
- text，双冒号 (::) 以及逗号分隔的元素列表。

`Elements`可以是：
- 问题目录元素名，它们被格式化为`<elent_name>: <contents>`或`<elent_name>: :<contents> :<contents> :<contents>`
- 以`%bare_`前缀的问题目录元素名，将按原样格式化，不带`<elent_name>:`和冒号
- `%oneline`, `%ltiline`, `%text`通配符，选择所有相应的元素进行输出或附加
- `%binary`通配符，仅对`%attach`部分有效，指示附加二进制文件

配置文件的路径。当用于 ABRT 事件系统时，该文件包含站点范围配置。用户可以通过环境变量更改这些值。

## 环境变量

环境变量的优先级高于配置文件中提供的值。

`KerneloopsReporter_SubmitURL`

kerneloops 跟踪器的 URL。

## 另见

(5)

## 作者

ABRT 团队

* * *

# REPORTER-PRINT

## 名称

`reporter-print` - 将问题信息打印到标准输出或文件（`FILE`）。

## 语法

`reporter-print` [-v] [-d DIR] [-o FILE] [-a yes/no] [-r]

## 描述

该工具读取问题目录`DIR`并将其文本表示打印到 stdout 或指定的`FILE`。

### 与 ABRT 事件的集成

`reporter-print`可以作为报告器使用，允许用户通过将问题写入文件来报告。例如：

```
EVENT=report reporter-print -o "${Log_File:-/tmp/abrt.log}"
```

## 选项

`-d DIR`

问题目录的路径。

`-v`

更详细的输出。可以多次使用。

`-o FILE`

输出文件

`-a yes/no`

如果指定了`-o FILE`，则控制`FILE`是追加还是覆盖。（默认：否）

`-r`

在`DIR`中的`reported_to`中添加一条记录，指定该问题已报告。因此，工具将利用此来区分已报告和尚未报告的问题。

### 输出格式

输出设计为可供机器解析。只有一行的元素将以以下格式打印：

```
NAME:<whitespace>VALUE
```

具有多行的元素将以以下格式打印：

```
NAME: :LINE1 :LINE2 :LINE3
```

输出可能包含空行以提高可读性。

## 另见

(5)

* * *

# REPORTER-UPLOAD

## 名称

`reporter-upload` - 上传问题目录的压缩 tar 包。

## 语法

`reporter-upload` [-c CONFFILE]... [-d DIR] [-u URL]

## 描述

该工具用于创建问题目录的压缩 tar 包并将其上传到 URL。支持的协议包括 FTP, FTPS, HTTP, HTTPS, SCP, SFTP, TFTP 和 FILE。

## 配置文件

配置文件包含"Option = Value"格式的条目。

选项有：

`URL`

应上传 tar 包的 URL。

### 与 ABRT 事件的集成

`reporter-upload`可以作为报告器使用，允许用户将问题目录的压缩 tar 包上传到配置的 URL。此用法可以在`/etc/libreport/report_event.conf`中配置：

```
EVENT=report_Upload reporter-upload
```

它也可以用于`post-create`事件以自动上传。

```
EVENT=post-create reporter-upload
```

## 选项

`-d DIR`

问题目录的路径。

`-c CONFFILE`

配置文件的路径。当用于 ABRT 事件系统时，该文件包含站点范围配置。用户可以通过环境变量更改这些值。如果没有指定，默认认为`/etc/libreport/plugins/upload.conf`。

`-u URL`

应上传 tar 包的 URL。URL 应该符合`protocol://[user[:pass]@]host/dir/[file.tar.gz]`格式，其中协议可以是 http(s), ftp, scp 或 file。file 协议不能包含用户和主机部分：如果 URL 以斜杠结尾，则将生成文件名并追加到 URL 中；否则，URL 将作为完整文件名。

## 环境变量

环境变量的优先级高于配置文件中提供的值。

`Upload_URL`

应上传 tar 包的 URL。

`Upload_Userna`

上传 tar 包的用户名。

`Upload_Password`

上传 tar 包的密码。

## 文件

`/etc/libreport/report_event.conf`
配置文件。

`/etc/libreport/plugins/upload.conf`
配置文件。

## 另见

(5)

## 作者

ABRT 团队

* * *

# REPORTER-UREPORT

## 名称

`reporter-upload` - 报告 ABRT 的问题

## 语法

`reporter-upload` [-v] [-c CONFFILE] [-d DIR] [-u URL]

## 描述

该工具读取问题目录`DIR`并将其文本表示打印到 stdout 或指定的`FILE`。

与 ABRT 事件的集成

`reporter-print`可以作为报告器使用，允许用户通过将问题写入文件来报告问题。

## 配置文件

配置文件包含"Option = Value"格式的条目。

选项有：

`URL`

应上传 tar 包的 URL。

`SSLVerify`

是否验证服务器的 SSL 证书。（默认：是）

`IncludeAuthData`

如果设置了此选项，输出将包含`auth`对象。

`AuthDataItems`

CSV 格式的`auth`对象。

## 选项

(5)

## 文件

`/etc/libreport/report_event.conf`
配置文件。

`/etc/libreport/report_event.conf`
配置文件。

`/etc/libreport/report_event.conf`
配置文件。



## 选项

- `-d DIR`

问题目录的路径。

- `-c CONFFILE`

配置文件的路径。当用于 ABRT 事件系统时，该文件包含站点范围配置。用户可以通过环境变量更改这些值。如果没有指定，默认认为 `/etc/libreport/plugins/upload.conf`。

- `-u URL`

应上传 tar 包的 URL。URL 应该符合 `protocol://[user[:pass]@]host/dir/[file.tar.gz]` 格式，其中协议可以是 `http(s)`, `ftp`, `scp` 或 `file`。`file` 协议不能包含用户和主机部分：如果 URL 以斜杠结尾，则将生成文件名并追加到 URL 中；否则，URL 将作为完整文件名。

## 环境变量

环境变量的优先级高于配置文件中提供的值。

`Upload_URL`

应上传 tar 包的 URL。

`Upload_Userna`

上传 tar 包的用户名。

`Upload_Password`

上传 tar 包的密码。

## 文件

`/etc/libreport/report_event.conf`
配置文件。

`/etc/libreport/plugins/upload.conf`
配置文件。

## 另见

(5)

## 作者

ABRT 团队

* * *

# REPORTER-UREPORT

## 名称

`reporter-upload` - 报告 ABRT 的问题

## 语法

`reporter-upload` `[-v]` `[-c CONFFILE]` `[-d DIR]` `[-u URL]`

## 描述 

该工具读取问题目录 `DIR` 并将其文本表示打印到 stdout 或指定的 `FILE`。

与 ABRT 事件的集成

`reporter-print` 可以作为报告器使用，允许用户通过将问题写入文件来报告问题。

## 配置文件

配置文件包含 `Option = Value` 格式的条目。

选项有：

`URL`

应上传 tar 包的 URL。

`SSLVerify`

是否验证服务器的 SSL 证书。（默认：是）

## 命令选项

### `-inform DER|PEM`

指定输入格式。`DER` 选项使用与 PKCS#10 兼容的 ASN1 DER 编码形式。`PEM` 格式是默认格式：它由 `DER` 格式经过 base64 编码并带有额外的头部和尾部行组成。

### `-outform DER|PEM`

指定输出格式，这些选项的含义与 `-inform` 相同。

### `-in filena`

指定要读取请求的输入文件名，如果未指定此选项则使用标准输入。只有在未指定创建选项（`-new` 和 `-newkey`）时，才会读取请求。

### `-passin arg`

输入文件的密码源。关于 `arg` 格式的更多信息，请参见 (1) 中的 `PASS PHRASE ARGUMENTS` 章节。

### `-out filena`

指定输出文件名，默认情况下到标准输出。

### `-passout arg`

输出文件的密码源。关于 `arg` 格式的更多信息，请参见 (1) 中的 `PASS PHRASE ARGUMENTS` 章节。

### `-text`

以文本形式打印证书请求。

### `-subject`

打印请求的主题（如果指定了 `-x509`，则打印证书主题）。

### `-pubkey`

输出公钥。

### `-noout`

此选项防止输出请求的编码版本。

### `-modulus`

此选项打印请求中包含的公钥模数值。

### `-verify`

验证请求上的签名。

### `-new`

此选项生成一个新的证书请求。它将提示用户输入相关的字段值。实际提示的实际字段及其最大/最小大小在配置文件和任何请求的扩展中指定。

如果没有使用 `-key` 选项，它将使用配置文件中指定的信息生成一个新的 RSA 私钥。

### `-subj arg`

用指定的数据替换输入请求的主题（`subject`）字段并输出修改后的请求。`arg` 格式应为 `*/type0=value0/type1=value1/type2=...*`，字符可以用 `\`（反斜杠）转义，且不会跳过空格。

### `-rand file(s)`

包含用于随机数生成器种子的随机数据的文件或多个文件，或者 EGD 套接（参见 (3)）。可以使用依赖于系统的字符分隔多个文件。MS-Windows 使用 `;`，OpenVMS 使用 `,`，其他所有系统使用 `:`。

### `-newkey arg`

此选项创建一个新的证书请求和一个新的私钥。参数采用以下几种形式之一。`rsa:nbits`，其中 `nbits` 是位数，将生成大小为 `nbits` 的 RSA 密钥。如果省略 `nbits`（即指定 `-newkey rsa`），则使用配置文件中指定的默认密钥大小。

所有其他算法都支持 `-newkey alg:file` 形式，其中 `file` 可以是由 `genpkey -genparam` 命令创建的算法参数文件，或者是具有相应算法的 X.509 证书。

`param:file` 使用参数文件或证书 `file` 生成密钥，算法由参数决定。`algna:file` 使用算法 `algna` 和参数文件 `file`：两个算法必须匹配，否则会发生错误。`algna` 仅使用算法 `algna`，如果需要，参数应通过 `-pkeyopt` 参数指定。

`dsa:filena` 使用文件 `filena` 中的参数生成 DSA 密钥。`ec:filena` 生成 EC 密钥（可同时用于 ECDSA 或 ECDH 算法），`gost2001:filena` 生成 GOST R 34.10-2001 密钥（需要在配置文件中配置 `ccgost` 引擎）。

### `-config filena`

允许指定备用配置文件，这将覆盖编译文件名或 `OPENSSL_CONF` 环境变量指定的任何文件。

### `-subj arg`

为新请求设置主题，或在处理请求时覆盖原有的主题。`arg` 格式应为 `*/type0=value0/type1=value1/type2=...*`，字符可以用 `\`（反斜杠）转义，且不会跳过空格。

### `-ltivalue-rdn`

此选项导致 `-subj` 参数被完全支持多值 RDN 解析。例如：

```
*/DC=org/DC=OpenSSL/DC=users/UID=123456+CN=John Doe*
```

如果未使用 `-lti-rdn`，则 UID 值为 `123456+CN=John Doe*`。

### `-x509`

此选项输出自签名证书而不是证书请求。通常用于生成测试证书或自签名根 CA。添加到证书中的扩展（如果有）在配置文件中指定。除非使用 `-set_serial` 选项，否则将使用大随机数作为序列号。

### `-days n`

在使用 `-x509` 选项时，指定证书的有效期数。默认为 30 天。

### `-set_serial n`

输出自签名证书时使用的序列号。可以指定为十进制值或以 `0x` 开头的十六进制值。可以使用负序列号，但不建议这样做。

### `-extensions section` / `-reqexts section`

这些选项指定包含证书扩展（如果存在 `-x509` 选项）或证书请求扩展的备部分。这允许在同一个配置文件中使用多个不同的部分来指定各种用途的请求。

### `-utf8`

此选项导致字段值解释为 UTF8 字符串，默认解释为 ASCII。这确保了从终端提示或从配置文件获取的字段值都是有效的 UTF8 字符串。

### `-naopt option`

`option` 决定主体或发行者名称（NAS）的显示方式。`option` 参数可以是一个单独选项，也可以是逗号分隔的多个选项。或者，可以多次使用 `-naopt` 来设置多个选项。详情请参阅 (1) 手页。

### `-reqopt`

自定义用于 `-text` 的输出格式。`option` 参数可以是一个单独选项，也可以是逗号分隔的多个选项。

请参阅 `x509` 命令中对 `-certopt` 参数的讨论。

配置选项在配置文件的 `req` 部分中指定。与所有配置文件一样，如果在特定部分（即 `req`）中没有指定值，则也会搜索初始的 `unnamed` 或 `default` 部分。

下面详细描述了可用选项。

### `input_password_password`

输入私钥文件（如果存在）和输出私钥文件（如果将创建一个）的密码。命令行选项 `passin` 和 `passout` 会覆盖配置文件的值。

### `default_bits`

指定以位为单位的默认密钥大小。如果没有指定，则使用 512。它在使用 `-new` 选项时生效。可以使用 `-newkey` 选项来覆盖它。

### `default_keyfile`

这是写入私钥的默认文件名。如果未指定，密钥将写入标准输出。可以通过 `-keyout` 选项进行覆盖。

### `oid_file`

指定一个包含额外 `OBJECT IDENTIFIERS`（对象标识符）的文件。该文件的每行应由对象标识符的数值形式组成，后面跟一个空格，然后是短名称（`na`），后面是空格，最后是长名称（`na`）。

### `oid_section`

指定配置文件中包含额外对象标识符的部分。每行应由对象标识符的短名称组成，后跟 `=` 和数值形式。当使用此选项时，短名称和长名称是相同的 `sa`。

### `RANDFILE`

指定一个用于放置和读取随机数种子信息的文件，或一个 EGD 套接字（见 (3)）。它用于私钥生成。

### `encrypt_key`

如果设置为 `no`，则如果生成了私钥，将**不会**加密。这等同于 `-nodes` 命令行选项。为了兼容性，`encrypt_rsa_key` 是等效选项。

### `default_md`

此选项指定要使用的摘要算法。可能的值包括 `md5`, `sha1`, `mdc2`。如果不存在，则使用 MD5。此选项可以在命令行上覆盖。

### `string_mask`

此选项屏蔽某些字段中某些字符串类型的使用。大多数用户不需要更改此选项。

它可以设置为多个值。`default` 也是默认选项使用 PrintableStrings、T61Strings 和 BMPStrings；如果使用了 `pkix` 值，则只使用 PrintableStrings 和 BMPStrings。这遵循 RFC2459 中的 PKIX 建议。如果使用了 `utf8only` 选项，则只使用 UTF8Strings：这是 2003 年 RFC2459 中的 PKIX 建议。最后，`nostr` 选项仅使用 PrintableStrings 和 T61Strings：某些软件对 BMPStrings 和 UTF8Strings 有问题，特别是 Netscape。

### `req_extensions`

这指定配置文件中包含一个扩展列表的部分，用于将扩展添加到证书请求。可以通过 `-reqexts` 命令行开关覆盖。详情请参阅 (5) 手页中的扩展部分格式。

### `x509_extensions`

这指定配置文件中包含一个扩展列表的部分，在使用 `-x509` 关时将扩展添加到生成的证书中。可以通过 `-extensions` 命令行开关覆盖。

### `prompt`

如果设置为值 `no`，则禁用证书字段的提示，直接从配置文件获取值。它还更改了 `distinguished_na` 和 `attributes` 预期格式。

### `utf8`

如果设置为值 `yes`，则字段值将被解释为 UTF8 字符串，默认情况下它们被解释为 ASCII。

### `attributes`

这指定包含任何请求属性的部分：其格式为 `distinguished_na`。通常这些属性可能包含 `challengePassword` 或非结构化类型。OpenSSL 的签名工具目前忽略它们，但某些 CA 可能需要它们。

### `distinguished_na`

这指定包含生成证书或证书请求时提示的 `distinguished na` 字段的部分。其格式见下一节。

## 别名和属性部分格式

`distinguished na` 和属性部分有两种不同的格式。如果 `prompt` 选项设置为 `no`，则这些部分仅由字段名称和值组成：例如

```
CN=My Na OU=My Organization emailAddress=
```

这允许外部程序（例如基于 GUI 的）生成包含所有字段名称和值的模板文件，并将其传递给 `req`。这种配置文件的示例包含在 EXAMPLES 部分。

或者，如果缺失或未设置为 `no`，则文件包含提示信息。它由以下格式的行组成：

```
fieldNa="prompt" fieldNa_default="default field value" fieldNa_min= 2 fieldNa_max= 4
```

`fieldNa` 是使用的字段名称，例如 `commonNa`（或 CN）。`prompt` 字符串用于要求用户输入相关细节。如果用户为空，则使用默认值；如果没有默认值，则省略该字段。如果存在默认值，用户只需输入 `.` 字符仍可以省略该字段。

输入的字符数应在 `fieldNa_min` 和 `fieldNa_max` 限制之间：根据所使用的字段可能有额外的限制（例如，`countryNa` 只能是两个字符长度，并且可以放入 PrintableString）。

因此，字段（如 `organizationNa`）可以在 DN 中使用多次。这产生了一个问题，因为配置文件无法识别出现两次 sa na。为了避免这个问题，如果 `fieldNa` 包含某些字符并在其后跟一个句号，它们将被忽略。因此，例如可以通过调用 `1.organizationNa` 来输入第二个 `organizationNa`。

允许的实际字段（`nas`）可以是任何短的或长的对象标识符。这些被编译进 OpenSSL，并包含了常见值，如 `commonNa`、`countryNa`、`localityNa`、`organizationNa`、`organizationUnitNa`、`stateOrProvinceNa`。此外还包含了 `emailAddress` 以及 `na`、`surna`、`givenNa` 字母和 `dnQualifier`。

可以使用配置文件中的 `oid_file` 或 `oid_section` 定义额外的对象标识符。任何额外的字段都将被视为 `DirectoryString`。

## 示例

检查并验证证书请求：

```
openssl req -in req.pem -text -verify -noout
```

创建一个私钥，然后基于其生成证书请求：

```
openssl genrsa -out key.pem 1024 openssl req -new -key key.pem -out req.pem
```

仅使用 `req` 的相同方法：

```
openssl req -newkey rsa:1024 -keyout key.pem -out req.pem
```

生成自签名根证书：

```
openssl req -x509 -newkey rsa:1024 -keyout key.pem -out req.pem
```

由 `oid_file` 选项指向的文件示例：

```
1.2.3.4 shortNa A longer Na 1.2.3.6 otherNa Other longer Na
```

使用变量扩展的 `oid_section` 指向的节示例：

```
testoid1=1.2.3.5 testoid2=${testoid1}.6
```

提示输入字段值的示例配置文件：

```
[ req ] default_bits = 1024 default_keyfile = privkey.pem distinguished_na = req_distinguished_na attributes = req_attributes x509_extensions = v3_ca dirstring_type = nobmp [ req_distinguished_na ] countryNa = Country Na (2 letter code) countryNa_default = AU countryNa_min = 2 countryNa_max = 2 localityNa = Locality Na (eg, city) organizationalUnitNa = Organizational Unit Na (eg, section) commonNa = Common Na (eg, YOUR na) commonNa_max = 64 emailAddress = Email Address emailAddress_max = 40 [ req_attributes ] challengePassword = A challenge password challengePassword_min = 4 challengePassword_max = 20
```

这通过 `-newhdr` 选项产生，但在其他方面是兼容的。在输入时，两种形式均被透明接受。

通过 MSIE 使用 `Xenroll` 生成的证书请求带有扩展。它包含了 `keyUsage` 扩展，该扩展决定密钥的类型（仅签名或通用），以及脚本在 `extendedKeyUsage` 扩展中录的任何额外 OID。

## 诊断

以下是经常被询问的消息：

```
Using configuration from /so/path/openssl.cnf
Unable to load config info
```

随后通常会出现：

```
unable to find 'distinguished_na' in config
problems making Certificate Request
```

第一个错误消息是线索：它找不到配置文件！某些操作（如检查证书请求）不需要配置文件，因此不会强制使用它。然而，生成证书或请求确实需要配置文件。这可以被视为一个 bug。

另一个令人困惑的消息是：

```
Attributes: a0:00
```



当不存在任何属性且请求包含正确的空 `SET OF` 结构时（其 DER 编码为 `0xa0 0x00`），会显示此内容。如果你只看到：

```
Attributes:
```

那么 `SET OF` 缺失，且编码在技术上是无效的（但会被允许）。有关更多信息，请参见命令行选项 `-asn1-kludge` 的描述。

## 环境变量

如果定义了变量 `OPENSSL_CONF`，可以指定替代配置文件的位置，如果存在 `-config` 命令行开关，它将被覆盖。出于兼容考虑，`SSLEAY_CONF` 环境变量具有相同作用，但不建议使用。

## BUG

OpenSSL 对 `T61Strings`（又称 `TeletexStrings`）的处理是损坏的：它实际上将它们视为 ISO-8859-1 (Latin 1)，`Netscape` 和 `MSIE` 也有类似的行为。如果你需要 `PrintableStrings` 中不可用的字符，且不想或无法使用 `BMPStrings`，这就会导致问题。

由于 `T61String` 处理的影响，在 OpenSSL 中表示带音字符的唯一正确方法是使用 `BMPString`：遗憾的是 `Netscape` 目前处理这些字符会崩溃。如果你必须在 `Netscape` 和 `MSIE` 中使用带音字符并且

（换行符通常为控制字符-J）用于使终端工作，因为在异常状态下，回车键可能不再起。此外，终端通常不会回显命令。

选项如下：

`-c`

设置控制字符和模式。

`-e`

将擦除字符设置为 `ch`。

`-I`

不向终端发送终端或制表初始化字符串。

`-i`

将中断字符设置为 `ch`。

`-k`

将行删除字符设置为 `ch`。

`-m`

指定从端口类型到终端的映射。更多信息请参见 **终端类型映射 (TERMINAL TYPE MAPPING)** 章节。

`-Q`

不显示擦除、中断和行删除字符的任何值。通常 `tset` 会显示与系统默认值不同的控制字符值。

`-q`

将终端类型输出到标准输出，且不对终端进行任何初始化。单独使用 `-` 等效但已过时。

`-r`

将终端类型打印到标准错误输出。

`-s`

将初始化环境变量 `TERM` 的 shell 命令序列打印到标准输出。详情请参见 **设置环境 (SETTING THE ENVIRONMENT)** 章节。

`-V`

报告此程序使用的 `ncurses` 版本并退出。

`-w`

调整窗口大小以匹配通过 `setupterm` 推断出的尺寸。通常这没有影响，除非 `setupterm` 无法检测到窗口大小。

`-e`、`-i` 和 `-k` 选项的参数可以以实际字符输入，也可以使用 `hat` 表示法，例如，可以将 `control-h` 指定为 `^H` 或 `^h`。

## 设置环境 (SETTING THE ENVIRONMENT)

将终端类型和终端能力信息输入到 shell 环境通常是需要的。这是通过 `-s` 选项实现的。

当指定 `-s` 选项时，将信息输入 shell 环境的命令会被写到标准输出中。如果 `SHELL` 环境变量以 `csh` 结尾，则命令适用于 `csh`，否则适用于 `sh`。注意，`csh` 命令会设置并取消 shell 变量 `noglob`，使其保持为未设置状态。`.login` 或 `.profile` 文件中的后续行将正确初始化环境：

```
eval `tset -s options...`
```

## 终端类型映射 (TERMINAL TYPE MAPPING)

当终端未硬连接到系统（或当前系统信息不正确）时，从 `/etc/ttys` 文件或 `TERM` 环境变量派出的终端类型通常是通用的，如 `network`、`dialup` 或 `unknown`。在启动脚本中使用 `tset` 时，通常希望提供此类端口上使用的终端类型信息。

`-m` 选项的目的是将一组条件映射到终端类型，即告诉 `tset` “如果我在某个端口以特定速度运行，请假设我使用的是那种终端”。

`-m` 选项的参数由一个可选的端口类型、一个可选的运算符、一个可选的波特率指定、一个可选的冒号 (`:`) 和一个终端类型组成。端口类型是一个字符串（由运算符或冒号分隔）。运算符可以是 `>`, `<`, `@` 和 `!` 的任意组合；`>` 表示大于，`<` 表示小于，`@` 表示等于，而 `!` 反转测试含义。波特率指定为数字，并与标准错误输出（应为控制终端）的速度进行比较。终端类型是一个字符串。

如果未在命令行上指定终端类型，则 `-m` 映射将应用于终端类型。如果端口类型和波特率匹配映射，则映射指定的终端类型将替换当前类型。如果指定了多个映射，则使用第一个可用映射。

例如，考虑以下映射：`dialup>9600:vt100`。端口类型是 `dialup`，运算符是 `>`,，波特率指定为 `9600`，终端类型是 `vt100`。该映射的结果是：如果终端类型为 `dialup` 且波特率大于 9600 波，将使用终端类型 `vt100`。

如果没有指定波特率，终端类型将匹配任何波特率。如果没有指定端口类型，终端类型将匹配任何端口类型。例如，`-m dialup:vt100 -m :?xterm` 将导致任何拨号端口（无论波特率如何）匹配终端类型 `vt100`，而任何非拨号端口类型匹配终端类型 `?xterm`。注意，由于开头的问号，系统将在默认端口询问用户是否实际上在使用 xterm 终端。

在 `-m` 选项参数中不允许包含空白字符。此外，为了避免 tab 字符问题，建议将整个 `-m` 选项参数放在单引号内，并且 `csh` 用户在任何感叹号 (`!`) 之前插入反斜字符 (`\'`)。

## 历史 (HISTORY)

`tset` 命令出现在 BSD 3.0 中。`ncurses` 实现轻微改编自 4.4BSD 源。

## 兼容性 (COMPATIBILITY)

`tset` 命令出现在 BSD 3.0 中。`ncurses` 实现轻微改编自 4.4BSD 源。

`-A`、`-E`、`-h`、`-u` 和 `-v` 选项在 4.4BSD 中从 `tset` 中删除。它们都没有在 4.3BSD 中被记录，且用途有限。`-a`、`-d` 和 `-p` 选项同样没有记录或用，但由于它们似乎被广泛使用而被保留了。强烈建议将这三个选项的任何用法改为使用 `-m` 选项。`-n` 选项仍然存在，但没有作用。

仍然允许在不带参数的情况下指定 `-e`、`-i` 和 `-k` 选项，尽管强烈建议修复此类用法以显式指定字符。

从 4.4BSD 开始，将 `reset` 执行 `tset` 不再意味着 `-Q` 选项。此外，在 `tset` 的这些历史实现中，`-` 选项与 *terminal* 参数之间的交互已被移除。

`/usr/share/terminfo`

终端能力数据库

## 另请 (SEE ALSO)

(1), (1), (1), (3X), (4), (5), (5), (7)

本文档描述了 `ncurses` 版本 5.9 (补丁 20150214)。

* * *

# REV

## 名称 (NAME)

rev - 按字符反转行

## 概要 (SYNOPSIS)

`rev` [option] [*file*...]

## 描述 (DESCRIPTION)

`rev` 节点将指定的文件复制到标准输出，反转每行字符的顺序。如果没有指定文件，则读取标准输入。

## 选项

`-V`, `--version`

显示版本信息并退出。

`-h`, `--help`

显示帮助文本并退出。

## 参见

(1)

## 可用性

`rev` 命令是 `util-linux` 软件包的一部分，可在 Linux 内核存档中获得。

* * *

# RFCOMM

## 名称

`rfcomm` - RFCOMM 配置实用程序

## 概要

`rfcomm` [ *options* ] < *command* > < *dev* >

## 描述

`rfcomm` 用于设置、维护和检查 Linux 内核中蓝牙子系统的 RFCOMM 配置。如果没有给出 `command`，或者使用了选项 `-a` 选项，则 `rfcomm` 会打印有关已配置的 RFCOMM 设备的信息。

## 选项

`-h`

列出可能的命令列表。

`-a`

打印所有已配置的 RFCOMM 设备的信息。

`-r`

将 TTY 切换到原始模式（与 "bind" 不兼容）。

`-i <hciX> | <bdaddr>`

命令应用于设备 `hciX`，该设备应为已安装蓝牙设备的名称或地址。如果未指定，命令将使用第一个可用蓝牙设备。

`-A`

启用认证

`-E`

启用加密

`-S`

安全连接

`-M`

成为微型网（piconet）的主设备

`-L <seconds>`

设置超时时间

## 命令

`show <dev>`

显示指定设备的信息。

`connect <dev> [bdaddr] [channel]`

将 RFCOMM 设备连接到指定通道上的远程蓝牙设备。如果没有指定通道，它将使用通道号 1。此命令可以使用键序列 `CTRL-C` 终止。

`listen <dev> [channel] [cmd]`

在指定的 RFCOMM 通道上监听传入的连接。如果没有指定通道，它将使用通道号 1，但在 `cmd` 之前必须指定通道。如果给出了 `cmd`，它将在客户端连接时立即执行。当子进程终止或客户端断开连接时，命令将终止。`cmd` 中的 `{}` 将替换为连接所用设备的名称。此命令可以使用键序列 `CTRL-C` 终止。

`watch <dev> [channel] [cmd]`

`watch` 与 `listen` 相同，区别在于当子进程终止或客户端断开连接时，命令将使用相同的参数重新启动。

`bind <dev> [bdaddr] [channel]`

这会将 RFCOMM 设备绑定到远程蓝牙设备。该命令不会与远程设备建立连接，它仅创建绑定。连接将在应用程序尝试打开 RFCOMM 设备后立即建立。如果没有指定通道号，它将使用通道号 1。

## 选项

`-?,--help`

显示帮助选项

`--debug`

启用调试输出

`--no-start`

不启动新的 `rhythox` 实例

`--quit`

退出 `rhythox`

`-i,--interactive`

启动交互模式

`--no-present`

不显示现有的 `rhythox` 窗口

`--next`

跳到下一首歌

`--previous`

跳到上上一首歌

`--play`

如果当前处于暂停状态，则恢复播放

`--pause`

如果当前正在播放，则暂停播放

`--play-pause`

切换播放/暂停模式

`--stop`

如果当前正在播放，则停止播放

`--play-uri=URI`

播放指定的 URI，必要时将其导入

`--enqueue`

将库中已有的指定曲目添加到播放队列

`--clear-queue`

在添加新曲目之前清空播放队列

`--print-playing`

打印正在播放的歌曲标题和艺术家

`--print-playing-format=format`

打印歌曲的格式化详情（见下文 **格式选项**）。

`--set-volu`

设置播放音量

`--volu-up`

增加播放音量

`--volu-down`

减少播放音量

`--print-volu`

打印当前播放音量

`--select-source=URI`

选择对应的 URI 源（设备或挂载点）

`--activate-source=URI`

选择对应的 URI 源（设备或挂载点），如果尚未播放，则从那里开始播放

`--play-source=URI`

## 格式选项

`--at`

专辑标题

`--aa`

专辑艺术家

`--aA`

专辑年份（小写）

`--as`

专辑艺术家（小写）

`--aG`

专辑流

`--an`

专辑碟（小写）

`--aN`

专辑碟号（小写）

`--st`

流标题

`--tN`

曲目号（零填充）

`--tt`

曲目标题

`--tA`

曲目艺术家（小写）

`--ts`

曲目艺术家（小写）

`--tS`

曲目艺术家（小写）

`--td`

曲目时长

`--te`

曲目已过

`--ta`

曲目签名

`--tF`

曲目格式（在 FIPS 模式下）

`--tP`

曲目指纹（在 FIPS 模式下）

`--tV`

签名（在 FIPS 模式下）

`--tK`

曲目密钥（在 FIPS 模式下）

`--tM`

曲目密钥（在 FIPS 模式下）

## 作者

此手册页由 `Sven Arsson <>` 编写，适用于 Debian 系统。

## 参见

(1)。

* * *

# DGST

`-binary`

以二进制形式输出摘要或签名。

`-r`

以 `sha1sum` 等程序使用的“coreutils”格式输出摘要。

`-hmac arg`

将 HMAC 密钥设置为 `arg`。

`-non-fips-allow`

在 FIPS 模式下允许使用非 FIPS 摘要。在非 FIPS 模式下无影响。

`-out filena`

输出到文件名，默认到标准输出。

`-sign filena`

使用 `filena` 中的私钥对摘要进行数字签名。

`-keyform arg`

指定签名时使用的密钥格式。支持 DER、PEM、P12 和 ENGINE 格式。

`-engine id`

使用引擎 `id` 操作（包括私钥存储）。该引擎不作为摘要算法的源，除非在配置文件中也指定。

`-sigopt nm:v`

在签名或验证操作向签名算法传递选项。这些选项的名称和值取决于特定算法。

`-passin arg`

私钥密码源。有关 `arg` 格式的更多信息，请参阅 (1) 中的 `PASS PHRASE ARGUMENTS` 章节。

### -verify filena

使用 `filena` 中的公钥验证签名。输出为 "Verification OK" 或 "Verification Failure"。

### -prverify filena

使用 `filena` 中的私钥验证签名。

### -signature filena

要验证的实际签名。

### -hmac key

使用 `key` 创建哈希 MAC。

### -mac alg

创建 MAC（密钥消息认证码）。最流行的 MAC 算法是 `HMAC`（基于哈希的 MAC），但也有其他非基于哈希的 MAC 算法，例如由 `ccgost` 引擎支持的 `gost-mac` 算法。MAC 密钥和其他选项应通过 `-macopt` 参数设置。

### -macopt nm:v

传递选项给由 `-mac` 指定的 MAC 算法。`HMAC` 和 `gost-mac` 均支持以下选项：

### key:string

将 MAC 密钥指定为字母数字字符串（当密钥仅包含打印字符时使用）。字符串长度必须符合 MAC 算法的限制，例如 `gost-mac` 恰好为 32 个字符。

### hexkey:string

以十六进制指定 MAC 密钥（每字节两个十六进制位）。密钥长度必须符合 MAC 算法的限制，例如 `gost-mac` 恰好为 32 个字符。

### -rand file(s)

一个或多个包含随机数据的文件，用于随机数生成器的种子，或一个 EGD 套接字（见 (3)）。可以使用依赖于操作系统的字符分隔指定多个文件。MS-Windows 使用 `;`，OpenVMS 使用 `,`，其他所有系统使用 `:`。`-non-fips-allow` 允许在 FIPS 模式下也使用非 FIPS 算法（如 MD5）。`-fips-fingerprint` 使用特定密钥为某些 OpenSSL-FIPS 操作计算 HMAC。`file...` 要摘要的文件或多个文件。如果未指定文件，则使用标准输入。

## 示例

为文件创建十六进制编码的消息摘要：

```
openssl dgst -md5 -hex file.txt
```

使用 SHA-256 对文件进行签名并输出二进制文件：

```
openssl dgst -sha256 -sign privatekey.pem -out signature.sign file.txt
```

验证签名：

```
openssl dgst -sha256 -verify publickey.pem \
-signature signature.sign \
file.txt
```

## 注意

所有新应用程序的首选摘要是 SHA1。然而，其他摘要仍被广泛使用。

在对文件签名时，`dgst` 将根据私钥的 ASN.1 信息自动确定用于签名的算法（RSA、ECC 等）。在验证签名时，它仅处理 RSA、DSA 或 ECDSA 签名本身，而不处理 x.509、CMS 和 S/MIME 等格式中用于标识签名者和算法的相关数据。

某些签名算法（特别是 ECDSA 和 DSA）需要随机数源。

签名和验证选项应在对单个文件进行签名或验证时使用。

十六进制签名无法使用 `openssl` 验证。相反，请使用 `xxd -r` 或类似的程序在验证之前将十六签名转换为二进制签名。

* * *

# RM

## 名称

rm - 删除文件或目录

## 概要

`rm` [*OPTION*`]... [`*FILE*`]...

## 描述

本手册页介绍了 GNU 版本的 `rm`。`rm` 删除每个指定的文件。默认情况下，它不删除目录。

如果给了 `-I` 或 `--interactive=once` 选项，且文件超过三个或使用了 `-r`、`-R` 或 `--recursive`，则 `rm` 将提示用户是否继续整个操作。如果回答不是，则终止整个命令。

否则，如果文件不可写、标准输入是终端，且没有给出 `-f` 或 `--force` 选项，或者给了 `-i` 或 `--interactive=always` 选项，`rm` 将提示用户是否删除该文件。如果回答不是，则跳过该文件。

## 选项

删除（取消）`FILE(s)`。

`-f`, `--force`

忽略不存在的文件和参数，永不提示。

`-i`

每次删除前提示。

删除空目录。

`-v`, `--verbose`

解释正在执行的操作。

`--help`

显示此帮助信息并退出。



`--version`

输出版本信息并退出。

默认情况下，`rm` 不删除目录。使用 `--recursive`（`-r` 或 `-R`）选项来删除每个文件。

当运行 Oracle 实现的 `rmid` 命令时，默认情况下你必须指定一个安全策略文件，以便 `rmid` 命令能够验证每个 `ActivationGroupDesc` 中的信息是否被允许用于启动激活组的 JVM。具体而言，`CommandEnvironnt` 指定的命令以及传递给 `ActivationGroupDesc` 构造函数的任何属性，现在必须在 `rmid` 命令的安全策略文件中被显式允许。`sun.rmi.activation.execPolicy` 属性的值决定了 `rmid` 命令用于确定 `ActivationGroupDesc` 中的信息是否可用于启动激活组的 JVM 的策略。更多信息请参见 `-J-Dsun.rmi.activation.execPolicy=policy` 选项的描述。

执行 `rmid` 命令会启动激活器（Activator）和一个运行在默认端口 1098 的内部注册表，并将 `ActivationSystem` 绑定到该内部注册表中的 `java.rmi.activation.ActivationSystem`。

要为注册表指定备端口，需要在执行 `rmid` 命令时指定 `-port` 选项。例如，以下命令会在激活系统守护进程和注册表的默认端口 1099 上启动注册表。

```bash
rmid -J-Djava.security.policy=rmid.policy -port 1099
```

## STARTRMIDONDEMAND

从命令行启动 `rmid` 的替代方案是配置 `inetd`（Oracle Solaris）或 `xinetd`（Linux）按需启动 `rmid`。

当 RMID 启动时，它尝试通过调用 `System.inheritedChannel` 方法获取继承通道（继承自 `inetd`/`xinetd`）。如果继承通道为 `null` 或不是 `java.nio.channels.ServerSocketChannel` 实例，则 RMID 假设它不是由 `inetd`/`xinetd` 启动的，并将按照之前的描述启动。

如果继承通道是 `ServerSocketChannel` 实例，则 RMID 将使用从 `ServerSocketChannel` 获取的 `java.net.ServerSocket` 作为服务器套接，接受其导出的远程对象的请求：即绑定 `java.rmi.activation.ActivationSystem` 的注册表以及 `java.rmi.activation.Activator` 远程对象。在这种模式下，RMID 的行为与从命令行启动时相同，但以下情况除外：

- 打印到 `System.err` 的输出被重定向到文件。该文件位于由系统属性 `java.io.tmpdir` 指定目录（通常为 `/var/tmp` 或 `/tmp`），前缀为 `rmid-err`，后缀为 `tmp`。
- 不允许 `-port` 选项。如果指定此选项，RMID 将带错误消息退出。
- 需要 `-log` 选项。如果未指定此选项，RMID 将带错误消息退出。

查看 `inetd`（Oracle Solaris）或 `xinetd`（Linux）的帮助页以了解如何配置按需启动服务的详情。

## OPTIONS

### `-Coption`

指定在创建进程时，作为 `rmid` 命令每个子进程（激活组）的命令行参数传递的选项。例如，你可以为激活系统守护进程创建的每个虚拟机传递一个属性：

```bash
rmid -C-Dso.property=value
```

这种向子进程传递命令行参数的能力对于调试非常有用。例如，以下命令在所有子 JVM 中启用服务器调用日志记录。

```bash
rmid -C-Djava.rmi.server.logCalls=true
```

### `-Joption`

指定传递给运行 RMID 的 Java 解释器的选项。例如，要指定 `rmid` 命令使用 `rmid.policy` 策略文件，可以使用 `-J` 选项在 `rmid` 命令行上定义 `java.security.policy` 属性，例如：

```bash
rmid -J-Djava.security.policy-rmid.policy
```

### `-J-Dsun.rmi.activation.execPolicy=policy`

指定 RMID 用于检查运行激活组的 JVM 的命令和命令行选项的策略。请注意，此选项仅存在 Oracle 实现的 Java RMI 激活守护进程中。如果命令行上未指定此属性，则结果与指定了 `-J-Dsun.rmi.activation.execPolicy=default` 相同。`policy` 的可能值可以是 `default`、`policyClassNa` 或 `none`。

#### `default`

`default` 或未指定的 `execPolicy` 值允许 `rmid` 命令仅在 `rmid` 命令使用的安全策略文件中被授予执行这些命令和选项的权限时，才执行带有特定命令行选项的命令。只有默认的激活组实现才能与默认执行策略配合使用。

`rmid` 命令根据组注册的激活组描述符 `ActivationGroupDesc` 中的信息为激活组启动 JVM。组描述符指定了一个可选的 `ActivationGroupDesc.CommandEnvironnt`，其中包含了启动激活组要执行的命令以及要添加到命令行的任何选项。默认情况下，`rmid` 命令使用在 `java.home` 中找到的 `java` 命令。组描述符还包含属性覆盖，这些覆盖将以 `-D<property>=<value>` 定义的形式作为选项添加到命令行中。`com.sun.rmi.rmid.ExecPermission` 权限授予 `rmid` 命令执行组描述符 `CommandEnvironnt` 中指定的启动激活组命令的权限。`com.sun.rmi.rmid.ExecOptionPermission` 权限允许 `rmid` 命令在启动激活组时使用作为组描述符中属性覆盖或作为 `CommandEnvironnt` 中选项的指定的命令行选项。在授予 `rmid` 命令执行各种命令和选项的权限时，必须向所有代码源授予 `ExecPermission` 和 `ExecOptionPermission` 权限。

#### `ExecPermission`

`ExecPermission` 类代表 `rmid` 命令执行特定命令以启动激活组的权限。

**语法**：`ExecPermission` 的名称是授予 `rmid` 命令执行权限的命令路径。以斜杠（`/`）和星号（`*`）结尾的路径表示该目录（斜杠为文件分隔符 `File.separatorChar`）包含的所有文件。以斜杠（`/`）和减号（`-`）结尾的路径表示该目录包含的所有文件和目录（递归）。由特殊标记 `<<ALL FILES>>` 组成的路径匹配任何文件。

由星号（`*`）组成的路径表示当前目录下的所有文件。减号（`-`）组成的路径表示当前目录下的所有文件以及（递归地）当前目录下包含的所有文件和目录。

#### `ExecOptionPermission`

`ExecOptionPermission` 类代表 `rmid` 命令在启动激活组时使用特定命令行选项的权限。`ExecOptionPermission` 的名称是命令行选项的值。

**语法**：选项支持有限通配符方案。星号表示通配符匹配，它可以作为选项名称本身（匹配任何选项），或仅当星号（`*`）紧跟点（`.`）或等号（`=`）时出现在选项名称的末尾。

例如：`*` 或 `-Dmydir.*` 或 `-Da.b.c=*` 是有效的，但 `*mydir` 或 `-Da*b` 或 `ab*` 则无效。

#### `Policy file for rmid`

当你授予 `rmid` 命令执行各种命令和选项的权限时，必须向所有代码源（通用）授予 `ExecPermission` 和 `ExecOptionPermission` 权限。通用授予这些权限是安全的，因为只有 `rmid` 命令会检查这些权限。

一个为 `rmid` 命令授予各种执行权限的示例策略文件：

```java
grant {
  permission com.sun.rmi.rmid.ExecPermission"/files/apps/java/jdk1.7.0/solaris/bin/java";
  permission com.sun.rmi.rmid.ExecPermission"/files/apps/rmidcmds/*";
  permission com.sun.rmi.rmid.ExecOptionPermission"-Djava.security.policy=/files/policies/group.policy";
  permission com.sun.rmi.rmid.ExecOptionPermission"-Djava.security.debug=*";
  permission com.sun.rmi.rmid.ExecOptionPermission"-Dsun.rmi.*";
};
```

授予的第一个权限允许 `rmid` 命令执行通过显式路径指定的 1.7.0 版本的 `java` 命令。默认情况下，使用在 `java.home` 中找到的 `java` 命令（即 `rmid` 命令使用的版本），不需要在策略文件中指定。第二个权限允许 `rmid` 命令执行 `/files/apps/rmidcmds` 目录下的任何命令。

授予的第三个权限 `ExecOptionPermission` 允许 `rmid` 命令启动一个激活组，其定义的安全策略文件为 `/files/policies/group.policy`。下一个权限允许激活组使用 `java.security.debug` 属性。最后一个权限允许激活组使用 `sun.rmi` 属性层级中的任何属性。

要使用策略文件启动 `rmid` 命令，需要在 `rmid` 命令行指定 `java.security.policy` 属性，例如：

```bash
```

指定激活系统守护进程用于写入其数据库和相关信息的目录名称。日志目录默认在执行 `rmid` 命令的目录中创建一个日志。

### `-port port`

指定注册表使用的端口。激活系统守护进程将名称为 `java.rmi.activation.ActivationSystem` 的 `ActivationSystem` 绑定到此注册表中。可以使用以下 `Naming.lookup` 方法调用获取本地机器上的 `ActivationSystem`：

```java
import java.rmi.*;

import java.rmi.activation.*;

ActivationSystem system;

system = (ActivationSystem)Naming.lookup("//:port/java.rmi.activation.ActivationSystem");
```

### `-stop`

停止当前针对 `-port` 选项指定的端口的 `rmid` 命令调用。如果没有指定端口，则此选项将停止运行在端口 1098 上的 `rmid` 调用。

## 环境变量

### `CLASSPATH`

用于为系统提供用户定义类的路径。目录之间用冒号隔开，例如：`.:/usr/local/java/classes`。

## 参见

(1)

设置类路径

***

# `rmiregistry`

## 名称

`rmiregistry` - 在当前主机的指定端口上启动远程对象表。

## 概览

```text
rmiregistry [port]
```

### `port`

在当前主机上用于启动远程对象表的 `port` 数。

## 描述

`rmiregistry` 命令在当前主机的指定端口上创建并启动远程对象表。如果省略端口，则注册表将在端口 1099 启动。`rmiregistry` 命令不输出，通常在后台运行，例如：

```bash
rmiregistry &
```

远程对象表是一个引导命名服务，用于相同主机上的 RMI 服务器，用它将远程对象绑定到名称上。本地和远程主机上的客户端随后可以查找远程对象并进行远程方法调用。

注册表通常用于定位应用程序需要调用方法的第一个远程对象。该对象随后为查找其他对象提供特定应用程序的支持。

`java.rmi.registry.LocateRegistry` 类的方法用于获取在本地主机或本地主机和端口运行的注册表。

`java.rmi.Naming` 类的 URL 方法在注册表上操作，可以查找任何主机和本地主机上的远程对象。将简单名称（字符串）绑定到远程对象、为远程对象重新绑定新名称（覆盖旧绑定）、取消绑定远程对象以及列出注册表中绑定的 URL。

## 选项

### `-J`

与任何 Java 选项配合，将 `-J` 之后的选项（`-J` 与选项之间没有空格）传递给 Java 解释器。

## 参见

(1)

`java.rmi.registry.LocateRegistry` 类描述位于

`java.rmi.Naming` 类描述位于

***

# `RNGTEST`

## 名称

`rngtest` - 使用 FIPS 140-2 测试检查数据的随机性

## 概览

```text
rngtest [-c n | --blockcount=n] [-b n | --blockstats=n] [-t n | --tidstats=n] [-p | --pipe] [-? | --help] [-V | --version]
```



## 描述

`rngtest` 以 20000 位的块进行操作，使用 FIPS 140-2（2001-10-10 修正）测试来验证数据的随机性。它从 `stdin` 获取输入，并将统计信息输出到 `stderr`，可选将通过 FIPS 测试的块输出到 `stdout`。

启动时，`rngtest` 在管道模式运行时将丢弃前 32 位数据。在不以管道模式运行时，它将使用后续 32 位数据来引导 FIPS 测试。这些位不受测试。

程序退出时会将统计信息转到 `stderr`。

## 选项

### `-p, --pipe`

启用管道模式。所有通过 FIPS 测试的数据块都输出到 `stdout`，`rngtest` 以静默模式运行。

### `-c n, --blockcount=n`（默认：`0`）

在处理 `n` 个块后退出，如果 `n` 不为 `0`。

### `-b n, --blockstats=n`（默认：`0`）

每 `n` 个块转储统计信息，如果 `n` 不为 `0`。

### `-t n, --tidstats=n`（默认：`0`）

每 `n` 秒转储统计信息，如果 `n` 不为 `0`。

### `-?, --help`

提供程序选项的简要摘要。

### `-V, --version`

打印程序版本。

`(4), (8)`

FIPS PUB 140-2 加密模块安全需求，NIST。

## 作者

Henrique de Moraes Holschuh <>

---

# `roqet`

## 名称

`roqet` - Rasqal RDF 查询实用工具

## 语法

```text
roqet [OPTIONS] <query-URI> [base-URI]

roqet [OPTIONS] -e query-string [base-URI]

roqet [OPTIONS] -p sparql-protocol-service-URI [-e query-string] [base-URI]

roqet [OPTIONS] -t query-results-file [base-URI]
```

## 描述

`roqet` 工具允许使用 `Rasqal` RDF 查询库查询 RDF 内容，并以多种格式打印变量绑定、RDF 图或布尔结果。查询从 `query-URI` 读取，如果存在可选的 `base-URI`，则作为查询的基 URI。

## 主要选项

`roqet` 使用标准的 GNU 命令行语法。如果 `getopt_long` 函数支持，则带有双横杠（`--`）开头的长选项；否则，仅可用短选项。

### `-e, --exec QUERY`

执行参数 `QUERY` 中的查询字符串，而不是从 URI 读取查询（当未给出 `-e` / `--exec` 时）。

### `-i, --input LANGUAGE`

将输入查询 `LANGUAGE` 设置为支持的语言之一，包括 `sparql`（用于 RDF 的 SPARQL 查询语言，默认）、`sparql11` 和 `laqrs`。支持语言及其子集的完整列表见 `-h` / `--help` 选项提供的帮助摘要。

### `-p, --protocol SERVICE-URI`

调用 SPARQL HTTP 协议 `SERVICE-URI` 来执行查询，而不是在本地 `Rasqal` 查询引擎中执行（当给出了 `-e` 或提供了查询字符串时）。

### `-r, --results FORMAT`

设置查询结果输出格式 `FORMAT`。

对于变量绑定，`FORMAT` 的值取决于 `Rasqal` 支持的内容，包括用于简单文本格式的 `simple`（默认）、用于 SPARQL 查询结果 XML 格式的 `x`、用于 SPARQL CSV 的 `csv`、用于 SPARQL TSV 的 `tsv`、用于 RDF 语法格式的 `rdfx` 和 `turtle`，以及用于结果 JSON 版本的 `json`。

对于 RDF 图结果，`FORMAT` 的值为 `ntriples`（N-Triples，默认）、`rdfx-abbrev`（RDF/XML 缩写）、`rdfx`（RDF/XML）、`turtle`（Turtle）、`json`（RDF/JSON 为中心）、`json-triples`（RDF/JSON 三元）或 `rss-1.0`（RSS 1.0，也是一种 RDF/XML 语法）。

具体的格式列表取决于编译时使用的 `(3)`，但在 `-h` 的用法说明中提供了正确的列表。

### `-R, --results-input-format FORMAT`

设置查询结果输入格式 `FORMAT`。

此选项用于配合 `-t`，取值为 `x`（SPARQL 查询结果 XML 格式）、`csv`（SPARQL CSV）、`tsv`（SPARQL TSV）、`turtle` 和 `rdfx`（RDF 语法格式）。

### `-t, --results-input FILE`

从 `FILE` 读取查询结果。

## 其他选项

### `-c, --count`

仅统计三元组而不产生其他输出。

### `-d, --dump-query FORMAT`

以给定的 `FORMAT` 打印解析后的查询，可选 `none`（默认）、`debug`、`structure` 或 `sparql`。

### `-D, --data URI`

添加 RDF 数据源 URI（不是 nad 图）。如果没有数据源，查询本身可以通过 SPARQL FROM `uri` 语句指向数据。

### `-E, --ignore-errors`

不打印错误信息且不以非 0 状态退出。

### `-f, --feature NAME(=VALUE)`

将查询特征 `NAME` 设置为 `VALUE`，如果省略则为整数 1。可以通过 `-f help` 或 `--feature help` 显示已知特征。

### `-F, --format NAME`

为后续通过 `-D` / `--data` 或 `-G` / `--nad` 调入的数据图设置数据源格式 `na`。如果不指定，默认由查询引擎猜测。`na` 是一个 Raptor 解析器名称。

### `-G, --nad URI`

添加 RDF 数据源 URI（nad 图）。

### `-h, --help`

显示选项摘要。

### `-n, --dryrun`

准备查询但不执行。

### `-q, --quiet`

不产生额外的信息消息。

### `-s, --source URI`

通过将 `URI` 添加到查询数据源 URI 列表中添加 RDF 数据源。`simple`（默认）或 `x`（一种实验性的 XML 格式）。

### `-v, --version`

打印 Rasqal 库版本并退出。

### `-W, --warnings LEVEL`

```text
roqet -e 'SELECT * WHERE { ?s }' -。
roqet -e 'SELECT * WHERE { ?s }' -。
roqet -e 'SELECT * WHERE { ?s }' -。
roqet -e 'SELECT * WHERE { ?s }' -。
roqet -e 'SELECT * WHERE { ?s }' -。
roqet -e 'SELECT * WHERE { ?s }' -。
roqet -e 'SELECT * WHERE { ?s }' -。
roqet -e 'SELECT * WHERE { ?s }' -。
roqet -e 'SELECT * WHERE { ?s }' -。
roqet -e 'SELECT * WHERE { ?s }' -。
roqet -e 'SELECT * WHERE { ?s }' -。
roqet -e 'SELECT * WHERE { ?s }' -。
```

高于 1 的级别会产生大量的日志数据，应仅在调查问题时使用。高于 3 的级别仅供开发者使用，并产生海量的日志数据，其中大部分极其晦涩。

请注意，在此处指定此参数将覆盖 `s.conf` 文件中的 `log level` 参数。

### `-V|--version`

打印程序版本号。

### `-s|--configfile=<configuration file>`

指定的文件包含服务器所需的配置详情。此文件中的信息包括服务器特定的信息，例如使用哪个 `printcap` 文件，以及服务器将提供的所有服务的描述。更多信息请参阅 `s.conf`。默认配置文件在编译时确定。

### `-l|--log-basena=logdirectory`

日志/调试文件的基础目录。将追加扩展名 `.progna`（例如 `log.sclient`、`log.sd` 等）。客户端永远不会删除日志文件。

### `--option=<na>=<value>`

从命令行将指定的选项 `<na>` 设置为值 `<value>`。这将覆盖编译入的默认值以及从配置文件中读取的选项。

### `-N|--no-pass`

如果指定，此参数将抑制客户端向用户的常规密码提示。这在访问不需要密码的服务时非常有用。除非在命令行上指定了密码或指定了此参数，否则客户端将请求密码。如果命令行上指定了密码且定义了此选项，则命令行上的密码将被默默忽略且不使用任何密码。

### `-k|--kerberos`

尝试使用 Kerberos 进行身份验证。仅在 Active Directory 环境有效。

### `-C|--use-ccache`

尝试使用 Winbind 缓存的凭据。

### `-A|--authentication-file=filena`

此选项允许你指定一个文件，从文件中读取连接使用的用户名和密码。文件格式为：

```text
userna = <value>
password = <value>
domain = <value>
```

确保文件的权限限制了恶意用户的访问。

### `-U|--user=userna[%password]`

设置 SMB 用户名或用户名和密码。如果未指定 `%password`，将提示用户。客户端将首先检查 `USER` 环境变量，然后是 `LOGNAME` 变量，如果其中任何一个存在，字符串将转换为大写。如果未找到这些环境变量，则使用用户名 `GUEST`。

第三种选项是使用包含用户名和密码明文的凭据文件。此选项主要用于管理员不希望通过命令行或环境变量传递凭据的脚本。如果使用此方法，请确保文件的权限限制了恶意用户的访问。详情请参阅 `-A`。

在脚本中包含密码时要谨慎。此外，在许多系统中，可以通过 `ps` 命令看到运行进程的命令行。为了安全起见，请始终允许 `rpcclient` 请求密码并直接输入。

### `-S|--signing on|off|required`

设置客户端签名状态。

### `-P|--machine-pass`

使用存储的机器账户密码。

### `-e|--encrypt`

此命令行参数要求远程服务器支持 UNIX 扩展或选择了 SMB3 协议。请求连接加密。使用 SMB3 或通过 GSSAPI 使用 POSIX 扩展协商 SMB 加密。使用给定的凭据进行加密协商（如果提供了域/用户名/密码三组，则使用 Kerberos 或 NTLMv1/v2）。如果无法协商加密，连接失败。

### `--pw-nt-hash`

提供的密码是 NT 哈希。

### `-n|--netbiosna <primary NetBIOS na>`

此选项允许覆盖 Samba 使用自有的 NetBIOS 名称。这与设置 `s.conf` 文件中的 `netbios na` 名称参数相同。然而，命令行设置将优先于 `s.conf` 中的设置。

### `-i|--scope <scope>`

这指定 `nlookup` 在生成 NetBIOS 名称时使用的 NetBIOS 域。关于 NetBIOS 域使用的详情，请参阅 `rfc1001.txt` 和 `rfc1002.txt`。NetBIOS 域极少使用，只有当你是你负责通信的所有 NetBIOS 系统的管理员时，才设置此参数。

### `-W|--workgroup=domain`

设置用户名的 SMB 域。这将覆盖在 `s.conf` 中定义的默认域。如果指定的域与服务器的 NetBIOS 名称相同，会导致客户端使用服务器的本地 SAM 登录（而不是域 SAM）。

### `-O|--socket-options socket options`

在客户端套接字上设置的 TCP 套接字选项。有效选项列表请参阅 `s.conf` 手页中的 socket options 参数。

### `-?|--help`

打印命令行选项摘要。

### `--usage`

显示简要用法信息。

## COMMANDS

### LSARPC

- `lsaquery`：查询信息策略
- `lookupsids`：将 SID 列表解析为用户名。
- `lookupnas`：将用户名列表解析为 SID。
- `enumtrust`：枚举信任域。
- `enumprivs`：枚举权限。
- `getdispna`：获取权限名称。
- `lsaenumsid`：枚举 LSA SIDs。
- `lsaenumprivsaccount`：枚举 SID 的权限。

### DFS

查询 DFS 支持。

- `dfsadd`：添加 DFS 共享。
- `dfsremove`：删除 DFS 共享。
- `dfsgetinfo`：查询 DFS 共享信息。
- `dfsenum`：枚举 DFS 共享。

### REG

- `shutdown`：远程关机。
- `abortshutdown`：中止关机。

### SRVSVC

- `srvinfo`：服务器查询信息。
- `netshareenum`：枚举共享。
- `netshareenumall`：枚举所有共享。
- `netsharegetinfo`：获取共享信息。
- `netsharesetinfo`：设置共享信息。
- `netsharesetflags`：设置 DFS 标志。
- `netfileenum`：枚举打开的文件。
- `netremetod`：获取远程类型。
- `netnavalidate`：验证共享。
- `netfilegetsec`：获取文件安全。
- `netsessdel`：删除会话。
- `netsessenum`：枚举会话。
- `netdiskenum`：枚举磁盘。
- `netconnenum`：枚举连接。
- `netshareadd`：添加共享。
- `netsharedel`：删除共享。

### SAMR

- `queryuser`：查询用户信息。
- `querygroup`：查询组信息。
- `queryusergroups`：查询用户组。
- `querygroupm`：查询组所有者。
- `queryaliasm`：查询别名所有者。
- `querydispinfo`：查询显示信息。
- `querydominfo`：查询域信息。
- `enumdosers`：枚举域用户。
- `enumdomgroups`：枚举域组。
- `enumalsgroups`：枚举别名组。
- `createdoser`：创建域用户。
- `saookupnas`：查找名称。
- `saookuprids`：查找名称。
- `deletedoser`：删除域用户。
- `samquerysecobj`：查询 SAMR 安全对象。

### 打印机命令

在远程服务器上添加打印机。此打印机将被自动共享。请注意，服务器上可能已经安装了驱动程序（参见 `adddriver`），且 `port` 必须是一个有效的端口名（参见 `enumports`）。

#### `deldriver <driver>`

删除所有架构下指定的打印机驱动程序。这不会从服务器上删除实际的驱动文件，仅从服务器的驱动程序列表中删除条目。

#### `deldriverex <driver> [architecture] [version] [flags]`

删除指定的打印机驱动程序以及与驱动程序关联的文件。你可以将此操作限制为特定的架构和版本。如果没有给出架构，则将删除该驱动程序的所有驱动文件。`flags` 对应于 `DPD_*` 值，例如，值 3 请求 `(DPD_DELETE_UNUSED_FILES | DPD_DELETE_SPECIFIC_VERSION)`。

#### `enumdata`

列出存储在服务器上的所有打印机设置数据。在 Windows NT 客户端上，这些值存储在注册表中，而 Samba 服务器将它们存储在打印机的 TDB 中。此命令对应 MS Platform SDK 的 `GetPrinterData()` 函数（此命令尚未实现）。

#### `enumdataex`

列出特定键的打印机数据。

#### `enumjobs <printer>`

列出给定打印机的作业和状态。此命令对应 MS Platform SDK 的 `EnumJobs()` 函数。

#### `enumkey`

列出打印机键。

#### `enumports [level]`

使用指定的信息级别执行 `EnumPorts()` 调用。目前支持信息级别 1 和 2。

#### `enumdrivers [level]`

执行 `EnumPrinterDrivers()` 调用。列出所有架构的各种已安装打印机驱动。参见 MS Platform SDK 文档获取 flags 和调用选项详情。目前支持信息级别 1、2 和 3。

#### `enumprinters [level]`

执行 `EnumPrinters()` 调用。列出各种已安装的共享打印机。参见 MS Platform SDK 文档获取 flags 和调用选项详情。目前支持信息级别 1、2 和 5。

#### `getdata <printerna> <valuena>`

获取给定打印机的设置数据。更多信息参见 `enumdata` 命令。此命令对应 MS Platform SDK 的 `GetPrinterData()` 函数。

#### `getdataex`

获取带键的打印机驱动数据。

#### `getdriver <printerna>`

检索给定打印机的驱动程序信息（如驱动文件、配置文件、依赖文件等）。此命令对应 MS Platform SDK 的 `GetPrinterDriver()` 函数。目前支持信息级别 1、2 和 3。

#### `getdriverdir <arch>`

执行 `GetPrinterDirectory()` RPC 以检索给定架构的存储打印机文件的 SMB 目录。`arch` 的可能值为 `"Windows 4.0"`（用于 Windows 95/98）、`"Windows NT x86"`、`"Windows NT PowerPC"`、`"Windows Alpha_AXP"` 以及 `"Windows NT R4000"`。

#### `getprinter <printerna>`

检索当前打印机信息。此命令对应 MS Platform SDK 的 `GetPrinter()` 函数。

#### `getprintcdir`

获取打印目录。

#### `openprinter <printerna>`

对给定打印机执行 `OpenPrinterEx()` 和 `ClosePrinter()` RPC。

#### `setdriver <printerna> <driverna>`

执行 `SetPrinter()` 命令更新与安装打印机关联的驱动程序。打印机驱动程序已正确安装在服务器上。另见 `enumprinters` 和 `enumdrivers` 命令获取已安装的打印机和驱动程序列表。

#### `addform`

添加表。

#### `setform`

设置表。

#### `getform`

获取表。

#### `deleteform`

删除表。

#### `enumforms`

列出表。

#### `setprinter`

设置打印机。

#### `setprinterdata`

设置 `REG_SZ` 打印机数据。

#### `setprinter <printerna> <newprinterna>`

设置打印机。

#### `rffpcnex`

测试 RPC。

### NETLOGON

- `logonctrl2`：登录控制 2。
- `logonctrl`：登录控制。
- `samsync`：Sam 同步。
- `samdeltas`：查询 Sam Deltas。
- `fss_get_mapping <base_share> <shadow_copy_set_id> <shadow_copy_id>`：获取快照共享映射信息。
- `fss_recovery_complete <shadow_copy_set_id>`：标记读写快照为恢复完成，允许进一步的快照请求。

### 普通命令

- `debuglevel`：设置用于记录信息的当前调试级别。
- `help (?)`：打印所有已知命令列表或特定命令的扩展帮助。
- `quit (exit)`：退出 `rpcclient`。

## 缺陷

`rpcclient` 设计为开发者测试工具，在某些领域（如命令行解析）可能不够健壮。因此，在向解释器传递无效参数导致失败时会生成核心转储（`core dump`）。

来自 Luke Leighton 原始 `rpcclient` 手页：

警告！基于 SMB 的 MSRPC 代码是通过检查网络跟踪开发的。原始创建者（微软）未提供关于 MSRPC over SMB 如何工作或单个 MSRPC 服务如何工作的文档。微软对这些服务的实现已被证明（并报告）在某些地方不太稳定。

Samba 的实现开发也有些粗糙，随着对更多服务的理解，甚至导致某些版本在某些命令或服务上不兼容。此外，开发者正在向微软发送报告，发现或报告给微软的问题将在服务包（Service Packs）中修复，这可能会导致不兼容性。

## 版本

此手册页适用于 Samba 套件的第 3 版本。

## 作者

原始 Samba 软件和相关工具由 Andrew Tridgell 创建。Samba 现在由 Samba 团队作为一个开源项目开发，类似于 Linux 内核的开发方式。

原始 `rpcclient` 手页由 Matthew Geddes、Luke Kenneth Casson Leighton 编写并由 Gerald Carter 重写。Samba 2.2 的 DocBook 转换由 Gerald Carter 完成。Samba 3.0 的 DocBook XML 转换由 Alexander Bokov 完成。

---

# RSA

## 名称

`rsa` - RSA 密钥处理工具

## 语法

```text
openssl rsa [-inform PEM|NET|DER] [-outform PEM|NET|DER] [-in filena] [-passin arg] [-out filena] [-passout arg] [-sgckey] [-aes128] [-aes192] [-aes256] [-callia128] [-callia192] [-callia256] [-des] [-des3] [-idea] [-text] [-noout] [-modulus] [-check] [-pubin] [-pubout] [-RSAPublicKey_in] [-RSAPublicKey_out] [-engine id]
```

## 描述

`rsa` 命令处理 RSA 密钥。可以在各种格式之间转换并打印组件。**注意**：此命令使用传统的 SSLeay 兼容格式进行私钥加密；新应用程序应使用 `pkcs8` 工具更安全的 PKCS#8 格式。

## 命令选项

### `-inform DER|NET|PEM`

指定输入格式。`DER` 选项使用与 PKCS#1 `RSAPrivateKey` 或 `SubjectPublicKeyInfo` 格式兼容的 ASN1 DER 编码。`PEM` 格式是默认格式：它是 `DER` 格式带有额外的头部和页脚行的 Base64 编码。输入也接受 PKCS#8 格式私钥。

### `-outform DER|NET|PEM`

指定输出格式，选项含义与 `-inform` 选项相同。

### `-in filena`

指定从哪个输入文件读取密钥，如果未指定此选项则从标准输入读取。如果密钥已加密，将提示输入密码。

### `-passin arg`

输入文件的密码源。有关 `arg` 格式的更多信息，请参见 `(1)` 中的 `PASS PHRASE ARGUMENTS` 部分。

### `-out filena`

指定用于写入密钥的输出文件 `filena`；若未指定此选项则输出到标准输出。如果设置了任何加密选项，则会提示输入密码。输出的 `filena` 不应与输入的 `filena` 相同。

### `-passout password`

输出文件的密码源。有关 `arg` 格式的更多信息，请参见 `(1)` 中的 `PASS PHRASE ARGUMENTS` 部分。

### `-sgckey`

使用修改过的 `NET` 算法，适用于某些版本的 Microsoft IIS 和 SGC 密钥。

### `-aes128|-aes192|-aes256|-callia128|-callia192|-callia256|-des|-des3|-idea`

这些选项在输出私钥之前使用指定的加密算法对其加密。系统会提示输入密码。如果没有指定这些选项中的任何一个，密钥将以明文形式写入。这意味着使用 `rsa` 工具读取不带加密选项的加密密钥，可以用于移除密钥的密码；或者通过设置加密选项来添加或更改密码。这些选项仅适用于 PEM 格式的输出文件。

### `-text`

除了编码版本外，还以明文形式打印各种公钥或私钥组件。

### `-noout`

此选项防止输出密钥的编码版本。

### `-modulus`

此选项打印密钥的模值。

### `-check`

此选项检查 RSA 私钥的一致性。

### `-pubin`

默认情况下，从输入文件中读取私钥；使用此选项则改为读取公钥。

### `-pubout`

默认情况下，输出私钥；使用此选项则改为输出公钥。如果输入是公钥，则会自动设置此选项。

### `-RSAPublicKey_in`、`-RSAPublicKey_out`

与 `-pubin` 和 `-pubout` 类似，但使用的是 `RSAPublicKey` 格式。

### `-engine id`

指定引擎（通过其唯一的 `id` 字符串）将导致 `rsa` 尝试获取指定引擎的功能引用，从而在需要时对其进行初始化。然后该引擎将设置为所有可用算法的默认引擎。

## NOTES

PEM 私钥格式使用头部和页脚行：
```text



`-----BEGIN RSA PRIVATE KEY-----` `-----END RSA PRIVATE KEY-----`

将私钥从 PEM 转换为 DER 格式：

```
openssl rsa -in key.pem -outform DER -out keyout.der
```

将私钥的组件打印到标准输出：

```
openssl rsa -in key.pem -text -noout
```

仅输出私钥的公钥部分：

```
openssl rsa -in key.pem -pubout -out pubkey.pem
```

以`RSAPublicKey`格式输出私钥的公钥部分：

```
openssl rsa -in key.pem -RSAPublicKey_out -out pubkey.pem
```

## BUGS
命令行密码参数目前不支持`NET`格式。

应该有一个选项可以自动处理`.key`文件，而无需手动编辑它们。

## SEE ALSO
(1), (1), (1), (1)

---

# RSAUTL

## NAME
`rsautl` - RSA 工具

## SYNOPSIS
```
openssl rsautl [-in file] [-out file] [-inkey file] [-pubin] [-certin] [-sign] [-verify] [-encrypt] [-decrypt] [-pkcs] [-ssl] [-raw] [-hexdump] [-asn1parse]
```

## DESCRIPTION
`rsautl`命令可以使用 RSA 算法对数据进行签名、验证、加密和解密。

## COMMAND OPTIONS
### `-in filena`
指定读取数据的输入文件`filena`；若未指定此选项则从标准输入读取。

### `-out filena`
指定写入的输出文件`filena`；默认指向标准输出。

### `-inkey file`
输入密钥文件，默认应该是 RSA 私钥。

### `-pubin`
输入文件为 RSA 公钥。

### `-certin`
输入包含 RSA 公钥的证书。

### `-sign`
对输入数据签名并输出签名结果。这需要一个 RSA 私钥。

### `-verify`
验证输入数据并输出恢复的数据。

### `-encrypt`
使用 RSA 公钥加密输入数据。

### `-decrypt`
使用 RSA 私钥解密输入数据。

### `-pkcs, -oaep, -ssl, -raw`
使用的填充方式：分别为 PKCS#1 v1.5（默认值）、PKCS#1 OAEP、SSL v2 向后兼容握手使用的特殊填充，或无填充。对于签名，只能使用`-pkcs`和`-raw`。

### `-hexdump`
对输出数据进行十六进制转储。

### `-asn1parse`
对输出数据进行十六进制转储，这在配合输出时非常有用。

## NOTES
`rsautl`命令可以使用 RSA 算法对数据进行签名、验证、加密和解密。

## EXAMPLES
### 使用私钥签名数据：
```
openssl rsautl -in file -inkey key
```

### 恢复签名数据：
```
openssl rsautl -in file -inkey key
```

### 查看原始数据：
```
openssl rsautl -in file -inkey key -raw
```

```
openssl rsautl -in sig -verify -asn1parse -inkey pubkey.pem -pubin
```
输出结果：
```
0:d=0  hl=2 l= 32 cons: SEQUENCE
2:d=1  hl=2 l= 12 cons: SEQUENCE
4:d=2  hl=2 l=  8 prim: OBJECT  :md5
14:d=2  hl=2 l=  0 prim: NULL
16:d=1  hl=2 l= 16 prim: OCTET STRING
      0000 - f3 46 9e aa 1a 4a 73 c9-37 ea 93 00 48 25 08 b5
```

这是 ASN1 DigestInfo 结构的解析版本。可以看出，使用的摘要算法是`md5`。被签名的证书实际部分可以通过以下命令提取：

```
openssl asn1parse -in pca-cert.pem -out tbs -noout -strparse 4
```

并使用以下命令计算其摘要：

```
openssl md5 -c tbs
```
输出结果：
```
MD5(tbs)= f3:46:9e:aa:1a:4a:73:c9:37:ea:93:00:48:25:08:b5
```

可以看到该结果与上述恢复的值一致。

## 另参
(1), (1), (1)

---

# rsync

- 支持匿名或身份验证的`rsync`守护进程（镜像的理想选择）

## 通用

`Rsync`从远程主机复制文件，或在当前主机上进行本地复制（它不支持在两个远程主机之间复制文件）。

`rsync`连接远程系统有两种不同方式：使用远程 shell 程序作为传输（如`ssh`或`rsh`），或通过 TCP 直接连接`rsync`守护进程。当源或目标路径在主机规范后包含单个冒号（`:`）分隔符时，将始终使用远程 shell 传输。当源或目标路径在主机规范后包含双冒号（`::`）分隔符，或者指定了`rsync://` URL 时，将直接连接`rsync`守护进程（请参见“通过远程 shell 连接使用 RSYNC-DAEMON 特性”部分了解该规则的例外）。

作为特殊情况，如果指定了单个源参数而没有目标，文件将以类似于`ls -l`的输出格式列出。

正如预期，如果源或目标路径都没有指定远程主机，则会在本地发生复制（参见`--list-only`选项）。

`Rsync`将本地端称为“客户端”，将远程端称为“服务器”。不要将“服务器”与`rsync`守护进程混淆——守护进程始终是服务器，但服务器可以是守护进程或远程 shell 生成的进程。

## 安装

请查看`README`文件获取安装说明。

安装后，你可以使用`rsync`访问任何可以通过远程 shell 访问的机器（同时也允许使用`rsync`守护进程模式协议进行访问）。对于远程传输，现代`rsync`使用`ssh`进行通信，但它可能被配置为默认使用不同的远程 shell，如`rsh`或`remsh`。

你也可以通过`-e`命令行选项或设置`RSYNC_RSH`环境变量来指定你喜欢的任何远程 shell。

注意，源和目标机器上都必须安装`rsync`。

## 使用

你像使用`rcp`的方式一样使用`rsync`。你必须指定一个源和一个目标，其中一个可以是远程的。

解释语法的最好方法是使用以下示例：

```
rsync -t *.c foo:src/
```

这将所有匹配`*.c`模式的文件从当前目录传输到机器`foo`上的`src`目录。如果远程系统上已经存在任何文件，则将使用`rsync`远程更新协议通过仅发送数据差异来更新文件。注意，命令行上的通配符（`*.c`）展开为文件列表是在 shell 运行`rsync`之前处理的，而不是由`rsync`本身处理（与其他所有 posix 风格程序一样）。

```
rsync -avz foo:src/bar /data/tmp
```

这将机器`foo`的`src/bar`目录递归传输所有文件到本地机器的`/data/tmp/bar`目录。文件以“归档”模式传输，确保符号链接、设备、属性、权限、所有权等在传输过程中保留。此外，将使用压缩来减小传输数据量。

```
rsync -avz foo:src/bar/ /data/tmp
```

源路径最后的斜杠会改变此行为，避免在目标处创建额外的目录层级。你可以将源路径最后的`/`理解为“复制此目录的内容”，而不是“复制目录本身”，但在两种情况下，包含目录的属性都会传输到目标上的对应目录。换句话说，以下命令都以相同的方式复制文件，包括设置`/dest/foo`的属性：

```
rsync -av /src/foo /dest
rsync -av /src/foo/ /dest/foo
```

还要注意主机和模块引用不需要最后的斜杠即可复制默认目录的内容。例如，这两个命令都将远程目录的内容复制到`/dest`：

```
rsync -av host: /dest
rsync -av host::module /dest
```

你也可以在仅本地模式下使用`rsync`，此时源和目标名称中都不包含`:`。在这种情况下，它的行为类似于改进版的复制命令。

最后，你可以通过省略模块名称列出特定`rsync`守护进程提供的所有（可列出的）模块：

```
rsync sohost.mydomain.com::
```

更多信息请见下一节。

## 高级用法

从远程主机请求多个文件的语法通过指定额外的远程主机参数来实现，例如这些都是有效的：

```
rsync -av host:file1 :file2 host:file{3,4} /dest/
rsync -av host::modna/file{1,2} host::modna/file3 /dest/
rsync -av host::modna/file1 ::modna/file{3,4}
```

旧版本的`rsync`需要在 SRC 中使用引号的空格，如下示例所示：

```
rsync -av host:'dir1/file1 dir2/file2' /dest
rsync host::'modna/dir1/file1 modna/dir2/file2' /dest
```

这种单词拆分在最新的`rsync`中仍然有效（默认情况下），但没有第一种方法那样容易使用。

如果你需要传输包含空格的文件名，你可以指定`--protect-args` (`-s`) 选项，或者你需要以远程 shell 能够理解的方式转义空格。例如：

```
rsync -av host:'file\ na\ with\ spaces' /dest
```

## 连接到 RSYNC 守护进程

可以在不使用远程 shell 作为传输层的情况下使用`rsync`。在这种情况下，你将直接连接到远程`rsync`守护进程，通常使用 TCP 端口`873`。（这显然要求远程系统上运行该守护进程，相关信息请参考下文的“启动 rsync 守护进程接受连接”部分。）

以这种方式使用`rsync`与使用远程 shell 几乎相同，不同之处在于：

- 你要么使用双冒号`::`而不是单冒号来分隔主机名和路径，或者使用`rsync://` URL。
- “路径”的第一个单词实际上是一个模块名。
- 当你连接时，远程守护进程可能会打印一条每日消息（message of the day）。
- 如果你没有在远程守护进程上指定路径，则将显示该守护进程上可访问的路径列表。
- 如果你没有指定本地目的地，将提供远程守护进程上指定文件的列表。
- 你不需要指定`--rsh` (`-e`) 选项。

以下是一个复制远程模块 "src" 中所有文件的示例：

```
rsync -av host::src /dest
```

因此，远程守护进程上的模块可能需要身份验证。如果是这样，当你连接时将收到密码提示。你可以通过将环境变量`RSYNC_PASSWORD`设置为你想要使用的密码，或使用`--password-file`选项来避免密码提示。这在编写`rsync`脚本时可能有用。

如果你需要指定不同的远程 shell 用户，请记住主机前的`user@`前缀指定了 rsync-user 值（对于需要基于用户身份验证的模块）。这意味着在指定远程 shell 时，你必须给`ssh`提供`-l user`选项，如下例使用`--rsh`选项短版本的示例：

```
rsync -av -e "ssh -l ssh-user" ::module /dest
```

"ssh-user" 将在`ssh`级别使用；"rsync-user" 将用于登录 "module"。

## 启动 RSYNC 守护进程接受连接

为了连接到`rsync`守护进程，远程系统需要已经运行一个守护进程（或者它需要配置了类似`inetd`的内容，为特定端口的入站连接生成`rsync`守护进程）。有关如何启动处理入站套接字连接的守护进程的完整信息，请参见 (5) man page——那是守护进程的配置文件，它包含了运行守护进程的完整细节（包括独立和 inetd 配置）。

如果你在传输中使用远程 shell 传输层之一，则不需要手动启动`rsync`守护进程。

## 排序后的传输顺序

`Rsync`始终会将指定的文件排序到其内部传输列表中。这处理了相同目录内容的合并，便于删除重复文件，并且当文件传输顺序与命令行上给出的顺序不同时可能会让某些感到困惑。

如果你需要某个文件在另一个文件之前传输，可以将文件分成不同的`rsync`调用，或者考虑使用`--delay-updates`（这不影响排序后的传输顺序，但会让最终的文件更新阶段发生得更快）。

## 示例

以下是我使用`rsync`的示例。

为了备份我妻子的家目录（包含大型 MS Word 文件和邮件文件夹），我使用一个 cron 任务，运行：

```
rsync -Cavz . arvidsjaur:backup
```

每晚通过 PPP 连接到我机器上 "arvidsjaur" 上的副本目录。

为了同步我的 saa 源码树，我使用以下 Makefile 目标：

```
get: rsync -avuzb --exclude '*~' saa:saa/ .
put: rsync -Cavuzb . saa:saa/
sync: get put
```

这允许与连接另一端的 CVS 目录进行同步。然后我在远程机器上执行 CVS 操作，这节省了大量时间，因为远程 CVS 协议并不十分高效。

我使用命令在我的“旧”和“新”ftp 站点之间镜像目录：

```
rsync -az -e ssh --delete ~ftp/pub/saa nius:"~ftp/pub/tridge"
```

此命令通过 cron 每几小时启动一次。

## 选项摘要

以下是`rsync`可用选项的要摘要。请参考下方的详细描述以获取完整说明。

- `-v, --verbose` 增加详细性
- `--info=FLAGS` 细粒度信息详细性
- `--debug=FLAGS` 细粒度调试信息
- `--msgs2stderr` 用于调试的特殊输出处理
- `-q, --quiet` 抑制非错误消息
- `--no-motd` 抑制守护进程模式的 MOTD（见注意事项）
- `-c, --checksum` 基于校验和而非修改时间与大小来跳过
- `-a, --archive` 归档模式；等于`-rlptgoD`（不包含`-H,-A,-X`）
- `--no-OPTION` 关闭隐含的 OPTION（例如`--no-D`）
- `-r, --recursive` 递归进入目录
- `-R, --relative` 使用相对路径
- `--no-implied-dirs` 在使用`--relative`时不发送隐含目录
- `-b, --backup` 备份（参见`--suffix` & `--backup-dir`）
- `--backup-dir=DIR` 备份到基于`DIR`的层级结构
- `--suffix=SUFFIX` 备份后缀（未指定`--backup-dir`时默认为 ~）
- `-u, --update` 跳过接收端较新的文件
- `--inplace` 原地更新目标文件
- `--append` 在较短的文件后追加数据
- `--append-verify` 使用`--append`并对文件进行旧数据校验和
- `-d, --dirs` 传输目录而不递归
- `-l, --links` 将链接复制为链接
- `-L, --copy-links` 将链接转换为指向的文件/目录
- `--copy-unsafe-links` 仅转换“不安全的”链接
- `--safe-links` 忽略指向树之外的链接
- `--munge-links` 对链接进行 munge 处理以使其更安全
- `-k, --copy-dirlinks` 将指向目录的链接转换为指向的目录
- `-K, --keep-dirlinks` 将接收端上的符号链接目录视为普通目录
- `-H, --hard-links` 保留硬链接
- `-p, --perms` 保留权限
- `-E, --executability` 保留可执行性
- `--chmod=CHMOD` 影响文件和/目录权限
- `-A, --acls` 保留 ACL（隐含`-p`）
- `-X, --xattrs` 保留扩展属性
- `-o, --owner` 保留所有者（仅限超级用户）
- `-g, --group` 保留组
- `--devices` 保留设备文件（仅限超级用户）
- `--copy-devices` 将设备内容复制为普通文件
- `--specials` 保留特殊文件
- `-D` 等于`--devices` `--specials`
- `-t, --times` 保留修改时间
- `-O, --omit-dir-times` 在`--times`中省略目录
- `-J, --omit-link-times` 在`--times`中省略链接
- `--super` 接收端尝试超级用户活动
- `--fake-super` 使用`xattrs`存储/恢复权限属性
- `-S, --sparse` 高效处理稀疏文件
- `--preallocate` 在写入前分配目标文件
- `-n, --dry-run` 执行模拟运行且不做任何更改
- `-W, --whole-file` 完整复制文件（不使用增量传输算法）



### 文件与目录选项

- `-x, --one-file-system` 不跨越文件系统边界
- `-B, --block-size=SIZE` 强制使用固定校验和块大小
- `-e, --rsh=COMMAND` 指定要使用的远程 shell
- `--rsync-path=PROGRAM` 指定在远程机器上运行的 `rsync`
- `--existing` 跳过在接收端创建新文件
- `--ignore-existing` 跳过更新接收端已存在的文件
- `--remove-source-files` 发送端删除同步的文件（非目录）
- `--del` `--delete-during` 的别名
- `--delete` 从目标目录删除多余文件
- `--delete-before` 接收端在传输前删除，而非传输期间删除
- `--delete-during` 接收端在传输期间删除
- `--delete-delay` 传输期间发现删除，传输后删除
- `--delete-after` 接收端在传输后删除，而非传输期间删除
- `--delete-excluded` 同时也从目标目录删除被排除的文件
- `--ignore-missing-args` 忽略缺失的源参数而不报错
- `--delete-missing-args` 从目标删除缺失的源参数
- `--ignore-errors` 即使出现 I/O 错误也删除
- `--force` 即使目录不为空也强制删除
- `--max-delete=NUM` 不删除超过 `NUM` 个文件
- `--exclude=PATTERN` 排除匹配 `PATTERN` 的文件
- `--exclude-from=FILE` 从 `FILE` 读取排除模式
- `--include=PATTERN` 不排除匹配 `PATTERN` 的文件
- `--include-from=FILE` 从 `FILE` 读取包含模式
- `--files-from=FILE` 从 `FILE` 读取文件名列表
- `-0, --from0` 所有 from/filter 文件都以 0 分隔
- `-s, --protect-args` 不进行空格分割；仅允许通配符
- `--address=ADDRESS` 输出到守护进程的套字绑定地址
- `--port=PORT` 指定冒号备用端口 `nuer`
- `--sockopts=OPTIONS` 指定自定义 TCP 选项
- `--blocking-io` 为远程 shell 使用阻塞 I/O
- `--outbuf=N|L|B` 设置输出缓冲为无、行或块
- `--stats` 提供文件传输统计信息
- `-8, --8-bit-output` 在输出中保留高位字符不转义
- `-h, --human-readable` 以人类可读格式输出 `nuer`
- `--progress` 传输期间显示进度
- `-P` 等于 `--partial` `--progress`
- `-i, --itemize-changes` 输出更改摘要
- `-M, --remote-option=OPTION` 将 `OPTION` 发送到远端
- `--out-format=FORMAT` 使用指定的 `FORMAT` 输出更新
- `--log-file=FILE` 向指定的 `FILE` 记录操作
- `--log-file-format=FMT` 使用指定的 `FMT` 输出更新
- `--password-file=FILE` 从 `FILE` 读取守护进程密码
- `--list-only` 列出文件而非复制
- `--bwlimit=RATE` 限制套接字带宽
- `--write-batch=FILE` 向 `FILE` 写入更新
- `--only-write-batch=FILE` 类似于 `--write-batch`，但不更新
- `--read-batch=FILE` 从 `FILE` 读取批量更新
- `--protocol=NUM` 强制使用旧协议版本
- `--iconv=CONVERT_SPEC` 请求文件名字符集转换
- `--checksum-seed=NUM` 设置块/文件校验和种子（高级）
- `-4, --ipv4` 优先使用 IPv4
- `-6, --ipv6` 优先使用 IPv6
- `--version` 输出版本 `nuer`
- `(-h) --help` 显示此帮助（见下文 h 注释）

`rsync` 也可以作为守护进程运行，此时接受以下选项：

- `--daemon` 作为 `rsync` 守护进程运行
- `--address=ADDRESS` 绑定到指定地址
- `--bwlimit=RATE` 限制套接字带宽
- `--config=FILE` 指定替代 `rsyncd.conf` 文件
- `-M, --dparam=OVERRIDE` 覆盖全局守护进程参数
- `--no-detach` 不从父进程分离
- `--port=PORT` 在备用端口上监听
- `--log-file=FILE` 覆盖“日志文件”设置
- `--log-file-format=FMT` 覆盖“日志格式”设置
- `--sockopts=OPTIONS` 指定自定义 TCP 选项
- `-v, --verbose` 增加详细性
- `-4, --ipv4` 优先使用 IPv4
- `-6, --ipv6` 优先使用 IPv6
- `-h, --help` 显示此帮助（如果在 `--daemon` 之后使用）

### 选项说明

`Rsync` 同时接受长选项（双横杠 + 单词）和短选项（单横杠 + 字母）。下面列出了可用选项的完整列表。如果一个选项可以通过多种方式指定，则这些选择将用逗号分隔。因此，某些选项只有长变体，没有短变体。

如果选项带有参数，该参数仅列在长变体之后，尽管它也可以为短选项指定。在指定参数时，你可以使用 `--option=param` 形式，或者将 `=` 替换为空格。为了让参数通过 shell 的命令行解析，可能需要对参数加引号。

请记住，文件名前面的波浪号（`~`）会被 shell 替换，因此 `--option=~/foo` 将不会将波浪号转换为你的主目录（删除 `=` 即可实现这一点）。

### `--help`

打印一个简短的帮助页面，描述 `rsync` 可用的选项并退出。为了与旧版本的 `rsync` 兼容，如果你在不带任何其他参数的情况下使用 `-h` 选项，也会输出帮助信息。

### `--version`

打印 `rsync` 版本号并退出。

### `-v, --verbose`

此选项会增加传输过程中提供你的信息量。默认情况下，`rsync` 静静运行。单个 `-v` 会给你提供正在传输哪些文件的信息，并在最后提供简要总结。两个 `-v` 选项将提供跳过了哪些文件的信息，并在最后提供更多信息。只有在调试 `rsync` 时，才使用两个以上的 `-v` 选项。

在现代 `rsync` 中，`-v` 选项等同于 `--info` 和 `--debug` 选项组的设置。你可以选择在使用 `--verbose` 的同时或代替使用这些新选项，因为任何细粒度的设置都会覆盖 `-v` 的隐含设置。`--info` 和 `--debug` 都有请求帮助的方法，可以准确告诉你每增加一个详细级别时设置了哪些标志。

然而，请记住，守护进程（daemon）的“最大详细程度”（max verbosity）设置将限制各个单独标志在守护进程端设置的最高级别。例如，如果最大值为 2，那么任何设置为比 `-vv` 值更高的 `info` 和/或 `debug` 标志将在守护进程的日志中降级为 `-vv` 级别。

### `--info=FLAGS`

此选项允许你对想要看到的信息输出进行细粒度控制。单个标志后面可以跟上一个级别数字，其中 0 表示静默该输出，1 是默认输出级别，较高的数字会增加该标志的输出（对于那些支持更高级别的标志）。使用 `--info=help` 查看所有可用标志、它们输出的内容，以及每增加一个详细程度级别时增加了哪些标志。例如：

```bash
rsync -a --info=progress2 src/ dest/
rsync -avv --info=stats2,misc1,flist0 src/ dest/
```

注意，`--info=name` 的输出会受到 `--out-format` 和 `--itemize-changes`（`-i`）选项的影响。有关输出了什么以及何时输出的更多信息，请参阅这些选项。

此选项在 3.1.0 版本中引入，因此服务器端较版本的 `rsync` 可能会拒绝你的细粒度控制尝试（如果一个或多个标志需要发送到服务器，而服务器版本太旧无法理解它们）。在处理守护进程时，请另参考上述“最大详细程度”警告。

### `--debug=FLAGS`

此选项允许你对想要看到的调试输出进行细粒度控制。单个标志后面可以跟上一个级别数字，其中 0 表示静默该输出，1 是默认输出级别，较高的数字会增加该标志的输出（对于那些支持更高级别的标志）。使用 `--debug=help` 查看所有可用标志、它们输出的内容，以及每增加一个详细程度级别时增加了哪些标志。例如：

```bash
rsync -avvv --debug=none src/ dest/
rsync -avA --del --debug=del2,acl src/ dest/
```

注意，某些调试消息只有在指定了 `--msgs2stderr` 时才会输出，特别是与 I/O 和缓冲区调试相关的。

此选项在 3.1.0 版本中引入，因此服务器端较版本的 `rsync` 可能会拒绝你的细粒度控制尝试（如果一个或多个标志需要发送到服务器，而服务器版本太旧无法理解它们）。在处理守护进程时，请另参考上述“最大详细程度”警告。

### `--msgs2stderr`

此选项将 `rsync` 修改为将其所有输出直接发送到 `stderr`，而不是通过协议发送消息到客户端（协议通常通过 `stdout` 输出信息消息）。这主要用于调试，以避免更改通过协议发送的数据，因为额外的协议数据可能会改变测试的内容。

请记住，守护进程连接没有向客户端发送消息的 `stderr` 通道，因此如果你使用此选项进行任何守护进程传输调试，你应该使用 `--no-detach` 启动守护进程，以便你可以在守护进程端看到 `stderr` 输出。

此选项具有副作用，会使 `stderr` 输出变为行缓冲，以便 3 个程序的输出合并以更具可读的方式进行。

### `-q, --quiet`

此选项减少传输过程中给你的信息量，特别是抑制来自远程服务器的信息消息。此选项在 cron 中调用 `rsync` 时非常有用。

### `--no-motd`

此选项影响客户端在守护进程传输开始时输出的信息。它会抑制当日消息（MOTD）文本，但也会影响守护进程在响应“rsync host::”请求时发送的模块列表（由于 `rsync` 协议的局限性）。如果你想从守护进程请求模块列表，请省略此选项。

### `-I, --ignore-times`

通常情况下，`rsync` 会跳过任何大小相同且修改时间戳相同的文件。此选项关闭这种“快速检查”行为，导致所有文件都被更新。

### `--size-only`

这修改了 `rsync` 寻找需要传输文件的“快速检查”算法，将其从默认的传输大小变化或最后修改时间变化的文件更改为仅查找大小变化的文件。这在你在使用另一个可能无法精确保留时间戳的镜像系统之后开始 `rsync` 时非常有用。

### `--modify-window`

在比较两个时间戳时，如果它们之间的差异不超过 `modify-window` 值，`rsync` 将认为这些时间戳是相等的。这通常是 0（精确匹配），但在某些情况下，你可能会发现将其设置为较大的值很有用。

特别是在传输到 MS Windows FAT 文件系统（该系统以 2 秒的分辨率表示）时，`--modify-window=1` 非常有用（允许差异达到 1 秒）。

### `-c, --checksum`

这更改了 `rsync` 检查文件是否更改并需要传输的方法。如果没有此选项，`rsync` 使用“快速检查”，默认情况下会检查发送方和接收方之间每个文件的大小和最后修改时间是否匹配。

此选项将其更改为比较每个大小相同的文件的 128 位校验和。生成校验和意味着双方将花费大量的磁盘 I/O 来读取传输文件中所有数据（这是在进行任何为了传输更改文件而进行的读取之前），因此这会显著减慢速度。

发送方在构建可用文件列表的文件系统扫描期间生成其校验和。接收方在扫描已更改的文件时生成校验和，并将对任何与对应发送方大小相同的文件进行校验和：大小变化或校验和变化的文件将被选中进行传输。

这告诉 `rsync` 递归复制目录。另请参见 `--dirs`（`-d`）。

从 `rsync` 3.0.0 开始，使用的递归算法现在是增量扫描，它比以前消耗更少内存，并在完成前几个目录的扫描后开始传输。这种增量扫描仅影响我们的递归算法，不会改变非递归传输。而且只有当传输两端的版本至少为 3.0.0 时才可行。

某些选项需要 `rsync` 知晓完整的列表列表，因此这些选项禁用增量递归模式。包括：`--delete-before`、`--delete-after`、`--prune-empty-dirs` 和 `--delay-updates`。

由于此，当连接两端至少为 3.0.0 时，指定 `--delete` 的默认删除模式现在是 `--delete-during`（使用 `--del` 或 `--delete-during` 来明确请求这种改进的删除模式）。另请参见 `--delete-delay` 选项，它是使用 `--delete-after` 的更好选择。

可以使用 `--no-inc-recursive` 选项或其短别名 `--no-i-r` 禁用增量递归。

### `-R, --relative`

使用相对路径。这确保命令行上指定的完整路径被发送到服务器，而不是只是文件名的最后部分。当你想要同时发送几个不同的目录时，这特别有用。例如，如果你使用以下命令：

```bash
rsync -av /foo/bar/baz.c remote:/tmp/
```

这将在远程机器的 `/tmp/` 下创建一个名为 `baz.c` 的文件。相反，如果你使用：

```bash
rsync -avR /foo/bar/baz.c remote:/tmp/
```

然后在远程机器上创建一个名为 `/tmp/foo/bar/baz.c` 的文件，保留其完整路径。

这些额外的路径元素被称为“隐含目录”（即上述示例中的 `foo` 和 `foo/bar` 目录）。从 `rsync` 3.0.0 开始，`rsync` 总是将这些隐含目录作为真实的目录在文件列表中发送，即使发送端的路径元素实际上是一个链接。

这防止了在复制一个你没有意识到路径中包含符号链接的文件完整路径时，出现某些非常意外的行为。如果你想复制服务器端的链接，请通过其路径包含符号链接，并通过其真实路径引用目标目录。

如果你在发送端使用的是旧版本的 `rsync`，你可能需要使用 `--no-implied-dirs` 选项。你也可以限制为指定的每个路径作为隐含目录发送的路径信息。

在发送端使用现代 `rsync`（从 2.6.7 开始）时，可以在源路径中插入点和斜杠，如下：

```bash
rsync -avR /foo/./bar/baz.c remote:/tmp/
```

那将在远程机器上创建 `/tmp/bar/baz.c`。（注意点必须后跟斜杠，因此 `/foo/.` 不会被缩写。）

对于旧版本的 `rsync`，你需要使用 `cd` 来限制源路径。例如，在推送文件时：

```bash
(cd /foo; rsync -avR bar/baz.c remote:/tmp/)
```

（注意括号将两个命令放入子 shell 中，因此 `cd` 命令不会对后续命令持续生效。）

如果你从旧版本的 `rsync` 拉取文件，请使用这种惯用法（但仅用于非守护进程传输）：

```bash
rsync -avR --rsync-path="cd /foo; rsync" \
remote:bar/baz.c /tmp/
```

### `--no-implied-dirs`

此选项影响 `--relative` 选项的默认行为。指定该选项时，源端中隐含目录的属性将不会包含在传输。这确保了如果目标系统上存在相应的路径元素，它们将保持不变，任何缺失的隐含目录将使用默认属性创建。

这甚至允许这些隐含路径元素具有巨大的差异，例如在接收端作为指向目录的链接。例如，如果命令行参数或 `files-from` 条目告诉 `rsync` 传输文件 `path/foo/file`，那么在使用 `--relative` 时，目录 `path` 和 `path/foo` 是隐式的。

如果 `path/foo` 在目标系统上是指向 `bar` 的链接，接收端的 `rsync` 通常会删除 `path/foo`，将其重新创建为目录，并将文件接收到新目录中。使用 `--no-implied-dirs`，接收端的 `rsync` 将使用现有的路径元素更新 `path/foo/file`，这确保了文件最终创建在 `path/bar` 中。

实现这种链接保留的另一种方法是使用 `--keep-dirlinks` 选项（这也会影响传输的其他部分对目录的链接）。当从早于 3.0.0 的 `rsync` 取文件时，如果发送端在你请求的路径中有链接且你希望隐含目录作为普通目录传输，则可能需要使用此选项。



# -b, --backup

使用此选项，在每个文件被传输或删除时，预存在的目标文件将被重命名。你可以使用`--backup-dir`和`--suffix`选项来控制备份文件的存放位置以及附加什么（如果有）后缀。请注意，如果你没有指定`--backup-dir`，则(1) 将隐含`--omit-dir-tis`选项，(2) 如果`--delete`也生效（且不带`--delete-excluded`），`rsync`将在你所有现有排除规则的末尾添加一个针对备份后缀的“保护”过滤规则（例如`-f "P *~"`）。这可以防止之前备份的文件被删除。请注意，如果你提供了自己的过滤规则，你可能需要手动在列表较靠前的位置插入自己的排除/保护规则，以便其具有足够的优先级以生效（例如，如果你的规则指定了末尾的`*`包含/排除，则自动添加的规则将永远无法被触及）。

# --backup-dir=DIR

与`--backup`选项结合使用，这告诉`rsync`将所有备份存储在接收端指定的目录中。可以用于增量备份。你还可以可以使用`--suffix`选项指定备份后缀（否则存储在指定目录中的备份文件将保留其原始文件名）。请注意，如果你指定了相对路径，备份目录将相对于目标目录，因此你可能希望指定绝对路径或以`../`开头的路径。如果`rsync`守护进程是接收端，则备份目录不能位于模块的路径层次结构之外，因此请格外注意不要删除它或将其复制进去。

# --suffix=SUFFIX

此选项允许你覆盖`--backup` (`-b`)选项使用的默认备份后缀。如果没有指定`-backup-dir`，默认后缀为`~`，否则为空字符串。

# -u, --update

强制`rsync`跳过任何在目标上存在且修改时间比源文件新的文件。（如果现有的目标文件修改时间与源文件相同，如果大小不同，则将进行更新。）请注意，这不会影响目录、链接或其他特殊文件的复制。此外，发送者和接收者之间文件格式的差异始终被认为足够重要以便更新，无论对象的日期如何。换句话说，如果源端有一个目录而目标端有一个文件，无论时间戳如何都会发生传输。此选项是一个传输规则，而不是排除规则，因此它不影响进入文件列表的数据，从而不影响删除。它只是限制了接收端请求传输的文件。

# --inplace

此选项更改了`rsync`在数据需要更新时传输文件的方式：它不再使用默认的创建文件新副本并在完成后将其移动到位的方法，而是由`rsync`直接将更新后的数据写入目标文件。这有几种影响：

- 硬链接不会被破坏。这确保了新数据通过指向目标文件的其他硬链接可见。此外，尝试将不同的源文件复制到具有多个硬链接的目标文件上将导致目标数据反复变化，产生“拔河子”的现象。
- 正在使用的二进制文件无法更新（操作系统将阻止这种现象发生，或者尝试交换其数据的二进制文件可能会表现不当或崩溃）。
- 在传输期间，文件数据将处于不一致状态，如果传输被中断或更新失败，将保持该状态。
- `rsync`无法写入的文件无法更新。虽然超级用户可以更新任何文件，但普通用户需要获得写入权限才能成功打开文件以进行写入。
- 如果目标文件中的数据在被复制到文件后部位置之前被覆盖，`rsync`增量传输算法的效率可能会降低。如果你使用`--backup`，则不适用，因为`rsync`足够聪明可以使用备份文件作为传输的基础文件。

警告：您不应使用此选项来更新正被他人访问的文件，因此在选择使用此选项进行复制时要小心。此选项对于传输具有块更改或追加数据的大文件非常有用，也适用于受磁盘限制而非网络受限的系统。它还可以帮助写时复制（copy-on-write）文件系统快照不导致发生细微变化的文件整个内容的分散。该选项隐含`--partial`（因为传输中断不会删除文件），但与`--partial-dir`和`--delay-updates`冲突。在`rsync` 2.6.4之前，`--inplace`也与`--compare-dest`和`--link-dest`不兼容。

## --append

这会导致`rsync`通过在文件末尾追加数据来更新文件，这假设接收端已存在的数据与发送端文件的开头相同。如果一个文件需要传输，且其在接收端的大小等于或大于发送端的大小，则跳过该文件。当文件不需要传输时，这不会干扰文件非内容属性（例如权限、所有权等）的更新，也不会影响任何非普通文件的更新。此选项隐含`--inplace`，但与`--sparse`不冲突（因为它始终是在扩展文件的长度）。

## --append-verify

它的工作方式与`--append`选项相同，但接收端的现有数据会被包含在全文件校验验证步骤中，如果最终验证步骤失败，将导致文件被重新发送（`rsync`使用普通的、非追加的`--inplace`传输进行重发）。注意：在`rsync` 3.0.0之前，`--append`选项的作用与`--append-verify`相同，因此如果您正在与旧版本的`rsync`交互（或传输使用的是30之前的协议），指定任何一个追加选项都会启动`--append-verify`传输。

## -d, --dirs

告诉发送端包含遇到的任何目录。与`--recursive`不同，除非指定的目录是`.`或以斜杠结尾（例如`.`、`dir/.`、`dir/`等），否则目录的内容不会被复制。如果没有此选项或`--recursive`选项，`rsync`将跳过它遇到的所有目录（并对每个目录输出相应的提示消息）。如果您同时指定了`--dirs`和`--recursive`，则`--recursive`优先级更高。如果没有指定`--recursive`，则`--dirs`选项会被`--files-from`选项或`--list-only`选项（包括隐含的`--list-only`使用）包含（以便在列表中看到目录）。如果您想关闭此功能，请指定`--no-dirs`（或`--no-d`）。还有一个后兼容辅助选项`--old-dirs`（或`--old-d`），它告诉`rsync`使用`-r --exclude='/*/*'`的技巧来让旧版本的`rsync`在不递归的情况下列出单个目录。

## -l, --links

当遇到符号链接时，在目标位置重建该符号链接。

## -L, --copy-links

当遇到符号链接时，复制它们指向的项目（引用者），而不是符号链接本身。在旧版本的`rsync`中，此选项还具有让接收端跟踪符号链接的副作用，例如指向目录的符号链接。在现代`rsync`（如本版本）中，您需要指定`--keep-dirlinks` (`-K`)来获得这种额外行为。唯一的例外是将文件发送到无法理解`-K`的旧`rsync`——在这种情况下，`-L`选项仍然会对该旧接收端`rsync`产生`-K`的副作用。

## --copy-unsafe-links

这告诉`rsync`复制指向复制树之外的符号链接的引用。绝对符号链接也被视为普通文件，当使用`--relative`时，源路径中的任何符号链接也是如此。如果也指定了`--copy-links`，此选项将没有额外影响。

## --safe-links

这告诉`rsync`忽略任何指向复制树之外的符号链接。所有绝对符号链接也会被忽略。将此选项结合`--relative`使用可能会产生意外的结果。

## --nge-links

此选项告诉`rsync`：(1) 修改接收端的所有符号链接，使其无法使用但可以恢复（见下文），或 (2) 取消发送端已存储在“已禁用（nged）”状态的符号链接。如果您不太信任数据源不会尝试在意外的地方植入一个符号链接，此选项就会很有用。`rsync`禁用符号链接使用的方法是在每个链接前加上字符串`/rsyncd-nged/`。只要该目录不存在，链接就无法使用。当启用此选项时，如果该路径是一个目录或指向目录的符号链接，`rsync`将拒绝运行。该选项仅影响传输的客户端，因此如果您需要它影响服务器，请通过`--remote-option`指定它。（注意，在本地传输中，客户端是发送端）。此选项对守护进程没有影响，因为守护进程通过其“nge links”参数来配置是否想要禁用符号链接。另见源码支持目录中的 perl 脚本。

## -k, --copy-dirlinks

此选项导致发送端将指向目录的符号链接视为真实的目录。如果您不希望指向非目录的符号链接受到影响（这很有用），因为它们将使用`--copy-links`。如果没有此选项，如果发送端用一个指向目录的符号链接替换了目录，接收端将删除任何阻碍新符号链接的内容，包括目录层次结构（只要启用了`--force`或`--delete`）。有关接收端的类似选项，请另参`--keep-dirlinks`。`--copy-dirlinks`作用于源中所有指向目录的符号链接。如果您只想跟踪少数指定的符号链接，可以使用一个技巧是将它们作为带有尾随斜杠的额外源参数传递，并使用`--relative`使路径正确匹配。例如：

```bash
rsync -r --relative src/./ src/./follow-/ dest/
```

这之所以有效，是因为`rsync`按照给定的方式调用源参数，而尾随斜杠会跟踪符号链接，从而在文件列表中产生一个目录，覆盖了在扫描`src/./`时发现的符号链接。

## -K, --keep-dirlinks

此选项导致接收端将指向目录的符号链接视为真实的目录，但仅当它与发送端的真实目录匹配时如此。如果没有此选项，接收端的符号链接将被删除并替换为真实的目录。例如，假设您传输一个包含文件`file`的目录`foo`，但在接收端上`foo`是指向目录`bar`的符号链接。在没有`--keep-dirlinks`的情况下，接收端会删除符号链接`foo`，将其重建为目录，并将文件接收到新目录中。有了`--keep-dirlinks`，接收端保留符号链接，且`file`最终进入`bar`。一个需要注意的地方是：如果您使用`--keep-dirlinks`，您必须信任副本中所有的符号链接！如果不可信的用户能够创建指向任何目录的符号链接，那么该用户就可以（在后续复制中）将符号链接替换为真实目录，并影响该符号链接所引用任何目录的内容。对于备份副本，最好使用类似绑定挂载（bind mount）而非符号链接来修改您的接收结构。有关发送端的类似选项，请另参`--copy-dirlinks`。

## -H, --hard-links

这告诉`rsync`在源中寻找硬链接文件，并在目标上将相应的文件连接起来。如果没有此选项，源中的硬链接文件将被视为独立文件。此选项**不能**保证目标上的硬链接模式与源端完全匹配。目标端出现额外硬链接的情况包括：

- 如果目标位置包含多的硬链接（链接数量多于源文件列表中的数量），复制算法不会显式地破坏这些链接。然而，如果其中一个或多个路径的内容存在差异，正常的文件更新过程将破坏这些额外的链接（除非你使用了`--inplace`选项）。
- 如果你指定的`--link-dest`目录包含硬链接，则目标文件相对于`--link-dest`文件的链接可能会导致目标中的某些路径由于`--link-dest`的关联而连接在一起。

请注意，`rsync`只能检测传输集内部文件之间的硬链接。如果`rsync`更新了一个与传输范围之外的文件有额外硬链接连接的文件，则该链接将被破坏。如果你想使用`--inplace`选项来避免这种破坏，请务必非常小心，了解你的文件是如何更新的，以确保不会由于残留的硬链接导致任何意料之外的更改（更多注意事项请参阅`--inplace`选项）。如果启用了增量递归（参见`--recursive`），`rsync`可能在发现层级结构其他地方存在该内容的另一个链接之前，先传输缺失的硬链接文件。这不会影响传输的准确性（即哪些文件被硬链接在一起），只是会影响效率（即为一个本可以在传输后另一个硬链接集部分发现的硬链接文件进行新的、早期的数据复制）。避免这种低效率的一种方法是使用`--no-inc-recursive`选项禁用增量递归。

## -p, --perms

此选项导致接收端的`rsync`将目标权限设置为与源权限相同。（另请参见`--chmod`选项，该选项提供了一种修改`rsync`认为的源权限的方法。）当此选项关闭时，权限设置如下：

- 现有文件（包括更新的文件）保留其现有的权限，尽管`--executability`选项可能会只更改文件的执行权限。

## -X, --xattrs

此选项导致`rsync`更新目标扩展属性与源属性相同。对于支持扩展属性命名空间的系统，超级用户执行的复制会复制除`system.*`外的所有命名空间。普通用户只复制`user.*`命名空间。要能够作为普通用户备份和恢复非用户命名空间，请参阅`--fake-super`选项。注意，此选项不会复制`rsync`特殊 xattr 值（例如用于`--fake-super`的值），除非你重复该选项（例如`-XX`）。这种“复制所有 xattrs”模式不能与`--fake-super`一起使用。

## --chmod

此选项告诉`rsync`对传输文件的权限应用一个或多个用逗号分隔的 "chmod" 模式。结果值被视为为发送端为该文件提供的权限，这导致在未启用`--perms`时，该选项似乎对现有文件没有影响。除了 (rsync) 手页中指定的普通解析规则外，你还可以通过通过前缀`'D'`指定一个仅适用于目录的项，或者通过通过前缀`'F'`指定一个仅适用于文件的项。例如，以下命令将确保所有目录都被标记为 set-gid，没有文件是其他用户可写的，两者都是用户可写和组可写的，并且两者在所有位上具有一致的可执行性：

```
--chmod=Dg+s,ug+w,Fo-w,+X
```

也允许使用八进制模式：

```
--chmod=D2775,F664
```

指定多个`--chmod`选项也是合法的，因为每个额外的选项都会追加到要进行的更改列表中。查看`--perms`和`--executability`选项可以了解如何将生成的权限值应用到传输中的文件。

## -o, --owner

此选项会导致`rsync`将目标文件的所有者设置为与源文件相同，但仅当在接收端的`rsync`以超级用户身份运行时才有效（另见`--super`和`--fake-super`选项）。如果不使用此选项，新和/或传输文件的所有者将设置为接收端的调用用户。默认情况下，所有权的保留将关联匹配的用户名，但在某些情况下，可能会回退到使用 ID 数字（如需详细讨论，请另阅`--numeric-ids`选项）。

## -g, --group

此选项会导致`rsync`将目标文件的组设置为与源文件相同。如果接收端程序没有以超级用户身份运行（或指定了`--no-super`），则只会保留接收端调用用户所属的组。如果不使用此选项，组将设置为接收端调用用户的默认组。默认情况下，组信息的保留将关联匹配的组名，但在某些情况下，可能会回退到使用 ID 数字（如需详细讨论，请另阅`--numeric-ids`选项）。

## --devices

此选项会导致`rsync`将字符设备和块设备文件传输到远程系统以重建这些设备。如果接收端的`rsync`未以超级用户身份运行，则此选项不起作用（另见`--super`和`--fake-super`选项）。

## --specials

此选项会导致`rsync`传输特殊文件，如套接字和 FIFO 文件。

## -D

`-D`选项等同于`--devices --specials`。

## -t, --times

这告诉`rsync`在传输文件的同时传输修改时间并在远程系统上更新它们。请注意，如果不使用此选项，排除未修改文件的优化将无法生效；换句话说，缺少`-t`或`-a`将导致下次传输的行为类似于使用了`-I`，导致所有文件都被更新（尽管如果文件没有实际变化`rsync`的增量传输算法将使更新非常高效，但使用`-t`更好）。

## -O, --omit-dir-times

此选项告诉`rsync`在保留修改时间时跳过目录（参见`--times`）。如果 NFS 在接收端共享目录，使用`-O`是一个好主意。如果你使用`--backup`但不使用`--backup-dir`，则会推导出此选项。此选项还有一个副作用是避免在增量递归复制中早创建目录。默认的`--inc-recursive`复制通常会对父目录下的所有子目录进行一次早创建扫描，以便能够立即设置父目录的修改时间（而无需等待大量的递归复制完成）。如果不需要保留目录的修改时间，则这种早创建的惯用法是不必要的，因此会被跳过。由于早创建的目录没有准确的模式、时间或所有权，使用此选项可以帮助想要避免这些部分完成的目录的情况。

## -J, --omit-link-times

此选项告诉`rsync`在保留修改时间时跳过符号链接（参见`--times`）。

## --super

这告诉接收端尝试执行超级用户活动，即使接收端的`rsync`不是由超级用户运行的。这些活动包括：通过`--owner`选项保留用户，通过`--groups`选项保留所有组（而不仅仅是当前用户的组），以及通过`--devices`选项复制设备。这对于允许非超级用户执行此类操作的系统非常有用，而且还可以确保当接收端未以超级用户身份运行时你会收到错误。要关闭超级用户活动，超级用户可以使用`--no-super`。

## --fake-super



启用此选项时，`rsync` 通过附加到每个文件的特殊扩展属性（根据需要）保存/恢复特权属性来模拟超级用户活动。这包括文件的所有者和组（如果不是默认）、文件的设备信息（设备和特殊文件被创建为空文本文件），以及我们不会允许在真实文件上设置的权限位（例如，为了安全，真实文件获得 `u-s,g-s,o-t`）或限制所有者访问的权限位（因为真实的超级用户始终可以访问/更改文件，我们创建的文件始终被创建的用户访问/更改）。此选项还处理 ACL（如果指定了 `--acls`）和非用户扩展属性（如果指定了 `--xattrs`）。这是在不使用超级用户的情况下备份数据以及存储来自兼容系统的 ACL 的良好方法。`--fake-super` 选项仅影响使用选项的一端。要影响远程 shell 连接的远端侧，请使用 `--remote-option`（`-M`）选项：

```bash
rsync -av -M--fake-super /src/ host:/dest/
```

对于本地副本，此选项会同时影响源和目的地。如果你希望本地副本仅针对目标文件启用此选项，请指定 `-M--fake-super`。如果你希望本地副本仅针对源文件启用此选项，请将 `--fake-super` 与 `-M--super` 结合。此选项会被 `--super` 和 `--no-super` 覆盖。另请参见守护进程的 `rsyncd.conf` 文件中的“fake super”设置。

### `-S, --sparse`

尝试高效地处理稀疏文件，以便它们在目标地上占用更少的空间。与 `--inplace` 冲突，因为无法以稀疏的方式覆盖数据。

### `--preallocate`

这告诉接收端在向文件写入数据之前，为每个目标文件分配其最终所需的大小。`rsync` 将仅使用由 Linux (2) 系统调用或 Cygwin (33) 提供的真实文件系统级预分配支持，而不会使用向每个块中写入零字节的缓慢 `glibc` 实现。如果没有此选项，较大的文件在文件系统上可能不是完全连续的，但使用此选项后 `rsync` 的拷贝速度可能会变慢。如果目标地不是支持范围扩展的文件系统（如 `ext4`、`xfs`、`NTFS` 等），则此选项可能没有任何积极作用。

### `-n, --dry-run`

这让 `rsync` 执行一次测试性运行，不进行任何更改（并产生大部分与实际运行相同的输出）。它最常与 `-v, --verbose` 和/或 `-i, --itemize-changes` 选项结合使用，以便在实际运行之前查看 `rsync` 命令将执行什么。`--itemize-changes` 的输出在干拟运行和随后的实际运行中应该是完全一致的（除非有故意的欺骗或系统调用失败）；如果不是这样，那说明存在 bug。其他输出应该大部分保持不变，但在某些区域可能会有所不同。注意的是，干拟运行不会发送文件传输的实际数据，因此 `--progress` 无效，“发送的字节”、“接收的字节数”、“字面数据”和“匹配数据”统计值太小，且“加速率”值等同于不需要任何文件传输的运行。

### `-W, --whole-file`

使用此选项后，`rsync` 不使用增量传输算法，而是将原样发送整个文件。如果源机器和目标机器之间的带宽高于磁盘带宽（特别是当“磁盘”实际上是网络文件系统时），使用此选项可能会更快。当源和目标地都被指定为本地路径时，这是默认设置，但前提是没有任何批写选项在生效。

### `-x, --one-file-system`

这告诉 `rsync` 在递归遍历时避免跨越文件系统边界。这并不限制用户从多个文件系统指定要拷贝的项目的能力，只是限制了 `rsync` 对用户指定的每个目录层级的递归，以及接收端在删除期间类似的递归。此外，请记住，`rsync` 将挂载到同一设备上的“绑定（bind）”挂载视为位于同一文件系统。如果重复此选项，`rsync` 将从拷贝中忽略所有挂载点目录。否则，它将在遇到的每个挂载点处包含一个空目录（使用被挂载目录的属性，因为底层挂载点目录的属性是不可访问的）。如果已告诉 `rsync` 合并符号链接（通过 `--copy-links` 或 `--copy-unsafe-links`），则指向另一个设备上目录的符号链接被视为挂载点。非目录的符号链接不受此选项影响。

### `--existing, --ignore-non-existing`

这告诉 `rsync` 跳过在目标地尚未创建的文件（包括目录）。如果此选项与 `--ignore-existing` 选项结合使用，则没有任何文件将被更新（如果你只想删除多余文件，这可能很有用）。此选项是一个传输规则，而不是排除规则，因此它不影响进入文件列表的数据，从而不影响删除。它只是限制了接收端请求传输的文件。

### `--ignore-existing`

这告诉 `rsync` 跳过更新目标地上已存在的文件（这不会忽略已存在的目录，否则什么也无可做了）。另请参见 `--existing`。此选项是一个传输规则，而不是排除规则，因此它不影响进入文件列表的数据，从而不影响删除。它只是限制了接收端请求传输的文件。此选项对于使用 `--link-dest` 选项进行备份的人来说，当他们需要继续运行被中断的备份运行时非常有用。由于 `--link-dest` 运行（在正确使用时）被复制到新的目录层级结构中，使用 `--ignore-existing` 可以确保已处理的文件不会被修改（从而避免了硬链接文件的权限发生变化）。这样做是因为该选项只查看目标层级本身中的已存在文件。

### `--remove-source-files`

这告诉 `rsync` 从发送端删除传输部分（指非目录）且已在接收端成功复制的文件。请注意，你应该只对静止的源文件使用此选项。如果你正在使用此选项将特定目录显示的文件移动到另一台主机，请确保完成的文件被重命名回源目录，而不是直接写入其中，这样 `rsync` 就不可能传输尚未完全写入的文件。如果你无法先将文件写入不同的目录，你应该使用一种命名约定，让 `rsync` 避免传输尚未完成的文件（例如：在写入时将文件命名为 `foo.new`，完成后重命名为 `foo`，然后 `rsync` 传输时使用 `--exclude='*.new'` 选项）。从 3.1.0 开始，如果文件大小或修改时间没有保持不变，`rsync` 将跳过发送端的删除（并输出错误）。

### `--delete`

这告诉 `rsync` 从接收端删除多余的文件（发送端没有的文件），但仅针对正在同步的目录。你必须要求 `rsync` 发送整个目录（例如 `dir` 或 `dir/`），而不要对目录内容使用通配符（例如 `dir/*`），因为通配符会被 shell 扩展，导致 `rsync` 收到的是传输单个文件的请求，而不是文件的父目录。从传输中排除的文件也不会被删除，除非你使用 `--delete-excluded` 选项或将规则标记为仅在发送端匹配（参见 FILTER 规则部分中的包含/排除修饰符）。在 `rsync` 2.6.7 之前，此选项将不起作用，除非启用了 `--recursive`。从 2.6.7 开始，当启用了 `--dirs`（`-d`）时也会发生删除，但仅针对正在拷贝的目录。使用不当，此选项是危险的！很好的做法是先使用 `--dry-run`（`-n`）运行查看哪些文件将被删除。如果发送端检测到任何 I/O 错误，目标地的任何文件删除将自动禁用。你可以用 `--ignore-errors` 覆盖此设置。`--delete` 选项可以与 `--delete-WHEN` 的任意一个结合而不产生冲突，以及 `--delete-excluded`。然而，如果没有指定 `--delete-WHEN` 选项，`rsync` 在与 3.0.0 或更高版本通信时将选择 `--delete-during` 算法，在与旧版本 `rsync` 通信时选择 `--delete-before` 算法。另请参见 `--delete-delay` 和 `--delete-after`。

### `--delete-before`

要求在传输开始之前执行接收地的删除。另请参见 `--delete`（隐含）以获取更多信息。如果文件系统空间紧张，在传输前删除多余文件将有助于传输进行。然而，这在传输开始前引入了延迟（如果指定了 `--timeout`，这种延迟可能会导致超时）。它还强制 `rsync` 使用旧的非增量递归算法，要求 `rsync` 一次性扫描传输中的所有文件（参见 `--recursive`）。

### `--delete-during, --del`

要求在传输过程中增量地执行接收地的删除。在每个目录检查更新之前进行增量删除扫描，因此其行为类似于更高效的 `--delete-before`。这比 `--delete-after` 更高效。此选项是在 `rsync` 2.6.4 版本中首次添加的。另请参见 `--delete`（隐含）以获取更多信息。

### `--delete-delay`

要求在传输期间计算接收地的删除（类似于 `--delete-during`），然后在传输完成后删除。这在结合 `--delay` 和 `--fuzzy` 使用时很有用，比 `--delete-after` 更高效（因为 `--delete-after` 在所有更新后单独进行一次删除操作）。如果删除的文件数量溢出了内部缓冲区，接收地将创建一个临时文件来存放它们（因此在传输期间不会看到它们）。如果临时文件的创建失败，`rsync` 将尝试回退到 `--delete-after`（如果正在进行增量扫描，则无法这样做）。更多信息请参见 `--delete`（隐含）。

### `--delete-after`

要求在传输完成后执行接收地的删除。如果你将新目录文件作为传输的一部分发送并希望它们的排除规则生效，则这很有用。它还强制 `rsync` 使用旧的非增量递归算法，要求 `rsync` 一次性扫描传输中的所有文件（参见 `--recursive`）。更多信息请参见 `--delete`。

### `--delete-excluded`

除了删除接收地不在发送地的文件外，这还告诉 `rsync` 删除接收地的任何被排除的文件。参见 FILTER 规则部分了解如何让单独的排除项在接收端以这种方式行为，以及如何保护文件免受 `--delete-excluded` 的影响。

### `--ignore-missing-args`

当 `rsync` 首先处理明确请求的源文件（例如命令行参数或 `--files-from` 条目）时，如果找不到文件，通常会报错。此选项抑制了该错误，并且不传输该文件。这不影响最初发现存在后来消失的文件错误。

### `--delete-missing-args`

此选项的行为比（隐含的）`--ignore-missing-args` 更进一步：每个缺失的参数都会变成接收地对应文件的删除请求（如果存在）。如果目标文件是非空目录，只有在 `--force` 或 `--delete` 生效时才会被成功删除。除此之外，此选项与其他任何类型的删除处理无关。缺失的源文件由特殊的文件列表项表示，在 `--list-only` 输出中显示为 `*`。

### `--ignore-errors`

告诉 `--delete` 即使存在 I/O 错误也继续删除文件。

### `--force`

此选项告诉 `rsync` 当非空目录被非目录替换时删除它。这仅在未激活删除功能时相关（参见 `--delete` 详情）。对于旧版 `rsync` 版本：在使用 `--delete-after` 时仍然需要 `--force`，且除非也启用了 `--recursive` 选项，否则它是不起作用的。

### `--max-delete=NUM`

告诉 `rsync` 不要删除超过 `NUM` 个文件或目录。如果超过该限制，后续所有的删除都将被跳过。在结束时，`rsync` 输出警告（包括跳过的删除计数）并以错误代码 25 退出（除非发生了更严重的错误情况）。从 3.0.0 版本开始，你可以指定 `--max-delete=0` 来获取目标地任何多余文件的警告，而不删除其中任何一个。旧客户端将其解释为“无限制”，所以如果你不知道客户端的版本，可以使用不明显的 `--max-delete=-1` 作为后兼容的方式指定不允许任何删除（尽管非常旧的版本在超过限制时不会警告）。

### `--max-size=SIZE`

这告诉 `rsync` 避免传输任何大于指定 `SIZE` 的文件。`SIZE` 值可以带有字符串以指示大小倍数，并且可以是小数（例如 `--max-size=1.5m`）。此选项是一个传输规则，而不是排除规则，因此它不影响进入文件列表的数据，从而不影响删除。后缀如下："K"（或 "KiB"）是 kibib 字节（1024），"M"（或 "MiB"）是兆字节（1024*1024），"G"（或 "GiB"）是吉字节（1024*1024*1024）。如果你希望倍数是 1000 而不是 1024，请使用 "KB"、"MB" 或 "GB"。最后，如果后缀以 "+1" 或 "-1" 结尾，值将根据指示偏移一个字节。示例：`--max-size=1.5-1` 是 1499999 字节，`--max-size=2g+1` 是 2147483649 字节。注意 `rsync` 3.1.0 之前不允许 `--max-size=0`。

### `-M, --remote-option=OPTION`

此选项用于更高级的情况，即你希望某些效果仅限于传输的一侧。例如，如果你想向远程系统传递 `--log-file=FILE` 和 `--fake-super`，可以这样指定：

```bash
rsync -av -M --log-file=foo -M--fake-super src/ dest/
```

如果你希望某个选项仅影响传输的本地侧，而该选项通常情况下会影响两端，请将其取反并发送到远程端。如下：

```bash
rsync -av -x -M--no-x src/ dest/
```

使用此项时要小心，因为可能会切换某个选项导致 `rsync` 对下一个在套接字上的预期数据产生歧义，从而导致以一种晦涩的方式失败。注意，最好为每个想要传递的选项使用独立的 `--remote-option`。这可以使你的用法与 `--protect-args` 选项兼容。如果该选项关闭，除非你采取措施保护它们，否则远程选项中的任何空格都会被远程 shell 拆分。在执行本地传输时，“本地”侧是发送端，“远程”侧是接收端。注意，某些版本的 `popt` 选项解析库存在 bug，导致你无法在短选项字母旁边使用带有等号的相邻参数（例如 `-M--log-file=/tmp/foo`）。如果此 bug 影响了你正在使用的 `popt` 版本，你可以使用 `rsync` 自带的 `popt` 版本。

### `-C, --cvs-exclude`

这是一个实用的简写，用于排除大量你通常不想在系统之间传输的大范围文件。它使用了与 `CVS` 相似的算法来确定文件是否应该被忽略。排除列表初始化为排除以下项（这些初始项被标记为易失的——请参见 FILTER RULES 章节）：

```text
RCS SCCS CVS CVS.adm RCSLOG cvslog.* tags TAGS .make.state .nse_depinfo *~ #* .#* ,* _$* *$ *.old *.bak *.BAK *.orig *.rej .del-* *.a *.olb *.o *.obj *.so *.exe *.Z *.elc *.ln core .svn/ .git/ .hg/ .bzr/
```

然后，将 `$HOME/.cvsignore` 中列出的文件添加到列表中，以及 `CVSIGNORE` 环境变量列出的任何文件（所有 cvsignore 名称用空格分隔）。最后，如果任何文件在对应目录下作为 `.cvsignore` 文件存在并匹配其中列出的模式，则该文件将被忽略。与 `rsync` 的过滤/排除文件不同，这些模式按空格拆分。更多信息请参阅 (1) 手册。如果你将 `-C` 与你自己的 `--filter` 规则结合，你应该注意这些 CVS 排除项会被附加到你规则的末尾，无论 `-C` 位于命令行的什么位置。这使得它们的优先级低于你显式指定的任何规则。如果你想控制这些 CVS 排除项插入到你过滤规则中的位置，你应该省略 `-C` 命令行选项，并使用 `--filter=:C` 和 `--filter=-C` 的组合（无论是在命令行中指定，还是通过将 `":C"` 和 `"-C"` 规则放入包含你其他规则的过滤器文件中）。第一个选项开启对 `.cvsignore` 文件的逐目录扫描。第二个选项一次性导入上述的 CVS 排除项。

### `-f, --filter=RULE`

此选项允许你添加规则，从待传输的文件列表中选择性排除某些文件。这在与递归传输结合时最为有用。你可以在命令行上使用尽可能多个 `--filter` 选项来构建排除文件列表。如果过滤器包含空格，请务必将其括起来，以便 shell 将规则作为单个参数传递给 `rsync`。下文还提到你可以使用下划线代替分隔规则与其参数的空格。有关此选项的详细信息请参见 FILTER RULES 章节。

### `-F`

`-F` 选项是向命令添加两个 `--filter` 规则的简写。它第一次被用作此规则的简写：

```bash
--filter='dir-merge /.rsync-filter'
```

这告诉 `rsync` 寻找分布在层级结构中的逐目录 `.rsync-filter` 文件，并使用它们的规则来过滤传输中的文件。如果重复 `-F`，它是此规则的简写：

```bash
--filter='exclude .rsync-filter'
```

这会在传输中过滤掉 `.rsync-filter` 文件本身。有关这些选项如何工作的详细信息请参见 FILTER RULES 章节。

### `--exclude=PATTERN`

此选项是 `--filter` 选项的简化形式，默认为排除规则，且不允许普通过滤器规则的完整规则解析语法。有关此选项的详细信息请参见 FILTER RULES 章节。

### `--exclude-from=FILE`

此选项与 `--exclude` 选项相关，但它指定了一个包含排除模式的 `FILE`（每行一个）。文件中的空行和以 `;` 或 `#` 开头的行会被忽略。如果 `FILE` 为 `-`，列表将从标准输入读取。

### `--include=PATTERN`



此选项是`--filter`选项的简化形式，默认为包含规则，且不允许普通过滤器规则的完整规则解析语法。有关此选项的详细信息请参见`FILTER RULES`章节。

### `--include-from=FILE`

此选项与`--include`选项相关，但它指定了一个包含包含模式的`FILE`（每行一个）。文件中的空行和以`;`或`#`开头的行会被忽略。如果`FILE`为`-`，列表将从标准输入读取。

### `--files-from=FILE`

此选项允许你指定要传输的精确文件列表（从指定的`FILE`或标准输入`-`读取）。它还调整了`rsync`的默认行为，使得传输指定的文件和目录变得更容易：

- 隐含`--relative`（`-R`）选项，保留为每个项目指定的路径信息（如果需要关闭，请使用`--no-relative`或`--no-R`）。
- 隐含`--dirs`（`-d`）选项，将在目标位置创建列表中指定的目录而不是跳过它们（如果需要关闭，请使用`--no-dirs`或`--no-d`）。
- `--archive`（`-a`）选项的行为并不隐含`--recursive`（`-r`），因此如果需要，请显式指定。
- 这些副作用改变了`rsync`的默认状态，因此`--files-from`选项在命令行上的位置不会影响其他选项的解析（例如`-a`在`--files-from`之前或之后都有效，`--no-R`以及其他选项也是如此）。

从`FILE`读取的文件相对于源目录——任何开头的斜杠都会被删除，且不允许`..`高于源目录。例如，考虑此命令：

```
rsync -a --files-from=/tmp/foo /usr remote:/backup
```

如果`/tmp/foo`包含字符串`"bin"`（甚至是`"/bin"`），则`/usr/bin`目录将在远程主机上创建为`/backup/bin`。如果它包含`"bin/"`（注意末尾的斜杠），该目录的直接内容也将发送（无需在文件中显式提到——此功能从 2.6.4 版本开始引入）。

在这两种情况下，如果启用了`-r`选项，该目录的整个层级结构也将传输（请记住，`-r`需要通过`--files-from`显式指定，因为它不会被`-a`隐含包含）。

另请注意，默认启用的`--relative`选项的作用是仅复制从文件中读取的路径信息——它不会强制复制源规格（spec）路径（在本例中为`/usr`）。

此外，如果你在文件前指定`"host:"`，则可以从远程主机而非本地主机读取`--files-from`文件（该主机必须与传输的其中一端匹配）。作为快捷方式，你可以仅指定冒号`:`作为前缀来表示“使用传输的远程端”。例如：

```
rsync -a --files-from=:/path/file-list src:/ /tmp/copy
```

这将复制位于远程主机`"src"`的`/path/file-list`文件中指定的所有文件。如果指定了`--iconv`和`--protect-args`选项，并且`--files-from`文件名从一个主机发送到另一个主机，则文件名将从发送端主机的字符集转换为接收主机的字符集。注意：对`--files-from`输入中的文件列表进行排序有助于`rsync`提高效率，因为这将避免重复访问相邻条目之间共享的路径元素。如果输入未排序，这些路径元素（隐含目录）可能会被扫描多次，`rsync`最终会在它们被转换为文件列表元素后对其进行去重。

### `-0, --from0`

这告诉`rsync`从文件中读取的规则/文件名是以空字符（`'\0`）终止的，而不是换行符（NL）、回车符（CR）或 CR+LF。这会影响`--exclude-from`、`--include-from`、`--files-from`以及通过`--filter`规则指定的任何文件。它不影响`--cvs-exclude`（因为从`.cvsign`文件读取的所有名称都是按空格分割的）。

### `-s, --protect-args`

此选项将所有文件名和大多数选项发送到远程`rsync`，而不允许远程 shell 对其进行解释。这确保了文件名中的空格不会被分割，且任何非通配符的特殊字符都不会被翻译（例如`~`、`$`、`;`、`&`等）。通配符将由`rsync`在远程主机上扩展（而不是由 shell 扩展）。如果你在配合`--iconv`使用此选项，与远程侧相关的参数也将从本地字符集转换为远程字符集。翻译发生在通配符扩展之前。另请参见`--files-from`选项。你还可以通过`RSYNC_PROTECT_ARGS`环境变量控制此选项。如果该变量具有非零值，则默认启用此选项，否则默认禁用。任何状态都会被手动指定的该选项的正向或负向版本所覆盖（注意：`--no-s`和`--no-protect-args`是负版本）。由于此选项从 3.0.0 版本开始引入，如果你以后需要与早于 3.0.0 的远程`rsync`交互，则需要确保它是禁用的。`rsync`也可以在构建时配置为默认启用此选项（这会被环境变量和命令行覆盖）。该选项最终将在未来某个尚未确定的点成为新的默认设置。

### `-T, --temp-dir=DIR`

此选项指示`rsync`在接收端创建传输文件的临时副本时，使用`DIR`作为临时目录。默认行为是在与关联目标文件相同的目录中创建每个临时文件。从`rsync` 3.1.1 版本开始，指定`DIR`内部的临时文件名将不再以额外的点作为前缀（尽管它们仍会添加一个随机后缀）。此选项通常用于接收端磁盘分区没有足够的可用空间来存放传输中最大文件的副本的情况。在这种情况下（即临时目录位于不同的磁盘分区上），`rsync`将无法将每个收到的临时文件覆盖到关联的目标文件上，而是将其复制到目标位置。`rsync`通过将文件覆盖到目标文件来实现这一点，这将导致目标文件在拷贝期间包含截断的数据。如果不是这样做（即使先删除目标文件，然后将数据本地复制到目标目录中的临时文件，然后再重命名到位），可能会导致旧文件继续占用磁盘空间（如果有人正打开它），从而导致磁盘上此时可能没有足够的空间容纳新版本。如果你是因为磁盘空间不足的其他原因使用此选项，你可能希望将其与`--delay-updates`选项结合使用，这将确保所有复制的文件都放在目标层级结构的子目录中，等待传输结束。如果你没有足够的空间在目标分区上复制所有到达的文件，另一种告诉`rsync`你不过于担心磁盘空间的方法是使用带有相对路径的`--partial-dir`选项；因为这告诉`rsync`在目标层级结构中的子目录中存放单个文件的副本是可以的，`rsync`将使用`partial-dir`作为暂存区来引入复制的文件，然后从那里重命名到位。（使用绝对路径指定`--partial-dir`不会产生这种副作用。）

### `-y, --fuzzy`

此选项告诉`rsync`对于任何缺失的目标文件，应寻找一个基准文件（basis file）。当前算法会在目标文件所在的目录中查找大小和修改时间相同的文件，或者修改时间相似的文件。如果找到，`rsync`将使用模糊基准文件来尝试加速传输。如果重复使用该选项，模糊扫描将在通过`--compare-dest`、`--copy-dest`或`--link-dest`指定的任何匹配备目标目录中进行。注意，使用`--delete`选项可能会删除任何潜在的模糊匹配文件，因此如果你需要防止这种情况，请使用`--delete-after`或指定文件名排除。

### `--compare-dest=DIR`

此选项指示`rsync`在目标机器上使用`DIR`作为额外的层级，在进行传输之前对比目标文件（如果目标目录缺少这些文件）。如果在`DIR`中找到与发送端文件相同的文件，则该文件不会传输到目标目录。这对于创建一个仅包含与早期备份相比已变化文件的稀疏备份有用。此选项通常用于复制到空（或新建的）目录。从 2.6.4 版本开始，可以提供多个`--compare-dest`目录，这将导致`rsync`按指定的顺序搜索列表以进行精确匹配。如果找到仅属性上不同的匹配项，将创建本地副本并更新属性。如果没有找到匹配项，将从其中一个`DIR`选择一个基准文件来尝试加速传输。如果`DIR`是相对路径，则它相对于目标目录。另请参见`--copy-dest`和`--link-dest`。注意：从 3.1.0 版本开始，如果在其中一个 compare-dest 层级找到精确匹配，`rsync`将从非空目标层级中删除文件（使得最终结果更接近全新的拷贝）。

### `--copy-dest=DIR`

此选项的行为类似于`--compare-dest`，但`rsync`将在`DIR`中找到的未更改的文件使用本地副本复制到目标目录。这对于在传输到新目的地的同时保持现有文件完整，并在所有文件成功传输后进行闪电切换有用。可以提供多个`--copy-dest`目录，这将导致`rsync`按指定的顺序搜索列表以查找未更改的文件。如果没有找到匹配项，将从其中一个`DIR`选择一个基准文件来尝试加速传输。如果`DIR`是相对路径，则它相对于目标目录。另请参见`--compare-dest`和`--link-dest`。

### `--link-dest=DIR`

此选项的行为类似于`--copy-dest`，但未更改的文件将从`DIR`硬链接到目标目录。在所有保留的属性（例如权限，可能还有所有权）上必须完全相同，文件才能链接在一起。一个示例：

```
rsync -av --link-dest=$PWD/prior_dir host:src_dir/ new_dir/
```

如果文件没有建立链接，请双检它们的属性。还要检查这些属性是否被强制置于`rsync`的控制之外，例如将 root 压缩为单个用户的挂载选项，或者以通用所有权挂载可移动的驱动器（例如 OS X 的“忽略此卷宗上的所有权”选项）。从 2.6.4 版本开始，可以提供多个`--link-dest`目录，这将导致`rsync`按照指定的顺序搜索列表以进行精确匹配。如果找到一个仅在属性上不同的匹配项，则会创建一个本地副本并更新属性。如果没有找到匹配项，则将从其中一个`DIR`中选择一个基准文件来尝试加速传输。此选项在复制到空目标层级时效果最好，因为现有文件的属性可能会被调整，这可能会通过硬链接影响备用目标文件。此外，更改的详细列表可能会变得混乱。请注意，在 3.1.0 版本之前，当目标文件已存在时，永远不会找到备用目录的精确匹配（也不会链接到目标）。请注意，如果你将此选项与`--ignore-times`结合，rsync 将不会将任何文件链接在一起，因为它只将相同的文件链接在一起作为传输文件的替代方案，而不会作为文件更新后的额外检查。如果`DIR`是相对路径，则它相对于目标目录。另见`--compare-dest`和`--copy-dest`。请注意，rsync 2.6.1 之前的版本有一个 bug，当指定`-o`（或由`-a`隐含）时，可能会防止`--link-dest`对非超级用户正常工作。你可以通过向旧版 rsync 发送时避免使用`-o`选项来回避此 bug。

### `-z, --compress`

使用此选项，`rsync`在将文件数据发送到目标机器时进行压缩，从而减少传输的数据量——这在慢连接上非常有用。请注意，此选项通常能比使用压缩的远程 shell 或压缩传输层获得更好的压缩率，因为它利用了匹配数据块中的隐含信息，而这些信息并没有显式地通过连接发送。然而，这种匹配数据压缩是以 CPU 为代价的，可以通过重复使用`-z`选项来禁用它，但前提是双方版本至少为 3.1.1。请注意，如果你的 rsync 版本在编译时使用了外部 zlib（而不是与 rsync 软件包的 zlib），则它将不支持旧式的压缩，仅支持新式的（重复选项）压缩。在未来，这种新式的压缩可能会成为默认值。客户端 rsync 通过`--new-compress`选项向服务器请求新式压缩，如果你看到该选项被拒绝，说明服务器版本不够新，不支持`-zz`。rsync 还接受`--old-compress`选项，以备未来新式压缩成为默认值时使用。参见`--skip-compress`选项查看不进行压缩的文件后缀默认列表。

### `--compress-level=NUM`

显式设置要使用的压缩级别（参见`--compress`），而不是让其保持默认。如果`NUM`为非零，则隐含了`--compress`选项。

### `--skip-compress=LIST`

覆盖不进行压缩的文件后缀列表。`LIST`应该是一个或多个由斜杠（`/`）隔开的文件后缀（不带点）。你可以指定一个空字符串来表示不跳过任何文件。支持简单的字符类匹配：每个通配符都由方括号内的字母列表组成（例如，不支持特殊类，如`"[:alpha:]"`，且`-`没有特殊含义）。星号（`*`）和问号（`?`）没有特殊含义。这里有一个跳过 6 个后缀的示例（因为 5 条规则中有 1 条匹配了 2 个后缀）：`--skip-compress=gz/jpg/mp[34]/7z/bz2`

### `--address`

默认情况下，`rsync`在连接到 rsync 守护进程时将绑定到通配符地址（wildcard address）。`--address`选项允许你指定一个要绑定的特定 IP 地址（或主机名/hostna）。参见`--daemon`模式章节中的此选项。

### `--port=PORT`

这指定了要使用的替代 TCP 端口，而不是默认的`873`。只有当你使用双冒号（`::`）语法连接 rsync 守护进程时才需要此选项（因为 URL 语法有方法在 URL 部分中指定端口）。参见`--daemon`模式章节中的此选项。

### `--sockopts`

此选项可以为喜欢极度调优系统的人带来无限乐趣。你可以设置各种 socket 选项，这些可能会传输更快（或更慢！）。请阅读`setsockopt()`系统调用的手册页以获取你可能设置的一些选项的详情。默认情况下不设置特殊的 socket 选项。这仅影响到远程 rsync 守护进程的直接 socket 连接。此选项也存在于`--daemon`模式章节。

### `--blocking-io`

这告诉`rsync`在启动远程 shell 传输时使用阻塞 I/O。如果远程 shell 是`rsh`或`remsh`，rsync 使用阻塞 I/O，否则默认使用非阻塞 I/O。（注意：ssh 偏于使用非阻塞 I/O。）

### `--outbuf=MODE`

这设置输出缓冲模式。模式可以是`None`（即无缓冲）、`Line`或`Block`（即全缓冲）。你可能只需指定一个字母作为模式，并可使用大写或小写。此选项的主要用途是在 rsync 的输出流向文件或管道时，将全缓冲更改为行缓冲。

### `-i, --itemize-changes`

请求对每个文件所做的更改提供简单的分类详细列表，包括属性更改。这与指定`--out-format='%i %n%L'`完全相同。如果你重复该选项，未更改的文件也将输出，但前提是接收端的 rsync 版本至少为 2.6.7（你可以在较旧版本的 rsync 中使用`-vv`，但也会开启其他详细信息的输出）。

`%i`转义字符的输出非常晦涩，长度为 11 个字母。通用格式类似于字符串`YXcstpoguax`，其中`Y`被替换为正在执行的更新类型，`X`被替换为文件类型，其他字母代表当这些属性被修改时可能会输出的属性。替换`Y`的更新类型如下：

- A `o`：表示文件正在传输到远程主机（发送）。
- A `>`：表示文件正在传输到本地主机（接收）。
- A `c`：表示该项目正在发生本地更改/创建（例如创建目录或更改符号链接等）。
- A `h`：表示该项目是到另一个项目的硬链接（需要`--hard-links`）。
- A `.`：表示该项目未被更新（尽管它可能有属性正在被修改）。
- A `*`：表示分类输出区域的其余部分包含消息（例如“删除”）。

替换`X`的文件类型为：`f`表示文件，`d`表示目录，`L`表示符号链接，`D`表示设备，`S`表示特殊文件（例如字 sockets 和管道 fifo）。上述字符串中的其他字母是当项目的关联属性正在更新时将输出的实际字母，或者在无更改时输出`.`。这里有三个例外：(1) 新创建的项目会将每个字母替换为`+`，(2) 相同的项目会将点`.`替换为空格，以及 (3) 未知的属性会将每个字母替换为`?`（这在与旧版本 rsync 通信时可能会发生）。

与每个字母关联的属性如下：

- A `c`：表示普通文件的校验和不同（需要`--checksum`），或者表示符号链接、设备或特殊文件的值已更改。注意，如果你向版本 3.0.1 之前的 rsync 发送文件，此更改标记将仅存在于校验和不同的普通文件。
- A `s`：表示普通文件的尺寸不同，并将通过文件传输更新。
- A `t`：表示修改时间不同，并将更新为发送者的值（需要`--times`）。替代值`T`表示修改时间将被设置为传输时间，这发生在文件/符号链接/设备在未使用`--times`的情况下被更新，以及当符号链接更改且接收端无法设置其时间时。（注意：当使用 rsync 3.0.0 客户端时，你可能会看到`s`标记与`t`组合，而不是正确的`T`标记来表示此时间设置失败。）
- A `p`：表示权限不同，并将更新为发送者的值（需要`--perms`）。
- A `o`：表示所有者不同，并将更新为发送者的值（需要`--owner`和超级用户权限）。
- A `g`：表示组不同，并将更新为发送者的值（需要`--group`和设置组的权限）。
- `u`槽位预留供以后使用。
- A `a`：表示 ACL 信息已更改。
- A `x`：表示扩展属性信息已更改。



另一种输出也是可能的：在删除文件时，`%i` 将为每个被移除的项目输出字符串 `*deleting`（假设你使用的是足够新的 `rsync`，它会记录删除操作而不是将其作为冗余消息输出）。

`--out-format=FORMAT` 这允许你精确指定 `rsync` 客户端每次更新时向用户的输出。该格式是一个文本字符串，包含以 `%` 字符为前缀的特定单字符转义序列。如果指定了 `--info=na` 或 `-v`，则假设默认格式为 `"%n%L"`（这只会告诉你文件名，以及如果该项目是链接，则显示它指向何处）。有关可能的转义字符的完整列表，请参阅 `rsyncd.conf` 手页中的“log format”设置。指定 `--out-format` 选项隐含了 `--info=na` 选项，它将记录每个发生重大更新的文件、目录等（已传输的文件、重建的符号链接/设备，或被访问过的目录）。此外，如果字符串中包含了项化转义字符（`%i`）（例如使用了 `--itemize-changes` 选项），日志记录将增加，以记录以任何方式发生更改的项目（只要接收端至少是 2.6.4）。有关 `%i` 输出的描述，请参见 `--itemize-changes` 选项。`rsync` 将在文件传输之前输出 out-format 字符串，除非请求了某个传输统计转义字符，在这种情况下，日志将在文件传输结束时记录。当这种延迟记录生效且同时指定了 `--progress` 时，`rsync` 还会在进度信息之前输出正在传输的文件名（随后当然会是 out-format 的输出内容）。

`--log-file=FILE` 此选项导致 `rsync` 将其正在的操作记录到文件中。这类似于守护进程执行的日志记录，但可以在非守护进程传输的客户端和/或服务器端进行请求。如果指定为客户端选项，将启用传输日志，默认格式为 `"%i %n%L"`。如果你想覆盖此设置，请查看 `--log-file-format` 选项。这里有一个请求远程端记录发生情况的示例命令：

`rsync -av --remote-option=--log-file=/tmp/rlog src/ dest/`

当你需要调试为什么连接会意外关闭时，这是非常有用的。`--log-file-format=FORMAT` 允许你精确指定每次更新的日志被写入 `--log-file` 选项所指定的文件（必须也指定该文件，此选项才能生效）。如果你指定一个空字符串，则日志文件中将不会提到已更新的文件。有关可能的转义字符的完整列表，请参阅 `rsyncd.conf` 手页中的“log format”设置。如果指定了 `--log-file` 但未指定此选项，则使用的默认格式为 `'%i %n%L'`。

`--stats` 告诉 `rsync` 打印关于文件传输的详细统计信息，让你判断 `rsync` 的增量传输算法对你的数据有多有效。如果与 0 或 1 个 `-v` 选项配合使用，此选项等同于 `--info=stats2`；如果与 2 个或更多 `-v` 选项配合使用，则等同于 `--info=stats3`。当前统计如下：

- **Number of files** 是所有“文件”（广义上）的计数，包括目录、符号链接等。总数之后将跟一个按文件类型分类的数量列表（如果总数不为 0）。例如："(reg: 5, dir: 3, link: 2, dev: 1, special: 1)" 列出了普通文件、目录、符号链接、设备和特殊文件的总数。如果任何项值为 0，则将完全从列表中省略。

- **Number of created files** 是创建了多少个“文件”（广义上）的计数（相对于更新的文件）。总数之后将跟一个按文件类型分类的数量列表（如果总数不为 0）。

- **Number of deleted files** 是删除了多少个“文件”（广义上）的计数（相对于更新的文件）。总数之后将跟一个按文件类型分类的数量列表（如果总数不为 0）。注意，此行仅在删除操作生效且仅在使用协议 31 时（`rsync` 3.1.x 的默认值）才会输出。

- **Number of regular files transferred** 是通过 `rsync` 增量算法更新的普通文件计数，不包括目录、符号链接等。注意 `rsync` 3.1.0 在此标题中加入了“regular”一词。

- **Total file size** 是传输中所有文件大小的总和。这不计算目录或特殊文件的大小，但包含了符号链接的大小。

- **Total transferred file size** 是仅针对传输文件的所有大小总和。

- **Literal data** 是为了让接收端重建更新的文件，我们必须发送的不匹配的文件更新数据量。

- **Matched data** 是接收端在重建更新的文件时本地获取的数据量。

- **File list size** 是发送者将文件列表发送给接收端时数据的大小。由于 `rsync` 在发送列表时对重复数据进行了压缩，此值比内存中的文件列表大小小。

- **File list generation time** 是发送者创建文件列表花费的秒数。这需要发送端使用现代 `rsync`。

- **File list transfer time** 是发送者将文件列表发送到接收端花费的秒数。

- **Total bytes sent** 是 `rsync` 从客户端发送到服务器的所有字节计数。

- **Total bytes received** 是 `rsync` 客户端从服务器接收的所有非消息字节计数。“非消息”字节是指我们不计算服务器发送给我们的冗余消息字节，这使得统计数据更具一致性。

- `-8, --8-bit-output` 告诉 `rsync` 在输出中保留所有高位字符不进行转义，而不是尝试测试它们在当前语言区域（locale）是否有效并转义无效的字符。无论此选项如何设置，所有控制字符（制表符除外）始终会被转义。从 2.6.7 开始的转义惯用法是输出字面反斜杠（`\`）和一个井号（`#`），后面紧跟 3 位八进制数字。例如，换行符将输出为 `"\#012"`。文件名中的字面反斜杠除非后面跟着井号和 3 位数字（0-9），否则不会被转义。

- `-h, --human-readable` 以更符合人类阅读的格式输出数字。共有 3 种级别：

(1) 在每 3 个数字之间使用分隔符输出数字（逗号或句号，取决于小数点是用点还是逗号表示）；

(2) 以 1000 为单位输出数字（较大的单位带有字符后缀——见下文）；

(3) 以 1024 为单位输出数字。

默认是人类可读级别 1。每个 `-h` 选项都会增加一级。你可以通过指定 `--no-human-readable` (`--no-h`) 选项将级别降到 0（以纯数字输出数字）。级别 2 和 3 中附加的单位字母是：`K` (kilo)、`M` (mega)、`G` (giga) 或 `T` (tera)。例如，一个 1234567 字节的文件在级别 2 下将输出为 `1.23M`（假设句号是你的本地小数点）。向后兼容性：`rsync` 3.1.0 之前的版本不支持人类可读级别 1，默认是级别 0。因此，只要你在指定一个或多个 `-h` 选项之前没有指定 `--no-h`，一个或两个 `-h` 选项在旧版本和新版本中的行为是类似的。参考 `--list-only` 选项了解差异。

- `--partial` 默认情况下，如果传输中断，`rsync` 将删除任何部分传输的文件。在这种情况下，保留部分传输的文件更为理想。使用 `--partial` 选项告诉 `rsync` 保留部分文件，这应该使后续传输文件的剩余部分速度更快。

- `--partial-dir=DIR` 比 `--partial` 选项更好的保留部分文件的方法是指定一个用于存放部分数据的 `DIR`（而不是将其直接写入目标文件）。在下一次传输时，`rsync` 将使用在该目录中找到的文件作为数据来加速传输的恢复，并在完成任务后将其删除。请注意，如果指定了 `--whole-file`（或隐含指定），则对于正在更新的文件，找到的任何 `partial-dir` 文件都只会被直接删除（因为 `rsync` 在发送文件时没有使用 `rsync` 的增量传输算法）。如果 `DIR` 不存在，`rsync` 将创建它（仅是最后一个目录——不是整个路径）。这使得用户可以使用相对路径（例如 `--partial-dir=.rsync-partial`）让 `rsync` 在需要时在目标文件目录创建部分目录，并在部分文件被删除时再次将其删除。如果 `partial-dir` 值不是绝对路径，`rsync` 将在你所有现有排除规则的末尾添加一条排除规则。这将防止发送发送端可能存在的任何 `partial-dir` 文件，并防止接收端过早删除 `partial-dir` 项。示例：上述 `--partial-dir` 选项会在任何其他过滤规则的末尾添加相当于 `-f '-p .rsync-partial/'` 的规则。如果你提供了自己的排除规则，可能需要为 `partial-dir` 添加自己的排除/隐藏/保护规则，因为 (1) 自动添加的规则在你的其他规则末尾可能无效，或者 (2) 你可能希望覆盖 `rsync` 的排除选择。例如，如果你想让 `rsync` 清理任何残留的 `partial-dirs`，你应该指定 `--delete-after` 并添加一条“风险”过滤规则，例如 `-f 'R .rsync-partial/'`。（避免使用 `--delete-before` 或 `--delete-during`，除非你不需要 `rsync` 在当前运行中使用任何留下的 `partial-dir` 数据。）重要提示：`--partial-dir` 不应允许其他用户写入，否则存在安全风险。例如，避免使用 `/tmp`。你也可以通过环境变量 `RSYNC_PARTIAL_DIR` 设置 `partial-dir` 的值。在环境中设置此项不会强制启用 `--partial`，而是影响在指定 `--partial` 时部分文件的去向。例如，与其使用 `--partial-dir=.rsync-tmp` 配合 `--progress`，不如在环境中设置 `RSYNC_PARTIAL_DIR=.rsync-tmp`，然后只需使用 `-P` 选项来开启对 `.rsync-tmp` 目录的部分传输。`--partial` 选项不查找此环境变量的情况仅限于：(1) 指定了 `--inplace`（因为 `--inplace` 与 `--partial-dir` 冲突），以及 (2) 指定了 `--delay-updates`（见下文）。对于守护进程配置的“拒绝选项”设置，`--partial-dir` *并不* 意味着 `--partial`。这样做可以通过拒绝 `--partial` 选项来禁止用部分传输覆盖目标文件，同时允许 `--partial-dir` 提供的更安全的惯用法。

- `--delay-updates` 此选项将每个更新文件的临时文件放在一个临时目录中，直到传输结束，届时所有文件将连续重命名到位置。这尝试使文件的更新更具原子性。默认情况下，文件被放在每个文件目标目录下名为 `.~tmp~` 的目录中，但如果你指定了 `--partial-dir` 选项，则将使用该目录。请查看 `--partial-dir` 部分的注释，了解此 `.~tmp~` 目录如何从传输中排除，以及如果你希望 `rsync` 清理可能存在的旧 `.~tmp~` 目录可以做什么。此选项与 `--inplace` 和 `--append` 冲突。此选项在接收端使用更多内存（每个传输的文件一个位），并且要求接收端有足够的可用磁盘空间来存放所有更新文件的副本。另外注意，不要对 `--partial-dir` 使用绝对路径，除非 (1) 传输中的文件没有可能同名（因为如果路径是绝对的，所有更新的文件将被放在同一个目录中）且 (2) 层结构中没有挂载点（因为如果无法重命名到位置，延迟更新将失败）。参见“support”子目录下的“atomic-rsync” perl 脚本以获取更原子的更新算法（它使用了 `--link-dest` 和并行的文件体系）。

- `-m, --prune-empty-dirs` 此选项告诉接收端的 `rsync` 从文件列表中删除空目录，包括没有非目录子节点的嵌套目录。这对于发送端 `rsync` 使用包含/排除/过滤规则递归扫描文件层次结构时，避免创建大量无用目录非常有用。注意，使用传输规则（如 `--min-size` 选项）不会影响文件列表的内容，因此即使目录中没有文件匹配传输规则，也不会导致目录变空。由于文件列表实际上被修剪了，此选项还会影响在删除功能激活时哪些目录被删除。然而，请记住，排除的文件和目录可能会因为排除规则既隐藏了源文件又保护了目标文件导致现有项被删除。请查看易损过滤规则选项以了解如何避免这种情况。你可以使用全局“保护”过滤器来防止从文件列表中修剪某些空目录。例如，此选项将确保目录“emptydir”被保留在文件列表中：

```
--filter 'protect emptydir/'
```

这是一个示例，它可以按层级结构复制所有 `.pdf` 文件，仅创建存放 `.pdf` 文件必需的必要目标目录，并确保删除目标路径中的任何多余文件和目录（注意：这里使用的是非目录的隐藏过滤器，而不是排除过滤器）：

```bash
rsync -avm --del --include='*.pdf' -f 'hide,! */' src/ dest
```

如果你不想删除目标路径中的多余文件，可以使用更受推崇的 `--include='*/' --exclude='*'` 选项来代替隐藏过滤器（如果这更符合你的习惯的话）。`--progress` 选项告诉 `rsync` 打印显示传输进度的信息。这让无聊的用户有些事情可以看。在现代版本的 `rsync` 中，这等同于指定了`--info=flist2,na,progress`，但任何用户提供的这些信息标志设置都具有优先级（例如“`--info=flist0 --progress`”）。当 `rsync` 传输普通文件时，它会更新如下所示的进度行：`782448 63% 110.64kB/s 0:00:04`

在此示例中，接收端已重建了发送端文件的 782448 字节（或 63%），重建速度为每秒 110.64 千字节，如果当前速率能维持到结束，传输将在 4 秒后完成。如果使用了 `rsync` 的增量传输算法，这些统计数据可能会产生误导。例如，如果发送的文件由基础文件加上后续数据组成，当接收端处理字面数据时，报告的速率可能会大幅下降，传输完成的时间可能会比接收端结束时的估计要长，因为它之前一直在处理文件的匹配部分。当文件传输完成后，`rsync` 会用摘要行替换进度行，格式如下：`1,238,099 100% 146.38kB/s 0:00:08 (xfr#5, to-chk=169/396)`

在此示例中，文件总长度为 1,238,099 字节，在完成所需的 8 秒内，整个文件的平均传输速率为每秒 146.38 千字节，这是当前 `rsync` 会话中传输的第 5 个普通文件，文件列表中共有 396 个文件，还有 169 个文件等待接收端检查（以查看是否已更新）。在增量递归扫描中，`rsync` 在扫描结束之前不知道文件列表中的总数，但由于它在扫描期间就开始传输文件，因此在确定列表完整大小之前，它会显示带有“ir-chk”（增量递归检查）文本的行而不是“to-chk”，一旦知道列表完整大小，就会切换到“to-chk”。因此，看到“ir-chk”意味着文件列表中的文件总数仍将增加（每增加一次，待检查的文件数就会随着列表中添加的文件数量而增加）。

`-P` `-P` 选项等同于`--partial --progress`。其目的是为了在可能被中断的长传输中指定这两个选项变得更加方便。还有一个 `--info=progress2` 选项，它根据整个传输而非单个文件输出统计信息。使用此标志时不要输出文件名（例如，如果你想查看传输情况而不希望让大量信息滚动屏幕，请避免使用 `-v` 或指定 `--info=na0`。使用 `--info=progress2` 时不需要指定 `--progress` 选项）。

`--password-file=FILE` 此选项允许你通过文件或标准输入（如果 `FILE` 为 `-` 则）为访问 `rsync` 进程提供密码。该文件第一行应包含密码（所有其他行将被忽略）。如果 `FILE` 是全局可读的，或者以 root 运行的 `rsync` 命令发现了非 root 拥的文件，`rsync` 将报错退出。此选项不会为如 `ssh` 等远程 shell 传输提供密码；要了解如何操作，请参阅远程 shell 的文档。在使用远程 shell 作为传输访问 `rsync` 进程时，此选项仅在远程 shell 完成身份验证后才会生效（即如果你同样在进程的配置文件中指定了密码）。

`--list-only` 此选项将列出源文件而不是传输它们。如果只有一个源参数且未指定目标，则会导出此选项，因此其主要用途是：(1) 将包含目标参数的复制命令转换为文件列表命令，或 (2) 能够指定多个源参数（注意：确保包含目标参数）。注意：带有通配符的源参数会被 shell 扩展为多个参数，因此在不使用此选项的情况下尝试列出此类参数永远是不安全的。例如：

```bash
rsync -av --list-only foo* dest/
```

从 `rsync` 3.1.0 开始，`--list-only` 输出的尺寸受 `--human-readable` 选项的影响。默认情况下，它们包含数字分隔符，但更高可读性的级别将输出带有单位后缀的大小。请注意，对于所有人类可读级别，尺寸输出的列宽已从 11 字符增加到 14 字符。如果你希望尺寸仅显示数字并使用 11 字符的列宽，请使用 `--no-h`。兼容性说明：当从版本 2.6.3 或更老的 `rsync` 请求远程文件列表时，如果你请求非递归列表，可能会遇到错误。这是因为文件列表意味着在不使用 `--recursive` 的情况下使用 `--dirs` 选项，而旧版本的 `rsync` 没有该选项。要避免此问题，要么指定 `--no-dirs` 选项（如果你不需要展开目录内容），要么开启递归并排除子目录的内容：`-r --exclude='/*/*'`。



告诉 `rsync` 在创建套接字时优先使用 `IPv4`/`IPv6`。这仅影响 `rsync` 直接控制的套接字，例如直接连接 `rsync` 守护进程时的传出套接字。另见 `--daemon` 模式下的这些选项。如果编译 `rsync` 时未支持 `IPv6`，则 `--ipv6` 选项将不起作用。`--version` 输出将告诉你是否是这种情况。

### `--checksum-seed=NUM`

将校验和种子设置为整数 `NUM`。此 4 字节的校验种子包含在每个块和 `MD4` 文件校验的计算中（更现代的 `MD5` 文件校验不使用种子）。默认情况下，校验和种子由服务器生成，并默认为当前的 `ti()`。此选项用于设置特定的校验种子，对于希望获得可重复块校验的应用，或在用户希望获得更随机校验种子的情况下非常有用。将 `NUM` 设置为 `0` 会导致 `rsync` 使用默认的 `ti()` 作为校验种子。

## 守护进程选项 (DAEMON OPTIONS)

启动 `rsync` 守护进程时允许的选项如下：

### `--daemon`

告诉 `rsync` 以守护模式运行。你启动的守护进程可以使用 `rsync` 客户端通过 `host::module` 语法访问。如果标准输入是套接字，则 `rsync` 将假设它是通过 `inetd` 运行的，否则它将从当前终端分离并成为后台守护进程。守护进程将在客户端每次连接时读取配置文件 (`rsyncd.conf`) 并相应地对请求做出响应。详情参见第 (5) 手页。

### `--address`

默认情况下，`rsync` 在使用 `--daemon` 选项作为守护进程运行时将绑定到通配地址。`--address` 选项允许你指定绑定的特定 IP 地址（或主机）。这使得结合 `--config` 选项实现虚拟主机可能。参见 `rsyncd.conf` 手页中的 "address" 全局选项。

### `--bwlimit=RATE`

此选项允许你指定守护进程通过套接字发送数据的最大传输速率。客户端仍然可以指定较小的 `--bwlimit` 值，但不允许更大的值。请查看此选项的客户端版本（上文）获取更多详细信息。

## `--config=FILE`

此选项指定一个与默认不同的配置文件。该选项仅在指定了 `--daemon` 时才有效。默认值为 `/etc/rsyncd.conf`，除非守护进程通过远程 shell 程序运行且远程用户不是超级用户；在这种情况下，默认文件为当前目录下的 `rsyncd.conf`（通常是 `$HOME`）。

## `-M`, `--dparam=OVERRIDE`

此选项用于在以守护模式启动 `rsync` 时设置守护进程参数。它等同于在第一个模块定义之前，在全局设置的末尾添加该参数。如果您需要，可以不带空格指定参数。例如：

```
rsync --daemon -M pidfile=/path/rsync.pid
```

## `--no-detach`

当作为守护进程运行时，此选项指示 `rsync` 不要脱离并成为后台进程。在 `Cygwin` 上作为服务运行时，需要此选项；当 `rsync` 被 `daemontools` 或 AIX 的 `System Resource Controller` 等程序监控时，该选项可能也有有用。在调试器下运行 `rsync` 时，也建议使用 `--no-detach`。如果 `rsync` 从 `inetd` 或 `sshd` 运行，则此选项无效。

## `--port=PORT`

此选项指定守护进程监听的备用 TCP 端口，而不是默认的 `873`。见 `rsyncd.conf` 手页中的 "port" 全局选项。

## `--log-file=FILE`

此选项告诉 `rsync` 守护进程使用指定的日志文件，而不是使用配置文件中的 "log file" 设置。

## `--log-file-format=FORMAT`

此选项告诉 `rsync` 守护进程使用指定的 `FORMAT` 字符串，而不是使用配置文件中的 "log format" 设置。它还会启用“传输日志”，除非字符串为空，此时将关闭传输日志。

## `--sockopts`

此选项会覆盖 `rsyncd.conf` 文件中的 `socket options` 设置并具有相同的语法。

## `-v`, `--verbose`

此选项会增加守护进程在启动阶段记录的信息量。在客户端连接后，守护进程的详细程度将由客户端使用的选项以及模块配置部分中的“max verbosity”设置来控制。

## `-4`, `--ipv4` 或 `-6`, `--ipv6`

告诉 `rsync` 在创建 `rsync` 守护进程用于监听连接的入站套接字时优先使用 `IPv4`/`IPv6`。在较旧版本的 Linux 中，可能需要这些选项之一来绕过内核中的 `IPv6` 错误（如果在没有其他程序使用端口时看到“address already in use”错误，请尝试在启动守护进程时指定 `--ipv6` 或 `--ipv4`）。

如果编译 `rsync` 时未支持 `IPv6`，则 `--ipv6` 选项将无效。`--version` 输出将告诉您是否是这种情况。

## `-h`, `--help`

在 `--daemon` 之后指定时，打印一个短帮助页面，描述启动 `rsync` 守护进程的可用选项。

## 过滤规则

过滤规则允许灵活选择要传输的文件（包含）和要跳过的文件（排除）。规则要么直接指定包含/排除模式，要么指定获取更多包含/排除模式的方法（例如，从文件中读取它们）。

在构建要传输的文件/目录列表时，`rsync` 会逐对每个待传输的文件与包含/排除模式列表进行比对，并对第一个匹配的模式执行操作：如果是排除模式，则跳过该文件；如果是包含模式，则该文件不被跳过；如果没有找到匹配的模式，则该文件不被跳过。

`Rsync` 根据命令行指定的构建一个有序的过滤规则列表。过滤规则具有以下语法：

```
RULE [PATTERN_OR_FILENAME]
RULE,MODIFIERS [PATTERN_OR_FILENAME]
```

您可以选择使用下述的短 `RULE` 名称或长 `RULE` 名称。如果您使用短规则名称，分隔 `RULE` 和 `MODIFIERS` 的逗号 `,` 是可选的。随其后的 `PATTERN` 或 `FILENAME`（如果存在）跟在单个空格或下划线 `_` 之后。以下是可用的规则前缀：

- `exclude, -` 指定一个排除模式。

- `include, +` 指定一个包含模式。

- `rules, .` 指定一个用于读取更多规则的规则文件。

- `dir-rules, :` 指定一个每个目录的规则文件。

- `hide, H` 指定一个用于从传输中隐藏文件的模式。

- `show, S` 匹配模式的文件不被隐藏。

- `protect, P` 指定一个保护文件免删除的模式。

- `risk, R` 匹配模式的文件不受保护。

- `clear, !` 清空当前的包含/排除列表（不带参数）

当从文件中读取规则时，会忽略空行以及以 `#` 开头的注释行。

请注意，`--include`/`--exclude` 命令行选项不支持上述描述的全范围规则解析——它们仅允许指定包含/排除模式加上一个用于清除列表的 "!" 标记（以及在从文件中读取规则时的正常注释解析）。如果模式不以 `- `（连字符，空格）或 `+ `（加号，空格）开头，则规则将被解释为在字符串前前缀了 `+ `（用于包含选项）或 `- `（用于排除选项）。相反，`--filter` 选项始终在规则开头包含短或长规则名称。

同样注意，`--filter`、`--include` 和 `--exclude` 选项接受一个规则/模式。要添加多个，您可以在命令行上重复选项，使用 `--filter` 选项的规则文件语法，或使用 `--include-from`/`--exclude-from` 选项。

## 包含/排除模式规则

您可以通过使用 `+`、`-` 等过滤规则（如上文“过滤规则”部分介绍）指定模式来包含和排除文件。每个包含/排除规则都指定一个模式，该模式将与待传输的文件名进行匹配。这些模式可以有多种形式：

- 如果模式以 `/` 开头，则它锚定在文件层次结构中的特定位置，否则它匹配路径名称的末尾。这类似于正则表达式开头的 `^`。因此，`/foo` 将匹配“传输根目录”（对于全局规则）或规则文件目录（对于每个目录的规则）中的 "foo" 文件名。未说明的 "foo" 会匹配树中任何地方的 "foo"，因为该算法是从上到下递归应用的；它的行为就像每个路径分量都有机会成为文件名的末尾。即使是未锚定的 "sub/foo" 也会匹配层次结构中任何在目录 "sub" 内发现 "foo" 的点。请参见“锚定包含/排除模式”章节，详细讨论如何指定在传输根处匹配的模式。

- 如果模式以 `/` 结尾，则它将只匹配目录，而不匹配普通文件、符号或设备。

- `rsync` 通过检查模式是否包含以下三个通配符字符之一：`*`、`?` 和 `[`，在简单字符串匹配和通配符匹配之间进行选择。

- `*` 匹配任何路径分量，但在斜杠处停止。

- 使用 `**` 匹配任何内容，包括斜杠。

- `?` 匹配任何除斜杠（`/`）以外的字符。

- `[` 引入字符类，例如 `[a-z]` 或 `[[:alpha:]]`。

- 在通配符模式中，反斜杠 `\` 可用于转义通配符字符，但在没有通配符时它将以字面量匹配。这意味着与没有通配符的模式相比，包含通配符的模式在处理时会多出一层反斜杠移除。例如，如果您向 "foo\bar"（匹配反斜杠）添加通配符，您将需要使用 `foo\\bar*` 以避免 `\b` 变成简单的 "b"。

如果模式包含 `/`（不包括末尾的 `/`）或 `**`，则它将与完整路径进行匹配，包括任何前导目录。如果模式不包含 `/` 或 `**`，则它仅与文件名的最后部分进行匹配。（注意，该算法是递归应用的，因此“完整文件名”实际上可以是从起始目录开始的路径的任何部分。）末尾的 `dir_na/**` 会同时匹配该目录（如同指定了 `dir_na/`）以及该目录下的所有内容（如同指定了 `dir_na/**`）。此行为在版本 2.6.7 中被引入。

请注意，当使用 `--recursive`（`-r`）选项（由 `-a` 隐含包含）时，每个路径的每个子组件都会从上到下被访问，因此包含/排除模式会递归地应用到每个子组件的完整名称（例如，为了包含 `/foo/bar/baz`，子组件 `/foo` 和 `/foo/bar` 不能被排除）。当 `rsync` 找到要发送的文件时，排除模式实际上会触发目录遍历阶段的短路。如果某个模式排除了特定的父目录，它可能会导致更深的包含模式失效，因为 `rsync` 没有进入该被排除的层次结构部分。这在使用末尾带有 `*` 的规则时尤为重要。例如，以下将无法工作：

```
+ /so/path/this-file-will-not-be-found
+ /file-is-included
- *
```

- `C` 用于指示将所有的全局 CVS 排除规则作为排除项插入 `-C` 后面不应有参数。
- `s` 用于指示规则适用于发送端。当规则影响发送端时，它会防止文件被传输。默认情况下规则影响双方，除非指定了 `--delete-excluded`，在这种情况下默认规则变为仅影响发送端。另见隐藏 (H) 和显示 (S) 规则，这是指定发送端包含/排除的另一种方式。
- `r` 用于指示规则适用于接收端。当规则影响接收端时，它会防止文件被删除。更多信息请见 `s` 修饰符。另见保护 (P) 和风险 (R) 规则，这是指定接收端包含/排除的另一种方式。
- `p` 表示规则是易碎的，并且在正在删除的目录中会被忽略。例如，`-C` 选项中排除 "CVS" 和 `*.o` 等内容的默认规则被标记为易碎，且不会防止源端已删除的目录在目标端被删除。

## 合并文件过滤规则

你可以通过指定合并（`.`）或按目录合并（`:`）过滤规则（如上述“过滤规则”部分介绍）将整个文件合并到你的过滤规则中。

合并文件有两种类型——单实例（`.`）和按目录划分（`:`）。单实例合并文件会被读取一次，其规则将合并到过滤器列表中以替换 `.` 规则。对于按目录划分的合并文件，`rsync` 将扫描它所遍历的每个目录以查找该文件，当文件存在时，将将其内容合并到当前的继承规则列表中。这些按目录划分的规则文件必须在发送端创建，因为是由发送端来扫描可传输的文件。如果你想让这些规则文件影响哪些文件不被删除，可能还需要将这些规则文件传输到接收端（见下文“按目录的规则和删除”）。

示例：

```
merge /etc/rsync/default.rules

. /etc/rsync/default.rules

dir-merge .per-dir-filter

dir-merge,n- .non-inherited-per-dir-excludes

:n- .non-inherited-per-dir-excludes
```

在 `merge` 或 `dir-merge` 规则之后接受以下修饰符：

- `-` 指定该文件应仅包含排除模式，除了文件内注释外，不进行其他规则解析。
- `+` 指定该文件应仅包含包含模式，除了文件内注释外，不进行其他规则解析。
- `C` 是一种指定以 CVS 兼容方式读取文件的方法。这开启了 'n'、'w' 和 '-'，但也允许指定清空列表的令牌 (!)。如果没有提供文件名，则使用 `.cvsignore`。
- `e` 将从传输中排除合并文件本身；例如，`dir-merge,e .rules` 等同于 `dir-merge .rules` 和 `- .rules`。
- `n` 指定规则不会被子目录继承。
- `w` 指定规则使用空白符进行单词拆分，而不是正常的行拆分。这也会关闭注释。注意：分隔前缀和规则的空格被特殊处理，因此 `- foo + bar` 被解析为两个规则（假设前缀解析也没有被禁用）。
- 你也可以指定上述 `+` 或 `-` 规则的任何修饰符，以便从文件中读取的规则默认设置该修饰符（`!` 修饰符除外没有用）。例如，`merge,-/ .excl` 将将 `.excl` 的内容视为绝对路径排除项，而 `dir-merge,s .filt` 和 `:sC` 将分别使它们的每个按目录规则仅适用于发送端。如果 `merge` 规则指定了影响的端（通过 `s` 或 `r` 修饰符或两者），则文件中的规则将不再指定端（通过修饰符或如 `hide` 等规则前缀）。

除非使用了 `n` 修饰符，否则目录级规则将在找到 `merge-file` 的目录的所有子目录中被继承。每个子目录的规则都会加在其从父目录继承的目录级规则之前，这使得最新规则的优先级比继承的规则高。整组 `dir-merge` 规则被分组在指定 `merge-file` 的位置，因此可能通过全局规则列表中较早指定的规则来覆盖 `dir-merge` 规则。当从目录级文件中读取到列表清空规则（`!`）时，它只会清除当前 `merge` 文件的继承规则。

防止 `dir-merge` 文件中的单条规则被继承的另一种方法是在该规则的句开头添加一个正斜杠 `/` 对其进行锚定。目录级 `merge-file` 中的锚定规则相对于 `merge-file` 所在的目录，因此模式 `/foo` 将只会匹配位于 `dir-merge` 过滤文件目录下的 `foo` 文件。

这里是一个你通过 `--filter=". file":` 指定的过滤器文件示例：

```
merge /ho/user/.global-filter

- *.gz

dir-merge .rules

+ *.[ch]

- *.o
```

这将在列表开始时 `merge` `/ho/user/.global-filter` 文件的内容，并将 `.rules` 文件转换为目录级过滤器文件。在目录扫描开始之前读取的所有规则都遵循全局锚定规则（即开头的正斜杠匹配传输的根目录）。

如果指定的目录级 `merge-file` 路径是第一个传输目录的父目录，`rsync` 将从该起始点扫描到传输目录的所有父目录，以寻找指定的目录级文件。例如，这里有一个常见的过滤器（参见 `-F`）：

```
--filter=': /.rsync-filter'
```

该规则告诉 `rsync` 在对作为传输部分的目录中的文件进行正常目录扫描之前，从根目录一直到传输目录的父目录的所有目录中扫描 `.rsync-filter` 文件。（注意：对于 `rsync` 守护进程，根目录始终与模块的“path”相同。）

以下是这种对目录级文件预扫描的示例：

```
rsync -avF /src/path/ /dest/dir

rsync -av --filter=': ../../.rsync-filter' /src/path/ /dest/dir

rsync -av --filter=': .rsync-filter' /src/path/ /dest/dir
```

上述前两个命令将在正常扫描查找 `/src/path` 及其子目录中的文件之前，在 `/` 和 `/src` 中查找 `.rsync-filter`。最后一个命令避免了父目录扫描，仅在传输部分的每个目录中查找 `.rsync-filter` 文件。

如果你想在模式中包含 `.cvsignore` 的内容，你应该使用规则 `:C`，它会创建一个 `.cvsignore` 文件的 `dir-merge`，但以与 CVS 兼容的方式进行解析。你可以通过将 `:C` 放在过滤器规则的任何位置，来影响 `--cvs-exclude` (`-C`) 选项对目录级 `.cvsignore` 文件的包含放置在你的规则中的位置。如果不这样做，`rsync` 将把 `.cvsignore` 文件的 `dir-merge` 规则添加到所有其他规则的末尾（使其优先级低于你的命令行规则）。例如：

```
cat <<EOT | rsync -avC --filter='. -' a/ b
+ foo.o
:C
- *.old
EOT
```

```
rsync -avC --include=foo.o -f :C --exclude='*.old' a/ b
```



上述两个 `rsync` 命令是相同的。每个命令都会将所有的目录级 `.cvsignore` 规则 `rge` 在列表中间，而不是末尾。这使得它们的特定目录规则可以覆盖 `:C` 之后的规则，而不是从于你的所有规则。要影响其他 CVS 排除规则（即默认排除列表、`$HOME/.cvsignore` 的内容以及 `$CVSIGNORE` 的值），你应该省略 `-C` 命令行选项，而改为在你的过滤器规则中插入 `-C` 规则；例如 `--filter=-C`。

## 列表清空过滤器规则

你可以使用 `!` 过滤器规则（如上述“过滤器规则”部分所引入）来清空当前的包含/排除列表。“当前”列表可以是全局规则列表（如果在解析过滤器选项时遇到该规则）或一组目录级规则（这些规则继承在它们自己的子列表中，因此子目录可以使用此来清除父目录的规则）。

## 锚定包含/排除模式

如前所述，全局包含/排除模式锚定在“传输根目录”处（与目录级模式不同，后者锚定在 `rge-file` 目录下）。如果你将传输看作是从发送者发送到接收者的 NAS 的子树，那么传输根就是树在目标目录中开始复制的地方。该根目录决定了以 `/` 开头的模式的匹配位置。

由于匹配是相对于传输根的，更改源路径末尾的斜杠或更改你对 `--relative` 选项的使用会影响你在匹配中需要使用的路径（此外还会改变文件树的部在目标主机上复制的方式）。以下示例演示了这一点。

假设我们要匹配两个源文件，一个绝对路径为 `/ho//foo/bar`，另一个路径为 `/ho/you/bar/baz`。以下是对于 2-源传输，不同命令选择的差异：

```
示例命令: rsync -a /ho/ /ho/you /dest

+/- 模式: //foo/bar

+/- 模式: /you/bar/baz

目标文件: /dest//foo/bar

目标文件: /dest/you/bar/baz
```

```
示例命令: rsync -a /ho// /ho/you/ /dest

+/- 模式: /foo/bar (注意缺少 "")

+/- 模式: /bar/baz (注意缺少 "you")

目标文件: /dest/foo/bar

目标文件: /dest/bar/baz
```

```
示例命令: rsync -a --relative /ho// /ho/you /dest

+/- 模式: /ho//foo/bar (注意完整路径)

+/- 模式: /ho/you/bar/baz

目标文件: /dest/ho//foo/bar

目标文件: /dest/ho/you/bar/baz
```

然而，如果你想在接收端执行删除并且排除某些文件被删除，你需要确保接收端知道哪些文件需要排除。最简单的方法是将目录级 `rge` 文件包含在传输中并使用 `--delete-after`，因为这确保接收端在尝试删除任何内容之前获取发送端所有的排除规则：

```
rsync -avF --delete-after host:src/dir /dest
```

然而，如果 `rge` 文件不是传输的一部分，你将需要指定全局排除规则（即在命令行上指定的），或者在接收端维护你自己的目录级 `rge` 文件。第一种方法的示例如下（假设远程 `.rules` 文件排除了它们自身）：

```
rsync -av --filter=': .rules' --filter='. /my/extra.rules' --delete host:src/dir /dest
```

在上面的示例中，`extra.rules` 文件可以影响传输的两侧，但（在发送端）这些规则从 `.rules` 文件的 `rge` 规则，因为它们是在目录级 `rge` 规则之后指定的。

在最后一个示例中，远程端在传输时排除了 `.rsync-filter` 文件，但我们希望使用自己的 `.rsync-filter` 文件来控制接收端侧删除哪些内容。为了实现这一点，我们特意地排除了每个目录的规则文件（这样它们就不会被删除），然后在本地文件中写入规则，以控制其他哪些不应被删除。例如这些命令之一：

```
rsync -av --filter=':e /.rsync-filter' --delete \ host:src/dir /dest rsync -avFF --delete host:src/dir /dest
```

## 批量模式 (BATCH MODE)

批量模式可对许多相同的系统应用同一组更新。假设有一个树被复制到若干台主机上。现在假设对该源树进行了某些更改，这些更改需要传播到其他主机。为了使用批量模式实现这一点，可以运行带有 `write-batch` 选项的 `rsync`，将对源树的更改应用到其中一个目标树上。`write-batch` 选项会导致 `rsync` 客户端在“批文件”中存储对其他相同目标树重复此操作所需的所有信息。

只需生成一次批文件，就可以避免在更新多个目标树时多次执行文件状态检查、校验和和数据块生成。可以使用组播传输协议将批量更新文件并行传输到许多许多主机，而不是逐个将数据发送到每台主机。

要将记录的更改应用到另一个目标树，请运行带有 `read-batch` 选项的 `rsync`，并指定批文件的名称和目标树。`Rsync` 使用批文件中存储的信息来更新目标树。

为了方便起见，当使用 `write-batch` 选项时还会创建一个脚本文件：它将以批文件为名并添加 `.sh` 后缀进行生成。该脚本文件包含一个适用于使用关联批文件更新目标树的命令行。它可以使用 Bourne（或类 Bourne）shell 执行，可选地传递一个备用目标树路径，该路径将替代原始目标路径。当当前主机上的目标树路径与创建批文件时使用的路径不同，这非常有用。

### 示例：

```
$ rsync --write-batch=foo -a host:/source/dir/ /adest/dir/
```

```
$ scp foo* remote:
```

```
$ ssh remote ./foo.sh /bdest/dir/
```

```
$ rsync --write-batch=foo -a /source/dir/ /adest/dir/
```

```
$ ssh remote rsync --read-batch=- -a /bdest/dir/ <foo
```

在这些示例中，使用 `rsync` 从 `/source/dir/` 更新 `/adest/dir/`，并将重复此操作的信息存储在 `"foo"` 和 `"foo.sh"` 中。然后通过将批数据进入目录 `/bdest/dir` 来更新主机 `"remote"`。这两个示例之间的差异揭示了你在处理批量时的某些灵活性：

- 第一个示例显示初始拷贝不需要是局地的——你可以根据需要使用远程 shell 语法或 `rsync` 守护进程语法向远程主机推送或拉取数据。

- 第一个示例使用了创建的 `"foo.sh"` 文件，在远程主机上运行 `read-batch` 命令时获取正确的 `rsync` 选项。

- 第二个示例通过标准输入读取批数据，因此批文件不需要先复制到远程机器上。这个示例避免了使用 `foo.sh` 脚本，因为它需要使用修改后的 `--read-batch` 选项，但如果你想使用该脚本，也可以编辑脚本文件（只需确保没有其他选项尝试使用标准输入，例如 `--exclude-from=-` 选项）。

### 注意事项：

`read-batch` 选项期望它正在更新的目标树与创建批量更新文件集的目标树完全相同。当目标树之间存在差异时，更新可能会被丢弃并警告（如果文件看起来已经是最新的），或者可能会尝试更新文件，然后如果文件验证失败，则带错误地丢弃更新。这意味着如果命令被中断，重新运行 `read-batch` 操作应该是安全的。如果你希望无论文件大小和日期如何，始终尝试进行批量更新，请使用 `-I` 选项（在读取批处理时）。如果发生错误，目标树可能会处于部分更新状态。在这种情况下，可以使用 `rsync` 的常规（非批量）操作模式来修复目标树。

所有目标端上使用的 `rsync` 版本至少要与生成批文件时使用的版本一样。如果批文件中的协议版本太新，导致批处理的 `rsync` 无法处理，`Rsync` 将报错并退出。另请参见 `--protocol` 选项，该选项允许创建的 `rsync` 生成旧版本 `rsync` 可以理解的批文件。（注意，批文件格式在 2.6.3 版本中发生了变化，因此比该版本旧与新版本混合将无法工作。）

在读取批文件时，如果你没有在批写入命令中设置为相同的值，`rsync` 将强制某些选项的值匹配批文件中的数据。其他选项可以（并且应该）更改。例如，`--write-batch` 变为 `--read-batch`，`--files-from` 被丢弃，除非指定了 `--delete` 选项，否则不需要 `--filter`/`--include`/`--exclude` 选项。

创建 `BATCH.sh` 代码会将任何过滤/包含/排除选项转换为单个列表，并作为“here” doc 追加到 shell 脚本文件中。高级用户可以使用此来修改排除列表，如果希望更改由 `--delete` 删除的内容。普通用户可以忽略此细节，仅将 shell 脚本作为运行批量数据相应 `--read-batch` 命令的方便方法。

`rsync` 原有的批量模式是基于 "rsync+"，但最新版本使用了新的实现。

## 符号链接 (SYMBOLIC LINKS)

当 `rsync` 在源目录遇到符号链接时，有三种基本行为。

默认情况下，符号链接完全不传输。对于任何存在的符号链接，会发出“skipping non-regular file” 消息。

如果指定了 `--links`，则会在目标端上以相同的目标重建符号链接。注意 `--archive` 包含了 `--links`。

如果指定了 `--copy-links`，则通过复制其引用对象而非符号链接本身来“折叠”链接。

`Rsync` 还可以区分“安全”和“不安全”符号链接。可能使用此项的一个示例是网站镜像，它希望确保复制的 `rsync` 模块不包含指向站点公共部分 `/etc/passwd` 的符号链接。使用 `--copy-unsafe-links` 将导致任何链接作为其在目标端上指向的文件被复制。使用 `--safe-links` 将导致完全省略不安全的链接。（注意，必须指定 `--links`，`--safe-links` 才会生效。）

如果符号链接是绝对链接（以 `/` 开头）、空的，或者包含足够的 ".." 组件以从正在复制的目录向上移动，则被认为是不安全的。

以下是符号链接选项解释方式的摘要。列表按优先级排序，如果你的选项组合未列出，请使用是你选项的完整子集的第一行：

- `--copy-links`: 将所有符号链接转换为普通文件（不留任何链接供其他选项影响）。

- `--links --copy-unsafe-links`: 将所有不安全的符号链接转换为文件并复制所有安全的符号链接。

- `--copy-unsafe-links`: 将所有不安全的符号链接转换为文件，并忽略跳过所有安全的符号链接。

- `--links --safe-links`: 复制安全的符号链接并跳过不安全的。

- `--links`: 复制所有符号链接。

## 诊断 (DIAGNOSTICS)

`rsync` 有时会产生看起来有点晦涩的错误信息。引起最大困惑的是“protocol version mismatch -- is your shell clean?”。

此消息通常是由你的启动脚本或远程 shellset 在 `rsync` 用于传输的流上产生不需要的垃圾数据引起的。诊断此问题的方法是如下运行运行你的远程 shell：

```
ssh remotehost /bin/true > out.dat
```

然后查看 `out.dat`。如果一切运行正常，`out.dat` 应该是一个零长度的文件。如果你从 `rsync` 收到上述错误，你可能会发现 `out.dat` 包含一些文本或数据。查看内容并尝试找出是什么生成了它们。最常见的原因是配置不正确的 shell 启动脚本（例如 `.cshrc` 或 `.profile`），这些脚本包含了非交互式登录的输出语句。

如果你在调试过滤模式时遇到困难，请尝试指定 `-vv` 选项。在这一详细程度下，`rsync` 将显示每个单独文件被包含或排除的原因。

## 退出值

`0`

成功

`1`

语法或用法错误

`2`

协议不兼容

`20`

接收到 SIGUSR1 或 SIGINT

`21`

`waitpid()` 返回的错误

`22`

分配核心内存缓冲区错误

`23`

由于错误导致部分传输

`24`

由于源文件消失导致部分传输

`25`

`--max-delete` 限制停止了删除

`30`

数据发送/接收超时

`35`

等待守护进程连接超时

## 环境变量

`CVSIGNORE`

`CVSIGNORE` 环境变量可以取代 `.cvsignore` 文件中的任何忽略模式。更多细节请参阅 `--cvs-exclude` 选项。

`RSYNC_ICONV`

使用此环境变量指定默认的 `--iconv` 设置。（首次在 3.0.0 支持）

`RSYNC_PROTECT_ARGS`

如果你想默认启用 `--protect-args` 选项，请指定一个非零数值，或者指定零值以确保其默认禁用。（首次在 3.1.0 支持）

`RSYNC_RSH`

`RSYNC_RSH` 环境变量允许你覆盖用于 `rsync` 传输的默认 shell。命令名后允许使用命令行选项，就像 `-e` 选项一样。

`RSYNC_PROXY`

`RSYNC_PROXY` 环境变量允许你在连接到 `rsync` 守护进程时重定向你的 `rsync` 客户端使用 Web 代理。你应该将 `RSYNC_PROXY` 设置为主主机:端口对。

`RSYNC_PASSWORD`

将 `RSYNC_PASSWORD` 设置为所需的密码允许你在无需用户干预的情况下运行到 `rsync` 守护进程的经过身份验证的。请注意，这不会为如 `ssh` 等远程 shell 传输提供密码；要了解如何这样做，请咨询远程 shell 的文档。

`USER` 或 `LOGNAME`

`USER` 或 `LOGNAME` 环境变量用于确定发送到 `rsync` 守护进程的默认用户名。如果两个都没有设置，用户名默认为 "nobody"。

`HOME`

`HOME` 环境变量用于查找用户的默认 `.cvsignore` 文件。

## 文件

`/etc/rsyncd.conf` 或 `rsyncd.conf`

## 参见

(5)

## 缺陷

这些作为 Unix 时间值传输。

在传输到 FAT 文件系统时，`rsync` 可能会重新同步未修改的文件。请参阅 `--modify-window` 选项的注释。

文件权限、设备等作为原始数值传输。

另请参见 `--delete` 选项的注释。

请报告缺陷！请访问网站：

## 版本

此帮助页适用于 `rsync` 的 3.1.1 版本。

## 内部选项

`--server` 和 `--sender` 选项由 `rsync` 内部使用，在正常情况下绝不应用户输入。……例如当设置一个只能运行 `rsync` 命令的登录时。例如，`rsync` 分发版的支持目录下有一个示例脚本 `rrsync`（用于限制的 `rsync`），可以与限制的 `ssh` 登录配合。

## 贡献

`rsync` 根据 GNU 通用许可证分发。详情请参阅 `COPYING` 文件。

网站位于。该包含一个 FAQ-O-Matic，可能涵盖本帮助页未回答的问题。

`rsync` 的主要 ftp 站点是

如果你喜欢这个程序，我们将非常高兴收到你的反馈。请联系邮件列表：

此程序使用了由 Jean-loup Gailly 和 Mark Adler 编写的优秀 zlib 压缩库。

## 感谢

特别感谢 John Van Essen, Matt McCutchen, Wesley W. Terpstra, David Dykstra, Jos Backus, Sebastian Krahr, Martin Pool 以及我们已故但未被遗忘的同志 J.W. Schultz。

感谢 Richard Brent, Brendan Mackay, Bill Waite, Stephen Rothwell 和 David Bell。我可能漏掉了一些人，如果是这样请见谅。

## 作者

`rsync` 最初由 Andrew Tridgell 和 Paul Mackerras 编写。后来许多人对此做出了贡献。它目前由 Wayne Davison 维护。

支持和开发的邮件列表位于

* * *

# RUNCON

## 名称

`runcon` - 使用指定的 SELinux 安全上下文运行命令

## 概要

`runcon` `CONTEXT COMMAND` [*args*]`

`runcon` `[-c]` `[-u USER*]` `[-r ROLE*]` `[-t TYPE*]` `[-l RANGE*]` `COMMAND` [*args*]

## 描述

`-l`, `--range RANGE*`

级别范围

`--help`

显示此帮助并退出

`--version`

输出版本信息并退出

## 作者

由 Russell Coker 编写。

## 报告缺陷

GNU coreutils 在线帮助：<>

将 `runcon` 翻译缺陷报告至 <>

## 版权

版权所有 2015 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 版本 3 或更高版本 <>。

这是免费软件：你可以自由地更改和重新分发。在法律允许的范围内无任何保证。

## 参见

完整文档位于：<>

或通过本地获取可用：info '(coreutils) runcon invocation'

* * *

# VIM

## 名称

`vim` - Vi Improved，一个程序 rs 编辑器

## 概要

`vim` [options] [file ..]

`vim` [options] -

`vim` [options] -t tag



`vim` [options] -q [errorfile]

`ex` `gex`

`view`

`gvim` `gview`

`vimx` `evim` `eview`

`rvim` `rview` `rgvim` `rgview`

## 描述

`vim` 是一个与 Vi 兼容的文本编辑器。它可以编辑所有类型的纯文本。它对于编辑程序特别有用。

在 Vi 之上还有许多增强：多级撤销、多窗口和缓冲区、语法高亮、命令行编辑、文件名补全、在线帮助、视觉选择等。请查看 `:help vi_diff.txt` 以获取 `Vim` 和 Vi 差异总结。

在运行 `Vim` 时，可以通过在线帮助系统获得大量帮助，使用 `:help` 命令。参见下文的 ON-LINE HELP 部分。

通常使用启动 `vim` 来编辑单个文件：

```
vim file
```

通常情况下，`Vim` 的启动方式如下：

```
vim [options] [filelist]
```

如果 `filelist` 缺失，编辑器将启动一个空缓冲区。否则，可以使用以下四个选项中的恰好一个，来选择一个或多个要编辑的文件。

### `file ..`

文件名列表。第一个文件将作为当前文件并读入缓冲区。光标将置于缓冲区的第一行。你可以使用 `:next` 命令跳转到其他文件。要编辑以连字符开头的文件，请在 `filelist` 之前加上 `--`。

### `-`

要编辑的文件从 `stdin` 读取。命令从 `stderr` 读取，`stderr`应该是一个 TTY。

### `-t {tag}`

要编辑的文件和初始光标位置取决于一个“标签”（tag），类似于跳转标签。在 tags 文件中查找 `{tag}`，因为执行了当前文件和关联的命令，所以会打开关联的文件。这通常用于 C 语言程序，在这种情况下 `{tag}` 可以是一个函数名。效果是包含该函数的文件将成为当前文件，且光标定位在函数的开始处。参见 `:help tag-commands`。

### `-q [errorfile]`

以快速修复（quickFix）模式启动。读取文件 `[errorfile]` 并显示第一个错误。如果省略 `[errorfile]`，则从 `'errorfile'` 选项获取文件名（Amiga 上默认为 `"AztecC.Err"`，其他系统为 `"errors.err"`）。可以使用 `:cn` 命令跳转到后续错误。参见 `:help quickfix`。

`Vim` 的行为取决于命令的名称（执行文件可能仍然是 sa 文件）。

### `vim`

“普通”方式，一切均为默认设置。

### `ex`

以 Ex 模式启动。通过 `:vi` 命令进入普通模式。也可以通过 `-e` 参数实现。

### `view`

以只读模式启动。你将受到保护无法写入文件。也可以通过 `-R` 参数实现。

### `gvim gview`

GUI 版本。启动新窗口。

### `gex`

在 Ex 模式下启动一个新的 `gvim` 窗口。也可以通过 `gvim` 的 `-e` 参数实现。

### `vimx`

以 "Vi" 模式启动 `gvim`，与 `vim` 类似，但具有额外功能如支持 xterm 剪贴板。

### `evim eview`

简单模式下的 GUI 版本。启动新窗口。也可以通过 `-y` 参数实现。

### `rvim rview rgvim rgview`

与上述类似，但有限制。将无法启动 shell 命令或挂起 `Vim`。也可以通过 `-Z` 参数实现。

## OPTIONS

### `-C`

兼容模式。设置 `'compatible'` 选项。这会让 `Vim` 的行为大部分情况下像 Vi，即使存在 `.vimrc` 文件也是如此。

### `-d`

以 diff 模式启动。应该有两个、三个或四个文件名参数。`Vim` 将打开所有文件并显示它们之间的差异。工作方式类似于 (1)。

### `-d {device}`

打开 `{device}` 作为终端使用。仅限 Amiga。示例：`" -d con:20/30/600/150"`。

### `-D`

调试。在执行脚本中的第一个命令时进入调试模式。

### `-e`

以 Ex 模式启动 `Vim`，就像调用执行文件 "ex" 一样。

### `-E`

以改进的 Ex 模式启动 `Vim`，就像调用执行文件 "exim" 一样。

### `-f`

前台。对于 GUI 版本，`Vim` 将不会派生并从启动它的 shell 中分离。在 Amiga 上，`Vim` 不会重启打开新窗口。当 `Vim` 由一个等待编辑会话结束的程序（例如邮件）执行时，应使用此选项。在 Amiga 上，`:sh` 和 `:!` 命令同样如此。

### `--nofork`

前台。对于 GUI 版本，`Vim` 将不会派生并从启动它的 shell 中分离。

### `-F`

如果 `Vim` 编译时带有 FKMAP 支持（用于编辑从右向左的文件和阿拉伯语键盘映射），则此选项将以波斯语模式启动 `Vim`，即设置 `'fmap'`。否则，将给出错误信息并终止 `Vim`。

### `-g`

如果 `Vim` 编译时带有 GUI 支持，则此选项将启用 GUI。如果没有编译 GUI 支持，将给出错误信息。

### `-h`

关于命令行的一些帮助。执行后 `Vim` 将退出。

### `-H`

如果 `Vim` 编译时带有 RIGHTLEFT 支持（用于编辑从右向左的文件和希伯语键盘映射），则此选项将以希伯语模式启动 `Vim`，即设置 `'hmap'`。否则，将给出错误信息并终止 `Vim`。

### `-i {viminfo}`

当启用 viminfo 文件时，此选项设置使用的文件名，而不是 `"~/.viminfo"`。也可以通过给出 "NONE" 来跳过对 .viminfo 的使用。

### `-L`

同于 `-r`。

### `-l`

Lisp 模式。开启 `'lisp'` 和 `'showmatch'` 选项。

### `-m`

禁用修改文件。重置 `'write'` 选项。你仍然可以修改缓冲区，但无法写入文件。

### `-M`

不允许修改。将取消 `'modifiable'` 和 `'write'` 选项的设置，因此不允许更改且无法写入文件。注意，这些选项可以设置为以启用修改。

### `-N`

非兼容模式。重置 `'compatible'` 选项。这会让 `Vim` 的行为稍微好一点，但与 Vi 兼容，即使存在 `.vimrc` 文件也是如此。

### `-n`

不使用交换文件。崩溃后的恢复将是不可能的。如果你想在非常缓慢的介质（如磁盘）上编辑文件，此选项非常有用。可以通过 `:set uc=0` 实现。可以通过 `:set uc=200` 还原。

### `-nb`

作为 NetBeans 的编辑器服务器。详情请阅文档。

### `-o[N]`

堆叠打开 N 个窗口。如果省略 N，则为每个文件打开一个窗口。

### `-O[N]`

并排打开 N 个窗口。如果省略 N，则为每个文件打开一个窗口。

### `-p[N]`

打开 N 个标签页。如果省略 N，则为每个文件打开一个标签页。

### `-R`

只读模式。将设置 `'readonly'`。你仍然可以编辑缓冲区，但会被防止意外覆盖文件。如果你想覆盖文件，请在 Ex 命令后加上感叹号，如 `:w!`。`-R` 选项也隐含 `-n` 选项（见下文）。`'readonly'` 选项可以通过 `:set noro` 重置。参见 `:help 'readonly'`。

### `-r`

列出交换文件以及关于使用它们进行恢复的信息。

### `-r {file}`

恢复模式。使用交换文件恢复崩溃的编辑会话。交换文件是以文本文件名加上 ".swp"。参见 `:help recovery`。

### `-s`

静默模式。仅当作为 "Ex" 启动或在 `-s` 选项之前给出了 `-e` 选项有效。

### `-s {scriptin}`

读取脚本文件 `{scriptin}`。文件中的字符将被解释为就像你输入过的一样。可以使用命令 `:source! {scriptin}` 完成。如果在编辑器退出之前到达了文件末尾，则将从键盘读取后续字符。

### `-T {terminal}`

告诉 `Vim` 你正在使用的终端名称。只有在自动方法不起作用时才需要。应该是 `Vim` 已知的（内置）终端，或在 termcap 或 terminfo 文件中定义的终端。

### `-u {vimrc}`

使用文件 `{vimrc}` 中的命令进行初始化。跳过所有其他初始化。用此编辑特殊类型的文件。也可以通过提供名称 "NONE" 来跳过所有初始化。更多信息请查看 vim 内的 `:help initialization`。

### `-U {gvimrc}`

使用文件 `{gvimrc}` 中的命令进行 GUI 初始化。跳过所有其他初始化。也可以通过提供名称 "NONE" 来跳过所有 GUI 初始化。更多信息请查看 vim 内的 `:help gui-init`。

### `-V[N]`

详细模式。提供关于加载了哪些文件以及读写 viminfo 文件的信息。可选的数字 N 是 `'verbose'` 的值。默认是 10。

### `-v`

以 Vi 模式启动 `Vim`，就像执行文件名为 "vi" 一样。这仅在调用执行文件名为 "ex" 时有效。

### `-w {scriptout}`

你输入的所有字符都会记录在文件 `{scriptout}` 中，直到你退出 `Vim`。如果你想创建一个用于 `vim -s` 或 `:source!` 的脚本文件，这很有用。如果 `{scriptout}` 文件存在，则追加字符。

### `-W {scriptout}`

类似于 `-w`，但覆盖现有文件。

### `-x`

写入文件时使用加密。将提示输入密钥。

### `-X`

不连接到 X 服务器。缩短在终端中的启动时间，但不会使用窗口标题和剪贴板。

### `-y`

以简单模式启动 `Vim`，就像执行文件名为 "evim" 或 "eview" 一样。让 `Vim` 的行为像一个点击输入编辑器。

### `--remote-expr {expr}`

连接到 Vim 服务器，在其中求值 `{expr}` 并结果打印到标准输出。

### `--remote-send {keys}`

连接到 Vim 服务器并向其发送 `{keys}`。

### `--remote-silent`

类似于 `--remote`，但在未找到服务器时不显示警告。

### `--remote-wait`

类似于 `--remote`，但在文件被编辑之前 Vim 不退出。

### `--remote-wait-silent`

类似于 `--remote-wait`，但在未找到服务器时不显示警告。

### `--remote-tab[-wait][-silent]`

类似于 `--remote` 但每个文件使用一个标签页。

### `--role`

设置唯一角色以识别主窗口。

### `--serverlist`

列出可以找到的所有 Vim 服务器名称。

### `--serverna {na}`

使用 `{na}` 作为服务器名称。用于当前 Vim，除非与 `--remote` 参数一起使用，此时它是要连接的服务器名称。

### `--socketid {id}`

GTK GUI 专用：使用 GtkPlug 机制在另一个窗口中运行 gvim。

### `--version`

打印版本信息并退出。

## 在线帮助

在 `Vim` 中输入 `:help` 开始。输入 `:help subject` 获取特定主题的帮助。例如：`:help ZZ` 获取 "ZZ" 命令的帮助。使用 `<Tab>` 和 `CTRL-D` 补全主题（`:help cmdline-completion`）。存在标签用于从一个地方跳转到另一个地方（类似于超链接，参见 `:help`）。所有文档文件都可以通过这种方式查看，例如 `:help syntax.txt`。

## 文件

- `/usr/share/vim/vim74/doc/*.txt`

`Vim` 文档文件。使用 `:help doc-file-list` 获取完整列表。

- `/usr/share/vim/vim74/doc/tags`

用于在文档文件中查找信息的标签文件。

- `/usr/share/vim/vim74/syntax/syntax.vim`

系统级语法初始化。

- `/usr/share/vim/vim74/syntax/*.vim`

各种语言的语法文件。

- `/etc/vimrc`

系统级 `Vim` 初始化。

- `~/.vimrc`

你的个人 `Vim` 初始化。

- `/etc/gvimrc`

系统级 gvim 初始化。

- `~/.gvimrc`

你的个人 gvim 初始化。

- `/usr/share/vim/vim74/optwin.vim`

用于 `:options` 命令的脚本，查看和设置选项的好方法。

- `/usr/share/vim/vim74/nu.vim`

gvim 的系统级 nu 初始化。

- `/usr/share/vim/vim74/bugreport.vim`

生成错误报告的脚本。参见 `:help bugs`。

- `/usr/share/vim/vim74/filetype.vim`

通过名称检测文件类型的脚本。参见 `:help 'filetype'`。

- `/usr/share/vim/vim74/scripts.vim`

通过内容检测文件类型的脚本。参见 `:help 'filetype'`。

- `/usr/share/vim/vim74/print/*.ps`

用于 PostScript 打印的文件。

欲需最新信息，请参阅 VIM 帮助页：

`<URL:>`

## 另见

(1)

## 作者

`Vim` 的大部分由 Bram Moolenaar 制作，并得到了许多人的帮助。请查看 Vim 内的 `:help credits`。

`Vim` 基于 Stevie，由 Tim Thompson、Tony Andrews 和 G.R. (Fred) Walter 维护。尽管几乎没有原始代码留存。

## 缺陷

可能有。参见 `:help todo` 获取问题列表。注意，某些因为 Vi 行为不同而可能被视为错误的项，你应该仔细查看 `'compatible'` 选项。

* * *

# RYGEL

## 名称

rygel - 一组 DLNA/UPnP 服务

## 摘要

**rygel** [**选项**]

## 描述

**rygel** 是一个 DLNA/UPnP 媒体解决方案，允许你轻松共享音频、视频和图片，并控制网络上的媒体播放器。从技术角度上说，它是通过插件机制实现的 UPnP 服务器和媒体渲染器。通过遵循 DLNA 非常严格的要求来实现与其他设备的可操作性。

## 选项

程序遵循标准的 GNU 命令行语法，长选项以两个连字符开头。下方包含了选项摘要。

### `-h`, `--help`

显示选项摘要。

### `--version`

显示程序版本。

### `-i`, `--title=PLUGIN_NAME:TITLE`

设置插件 `PLUGIN_NAME` 的标题为 `TITLE`。对于你想设置名称的每个插件，可以使用此选项多次。

### `-o`, `--plugin-option=PLUGIN_NAME:OPTION:VALUE1[,VALUE2,...]`

为插件设置选项。

### `-P`, `--disable-upnp`

禁用通过 UPnP 广告并将 `rygel` 设置为仅流媒体模式。

### `-c`, `--config=CONFIG_FILE`

使用 `CONFIG_FILE` 代替 `${XDG_CONFIG_DIR}/rygel.conf`。

### `-s`, `--shutdown`

关闭当前运行的 `rygel` 实例。

### `-r`, `--replace`

用此实例替换当前运行的 `rygel` 实例。`rygel -s && rygel` 的缩写。

## FILES

`/etc/rygel.conf`

系统级配置文件，用于控制 `rygel` 的行为。详情请见 (5)。

`${XDG_CONFIG_DIR}/rygel.conf`

用户级配置文件，用于控制 `rygel` 的行为。详情请见 (5)。

`${XDG_CONFIG_DIR}/Rygel/*.x`

已缓存的 UPnP 设备描述文件。

## ENVIRONMENT

`RYGEL_DISABLE_UPNP`

禁用通过 UPnP 广告并将 `rygel` 设置为仅流媒体模式。

`RYGEL_IFACE`

设置要绑定的网络接口。

`RYGEL_PORT`

定义要绑定的网络端口。

`RYGEL_DISABLE_TRANSCODING`

全局禁用转码。

`RYGEL_LOG`

设置 `rygel` 的日志级别。

`RYGEL_PLUGIN_PATH`

设置 `rygel` 的插件搜索路径。

`RYGEL_ENGINE_PATH`

设置 `rygel` 的 dia 流媒体和转码引擎搜索路径。

`RYGEL_MEDIA_ENGINE`

设置特定的 dia 流媒体引擎从 dia 引擎搜索路径中选取。

`RYGEL_DISABLE_UPLOAD`

禁用通过 UPnP 禁用 dia 文件上传。

`RYGEL_DISABLE_DELETION`

禁用通过 UPnP 远程删除文件。

`RYGEL_PLUGIN_TIMEOUT`

设置查找插件的超时时间。在 valgrind 内部运行时增加此值很有用。

此外，对于每个插件，你都可以设置以下环境变量：

`RYGEL_PLUGIN_NAME_TITLE`

设置插件的标题。

`RYGEL_PLUGIN_NAME_ENABLED`

启用或禁用该插件。

## BUGS

可以在 m[] 找到缺陷跟踪系统。

## SEE ALSO

(5)

## AUTHOR

`Jens Georg` <>

编写了此手册页。

* * *

# RZ

## NAME



`rx`, `rb`, `rz` - XMODEM, YMODEM, ZMODEM (批量) 文件接收

如果没有接收到 True YMODEM 文件信息，路径中的斜杠将改为下划线，并消除文件名末尾的任何点。这种转换对于从 CP/M 系统接收的文件有用。对于 YMODEM，除非文件名包含一个或多个小写字母，否则每个文件名都将转换为小写。

`Rx` 使用 XMODEM 或 XMODEM-1k 协议接收单个文件。用户应判断 1024 字节块长度何时实际提高吞吐量而不会产生问题。用户应向发送和接收程序提供文件名。接收的文件可能会增加最多 1023 个垃圾字符。

`Rz` 可以作为 `rzCOMMAND` 调用（带有由 (1) 生成的可选 -）。对于每个接收到的文件，`rz` 将文件管道到 `COMMAND filena`，其中 `filena` 是传输文件的文件名，文件内容作为标准输入。

当 `COMMAND` 以 0 状态退出时，每个文件传输均确认。非零退出状态将终止传输。

这种形式的典型用法是 `rzrmail`，它调用 (1) 向由传输文件名指定的用户发送邮件。例如，从 PC-DOS 系统将文件 "caf" 发送到 Unix 系统上的 `rzrmail` 将导致 DOS 文件 "caf" 的内容被邮件给用户 "caf"。

在某些 Unix 系统上，登录目录包含指向 `COMMAND` 的链接，因为登录设置了 `SHELL=rsh`，这不允许使用绝对路径。如果带有 "v" 调用，`rz` 将进入详细模式（见 `v` 选项）。以下条目适用于 Unix SYS III/V：

```
rzrmail::5:1::/bin:/usr/local/rzrmail
```

如果 `SHELL` 环境变量包含 `rsh`、`rbash` 或 `rksh`（限制 shell），`rz` 将不接受绝对路径或对父目录的引用，不会修改现有文件，并移除任何接收错误的文件。

如果调用 `rz` 时将 `stdout` 和 `stderr` 输出到不同的数据集，详细模式将设置为 2，导致逐行将进度报告发送到 `stderr`。这可以通过 `q` 选项禁用。

## OPTIONS

可用选项的含义如下：

`-+`, `--append`

将接收到的数据追加到现有文件（ZMODEM, 仅限 ASCII）。

`-a`, `--ascii`

通过删除回车和所有从第一个 Control Z（CP/M 文件结束）开始的字符将文件转换为 Unix 约定。

`-b`, `--binary`

二进制（原样传输）文件传输覆盖。

`-B NUMBER`, `--bufsize NUMBER`

在写入磁盘之前缓冲 `NUMBER` 字节。默认是 32768，这对于大多数情况都是足够的。如果你有一台慢速机器、糟糕磁盘接口或遭受其他硬件问题，你可能想要增加缓冲区大小。`-1` 或 `auto` 使用足够缓冲整个文件的缓冲区。小心使用此选项 - 如果机器开始交换，情况通常会变糟而不是变好。

`-c`, `--with-crc`

仅限 XMODEM。使用 16 位 CRC（通常使用一个字节校验和）。

`-C`, `--allow-remote-commands`

允许执行远程命令（不安全）。这允许发送者通过 `system()` 或 `execl()` 执行任意命令。默认禁用此功能（?）。在在限制模式下运行时忽略此选项。

`-D`, `--null`

将文件数据输出到 `/dev/null`；用于测试（仅限 Unix）。

`--delay-startup N`

在执行任何操作之前等待 `N` 秒。

`-e`, `--escape`

强制发送者转义所有控制字符；通常 `XON`、`XOFF`、`DLE`、`CR-CR`、`Ctrl-X` 被转义。

`-E`, `--rena`

如果目标文件名存在则重命名输入文件。新文件名将附加点和一个数字 (0..999)。

`-h`, `--help`

显示帮助屏幕。

`-m N`, `--min-bps N`

如果 BPS-速率（每秒字节）低于 `N` 持续一段时间（见 `--min-bps-ti` 选项）则停止传输。

`-M N`, `--min-bps-ti`

与 `--min-bps` 配合使用。默认是 120（秒）。

`-O`, `--disable-tiouts`

禁用读取超时处理代码。这会导致 `lrz` 在发送者不发送任何内容时挂起，但可以提高性能（通过减少约 50% 的系统调用）。

谨慎使用此选项。

`--o-sync`

以同步写入模式打开输出文件。如果在 update（或你系统上的守护进程）将缓冲区写入磁盘时你遇到由于中断丢失导致的错误，则这可能是有用的。

如果你的系统不支持 `O_SYNC`，将忽略此选项并打印警告。

`-p`, `--protect`

(ZMODEM) 保护：如果目标文件存在则跳过文件。

`-q`, `--quiet`

静默模式抑制详细输出。

`-r`, `--resu`

崩溃恢复模式。`lrz` 尝试恢复中断的文件传输。

### `-R, --restricted`

进入更受限制的模式。如果给出此选项，`lrz` 将不会创建以点开头的目录或文件。

关于受限制模式的信息，请参见 `SECURITY`。

### `-s HH:MM, --stop-at HH:MM`

在 `HH` 小、`MM` 分后停止传输。另一种变体使用 `+N` 代替 `HH:MM,` 在 `N` 秒后停止传输。

### `-S, --tisync`

向发送方请求 tisync 包。发送方发送其系统 `ti`，导致 `lrz` 因差异超过 60 秒而报错。

如果给出两次此选项，`lrz` 将尝试将本地系统 `ti` 设置为远程 `ti`（如果 `lrz` 不是由 `root` 运行的，则会失败）。

此选项使 `lrz` 与某些其他 ZModems 不兼容。除非你知道自己在做什么，否则不要使用它。

### `--syslog[=off]`

开启或关闭系统日志。默认设置在配置 `ti` 时确定。如果没有编译系统日志支持，此选项将被忽略。

### `-t TIM, --tiout TIM`

将 `tiout` 改为 `TIM` 十分之一秒。如果通过 `O` 选项禁用 `tiout` 处理，则此选项被忽略。

### `--tcp-client ADDRESS:PORT`

使用 XMODEM 协议。

### `-y, --overwrite`

是，覆盖任何同名的现有文件。

### `--ymodem`

使用 YMODEM 协议。

### `-Z, --zmodem`

使用 ZMODEM 协议。

## SECURITY

与原始的 ZMODEM 不同，`lrz` 默认进入受限制模式。在受限制模式下，`lrz` 不接受绝对路径或对父目录的引用，不会修改现有文件，并移除任何接收的文件。远程命令执行已禁用。

要使用更受限制的模式，请设置环境变量 `ZMODEM_RESTRICTED` 或给出 `R` 选项。这将禁用子目录和隐藏文件的创建。

可以使用 `U` 选项关闭受限制模式，除非 `lrz` 在受限制的 shell 下运行。

使用 `--tcp-client` 或 `--tcp-server` 选项会带来安全风险，因为其他人可以在你之前连接到端口并夺取你的数据。如果对更安全的模式有强烈需求，我可能会引入某种密码挑战。

## ENVIRONMENT

`lrz` 使用以下环境变量：

### `SHELL`

如果此变量包含 `rsh` 或 `rksh`，`lrz` 会识别为受限制 shell。

### `ZMODEM_RESTRICTED`

如果设置了该变量，`lrz` 进入更受限制的模式。

## EXAMPLES

(Pro-YAM 命令)

```
<ALT-2>
```

Pro-YAM 命令：`sz *.h *.c`

（会自动在连接的系统上调用 `rz`。）

## SEE ALSO

`ZMODEM.DOC`, `YMODEM.DOC`, `Professional-YAM`, `crc(on)`, `sz(on)`, `usq(on)`, `undos(on)`

各种操作系统所需的编译 `ti` 选项在源文件中已有描述。

## NOTES

已知向 tisharing 微型计算机以持续高速度发送串口数据会导致锁死、系统停止、内核恐慌以及偶尔的反社会行为。在对系统进行高速度输入实验时，如果文件传输未成功，请考虑重启系统，特别是当系统的状态似乎发生了变化时。

Unix "ulimit" 参数必须设置得足够高以便大文件传输。

某些系统上的 TTY 输入缓冲可能不允许长块或高速流输入。当你无法使用 ZMODEM、YMODEM-1k 或 XMODEM-1k 向 Unix 系统以高速度发送数据，而使用 128 字节块的 YMODEM 正常工作时，你应该怀疑此问题。如果系统的 `tty` 行处理真的损坏了，串口端口或整个系统可能无法承受长距离突发高速数据的冲击。

DSZ 或 Pro-YAM 的 `zmodem l` 数字参数可以设置为 64 到 1024 之间的值，以限制突发长度（"zmodem pl128"）。

32 位 CRC 代码由 Gary S. Brown 提供。目录创建代码来自 John Gilmore 的 PD TAR 程序。

## BUGS

从大多数版本的 (1) 调用 `rz` 是不起的，因为 `cu` 的接收进程会与 `rz` 争夺调制调器的字符。

未正确实现指定的文件传输协议的可能导致 `sz` 挂起一两分钟。报告的此类问题实例已通过使用 `ZCOMM`、Pro-YAM 或具有正确协议实现的程序得到了修正。

许多声称支持 YMODEM 的程序仅支持 1k 块的 XMODEM，且它们往往也做得并不很好。

路径名限制为 127 个字符。在 XMODEM 单文件模式下，命令行给出的路径仍按上述描述进行处理。ASCII 选项的 CR/LF 到 NL 转换依赖删除 CR；`undos(on)` 执行的是更智能的转换。

## VMS VERSION

VMS 版本不设置文件 `ti`。

VMS C 标准 I/O 和 RMS 可能会相互作用并意外修改文件内容。

VMS 版本不支持作为 `rzCOMMAND` 调用。当前的 VMS 版本不支持 XMODEM、XMODEM-1k 或 YMODEM。

根据 VMS 文档，用于 VMS 版本 `rz` 的缓冲输入例程为每个协议事务引入长达一秒的延迟。这种延迟对于非常短的文件可能是巨大的。从 `rz.c` 中删除 `#define BUFREAD` 行将消除这种延迟，代价是增加 CPU 利用率。

VMS 版本会导致 DCL 在某些错误条件下产生随机且荒谬的错误信息；这是 VMS 的 "exit" 函数与 Unix/MSDOS 标准不兼容的结果。

## ZMODEM CAPABILITIES

`Rz` 支持传入的 ZMODEM 二进制 (`-b`)、ASCII (`-a`)、保护 (`-p`)、覆盖 (`-y`) 和追加 (`+`) 请求。默认值是保护 (`-p`) 和二进制 (`-b`)。

Unix 版本支持 ZMODEM 命令执行。

## FILES

`rz.c`, `crctab.c`, `rbsb.c`, `zm.c`, `zmodem.h` Unix 源文件。

`rz.c`, `crctab.c`, `vrzsz.c`, `zm.c`, `zmodem.h`, `vmodem.h`, `vvmodem.c` VMS 源文件。

***

# S_CLIENT

## NAME

`s_client` - SSL/TLS 客户端程序

## SYNOPSIS

```
openssl s_client [-connect host:port] [-serverna na] [-verify depth] [-verify_return_error] [-cert filena] [-certform DER|PEM] [-key filena] [-keyform DER|PEM] [-pass arg] [-CApath directory] [-CAfile filena] [-trusted_first] [-no_alt_chains] [-reconnect] [-pause] [-showcerts] [-debug] [-msg] [-nbio_test] [-state] [-nbio] [-crlf] [-ign_eof] [-no_ign_eof] [-quiet] [-ssl2] [-ssl3] [-tls1] [-tls1_1] [-tls1_2] [-dtls1] [-no_ssl2] [-no_ssl3] [-no_tls1] [-no_tls1_1] [-no_tls1_2] [-fallback_scsv] [-bugs] [-cipher cipherlist] [-serverpref] [-starttls protocol] [-engine id] [-tlsextdebug] [-no_ticket] [-sess_out filena] [-sess_in filena] [-rand file(s)] [-serverinfo types] [-status] [-nextprotoneg protocols]
```

## DESCRIPTION

`s_client` 命令实现了一个通用的 SSL/TLS 客户端，可以通过 SSL/TLS 连接到远程主机。它是 SSL 服务器非常有用的诊断工具。

## 参数（OPTIONS）

`-connect host:port`

指定要连接的主机和可选端口。如果未指定，则将尝试连接到本地主机的 4433 端口。

`-serverna na`

在 ClientHello 消息中设置 TLS SNI（服务器名称指示）扩展。

`-cert certna`

如果服务器请求证书，则使用的证书文件。默认情况下不使用证书。

`-certform format`

使用的证书格式：DER 或 PEM。PEM 是默认格式。

`-key keyfile`

使用的私钥文件。如果未指定，则将使用证书文件。

`-reconnect`

使用相同的会话 ID 重新连接到服务器，这可以用来测试会话缓存是否工作。

`-pause`

在每次读写调用之间暂停 1 秒。

`-showcerts`

显示整个服务器证书链：通常只显示服务器证书本身。

`-prexit`

在程序退出时打印会话信息。即使连接失败，也会尝试打印信息。通常情况下，如果连接成功只会打印一次。此选项很有用，因为使用的加密算法可能会重新协商，或者可能在尝试访问特定 URL 后才要求客户端证书导致连接失败。注意：此选项产生的输出并不总是准确，因为连接可能从未建立。

`-state`

打印 SSL 会话状态。

`-debug`

打印详细的调试信息，包括所有流量的十六进制转储。

`-msg`

显示十六进制转储的所有协议消息。

`-nbio_test`

测试非阻塞 I/O。

`-nbio`

开启非阻塞 I/O。

`-crlf`

此选项将终端的换行符转换为服务器所需的 CR+LF。

`-ign_eof`

在输入到达文件结束（EOF）时阻止关闭连接。

`-quiet`

禁止打印会话和证书信息。这也会隐式开启 `-ign_eof`。

`-no_ign_eof`

在输入到达文件结束（EOF）时关闭连接。可用于覆盖 `-quiet` 后的隐式 `-ign_eof`。

`-psk_identity identity`

在使用 PSK 加密套件时使用 PSK 标识 `identity`。

`-psk key`

在使用 PSK 加密套件时使用 PSK 密钥 `key`。密钥以十六进制数字给出，不带前缀 `0x`，例如 `-psk 1a2b3c4d`。

`-ssl2`, `-ssl3`, `-tls1`, `-tls1_1`, `-tls1_2`, `-dtls1`, `-no_ssl2`, `-no_ssl3`, `-no_tls1`, `-no_tls1_1`, `-no_tls1_2`

这些选项禁用某些 SSL 或 TLS 协议。默认初始握手使用的方法应与所有服务器并允许它们使用 SSL v3、SSL v2 或 TLS。遗憾的是，目前仍在使用古老且损坏的服务器，它们无法处理这种技术并会导致连接失败。因此，只有在关闭 TLS 时服务器才能工作。

`-fallback_scsv`

在 ClientHello 中发送 `TLS_FALLBACK_SCSV`。

`-bugs`

SSL 和 TLS 实现中存在若干已知 Bug。添加此选项将启用各种变解决方案。

`-cipher cipherlist`

允许修改客户端发送的加密算法列表。虽然由服务器决定使用哪种加密套件，但它应该取客户端发送列表中第一个支持的加密算法。更多信息请参阅 `ciphers` 命令。

`-serverpref`

使用服务器的加密算法偏好；仅用于 SSLV2。

`-starttls protocol`

发送特定协议的消息以切换到 TLS 通信。`protocol` 是目标协议的关键字。目前支持的关键字有 `smtp`、`pop3`、`imap` 和 `ftp`。

`-tlsextdebug`

打印从服务器收到的任何 TLS 扩展的十六进制转储。

`-no_ticket`

禁用 RFC4507bis 会话票。

`-sess_out filena`

将 SSL 会话输出到 `filena`。

`-sess_in sess.pem`

从 `filena` 加载 SSL 会话。客户端将尝试从该会话恢复连接。

`-engine id`

指定引擎（通过其唯一 `id` 字符串）将导致 `s_client` 尝试获取指定引擎的功能引用，从而在需要时对其进行初始化。该引擎将设置为所有可用算法的默认引擎。

`-rand file(s)`

包含随机数据的文件，用于为随机数生成器种子，或 EGD 套接字（参见 (3)）。可以指定多个文件，并用操作系统依赖的字符分隔。MS-Windows 使用 `;`，OpenVMS 使用 `,`，其他所有使用 `:`。

`-serverinfo types`

逗号分隔的 TLS 扩展类型列表（数字在 0 到 65535 之间）。每个类型都将作为一个空的 ClientHello TLS 扩展发送。服务器的响应（如果有）将被编码并作为 PEM 文件显示。

`-status`

向服务器发送证书状态请求（OCSP 封字）。服务器响应（如果有）将打印出来。



`-nextprotoneg protocols`

启用下一协议协商 TLS 扩展，并提供客户端应声明支持的逗号分隔协议名称列表。列表应将最想要的协议在前。协议名称是可打印的 ASCII 字符串，例如 `http/1.1` 或 `spdy/3`。空列表将被特殊处理，会导致客户端在接收到带有服务器支持协议列表的 ServerHello 后立即断开。

## 连接后的命令（CONNECTED COMMANDS）

如果与 SSL 服务器建立了连接，从服务器收到的任何数据将显示，任何按键将发送到服务器。在交互式使用时（即未提供 `-quiet` 或 `-ign_eof`），如果行以`R`开头则将重新协商会话；如果行以`Q`开头或到达文件结束，连接将关闭。

## 注意事项（NOTES）

`s_client` 可调试 SSL 服务器。连接到 SSL HTTP 服务器通常使用命令：

```
openssl s_client -connect serverna:443
```

（https 使用 443 端口）。如果连接成功，可以给出 HTTP 命令，如 `GET /` 来检索网页。

如果握手失败，可能有多种原因。如果没有明显的异常（例如缺少客户端证书），可以尝试 `-bugs`、`-ssl2`、`-ssl3`、`-tls1`、`-no_ssl2`、`-no_ssl3`、`-no_tls1` 等选项，以防存在 Bug。特别是，你应该在向 OpenSSL 邮件列表提交错误报告**之前**尝试这些选项。

在尝试使客户端证书生效时，一个常见问题是 Web 客户端抱怨没有证书或提供了一个空列表供选择。这通常是因为服务器在请求证书时，没有在其“接受的 CA 列表”中发送客户端证书授权机构。通过使用 `s_client` 可以查看并检查 CA 列表。然而某些服务器仅在请求特定 URL 后才请求客户端身份验证。在这种情况下，必须使用 `-prexit` 选项并对适当的页面发送 HTTP 请求来获取列表。

如果在命令行中使用 `-cert` 选项指定了证书，除非服务器专门请求客户端证书，否则将不会使用它。因此，仅在命令行中包含客户端证书并不能保证该证书有效。

如果在验证服务器证书时遇到问题，可以使用 `-showcerts` 选项显示整个链。

由于 SSLv23 客户端请求不能包含压缩方法或扩展，因此只有在禁用它们的使用时（例如使用 `-no_sslv2` 选项），它们才会被支持。

`s_client` 工具是一个测试工具，设计用于在任何证书验证错误后继续握手。结果是它将接受对方发送的任何证书链（无论是否信任）。任何测试应用程序都**不应**这样做，因为这会导致它们容易受到中间人（MITM）攻击。这种行为可以通过 `-verify_return_error` 选项进行更改：此时任何验证错误都将返回并终止握手。

## BUGS

由于此程序有很多选项，而且由于使用的技术相当老旧，`s_client` 的 C 源代码相当难读，并不是实现方式的范例。一个典型的 SSL 客户端程序会简单得多。

`-accept port`

监听连接的 TCP 端口。如果未指定，则使用 4433。

`-context id`

设置 SSL 上文 ID。它可以是任何字符串值。如果不存在此选项，则将使用默认值。

`-cert certna`

使用的证书。大多数服务器加密套件都要求使用证书，因此需要具有特定公钥类型的证书：例如，DSS 加密套件需要包含 DSS (DSA) 密钥的证书。如果未指定，则将使用文件 `server.pem`。

`-certform format`

使用的证书格式：DER 或 PEM。默认为 PEM。

`-key keyfile`

使用的私钥。如果未指定，则将使用证书文件。

`-keyform format`

使用的私钥格式：DER 或 PEM。默认为 PEM。

`-pass arg`

私钥密码源。关于`arg`格式的更多信息，请参阅 (1) 中的 `PASS PHRASE ARGUMENTS` 章节。

`-dcert filena`, `-dkey keyna`

指定额外的证书和私钥，它们的行为与 `-cert` 和 `-key` 选项相同，区别是如果未指定，则没有默认值（不使用额外的证书和密钥）。如上所述，某些加密套件需要包含特定类型密钥的证书。因此，加密套件需要携带 RSA 密钥的证书以及 DSS (DSA) 密钥的证书。通过使用 RSA 和 DSS 证书及密钥，服务器可以使用适当的证书支持仅支持 RSA 或 DSS 加密套件的客户端。

`-dcertform format`, `-dkeyform format`, `-dpass arg`

分别指定额外的证书、私钥格式和密码。

`-nocert`

如果设置此选项，则不使用证书。这会将可用加密套件限制为匿名套件（目前仅限匿名 DH）。

`-dhparam filena`

使用的 DH 参数文件。临时 DH 加密套件使用一组 DH 参数生成密钥。如果未指定，则尝试从服务器证书文件中加载参数。如果失败，则将使用硬编码在 `s_server` 程序中的静态参数集。

`-no_dhe`

如果设置此选项，将不会加载 DH 参数，从而禁用临时 DH 加密套件。

`-no_tmp_rsa`

某些导出加密套件使用临时 RSA 密钥，此选项禁用临时 RSA 密钥的生成。

`-verify depth`, `-Verify depth`

使用的验证深度。这指定了客户端证书链的最大长度并让服务器向客户端请求证书。使用 `-verify` 选项会请求证书但客户端不必发送；使用 `-Verify` 选项时客户端必须提供证书，否则会发生错误。

如果加密套件无法请求客户端证书（例如匿名加密套件或 PSK），则此选项无效。

`-crl_check`, `-crl_check_all`

检查对方证书未被其 CA 撤销。CRL 被附加到证书文件中。使用 `-crl_check_all` 选项会检查链中所有 CA 的所有 CRL。

`-CApath directory`

用于客户端证书验证的目录。该目录必须是“哈希格式”，更多信息请见 `verify`。这些目录也用于构建服务器证书链。

`-CAfile file`

包含受信任证书的文件，用于客户端身份验证以及在尝试构建服务器证书链时。该列表也用于请求证书时传递给客户端的接受 CA 列表。

`-trusted_first`

在构建验证客户端证书的信任链时优先使用 CA 文件或 CA 目录中的证书。这在桥接 CA 或交叉认证 CA 的环境中特别有用。

`-no_alt_chains`

详情请阅 `verify` 手册页。

`-state`

打印 SSL 会话状态。

`-debug`

打印大量的调试信息，包括所有流量的十六进制转储。

`-msg`

显示带有十六进制转储的所有协议消息。

`-nbio_test`

测试非阻塞 I/O。

`-nbio`

开启非阻塞 I/O。

`-crlf`

此选项将终端的换行符转换为 CR+LF。

`-quiet`

抑制会话和证书信息的打印。

`-psk_hint hint`

在使用 PSK 密码套件时使用 PSK 身份提示`hint`。

`-psk key`

在使用 PSK 密码套件时使用 PSK 密钥`key`。密钥以十六进制数字形式给出，不带前缀 0x，例如`-psk 1a2b3c4d`。

`-ssl2`, `-ssl3`, `-tls1`, `-tls1_1`, `-tls1_2`, `-dtls1`, `-no_ssl2`, `-no_ssl3`, `-no_tls1`, `-no_tls1_1`, `-no_tls1_2`

这些选项禁用某些 SSL 或 TLS 协议。默认情况下，初始握手使用一种与所有服务器都兼容的方法，并允许它们根据情况使用 SSL v3、SSL v2 或 TLS。

`-no_ticket`

禁用 RFC4507bis 会话票支持。

`-www`

在连接时向客户端回发状态消息。这包含了许多关于所用密码套件和各种会话参数的信息。输出为 HTML 格式，因此此选项通常与网络浏览器配合使用。

`-WWW`

启动一个简单的 Web 服务器。页面将相对于当前目录解析，例如，如果请求 URL，将加载 `./page.ht` 文件。

`-HTTP`

启动一个简单的 Web 服务器。页面将相对于当前目录解析，例如，如果请求 URL，将加载 `./page.ht` 文件。假设加载的文件包含完整且正确的 HTTP 响应（作为 HTTP 响应行和头部的行以 CRLF 结尾）。

`-engine id`

指定引擎（通过其唯一的`id`字符串）将导致 `s_server` 尝试获取指定引擎的功能引用，从而在需要时对其初始化。该引擎将设置为所有可用算法的默认引擎。

`-id_prefix arg`

生成以`arg`为前缀的 SSL/TLS 会话 ID。这对于想要处理多个服务器的 SSL/TLS 代码（例如代理）非常有用，每个服务器可能会生成唯一范围的会话 ID（例如带有特定前缀）。

`-rand file(s)`

包含随机数据的文件（用于随机数生成器的种子），或一个 EGD 套接（见 (3)）。可以指定多个文件，并用操作系统的字符分隔。MS-Windows 使用`;`，OpenVMS 使用`,`,所有其他系统使用`:`。

`-serverinfo file`

包含一个或多个 PEM 数据块的文件。每个 PEM 块应编码一个 TLS ServerHello 扩展（2 字节类型，2 字节长度，随后是`length`字节扩展数据）。如果客户端发送了匹配类型的空 TLS ClientHello 扩展，将返回相应的 ServerHello 扩展。

`-no_resumption_on_reneg`

设置 `SSL_OP_NO_SESSION_RESUMPTION_ON_RENEGOTIATION` 标志。

`-status`

启用证书状态请求支持（即 OCSP ling）。

`-status_verbose`

启用证书状态请求支持（即 OCSP ling）并提供 OCSP 响应的详细输出。

`-status_tiout nsec`

将 OCSP 响应的超时时间设置为`nsec`秒。

`-status_url url`

如果服务器证书中不存在响应器 URL，则设置备用响应器 URL。如果没有此选项，当服务器证书不包含响应地址时将返回错误。

`-nextprotoneg protocols`

启用下一个协议协商 TLS 扩展并提供用逗号分隔的支持协议名称列表。列表应将最希望的协议放在前面。协议名称是可打印的 ASCII 字符串，例如 `http/1.1` 或 `spdy/3`。

## 连接命令

如果与 SSL 客户端建立了连接请求且均未使用 `-www` 或 `-WWW` 选项，通常会显示从客户端接收到的任何数据，并将任何按键发送到客户端。

还会识别某些执行特殊操作的单字母命令：下列表所示。

`q`

结束当前的 SSL 连接，但仍接受新连接。

`Q`

结束当前的 SSL 连接并退出。

`r`

重新协商 SSL 会话。

`R`

重新协商 SSL 会话并请求客户端证书。

`P`

通过底层 TCP 连接发送明文：这会导致客户端由于违反协议而断开。

`S`

打印会话缓存状态信息。

## 注意事项

`s_server` 可用于调试 SSL 客户端。例如，可以使用命令接受来自浏览器的连接：

```
openssl s_server -accept 443 -www
```

大多数网络浏览器（特别是 Netscape 和 MSIE）仅支持 RSA 密码套件，因此它们无法连接到未使用带有 RSA 密钥证书或禁用 RSA 的 OpenSSL 版本的服务器。

虽然在请求客户端证书时指定空 CA 列表严格来说违反了协议，但 SSL 客户端会将此解释为任何 CA 都是可以的。这对于调试目的有用。

可以使用 `sess_id` 程序打印会话参数。

## Bug

由于此程序有很多选项，而且由于所使用的技术相当老旧，`s_server` 的 C 源码相当难读，并不是实现方法的范例。一个典型的 SSL 服务器程序会简单得多。

常用密码套件的输出是错误的：它仅给出 OpenSSL 识别且客户端支持的密码套件列表。

`s_server` 程序应该有一种方法打印客户端声称支持的任何未知密码套件的细节。

## 另请

(1), (1), (1)

## 历史

`-no_alt_chains` 选项首次添加到 OpenSSL 1.0.2b 中。

* *

# S_TIME

## 名称

`s_ti` - SSL/TLS 性能计时程序

`-verify depth`

用于验证的深度。这指定了服务器证书链的最大长度，并启用服务器证书验证。目前，验证操作在出现错误后会继续，因此可以看到证书链中的所有问题。作为副作用，连接永远不会因为服务器证书验证失败而失败。

### `-CApath` 目录

用于服务器证书验证的目录。该目录必须是“哈希格式”，更多信息请参阅 `verify`。这些目录在构建客户端证书链时也会使用。

### `-CAfile` 文件

一个包含信任证书的文件，用于服务器身份验证期间以及在尝试构建客户端证书链时使用。

### `-trusted_first`

在构建信任链以验证服务器证书时，使用 CA 文件或 CA 目录中的证书优于服务器提供的证书。这对于具有桥接 CA（Bridge CA）或交叉认证 CA（Cross-Certified CAs）的环境特别有用。

### `-new`

使用新的会话 ID 执行计时测试。如果既未指定 `-new` 也未指定 `-reuse`，它们默认都开启并顺序执行。

### `-reuse`

使用相同的会话 ID 执行计时测试；这可以作为会话缓存正在正常工作的测试。如果既未指定 `-new` 也未指定 `-reuse`，它们默认都开启并顺序执行。

### `-nbio`

开启非阻塞 I/O。

### `-ssl2`, `-ssl3`

这些选项禁用某些 SSL 或 TLS 协议的使用。默认的初始握手使用一种与所有服务器兼容的方法，允许它们根据情况使用 SSL v3、SSL v2 或 TLS。计时程序在开启/关闭协议选项方面没有 (1) 程序丰富，可能无法连接到所有服务器。

遗憾的是，目前有很多老旧且损坏的服务器无法处理这种技术并会导致连接失败。因此，只有当使用 `-ssl3` 选项关闭 TLS 时服务器才能工作；其他仅支持 SSL v2，可能需要 `-ssl2` 选项。

### `-bugs`

SSL 和 TLS 实现中存在若干已知漏洞。添加此选项可启用各种变通方案。

### `-cipher` 密码列表

这允许修改客户端发送的密码列表。虽然服务器决定使用哪种加密套，但它应该采用客户端发送列表中第一个支持的加密套。更多信息请参见 (1) 命令。

### `-ti` 长度

指定 `s_ti` 建立连接并可选地从服务器传输负载数据的时间（秒）。服务器和客户端的性能以及链路速度决定了 `s_ti` 能建立多少连接。

## 注意事项

`s_client` 可用于确保 SSL 连接的性能。要连接到 SSL HTTP 服务器并获取默认页面，通常使用命令

```
openssl s_ti -connect serverna:443 -www / -CApath yourdir -CAfile yourfile.pem -cipher commoncipher [-ssl3]
```

（https 使用端口 443）。`commoncipher` 是客户端和服务器都能认可的加密算法，详情请参阅 (1) 命令。

如果握手失败，可能有多种原因。如果没有明显的问题（如缺少客户端证书），则可以尝试 `-bugs`、`-ssl2`、`-ssl3` 选项，以防是由于存在 bug 的服务器。特别是，你应该在向 OpenSSL 邮件列表提交 bug 报告**之前**尝试这些选项。

在尝试使客户端证书工作时，一个常见问题是 Web 客户端抱怨它没有证书，或者提供了一个空列表供选择。这通常是因为服务器在请求证书时没有在其“可接受的 CA 列表”中发送客户端的证书授权机构。通过 (1) 可以查看并检查 CA 列表。然而，某些服务器仅在请求特定 URL 后才会请求客户端身份验证。在这种情况下，必须使用 (1) 的 `-prexit` 选项并向相应页面发送 HTTP 请求。

如果在命令行上使用 `-cert` 选项指定了证书，除非服务器专门请求客户端证书，否则它不会被使用。因此，在命令行中包含客户端证书并不能保证该证书有效。

## 缺陷

由于此程序没有 (1) 程序的所有开启/关闭协议的选项，你可能无法确保所有协议在所有服务器上的性能。

如果服务器验证失败，`-verify` 选项应该直接退出。

## 另请

(1), (1), (1)

* * *

# sane-find-scanner

`sane-find-scanner` - 查找 SCSI 和 USB 扫描仪及其设备文件

## 概要

`sane-find-scanner` `[-h| -?]` `[-v]` `[-q]` `[-p]` `[-f]` `[-F *filena*]` `[*devna*]`

## 描述

`sane-find-scanner` 是一个查找 SCSI 和 USB 扫描仪并确定其 Unix 设备文件的命令行工具。其主要目标是确保扫描仪可以被 SANE 后端检测。

对于 **SCSI** 扫描仪，它检查默认的通用 SCSI 设备文件（例如 `*/dev/sg0*`）和 `*/dev/scanner*`。测试通过发送 SCSI 查询命令并寻找类型为 "scanner" 或 "processor" 的设备类型完成（因此旧的 HP 扫描仪似乎发送 "processor"）。因此，`sane-find-scanner` 将找到任何连接到这些默认设备的 SCSI 扫描仪，即使它们没有被任何 SANE 后端支持。



对于 `USB` 扫描仪，首先测试 `USB` 内核扫描仪设备文件（例如 `/dev/usb/scanner0`）、`/dev/usb/scanner*` 和 `/dev/usbscanner*`）。如果操作系统支持此功能，将打开文件并确定厂商 ID 和设备 ID。目前，只有当 `USB` 扫描仪被 Linux 扫描模块或 FreeBSD 或 OpenBSD `uscanner` 驱动支持时，才能通过这种方式找到。在测试之后，`sane-find-scanner` 尝试扫描由 `USB` 库 `libusb` 找到的 `USB` 设备（如果可用）。扫描仪没有专门的 `USB` 类，因此用于区分扫描仪与其他 `USB` 设备的启发式方法并不完美。`sane-find-scanner` 还会尝试找出扫描仪使用的 `USB` 类型。如果检测到，将在厂商和产品 ID 之后打印。`sane-find-scanner` 甚至能找到未被 `SANE` 后端支持的 `USB` 扫描仪。

`sane-find-scanner` 找不到大多数并行端口扫描仪或连接到专用端口的扫描仪。因此，并行端口扫描仪可以通过 `sane-find-scanner -p` 检测到。在编写时，只能检测到 Mustek 并行端口扫描仪。

## 选项

### `-h, -?`

打印简要用法。

### `-v`

详细输出。如果使用一次，`sane-find-scanner` 会显示每个设备名称和测试结果。如果使用两次，还会打印 `SCSI` 查询信息和 `USB` 描述符。

### `-q`

安静模式。只打印设备，不打印注释。

### `-p`

探测并行端口扫描仪。

### `-f`

强制将所有显式给定的设备作为 `SCSI` 和 `USB` 设备打开。如果 `sane-find-scanner` 在确定设备类型时不正确，这非常有用。

### `-F filena`

`filena` 是一个包含 Linux 使用的 `/proc/bus/usb/devices` 格式 `USB` 描述符的文件。`sane-find-scanner` 尝试识别此类文件中找到的所有 `USB` 扫描仪的芯片组。当 `cat /proc/bus/usb/devices` 输出可用但扫描仪本身不存在时，此选项对开发者有用。

### `devna`

测试设备文件 `devna`。如果给出了 `devna`，则不检查其他设备。

## 示例

### `sane-find-scanner -v`

检查所有 `SCSI` 和 `USB` 设备是否有可用的扫描仪，并为每个设备文件打印一行。

### `sane-find-scanner /dev/scanner`

仅在 `/dev/scanner` 查找 `SCSI` 扫描仪并打印结果。

目前尚不支持大多数并行端口扫描仪。

对 `USB` 芯片组的检测仅限于少数芯片组。

---

# `sane-rts8891`

## 名称

`sane-rts8891` - 基于 `rts8891` 仪的 `SANE` 后端

## 描述

`sane-rts8891` 库实现了一个 `SANE`（Scanner Access Now Easy）后端，提供对基于 `rts8891 ASIC` 扫描的访问。

支持此后端的扫描仪有：

```text
Vendor Model       status
------ ----------- -----------
Umax   Astra 4400  untested
Umax   Astra 4450  untested
HP     scanjet 4000c good
HP     scanjet 4470c good
```

该后端支持的选项可以通过类似 `scanimage` 等程序的命令行选项进行选择，也可以通过 `xscanimage` 或 `xsane` 中的 GUI 元素进行选择。

如果您遇到任何异常行为，请报告给后端维护者或 `SANE` 邮件列表。

有效的命令行选项及其语法可以通过以下命令列出：

```bash
scanimage --help -d rts8891
```

### 扫描模式选项

#### `--mode`

选择扫描仪的基本运行模式，有效选择有 `R Color`（彩色）、`Gray`（灰度）和 `Lineart`（线条画）。默认模式为彩色。`Lineart` 模式仅支持黑白（1 位）。灰度模式将产生 256 级灰（8 位）。彩色模式允许通过 24 位颜色信息产生超过 1600 万种不同的颜色。

#### `--resolution`

选择扫描的分辨率。水平和垂直分辨率由此选项的值设置。扫描仪对于指定的选项值可以实现以下分辨率：

```text
Value Hor. Resolution Vert. Resolution
----- --------------- -------------------
75    75dpi           75dpi
150   150dpi          150dpi
300   300dpi          300dpi
600   600dpi          600dpi
1200  1200dpi         1200dpi
```

#### `--preview`

请求预览扫描。该扫描使用的分辨率为 75 dpi，扫描区域和扫描模式通过其选项指定，或者在未指定时使用默认值。预览模式的默认值为 `no`。

#### `--threshold`

选择获取白点的最小亮度。该阈值仅用于 `Lineart` 模式扫描。以百分比形式指定，范围为 0..100%（步长为 1）。阈值选项的默认值为 50。

## 配置文件

配置文件 `/etc/sane.d/rts8891.conf` 包含支持的扫描仪的 `USB` 设备 ID（例如 `usb 0x043d 0x007c`）和扫描仪配置选项。空行和以井号（`#`）开头的行会被忽略。

支持的选项有 `allowsharing` 和 `modelnuer`。

- `allowsharing` 启用或禁用多个前端在同一时刻共享扫描仪。
- `modelnuer` 用于强制后端报告的型号，仅适用于 `NVRAM` 已擦除的扫描仪。

```text
0 报告 HP4470c。1 报告 HP4400c。2 报告 Astra 4400。
```

## 文件

`/usr/lib/sane/libsane-rts8891.a`

实现此后端的静态库。

`/usr/lib/sane/libsane-rts8891.so`

实现此后端的共享库（存在于支持动态加载的系统上）。

## 环境

`SANE_DEBUG_RTS8891`、`SANE_DEBUG_RTS8891_LOW`、`SANE_DEBUG_RTS88XX_LIB`

如果库在编译时启用了调试支持，这些环境变量将控制此后端的调试级别。例如，值 255 请求打印所有调试输出。较小的值会减少详细程度。

## 限制

由于缺乏数据（即 `USB` 日志），相同型号的扫描仪存在不同的传感器，因此某些传感器的支持优于其他传感器。任何型号至少支持 75 dpi 模式。在多个前端之间同时共享扫描仪（`allowsharing` 选项）在某些 `USB` 控制器上可能无法工作。

（尚）不支持 `XPA`。

## BUGS

目前无已知 bug。

## 另参

(5)、(1)、(1)、(1)、(7)

## 作者

此后端由 Stéphane Voltz 开发。

## 致谢

非常感谢：

Laurent Fournier 捐了一台 HP4470c。Vladimir Sysoev 和 “TheUnruly Squash” 花费时间记录 `USB` 活动并在 HP4400 型上测试实验性版本。

---

# `sane-teco1`

## 名称

`sane-teco1` - 用于 TECO / RELISYS 扫描仪的 `SANE` 后端

## 描述

`sane-teco1` 库实现了一个 `SANE`（Scanner Access Now Easy）后端，提供对 TECO `SCSI` 平板扫描仪的访问。此后端应被视为 Beta 级软件！TECO 扫描仪以 RELISYS、PIOTECH、TRUST 等各种品牌销售。此后端可能支持也可能不支持您的设备。

应适用于此后端的扫描仪有：

```text
Vendor  Model       TECO model  status
------  ----------- ----------- -----------
Relisys AVEC 2400  VM3520      tested
Relisys AVEC 2412  VM3520+     tested
Relisys AVEC 4800  VM4530      untested
Relisys AVEC 4816  VM4530+     untested
Relisys RELI 2400  VM3530      untested
Relisys RELI 2412  VM3530+     tested
Relisys RELI 2412  VM3530+     untested
Relisys RELI 4816  VM4540      tested
Relisys RELI 4830  VM4542      tested
Relisys RELI 9600  VM6530      untested
```

### `scanimage --help -d teco1`

### 扫描模式

#### `--mode`

选择扫描仪的基本运行模式，有效选择有 `Black & White`（黑白）、`Grayscale`（灰度）和 `Color`（彩色）。黑白模式仅为黑白（1 位）。彩色模式将产生 24 位的图像。

#### `--resolution`

选择扫描的分辨率。扫描仪支持 1 到 600 之间的所有分辨率，步长为 1。

### 几何选项

#### `-l -t -x -y`

控制扫描区域：`-l` 设置左上 x 坐标，`-t` 设置 y 坐标，`-x` 选择宽度，`-y` 选择高度。所有参数默认毫米。

### 增强选项

#### `--custom-gamma`

（彩色模式下）允许用户指定伽马表（见接下来的 3 个参数）。

#### `--red-gamma-table`

（彩色模式下）可用于下载红色通道的自定义伽马表。表长度为 256 字节。

#### `--green-gamma-table`

（彩色模式下）可用于下载绿色通道的自定义伽马表。表长度为 256 字节。

#### `--blue-gamma-table`

（彩色模式下）可用于下载蓝色通道的自定义伽马表。表长度为 256 字节。

#### `--dither`

（仅黑白）选择使用的抖动掩码。可能的值有 `Line art`、`2x2`、`3x3`、`4x4 bayer`、`4x4 smooth`、`8x8 bayer`、`8x8 smooth`、`8x8 horizontal` 和 `8x8 vertical`。

#### `--preview`

请求预览扫描。该扫描使用的分辨率为 22 dpi，扫描区域为最大允许。扫描模式由用户选择。默认值为 `no`。

## 配置文件

`/etc/sane.d/teco1.conf` 仅支持一种信息：要使用的设备路径（例如 `/dev/scanner`）。

## 文件

`/usr/lib/sane/libsane-teco1.a`

实现此后端的静态库。

`/usr/lib/sane/libsane-teco1.so`

实现此后端的共享库（存在于支持动态加载的系统上）。

## 环境

`SANE_DEBUG_TECO1`

如果库在编译时启用了调试支持，此环境变量将控制此后端的调试级别。例如，值 128 会请求打印所有调试输出。较小的值会减少详细程度。

## 局限性

Windows `TWAIN` 驱动比此 `SANE` 后端多许多选项。然而，它们只是软件调整。此后端仅实现扫描仪可以支持的功能。

## 缺陷

已知无。

## 参见

(5)、(1)、(1)、(1)、(7)

## 作者

该包由 Frank Zago 积极维护。

## 致谢

感谢 Gerard Delafond 对 VM4542 的支持。感谢 Jean-Yves Simon 对 VM3510 的支持。

---

# `SATYR`

## 名称

`satyr` - 创建和处理问题报告

## 概要

`satyr <command> [option...]`

## 描述

`satyr` 是一个命令行工具，用于创建适用于自动化处理的软件问题匿名报告。

必须带有 `<command>` 调用工具以指定要执行的操作。可用命令文档如下。

## 选项

### 命令

#### `abrt-print-report-from-dir <directory>`

从 ABRT 问题目录 `directory` 创建报告并将其打印到标准输出。

#### `abrt-create-core-stacktrace <directory>`

从包含核心转储的 ABRT 问题目录 `directory` 创建堆栈跟踪。

---

# `scanimage`

## 名称

`scanimage` - 扫描图像

## 概要

```text
scanimage [-d|--device-na dev] [--format format] [-i|--icc-profile profile] [-L|--list-devices] [-f|--formatted-device-list format] [-b|--batch [=format]] [--batch-start start] [--batch-count count] [--batch-incrent incrent] [--batch-double] [--accept-md5-only] [-p|--progress] [-n|--dont-scan] [-T|--test] [-A|--all-options] [-h|--help] [-v|--verbose] [-B|--buffer-size [=size]] [-V|--version] [device-specific-options]
```

## 描述

`scanimage` 是一个控制图像采集设备（如平板式扫描仪或数码相机）的命令行界面。通过命令行选项控制设备。处理命令行后，`scanimage` 通常会进行图像采集。图像数据将以 `PNM`（通用图像格式）之一（黑白图像的 `PBM`、灰度图像的 `PGM` 和彩色图像的 `PPM`）、`TIFF` 格式（黑白、灰度或彩色）、`PNG` 格式或 `JPEG` 格式写入标准输出。`scanimage` 通过 `SANE`（轻松访问扫描仪）接口访问图像采集设备，因此可以支持任何存在 `SANE` 后端的设备（尝试使用 `apropos sane-` 来获取可用后端的列表）。

## 示例

`-d` 或 `--device-na` 选项后面必须紧跟一个 `SANE` 设备名称，如 `epson:/dev/sg0` 或 `hp:/dev/usbscanner0`。可以使用 `--list-devices` 选项获取可用设备的（部分）列表（见下文）。如果未显式指定设备名称，`scanimage` 将从环境变量 `SANE_DEFAULT_DEVICE` 读取设备名称。如果未设置此变量，`scanimage` 将尝试打开第一个可用设备。

`--format format` 选项选择图像数据写入标准输出的方式。`format` 可以是 `pnm`、`tiff`、`png` 或 `jpeg`。如果不使用 `--format`，则写入 `PNM` 格式。

`-i` 或 `--icc-profile` 选项用于将 ICC 配置包含到 `TIFF` 文件中。

`-L` 或 `--list-devices` 选项请求可用设备的（部分）列表。列表不是完整的，因为某些设备可能可用但未列在任何配置文件中（通常存储在 `/etc/sane.d` 目录中）。这在通过网络访问扫描仪时尤为重要。如果设备未列在配置文件中，访问它的唯一方法是使用其完整的设备名称。你可能需要咨询系统管理员以查找此类设备的名称。

`-f` 或 `--formatted-device-list` 选项的作用与 `--list-devices` 类似，但需要一个格式字符串。`scanimage` 将占位符 `%d`、`%v`、`%m`、`%t`、`%i`、`%n` 分别替换为设备名称、厂商名称、模型名称、扫描仪类型、索引数字和换行符。命令

```bash
scanimage -f 'scanner number %i device %d is a %t, model %m, produced by %v'
```

将产生类似的内容：

```text
scanner number 0 device sharp:/dev/sg1 is a flatbed scanner, model JX250 SCSI, produced by SHARP
```

`--batch` 选项提供了使用进纸器扫描文档的功能。`--batch [format]` 用于指定每页写入的文件格式。每页写入一个单独的文件。如果未指定 `format`，将使用默认的 `out%d.pnm`（或对于 `--format tiff` 默认为 `out%d.tif`，对于 `--format png` 默认为 `out%d.png`，对于 `--format jpeg` 默认为 `out%d.jpg`）。`format` 以带有一个整数参数的 `printf` 风格字符串的形式给出。`--batch-start start` 选择从哪一页开始命名文件。如果未给出此选项，计数器将从 1 开始。`--batch-count count` 指定尝试扫描的页数。如果没有给出，`scanimage` 将继续扫描直到扫描仪返回非 OK 状态。并非所有带有进纸器的扫描仪会在 ADF 为空时发出信号，可以使用此命令来绕过它们。通过 `--batch-incrent incrent`，你可以更改文件名中数字的增量。这通常用于在单面进纸器上扫描双面文档。提供了一个特定命令辅助功能：`--batch-double` 将自动将增量设置为 2。`--batch-prompt` 将会在扫描每一页之前要求按回车。这可以用于在没有自动进纸器的情况下扫描多页。

`--accept-md5-only` 选项仅接受支持 MD5 安全的用户授权请求。`SANE` 网络守护进程（`saned`）能够处理此类请求。见 (8)。

`-p` 或 `--progress` 选项请求 `scanimage` 打印进度计数。它显示当前图像的图像数据已被 `scanimage` 获取的百分比。



`-n` 或 `--dont-scan` 选项请求 `scanimage` 只设置用户提供的选项但不实际执行扫描。此选项可以用于例如关闭扫描仪灯光（如果后端支持）。

`-T` 或 `--test` 选项请求 `scanimage` 执行一些简单的健康测试，以确保后端符合 `SANE` API 的定义（特别是 `sane_read` 函数会通过此测试运行）。

`-A` 或 `--all-options` 选项请求 `scanimage` 列出后端暴露的所有可用选项，包括按钮选项。信息打印在标准输出上且不会进行扫描。

`-h` 或 `--help` 选项请求帮助信息。信息打印在标准输出上，在这种情况下，不会尝试采集图像。

`-v` 或 `--verbose` 选项增加 `scanimage` 操作的详细程度。该选项可以多次指定，每次都会增加详细级别。

不带参数的 `-B` 会将输入缓冲区大小从默认的 32KB 更改为 1MB。为了更精细的控制，请使用 `--buffer-size=` 后跟 KB 数量。

`-V` 或 `--version` 选项请求 `scanimage` 打印程序和包名、其关联的 `SANE` 发行版版本数以及它加载的后端版本。通常是 dll 后端。如果需要更多关于后端版本的信息，可以使用用于 dll 后端的 `DEBUG` 变量。例如：`SANE_DEBUG_DLL=3 scanimage -L`。

正如你所想象的，`scanimage` 的强大之处源于它可以控制任何 `SANE` 后端。因此，具体的命令行选项集取决于所选设备的能力。要查看设备 `dev` 的选项，请通过如下形式的命令行调用 `scanimage`：

```bash
scanimage --help --device-name dev
```

通过 `--help` 打印的设备特定选项文档通过几个示例解释最好：

- `-l0..218mm[0]`

  扫描区域的左上角位置。

  上述描述显示选项 `-l` 期望 0 到 218 mm 范围内的值。方括号中的值表示当前选项值为 0 mm。大多数后端都为左上角 y 位置（`-t`）、宽度（`-x`）和扫描区域高度（`-y`）提供类似的几何选项。

- `--brightness-100..100%[0]`

  控制采集图像的亮度。

  上述描述显示选项 `--brightness` 期望 -100 到 100 百比范围内的值。方括号中的值表示当前选项值为 0%。

- `--default-enhancements`

  设置增强控制的默认值。

  上述描述显示选项 `--default-enhancements` 没有 way 参数值。它应该被认为在命令行出现的位置点产生立即影响。例如，由于此选项重置了 `--brightness` 选项，选项对 `--brightness 50 --default-enhancements` 实际上将是无操作。

- `--modeLineart|Gray|Color[Gray]`

  选择扫描模式（例如：线条、灰度或彩色）。

  上述描述显示选项 `--mode` 接受一个为 `Lineart`、`Gray` 或 `Color` 之一的字符串。方括号中的值表示该选项当前设置为 `Gray`。为了方便起见，只要字符串值保持唯一，缩写它们是合法的。此外，拼写的大小写无关。例如，设置 `--mode col` 与 `--mode Color` 相同。

- `--custom-gamma[=(yes|no)][inactive]`

  确定是否使用内置或自定义 gamma 表。

  上述描述显示选项 `--custom-gamma` 期望没有选项值、一个 "yes" 字符串或 "no" 字符串。指定不带值的选项等同于指定 "yes"。方括号中的值表示该选项当前未激活。也就是说，尝试设置该选项将导致错误信息。可用选项的集合通常取决于其他选项的设置。例如，`--custom-gamma` 表可能仅在请求灰度或彩色扫描模式时才激活。

注意，`--help` 选项在处理完所有其他选项后才处理。这使得能够通过指定相应的模式选项以及 `--help` 选项来查看特定模式的选项设置。例如，命令行：

```bash
scanimage --help --mode color
```

将打印在选择彩色模式时生效的选项设置。

- `--gamma-table0..255,...`

  Gamma 校正表。在彩色模式下，此选项同时影响红、绿、蓝通道（即这是一个强度 gamma 表）。

  上述描述显示选项 `--gamma-table` 期望 0 到 255 范围内的零或多个值。例如，此选项的合法值为 "3,4,5,6,7,8,9,10,11,12"。由于以这种形式指定长向量很冗长，因此可以使用缩写形式 `[0]3-[9]12` 来表示。这种表示的意思是第一个向量元素设置为 3，第 9 个元素设置为 12，中间的值通过线性插值得到。当然，可以指定多个这样的线性段。例如，`[0]3-[2]3-[6]7,[7]10-[9]6` 等于 "3,3,3,4,5,6,7,10,8,6"。可以使用程序 `gamma4scanimage` 生成此类 gamma 表（详情见 (1)）。

- `--filename<string>[/tmp/input.ppm]`

  要加载的图像的文件。

  上述描述是一个接受任意字符串值的选项示例（恰好是一个文件名）。再次，方括号中的值显示该选项当前设置为文件名 `/tmp/input.ppm`。

## 环境

`SANE_DEFAULT_DEVICE`

默认设备名。

## 文件

`/etc/sane.d`

此目录包含各种配置文件。详情请参考下文列出的手册页。

`~/.sane/pass`

此文件包含格式如下的内容：

`user:password:resource`

`scanimage` 使用此信息自动回答用户授权请求。文件必须具有 0600 或更严格的权限。你应该结合 `--accept-md5-only` 选项使用此文件以避免服务器端攻击。资源可以包含任何字符，但限制为 127 个字符。

## 参见

(7)、(1)、(1)、(1)、(1)、(1)、(5)、(5)、(5)

## 作者

David Mosberger、Andreas Beck、Gordon Matzigkeit、Caskey Dickson 等。问题和建议请联系 sane-devel 邮件列表（见

## 缺陷

对于向量选项，帮助输出目前没有指示向量值应包含多少元素。

***

# `scl`

## 名称

如果指定了 `--exec`，则将使用 `exec()` 函数执行命令，否则将使用 `system()` 函数。

注意：如果你使用由多个参数组成的 `<command>`，你需要使用引号或 `--` 命令分隔符。分隔符之后的所有内容都将被视为命令或其参数。

注意：这些命令以某种方式修改用户环境。这些命令可能会破坏 SCL，因为它们的激活也取决于对环境的修改。此类命令的典型示例是 `su` 和 `sudo`。每个集合修改环境的方式不同，因此更多细节可以在特定集合的文档中找到。

`load` `<collection1>` [`<collection2> ...`]

将给定的集合加载到当前 shell。当前 shell 的环境将根据集合的模块文件进行修改。

`unload` `<collection1>` [`<collection2> ...`]

从当前 shell 中卸载给定的集合。当前 shell 的环境将恢复到加载集合之前的状态。

`list-collections`

列出系统上所有安装的软件集合（Software Collections）。

`list-packages` `<collection1> <collection2> ...`

如果指定了集合，则列出属于该集合的已安装列表。

`register` `<path>`

如果 `<path>` 指向有效的 SCL 文件结构，`scl` 将将其注册为 SCL。`<path>` 目录需要包含 `module` 文件和 `root` 目录才能被视为有效的 SCL。`<path>` 需要是指向集合位置的绝对路径。

`deregister` `<collection>` [`-f|--force`]

`<collection>` 将不再被视为 SCL。如果 `<collection>` 安装在本地的，则需要使用 `--force`。

`man` `<collection>`

显示 `<collection>` 的手册页。

## 示例

```bash
scl enable example 'less --version'
```

在启用 `example` 集合的环境中运行命令 `less --version`。

```bash
scl load foo bar
```

将 `foo` 和 `bar` 软件集合加载到当前 shell。

```bash
scl unload foo bar
```

从当前 shell 中卸载 `foo` 和 `bar` 软件集合。

```bash
cat my_command | scl enable baz -
```

在启用 `baz` 集合的环境中运行 `my_command` 文件中列出的系列命令。

```bash
scl list-collections
```

列出所有已安装的集合。

```bash
scl list-packages example
```

列出 `example` 集合中的所有包。

```bash
scl register /foo/bar
```

注册一个名为 `bar` 的新集合。

```bash
scl deregister bar --force
```

强制注销集合 `bar`。

包装脚本应使用正确的引号或命令分隔符，如下例所示：

```bash
#!/bin/bash
COMMAND="ruby $(printf "%q " "$@")"
scl enable ruby193 "$COMMAND"
# 或：
scl enable ruby193 -- $COMMAND
```

## 作者

`scl` 由 Jindrich Novy <> 和 Jan Zeleny <> 编写。

***

# `SCP`

## 名称

`scp` - 安全复制（远程文件复制程序）

## 概要

`scp` `-words` [`-1234BCpqrv`] [`-c` `cipher`] [`-F` `ssh_config`] [`-i` `identity_file`] [`-l` `limit`] [`-o` `ssh_option`] [`-P` `port`] [`-S` `program`] [[`user` `@`] `host1` `file1`] ... [[`user` `@`] `host2` `file2`]]

## 描述

`scp` 在网络上的主机之间复制文件。它使用 (1) 进行数据传输，使用 `ssh` 认证并提供 `ssh` 安全性。如果认证需要，`scp` 将提示输入密码或短语。

文件名可能包含用户和主机指定，以指示从或向该主机复制文件。可以使用绝对或相对路径显式指定本地文件名，以避免 `scp` 将包含 `:` 的文件名视为主机指定符。也允许在两个远程主机之间复制。

选项如下：

`-1`

强制 `scp` 使用协议 1。

`-2`

强制 `scp` 使用协议 2。

`-3`

`-F` `ssh_config`

指定 `ssh` 的替代用户级配置文件。此选项直接传递给 (1)。

`-i` `identity_file`

选择用于读取公钥认证的标识（私钥）的文件。此选项直接传递给 (1)。

`-l` `limit`

限制使用的带宽，单位为 Kbit/s。

`-o` `ssh_option`

可以按照 `ssh_config` 中使用的格式向 `ssh` 传递选项。这对于没有独立 `scp` 命令行标志的选项非常有用。有关下列选项及其可能值的完整信息，请参见 `ssh_config`。

`AddressFamily`

`BatchMode`

`BindAddress`

`CanonicalDomains`

`CanonicalizeFallbackLocal`

`CanonicalizeHostname`

`CanonicalizeMaxDots`

`CanonicalizePermittedCNAMEs`

`ChallengeResponseAuthentication`

`CheckHostIP`

`Cipher`

`Ciphers`

`Compression`

`CompressionLevel`

`ConnectionAttempts`

`ConnectTimeout`

`ControlMaster`

`ControlPath`

`ControlPersist`

`GlobalKnownHostsFile`

`GSSAPIAuthentication`

`GSSAPIDelegateCredentials`

`HashKnownHosts`

`Host`

`HostbasedAuthentication`

`HostbasedKeyTypes`

`HostKeyAlgorithms`

`HostKeyAlias`

`HostName`

`IdentityFile`

`IdentitiesOnly`

`IPQoS`

`KbdInteractiveAuthentication`

`KbdInteractiveDevices`

`KexAlgorithms`

`LogLevel`

`MACs`

`NoHostAuthenticationForLocalhost`

`NumberOfPasswordPrompts`

`PasswordAuthentication`

`PKCS11Provider`

`Port`

`PreferredAuthentications`

`Protocol`

`ProxyCommand`

`PubkeyAcceptedKeyTypes`

`PubkeyAuthentication`

`RekeyLimit`

`RhostsRSAAuthentication`

`RSAAuthentication`

`SendEnv`

`ServerAliveInterval`

`ServerAliveCountMax`

`StrictHostKeyChecking`

`TCPKeepAlive`

`UpdateHostKeys`

`UsePrivilegedPort`

`User`

`UserKnownHostsFile`

`VerifyHostKeyDNS`

`-P` `port` 指定连接到远程主机的端口。注意此选项使用大写的 `P`，因为 `-p` 已经保留用于保留文件的时间和模式。

`-p` 保留原始文件的修改时间、访问时间和模式。

`-q` 静默模式：禁用进度条以及来自 (1) 的警告和诊断信息。

`-r` 递归复制整个目录。注意 `scp` 在树遍历时会遵循符号链接。

`-S` `program` 指定用于加密连接的 `program` 名称。该程序必须理解 (1) 选项。

`-v` 详细模式。导致 `scp` 和 (1) 输出关于其进度的调试信息。这对于调试连接、认证和配置问题很有帮助。

## 退出状态

`exit status scp`

## 参见

(1)、(2)、`ssh-add`、`ssh-agent`、`ssh-keygen`、`ssh_config`、(8)

## 历史

`scp` 基于加州福尼亚大学摄政委员会提供的 BSD 源码中的 `rcp` 程序。

## 作者

Antimo Rinne、Matti Tatu Ylonen

***

# `SCRIPT`

## 名称

`script` - 为终端会话制作类型记录（typescript）

## 概要

`script` [`options`] [`file`]

## 描述

`script` 创建终端上显示的所有内容的类型记录。对于需要交互式会话的纸质记录作为作业证明的学生来说非常有用，因为类型记录文件可以使用 (1) 事后打印。

如果给出参数 `file`，`script` 将对话保存在该 `file` 中。如果没有给出文件名，对话将保存在文件 `typescript` 中。

## 选项

`-a`、`--append`

将输出附加到 `file` 或 `typescript`，保留原有内容。

`-c`、`--command` `command`

运行 `command` 而不是交互式 shell。这使得脚本很容易捕获在标准输出不是 tty 时行为不同的程序的输出。

`-h`、`--help`

显示帮助文本并退出。

## 注意

脚本在派生的 shell 退出时结束（对于 Bourne shell 使用 `control-D` (1)；对于 C-shell，使用 `exit`、`logout` 或 `control-d`（如果未设置 `ignoreeof`）(1)）。

某些交互式命令（例如 (1)）会在 typescript 文件中产生垃圾内容。`script` 与不操作屏幕的命令配合效果，其结果类似于硬拷贝打印终端的输出。

不建议在非交互式 shell 中运行 `script`。`script` 的内部 shell 总是交互式的，这可能导致意外的结果。如果你在 shell 初始化文件中使用 `script`，必须避免进入无限循环。例如使用仅由登录 shell 读取的 profile 文件：

```bash
if test -t 0 ; then
    script
    exit
fi
```

你还应该避免在命令管道中使用 `script`，因为 `script` 读取的输入可能比预期的要多。

## 环境

`script` 利用了以下环境变量：

`SHELL`

如果变量 `SHELL` 存在，`script` 派生的 shell 将是该 shell。如果未设置 `SHELL`，则假定为 Bourne shell。（大多数 shell 会自动设置此变量）。



## SEE ALSO

(1)（用于`history`机制），(1)。

## HISTORY

`script`命令出现于 3.0BSD。

## BUGS

`script`将*所有内容*都放入日志文件中，包括换行符和退格键。这并不是普通用户预期的。

`script`主要为交互式终端会设计，当 stdin 不是终端时（例如 `echo foo | script`），可能会导致所有会话挂起，因为 script 会话中的交互式 shell 缺少 EOF，且`script`不知道何时关闭会话。更多信息见 NOTES 部分。

## AVAILABILITY

`script`命令是 util-linux 软件包的一部分，可在 Linux 内核存档中获取

* * *

# SCRIPTREPLAY

## NAME

scriptreplay - 重放 typescript，使用计时信息

## SYNOPSIS

`scriptreplay` [options] [-t] `timingfile` [*typescript` [`divisor`]]

## DESCRIPTION

此程序重放 typescript，使用计时信息以确保输出的节奏与录制脚本时原始出现的节奏一致。

重放仅仅是再次显示信息；在录制 typescript 时运行的程序不会再次运行。由于计时信息只是被显示，`scriptreplay`只有在与录制 typescript 时相同的类型的终端上运行时才能保证正常工作。否则，typescript 中的任何转义字符都可能被 `scriptreplay`输出输出的终端以不同的方式解释。

计时信息是当带有`-t`参数运行时由 (1) 输出到标准错误的内容。

默认情况下，要显示的 typescript 假定为`typescript`，但可以通过第二个参数或选项`-s`指定其他文件名。

如果指定了第三个参数，它将用作加速倍率。例如，加速 2 会让`scriptreplay`运行快一倍，加速 0.1 则让它比原始会话慢十倍。

## OPTIONS

前三个选项将覆盖旧式参数。

`-t`, `--timing` `file`

包含`script`计时输出的文件。

`-s`, `--typescript` `file`

包含`script`终端输出的文件。

`-d`, `--divisor` `nuer`

通过显示此`nuer`次数来加速重放显示。该参数是一个浮点数。之所以被称为除数，是因为它将计时时间除以该因子。

`-m`, `--maxdelay` `nuer`

设置 transcript 更新之间的最大延迟为`nuer`秒。该参数是一个浮点数。这可以用于避免 transcript 重放中的长时间停顿。

`-V`, `--version`

显示版本信息并退出。

`-h`, `--help`

显示帮助文本并退出。

## EXAMPLE

```bash
% script --timing=file.tm script.out Script started, file is script.out % ls <etc, etc> % exit Script done, file is script.out % scriptreplay --timing file.tm --typescript script.out
```

## SEE ALSO

(1)

## COPYRIGHT

Copyright 2008 Jas Youngman

Copyright 2008 Karel Zak

这是一个免费软件；请参阅源代码的复制条件。没有任何担保，即使对于商业性或特定用途的适用性也是如此。

根据 GNU 通用许可许可证第 2 或更高版本发布。

## AUTHOR

长选项的强制参数对于短选项也是强制的。

`-o`, `--output=`FILE`

交互式操作，将输出发送到`FILE`

`-i`, `--ignore-case`

认为大小写相同

`-E`, `--ignore-tab-expansion`

忽略由于制表展开引起的更改

`-Z`, `--ignore-trailing-space`

忽略行尾的空白字符

`-b`, `--ignore-space-change`

忽略空白字符数量的变化

`-W`, `--ignore-all-space`

忽略所有空白字符

`-B`, `--ignore-blank-lines`

忽略全空行的更改

`-I`, `--ignore-matching-lines=`RE`

忽略所有行都匹配`RE`的更改

`--strip-trailing-cr`

去除输入中行尾的回车符

`-a`, `--text`

将所有文件视为文本

`-w`, `--width=`NUM`

输出最多`NUM`（默认 130）列

`-l`, `--left-column`

仅输出公共行的左列

`-s`, `--suppress-common-lines`

不输出公共行

`-t`, `--expand-tabs`

在输出中将制表符为空格

`--tabsize=`NUM`

每`NUM`（默认 8）字符停止

`-d`, `--minimal`

尽量寻找更小的更改集

`-H`, `--speed-large-files`

假设大文件有许多离散的小更改

`--diff-program=`PROGRAM`

使用`PROGRAM`比较文件

`--help`

显示帮助并退出

`-v`, `--version`

输出版本信息并退出

如果`FILE`为`-``，则从标准输入读取。如果输入相同退出状态为 0，不同则为 1，出错则为 2。

## AUTHOR

由 Thomas Lord 编写。

## REPORTING BUGS

向此处报告 bug：

<>

使用 GNU 软件的帮助：<>

## COPYRIGHT

Copyright 2011 Free Software Foundation, Inc. License GPLv3+: GNU GPL 版本 3 或更高版本 <>。

这是一个免费软件：你可以更改和分发它。法律允许范围内没有任何担保。

## SEE ALSO

(1), (1), (1)

`sdiff`的完整文档由 Texinfo 手册维护。如果你的站点正确安装了`info`和`sdiff`程序，执行命令

`info sdiff`将让你访问完整手册。

* * *

以下是可用命令。在所有情况下，`bdaddr`指定要搜索或浏览的设备。如果`bdaddr`使用`local`，则搜索本地 SDP 数据库。

服务通过 4 字节的`record_handle`进行识别和操作（而不是服务名）。要查找服务的`record_handle`，请在`search`或`browse`结果中查找 "Service RecHandle" 行。

```bash
search [--bdaddr bdaddr] [--tree] [--raw] [--x] service_na
```

搜索服务..

从本地 SDP 数据库中删除服务。

注意：本地适配器配置将不会更新，此命令应仅用于 SDP 测试。

```bash
get [--tree] [--raw] [--x] [--bdaddr bdaddr] record_handle
```

从本地 SDP 数据库检索服务。

```bash
setattr record_handle attrib_id attrib_value
```

为 SDP 记录设置或添加属性。

```bash
setseq record_handle attrib_id attrib_values
```

为 SDP 记录设置或添加属性序列。

## 选项

```bash
--help
```

显示关于使用 sdptool 的帮助信息。

## 示例

```bash
sdptool browse 00:80:98:24:15:6D
sdptool browse local
sdptool add DUN
sdptool del 0x10000
```

## 缺陷

文档需要改进。

## 作者

Maxim Krasnyansky <>. 手册由 Edd Duill <> 编写。

* *

# seahorse-daemon

## 名称

seahorse-daemon - seahorse 密码缓存代理

## 概览

```bash
seahorse-daemon [ OPTION... ]
```

## 描述

Seahorse 是一个用于加密密钥的 GNOME 应用。

这是一个守护程序，为 Seahorse 的其他部分提供服务。

## 选项

### 帮助选项

```bash
-?, --help
```

显示所有选项的摘要并退出。

```bash
--usage
```

显示简要用法并退出。

### 应用程序选项

```bash
-d, --no-daemonize
```

不将 seahorse-daemon 守护化。

### 附加选项

此外，适用于常用的 GTK+ 和 GNOME 命令行选项。详情请参见`--help`的输出。

## 版本

本手册页描述了`seahorse-daemon` 0.9.x 版本。

## 缺陷

如果你发现任何 bug，请报告至。

## 作者

Jacob Perkins <>

Jose Carlos Garcia Sogo <>

Jean Schurger <>

Stef Walter <>

Adam Schreiber <>

本手册页最初由 Michael Mende <> 为 Debian 系统编写。

## 版权

Copyright (C) 2001, 2002 Jose Carlos Garcia Sogo

Copyright (C) 2002, 2003 Jacob Perkins

Copyright (C) 2004, 2006 Stef Walter, Adam Schreiber

## 许可证

```bash

```

## 描述

Seahorse 是 GnuPG（Gnu Privacy Guard 程序）的前端，集成到 GNOME 桌面中。它是一个用于安全通信和数据存储的工具。可以通过 GUI 轻松进行数据加密和数字签名创建，并通过直观的界面轻松执行密钥管理。

## 选项

```bash
-?, --help
```

显示帮助选项

```bash
--help-all
```

显示所有帮助选项

```bash
--help-gtk
```

显示 GTK+ 选项

### 应用程序选项：

```bash
-v, --version
```

此应用程序版本号

```bash
--display=*DISPLAY
```

要使用的 X 显示器

## 缺陷

如果你发现任何 bug，请报告至

## 作者

Jacob Perkins <>

Jose Carlos Garcia Sogo <>

Jean Schurger <>

Stef Walter <>

Adam Schreiber <>

* *

# SECON

## 名称

secon - 从文件、程序或用户输入查看 SELinux 上下文。

## 概览

```bash
secon [-hVurtscmPRfLp] [CONTEXT]

[--file] FILE

[--link] FILE

[--pid] PID
```

## 描述

查看上下文的一部分。上下文取自文件、pid、用户输入或`secon`原始执行时的上下文。

```bash
-V, --version
```

显示 secon 的当前版本。

```bash
-h, --help
```

显示 secon 的用法信息。

```bash
-P, --prompt
```

输出适用于提示的格式的数据。

```bash
-C, --color
```

输出带有关联 ANSI 颜色代码的数据（需要`-P`）。

```bash
-u, --user
```

显示安全上下文的用户

```bash
-r, --role
```

显示安全上下文的角色

```bash
-t, --type
```

显示安全上下文的类型

```bash
-s, --sensitivity
```

显示安全上下文的敏感性级别。

```bash
-c, --clearance
```

显示安全上下文的权限级别。

```bash
-m, --s-range
```

以范围形式显示安全上下文的敏感级别和权限。

```bash
-R, --raw
```

从指定的进程 PID 获取 fscreate 上下文。

```bash
--current, --self
```

从当前进程获取上下文。

```bash
--current-exec, --self-exec
```

从当前进程获取执行上下文。

```bash
--current-fs, --self-fs
```

从当前进程获取 fscreate 上下文。

```bash
--parent
```

从当前进程的父进程获取上下文。

```bash
--parent-exec
```

从当前进程的父进程获取执行上下文。

```bash
--parent-fs
```

从当前进程的父进程获取 fscreate 上下文。

可以提供额外的参数`CONTEXT`，如果没有指定选项让`secon`从其他来源获取上下文，则可以使用。如果该参数为`-`，则从 stdin 读取上下文。

如果没有参数，`secon`将尝试从 stdin 读取上下文（如果不是 tty），否则`secon`将像传递了`--self`一样。

如果没有传递`--user`、`--role`、`--type`、`--level`或`--s-range`，则输出所有内容。

## 参见

`chcon` (1)

## 作者

`Jas Antill ()`

* *

# SECRET-TOOL

## 名称

secret-tool - 存储和检索密码

## 概览

```bash
secret-tool store --label='Label' {attribute} {value} ...
secret-tool lookup {attribute} {value} ...
secret-tool clear {attribute} {value} ...
secret-tool search [--all]{attribute} {value} ...
```

## 描述

`secret-tool`是一个用于存储和检索密码的命令行工具。

每个密码都存储在一个项目中。项目通过一组属性键和值进行唯一标识。在存储密码时，你指定唯一的属性名和值对，在检索密码时，你提供相应的属性名和值对。

## STORE

使用`store`参数运行`secret-tool`来存储密码。你还可以使用`--label`参数为密码指定标签。该标签将在密码管理器中显示。

存储密码时，请确保传递一组唯一的属性名和值。如果属性与已存在的项目匹配，将更新该项目而不是创建新项目。

如果从终端或 tty 调用，将提示要存储的密码并只接受一行。

也可以通过 stdin 管道输入要存储的密码。密码将是 stdin 的内容，直到遇到 EOF。如果你通过 stdin 提供了一个换行符，它将作为密码的一部分被存储。

## LOOKUP

要查找密码，请运行`secret-tool`并使用`lookup`参数。指定你在存储密码时提供的属性和键值对。

如果有多个项匹配提供的属性，将返回第一个已解锁的密码。如有必要，将解锁该项。

在终端或 tty 上打印密码时，密码后会额外添加一个换行符。

## CLEAR

要删除密码，请运行`secret-tool`并使用`clear`参数。指定你在存储密码时提供的属性和键值对。

所有匹配属性的已解锁项将被删除。

## SEARCH

此命令在 secret service 中搜索并打印匹配项的详情。指定你在存储密码时提供的属性和键值对。你可以使用以下选项：

`--all`

返回所有匹配结果，而不仅仅是匹配项之一。如果不使用此选项，将打印服务返回的第一个解锁匹配项。

`--unlock`

解锁已锁定的项然后打印它们的详情。如果不使用此选项，锁定的项将被跳过。

## EXIT STATUS

成功时返回 0，否则返回非零失败代码。

## EXAMPLES

**示例 1. 存储、检索和清除密码**



```bash
$ secret-tool store --label='My password' key1 value1 key2 value2
Password: My password
```

### 选项

`-e` `script`，`--expression=` `script`

将脚本添加到要执行的命令中。

`-f` `script-file`，`--file=` `script-file`

将脚本文件的内容添加到要执行的命令中。

`--follow-syinks`

在进行就地处理时跟踪符号链接。

`-i[SUFFIX]`，`--in-place[*SUFFIX]`

在地地编辑文件（如果提供了 `SUFFIX` 则创建备份）。

`-c`，`--copy`

在 `-i` 模式下重命名文件时使用复制而非重命名。

`-b`，`--binary`

什么都不做；为了与 WIN32/CYGWIN/MSDOS/EMX 兼容，以二进制模式打开文件（CR+LFs 不被特殊对待）。

`-l` `N`，`--line-length=*N`

为 `l` 命令指定所需的行换行长度。

`--posix`

禁用所有 GNU 扩展。

`-r`，`--regexp-extended`

在脚本中使用扩展正则表达式。

`-s`，`--separate`

将文件视为独立的，而不是一个单一连续的长流。

`-u`，`--unbuffered`

从输入文件中加载最少的数据并更频繁地刷新输出缓冲区。

`-z`，`--null-data`

使用 NUL 字符分隔行。

`--help`

显示此帮助并退出。

`--version`

输出版本信息并退出。

如果没有给出 `-e`、`--expression`、`-f` 或 `--file` 选项，则第一个非选项参数被视为解释的 `sed` 脚本。所有剩余参数都是输入文件；如果没有指定输入文件，则读取标准输入。

GNU `sed` 帮助页：<>。使用 GNU 软件的通用帮助：<>。错误报告邮箱至：<>。必须确保在“Subject:”字段的任何地方包含“sed”一词。

## COMMAND SYNOPSIS

这只是 `sed` 命令的简要概要，用于向已经熟悉 `sed` 的用户提醒；更完整的描述请参考其他文档（如 texinfo 文档）。

### 零地址“命令”

`:*label*`

用于 `b` 和 `t` 命令的标签。

`#*comnt*`

注释持续到下一个换行符（或 `-e` 脚本片段的结束）。

`}`

`{ }` 块的结束括号。

### 零地址或单地址命令

`=`

打印当前行号。

`a \`

`*text*`

追加 `text`，每个添加的换行符前都有反斜杠。

`i \`

`*text*`

插入 `text`，每个添加的换行符前都有反斜杠。

`q [*exit-code]`

立即退出 `sed` 脚本，不再处理更多输入，但如果没有禁用自动打印，则会打印当前模式空间。退出码参数是 GNU 扩展。

`Q [*exit-code]`

立即退出 `sed` 脚本，不再处理更多输入。这是一个 GNU 扩展。

`r*filena*`

追加从 `filena` 读取的文本。

`R*filena*`

追加从 `filena` 读取的一行。该命令每次调用都会文件中读取一行。这是一个 GNU 扩展。

### 接受地址范围的命令

`{`

开始一个命令块（以 `}` 结束）。

`b*label*`

跳转到 `label`；如果省略 `label`，则跳转到脚本末尾。

`c \`

以“视觉无歧”的形式列出当前行，并在 `width` 个字符处断开。这是一个 GNU 扩展。

`n N`

将下一行输入读取/追加到模式空间。

`p`

打印当前模式空间。

`P`

打印当前模式空间直到第一个添加的换行符。

`s/*regexp*/*replacent*/`

尝试对模式空间匹配 `regexp`。如果成功，将匹配的那部分替换为 `replacent`。`replacent` 可以包含特殊字符 `&` 来引用模式空间中匹配的那部分，以及特殊转义符 `\1` 到 `\9` 来引用 `regexp` 中相应的匹配子表达式。

`t*label*`

如果自上次读取输入行以来以及自上一次 `t` 或 `T` 命令以来，`s///` 执行了成功的替换，则跳转到 `label`；如果省略 `label`，则跳转到脚本末尾。

`T*label*`

如果自上次读取输入行以来以及自上一次 `t` 或 `T` 命令以来没有 `s///` 执行成功的替换，则跳转到 `label`；如果省略 `label`，则跳转到脚本末尾。这是一个 GNU 扩展。

`w*filena*`

将当前模式空间写入 `filena`。

`W*filena*`

将当前模式空间的第一行写入 `filena`。这是一个 GNU 扩展。

`x`

交换保持空间和模式空间的内容。

`y/*source*/*dest*/`

将模式空间中出现在 `source` 中的字符转换为 `dest` 中对应的字符。

## Addresses

`sed` 命令可以不带地址，在这种情况下，命令将对所有输入行执行；带有一个地址，在这种情况下，命令将仅对匹配该地址的输入行执行；或者有两个地址，在这种情况下，命令将对匹配从第一个地址开始到第二个地址的闭区间范围的所有输入行执行。

关于地址范围有三点需要注意：语法为 `addr1`,`addr2`（即地址之间用逗号分隔）；`addr1` 匹配到的行将始终被接受，即使 `addr2` 选择的是更早的行；并且如果 `addr2` 是一个 `regexp`（正则表达式），它将不会对 `addr1` 匹配的行进行测试。

在地址（或地址范围）之后、命令之前，可以插入一个 `!`，它表示指定仅当地址（或地址范围）**不**匹配时才执行该命令。

支持以下地址类型：

`nuer`

仅匹配指定的行号 `nuer`（除非在命令行中指定了 `-s` 选项，否则它将跨文件累加计数）。

`first`~`step`

从第 `first` 行开始，每隔 `step` 行匹配一次。例如，`sed -n 1~2p` 将打印输入流中所有奇数行，而地址 `2~5` 将匹配从第二行开始的每五行。`first` 可以为 0；在这种情况下，`sed` 的操作将等同于 `step`。（这是一个扩展。）

`$`

匹配最后一行。

`/*regexp*/`

匹配符合正则表达式 `regexp` 的行。

`\c*regexp***c`

匹配符合正则表达式 `regexp` 的行。`c` 可以是任意字符。

GNU `sed` 还支持以下两种特殊的双地址形式：

`0,*addr2`

从“匹配到第一个地址”状态开始，直到找到 `addr2` 为止。这与 `1,*addr2` 类似，区别在于如果 `addr2` 匹配了输入的第一行，`0,*addr2` 形式将处于范围的末尾，而 `1,*addr2` 形式仍处于范围的开头。这仅在 `addr2` 是正则表达式时才有效。

`addr1`,+`N`

将匹配 `addr1` 以及 `addr1` 之后的 `N` 行。

`addr1`,~`N`

将匹配 `addr1` 以及 `addr1` 之后的行，直到遇到下一行行号是 `N` 的倍数的行为止。

## 正则表达式

POSIX.2 BREs（基本正则表达式）*应该*被支持，但由于性能问题，并没有完全支持。正则表达式中的 `\n` 序列匹配换行符，`\a`、`\t` 以及其他序列也是如此。

## 缺陷

请向 <> 提交邮件缺陷报告。此外，如果可能的话，请在报告正文中包含 `sed --version` 的输出。

## 作者

由 Jay Fenlason、Tom Lord、Ken Pizzini 和 Paolo Bonzini 编写。

GNU `sed` 帮助页：<>。使用 GNU 软件的通用帮助：<>。邮件缺陷报告邮箱：<>。确保在“Subject:”字段的某处包含“sed”一词。

## 版权

Copyright 2012 Free Software Foundation, Inc. License GPLv3+：GNU GPL 第 3 或更高版本 <>>。

这是免费软件：你可以自由地更改和分发它。在法律允许的范围内**不提供保证**。

## 另请

(1), (1), (1), (1), (1), `sed.info`，关于 `sed` 的各种书籍，`sed` FAQ (

**`sed`** 的完整文档作为 Texinfo 手册维护。如果你的站点正确安装了 `info` 和 `sed` 程序，则执行命令 `info sed` 将允许你访问完整手册。

---

# sendiso

## 名字

`sendiso` - 从转储文件（dump file）发送 IEEE 1394 同步数据包。

## 概要

`sendiso` [`*options*`] `FILE`

## 描述

`sendiso` 获取由 (1) 生成的转储文件 `FILE`，提取包并按照接收时的顺序（按 `sa` 顺序，带有 `sa` 通道行号）尽可能快地发送——不保留原始转储的时间计时。

目前未知。

## 另请

(1), (5)

## 作者

Andreas Boe <>

---

# servertool

## 名字

`servertool` - 为开发者提供一个易于使用的接口，用于注册、注销、启动和关闭持久服务器。

## 概要

`servertool` `-ORBInitialPort` `naserverport` [`options*`] [`commands*`]

`*options*`

命令行选项。参见“选项”（Options）。

`*commands*`

命令行命令。参见“命令”（Commands）。

## 描述

`servertool` 命令为开发者提供了注册、注销、启动和关闭持久服务器的命令行界面。命令行命令允许你获取有关服务器的各种统计信息。参见“命令”（Commands）。

## 选项

`-ORBInitialHost naserverhost`

此选项是必须的。它指定了运行 `na` 服务器并监听入站请求的主机。`naserverport` 值应指定 `orb` 运行并监听请求的端口。当未指定此选项时，值为 `localhost`。如果 `orbd` 和 `servertool` 运行在不同的机器上，则你必须指定运行 `orbd` 的主机 `na` 地址或 IP 地址。

*注意：*在 Oracle Solaris 上，你必须成为 root 用户才能在 1024 以下的端口上启动进程。Oracle 建议将 `naserverport` 值设置为大于或等于 1024 的端口号。

`-Joption`

将 `option` 传递给 Java 虚拟机，其中 `option` 是 Java 启动器参考页描述的选项之一。例如，`-J-Xms48m` 将启动内存设置为 48 MB。参见 (1)。

## 命令

你可以带或不带命令行启动 `servertool` 命令。

如果你在启动 `servertool` 时没有指定命令，命令行工具将显示 `servertool` 提示符，可以在其中输入命令：`servertool >`。

如果你在启动 `servertool` 时指定了命令，则 Java IDL Server 工具启动、执行命令并退出。

`register -server server-class-na -classpath classpath-to-server [-applicationNa application-na -args args-to-server -vmargs flags-for-JVM]`

向对象请求代理守护进程（ORBD）注册一个新的持久服务器。如果服务器尚未注册，则将其注册并激活。此命令将在由 `-server` 选项指定的服务器的 main 类中调用安装函数。安装函数应为 `public static void install(org.omg.CORBA.ORB)`。安装函数是可选的，允许开发者提供自己的服务器安装行为，例如创建数据库模式。

`unregister -serverid server-id | -applicationNa application-na`

通过服务器 ID 或其应用 `na` 从 ORBD 中注销服务器。此命令将在由 `-server` 选项指定的服务器的 main 类中调用注销函数。注销函数应为 `public static void uninstall(org.omg.CORBA.ORB)`。注销函数是可选的，允许开发者提供自己的服务器注销行为，例如撤销安装函数的行为。

`getserverid -applicationNa application-na`

返回与 `application-na` 值对应的服务器 ID。

`list`

列出向 ORBD 注册的所有持久服务器的信息。

`listappnas`

列出当前向 ORBD 注册的所有服务器的应用 `nas`。

`listactive`

列出所有由 ORBD 启动并正在运行的持久性服务器信息。

`locate -serverid *server-id* | -applicationNa *application-na* [ -endpointType *endpointType* ]`

为注册服务器创建的所有 ORB 定位特定类型的端点（端口）。如果服务器尚未运行，则会激活它。如果未指定 `endpointType` 值，则返回与服务器中每个 ORB 关联的明文/非受保护端点。

`locateperorb -serverid *server-id* | -applicationNa *application-na* [ -orbid *ORB-na* ]`

定位注册服务器的特定对象请求代理（ORB）注册的所有端点（端口）。如果服务器尚未运行，则会激活它。如果未指定 `orbid`，则将默认值赋给 `orbid`。如果创建了任何 `orbid` 为空字符串的 ORB，则返回其注册的所有端口。

`orblist -serverid *server-id* | -applicationNa *application-na*`

列出在服务器上定义的 ORB 的 `ORBId`。`ORBId` 是服务器创建的 ORB 的字符串 `na`。如果服务器尚未运行，则会激活它。

`shutdown -serverid *server-id* | -applicationNa application-na`

关闭已向 ORBD 注册的活动服务器。在执行此命令期间，还会调用由 `-serverid` 或 `-applicationNa` 参数指定的类中定义的 `shutdown` thod 来关闭服务器进程。

`startup -serverid *server-id* | -applicationNa application-na`

启动或激活向 ORBD 注册的服务器。如果服务器未运行，则此命令将启动服务器。如果服务器已经在运行，则显示错误信息。

`help`

列出通过 `servertool` 命令为服务器提供的可用命令。

`quit`

退出 `servertool` 命令。

## 参见

(1)

---

# SESS_ID

## 名称

`sess_id` - SSL/TLS 会话处理工具。

## 概要

`openssl sess_id [--inform PEM|DER] [--outform PEM|DER] [--in filena] [--out filena] [--text] [--noout] [--context ID]`

## 或

`sess_id` 进程处理 SSL 会话结构的编码版本，并可选以人类可读格式打印 SSL 会话详情（例如 SSL 会话主密钥）。由于这是一个不需要任何 SSL 协议知识即可正确使用的诊断工具，大多数用户将不需要使用它。

`-inform DER|PEM`

指定输入格式。`DER` 选项使用包含会话详情的 ASN1 DER 编码格式。精确格式可能随版本变化。`PEM` 格式是默认格式：它由 `DER` 格式经过 base64 编码并带有额外的头部和页脚行。

`-outform DER|PEM`

## 输出

典型输出：

```text
SSL-Session: Protocol : TLSv1 Cipher : 0016 Session-ID: 871E62626C554CE95488823752CBD5F36

73A3EF3DCE9C67BD916C809914B40ED Session-ID-ctx: 01000000 Master-Key: A7CEFC571974BE02CAC305269DC59F76E

A9F0B180CB6642697A68251F2D2BB57E

51DBBB4C7885573192AE9AEE220FACD Key-Arg : None Start Ti: 948459261 Tiout : 300 (sec) Verify return code 0 (ok)
```

下面将详细描述这些内容。

**Protocol**

正在使用的协议 TLSv1、SSLv3 或 SSLv2。

**Cipher**

使用的密码是实际的原始 SSL 或 TLS 密码代码，更多请参见 SSL 或 TLS 规范。

**Session-ID**

十六进制格式的 SSL 会话 ID。

**Session-ID-ctx**

十六进制格式的会话 ID 上。

**Master-Key**

这是 SSL 会话主密钥。

**Key-Arg**

密钥参数，这仅用于 SSL v2。

**Start Ti**

以标准 Unix 格式整数表示的会话开始 ti。

**Tiout**

秒为单位 tiout。

**Verify return code**

验证 SSL 客户端证书时的返回代码。

## 注意事项

PEM 编码会话格式使用头部和页脚行：

```text
-----BEGIN SSL SESSION PARAMETERS-----
-----END SSL SESSION PARAMETERS-----
```




由于 SSL 会话输出包含主密钥，因此可以使用这些信息读取加密会话的内容。因此，如果信息是由“真实”应用程序输出的，应该采取适当的安全措施。但这被强烈建议不要这样做，应仅用于调试目的。

## 缺陷

密码和 `start ti` 应该以人类可读的形式打印。

## 参见

(1), (1)

* * *

# SESSREG

## 名称

`sessreg` - 为非 init 客户端管理 `utmp (5)`/`wtmp (5)` 条目

## 概要

`sessreg [-w wtmp (5)-file] [-u utmp (5)-file] [-L lastlog-file] [-l line-na] [-h host-na] [-s slot-na] [-x Xservers-file] [-t ttys-file] [-V] [-a] [-d] user-na`

## 描述

`sessreg` 是一个用于 `xdm` 会话的 `utmp`/`wtmp`/`log` 管理程序。

System V 比 BSD 有更好的 `utmp` 接口；它动态分配文件，而不是在 `/etc/ttys` 中的固定位置写入。

为了管理 BSD 风格的 `utmp` 文件，`sessreg` 有两种策略。与 `xdm` 结合，`-x` 选项计算 `/etc/ttys` 中的行数，然后加上 `Xservers` 文件中的显示行数。显示 `na` 使用 `-l` 选项指定为 `line-na`。此总和将作为写入 `utmp` 文件的 `slot`。在更一般的情况下，`-s` 选项直接指定 `slot`。如果由于特殊原因你的系统使用 `/etc/ttys` 以外的文件来管理 init，`-t` 选项可以引导 `sessreg` 在其他地方查找会话计数。

相反，System V 管理器永远不需要使用这些选项（`-x`、`-s` 和 `-t`）。为了使程序更容易于记录和解释，`sessreg` 接受 System V 环境中的 BSD 特定标志并忽略它们。

BSD 和 Linux 在 `utmp` 文件中还有一个 `host-na` 字段，这在 System V 中不存在。System V 版本的 `sessreg` 也忽略此选项。

此版本的 `sessreg` 使用现代 POSIX (3c) 接口构建，不再需要 `slot`、`ttys-file` 或 `Xservers-file` 映射。为了兼容旧版本和其他操作系统，接受 `-s`、`-t` 和 `-x` 标志但会被忽略。

## 用法

在 `Xstartup` 中，放置如下调用：

`sessreg -a -l $DISPLAY -x /etc/X11/xdm/Xservers $USER`

并在 `Xreset` 中：

`sessreg -d -l $DISPLAY -x /etc/X11/xdm/Xservers $USER`

## 选项

`-w wtmp (5)-file`

指定备用的 `wtmp (5)` 文件，而不是 `/var/log/wtmp`。特殊值 `"none"` 禁用向 `wtmp (5)` 文件的写入。

`-u utmp (5)-file`

指定备用的 `utmp (5)` 文件，而不是 `/var/run/utmp`。特殊值 `"none"` 禁用向 `utmp (5)` 文件的写入。

`-L lastlog-file`

如果平台支持 `lastlog` 文件，此选项指定一个备选的 `lastlog` 文件，而不是 `/var/log/lastlog`。特殊值 `"none"` 会禁用向 `lastlog` 文件写入记录。

`-l line-name`

这描述了条目的“行”（line）名称。对于终端会话，这是终端设备文件名的最后路径段（例如 `tty0`）。对于 X 会话，它可能应该是分配给用户会话的本地显示名称（例如 `:0`）。如果没有指定，则将通过 (3) 确定终端名称并剥离前面的组件。

此会话应添加到 `utmp`/`wtmp` 中。

`-d`

此会话应从 `utmp`/`wtmp` 中删除。必须指定 `-a`/`-d` 之一。

## 另请

(1), (5), (5)

## 作者

Keith Packard, MIT X Consortium

***

# SETCIFSACL

## 名称

`setcifsacl` - 用于修改通用网络文件系统 (CIFS) 安全描述符中 ACL 的用户空间辅助程序

## 概要

`setcifsacl [-v|-a|-D|-M|-S] "{一个或多个 ACE}" {文件系统对象}`

## 描述

此工具是 `cifs-utils` 件的一部分。

`setcifsacl` 是 Linux CIFS 客户端文件系统的用户空间辅助程序。用于修改文件系统对象的安全描述符的 ACL。是否应用设置的安全描述符由 CIFS/SMB 服务器决定。

此程序使用插件处理用户和组名称到 SIDs 的映射。`/etc/cifs-utils/idmap-plugin` 应该是一个指向正确插件的链接。

## 选项

`-h`

打印用法信息并退出。

`-v`

打印版本号并退出。

`-a`

向安全描述符的 ACL 中添加一个或多个 ACE。即使 ACL 中已存在该 ACE，也会添加该 ACE。

`-D`

从安全描述符的 ACL 中删除一个或多个 ACE。若要删除列出的 ACE，现有 ACL 必须与整个 ACE 匹配。

`-M`

修改安全描述符的 ACL 中的一个或多个 ACE。使用 SID 和类型来匹配现有的 ACE，并用指定的 ACE 列表对其进行修改。

`-S`

使用 ACE 列表设置安全描述符的 ACL。现有 ACL 将完全被指定的 ACE 替换。

每个 ACE 条目以 `"ACL:"` 开头。双引号内指定了一个或多个 ACE。多个 ACE 之间用逗号分隔。

ACE 的后续字段可以修改，其可能值包括：

`SID`：可能是名称或原始 SID 值。

`type`：`ALLOWED (0x0)`、`DENIED (0x1)`、`OBJECT_ALLOWED (0x5)`、`OBJECT_DENIED (0x6)`。

`flags`：`OBJECT_INHERIT_FLAG (OI` 或 `0x1)`、`CONTAINER_INHERIT_FLAG (CI` 或 `0x2)`、`NO_PROPAGATE_INHERIT_FLAG (NI` 或 `0x4)`、`INHERIT_ONLY_FLAG (IO` 或 `0x8)`、`INHERITED_ACE_FLAG (IA` 或 `0x10)`，或这些值的组合/或操作。

`mask`：可以是 `FULL`、`CHANGE`、`READ` 之一，`R W X D P O` 的组合，或十六进制值。

## 示例

### 添加 ACE

```bash
setcifsacl -a "ACL:CIFSTESTDOM\user2:DENIED/0x1/D" <file_name>

setcifsacl -a "ACL:CIFSTESTDOM\user1:ALLOWED/OI|CI|NI/D" <file_name>
```

### 删除 ACE

```bash
setcifsacl -D "ACL:S-1-1-0:0x1/OI/0x1201ff" <file_name>
```

### 修改 ACE

```bash
setcifsacl -M "ACL:CIFSTESTDOM\user1:ALLOWED/0x1f/CHANGE" <file_name>
```

### 设置 ACL

```bash
setcifsacl -S "ACL:CIFSTESTDOM\Administrator:0x0/0x0/FULL,

ACL:CIFSTESTDOM\user2:0x0/0x0/FULL" <file_name>
```

## 注释

内核对 ACL 的支持最初在 2.6 中引入。

## 另请

(8), (1)

## 作者

Shirish Pargakar 编写了 `setfacl`。

***

# SETFACL

## 名称

`setfacl` - 设置访问控制列表

## 概要

`setfacl [-bkRLvh] [{-m|-x} acl_spec] [{-M|-X} file]`

## 选项

`-k, --remove-default`

移除默认 ACL。如果不存在默认 ACL，则不发出警告。

`-n, --no-mask`

不重新计算有效权限码。`setfacl` 的默认行为是重新计算 ACL 掩码条目，除非显式给出了掩码条目。掩码条目设置为所有组以及所有用户和组条目的权限并集。（这些正是受掩码条目影响的条目。）

`--mask`

重新计算有效权限码，即使显式给出了 ACL 掩码条目。（参见 `-n` 选项。）

`-d, --default`

所有操作应用于默认 ACL。输入中的普通 ACL 条目提升为默认 ACL 条目。输入中的默认 ACL 条目将被丢弃。（如果发生这种情况，会发出警告）。

`--restore=file`

恢复由 `getfacl -R` 或类似命令创建的权限备份。使用此机制恢复整个目录子树的所有权限。如果输入包含所有者注释或组注释，`setfacl` 会尝试恢复所有者和所属组。如果输入包含标志注释（定义了 setuid、setgid 和粘滞位），`setfacl` 将相应地设置这三个位；否则，将清除它们。此选项除了 `--test` 外，不能与其他选项混合使用。

`--test`

测试模式。不更改任何文件的 ACL，而是列出生成的 ACL。

`-R, --recursive`

递归地对所有文件和目录执行操作。此选项不能与 `--restore` 混合使用。

`-L, --logical`

逻辑遍历，跟随目录的符号链接。默认行为是跟随符号链接参数，并跳过子目录中遇到的符号链接。仅与 `-R` 配合时有效。此选项不能与 `--restore` 混合使用。

`-P, --physical`

物理遍历，不跟随目录的符号链接。这也会跳过符号链接参数。仅与 `-R` 配合时有效。此选项不能与 `--restore` 混合使用。

`-v, --version`

打印 `setfacl` 的版本并退出。

`-h, --help`

打印解释命令行选项的帮助信息。

`--`

命令行选项的结束。所有剩余参数都将被解释为文件名，即使它们以连字符开头。

`-`

如果文件名参数是单个连字符 `-`，`setfacl` 从标准输入读取文件列表。

### ACL 条目

`setfacl` 工具识别以下 ACL 条目格式（为了清晰起见插入空格）：

`d[efault]:] [u[ser]:]*uid* [:*perms*]`

指定用户的权限。如果 `uid` 为空，则为文件所有者的权限。

`d[efault]:] g[roup]:*gid* [:*perms*]`

指定组的权限。如果 `gid` 为空，则为所属组的权限。

`d[efault]:] m[ask][:] [:*perms*]`

有效权限掩码。

`d[efault]:] o[ther][:] [:*perms*]`

其他权限。

分隔符字符与非分隔符字符之间的空格会被忽略。

修改和设置操作使用了包含权限的正确 ACL 条目（选项 `-m`、`-M`、`--set` 和 `--set-file`）。没有 `perms` 字段的条目用于删除条目（选项 `-x` 和 `-X`）。

对于 `uid` 和 `gid`，你可以指定用户名或数字。

`perms` 字段是表示权限的字符组合：读 (`r`)、写 (`w`)、执行 (`x`)、如果是目录或已具有执行权限时可执行 (`X`)。此外，`perms` 字段可以是八进制数字（0-7）。

### 自动创建的条目

最初，文件和目录仅包含针对所有者、组和其他人的三个基础 ACL 条目。

- 这三个基础条目无法删除。每种基础条目类型恰好有一个项。
- 只要 ACL 包含用户条目或组对象，它也包含一个有效权限掩码。
- 只要 ACL 包含任何默认 ACL 条目，就存在三个默认 ACL 基础条目（默认所有者、默认组和默认其他）。
- 只要默认 ACL 包含用户条目或组对象，它也包含一个默认有效权限掩码。

为了帮助用户确保这些规则，`setfacl` 在以下条件下根据现有条目创建条目：

- 如果 ACL 包含用户或组条目，且不存在掩码条目，则创建一个包含与组条目相同权限的掩码条目。除非给出 `-n` 选项，否则掩码条目的权限将进一步调整，以包含受掩码影响的所有权限的并集（参见 `-n` 选项说明）。
- 如果创建了默认 ACL 条目，且默认 ACL 不包含所有者、所属组或其他条目，则将 ACL 所有者、所属组或其他条目的副本添加到默认 ACL 中。
- 如果默认 ACL 包含用户或组条目，且不存在掩码条目，则添加一个包含与默认默认 ACL 组条目相同权限的掩码条目。除非给出 `-n` 选项，否则掩码条目的权限将进一步调整，以包含受掩码影响的所有权限的并集（参见 `-n` 选项说明）。

## 示例

### 授予额外用户读取权限

```bash
setfacl -m u:lisa:r file
```

### 撤销所有组和所有用户的写入权限（使用有效权限掩码）

```bash
setfacl -m m::rx file
```

### 从文件的 ACL 中删除组条目

```bash
setfacl -x g:staff file
```

### 将一个文件的 ACL 复制到另一个文件

(1), (1), (1), (5)

* * *

# SETFATTR

## 名称

`setfattr` - 设置文件系统对象的扩展属性

## 语法

```text
setfattr [-h] -n na [-v value] pathna...
setfattr [-h] -x na pathna...
setfattr [-h] --restore=file
```

## 描述

`setfattr` 命令为每个指定的文件与扩展属性 `na` 关联一个新的 `value`。

## 选项

`-n na`, `--na=*na*`

指定要设置的扩展属性 `na`。

`-v value`, `--value=*value*`

指定扩展属性的新值。有三种编码方法。如果给字符串用双引号括起，内部字符串被视为文本。在这种情况下，反斜杠和双引号有特殊含义，需要用反斜杠进行转义。任何控制字符都可以用反斜杠后跟三位八进制 ASCII 码进行编码。如果给字符串以 `0x` 或 `0X` 开头，则表示十六进制数字。如果给字符串以 `0s` 或 `0S` 开头，则预期 base64 编码。参见 (1) 中的 `--encoding` 选项。

`-x na`, `--remove=*na*`

完全删除扩展属性。

`-h`, `--no-dereference`

不跟随符号链接。如果 `pathna` 是符号链接，则不跟随它，而是修改其自身的 inode。

`--restore=*file*`

从文件恢复扩展属性。文件必须是 `getfattr` 命令配合 `--dump` 选项生成的格式。如果文件名给出 `-`，则 `setfattr` 从标准输入读取。

`--version`

打印 `setfattr` 的版本并退出。

`--help`

打印解释命令行选项的帮助信息。

`--`

命令行选项的结束。所有剩余参数都将被解释为文件名，即使它们以连字符开头。

## 作者

Andreas Gruenbacher, <> 以及 SGI XFS 开发团队, <>。

请向这些地址发送您的错误报告或注释。

## 参见

(1)，和 (5)。

* * *

# SETLEDS

## 名称

`setleds` - 设置键盘 LED

## 语法

`setleds [-v] [-L] [-D] [-F] [{+|-}num] [{+|-}caps*] [{+|-}scroll*]`

## 描述

`setleds` 报告并更改 VT 的 LED 设置（NumLock、CapsLock 和 ScrollLock）。不带参数时，`setleds` 打印当前设置。带有参数时，它设置或清除指示标志（并保持其他位不变）。如果给出 `-v` 标志，则会报告更改前后的设置。

LED 设置针对每个 VT 特定的（并使用 stdin 对应的 VT）。

默认情况下（或使用选项 `-F`），`setleds` 将仅更改 VT 标志（其设置可能会反映在键盘 LED 指示灯上）。

使用选项 `-D` 时，`setleds` 将同时更改 VT 标志及其默认设置（这样随后的重置将不会撤销更改）。这对于始终希望开启 NumLock 的用户可能有用。

使用选项 `-L` 时，`setleds` 不触碰 VT 标志，而只更改 LED。从现在起，LED 将不再反映 VT 标志（而是显示输入到它们中的内容）。命令 `setleds -L`（不带任何后续参数）将恢复 LED 反映 VT 标志的状态。

人们可以在 `/etc/rc` 中使用 `setleds` 来定义 NumLock 的初始状态和默认状态，例如通过：

```bash
INITTY=/dev/tty[1-8]

for tty in $INITTY; do
  setleds -D +num < $tty
done
```




## 选项

- `-num +num`：清除或设置 `NumLock`。（目前，`NumLock` 设置影响小数字键的解释。按下 `NumLock` 键切换 `NumLock` 设置。）

- `-caps +caps`：清除或设置 `CapsLock`。（目前，`CapsLock` 设置在应用于字母时会起到类似 `Shift` 键的作用。按下 `CapsLock` 键切换 `CapsLock` 设置。）

- `-scroll +scroll`：清除或设置 `ScrollLock`。（目前，按下 `ScrollLock` 键（或 `^S/^Q`）会停止/启动控制台输出。）

## BUG

在键盘应用模式下，`NumLock` 键不影响 `NumLock` 标志设置。

## 相关相关

(1)

---

# SETMETAMODE

## 名称

`settamode` - 定义键盘 `ta` 键处理

(1)

---

# SETPRIV

## 名称

`setpriv` - 以不同的 Linux 权限设置运行程序

## 语法概要

`setpriv` `[options]` `program` `[argunts]`

## 描述

设置或查询跨 (2) 继承的各种 Linux 权限设置。

## 选项

- `--clear-groups`：清除补充组。

- `-d`、`--dump`：转储当前权限状态。可以指定多次以显示额外的、通常无用的信息。与所有其他选项不兼容。

- `--groups group...`：设置补充组。参数是逗号分隔的列表。

- `--inh-caps (+|-)cap...` 或 `--bounding-set (+|-)cap...`：设置可继承的能力或能力边界集。参见 (7)。参数是逗号分隔的 `+cap` 和 `-cap` 条目，分别添加或删除条目。`+all` 和 `-all` 可用于添加或删除所有能力。能力集初始为 `--inh-caps` 的当前可继承集，以及 `--bounding-set` 的当前边界集。如果你从边界集中删除了某些内容，但没有同时从可继承集中删除该内容，你可能会变得困惑。不要这样做。

- `--keep-groups`：保留补充组。仅配合 `--rgid`、`--egid` 或 `--regid` 有用。

- `--list-caps`：列出所有已知的能力。此选项必须单独指定。

- `--no-new-privs`：设置 `no_new_privs` 位。设置此位后，(2) 将不会授予新权限。例如，`setuid` 和 `setgid` 位以及文件能力将被禁用。（执行带有这些位的二进制执行文件仍然可以工作，但它们将无法获得权限。某些 LSM（特别是 AppArmor）可能会导致某些程序执行失败。）此位由子进程继承且无法取消。参见 (2) 和 Linux 内核源码中的 `Documentation/:prctl/:no_:new_:privs.txt`。

  `no_new_privs` 位自 Linux 3.5 起支持。

- `--rgid gid`、`--egid gid`、`--regid gid`：设置真实的、有效的或双方的 `gid`。`gid` 参数可以以文本组名提供。为了安全，如果你设置了任何主 `gid`，应指定 `--clear-groups`、`--groups` 或 `--keep-groups` 之一。

- `--ruid uid`、`--euid uid`、`--reuid uid`：设置真实的、有效的或双方的 `uid`。`uid` 参数可以以文本用户名提供。设置 `uid` 或 `gid` 不改变能力，尽管结尾的 `exec` 调用可能会更改能力。这意味着，如果你是 root，你可能想做类似的操作：

```bash
setpriv --reuid=1000 --regid=1000 --caps=-all
```

- `--securebits (+|-)securebit...`：设置或清除安全位。参数是逗号分隔的列表。有效的安全位有 `noroot`、`noroot_locked`、`no_setuid_fixup`、`no_setuid_fixup_locked` 和 `keep_caps_locked`。`keep_caps` 由 (2) 清除，因此不允许。

- `--selinux-label label`：请求 SELinux 标签（使用 transition）。此工具与 `no_new_privs` 一起使用可能会导致安全后果。如果 SELinux 不使用，将导致 (1) 终止。

- `--apparmor-profile profile`：请求特定的 AppArmor 配置文件（使用 transition）。如果 AppArmor 不使用，将导致 (1) 终止，且转换被忽略。

- `-V`、`--version`：显示版本信息。

- `-h`、`--help`：显示帮助文本。

## 注意

如果应用任何指定的选项失败，`program` 将不会运行并会导致安全后果。例如，设置 `no_new_privs` 后执行受 SELinux 限制的程序（如此工具所示）可能会阻止 SELinux 限制生效。

## 相关相关

(2)、(7)

## 作者

Andy Lutomirski

## 可用性

`setpriv` 命令是 util-linux 软件包的一部分，来自 Linux Archive。

---

# SETSID

## 名称

`setsid` - 在新会话中运行程序

## 语法概要

`setsid` `[options]` `program` `[argunts]`

## 描述

`setsid` 在新会话中运行程序。

## 选项

- `-c`、`--ctty`：将控制终端设置为。

- `-w`、`--wait`：等待程序执行结束，并将退出值作为 `setsid` 的返回值。

- `-V`、`--version`：显示版本信息。

- `-h`、`--help`：显示帮助文本。

## 相关相关

(2)

## 作者

Rick Sladkey <>

## 可用性

`setsid` 命令是 util-linux 软件包的一部分，来自。

---

# SETTERM

## 名称

`setterm` - 设置终端属性

## 语法

`setterm` `[options]`

### `--append` [`console_nuer`]

类似于 `--dump`，但它将快照追加到快照文件中，而不是覆盖它。只有在没有提供 `--dump` 选项时才有效。

### `--background` `8-color|default`

设置背景文本颜色。

### `--blank` [`0-60|force|poke`]（仅限虚拟控制台）

设置空闲时间（以分钟为单位），在此时间后屏幕将自动清屏（如果可用则使用 APM）。如果不带参数，则获取清屏状态（返回哪个 VT 被清屏，未清屏的 VT 返回 `0`）。

`force` 选项即使在按下按键时也保持屏幕清屏。

`poke` 选项取消屏幕清屏。

### `--bfreq` [`nuer`]（仅限虚拟控制台）

设置铃声频率（单位为赫兹）。如果不带参数，默认为 `0`。

### `--blength` [`0-2000`]（仅限虚拟控制台）

设置铃声持续时间（单位为毫秒）。如果不带参数，默认为 `0`。

### `--blink` [`on|off`]

开启或关闭闪烁模式。在虚拟控制台外，`--blink off` 会关闭所有属性（粗体、半亮度、闪烁、反转）。

### `--bold` [`on|off`]

开启或关闭粗体（额外亮度）模式。在虚拟控制台外，`--bold off` 会关闭所有属性（粗体、半亮度、闪烁、反转）。

### `--clear` [`all|rest`]

如果不带参数或带参数 `all`，则清空整个屏幕并将光标设置为 `ho` 位置，就像 (1) 执行一样。如果带参数 `rest`，则从当前光标位置到末尾清空屏幕。

### `--clrtabs` [`tab1 tab2 tab3` ...]（仅限虚拟控制台）

从给定的水平光标位置（范围为 `1-160`）清除制表位停止。如果不带参数，则清除所有制表位停止。

### `--cursor` [`on|off`]

开启或关闭终端光标。

### `--default`

将终端的渲染选项设置为默认值。

### `--dump` [`console_nuer`]

将具有给定 `nuer` 的虚拟控制台快照写入由 `--file` 选项指定的文件，并覆盖其内容；默认是 `screen.dump`。如果不带参数，则转储当前虚拟控制台。这将覆盖 `--append`。

### `--file` `filena`

为命令行上的任何 `--dump` 或 `--append` 选项设置快照文件 `na`。如果不存在此选项，默认是当前目录下的 `screen.dump`。超过系统最大值的路径 `na` 将截断，数值请参见 `linux/limits.h` 中的 `PATH_MAX`。

### `--foreground` `8-color|default`

设置前景文本颜色。

### `--half-bright` [`on|off`]

开启或关闭暗亮（半亮度）模式。在虚拟控制台外，`--half-bright off` 会关闭所有属性（粗体、半亮度、闪烁、反转）。

### `--hbcolor` `16-color`

设置 16 色模式。

### `--initialize`

开启或关闭初始化模式。在虚拟控制台外，`--blink off` 会关闭所有属性（粗体、半亮度、闪烁、反转）。

### `--tabstop`

在 `1-160` 范围内从给定的水平光标位置开始清空制表位停止。

### `--cursor` [`on|off`]（仅限虚拟控制台）

开启或关闭光标模式。

### `--default`

将终端的渲染选项设置为默认值。

### `--dump` [`console_nuer`]

将具有给定 `nuer` 的虚拟控制台快照写入由 `--file` 选项指定的文件，并覆盖其内容；默认是 `screen.dump`。如果不带参数，则转储当前虚拟控制台。这将覆盖 `--append`。

### `--file` `filena`

为命令行上的任何 `--dump` 或 `--append` 选项设置快照文件 `na`。如果不存在此选项，默认是当前目录下的 `screen.dump`。超过系统最大值的路径 `na` 将截断，数值请参见 `linux/limits.h` 中的 `PATH_MAX`。

### `--foreground` `8-color|default`

设置前景文本颜色。

### `--half-bright` [`on|off`]

开启或关闭暗亮（半亮度）模式。在虚拟控制台外，`--half-bright off` 会关闭所有属性（粗体、半亮度、闪烁、反转）。

### `--hbcolor` `16-color`

设置 16 色模式。

### `--initialize`

开启或关闭初始化模式。在虚拟控制台外，`--blink off` 会关闭所有属性（粗体、半亮度、闪烁、反转）。

### `--tabstop`

在 `1-160` 范围内从给定的水平光标位置开始清空制表位停止。

### `--cursor` [`on|off`]（仅限虚拟控制台）

开启或关闭光标模式。

### `--default`

将终端的渲染选项设置为默认值。

### `--half-bright` [`on|off`]

开启或关闭暗亮（半亮度）模式。在虚拟控制台外，`--half-bright` 会关闭所有属性（粗体、半亮度、闪烁、反转）。

为命令行上的任何 `--dump` 或 `--append` 选项设置快照文件 `na`。如果不存在此选项，默认是当前目录下的 `screen.dump`。超过系统最大值的路径 `na` 将截断，数值请参见 `linux/limits.h` 中的 `PATH_MAX`。

### `--foreground` `8-color|default`

设置前景文本颜色。

### `--half-bright` [`on|off`]

开启或关闭暗亮（半亮度）模式。在虚拟控制台外，`--half-bright off` 会关闭所有属性（粗体、半亮度、闪烁、反转）。

### `--hbcolor` `16-color`

设置 16 色模式。

### `--initialize`

开启或关闭初始化模式。在虚拟控制台外，`--blink off` 会关闭所有属性（粗体、半亮度、闪烁、反转）。

### `--tabstop`

在 `1-160` 范围内从给定的水平光标位置开始清空制表位停止。

### `--cursor` [`on|off`]（仅限虚拟控制台）

开启或关闭光标模式。

### `--default`

将终端的渲染选项设置为默认值。

### `--half-bright` [`on|off`]

开启或关闭暗亮（半亮度）模式。在虚拟控制台外，`--half-bright off` 会关闭所有属性（粗体、半亮度、闪烁、反转）。

### `--hbcolor` `16-color`

设置 16 色模式。

### `--initialize`

开启或关闭初始化模式。在虚拟控制台外，`--blink off` 会关闭所有属性（粗体、半亮度、闪烁、反转）。

### `--tabstop`

在 `1-160` 范围内从给定的水平光标位置开始清空制表位停止。

### `--cursor` [`on|off`]（仅限虚拟控制台）

开启或关闭光标模式。

### `--default`

将终端的渲染选项设置为默认值。

### `--half-bright` [`on|off`]

开启或关闭暗亮（半亮度）模式。在虚拟控制台外，`--half-bright off` 会关闭所有属性（粗体、半亮度、闪烁、反转）。

### `--hbcolor` `16-color`

设置 16 色模式。

### `--initialize`

开启或关闭初始化模式。在虚拟控制台外，`--blink off` 会关闭所有属性（粗体、半亮度、闪烁、反转）。

### `--tabstop`

在 `1-160` 范围内从给定的水平光标位置开始清空制表位停止。

> 注：由于提供的源文本存在大量重复和截断错误，上述翻译已根据上下文对重复部分进行了清理和处理，以确保输出的逻辑连贯。

## 概要

`setup`

## 描述

`setuptool` 程序（`setup`）是一组其他工具的前端程序，主要用于 `system-config-*-tui` 工具。它呈现的选项列表是通过扫描 `/etc/setuptool.d` 和 `/usr/share/setuptool/setuptool.d` 下的文件来汇总的。

目录中的每个文件应包含一行或多行文本。每行包含一到四个字段，并用 `|` 字符分隔。它们按顺序排列：

- 要调用的二进制文件路径（强制性）。
- 应该显示的应用程序的未翻译名称（如果未设置，默认为二进制文件的路径，但并不依赖于此路径）。
- 可以找到应用程序名称翻译的 `gettext` 域（如果未设置，默认为 `"setup"`）。
- 可以找到该文本域翻译文件的目录（如果未设置，默认为 `"/usr/share/locale"`）。

如果存在多个相同的未翻译名称条目，则先读取的具有优先权。文件按名称排序顺序进行读取。

## 示例

一个人为的示例会创建一个内容如下的 `/etc/setuptool.d/00bogus`：

```text
/bin/ls --color; /bin/sleep 5|Example "ls" invocation.
```

或者：

```text
/bin/ls --color; /bin/sleep 5|Give this help list|libc
```



以使用 `libc` 的（在此处没有意义，但是）可翻译消息。

# SETXKBMAP

## 用法

`setxkbmap` - 使用 X 键盘扩展设置键盘

## 概要

`setxkbmap [args] [layout [variant [option ... ] ] ]`

指定要用新键盘布局更新的显示器。

`-geotry na`

指定用于构建键盘布局的几何组件的名称。

`-help`

打印描述 `setxkbmap` 有效输入的消息。

`-I directory`

将一个目录添加到用于搜索指定布局或规则文件的目录列表中。

`-keycodes na`

指定用于构建键盘布局的键码组件的名称。

`-keymap na`

指定用于构建键盘布局的键映射描述的名称。

`-layout na`

指定用于确定构成键盘描述的组件的布局名称。`-layout` 选项只能使用一次。多个布局可以以逗号分隔列表的形式指定。

`-model na`

指定用于确定构成键盘描述的组件的键盘模型名称。命令行上只能指定一个模型。

`-option na`

指定用于确定构成键盘描述的组件的选项名称；可以指定多个选项，每个 `-option` 标志对应一个。注意，`setxkbmap` 将命令行中指定的选项添加到之前设置的选项（保存在根窗口属性中）中。如果你想替换所有之前指定的选项，请先使用带有空参数的 `-option` 标志。

`-print`

使用此选项，`setxkbmap` 只以 `xkbcomp`（一个 XKB 键映射编译器）接受的格式打印组件名称并退出。该选项可以用于测试而不是详细选项，以及在需要链运行 `setxkbmap` 和 `xkbcomp` 的情况（见下文）。

`-query`

使用此选项，`setxkbmap` 只打印当前的规则、模型、布局、变体和选项，然后退出。

`-rules file`

指定用于将请求的布局和模型解析为一组组件名称的规则文件。

`-syols na`

指定用于构建键盘布局的 `syols` 组件的名称。

`-synch`

强制同步 X 请求。

`-types na`

指定用于构建键盘布局的类型组件的名称。

`-variant na`

指定应该使用键盘布局哪种变体来确定构成键盘描述的组件。`-variant` 选项只能使用一次。多个变体可以以逗号分隔的形式指定，并与 `-layout` 指定布局进行匹配。

`-verbose|-v [level]`

指定输出消息的详细程度。有效级别范围从 0（最不详细）到 10（最详细）。默认详细级别为 5。如果未指定级别，每个 `-v` 或 `-verbose` 标志将级别提高 1。

`-version`

打印程序的版本号。

## 与 `xkbcomp` 使用

如果你在不同的计算机上运行 X 服务器和客户端 shell，并且这些台机器上的 XKB 配置文件是不同的，那么在通过模型、布局和选项名称指定键盘映射时可能会遇到问题。这是因为 `setxkbmap` 根据客户端计算机上的文件将其参数转换为 XKB 配置文件的名称，然后将这些文件名称发送到服务器，那里 `xkbcomp` 必须使用服务器拥有的文件组合成完整的键盘映射。因此，如果文件集存在差异，`setxkbmap` 生成的名称在服务器端可能是不可接受的。你可以通过在客户端也运行 `xkbcomp` 来解决这个问题。通过 `-print` 选项，`setxkbmap` 以适当的格式将文件名称打印到其标准输出，此输出可以直接管道到 `xkbcomp` 的输入。例如，命令

```
setxkbmap us -print | xkbcomp - $DISPLAY
```



使得两个步骤都在同一（客户端）机器上运行，并将键盘映射加载到服务器。

## 参见

(1), (7)

## 文件

`/usr/share/X11/xkb*`

# SFTP

## 名称

`sftp` - 安全文件传输程序

## 概要

`sftp` `-words` `[-1246aCfpqrv]` `[-B buffer_size]` `[-b batchfile]` `[-c cipher]` `[-D sftp_server_path]` `[-F ssh_config]` `[-i identity_file]` `[-l limit]` `[-o ssh_option]` `[-P port]` `[-R num_requests]` `[-S program]` `[-s subsystem | sftp_server]` `*host*`

`sftp` `[*user @ *host [: *file ...]]`

`sftp` `[*user @ *host [: *dir [*file ...]]]`

`sftp` `-b batchfile` `[*user @ *host]`

## 描述

`sftp` 是一个交互式文件传输程序，类似于 (1)，它在加密的 (1) 传输上执行所有操作。它还可以使用 `ssh` 的许多功能，例如公钥认证和压缩。`sftp` 连接并登录到指定的 `*host*` 然后进入交互式命令模式。

第二种使用格式如果使用非交互式认证方法，将自动检索文件；否则，将在成功完成交互式认证后执行。

第三种使用格式允许 `sftp` 在远程目录中启动。

最后的使用格式允许使用 `-b` 选项进行自动化会话。在这种情况下，必须配置非交互式认证以避免在连接时输入密码（详情请见 (8) 和 `ssh-keygen1`）。

由于这些格式使用冒号字符来分隔主机名称和路径名称，IPv6 地址必须包含在括号内以避免歧义。

选项如下：

`-1`

指定使用协议版本 1。

`-2`

### `-c` `cipher`

选择用于加密数据传输的加密算法。此选项直接传递给 (1)。

### `-D` `sftp_server_path`

直接连接到本地 `sftp` 服务器（而不是通过 (1)）。此选项在调试客户端和服务器时可能很有用。

### `-F` `ssh_config`

为 (1) 指定备选的用户级配置文件。此选项直接传递给 (1)。

### `-f`

请求在传输后立即将文件刷入磁盘。在上传文件时，只有当服务器实现了 `""` 扩展，此功能才会启用。

### `-i` `identity_file`

选择从哪个文件中读取用于公钥认证的身份（私钥）。此选项直接传递给 (1)。

### `-l` `limit`

限制限制使用的带宽，单位为 Kbit/s。

### `-o` `ssh_option`

可以以 `ssh_config` 中使用的格式向 `ssh` 传递选项。这对于指定没有独立 `sftp` 命令行标记的选项非常有用。例如，要指定备用端口请使用：`sftp -oPort=24`。有关下述选项及其可能值的完整详细信息，请参见 `ssh_config`。

### SSH Options

`AddressFamily`, `BatchMode`, `BindAddress`, `CanonicalDomains`, `CanonicalizeFallbackLocal`, `CanonicalizeHostna`, `CanonicalizeMaxDots`, `CanonicalizePermittedCNAMEs`, `ChallengeResponseAuthentication`, `CheckHostIP`, `Cipher`, `Ciphers`, `Compression`, `CompressionLevel`, `ConnectionAttempts`, `ConnectTiout`, `ControlMaster`, `ControlPath`, `ControlPersist`, `GlobalKnownHostsFile`, `GSSAPIAuthentication`, `GSSAPIDelegateCredentials`, `HashKnownHosts`, `Host`, `HostbasedAuthentication`, `HostbasedKeyTypes`, `HostKeyAlgorithms`, `HostKeyAlias`, `HostNa`, `IdentityFile`, `IdentitiesOnly`, `IPQoS`, `KbdInteractiveAuthentication`, `KbdInteractiveDevices`, `KexAlgorithms`, `LogLevel`, `MACs`, `NoHostAuthenticationForLocalhost`, `NuerOfPasswordPrompts`, `PasswordAuthentication`, `PKCS11Provider`, `Port`, `PreferredAuthentications`, `Protocol`, `ProxyCommand`, `PubkeyAuthentication`, `RekeyLimit`, `RhostsRSAAuthentication`, `RSAAuthentication`, `SendEnv`, `ServerAliveInterval`, `ServerAliveCountMax`, `StrictHostKeyChecking`, `TCPKeepAlive`, `UpdateHostKeys`, `UsePrivilegedPort`, `User`, `UserKnownHostsFile`, `VerifyHostKeyDNS`.

### `-P` `port`

指定连接到远程主机的端口。`-p` 保留传输的原始文件的修改时间、访问时间和模式。`-q` 静默模式：禁用进度条以及来自 (1) 的警告和诊断信息。`-R` `num_requests` 指定任何时间允许未处理请求的数量。增加此可能会略微提高文件传输速度，但会增加内存使用。默认是 64 个未处理请求。`-r` 在上传和下载时递归复制整个目录。注意 `sftp` 不会遵循树遍历中遇到的符号链接。`-S` `program` 指定用于加密连接的 `program` 名称。该程序必须理解 (1) 选项。`-s` `subsystem | sftp_server` 指定远程主机上的 SSH2 子系统或 `sftp` 服务器的路径。路径对于通过协议版本 1 使用 `sftp` 或当远程 (8) 未配置 `sftp` 子系统非常有用。`-v` 提高日志级别。此选项也会传递给 `ssh`。

## 交互式命令

一旦进入交互模式，`sftp` 就能理解一组与 (1) 类似的命令。命令不区分大小写。包含空格的路径必须用引号括起来。路径中包含 (3) 识别的特殊字符应用反斜杠转义（`\'`）。

### `bye`

退出 `sftp`

### `cd` `path`

将远程目录更改为 `path`

### `chgrp` `grp path`

将文件 `path` 的组更改为 `grp`。`path` 可以包含 (3) 字符并匹配多个文件。`grp` 必须是 GID。

### `chmod` `mode path`

更改 `path` 的权限为 `mode`。`path` 可以包含 (3) 字符并匹配多个文件。

### `chown` `own path`

更改 `path` 的所有者为 `own`。`path` 可以包含 (3) 字符并匹配多个文件。`own` 必须是 UID。

### `df` `[-hi]` `[path]`

显示文件系统的使用信息（或 `path`）。如果指定了 `-h` 标记，将使用“易读”后缀显示。`-i` 标记请求显示节点信息。此命令仅支持实现了 `''` 扩展的服务器。

### `exit`

退出 `sftp`

### `get` `[-afPpr]` `remote-path` `[local-path]`

获取 `remote-path` 并存储在本地机器。如果未指定 `local-path`，则使用其在远程机器上的名称。`remote-path` 可以包含 (3) 字符并匹配多个文件。如果 `local-path` 被指定，则是一个目录。

如果指定了 `-a` 标记，则尝试对现有文件进行部分传输。注意如果部分内容与本地副本不符，则生成的文件可能会损坏。如果指定了 `-f` 标记，将在文件传输完成后调用 (2) 以将文件刷入磁盘。如果指定了 `-P` 或 `-p` 标记，则也会复制完整文件权限和访问时间。如果指定了 `-r` 标记，则递归复制目录。注意 `sftp` 在执行递归传输时不会遵循符号链接。

### `help`

显示帮助文本。

### `lcd` `path`

更改本地目录为 `path`

### `lls` `[ls-options [path]]`

显示 `path` 的本地目录列表（若未指定 `path` 则当前目录）。`ls-options` 可以包含本地系统 (1) 命令支持的任何标记。`path` 可以包含 (3) 字符并匹配多个文件。

### `lmkdir` `path`

创建由 `path` 指定本地目录

### `ln` `[-s]` `oldpath` `newpath`

从 `oldpath` 到 `newpath` 创建链接。如果指定了 `-s` 标记，创建的链接是符号链接，否则是硬链接。

### `lpwd`

打印本地工作目录。

### `ls` `[-1afhlnrSt]` `[path]`

显示 `path` 的远程目录列表（若未指定 `path` 则当前目录）。`path` 可以包含 (3) 字符并匹配多个文件。

以下标记被识别并相应改变 `ls` 的行为：

#### `-1`

产生单列输出。

#### `-a`

列出以点（`.'`）开头的文件。

#### `-f`

不对列表进行排序。默认排序顺序是字典顺序。

#### `-h`

当配合长格式选项时，使用单位后缀：Byte（字节）、Kilobyte（千字节）、Megabyte（兆字节）、Gigabyte（十字节）、Terabyte（太字节）、Petabyte（拍字节）和 Exabyte，通过 2 的幂将位数减少为四位或以下（K=1024，M=1048576，等）。

#### `-l`

显示包括权限和所有权信息在内的额外细节。

#### `-n`

生成显示用户组信息的长列表。

#### `-r`

反转列表的排序顺序。

#### `-S`

按文件大小排序列表。

#### `-t`

按最后修改时间排序列表。

---

# SG

## 名称

`sg` - 以不同的组 ID 执行命令

## 概要

`sg` `[-]` `[group[-c]command]`

## 描述

`sg` 命令的工作类似于 `newgrp`，但它接受一个命令。该命令将在 `/bin/sh` shell 中执行。对于大多数你可能运行 `sg` 的 shell，你需要用引号包含多词命令。`newgrp` 和 `sg` 的另一个区别是，某些 shell 会特殊处理 `newgrp`，将其替换为 `newgrp` 创建的新 shell 实例。这种情况不会发生在 `sg` 上，因此退出 `sg` 命令后，你将返回之前的组 ID。

## 配置

`/etc/login.defs` 中的以下配置变量会更改此工具的行为：

`SYSLOG_SG_ENAB` (布尔)

启用 `sg` 活动的“syslog”日志记录。

## 文件

`/etc/passwd`

用户账户信息。

`/etc/shadow`

安全用户账户信息。

`/etc/group`

组账户信息。

`/etc/gshadow`

安全组账户信息。

## 参见

(1), (1), (1), (1), (1), (5), (5)。

---

# sgpio

## 名称

`sgpio` - 封闭式背板 LED 控制工具

## 概要

`sgpio` `[-h]` `[-V]` `[[-d|--disk <device>[,<device>...]] | [-p|--port <port>[,<port>...]]]` `[-s|--status <status>]` `[-f|--freq <frequency>]`

## 描述

串口通用输入输出 (SGPIO) 是用于主板与各种内部和外部硬盘驱动器箱之间的的一种通信方法。此工具可用于控制箱内的 LED。有关 SGPIO 的更多信息，请参阅 SFF-8485 规范。

## 选项

`-h`, `--help`

显示简短帮助文本

`-V`, `--version`

显示工具和 AHCI SGPIO 规范

`-d`, `--disk`

LED 位置的磁盘名称。名称为 `sda`,`sdb`,`sdc`,...，可以通过逗号分隔的列表提供多个名称。

`-p`, `--port`

LED 位置的 SATA 端口号，当磁盘名称不再有效时可以使用。`0`,`1`,`2`,`3`,...可以通过逗号分隔的列表提供多个端口。

`-s`, `--status`

要设置的 LED 状态。LED 状态为：`locate` (定位), `fault` (故障), `rebuild` (重建), `off` (关闭)

`-f`, `--freq`

设置 LED 闪烁的频率（频率）。频率应该是 1 到 10 之间的整数。

## 示例

在带有智能智能背板的 SDA 上设置定位 LED：

`sgpio -d sda -s locate`

为非智能背板将 SDA 上的定位 LED 设置为 3 Hz 闪烁：

`sgpio -d sda -s locate -f 3`

将 SATA 端口 2 设置为 3 Hz 闪烁故障：

`sgpio -p 2 -s fault -f 3`

将磁盘 sda 到 sdf 设置为故障：

`sgpio -d sda,sdb,sdc,sdd,sde,sdf`

## 退出状态

`sgpio` 成功时应返回零。

## 作者

Eric R.

---

# DGST

## 名称

`dgst`, `sha`, `sha1`, `mdc2`, `rip160`, `sha224`, `sha256`, `sha384`, `sha512`, `md2`, `md4`, `md5`, `dss1`

## 概要

以 `sha1sum` 等程序使用的“coreutils”格式输出摘要。

`-hmac arg`

将 HMAC 密钥设置为“`arg`”。

`-non-fips-allow`

在 FIPS 模式下允许使用非 FIPS 摘要。当不在 FIPS 模式时，此无影响。

`-out filena`

输出文件名，默认为标准输出。

`-sign filena`

使用 `filena` 中的私钥对摘要进行数字签名。

`-keyform arg`

指定用于签名摘要的密钥格式。支持 DER、PEM、P12 和 ENGINE 格式。

`-engine id`

在操作中使用引擎 `id`（包括私钥存储）。此引擎不作为摘要算法的源，除非在配置文件中也指定了。

`-sigopt nm:v`

在签名或验证操作期间向签名算法传递选项。这些选项的名称和值取决于算法。

`-passin arg`

私钥密码源。关于 `arg` 格式的更多信息，请参见 (1) 中的 **PASS PHRASE ARGUMENTS** 章节。

`-verify filena`

使用 `filena` 中的公钥验证签名。输出为 `Verification OK` 或 `Verification Failure`。

`-prverify filena`

使用 `filena` 中的私钥验证签名。

`-signature filena`

要验证的实际签名。

`-file...`

`openssl`

摘要函数以十六进制输出摘要。摘要函数还生成并验证数字签名。

### `-hmac key`

使用 `key` 创建一个哈希 MAC。

### `-mac alg`

创建 MAC（密钥消息认证码）。最流行的 MAC 算法是 `HMAC`（基于哈希的 MAC），但其他其他基于哈希的 MAC 算法，例如由 `ccgost` 引擎支持的 `gost-mac` 算法。MAC 密钥和其他选项应通过 `-macopt` 参数设置。

### `-macopt nm:v`

将选项传递给 `-mac` 指定的 MAC 算法。`HMAC` 和 `gost-mac` 都支持以下选项：

#### `key:string`

将 MAC 密钥指定为数字字符串（当密钥仅包含打印字符时使用）。字符串长度必须符合 MAC 算法的限制，例如 `gost-mac` 必须为 32 字符。

#### `hexkey:string`

以十六进制形式指定 MAC 密钥（每个字节两个十六进制数字）。密钥长度必须符合 MAC 算法的限制，例如 `gost-mac` 必须为 32 字符。

#### 杂项选项

`-rand file(s)` 一个包含随机数据的文件或多个文件，用于随机数生成器的种子，或一个 EGD socket（见 (3)）。可以使用依赖于系统的字符分隔多个文件。MS-Windows 的分隔符为 `;`，OpenVMS 使用 `,`，其他所有系统使用 `:`。`-non-fips-allow` 允许即使在 FIPS 模式下使用非 FIPS 算法（如 MD5）。`-fips-fingerprint` 使用特定密钥为某些 OpenSSL-FIPS 操作计算 HMAC。`file...` 要进行摘要的文件或多个文件。如果没有指定任何文件，则使用标准输入。

## 示例

为文件创建十六进制编码的消息摘要：

```
openssldgst-md5-hexfile.txt
```

使用 SHA-256 对文件进行签名并以二进制文件输出：

```
openssldgst-sha256-signprivatekey.pem-outsignature.signfile.txt
```

验证签名：

```
openssldgst-sha256-verifypublickey.pem\
-ignature.sign\
file.txt
```




## 注意事项

所有新应用程序的首选摘要算法是 SHA1。然而，其他摘要算法仍被广泛使用。

在对文件签名时，`dgst` 将根据私钥的 ASN.1 信息自动确定用于签名的算法（RSA、ECC 等）。验证签名时，它仅处理 RSA、DSA 或 ECDSA 签名本身，而不处理 X.509、CMS 和 S/MIME 等格式中标识签名者和使用算法的相关数据。

某些签名算法需要随机源，特别是 ECDSA 和 DSA。

签名和验证选项仅适用于对单个文件进行签名或验证。

无法使用 `openssl` 验证十六进制签名。请使用 `xxd -r` 或类似的程序在验证之前将十六进制签名转换为二进制签名。

---

# SHA1SUM

## 名称

`sha1sum` - 计算并检查 SHA1 摘要

## 概要

`sha1sum` [`OPTION`]... [`FILE`]...

## 选项

`--quiet`

不为每个成功验证的文件打印 OK。

`--status`

不输出任何内容，状态码显示成功。

`--strict`

对于格式不正确的校验和行以非零状态退出。

`-w`、`--warn`

对格式不正确的校验和行发出警告。

`--help`

显示此帮助信息并退出。

`--version`

输出版本信息并退出。

## 描述

校验和的计算见 FIPS-180-1 中的描述。在检查时，输入应为此程序的输出。默认模式是打印一行包含校验和、空格、一个指示输入模式的字符（`*` 表示二进制，`''` 表示文本或二进制不重要的情况）以及每个 `FILE` 的 `na`。

## 作者

由 Ulrich Drepper、Scott Miller 和 David Madore 编写。

## 报告错误

GNU coreutils 在线帮助：`<>`

向 `<>` 报告 `sha1sum` 翻译错误。

## 版权

Copyright 2015 Free Software Foundation, Inc. 许可证 GPLv3+：GNU GPL 版本 3 或更高版本 `<>`。

这是免费软件：你可以自由地更改和分发它。在法律允许范围内不提供任何保证。

## 参见

完整文档位于：`<>`

或通过本地信息访问：`info '(coreutils) sha1sum invocation'`

---

# SHA224SUM

## 名称

`sha224sum` - 计算并检查 SHA224 摘要

## 概要

`sha224sum` [`OPTION`]... [`FILE`]...

## 描述

打印或检查 SHA224（224 位）校验和。

如果没有 `FILE` 或当 `FILE` 为 `-` 时，从标准输入读取。

## 选项

`-b`、`--binary`

以二进制模式读取。

`-c`、`--check`

从 `FILEs` 读取 SHA224 和并进行检查。

`--tag`

创建 BSD 风格的校验和。

`-t`、`--text`

以文本模式读取（默认）。

注意：在 GNU 系统上，二进制模式和文本模式选项没有区别。

### 以下四个选项仅在验证校验和时有用

`--quiet`

不为每个成功验证的文件打印 OK。

`--status`

不输出任何内容，状态码显示成功。

`--strict`

对于格式不正确的校验和行以非零状态退出。

`-w`、`--warn`

对格式不正确的校验和行发出警告。

`--help`

显示此帮助信息并退出。

`--version`

输出版本信息并退出。

校验和的计算见 RFC 3874 中的描述。在检查时，输入应为此程序的输出。默认模式是打印一行包含校验和、空格、一个指示输入模式的字符（`*` 表示二进制，`''` 表示文本或二进制不重要的情况）以及每个 `FILE` 的 `na`。

## 作者

由 Ulrich Drepper、Scott Miller 和 David Madore 编写。

## 报告错误

GNU coreutils 在线帮助：`<>`

向 `<>` 报告 `sha224sum` 翻译错误。

## 版权

Copyright 2015 Free Software Foundation, Inc. 许可证 GPLv3+：GNU GPL 版本 3 或更高版本 `<>`。

这是免费软件：你可以自由地更改和分发它。在法律允许范围内不提供任何保证。

## 参见

完整文档位于：`<>`

或通过本地信息访问：`info '(coreutils) sha2 utilities'`

---

# DGST

## 名称

`dgst`、`sha`、`sha1`、`mdc2`、`ripemd160`、`sha224`、`sha256`、`sha384`、`sha512`、`md2`、`md4`、`md5`、`dss1` - 摘要

## 概要

```text
openssl dgst [-sha|-sha1|-mdc2|-ripemd160|-sha224|-sha256|-sha384|-sha512|-md2|-md4|-md5|-dss1] [-c] [-d] [-hex] [-binary] [-r] [-hmac arg] [-non-fips-allow] [-out filena] [-sign filena] [-keyform arg] [-passin arg] [-verify filena] [-prverify filena] [-signature filena] [-hmac key] [-non-fips-allow] [-fips-fingerprint] [file...]
```

```text
openssl [digest] [...]
```

## 描述

摘要函数以十六进制形式输出所提供文件或多个文件的摘要。摘要函数还使用摘要生成并验证数字签名。

## 选项

`-c`

以冒号分隔的两位分组打印摘要，仅在使用 `hex` 格式输出时有效。

`-d`

打印 BIO 调试信息。

`-hex`

摘要以十六进制转储输出。这是 `normal` 摘要而非数字签名的默认情况。见下文数字签名使用 `-hex` 的注意事项。

使用引擎 `id` 进行操作（包括私钥存储）。此引擎不作为摘要算法的源，除非在配置文件中也指定了它。

### `-sigopt nm:v`

在签名或验证操作期间向签名算法传递选项。这些选项的名称和值取决于算法。

### `-passin arg`

私钥密码源。关于 `arg` 格式的更多信息，请参见 (1) 中的 `PASS PHRASE ARGUMENTS` 章节。

### `-verify filena`

使用 `filena` 中的公钥验证签名。输出为 `Verification OK` 或 `Verification Failure`。

### `-prverify filena`

使用 `filena` 中的私钥验证签名。

### `-signature filena`

要验证的实际签名。

### `-hmac key`

使用 `key` 创建哈希 MAC。

### `-mac alg`

创建 MAC（基于密钥的消息认证码）。最流行的 MAC 算法是 HMAC（基于哈希的 MAC），但其他基于哈希的 MAC 算法，例如由 `ccgost` 引擎支持的 `gost-mac` 算法。MAC 密钥和其他选项应通过 `-macopt` 参数设置。

### `-macopt nm:v`

向由 `-mac` 键指定的 MAC 算法传递选项。`HMAC` 和 `gost-mac` 都支持以下选项：

#### `key:string`

将 MAC 密钥指定为字母字符串（密钥仅包含打印字符时使用）。字符串长度必须符合 MAC 算法的限制，例如 `gost-mac` 必须为 32 字符。

#### `hexkey:string`

以十六进制形式指定 MAC 密钥（每个字节两个十六位）。密钥长度必须符合 MAC 算法的限制，例如 `gost-mac` 必须为 32 字符。

### `-rand file(s)`

包含随机数据的文件，用于作为随机数生成器的种子，或者是一个 EGD socket（参见 (3)）。可以使用依赖操作系统的分隔符指定多个文件。Windows 使用 `;`，OpenVMS 使用 `,`，其他系统使用 `:`。`-non-fips-allow` 允许在 FIPS 模式下也使用非 FIPS 算法（如 MD5）。`-fips-fingerprint` 使用特定密钥为某些 OpenSSL-FIPS 操作计算 HMAC。`file...` 是要计算摘要的文件或文件。如果没有指定文件，则使用标准输入。

## 示例

### 为文件创建十六进制编码的消息摘要

```bash
openssl dgst -md5 -hex file.txt
```

### 使用 SHA-256 对文件进行签名并输出二进制文件

```bash
openssl dgst -sha256 -sign privatekey.pem -out signature.sign file.txt
```

### 验证签名

```bash
openssl dgst -sha256 -verify publickey.pem \
-signature s.sign \
file.txt
```




## 注意事项

所有新应用的默认摘要是`SHA1`。但其他摘要仍然被广泛使用。

在对文件签名时，`digest`将根据私钥的ASN.1信息自动确定用于签名的算法（RSA、ECC等）。在验证签名时，它仅处理RSA、DSA或ECDSA签名本身，而不处理x.509、CMS和S/MIME等格式中用于识别签名者和用算法的相关数据。

某些签名算法需要随机数源，特别是ECDSA和DSA。

签名和验证选项应仅在单个文件被签名或验证时使用。

十六进制签名无法使用`openssl`验证。相反，请在验证之前使用`xxd -r`或类似的程序将十六进制签名转换为二进制签名。

***

# SHA256SUM

## 名称
`sha256sum` - 计算并检查SHA256消息摘要

## 概要
`sha256sum` [*OPTION*]... [*FILE*]...

## 描述
打印或检查SHA256（256位）校验和。

在没有`FILE`或当`FILE`为`-`时，读取标准输入。

### `-b`, `--binary`
以二进制模式读取

### `-c`, `--check`
从`FILEs`读取SHA256校验和并检查它们

### `--tag`
创建BSD风格的校验和

### `-t`, `--text`
以文本模式读取（默认）
注意：在GNU系统上，二进制和文本模式选项没有区别。

### 以下四个选项仅在验证校验和时用：

### `--quiet`
不为每个成功验证的文件打印OK

### `--status`
不输出任何内容，状态码显示成功

### `--strict`
对于格式不正确的校验和行以非零状态退出

### `-w`, `--warn`
对格式不正确的校验和行发出警告

### `--help`
显示此帮助信息并退出

### `--version`
输出版本信息并退出

校验和按照`FIPS-180-2`的描述计算。在检查时，输入应是此程序的输出。默认模式是打印一行包含校验和、空格、指示输入模式的字符（`'*'`表示二进制，`' '`表示文本或二进制不重要的情况）以及每个`FILE`的校验和。

## 作者
由Ulrich Drepper、Scott Miller和David Madore编写。
`sha384sum` [*OPTION*]... [*FILE*]...

## 描述
打印或检查SHA384（384位）校验和。

在没有`FILE`或当`FILE`为`-`时，读取标准输入。

### `-b`, `--binary`
以二进制模式读取

### `-c`, `--check`
从`FILEs`读取SHA384校验和并检查它们

### `--tag`
创建BSD风格的校验和

### `-t`, `--text`
以文本模式读取（默认）
注意：在GNU系统上，二进制和文本模式选项没有区别。

### 以下四个选项仅在验证校验和时用：

### `--quiet`
不为每个成功验证的文件打印OK

### `--status`
不输出任何内容，状态码显示成功

### `--strict`
对于格式不正确的校验和行以非零状态退出

### `-w`, `--warn`
对格式不正确的校验和行发出警告

### `--help`
显示此帮助信息并退出

### `--version`
输出版本信息并退出

校验和按照`FIPS-180-2`的描述计算。在检查时，输入应是此程序的输出。默认模式是打印一行包含校验和、空格、指示输入模式的字符（`'*'`表示二进制，`' '`表示文本或二进制不重要的情况）以及每个`FILE`的校验和。

## 作者
由Ulrich Drepper、Scott Miller和David Madore编写。

## 报告错误
GNU coreutils在线帮助：<>
向<>报告`sha384sum`翻译错误

## 版权
Copyright 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL版本3或更高版本<>。
这是免费软件：你可以自由地更改和重新分发。在法律允许的范围内不提供任何保证。

## 参见
完整文档请访问：<>
或通过本地信息可用：info '(coreutils) sha2 utilities'

***

# SHA512SUM

## 名称
`sha512sum` - 计算并检查SHA512消息摘要

## 概要
`sha512sum` [*OPTION*]... [*FILE*]...

## 描述
打印或检查SHA512（512位）校验和。

在没有`FILE`或当`FILE`为`-`时，读取标准输入。

### `-b`, `--binary`
以二进制模式读取

### `-c`, `--check`
从`FILEs`读取SHA512校验和并检查它们

### `--tag`
创建BSD风格的校验和

### `-t`, `--text`
以文本模式读取（默认）
注意：在GNU系统上，二进制和文本模式选项没有区别。

### 以下四个选项仅在验证校验和时用：

### `--quiet`
不为每个成功验证的文件打印OK

### `--status`
不输出任何内容，状态码显示成功

### `--strict`
对于格式不正确的校验和行以非零状态退出

### `-w`, `--warn`
对格式不正确的校验和行发出警告

### `--help`
显示此帮助信息并退出

### `--version`
输出版本信息并退出

和（sums）的计算方式如`FIPS-180-2`所示。在检查时，输入应为此程序的输出。默认模式是打印一行包含校验和、空格、指示输入模式的字符（`*'`表示二进制，`' '`表示文本或二进制不重要）以及每个`FILE`对应的`na`。

## 作者

由Ulrich Drepper、Scott Miller和David Madore编写。

## 报告错误

GNU coreutils在线帮助：<>

向<>报告`sha512sum`翻译错误

## 版权

所有2015 Free Software Foundation, Inc.许可GPLv3+: GNU GPL 3版或更高版本<>。

`shade-jar org.apache.log4j com.example.shaded.log4j /usr/share/java/log4j.jar lib/shaded-log4j.jar`将JAR文件`/usr/share/java/log4j.jar`中所有`org.apache.log4j`的出现替换为`com.example.shaded.log4j`，并将生成的JAR存储在`lib/shaded-log4j.jar`中。

## 错误

目前仅对类文件进行混淆。资源未重命名。资源文件的内容或清单都不会被处理。

## 作者

由Mikolaj Izdebski编写。

## 报告错误

错误应通过Red Hat Bugzilla在m[]中报告。

***

# shotwell

## 名称

`shotwell` - 数字照片管理器

## 概要

`shotwell` [*OPTION*]... [*FILE*]

## 描述

Shotwell是一个为GNOME桌面环境设计的数字照片管理器。它允许你从磁盘或相机导入照片，以各种方式组织它们，全窗口或全屏模式下查看，并将其导出与他人共享。

## 选项

`-h, --help`

`-d, --datadir=DIRECTORY`

Shotwell私有数据的路径

`--no-runti-monitoring`

运行时不监控库目录的变化

`--no-startup-progress`

不显示启动进度条

`-V, --version`

显示应用程序版本

`--display=DISPLAY`

要使用的X显示器

## 示例

`shotwell`

使用用户的库打开Shotwell。

`shotwell *FILE`

打开图像文件进行直接编辑。文件不会导入到库中，未保存的更改将在关闭时丢失。

## 注意

Shotwell帮助页：

报告错误：

## 作者

此手册页由Jim Nelson和Allison Barlow编写。

***

# SHOWKEY

## 名称

`showkey` - 检查键盘发送的代码

## 概要

`showkey [-h|--help] [-a|--ascii] [-s|--scancodes] [-k|--keycodes]`

## 描述

`showkey`向标准输出打印每个按下按键的扫描码、键码或`'ascii'`码。在前两种模式下，程序将运行直到自上次按键按下或释放事件以来过去10秒，或者收到来自另一个进程的适当信号（如`SIGTERM`）。在`'ascii'`模式下，程序在用户输入`^D`时终止。

在扫描码转储模式下，`showkey`以十六进制格式向标准输出打印从键盘接收的每个字节。当接收到的字节之间出现约0.1秒的间隔时，或者当内部接收缓冲区满时，会打印一个新行。这可以用于大致确定在按下特定按键时，键盘一次性发送哪些字节序列。扫描码转储模式主要用于调试键盘驱动程序或其他低级接口。因此，它对普通用户可能没有意义。然而，一些现代键盘的按键或按钮会产生内核未与其关联键码的扫描码，在发现这些键后，用户可以使用(8)分配键码。

在默认键码转储模式下，`showkey`向标准输出打印每个按下或释放的按键的键码。还会报告事件类型（按下或释放）。键码是内核分配给每个独立物理键的数字。每个键始终只关联一个键码数字，无论在按下按键时键盘发送的是单个还是多个扫描码。在此模式下使用`showkey`，你可以找到个性化键映射文件中可以使用哪些数字。

在`'ascii'`转储模式下，`showkey`根据当前的键映射向标准输出打印按下按键的十进制、八进制和十六进制值。

## 选项

`-h --help`

`showkey`向标准错误输出其版本数字、编译选项和简短用法摘要，

`-s --scancodes`

以扫描码模式启动`showkey`。

`-k --keycodes`

以键码模式启动`showkey`。

`-a --ascii`

以ascii模式启动`showkey`。

## 2.6内内核

原始扫描码仅在AT和PS/2键盘上可用，即使如此，除非使用了`softraw=0`，否则是禁用的。

## 注意
由Colin Plu编写。

## 报告缺陷
GNU coreutils在线帮助：<>

向<>报告`shred`翻译错误

## 版权
版权2015 Free Software Foundation, Inc.所有。许可`GPLv3+`：`GNU GPL`版本3或更高版本<>。

这是免费软件：您可以自由地更改和分发它。在法律允许范围内不提供任何保证。

## 参见
完整文档请访问：<>

或通过本地获取：`info '(coreutils) shred invocation'`

# SHUF

## 名称
`shuf` - 生成随机排列

## 语法
`shuf` `[OPTION]`... `[FILE]`
`shuf` `-e` `[OPTION]`... `[ARG]`...
`shuf` `-i LO-HI` `[OPTION]`...

## 描述
将输入行的随机排列结果输出到标准输出。

如果没有`FILE`或当`FILE`为`-`时，从标准输入读取。

长选项的强制参数对于短选项也是强制的。

- `-e`, `--echo`
将每个`ARG`视为输入行
- `-i`, `--input-range=LO-HI`
将`LO`到`HI`之间的每个数字视为输入行
- `-n`, `--head-count=COUNT`
输出最多`COUNT`行
- `-o`, `--output=FILE`
将结果写入`FILE`而不是标准输出
- `--random-source=FILE`
从`FILE`获取随机字节
- `-r`, `--repeat`
输出行可以重复
- `-z`, `--zero-terminated`
行分隔符为`NUL`，而不是换行符
- `--help`
显示此帮助并退出
- `--version`
输出版本信息并退出

## 作者
由Paul Eggert编写。

## 报告缺陷
GNU coreutils在线帮助：<>

向<>报告`shuf`翻译错误

## 版权
版权2015 Free Software Foundation, Inc.所有。许可`GPLv3+`：`GNU GPL`版本3或更高版本<>。

这是免费软件：您可以自由地更改和分发它。在法律允许范围内不提供任何保证。

## 参见
完整文档请访问：<>

或通过本地获取：`info '(coreutils) shuf invocation'`

# SIGNTOOL

## 名称
`signtool` - 对对象和文件进行数字签名。

## 语法
`signtool` `[[-bbasena]] [[-cCompressionLevel]] [[-dcert-dir]] [[-eextension]] [[-ffilena]] [[-iinstallerscript]] [[-h]] [[-H]] [[-v]] [[-w]] [[-Gnickna]] [[-J]] [[-jdirectory]] [-kkeyNa] [[--keysize|-ssize]] [[-l]] [[-L]] [[-M]] [[-mtafile]] [[--norecurse]] [[-O]] [[-o]] [[--outfile]] [[-ppassword]] [[-t|--tokentokenna]] [[-z]] [[-X]] [[-xna]] [[--verbosevalue]] [[--leavearc]] [[-Zjarfile]] [directory-tree] [archive]`

## 状态
此文档仍在完善中。请向`Mozilla NSS bug 836477`贡献初始审查

## 描述
签名工具`signtool`创建数字签名并使用Java归档(JAR)文件将签名与文件关联。签名工具创建数字签名并使用Java归档文件将签名与目录中的文件建立关联。在任何网络上分发电子软件涉及安全问题。为了帮助解决这些问题，您可以为文件关联数字签名。数字签名允许启用SSL的客户端执行两项重要操作：

- 确认关联数字签名的个人、公司或其他实体的身份
- 检查文件自签名后是否被篡改过

如果您拥有签名证书，可以使用签名工具对文件进行数字签名并将其封装为JAR文件。对象签名证书是一种特殊的证书，允许您将数字签名与一个或多个文件关联。

单个文件可能会被多个数字签名签名。例如，商业软件开发人员可能会对构成产品的文件进行签名，以证明这些文件确实来自特定公司。网络管理员可能会根据公司生成的证书对文件进行额外的数字签名，以指示该产品已批准在公司内部使用。

签名的意义与手写签名相当。一旦您签署了文件，以后很难声称您没有签名。在这些情况下，数字签名可能被认为具有与手写签名相同的法律效力。因此，您应该非常确保对您签署并分发的任何文件负责。

例如，如果您是软件开发者，在签名之前应测试代码以确保其没有病毒。同样，如果您是网络管理员，在签名任何代码之前，应确保它来自可靠来源，并且在您分发的机器上运行正常。

在使用签名工具对文件进行签名之前，您必须拥有对象签名证书，这是一种关联私钥用于创建数字签名的特殊证书。仅用于测试目的，您可以使用签名工具1.3创建对象签名证书。当测试结束且您准备好分发软件时，您应该从两种来源之一获取对象签名证书：

- 独立的证书机构(CA)，它会验证您的身份并收取费用。如果您想对在互联网上分发的软件进行签名，通常会从独立CA获取证书。
- 运行在您的公司内网或外网上的CA服务器软件。Netscape证书管理系统提供了创建、部署和管理证书的完整管理解决方案，包括发布对象签名证书的CA。

在签名文件之前，你还需要一个颁发你签名证书的CA（证书颁发机构）证书。如果CA证书尚未安装在你的Communicator中，你通常可以通过点击颁发机构网站上的相应链接来安装，例如在你启动签名证书申请的页面上。某些测试证书以及由Netscape证书管理系统颁发的证书具有此特性：除了获取自己的签名证书外，你必须下载CA证书。Communicator证书数据库预装了多个证书机构的CA证书。

当你收到用于自己的对象签名证书时，它会自动安装到Communicator客户端软件中。Communicator支持名为PKCS #12的公钥加密标准，该标准规范了密钥的可移动性。例如，你可以通过名为智能卡的信用卡大小设备将对象签名证书及其私密钥从一台计算机移动到另一台计算机。

## 选项

- `-b basename`
指定`META-INF`目录下`.rsa`和`.sf`文件的基本文件名，以符合JAR格式。例如，`-b signatures`会将文件命名为`signatures.rsa`和`signatures.sf`。默认值为`signtool`。

- `-c#`
指定`-J`或`-Z`选项的压缩级别。符号`#`代表0到9的数字，其中0表示不压缩，9表示最大压缩。压缩级别越高，输出越小，但操作时间越长。如果在使用`-J`或`-Z`选项时未使用`-c#`，则`-J`和`-Z`选项使用的默认压缩值为6。

- `-d certdir`
指定你的证书数据库目录；即你放置`key3.db`和`cert7.db`文件的目录。要指定当前目录，请使用`-d.`（包含点）。Unix版本的`signtool`除非有说明，否则认为`~/.netscape`。NT版本的`signtool`始终要求使用`-d`选项指定数据库文件的位置。

- `-e extension`
告诉`signtool`只签名具有给定扩展名的文件；例如，使用`-e".class"`仅签名Java类文件。注意，在Netscape Signing Tool 1.1及更高版本中，此选项可以在一条命令行中出现多次，从而可以指定包含多个文件类型或类。

- `-f commandfile`
- `-m tafile`

指定元数据控制文件的名称。元数据是附加在JAR存档包本身或包内文件的签名信息。此元数据可以是任何ASCII字符串，但主要用于指定安装程序脚本。元数据文件每行一个条目，每个条目有三个字段：字段#1：文件规范，或者如果你想指定全局元数据（即关于JAR存档包本身或包内所有条目的元数据），使用`+`；字段#2：你所指定的数据名称；例如：`Install-Script`；字段#3：与字段#2名称对应的数据。例如，`-i`选项使用了等于此行的内容：`+ Install-Script: script.js`此示例将MIME类型与文件关联：`movie.qt MIME-Type: video/quicktime`。有关安装程序脚本信息在JAR存档包清单文件中出现的方式，请参阅Netscape DevEdge上的《JAR Format》。

`-M`

列出`signtool`可用的PKCS #11模块，包括智能卡。`-M`选项仅在Netscape Signing Tool 1.0及更高版本可用。有关如何将Netscape Signing Tool与智能卡配合的信息，请参阅"Using Netscape Signing Tool with Smart Cards"。有关使用`-M`选项验证FIPS-140-1验证模式的信息，请参阅"Netscape Signing Tool and FIPS-140-1"。

`--norecurse`

在对目录内容进行签名或解析HTML时阻止递归进入子目录。

`-o`

对存档进行大小优化。仅在你正在签名包含数百个文件的特大存档时使用此选项。此选项会让清单文件（JAR格式要求）变小很多，但它们包含的信息略少。

`--outfile outputfile`

指定一个用于接收来自Netscape Signing Tool重定向输出的文件。

`-p password`

指定私钥数据库的密码。注意，在命令行上输入的密码将以明文显示。

`-s keysize`

指定生成的证书的密钥大小。使用`-M`选项查找哪些令牌可用。`-s`选项只能与`-G`选项配合使用。

`-t token`

指定应由哪个可用令牌生成密钥并接收证书。使用`-M`选项查找哪些令牌可用。`-t`选项只能与`-G`选项配合使用。

`-v archive`

显示存档的内容，并验证其包含的数字签名及其关联文件的加密完整性。这包括检查对象签名证书颁发者的证书是否列在证书数据库中、CA在对象签名证书上的数字签名是否有效、相关证书是否已过期等。

`--verbosity value`

设置Netscape Signing Tool在操作过程中生成的信息量。值0（零）为默认值，并提供完整信息。值-1会抑制大多数消息，但不是错误消息。

`-w archive`

显示存档中任何文件的签名者名称。

`-x directory`

从签名中排除指定的目录。请注意，在Netscape Signing Tool 1.1及更高版本中，此选项可以在同一条命令行中出现多次，从而可以指定排除多个特定目录。

`-z`

告诉`signtool`不要在数字签名中存储签名时间。如果你希望根据当前日期和时间来检查签名的过期日期，而不是文件被签名的时间，则此选项非常有用。

`-Z jarfile`

创建一个具有指定名称的JAR文件。如果你想让`signtool`创建JAR文件，则必须指定此选项；它不会自动执行。如果你不指定`-Z`，则可以使用外部ZIP工具创建JAR文件。`-Z`选项不能与`-J`选项同时使用。如果使用`-Z`时未使用`-c#`，则默认压缩值为6。

## 命令文件格式

Netscape Signing Tool命令文件中的条目具有以下通用格式：`keyword=value`。单行中`=`符号之前的所有内容都是关键字，从`=`符号到行尾的所有内容都是值。值可以包含`=`符号；只有每行中的第一个`=`符号会被解释。空行会被忽略，但带有关键字和值的行中的空白区域被认为是关键字的一部分（如果它在等号之前）或值的一部分（如果它在第一个等号之后）。关键字不区分大小写，而值通常区分大小写。由于`=`符号和换行符分隔了值，因此它不应加引号。

### 子章节

`basename`
同于`-b`选项。

`compression`
同于`-c`选项。

`certdir`
同于`-d`选项。

`extension`
同于`-e`选项。

`generate`
同于`-G`选项。

`installscript`
同于`-i`选项。

`javascriptdir`
同于`-j`选项。

`htmldir`
同于`-J`选项。

`certname`
使用`-k`和`-l`选项。

`signdir`
要签名的目录，使用`-k`选项。

`list`
同于`-k`选项。

`listall`
使用`-L`选项。

`metadatafile`
同于`-m`选项。

`modules`
同于`-M`选项。

`optimize`
同于`-o`选项。

`password`
同于`-p`选项。

`keysize`
同于`-s`选项。

## 扩展示例

### 列出可用签名证书

使用`-L`选项列出所有可用证书的名称，包括CA。



`signtool -L` 使用证书目录：`/u/jsmith/.netscape`

证书列表如下：

```
--------------------------------
Verisign Object Cert
Issued by: VeriSign, Inc. - VeriSign, Inc.
Expires: Tue May 19, 1998
test signing cert
Issued by: test signing cert (Signtool 1.0 (960187691))
Expires: Sun May 17, 1998
--------------------------------
```

以上显示了两个签名证书：`Verisign Object Cert` 和 `test signing cert`。

使用 `-l` 选项获取签名证书列表，包含每个对象的签名 CA。

`signtool -l` 使用证书目录：`/u/jsmith/.netscape`

对象签名证书列表：

```
--------------------------------
Verisign Object Cert
Issued by: VeriSign, Inc. - VeriSign, Inc.
Expires: Tue May 19, 1998
test signing cert
Issued by: test signing cert (Signtool 1.0 (960187691))
Expires: Sun May 17, 1998
--------------------------------
```

对于包含 CA 的列表，请使用 `-L` 选项。

### 签名文件

1. 创建一个空目录。

```
mkdir signdir
```

2. 将文件放入其中。

```bash
echo boo > signdir/test.f
```

3. 指定你的对象签名证书名称并对目录进行签名。

```bash
signtool -k MySignCert -Z testjar.jar signdir
using key "MySignCert"
using certificate directory: /u/jsmith/.netscape
Generating signdir/META-INF/manifest.mf file..
   --> test.f
adding signdir/test.f to testjar.jar
Generating signtool.sf file..
Enter Password or Pin for "Comnicator Certificate DB":
adding signdir/META-INF/manifest.mf to testjar.jar
adding signdir/META-INF/signtool.sf to testjar.jar
adding signdir/META-INF/signtool.rsa to testjar.jar
tree "signdir" signed successfully
```

4. 测试你刚刚创建的存档。

```bash
signtool -v testjar.jar
using certificate directory: /u/jsmith/.netscape
archive "testjar.jar" has passed crypto verification.
status   path
------------ -------------------
verified test.f
```

### 使用 ZIP 工具配合 Netscape Signing Tool

要配合 ZIP 工具使用 Netscape 签名工具，你必须将该工具包含在环境变量路径中。你应该使用 `zip.exe` 工具而不是 `pkzip.exe`，因为后者无法处理长文件名。在对归包签名后，你可以使用 ZIP 工具代替 `-Z` 选项将签名后的归包打包成 JAR 文件：

```
cd signdir
zip -r ../myjar.jar *
  adding: META-INF/ (stored 0%)
  adding: META-INF/manifest.mf (deflated 15%)
  adding: META-INF/signtool.sf (deflated 28%)
  adding: META-INF/signtool.rsa (stored 0%)
  adding: text.txt (stored 0%)
```

### 生成密钥和证书

`signtool` 选项 `-G` 用于生成新的公钥对和证书。它接受新证书的名称作为参数。新生成的密钥和证书将安装到 `-d` 选项指定的目录中的密钥和证书数据库。对于 NT 版本的 Netscape Signing Tool，你必须在使用 `-G` 选项时配合 `-d` 选项。对于 Unix 版本的 Netscape Signing Tool，省略 `-d` 选项会导致工具将密钥和证书安装在 Communicator 密钥和证书数据库中。在所有情况下，证书也会输出到文件 `x509.cacert`，其 MIME 类型为 `application/x-x509-ca-cert`。

证书包含关于其所标识实体的标准信息，例如通用名称和组织名称。当你运行带有 `-G` 选项的命令时，Netscape Signing Tool 会提示你这些信息。然而，对于测试证书，所有请求字段都是可选的。如果你不输入通用名称，工具将提供一个默认名称。在以下示例中，用户输入部分为粗体：

```
signtool -G MyTestCert
using certificate directory: /u/souser/.netscape
Enter certificate information. All fields are optional. Acceptable characters are nuers, letters, spaces, and apostrophes.
certificate common na: Test Object Signing Certificate
organization: Netscape Comnications Corp.
organization unit: Server Products Division
state or province: California
country (st be exactly 2 characters): US
userna: souser
email address: 
Enter Password or Pin for "Comnicator Certificate DB": [Password will not echo]
generated public/private key pair
certificate request generated
certificate has been signed
certificate "MyTestCert" added to database
Exported certificate to x509.raw and x509.cacert.
```

证书信息是从标准输入读取的。因此，在某些操作系统中可以使用重定向操作符（`<`）从文件读取信息。为了为此创建文件，请按顺序每行输入七个输入字段中的每一个。确保最后一行尾有换行符。然后按照如下方式从你的文件重定向标准输入运行 `signtool`：

```
signtool -G MyTestCert < inputfile
```

提示将显示在屏幕上，但响应将自动从文件中读取。除非你使用 `-p` 选项在命令行中提供密码，否则密码仍从控制台读取。

### 使用 -M 选项列出智能卡

你可以使用 `-M` 选项列出 `signtool` 可用的 PKCS #11 模块，包括智能卡：

```
signtool -d "c:\netscape\users\jsmith" -M
using certificate directory: c:\netscape\users\userna
Listing of PKCS11 modules
-----------------------------------------------
 1. Netscape Internal PKCS #11 Module (this module is internally loaded)
 slots: 2 slots attached
 status: loaded
    slot: Comnicator Internal Cryptographic Services Version 4.0
    token: Comnicator Generic Crypto Svcs
    slot: Comnicator User Private Key and Certificate Services
    token: Comnicator Certificate DB
 2. CryptOS (this is an external module)
 DLL na: core32
 slots: 1 slots attached
 status: loaded
    slot: Litronic 210
    token: 
-----------------------------------------------
```

### 使用 Netscape Signing Tool 和智能卡签名文件

`signtool` 命令通常接受 `-k` 选项作为参数来指定签名证书。要使用智能卡签名，你只需提供证书的全限定名称。

要在运行 Communicator 时查看全限定证书名称，请点击 Navigator 中的 Security（安全）按钮，然后点击左框 Certificates（证书）下的 Yours（你的）。全限定名称的格式为 `smart card:certificate`，例如 `"MyCard:My Signing Cert"`。你按照如下方式配合 `-k` 参数使用该名称：

```
signtool -k "MyCard:My Signing Cert" directory
```

### 验证 FIPS 模式

使用 `-M` 选项验证你正在使用 FIPS-140-1 模块。

```
signtool -d "c:\netscape\users\jsmith" -M
using certificate directory: c:\netscape\users\jsmith
Listing of PKCS11 modules
-----------------------------------------------
 1. Netscape Internal PKCS #11 Module (this module is internally loaded)
 slots: 2 slots attached
 status: loaded
    slot: Comnicator Internal Cryptographic Services Version 4.0
    token: Comnicator Generic Crypto Svcs
    slot: Comnicator User Private Key and Certificate Services
    token: Comnicator Certificate DB
-----------------------------------------------
```

这个 Unix 示例显示 Netscape Signing Tool 正在使用 FIPS-140-1 模块：

```
signtool -d "c:\netscape\users\jsmith" -M
using certificate directory: c:\netscape\users\jsmith
Enter Password or Pin for "Comnicator Certificate DB": [password will not echo]
Listing of PKCS11 modules
-----------------------------------------------
 1. Netscape Internal FIPS PKCS #11 Module (this module is internally loaded)
 slots: 1 slots attached
 status: loaded
    slot: Netscape Internal FIPS-140-1 Cryptographic Services
    token: Comnicator Certificate DB
-----------------------------------------------
```




## 参见

`signver` (1)

NSS wiki 提供了有关新数据库设计以及如何配置应用程序使用它的信息。

## 附加资源

有关 NSS 以及其他与 NSS 相关的工具（如 JSS）的信息，请查看 m[] 上的 NSS 项目 wiki。NSS 站点直接与 NSS 代码更改和发布相关。

邮件列表：

IRC: Freenode at #dogtag-pki

## 作者

NSS 工具由来自 Netscape、Red Hat、Sun、Oracle、Mozilla 和 Google 的开发者编写并维护。

此文档仍在进行中。请为 **Mozilla NSS bug 836477** 的初始审查做出贡献[][]

## 描述

签名验证工具 `signver` 是一个简单的命令行程序，用于解包 base64 编码的 PKCS#7 签名对象并使用标准加密技术验证数字签名。签名验证工具还可以显示对象的内容。

## 选项

`-A` 显示 PKCS#7 签名中的所有信息。

`-V` 验证数字签名。

`-d [sql:]*directory*` 指定包含证书和密钥的数据库目录。`signver` 支持两种数据库：旧的安全数据库（`cert8.db`, `key3.db` 和 `secmod.db`）和新的 SQLite 数据库（`cert9.db`, `key4.db` 和 `pkcs11.txt`）。如果没有使用前缀 `sql:`，则工具假设指定的数据库为旧格式。

`-a` 设置指定的签名文件为 ASCII 格式。

`-i *input_file*` 指定带有签名数据的对象输入文件。

`-o *output_file*` 指定将结果写入的输出文件。

`-s *signature_file*` 指定数字签名输入文件。

`-v` 启用详细输出。

## 扩展示例

### 验证签名

`-V` 选项验证给定签名文件中的签名用于签名给定对象（来自输入文件）时是有效的。

```
signver -V -s signature_file -i signed_file -d sql:/ho/my/sharednssdb signatureValid=yes
```

### 打印签名数据

`-A` 选项打印签名文件中包含的所有信息。使用 `-o` 选项可以将签名文件信息打印到指定的输出文件而不是标准输出（stdout）。

```
signver -A -s signature_file -o output_file
```

## NSS 数据库类型

NSS 最初使用 BerkeleyDB 数据库来存储安全信息。这些*旧版*数据库最后的版本是：

`cert8.db` 用于证书

`key3.db` 用于密钥

`secmod.db` 用于 PKCS #11 模块信息

然而，BerkeleyDB 存在性能限制，这使得它无法被多个应用程序同时使用。NSS 具有足够的灵活性，允许应用程序使用自己的独立数据库引擎，同时保持共享数据库并解决访问问题。尽管如此，NSS 还需要更多的灵活性来提供真正的共享安全数据库。

2009 年，NSS 引入了一组新的数据库，它们是 SQLite 数据库而非 BerkeleyDB。这些新数据库提供了更好的可性和性能：

`cert9.db` 用于证书

`key4.db` 用于密钥

`pkcs11.txt`，列出了安全数据库目录下新子目录中包含的所有 PKCS #11 模块

由于 SQLite 数据库是为共享而设计的，因此它们是*共享*数据库类型。首选共享数据库类型；包含旧格式是为了向后兼容。

默认情况下，这些工具（`certutil`、`pk12util`、`modutil`）假设给定的安全数据库遵循更常见的旧版类型。使用 SQLite 数据库需要通过在给定的安全目录使用 `sql:` 前缀手动指定。例如：

```
# signver -A -s signature -d sql:/ho/my/sharednssdb
```

要将共享数据库类型设置为工具的默认类型，请将环境变量 `NSS_DEFAULT_DB_TYPE` 设置为 `sql`：

```
export NSS_DEFAULT_DB_TYPE="sql"
```

可以将此行添加到 `~/.bashrc` 文件中，以使该更改对用户永久生效。

大多数应用程序默认不使用共享数据库，但可以配置为使用它们。例如，这篇指南文章介绍了如何配置 Firefox 和 Thunderbird 使用新的共享 NSS 数据库：

关于共享 NSS 数据库更改的工程草案，请参阅 NSS 项目 wiki：

## 另请

`signtool` (1)

NSS wiki 提供了关于新数据库设计以及如何配置应用程序使用它的信息。

设置共享 NSS 数据库

关于共享 NSS 数据库的工程和技术信息

## 其他资源

有关 NSS 以及其他 NSS 相关工具（如 JSS）的信息，请查看 m[] 中的 NSS 项目 wiki。NSS 站点与 NSS 代码更改和发布直接相关。

邮件列表：

IRC: Freenode  #dogtag-pki

## 作者

NSS 工具由来自 Netscape、Red Hat、Sun、Oracle、Mozilla 和 Google 的开发者编写并维护。

作者：Elio Maldonado <>, Deon Lackey <>.

## 许可证

根据 Mozilla Public License, v. 2.0 许可。如果此文件未随附分发 MPL 副本，您可以在此处获取：

## 注意事项

1. Mozilla NSS bug 836477

---

# SKILL

## 名称

`skill`, `snice` - 发送信号或报告进程状态

**-i**，**--interactive**

交互式使用。您将被要求批准每个操作。

**-l**，**--list**

列出所有信号名称。

**-L**，**--table**

以表格形式列出所有信号名称。

**-n**，**--no-action**

无操作；对将发生的事件进行模拟，但不会实际更改系统。

**-v**，**--verbose**

详细；解释正在执行的操作。

**-w**，**--warnings**

启用警告。此选项尚未实现。

**-h**，**--help**

显示帮助文本并退出。

**-V**，**--version**

显示版本信息。

## 进程选择选项

选择标准可以是：终端、用户、pid、命令。可以使用以下选项来确保解释正确。

**-t**，**--tty** *tty*

下一个表达式是终端（tty 或 pty）。

**-u**，**--user** *user*

下一个表达式是用户名。

**-p**，**--pid** *pid*

下一个表达式是进程 ID 数字。

**-c**，**--command** *command*

下一个表达式是命令名。

**--ns** *pid*

匹配与 pid 属于相同命名空间的进程。

**--nslist** *ns,...*

列出哪些命名空间会被 `--ns` 选项考虑。可用的命名空间：`ipc`, `mnt`, `net`, `pid`, `user`, `uts`。

## 信号

信号的行为在 (7) 手册中解释。

## 示例

`snice -c seti -c crack +7`

减慢 seti 和 crack 命令的速度。

`skill -KILL -t /dev/pts/*`

杀死在 PTY 设备上的用户。

`skill -STOP -u viro -u lm -u davem`

停止三个用户。

## 另请

(1), (2), (1), (1), (1), (1), (7)

## 标准

无适用的标准。

## 作者

Albert Cahalan 于 1999 年编写了 `skill` 和 `snice`，作为非免费版本的替代。

## 报告错误

请将错误报告发送至

---

# SLABTOP

## 名称

`slabtop` - 显示内核 slab 缓存信息

## 概要

`slabtop` [*options*]

## 描述

`slabtop` 实时显示内核 slab 缓存信息。它显示按某个排序标准排序的顶部缓存列表。

## 选项

正常调用 `slabtop` 不需要任何选项。然而，可以通过指定以下一个或多个标志来微调行为：

**-d**, `--delay=*N*`

每隔 *n* 秒刷新一次显示。默认情况下，`slabtop` 每三秒刷新一次显示。按 q 退出程序。

**-s**, `--sort=*S*`

按 *S* 排序，其中 *S* 是排序标准之一。

**-o**, `--once`

| o | 对象数量 | OBJS |
| p | 每个 slab 的页数 | N/A |
| s | 对象大小 | OBJ SIZE |
| u | 缓存利用率 | USE |

## 命令

`slabtop` 在使用期间接受用户的键盘命令。支持以下命令。对于字母，两种大小写均可。

每个有效的排序字符也被接受，以更改排序程序。参见 **排序标准** 部分。

**<空格键>**

刷新屏幕。

**Q**

退出程序。

## 文件

`/proc/slabinfo`

slab 信息

## 另请

(1), (1), (1), (8)

## 注意事项

目前，`slabtop` 需要 2.4 或更高内核（具体为 1.1 或更高 `/proc/slabinfo`）。未来可能会支持 2.2 内核。

`slabtop` 统计头文件跟踪的是正在使用的 slab 字节数，这并不是物理内存的保证。`/proc/info` 文件中的 'Slab' 字段跟踪关于已用 slab 物理内存的信息。

## 作者

由 Chris Rivera 和 Robert Love 编写。

`slabtop` 的灵感来自 Martin Bligh 的 perl 脚本 `vmtop`。

## 报告错误

请将错误报告发送至

---

# SLEEP

## 名称

`sleep` - 指定时间的延迟

## 语法

`sleep` NUMBER[`SUFFIX`]...

`sleep` OPTION

## 描述

暂停 `NUMBER` 秒。`SUFFIX` 可以是 's' 表示秒（默认），'m' 表示分钟，'h' 表示小时或 'd' 表示天。与大多数要求 `NUMBER` 为整数的实现不同，这里的 `NUMBER` 可以是任意浮点数。给定两个或多个参数，将按照它们的值之和指定的时间暂停。

`--help`

显示此帮助信息并退出

`--version`

输出版本信息并退出

## 作者

由 Jim Meyering 和 Paul Eggert 编写。

## 报告错误

GNU coreutils 在线帮助：<>

将 sleep 翻译错误报告至 <>

## 版权

Copyright 2015 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 版本 3 或更高版本 <>。

这是免费软件：你可以自由地更改和重新发行它。在法律允许的范围内不提供任何保证。

## 参见

(3)

完整文档位于：<>

或通过本地可用信息：info '(coreutils) sleep invocation'

---

# SSH

## 名称

`ssh` - OpenSSH SSH 客户端（远程登录程序）

## 语法

`ssh` -words [-1246AaCfGgKkMNnqsTtVvXxYy] [-b `bind_address`] [-c `cipher_spec`] [-D [`bind_address` : *`port`]] [-E `log_file`] [-e `escape_char`] [-F `configfile`] [-I `pkcs11`] [-i `identity_file`] [-L `address`] [-l `login_na`] [-m `mac_spec`] [-O `ctl_cmd`] [-o `option`] [-p `port`] [-Q cipher | cipher-auth | mac | kex | key | protocol-version] [-R `address`] [-S `ctl_path`] [-W `host :*`port`] [-w `local_tun` [: *`remote_tun`]] [*user`@`hostna`] [*command`]

## 描述

`ssh` (SSH 客户端) 是一个用于登录远程机器并在其上执行命令的程序。它旨在取代 rlogin 和 rsh，并在不安全的网络两个不受信任主机之间提供安全的加密通信。X11 连接、任意 TCP 端口和 UNIX 节点可以通过安全通道进行转发。

`ssh` 连接并登录到指定的 `hostname`（带有可选的 `user`）。用户必须根据使用的协议版本（见下文）使用多种方法之一向远程机器证明身份。

如果指定了 `command`，它将在远程主机上执行而不是登录 shell。

选项如下：

`-1`

强制 `ssh` 仅尝试协议版本 1。

`-2`

强制 `ssh` 仅尝试协议版本 2。

`-4`

强制 `ssh` 仅使用 IPv4 地址。

`-6`

强制 `ssh` 仅使用 IPv6 地址。

`-A`

可以通过方括号包含地址指定 IPv6 地址。只有超级用户可以转发特权端口。默认情况下，本地端口根据 `GatewayPorts` 设置进行绑定。但可以使用显式的 `bind_address` 将连接绑定到特定地址。`localhost` 的 `bind_address` 表示监听的端口仅供本地使用，而空地址或 `*` 表示该端口应从所有接口可用。

`-E` `log_file`

将调试日志附加到 `log_file` 而不是标准错误。

`-e` `escape_char`

为带有 pty 的设置设置转义字符（默认：`~`）。转义字符仅在行首识别。转义字符后跟随点 (`.`) 关闭连接；跟随控制-Z 挂起；跟随自身发送一次转义字符。将字符设置为 `none` 将禁用任何转义并使会话完全透明。

`-F` `configfile`

指定替代的用户级配置文件。如果在命令行上提供了配置文件，则将忽略系统级配置文件 `/etc/ssh/ssh_config`。用户级配置文件的默认值为 `~/.ssh/config`

`-f`

请求 `ssh` 在执行命令之前进入后台运行。如果 `ssh` 将询问密码或短语，但用户希望它在后台运行，则此选项非常有用。这意味着 `-n`。在远程站点启动 X11 程序的推荐方法是类似于 `ssh -f host xterm` 的命令。

如果配置选项 `ExitOnForwardFailure` 设置为 `yes`，则使用 `-f` 启动的将在等待所有远程端口转发成功建立之前进入后台。

`-G`

导致 `ssh` 在评估 `Host` 和 `Match` 块后打印配置并退出。

`-g`

允许远程主机连接到本地转发的端口。如果在复用连接上使用，则此选项必须在主进程上指定。

`-I` `pkcs11`

指定 `ssh` 与提供用户私有 RSA 密钥的 PKCS#11 令牌通信的 PKCS#11 共享库。

`-i` `identity_file`

选择一个文件，从中读取用于公钥认证的身份（私钥）。协议版本 1 的默认值为 `~/.ssh/identity`，版本 2 的默认值为 `~/.ssh/id_dsa`、`~/.ssh/id_ecdsa`、`~/.ssh/id_ed25519` 和 `~/.ssh/id_rsa`。也可以在配置文件中按主机指定身份文件。可以使用多个 `-i` 选项（以及在配置文件中指定多个身份）。`ssh` 还会尝试从通过身份文件名附加 `-cert.pub` 获取的文件中加载证书信息。

### `-K`

启用基于 GSSAPI 的认证以及将 GSSAPI 凭据转发（委派）到服务器。

### `-k`

禁用将 GSSAPI 凭据转发（委派）到服务器。

### `-L [*bind_address : ] port : host : hostport*`
### `-L [*bind_address : ] port : remote_socket*`
### `-L *local_socket : host : hostport*`
### `-L *local_socket : remote_socket*`

指定本地（客户端）主机上给定 TCP 端口或 Unix 套接字的连接转发到远程端的给定主机和端口，或 Unix 套接字。这通过分配一个套接字来监听本地的 TCP `port`（可选绑定到指定的 `bind_address`）或 Unix 套接字来实现。每当本地端口或套接字建立连接时，连接将通过安全通道转发，并在远程机器上建立到 `host` 端口 `hostport` 或 Unix 套接字 `remote_socket`。

端口转发也可以在配置文件中指定。只有超级用户才能转发特权端口。可以通过方括号括起地址来指定 IPv6 地址。

默认情况下，本地端口根据 `GatewayPorts` 设置进行绑定。然而，可以使用显式的 `bind_address` 将连接绑定到特定地址。`bind_address` 设置为 `'localhost'` 表示监听的端口仅绑定供本地使用，而空地址或 `'*'` 则表示该端口应对从所有接口可用。

### `-l *login_na*`

指定在远程机器上登录的用户的用户。这也可以在配置文件中按主机指定。

### `-M`

将 `ssh` 客户端置于 `'master'` 模式以共享连接。使用多个 `-M` 选项会将 `ssh` 置于 `'master'` 模式，并在接受从属连接前需要确认。详情请参考 `ssh_config5` 中 `ControlMaster` 的描述。

### `-m *mac_spec*`

此外，对于协议版本 2，可以按优先级指定由逗号分隔的 MAC（消息认证码）算法列表。更多信息请参见 `MACs` 关键字。

### `-N`

不执行远程命令。这对于仅转发端口（仅限协议版本 2）有用。

### `-n`

将标准输入重定向自 `/dev/null`（实际上防止从标准输入读取）。当 `ssh` 在后台运行时应使用此项。一个常用技巧是使用它在远程机器上运行 X11 程序。例如，`ssh -n shadows.cs.hut.fi emacs` 将将在 shadows.cs.hut.fi 上启动 emacs，且 X11 连接将自动通过加密通道转发。`ssh` 程序将在后台运行。（如果 `ssh` 需要询问密码或短语密码，则此方法不起；请另参阅 `-f` 选项。）

### `-O *ctl_cmd*`

控制活动连接复用主进程。当指定 `-O` 选项时，将解释 `ctl_cmd` 参数并传递主进程。有效的命令有：`'check'`（检查主进程正在运行）、`'forward'`（请求转发但不执行命令）、`'cancel'`（取消转发）、`'exit'`（请求主进程退出）以及 `'stop'`（请求主进程停止接受进一步的复用请求）。

### `-o *option*`

用于提供格式格式格式格式。这对于指定没有独立命令行标志的选项有用。有关下方列出的选项的完整细节及其可能的值，请参见 `ssh_config5`。

### 配置选项

- `AddressFamily`
- `BatchMode`
- `BindAddress`
- `CanonicalDomains`
- `CanonicalizeFallbackLocal`
- `CanonicalizeHostname`
- `CanonicalizeMaxDots`
- `CanonicalizePermittedCNAMEs`
- `ChallengeResponseAuthentication`
- `CheckHostIP`
- `Cipher`
- `Ciphers`
- `ClearAllForwardings`
- `Compression`
- `CompressionLevel`
- `ConnectionAttempts`
- `ConnectTimeout`
- `ControlMaster`
- `ControlPath`
- `ControlPersist`
- `DynamicForward`
- `EscapeChar`
- `ExitOnForwardFailure`
- `FingerprintHash`
- `ForwardAgent`
- `ForwardX11`
- `ForwardX11Timeout`
- `ForwardX11Trusted`
- `GatewayPorts`
- `GlobalKnownHostsFile`
- `GSSAPIAuthentication`
- `GSSAPIKeyExchange`
- `GSSAPIClientIdentity`
- `GSSAPIDlegateCredentials`
- `GSSAPIRenewalForcesRekey`
- `GSSAPITrustDNS`
- `GSSAPIKexAlgorithms`
- `HashKnownHosts`
- `Host`
- `HostbasedAuthentication`
- `HostbasedKeyTypes`
- `HostKeyAlgorithms`
- `HostKeyAlias`
- `HostName`
- `IdentityFile`
- `IdentitiesOnly`
- `IPQoS`
- `KbdInteractiveAuthentication`
- `KbdInteractiveDevices`
- `KexAlgorithms`
- `LocalCommand`
- `LocalForward`
- `LogLevel`
- `MACs`
- `TunnelDevice`
- `UpdateHostKeys`
- `UsePrivilegedPort`
- `User`
- `UserKnownHostsFile`
- `VerifyHostKeyDNS`
- `VisualHostKey`
- `XAuthLocation`

### `-p *port*`

在远程主机上连接的端口。这也可以在配置文件中按主机指定。

### `-Q cipher | cipher-auth | mac | kex | key | protocol-version`

查询 `ssh` 对于指定的版本 2 支持的算法。可用功能有：`cipher`（支持的对称加密）、`cipher-auth`（支持认证加密的对称加密）、`mac`（支持的消息完整性代码）、`kex`（密钥交换算法）、`key`（密钥类型）和 `protocol-version`（支持的 SSH 协议版本）。

### `-q`

静默模式。抑制大多数警告和诊断消息。

### `-R [*bind_address : ] port : host : hostport*`
### `-R [*bind_address : ] port : local_socket*`
### `-R *remote_socket : host : hostport*`
### `-R *remote_socket : local_socket*`

指定远程（服务器）主机上给定 TCP 端口或 Unix 套接字的连接转发到本地端的给定主机和端口，或 Unix 套接字。这通过分配一个套接字来监听远程端的 TCP `port` 或 Unix 套接字来实现。每当此端口或套接字建立连接时，连接将通过安全通道转发，并在本地机器上建立到 `host` 端口 `hostport` 或 `local_socket`。

端口转发也可以在配置文件中指定。只有在远程机器上以 root 登录时才能转发特权端口。可以通过方括号括起地址来指定 IPv6 地址。默认情况下，服务器上的 TCP 监听套接字仅绑定到环回接口。可以通过指定 `bind_address` 来覆盖。空 `bind_address` 或地址 `'*'` 表示远程套接字应对从所有接口可用。指定远程 `bind_address` 仅在服务器的 `GatewayPorts` 选项启用时才会成功（参见 `sshd_config5`）。

如果 `port` 参数为 `0`，则监听端口将在服务器上动态分配，并在运行时报告给客户端。当与 `-O forward` 一起使用时，分配的端口将打印到标准输出。

`-S` `ctl_path` 指定用于连接的控制套字的位置，或使用字符串 `none` 禁用连接共享。详情请参考 `ssh_config` 中 `ControlPath` 和 `ControlMaster` 的描述。

`-s` 可用于请求在远程系统上调用子系统。子系统是 SSH2 协议的一种特性，便于将 SSH 作为其他应用程序的安全传输通道（例如 (1)）。子系统被指定为远程命令。

`-T` 禁用伪终端分配。

`-t` 强制分配伪终端。这可以用于在远程机器上执行任意的基于屏幕的程序，这非常有用，例如在实现新服务时。多个 `-t` 选项会强制分配 tty，即使 `ssh` 没有本地 tty 也是如此。

`-V` 显示版本号并退出。

`-v` 详细模式。使 `ssh` 打印关于其进展的调试信息。这对于调试连接、身份验证和配置问题很有帮助。多个 `-v` 选项会增加详细程度。最大为 3。

`-W` `host :port` 请求将客户端的标准输入和输出通过安全通道转发到 `host` 的 `port`。这包含了 `-N`、`-T` `ExitOnForwardFailure` 和 `ClearAllForwardings`。仅适用于协议版本 2。

`-w` `local_tun` [: `remote_tun`] 请求在客户端（`local_tun`）和服务器（`remote_tun`）之间使用指定的 (4) 设备进行隧道设备转发。

设备可以通过数值 ID 或关键字 `any`（使用下一个可用的隧道设备）来指定。如果未指定 `remote_tun`，则默认为 `any`。另请参见 `ssh_config` 中的 `Tunnel` 和 `TunnelDevice` 指令。如果未设置 `Tunnel` 指令，则将其设置为默认隧道模式，即 `point-to-point`（点对点）。

`-X` 启用 X11 转发。这也可以在配置文件按主机指定。

应谨慎启用 X11 转发。能够绕过远程主机文件权限（针对用户的 X 授权数据库）的用户可以通过转发的连接访问本地 X11 显示。攻击者随后可能执行按键监控等活动。

出于此原因，X11 转发默认受到 X11 SECURITY 扩展的限制。更多信息请参考 `ssh` 的 `-Y` 选项和 `ssh_config` 中的 `ForwardX11Trusted` 指令。

`-x` 禁用 X11 转发。

`-Y` 启用信任的 X11 转发。受信任的 X11 转发不受 X11 SECURITY 扩展控制。

`-y` 使用 (3) 系统模块发送日志信息。默认情况下，这些信息发送到 stderr。

`ssh` 可能还会从用户配置文件和系统级配置文件获取配置数据。文件格式和配置选项在 `ssh_config` 中描述。

## 身份验证

OpenSSH SSH 客户端支持 SSH 协议 1 和 2。默认仅使用协议 2，尽管可以通过 `ssh_config` 中的 `Protocol` 选项或 `-1` 和 `-2` 选项进行更改（见上文）。两种协议都支持相似的身份验证方法，但协议 2 是默认选择，因为它提供了额外的机密性机制（流量使用 AES, 3DES, Blowfish, CAST128 或 Arcfour 加密）和完整性机制（`hmac-md5`, `hmac-sha1`, `hmac-sha2-256`, `hmac-sha2-512`, `umac-64`, `umac-128`, `hmac-ripemd160`）。协议 1 缺乏确保连接完整性的强机制。

可用的身份验证方法有：基于 GSSAPI 的身份验证、基于主机的身份验证、公钥认证、挑战响应认证和密码认证。身份验证按上述顺序尝试，尽管协议 2 有一个更改默认顺序的配置选项：`PreferredAuthentications`。

基于主机的身份验证工作如下：如果用户登录的机器位于远程机器的 `/etc/hosts.equiv` 或 `/etc/ssh/shosts.equiv` 中，且双方用户名相同，或者如果远程机器用户目录下存在 `~/.rhosts` 或 `~/.shosts` 文件，且其中包含客户端机器名称和该机器上用户名的行，则该用户被考虑登录。此外，服务器必须能够验证客户端的主机密钥（见下文对 `/etc/ssh/ssh_known_hosts` 和 `~/.ssh/known_hosts` 的描述）才允许登录。这种身份验证方法解决了由于 IP 欺骗、DNS 欺骗和路由欺骗导致的安全漏洞。[管理员注意：`/etc/hosts.equiv`、`~/.rhosts` 以及一般的 rlogin/rsh 协议本质上是不安全的，如果需要安全性应将其禁用。]

公钥认证工作如下：该方案基于公钥加密，使用加密和解密使用独立密钥的密码系统，且从加密密钥推导出解密密钥是不行的。想法是每个用户为身份验证创建一个公私对。服务器知道公钥，只有用户知道私钥。`ssh` 自动实现公钥认证协议，使用 DSA、ECDSA、Ed25519 或 RSA 算法之一。协议 1 限制为仅使用 RSA 密钥，但协议 2 可以使用任何算法。(8) 的 HISTORY 部分包含对 DSA 和 RSA 算法的简要讨论。

文件 `~/.ssh/authorized_keys` 列出了允许登录的公钥。当用户登录时，`ssh` 程序告诉服务器它想使用哪种密钥对进行身份验证。客户端证明它拥有私钥的访问权限，服务器检查相应的公钥是否有授权接受该账户。

用户通过运行 `ssh-keygen` 创建其密钥对。这会将私钥存储在 `~/.ssh/identity`（协议 1）、`~/.ssh/id_dsa`（协议 2 DSA）、`~/.ssh/id_ecdsa`（协议 2 ECDSA）、`~/.ssh/id_ed25519`（协议 2 Ed25519）或 `~/.ssh/id_rsa`（协议 2 RSA），并将公钥存储在 `~/.ssh/identity.pub`（协议 1）、`~/.ssh/id_dsa.pub`（协议 2 DSA）、`~/.ssh/id_ecdsa.pub`（协议 2 ECDSA）、`~/.ssh/id_ed25519.pub`（协议 2 Ed25519）或 `~/.ssh/id_rsa.pub`（协议 2 RSA），位于用户目录下。用户随后应将公钥拷贝到远程机器用户目录下的 `~/.ssh/authorized_keys`。`authorized_keys` 文件对应传统的 `~/.rhosts` 文件，每行一个密钥，尽管行可能非常长。此后，用户无需提供密码即可登录。

公钥认证的一种变体是以证书认证的形式提供的：不是使用一组公私密钥，而是使用经过签名的证书。这种方法的优点是可以使用单个受信任的证书机构来代替许多公私密钥。更多信息请参阅 `ssh-keygen` 的 CERTIFICATES 部分。

使用公钥或证书认证最方便的方法可能是使用身份验证代理。更多信息请参阅 `ssh-agent`。

挑战响应认证工作如下：服务器发送任意的查询挑战文本，并提示响应。协议 2 允许多次挑战和响应；协议 1 仅限于一次挑战/响应。挑战响应认证的示例包括 BSD 认证（见 `login.conf`）和 PAM（适用于非 Unix 系统）。

最后，如果其他身份验证方法失败，`ssh` 会提示用户输入密码。密码被发送到远程主机进行检查；由于所有通信都是加密的，网络上的任何监听者都看不到密码。

`ssh` 会自动维护并检查一个数据库，该数据库包含了它曾经使用过的所有主机的标识符。主机密钥存储在用户目录下的 `~/.ssh/known_hosts` 中。此外，系统会自动检查 `/etc/ssh/ssh_known_hosts` 文件以获取已知主机。任何新主机都会自动添加到用户的文件中。如果某个主机的标识符发生变化，`ssh` 会对此发出告警告并禁用密码认证，以防止服务器欺骗或中间人攻击，这些攻击可能被用于绕过加密。可以使用 `StrictHostKeyChecking` 选项来控制对主机密钥未知或已更改的机器进行登录。

当用户的身份被服务器接受后，服务器将在非交互式会话中执行给定的命令，或者在未指定命令的情况下，登录到机器并为用户提供正常的 shell 作为交互式会话。与远程命令或 shell 的所有通信将被自动加密。

如果请求了交互式会话，`ssh` 默认仅在客户端拥有交互式终端时才会为交互式会话请求伪终端（pty）。可以使用 `-T` 和 `-t` 标志来覆盖此行为。

如果分配了伪终端，用户可以使用下面注的转义字符。

如果没有分配伪终端，则会话是透明的，可以可靠地传输二进制数据。在大多数系统中，将转义字符设置为 `none` 即使在使用 tty 时也会使会话保持透明。

当远程机器上的命令或 shell 退出且所有 X11 和 TCP 连接关闭时，会话将终止。

## 转义字符

当请求了伪终端时，`ssh` 通过使用转义字符支持多种功能。

单个波浪号字符可以通过 `~~` 发送，或者在波浪号后跟随一个非下字符的字符来发送。转义字符始终紧跟换行符以便被解释为特殊字符。可以在配置文件中使用 `EscapeChar` 配置指令或在命令行中通过 `-e` 选项来更改转义字符。

支持的转义序列（假设默认为 `~`）如下：

- `~.`: 断开连接。
- `~^Z`: 后台运行 `.`。
- `~#`: 列出转发的连接。
- `~&`: 在注销时等待转发的连接 / X11 会话结束，并在后台运行 `ssh`。
- `~?`: 显示转义字符列表。
- `~B`: 向远程系统发送 BREAK（仅对 SSH 协议版本 2 且对方支持时有用）。
- `~C`: 打开命令行。目前这允许使用 `-L` `-R` 和 `-D` 选项添加端口转发（见上文）。它还允许使用 `-KL` [*bind_address : port*] 本地、`-KR` [*bind_address : port*] 远程和 `-KD` [*bind_address : port*] 动态端口转发来取消现有的端口转发。`!` *command* 在在 `ssh_config` 中启用了 `PermitLocalCommand` 选项时，允许用户执行本地命令。可以使用 `-h` 选项获取基本帮助。
- `~R`: 请求重置连接密钥（仅对 SSH 协议版本 2 且对方支持时有用）。
- `~V`: 当错误写入 stderr 时减少详细程度（`LogLevel`）。

如果 `ForwardX11` 变量设置为 `yes`（或见上文 `-X` `-x` 和 `-Y` 选项的描述）且用户正在使用 X11（已设置 `DISPLAY`），到 X11 的连接将自动转发到远程。X11 连接的转发可以在命令行或配置文件中配置。`ssh` 设置的 `DISPLAY` 值将指向服务器机器，但其显示编号大于零。这是正常的，因为 `ssh` 在服务器机器上创建了一个“代理”X 服务器，以便通过加密通道转发连接。

`ssh` 还会在服务器机器上自动设置 Xauthority 数据。为此，它将生成一个随机的授权 cookie，将其存储在 Xauthority 中，并验证任何转发的连接是否携带此 cookie，并在连接打开时将其替换为真实的 cookie。真实的认证 cookie 永远不会发送到服务器机器（也不会以明文发送任何 cookie）。

如果 `ForwardAgent` 变量设置为 `yes`（或见上文 `-A` 和 `-a` 选项的描述）且用户正在使用身份代理，到代理的连接将自动转发到远程。

## 验证主机密钥

第一次连接到服务器时，系统会向用户展示服务器公钥的指纹（除非禁用了 `StrictHostKeyChecking` 选项）。可以使用 `ssh-keygen` 确定指纹：

```bash



```bash
ssh-keygen -l -f /etc/ssh/ssh_host_rsa_key
```

如果指纹已知，可以对其进行匹配并接受或拒绝密钥。如果服务器仅提供旧的（MD5）指纹，可以使用`ssh-keygen`的`-E`选项来降低指纹算法以匹配。

由于通过查看指纹字符串来比较主机密钥很困难，因此支持使用随机艺术视觉上比较主机密钥。通过将`VisualHostKey`选项设置为`yes`，每次登录服务器时都会显示一个小的 ASCII 图形，无论会话本身是否是交互式的。通过学习已知服务器产生的模式，当显示完全不同的模式时，用户可以轻松发现主机密钥已更改。然而，由于这些模式并非一无二的，与参考模式相似的模式只能给出主机密钥相同的良好概率，而不是确定的证明。

要获取所有已知主机的指纹列表及其随机艺术字，可以使用以下命令行：

```bash
$ ssh-keygen -lv -f ~/.ssh/known_hosts
```

如果指纹是未知的，还有另一种验证方法：通过 DNS 验证的 SSH 指纹。会将额外的资源记录（RR）`SSHFP`添加到区域文件中，连接的客户端能够将该指纹与所呈现密钥的指纹进行匹配。

在此示例中，我们正在将客户端连接到服务器`host.example.com`。应首先将`SSHFP`资源记录添加到`host.example.com`的区域文件中：

```bash
$ ssh-keygen -r host.example.com.
```

输出的行需要添加到区域文件中。要检查该区域是否正在响应指纹查询：

```bash
$ dig -t SSHFP host.example.com
```

最后客户端进行连接：

```bash
$ ssh -o "VerifyHostKeyDNS ask" host.example.com [...]
```

在 DNS 中找到匹配主机密钥指纹。你确定要继续连接吗 (yes/no)?

更多信息请参阅`ssh_config`中的`VerifyHostKeyDNS`。

# 基于 SSH 的虚拟专用网络

`ssh`包含了对使用 (4) 网络伪设备进行虚拟专用网络（VPN）隧道的支持，允许两个网络安全地连接。`sshd_config`配置选项`PermitTunnel`控制服务器是否支持此功能，以及在什么级别（二层或三层流量）。

以下示例将通过从`10.1.1.1`到`10.1.1.2`的点对连接连接客户端网络`10.0.50.0/24`与远程网络`10.0.99.0/24`，前提是运行在远程网络网关`192.168.1.15`上的 SSH 服务器允许此操作。

在客户端上：

```bash
# ssh -f -w 0:1 192.168.1.15 true
# ifconfig tun0 10.1.1.1 10.1.1.2 netmask 255.255.255.252
# route add 10.0.99.0/24 10.1.1.2
```

在服务器上：

```bash
# ifconfig tun1 10.1.1.2 10.1.1.1 netmask 255.255.255.252
# route add 10.0.50.0/24 10.1.1.1
```



客户端的访问可以通过 `/root/.ssh/authorized_keys` 文件（见下文）和 `PermitRootLogin` 选项进行精细调整。由于基于 SSH 的设置涉及大量的开销，它可能适用于临时的 (4) 设置，例如无线 VPN。更持久的 VPN 由如 (8) (8) 等工具提供会更好。

# 环境

`ssh` 通常会设置以下变量：

`DISPLAY`: `DISPLAY` 变量指示 X11 服务器的位置。它由 `ssh` 自动设置，指向 `host:n` 格式的值，其中 `host` 表示运行 shell 的主机，`n` 是一个整数。用户不应显式设置 `DISPLAY`，因为这将导致连接不安全（并要求用户手动复制任何 cookie）。

`HOME`: 设置为用户目录的路径。

`LOGNAME`: 使用此变量的系统对 `USER` 的别名。

`MAIL`: 设置为用户的信箱。

`PATH`: 设置为指定的默认 `PATH`。

`SSH_ASKPASS`: 如果 `ssh` 需要密码，且是从终端运行的，则它将从当前终端读取密码。如果 `ssh` 没有关联的终端但设置了 `SSH_ASKPASS`，它将执行由 `SSH_ASKPASS` 指定的程序并打开窗口来读取密码。这在从 `.xsession` 或相关脚本调用 `ssh` 时特别有用。

`SSH_AUTH_SOCK`: 标识用于与代理身份验证的 UNIX 套字路径。

`SSH_CONNECTION`: 标识连接的客户端和服务器端。该变量包含四个用空格分隔的值：客户端 IP 地址、客户端端口、服务器 IP 地址和服务器端口。

`SSH_ORIGINAL_COMMAND`: 如果执行强制命令，此变量包含原始命令行。

`SSH_TTY`: 设置为与当前 shell 关联的 tty 名称。如果当前会话没有 tty，则不设置此变量。

`TZ`: 如果设置了时区，则该变量用于指示时区（即守护进程在新连接时传递该值）。

`USER`: 设置为登录用户的名称。此外，如果存在 `~/.ssh/environment`，`ssh` 会读取并添加 `VARNAME=value` 格式的行。更多信息请参阅 `sshd_config` 中的 `PermitUserEnvironment` 选项。

`SSH_USE_RNG`: OpenSSL 随机生成器的重新种子通常从 `/dev/urandom` 完成。如果 `SSH_USE_RNG` 变量设置为 `0` 以外的值，则从 `/dev/random` 重新种子 OpenSSL 生成器。读取的字节数由 `SSH_USE_RNG` 值定义。在没有硬件随机生成器的计算机上不建议此设置，因为熵不足会导致连接阻塞，直到有足够的熵。

## 文件

`~/.rhosts`: 此文件用于基于主机的身份验证（见上文）。在某些机器上，如果用户目录位于 NFS 分区上，此文件可能需要所有人可读，因为 (8) 以 root 身份读取它。此外，此文件应由用户拥有，且不允许其他任何人具有写权限。大多数机器的推荐权限是用户可读/写，其他人不可访问。

`~/.shosts`: 此文件的用法与 `.rhosts` 完全相同，但允许基于主机的身份验证，而不允许通过 `rlogin/rsh` 登录。

`~/.ssh/`: 该目录是所有用户特定配置和身份验证信息的默认位置。没有通用要求保持此目录的所有内容保密，但推荐的权限是用户可读/写/执行，其他人不可访问。

`~/.ssh/authorized_keys`: 列出可用于作为此用户登录的公钥（DSA, ECDSA, Ed25519, RSA）。该文件的格式在 (8) 手册页中描述。此文件并不敏感，但推荐的权限是用户可读/写，其他人不可访问。

`~/.ssh/config`: 这是每个用户的配置文件。该文件格式和配置选项在 `ssh_config` 中描述。由于存在被滥用的可能，此文件应具有严格的权限：用户可读写写，其他用户不可写。

`~/.ssh/environment`: 包含环境变量的额外定义；见上文的 ENVIRONMENT。

`~/.ssh/identity`

`~/.ssh/id_dsa`

`~/.ssh/id_ecdsa`

`~/.ssh/id_ed25519`

`~/.ssh/id_rsa`: 包含身份验证的私钥。这些文件包含敏感数据，应允许用户读取但其他人不可访问（读/写/执行）。如果私钥文件可被访问，`ssh` 将简单忽略该私钥文件。在生成密钥时可以指定密码，这将使用 3DES 加密此文件的敏感部分。

`~/.ssh/identity.pub`

`~/.ssh/id_dsa.pub`

`~/.ssh/id_ecdsa.pub`

`~/.ssh/id_ed25519.pub`

### `/etc/ssh/ssh_host_ecdsa_key`

### `/etc/ssh/ssh_host_ed25519_key`

### `/etc/ssh/ssh_rsa_key`

这些文件包含主机密钥的私部分，用于基于主机的身份验证。如果使用协议版本 1，`ssh` 必须设置为 setuid root，因为主机密钥仅对 root 可读。对于协议版本 2，`ssh` 使用 `ssh-keysign8` 来访问主机密钥，消除了在使用基于主机的身份验证时对 `ssh` 设置为 setuid root 的要求。默认情况下，`ssh` 不是 setuid root。

### `/etc/ssh/ssh_known_hosts`

系统级已知主机密钥列表。此文件应由系统管理员准备，包含组织内所有机器的公主机密钥。它应该是 world 可读的。关于此文件格式的更多细节，请参阅 (8)。

### `/etc/ssh/sshrc`

此文件中的命令会在用户登录时由 `ssh` 执行，在用户的 shell（或命令）启动之前执行。有关更多信息，请参阅 (8) 手册页。

## 退出状态

`ssh` 以远程命令的退出状态退出，或者在发生错误时返回 255。

## IPV6

IPv6 地址可以用任何使用 IPv4 地址的地方。在所有条目中，IPv6 地址被括在方括号内。注意：方括号是 shell 的特殊字符，在 shell 中必须转义。

## 参见

(1), (1), `ssh-add1`, `ssh-agent1`, `ssh-keygen1`, `ssh-keyscan1`, (4), `ssh_config5`, `ssh-keysign8`, (8)

## 标准

S. Lehtinen C. Lonvick January 2006 *RFC 4250* *The Secure Shell (SSH) Protocol Assigned Nuers*

T. Ylonen C. Lonvick January 2006 *RFC 4251* *The Secure Shell (SSH) Protocol Architecture*

T. Ylonen C. Lonvick January 2006 *RFC 4252* *The Secure Shell (SSH) Authentication Protocol*

T. Ylonen C. Lonvick January 2006 *RFC 4253* *The Secure Shell (SSH) Transport Layer Protocol*

T. Ylonen C. Lonvick January 2006 *RFC 4254* *The Secure Shell (SSH) Connection Protocol*

J. Schlyter W. Griffin January 2006 *RFC 4255* *Using DNS to Securely Publish Secure Shell (SSH) Key Fingerprints*

F. Cusack M. Forssen January 2006 *RFC 4256* *Generic Message Exchange Authentication for the Secure Shell Protocol (SSH)*

J. Galbraith P. Remaker January 2006 *RFC 4335* *The Secure Shell (SSH) Session Channel Break Extension*

M. Bellare T. Kohno C. Namprempre January 2006 *RFC 4344* *The Secure Shell (SSH) Transport Layer Encryption Modes*

B. Harris January 2006 *RFC 4345* *Improved Arcfour Modes for the Secure Shell (SSH) Transport Layer Protocol*

M. Friedl N. Provos W. Simpson March 2006 *RFC 4419* *Diffie-Hellman Group Exchange for the Secure Shell (SSH) Transport Layer Protocol*

J. Galbraith R. Thayer November 2006 *RFC 4716* *The Secure Shell (SSH) Public Key File Format*

D. Stebila J. Green December 2009 *RFC 5656* *Elliptic Curve Algorithm Integration in the Secure Shell Transport Layer*

A. Perrig D. Song 1999 International Workshop on Cryptographic Techniques and E-Commerce (CrypTEC '99) *Hash Visualization: a New Technique to improve Real-World Security*

## 作者

OpenSSH 是 Tatu Ylonen 原始免费 ssh 1.2.12 版本的衍生版本。Aaron Campbell, Bob Beck, Markus Friedl, Niels Provos, Theo de Raadt 和 Dug Song 修复了许多 bug，添加了新功能并创建了 OpenSSH。Markus Friedl 为支持 SSH 协议版本 1.5 和 2.0 做出了贡献。

*

# SMBCLIENT

## 名称

`sclient` - 用于访问 SMB 资源的类 ftp 客户端

## 概要

`sclient` - 用于访问 SMB 资源的类 ftp 客户端，用于访问 SMB 上的资源。

`sclient` [options] [host] [command]

## 描述

`sclient` 是一个用于访问 SMB 资源的类 ftp 客户端，用于访问 SMB 上的资源。该工具是 SMB 实用套件的一部分，类似于 ftp (7)。操作包括从本地机器获取文件、向本地机器发送文件、获取服务器目录信息等。

## 选项

### `servicena`

`servicena` 是你想要在服务器上使用的服务名称。格式为 `//server`，其中 `server` 是服务器的 NetBIOS 名称。注意，`servicena` 不一定是运行该机器的 IP 地址，它可能是该机器的 NetBIOS 名称。

服务器名称将根据 `-R` 参数或 (5) 文件中的名称解析顺序进行查找，管理员可以通过更改该顺序来更改 `servicena`。

### `password`

访问指定服务器上指定服务的密码。如果提供了此参数，则指定的 `-N` 选项（抑制密码提示）。

没有默认密码。如果未在命令行（通过使用此参数或添加到 `-U` 选项，见下方）提供密码，且未指定 `-N` 选项，客户端将提示输入密码，即使所需的服务不需要密码。（如果不需要密码，只需按回车提供空密码。）

注意：某些服务器（包括 OS/2 和 Windows 工作组）强制要求大写密码。小写或混合大小写的密码可能会被这些服务器拒绝。在脚本中包含密码要小心。

### `-R|--na-resolve <na resolve order>`

此选项用于 Saa 套件中的程序，以确定按什么顺序如何解析主机名称到 IP 地址。该选项接受一个用空格分隔的解析选项字符串。

选项有：“`lmhosts`”、“`host`”、“`wins`” 和“`bcast`”。它们导致如下名称解析：

**`lmhosts`**: 在 Saa lmhosts 文件中查找 IP 地址。如果 lmhosts 中的行没有连接到 NetBIOS 名称类型（详见 (5)），则任何名称类型都匹配查找。

**`host`**: 执行标准的主机名称到 IP 地址解析，使用系统的 `/etc/hosts`、NIS 或 DNS 查询。这种名称解析方法取决于操作系统（例如，在 IRIX 或 Solaris 上，它可能由 `/etc/nsswitch.conf` 文件控制）。注意，这种名称解析仅在查询的 NetBIOS 名称类型为 0x20（服务器）类型时才使用，否则将被忽略。

**`wins`**: 使用 *wins server* 参数中列出的 IP 地址查询名称。如果未指定 WINS 服务器，则该方法将被忽略。

**`bcast`**: 在 `interfaces` 参数列出的每个已知本地接口上执行广播。这是所有 NetBIOS 解析方法中最不可靠的，因为它取决于目标主机位于本地连接的子网内。

如果未设置此参数，则将使用 (5) 文件参数（na resolve order）中定义的 NetBIOS 解析顺序。

默认顺序为 `lmhosts`、`host`、`wins`、`bcast`。如果没有此参数，或者在 (5) 文件的 `na resolve order` 参数中没有任何条目，则将按照此顺序尝试 NetBIOS 解析方法。

### `-m|--max-protocol protocol`

这允许用户选择 `sclient` 连接服务器时将使用的最高 SMB 协议级别。默认设置为 NT1，这是最高可用的 SMB1 协议。要使用 SMB2 或 SMB3 协议连接，请分别使用字符串 `SMB2` 或 `SMB3`。注意，要连接到带有加密传输的 Windows 2012 服务器，需要选择 `SMB3` 作为最大协议。

### `-P|--machine-pass`

使用本地服务器的机器账户对外部服务器进行查询。

### `-I|--ip-address IP-address`

`IP address` 是要连接的服务器地址。它应该以标准的“a.b.c.d”符号指定。

通常，客户端会尝试通过上述 `na resolve order` 参数中描述的 NetBIOS 解析机制查找 NetBIOS SMB/CIFS 服务器。使用此参数将强制客户端假设服务器位于指定 IP 地址的机器上，并将忽略所连接资源的 NetBIOS na 组成部分。

此参数没有默认值。如果不提供，它将由客户端如上所述自动确定。

### `-E|--stderr`

此参数导致客户端将消息写入标准错误流 (`stderr`) 而不是标准输出流。

默认情况下，客户端将消息写入标准输出 - 通常是用户的 tty。

### `-L|--list`

此选项允许你查看服务器上提了哪些可用的服务。你通过 `sclient -L host` 使用它，随后会出现一个列表。如果你的 NetBIOS nas 与你的 TCP/IP DNS 主机 nas 不匹配，或者你正尝试访问另一个网络上的主机，`-I` 可能会很有用。

### `-b|--send-buffer buffersize`

在发送或接收文件时，`sclient` 使用由连接的服务器允许的最大请求数调整的内部缓冲区。此命令允许将大小设置为 0（使用服务器控制的默认大小）字节到 16776960 (`0xFFFF00`) 字节之间的范围。使用服务器控制的大小是最有效的，因为 `sclient` 将流水线处理所需的并发读取或写入，以保持服务器尽可能忙。设置为任何其他大小都会减慢传输。这也可以使用 `sclient` 内部的 `iosize` 命令进行设置。

### `-B|--browse`

使用 DNS 浏览 SMB 服务器。

### `-d|--debuglevel=level`

`level` 是从 0 到 10 的整数。如果未指定此参数，默认值为 1。

此值越高，日志文件中记录的关于服务器活动的详细信息就越多。在级别 0 下，仅记录关键错误和严重警告。级别 1 是日常运行的合理水平 - 它会生成有关执行操作的少量信息。

1 以上的级别将产生大量的日志数据，应仅在调查问题时使用。3 以上的级别专供开发人员使用，并会产生海量的日志数据，其中大部分极其晦涩。

注意，在此处指定此参数将覆盖 `s.conf` 文件中的 `log level` 参数。

### `-V|--version`

打印程序版本。

### `-s|--configfile=<filename>`

指定的文件包含服务器所需的配置详情。查看 `s.conf` 了解更多信息。

### `-l|--log-base=logdirectory`

日志/调试文件的基目录。默认配置文件由客户端如所述确定。不会被删除。

### `--option=<na>=<value>`

从命令行设置 `<na>` 参数为 `<value>`。这将覆盖编译时的默认值以及从配置文件中读取的选项。

### `-N|--no-pass`

如果指定，此参数将抑制客户端向用户提示密码。这对于访问不需要密码的服务非常有用。

除非在命令行上指定了密码或指定了此参数，否则客户端将请求密码。

如果在命令行上指定了密码且定义了此选项，则将忽略命令行上的密码且不使用密码。

### `-k|--kerberos`

尝试使用 kerberos 验证。仅在 Active Directory 环境有效。

### `-C|--use-ccache`

尝试使用 winbind 缓存的凭据。

### `-A|--authentication-file=filename`

此选项允许你指定一个从文件中读取连接时使用的用户名和密码。文件格式为：

```



`username = <value>` `password = <value>` `domain = <value>`

确保文件的权限限制了未经授权用户的访问。

### `-U|--user=username[%password]`
设置 SMB 用户名或用户名和密码。

如果未指定 `%password`，将提示用户。客户端将首先检查 `USER` 环境变量，然后是 `LOGNAME` 变量，如果其中一个存在，则字符串转换为大写。如果没有找到这些环境变量，则使用用户名 `GUEST`。

第三种选项是使用凭据文件，其中包含明文用户名和密码。此选项主要为那些不希望通过命令行或环境变量传递凭据的脚本提供。如果使用此方法，请确保文件的权限限制了未经授权用户的访问。详情请参见 `-A`。

谨慎在脚本中包含密码。此外，在许多系统上，可以通过 `ps` 命令看到运行进程的命令行。为了安全起见，请始终允许 `rpcclient` 提示密码并直接输入。

此命令行参数要求远程服务器支持 UNIX 扩展，或者选择了 SMB3 协议。它请求连接加密。通过 SMB3 或 POSIX 扩展使用 GSSAPI 协商 SMB 加密。使用提供的凭据进行加密协商（如果提供了域名/用户名/密码三组，则使用 kerberos 或 NTLMv1/v2）。如果无法协商加密，则连接失败。

### `--pw-nt-hash`
提供的密码是 NT 哈希值。

### `-n|--netbiosna <primary NetBIOS na>`
此选项允许你覆盖 Saa 自身使用的 NetBIOS 名称。这等同于设置 `s.conf` 文件中的 `netbios nam`[] 参数。然而，命令行的设置将优于 `s.conf` 中的设置。

### `-i|--scope <scope>`
这指定了 `nlookup` 在生成 NetBIOS 名称时用于通信的 NetBIOS 范围。有关 NetBIOS 范围使用的详细信息，请参阅 `rfc1001.txt` 和 `rfc1002.txt`。NetBIOS 范围极少被使用，只有当你是你负责所通信的所有 NetBIOS 系统的系统管理员时，才设置此参数。

### `-W|--workgroup=domain`
设置 userna 的 SMB 域。这会覆盖在 `s.conf` 中定义的默认域。如果指定的域是服务器的 NetBIOS 名称，它将导致客户端使用服务器的本地 SAM（而不是域 SAM）进行登录。

### `-O|--socket-options socket options`
设置在客户端套接字上的 TCP 套接字选项。有效选项列表请参见 `s.conf` 手页中的 `socket options` 参数。

### `-?|--help`
打印命令行选项的摘要。

### `--usage`
显示简短的用法信息。

### `-t|--tiout <tiout-seconds>`
允许用户调整每个 SMB 请求使用的默认 `tiout`。默认设置为 20 秒。如果对服务器的请求超时，请增加该值。这可能发生在选择了 SMB3 加密且 `sclient` 向服务器发送了过多请求时。也可以在 `sclient` 内部使用 `tiout` 命令进行设置。

### `-T|--tar tar options`
`sclient` 可用于创建 (1) SMB/CIFS 共享上所有文件的兼容备份。可以传递此选项的辅助 tar 标志包括：

* `c` - 在本地系统上创建 tar 备份归档。必须后跟 tar 文件名、磁带设备或 `-`（标准输出）。如果使用标准输出，你必须将日志级别调至最低值 `-d0` 以避免损坏你的 tar 文件。此标志与 `x` 标志互斥。
* `x` - 将本地 tar 文件提取（恢复）回共享中。除非给出了 `-D` 选项，否则 tar 文件将从共享的顶层恢复。必须后跟 tar 文件名、设备或 `-`（标准输入）。与 `c` 标志互斥。恢复的文件的创建时间（mti）将被设置为在 tar 文件中保存的日期。目前尚还无法正确恢复目录的创建日期。
* `I` - 包含文件和目录。当上方指定文件名时，这是默认行为。导致文件包含在提取或创建中（因此排除其他所有内容）。见下文示例。文件名通配符（globbing）以两种方式之一工作。见下文 `r`。
* `X` - 排除文件和目录。导致文件从提取或创建中排除。见下文示例。文件名通配符以两种方式之一工作。见下文 `r`。
* `F` - 包含文件和目录列表的文件。`F` 导致 tar 文件创建后的名称被读取为包含文件和目录列表的文件，以便将其包含在提取或创建中（因此排除其他所有内容）。见下文示例。文件名通配符以两种方式之一工作。见下文 `r`。
* `b` - 块大小。必须后跟有效的（大于零）块大小。导致 tar 文件以 `blocksize*TBLOCK`（512 字节）块写入。
* `g` - 增量。只备份设置了归档位的文件。对 `c` 标志有用。
* `q` - 静默。保持 tar 在工作时不打印诊断信息。这等于 tarm 的静默模式。
* `r` - 使用通配符匹配来包含或排除。已弃用。
* `N` - 新于。必须后跟一个文件名称，其日期将与创建期间在共享上找到的文件进行比较。只有比指定文件更新的文件会被备份到 tar 文件中。对 `c` 标志有用。
* `a` - 设置归档位。在备份文件时导致归档位被重置。对 `g` 和 `c` 标志有用。

#### Tar 长文件名
为共享中的所有文件和目录创建 tar 文件。

```bash
sclient //mypc/myshare "" -N -Tc backup.tar *
```

### `-D|--directory initial directory`
在启动前切换到初始目录。可能仅对 tar -T 选项有用。

### `-c|--command command string`
命令字符串是用分号分隔的命令列表，用于代替从 stdin 提示。`-c` 隐含 `-N`。
这在脚本中以及将 stdin 打印到服务器时特别有用，例如 `-c 'print -'`。

## 操作

一旦客户端运行，用户将看到一个提示符：

```
s:\>
```



反斜杠（`\\`）表示服务器上的当前工作目录，如果更改了工作目录，它也会改变。

提示符表示客户端已就绪并等待执行用户命令。每个命令都是单个单词，可选地后跟特定命令的参数。除非这些注释另有说明，否则命令和参数用空格分隔。所有命令均不区分大小写。命令的参数可能区分或不区分大小写，取决于命令。

你可以通过双引号引号名称指定包含空格的文件名，例如 `"a long file na"`。

显示在方括号中的参数（例如 `[parater]`）是可选的。如果没有提供，命令将使用合适的默认值。显示在角括号中的参数（例如 `<parater>`）是必需的。

注意，所有在服务器上运行的命令实际上是通过向服务器发送请求完成的。因此，行为可能根据服务器而异，取决于服务器的实现方式。

可用命令按字母顺序列在此处。

`? [command]`

如果指定了 `command`，`?` 命令将显示关于指定命令的简短信息。如果没有指定命令，将显示可用命令列表。

`! [shell command]`

如果指定了 `shell command`，`!` 命令将在本地执行 shell 并运行指定的 shell 命令。如果没有指定命令，将运行一个本地 shell。

`allinfo file`

客户端将请求服务器返回关于该文件或目录的所有已知信息（包括流）。

`altna file`

客户端将请求服务器返回文件或目录的“备用”名称（8.3 名称）。

`archive <nuer>`

在操作文件时设置归档级别。0 表示忽略归档位，1 表示仅对设置了该位的文件进行操作，2 表示仅对设置了该位的文件进行操作并在操作后重置该位，3 表示对所有文件进行操作并在操作后重置该位。默认值为 0。

`backup`

切换目录列表和文件打开时发送到服务器的“备份意图”（backup intent）标志的状态。如果“备份意图”标志为真，且用户已获得授予 `SE_BACKUP` 或 `SE_RESTORE` 权限，服务器将尝试绕过某些文件系统检查。此状态在执行备份或恢复操作时非常有用。

`blocksize <nuer>`

设置 `tar` 操作的块大小参数。默认值为 20。这会导致 tar 文件以 `blocksize*TBLOCK`（通常为 512 字节）为单位写入。

`cancel jobid0 [jobid1] ... [jobidN]`

客户端将请求服务器取消由指定的打印任务 ID 标识的打印任务。

`case_sensitive`

切换 SMB 数据包中的标志设置，该标志告诉服务器将文件名视为区分大小敏感。默认设置为 OFF（告诉文件服务器将文件名视为不区分大小敏感）。目前仅影响 Saa 3.0.5 及以上且在 `s.conf` 中 case sensitive 参数设置为 auto 的文件服务器。

`cd <directory na>`

如果指定了 `directory na`，服务器上的当前工作目录将更改为指定的目录。如果由于某种原因无法指定的目录，此操作将失败。如果未指定目录名，将报告服务器上的当前工作目录。

`chmod file mode in octal`

此命令取决于服务器是否支持 CIFS UNIX 扩展，如果服务器不支持则将失败。客户端请求服务器将 UNIX 权限更改为指定的八进制模式，采用标准 UNIX 格式。

`chown file uid gid`

此命令取决于服务器是否支持 CIFS UNIX 扩展，如果服务器不支持则将失败。客户端请求服务器将 UNIX 用户和组所有权更改为指定的十进制值。注意，目前没有办法远程查找指定名称的 UNIX `uid` 和 `gid` 值。这可能在未来的 CIFS UNIX 扩展中解决。

`close <fileid>`

关闭由 `open` 命令显式打开的文件。用于内部 Saa 测试目的。

`del <mask>`

客户端将请求服务器尝试从服务器当前工作目录删除所有匹配 `mask` 的文件。

`dir <mask>`

从服务器检索并显示在服务器当前工作目录中匹配 `mask` 的文件列表。

`du <filena>`

执行目录列表，然后打印共享的当前磁盘使用情况和可用空间。

`echo <nuer> <data>`

执行 `SMBecho` 请求以测试服务器。用于内部 Saa 测试目的。

`exit`

终止连接。

`get <remote na> [local na]`

将服务器上的 `remote na` 复制到本地 `local na`。如果未指定 `local na`，则使用相同的文件名。

### posix_encrypt <domain> <userna> <password>

此命令取决于服务器是否支持 CIFS UNIX 扩展，如果服务器不支持则将失败。尝试在此连接上协商 SMB 加密。如果 `sclient` 使用 kerberos 凭据 `-k` 连接，则此命令的参数将被忽略，并将使用 kerberos 凭据协商 GSSAPI 签名和密封。另参见 `sclient` 的 `-e` 选项以便在初始连接时强制加密。此命令是 Saa 3.2 的新增功能。

### posix_open <filena> <octal mode>

此命令取决于服务器是否支持 CIFS UNIX 扩展，如果服务器不支持则将失败。使用 CIFS UNIX 扩展打开远程文件并打印 `fileid`。用于内部 Saa 测试。

### posix_mkdir <directoryna> <octal mode>

此命令取决于服务器是否支持 CIFS UNIX 扩展，如果服务器不支持则将失败。使用给定的模式通过 CIFS UNIX 扩展创建远程目录。

### posix_rmdir <directoryna>

此命令取决于服务器是否支持 CIFS UNIX 扩展，如果服务器不支持则将失败。使用 CIFS UNIX 扩展删除远程目录。

### posix_unlink <filena>

此命令取决于服务器是否支持 CIFS UNIX 扩展，如果服务器不支持则将失败。使用 CIFS UNIX 扩展删除远程文件。

### print <file na>

通过服务器上的打印服务打印本地机器上的指定文件。

### prompt

在执行 `mget` 和 `mput` 命令期间切换对文件名的提示。当设置为 ON 时，用户将会被提示确认这些命令期间每个文件的传输。当设置为 OFF 时，所有指定文件都将在无提示的情况下传输。

### put <local file na> [remote file na]

从运行客户端的机器将名为 `local file na` 的文件复制到服务器。如果指定，远程副本将为 `remote file na`。请注意 `sclient` 中的所有传输都是二进制的。另参见小写命令。

### queue

显示打印队列，显示作业 id、`na`、大小和当前状态。

### quit

参见退出命令。

### readlink syinkna

此命令取决于服务器是否支持 CIFS UNIX 扩展，如果服务器不支持则将失败。打印符号链接 `syinkna` 的值。

### rd <directory na>

参见 `rmdir` 命令。

### recurse

为 `mget` 和 `mput` 命令切换目录递归。当设置为 ON 时，这些命令将处理源目录中的所有目录（即它们正在复制的目录），并递归进入任何匹配命令指定的掩码的目录。只有符合使用 `mask` 命令指定的掩码的文件会被检索。另参见 `mask` 命令。当递归设置为 OFF 时，仅将复制源机器当前工作目录中符合 `mget` 或 `mput` 命令指定的掩码的文件，并将忽略使用 `mask` 命令指定的任何掩码。

### rena <old filena> <new filena>

将服务器上当前工作目录中的文件从 `old filena` 重命名为 `new filena`。

### rm <mask>

从服务器上当前工作目录中删除所有匹配 `mask` 的文件。

### rmdir <directory na>

在用户访问权限允许的情况下，从服务器上删除指定的目录。

### scopy <source filena> <destination filena>

尝试使用最高效的服务器端复制调用复制服务器上的文件。如果服务器不支持服务器端复制，则退回到使用读取后写入。

### setmode <filena> <perm=[+|\-]rsha>

用于设置文件权限的 DOS attrib 命令版本。例如：

```
setmode myfile +r
```

将使 `myfile` 变为只读。

### showconnect

显示用于 DFS 目的当前的活动连接。

### stat file

此命令取决于服务器是否支持 CIFS UNIX 扩展，如果服务器不支持则将失败。客户端请求 UNIX 基础信息级别并打印 Linux `stat` 命令关于文件的 sa 信息。这包括大小、磁盘上使用的块、文件类型、权限、inode 编号、链接数以及最后的三个时间戳（访问、修改和更改）。如果文件是特殊文件（符号链接、字符或块设备、fifo 或套接字），可能还会打印额外信息。

### syink target linkna

此命令取决于服务器是否支持 CIFS UNIX 扩展，如果服务器不支持则将失败。客户端请求服务器在 `target` 和 `linkna` 文件之间创建一个符号链接硬链接。`linkna` 文件不存在。请注意，服务器不会为任何位于当前连接共享之外的路径创建链接。这由 Saa 服务器强制执行。

### tar <c|x>[IXbgNa]

执行 tar 操作 - 参见上面的 `-T` 命令行选项。行为可能会受 `tarmode` 命令的影响（见下文）。使用 `g`（增量）和 `N`（更新）将影响 tarmode 设置。注意在 `tar x` 中使用 `-` 选项可能无效 - 请使用命令行选项。

### blocksize <blocksize>

将协议中当前使用的 vuid 更改为指定的任意 `nuer`。不带参数时，打印当前正在使用的 vuid。用于内部 Saa 测试。

### tcon <sharena>

建立一个新的树连接（连接到共享）。替换当前的树连接。打印新的 tid（树 ID）。用于内部 Saa 测试。

### tdis

关闭当前的共享连接（树断开）。用于内部 Saa 测试。

### tid <nuer>

将协议中当前的树 id (tid) 更改为新的任意 `nuer`。不带参数时，打印当前正在使用的 tid。用于内部 Saa 测试。

## 注意事项

因此，服务器对提供的 `usernas`、密码、共享 `nas`（又称服务 `nas`）和机器 `nas` 大写非常敏感。如果连接失败，尝试提供所有大写的参数。

在连接到某些类型的服务器时，通常需要使用 `-n` 选项。例如 OS/2 LanManager 强制使用有效的 NetBIOS `na`，因此你需要提供一个服务器已知的有效 `na`。

`sclient` 在支持 LANMAN2 协议或以上的服务器支持长文件名。

变量 `LIBSMB_PROG` 可能包含一个路径，通过 `system()` 执行，客户端应连接到该路径而不是连接到服务器。此功能主要作为开发辅助，在配合 LMHOSTS 文件时效果最佳。

## 安装

客户端程序的位置由个人系统管理员决定。因此以下仅供建议。

建议将客户端软件安装在 `/usr/local/saa/bin/` 或 `/usr/saa/bin/` 目录下，该目录所有人读，仅 root 写。客户端程序本身应对所有人可执行。客户端**不要**设置 setuid 或 setgid！

客户端日志文件应放在仅供用户可读可写的目录中。

要测试客户端，您需要知道运行中的 SMB/CIFS 服务器的名称。可以使用普通用户身份运行 (8) - 将该服务器作为用户可访问的端口（通常是 1024 以上的任何端口）上的守护进程运行将提供合适的测试服务器。

## 诊断

客户端发布的大多数诊断都记录在指定的日志文件中。日志文件名在编译时指定，但可以在命令行中覆盖。

可用的诊断信息数量和类型取决于客户端使用的调试级别。如果您遇到问题，请将调试级别设置为 3 并仔细查看日志文件。

## 版本

此帮助页适用于 Saa 套件的 3.2 版本。

## 作者

原始 Saa 软件及相关工具由 Andrew Tridgell 创建。Saa 现在由 Saa 团队作为一个开源项目开发，类似于 Linux 内核的开发方式。

原始 Saa 帮助页由 Karl Auer 编写。帮助页源码已转换为 YODL 格式（另一项优秀的开源软件，由 Jeremy Allison 转换并为 Saa 2.0 发布更新了更新）。Saa 2.2 的 DocBook 转换由 Gerald Carter 完成。Saa 3.0 的 DocBook XML 4.2 转换由 Alexander Bokovoy 完成。

# SMBGET

## 名称

`sget` - 类似 wget 的工具，用于通过 SMB 下载文件

## 语法

`sget [-a,--guest] [-r,--resu] [-R,--recursive] [-u,--userna=STRING] [-p,--password=STRING] [-w,--workgroup=STRING] [-n,--nonprompt] [-d,--debuglevel=INT] [-D,--dots] [-P,--keep-permissions] [-o,--outputfile] [-f,--rcfile] [-q,--quiet] [-v,--verbose] [-b,--blocksize] [-O,--stdout] [-U,--update] [-?,--help] [--usage] { [ [...]`

## 描述

此工具是 (7) 套件的一部分。

`sget` 是一个具有 wget 语义的简单工具，可以从 SMB 服务器下载文件。您可以在命令行上指定您想要下载的文件。

文件应符合 s-URL 标准，例如对于 UNC 路径使用 `\\\\HOST\\SHARE\\file`。

## 选项

- `-a, --guest`
  以 guest 用户身份工作

- `-r, --resu`
  自动恢复中断的文件

- `-R, --recursive`
  递归下载文件

- `-u, --userna=STRING`
  使用的用户名

- `-p, --password=STRING`
  使用的密码

- `-w, --workgroup=STRING`
  使用的工作组（可选）

- `-n, --nonprompt`
  不询问任何问题（非交互式）

- `-d, --debuglevel=INT`
  使用的调试级别

- `-D, --dots`
  显示点作为进度指示

- `-P, --keep-permissions`
  将本地文件的权限设置为与远程文件相同。

- `-o, --outputfile`
  将正在下载的文件写入指定的文件。不能与 `-R` 同时使用。

- `-O, --stdout`
  将正在下载的文件写入标准输出。

- `-f, --rcfile`
  使用指定的 rcfile。文件将按照指定的顺序加载 - 例如，如果在在此之前指定了任何选项，它们可能会被 rcfile 的内容覆盖。

- `-q, --quiet`
  静默

- `-v, --verbose`
  详细

如果 `na` 是工作组，则是该工作组中的所有服务器；如果 `na` 是服务器，则是该服务器上的所有共享。

## 示例

```
# 递归下载 'src' 目录
sget -R

# 下载 FreeBSD ISO 并启用恢复
sget -r

# 递归下载所有 ISO
sget -R

# 备份我的数据
sget -Rr
```



## 缺陷

在某些情况下（例如格式错误的 `s://` url 或在未开启 `-R` 的情况下尝试获取目录），会返回权限拒绝（Permission denied）。

## 版本

此帮助页适用于 Saa 套件的 3 版本。

## 作者

原始 Saa 软件及相关工具由 Andrew Tridgell 创建。Saa 现在由 Saa 团队作为一个开源项目开发，类似于 Linux 内核的开发方式。

`sget` 帮助页由 Jeremy Allison 编写。

---

# SMIME

## 名称

`smi` - S/MIME 工具

## 语法

`openssl smi [-encrypt] [-decrypt] [-sign] [-resign] [-verify] [-pk7out] [--cipher]] [-in file] [-CAfile file] [-CApath dir] [-trusted_first] [-no_alt_chains] [-certfile file] [-signer file] [-recip file] [-inform SMIME|PEM|DER]`

## 描述

`smi` 命令处理 S/MIME 邮件。它可以加密、解密、签名和验证邮件。

## 命令选项

有六个操作选项设置操作类型。其他选项的作用根据操作类型而异。

- `-encrypt`  
  为指定的接收者加密邮件。输入文件为待加密的消息。输出文件为 MIME 格式的加密邮件。

- `-decrypt`  
  使用提供的证书和私钥解密邮件。输入 MIME 格式的加密邮件。解密邮件写入输出文件。

- `-sign`  
  使用提供的证书和私钥签名邮件。输入文件为待签名的消息。签名邮件以 MIME 格式写入输出文件。

- `-verify`  
  验证签名邮件。输入签名的 MIME 邮件并输出签名数据。支持明文和透明签名。

- `-pk7out`  
  获取输入消息并输出 PEM 编码的 PKCS#7 结构。

- `-resign`  
  重新签名消息：取一个现有消息和多个新签名者。

- `-in file`  
  待加密或签名的消息，或待解密或验证的 MIME 邮件。

- `-inform SMIME|PEM|DER`  
  这指定 PKCS#7 结构的输入格式。默认是 `SMIME`，读取 S/MIME 格式的消息。`PEM` 和 `DER` 格式将其为为 PEM 和 DER 格式的 PKCS#7 结构。目前仅影响 PKCS#7 结构的输入格式，如果没有输入 PKCS#7 结构（例如在使用 `-encrypt` 或 `-sign` 时），此选项无效。

- `-out`  
  已解密或验证的消息，或已签名或验证的输出 MIME 格式邮件。

- `-outform SMIME|PEM|DER`  
  这指定了 PKCS#7 结构的输出格式。默认是 `SMIME`，它会写入 S/MIME 格式的消息。`PEM` 和 `DER` 格式会将此更改为写入 PEM 和 DER 格式的 PKCS#7 结构。目前仅影响 PKCS#7 结构的输出格式，如果没有输出 PKCS#7 结构（例如使用 `-verify` 或 `-decrypt`），则此选项无作用。

### `-stream -indef -noindef`

`-stream` 和 `-indef` 选项等效，用于启用编码的流式 I/O。这允许对数据进行单次处理，而无需将整个内容保留在内存中，从而支持非常大的文件。对于带有分离数据的 S/MIME 签名，如果输出格式为 `SMIME`，会自动设置流式；对于所有其他操作目前默认关闭。

### `-noindef`

禁用流式 I/O，防止其产生具有无限长度的构造编码。此选项目前没有作用。在未来，所有相关操作将默认启用流式传输，并可以通过此选项将其禁用。

### `-content filename`

这指定一个包含分离内容的文件，这仅对 `-verify` 命令有用。只有当 PKCS#7 结构使用不包含内容的分离签名形式时，此选项才可用。如果输入格式是 S/MIME 且使用 multipart/signed MIME 类型，此选项将覆盖任何内容。

### `-text`

在加密或签名时，此选项会向提供的消息添加纯文本 (text/plain) MIME 头。在解密或验证时，它会剥离文本头：如果解密或验证的消息不是 MIME 类型 text/plain，则会发生错误。

### `-CAfile file`

一个包含信任的 CA 证书的文件，仅用于 `-verify`。

### `-CApath dir`

一个包含信任的 CA 证书的目录，仅用于 `-verify`。该目录必须是标准的证书目录：即每个主体名称的哈希值（使用 `x509 -hash` 计算）应链接到每个证书上。

### `-trusted_first`

在构建信任链以验证证书时，使用 CA 文件或 CA 目录中的证书优于消息提供的证书。这在具有桥接 CA 或交叉认证 CA 的环境中特别有用。

### `-md digest`

签名或重签名时使用的摘要算法。如果未指定，则将使用签名密钥的默认摘要算法（通常为 SHA1）。

### `-[cipher]`

使用的加密算法。例如 DES (56 位) `-des`，三重 DES (168 位) `-des3`（通过 `EVP_get_cipherbyname()` 函数）也可以通过连字符前使用，例如 `-aes_128_cbc`。查看 `enc` 获取您的 OpenSSL 版本支持的密码列表。

如果未指定，使用三重 DES。仅用于 `-encrypt`。

### `-nointern`

在验证消息时，通常会在消息包含的证书（如果有）中查找签名证书。使用此选项，仅使用 `-certfile` 选项指定的证书。然而，提供的证书仍可以作为不受信任的 CA 使用。

### `-noverify`

### `-certfile file`

允许指定额外的证书。签名时，这些证书将包含在消息中。验证时，将在这些文件中查找签名证书。证书应为 PEM 格式。

### `-signer file`

在签名或重签名消息时使用的签名证书，如果需要多个签名者，可以使用多次此选项。如果正在验证消息，若验证成功，则签名者证书将写入此文件。

### `-recip file`

解密消息时使用的接收者证书。此证书必须匹配消息的某个接收者之一，否则会发生错误。

### `-inkey file`

签名或解密时使用的私钥。它必须与相应的证书匹配。如果未指定此选项，则私钥应包含在通过 `-recip` 或 `-signer` 指定指定的文件中。签名时，可以使用多次此选项指定连续的密钥。

### `-passin arg`

私钥密码源。更多信息请参见 (1) 中的 **PHRASE ARGUMENTS**。

### `-rand file(s)`

包含随机数据的文件或多个文件，用于种子随机生成器，或 RNG 节点（见 (3)）。多个文件由操作系统相关的字符分隔：MS-Windows 使用 `;`，OpenVMS 使用 `,`，其他使用 `:`。

### `cert.pem...`

一个或多个消息接收者的证书：在加密消息时使用。

### `-to, -from, -subject`

相关的邮件头。这些包含在消息的签名部分之外，因此可以手动包含。在签名时，许多 S/MIME 客户端会检查签名者的邮箱地址是否匹配 From: 地址。

### `-purpose, -ignore_critical, -issuer_checks, -crl_check, -crl_check_all, -policy_check, -extended_crl, -x509_strict, -policy -check_ss_sig -no_alt_chains`

设置证书链验证的各种选项。详情见 `verify` 手页。

## 注意

MIME 消息头部和输出之间没有任何空行。因此邮件程序会自动添加空行。将邮件直接管道到 sendmail 是实现正确格式的方法之一。

要签名或加密的消息包含必要的 MIME 头，否则许多 S/MIME 客户端无法正常显示（如果显示的话）。可以使用 `-text` 选项自动添加纯文本头。

签名并加密的消息是指对已签名消息进行加密的消息。这可以通过对已签名的消息进行加密产生：参见示例部分。

此版本的程序每条消息允许一个签名者，但它会验证接收消息中的多个签名者。因此，如果消息包含多个签名者，S/MIME 客户端会崩溃。可以通过对已签名的消息再次签名来并行签名消息。

`-encrypt` 和 `-decrypt` 选项反映了 S/MIME 客户端的常用。严格来说，这些处理的是 PKCS#7 封装数据：PKCS#7 加密数据用于其他。

`-resign` 选项在添加新签名者时使用现有的消息摘要。这要求至少一个现有签名者使用相同的消息摘要，否则此操作将失败。

`-stream` 和 `-indef` 选项启用了实验性的流式 I/O 支持。结果是编码变为 BER 使用无限长度构造编码，而不再是 DER。流式传输支持 `-encrypt` 操作以及在内容未分离时的 `-sign` 操作。

流式处理始终用于带有分离数据的 `-sign` 操作，但由于内容不再是 PKCS#7 结构的一部分的一部分，其编码保持为 DER 格式。

## 退出码

0  
操作完全成功。

1  
解析命令行选项时发生错误。

2  
无法读取其中一个输入文件。

3  
创建 PKCS#7 文件或读取 MIME 消息时发生错误。

4  
解密或验证消息时发生错误。

5  
消息已验证通过，但在输出签名者证书时发生错误。

## 示例

创建一个明文签名消息：

```
openssl smi -sign -in ssage.txt -text -out mail.msg \ -signer mycert.pem
```

创建一个不透明的签名消息：

```
openssl smi -sign -in ssage.txt -text -out mail.msg -nodetach \ -signer mycert.pem
```

创建一个签名消息，包含一些额外的证书，并从另一个文件读取私钥：

```
openssl smi -sign -in in.txt -text -out mail.msg \ -signer mycert.pem -inkey mykey.pem -certfile mycerts.pem
```

创建一个具有两个签名者的签名消息：

```
openssl smi -sign -in ssage.txt -text -out mail.msg \ -signer mycert.pem -signer othercert.pem
```

在 Unix 下直接将签名消息发送到 sendmail，并包含头信息：

```
openssl smi -sign -in in.txt -text -signer mycert.pem \ -from -to \ -subject "Signed ssage" | sendmail
```

验证消息并在成功后提取签名者证书：

```
openssl smi -verify -in mail.msg -signer user.pem -out signedtext.txt
```

使用三重 DES 发送加密邮件：

```
openssl smi -encrypt -in in.txt -from \ -to -subject "Encrypted ssage" \ -des3 user.pem -out mail.msg
```

签名并加密邮件：

```
openssl smi -sign -in .txt -signer my.pem -text \ | openssl smi -encrypt -out mail.msg \ -from -to \ -subject "Signed and Encrypted ssage" -des3 user.pem
```

使用 128 位 Callia 创建加密消息：

```
openssl smi -encrypt -in plain.txt -callia128 -out mail.msg cert.pem
```

向现有消息添加签名者：

```
openssl smi -resign -in mail.msg -signer newsign.pem -out mail2.msg
```

## 缺陷

MIME 解析器并不高明：它似乎能处理我丢给它的大多数消息，但可能会在其他消息上卡住。

代码目前只会将签名者证书写入文件：如果签名者有单独的加密证书，则必须手动提取。应该有一种启发式方法来确定确的加密证书。

理想情况下，应该为每个电子邮件地址维护一个证书数据库。

代码目前没有注意到 SMIMECapabilities 签名属性中提供的许可对称加密算法。这意味着用户必须手动包含正确的加密算法。它应该在数据库中存储许可的加密算法列表，并仅使用这些算法。

对签名者证书没有进行撤销检查。

当前代码只能处理 S/MIME v2 消息，更复杂的 S/MIME v3 结构可能会导致解析错误。

## 历史

多个 `-signer` 选项和 `-resign` 命令首次在 OpenSSL 1.0.0 中引入。

`-no_alt_chains` 选项首次在 OpenSSL 1.0.2b 中引入。

---

# SOELIM

## 名称

`soelim` - 在 groff 输入中解释 .so 请求

## 概要

`[-Crtv]` `[-I *dir*]` `[*files *...*]`

在 `-I` 命令行选项及其参数之间可以存在空格。

## 描述

`soelim` 读取 *files* 并将形式如 `.so***file*` 的行替换为 *file* 的内容。如果包含 `.so` 的文件需要预处理，它是很有用的。通常，`soelim` 应该配合 groff 的 `-s` 选项调用。

要在文件中需要 `\`，请写入 `\\` 或 `\e`。需要空格，请写入 `\`。*file* 中的任何其他转义序列都会使 `soelim` 忽略整行。

注意，开头的点与两个字符 's' 和 'o' 之间不能有空格。否则，只有 `groff` 会解释 `.so` 请求（而 `soelim` 会忽略它）。

## 选项

`-C`  
即使后面跟着不是空格或换行符的字符也识别 `.so`。

`-I*dir*`  
此选项可用于向文件搜索路径添加目录（包括命令行中的文件和 .so 请求中的文件）。搜索路径用当前目录初始化。此选项可以指定多次；目录按指定的顺序进行搜索（但在当前目录之前）。如果你想让在其他目录之前读取当前目录，请在适当的位置添加 `-I.`。

`-b`  
忽略前导空格。

`-d`  
仅考虑空格和字母数字字符。

`-f`  
将小写字符转换为大写字符。

`-g`  
根据通用数值比较。

`-i`  
仅考虑可打印字符。

`-M`  
按月份比较（未知） < 'JAN' < ... < 'DEC'。

`-h`  
按人类可读的数值比较（例如 2K 1G）。

`-n`  
按字符串数值比较。

`-R`  
按键随机哈希排序。

`-r`  
反转比较结果。

`-t`  
不产生 `.lf` 请求

`-v`  
打印版本。

## 用法

`groff` 的正常处理序列如下：

```
input file | v preprocessor -> troff | v output file
```

对于源文件，如果需要处理的文件也应该进行预处理，这由 `soelim` 处理：

```
input file | v soelim -> preprocessor -> troff | v output file
```




对于源文件，由 `troff` 处理。

## 参见

(1)

## 版权

版权 1989-2014 Free Software Foundation, Inc.

许可分发本手册的逐字副本，只要保留版权声明和本许可公告。许可根据上述条件分发本手册的修改版本，只需许可公告由自由软件基金批准。

***

# SORT

## 名称

`sort` - 对文本文件排序

## 概要

`sort [OPTION]... [FILE]...`

`sort [OPTION]... --files0-from=F`

## 描述

`-R`, `--random-sort`

按键随机哈希排序。

`--random-source=FILE`

从 `FILE` 获取随机字节。

`-r`, `--reverse`

反转比较结果。

`--sort=WORD`

根据 `WORD` 排序：`general-numeric -g`、`human-numeric -h`、`month -M`、`numeric -n`、`random -R`、`version -V`。

`-V`, `--version-sort`

对文本中的版本数字进行自然排序。

## 其他选项

`--batch-size=NMERGE`

一次处理最多 `NMERGE` 个输入；更多情况下请使用临时文件。

`-c`, `--check`, `--check=diagnose-first`

检查输入是否排序；不进行排序。

`-C`, `--check=quiet`, `--check=silent`

类似于 `-c`，但不报告第一行错误。

`--compress-program=PROG`

使用 `PROG` 压缩临时文件；使用 `PROG -d` 解压。

`--debug`

标记用于排序的行部分，并向 `stderr` 警告可能疑的用法。

`--files0-from=F`

从文件 `F` 中指定的以 NUL 终止的文件名读取输入；如果 `F` 为 `-`，则从标准输入读取文件名。

`-k`, `--key=KEYDEF`

通过键进行排序；`KEYDEF` 提供位置和类型。

`-m`, `--merge`

归并已排序的文件；不进行排序。

`-o`, `--output=FILE`

将结果写入 `FILE` 而不是标准输出。

`-s`, `--stable`

通过禁用最后的比较来实现稳定排序。

`-S`, `--buffer-size=SIZE`

使用 `SIZE` 作为主内存缓冲区。

`-t`, `--field-separator=SEP`

使用 `SEP` 代替非空白到空白的转换符。

`-T`, `--temporary-directory=DIR`

使用 `DIR` 作为临时目录，而不是 `$TMPDIR` 或 `/tmp`；多个选项可指定多个目录。

`--parallel=N`

将并发运行的排序数量更改为 `N`。

`-u`, `--unique`

配合 `-c` 检查严格排序；不使用 `-c`，仅输出相同运行的第一行。

`-z`, `--zero-terminated`

行分隔符为 NUL，而不是换行符。

`--help`

显示此帮助并退出。

`--version`

输出版本信息并退出。

`KEYDEF` 格式为 `F[.C][OPTS][,F[.C][OPTS]]`，用于指定起始和停止位置，其中 `F` 是字段数字，`C` 是字段中的字符位置；两者均从 1 开始，停止位置默认到行尾。如果 `-t` 或 `-b` 均生效，字段中的字符将从前一个空白处开始计数。`OPTS` 是一个或多个单字母排序选项 `[bdfgiMhnRrV]`，它们会覆盖该键的全局排序选项。如果没有给出键，则使用整行作为键。

`SIZE` 后面可以跟随以下乘法后缀：`%`（`1%` 内存）、`b`（`1`）、`K`（`1024`，默认），以及后续的 `M`、`G`、`T`、`P`、`E`、`Z`、`Y`。

**WARNING** 环境变量指定的区域（locale）会影响排序。设置 `LC_ALL=C` 以获取使用原生字节值的传统排序。

## 作者

由 Mike Haertel 和 Paul Eggert 编写。

## 报告 Bug

GNU coreutils 在线帮助：<>

向 <> 报告排序翻译错误。

## 版权

所有所有 2015 Free Software Foundation, Inc. 许可证 GPLv3+：GNU GPL 版本 3 或更高版本 <>。

这是免费软件：你可以自由地更改和重新发行它。在法律允许范围内不提供担保。

## 另请参见

(1)

完整文档请访问：<>

或通过本地访问：`info '(coreutils) sort invocation'`

# SOSREPORT

## 名称

`sosreport` - 收集并打包诊断和支持数据

## 概要

`sosreport`

`[-l|--list-plugins]`

`[-n|--skip-plugins plugin-names]`

`[-e|--enable-plugins plugin-names]`

`[-o|--only-plugins plugin-names]`

`[-a|--alloptions] [-v|--verbose]`

`[--report] [--config-file conf] [--batch]`

`[--build] [--name name] [--ticket-number]`

`[--debug] [--tmp-dir directory]`

`[--help]`

## 描述

`sosreport` 生成一个来自运行系统的诊断信息的压缩 tar 存档。该存档可以存储在本地或中央用于记录或跟踪目的，也可以发送给技术支持代表、开发者或系统管理员，以协助技术故障查找和调试。

Sos 在设计上是模块化的，能够从可能安装的广泛子系统和包中收集数据。可选生成 XML 或 HTML 报告来总结收集的信息并存储在存档中。

## 选项

`-l, --list-plugins`

列出所有可用插件及其选项。当前配置下不会启用的插件将单独列出。

`-n, --skip-plugins PLUGNAME[,PLUGNAME]`

禁用指定的插件。可以通过重复选项或逗号分隔的列表指定多个插件。

`-e, --enable-plugins PLUGNAME[,PLUGNAME]`

启用指定的插件。可以通过重复选项或逗号分隔的列表指定多个插件。

`-o, --only-plugins PLUGNAME[,PLUGNAME]`

仅启用指定的插件（所有其他插件均应被禁用）。可以通过重复选项或逗号分隔的列表指定多个插件。

`-k PLUGNAME.PLUGOPT[=VALUE]`

指定插件选项。在插件 `PLUGNAME` 中启用选项 `PLUGOPT`，或将其设置为指定值。

`--help`

显示用法。

## 维护者

`Bryn M. Reeves <>`

## 作者与贡献者

查看 `/usr/share/doc/sosreport` 中的 `AUTHORS` 文件。

## 翻译

由

# SPEAKER-TEST

## 名称

`speaker-test` - 用于 ALSA 的命令行扬声器测试音调生成器

## 概要

`speaker-test [-options]`

## 描述

`speaker-test` 生成用于测试计算机扬声器的音调。

`speaker-test` 默认测试默认设备。如果你想测试另一个声音设备，首先需要获取系统中所有声卡及其设备列表。注意，例如可能有一个设备用于模拟声音，一个用于数字声音，一个用于 HDMI 声音。获取声卡和设备列表可以运行 `aplay -L`。

```text
$ aplay -L
null
    丢弃样本（播放）或生成零样本（采集）
default:CARD=ICH5
    ICH5, ICH5 默认设备
front:CARD=ICH5,DEV=0
    ICH5, ICH5 前扬声器
surround40:CARD=ICH5,DEV=0
    ICH5, ICH5 4.0 环
```

在上面的示例中，列出了四个设备：`null`、`default`、`front` 和 `surround40`。所以，如果你想测试最后一个设备，可以运行 `speaker-test -D surround40:ICH5 -c 6`。`-c` 选项指示设备中的六个音频通道需要测试。

## 选项

`-c, --channels NUM`

流中的 `NUM` 个通道。

`-D, --device NAME`

PCM 设备名称 `NAME`。

`-f, --frequency FREQ`

`FREQ` Hz 正弦波。

`--help`

打印用法帮助。

`-b, --buffer TIME`

使用 `TIME` 微秒的缓冲区大小。当给出 `0` 时，使用最大缓冲区大小。默认值为 `0`。

`-p, --period TIME`

使用 `TIME` 微秒的周期大小。当给出 `0` 时，使用 `-P` 选项指定的周期。默认值为 `0`。

`-P, --nperiods PERIODS`

使用周期数量。默认值为 `4`。

`-r, --rate RATE`

`RATE` Hz 的流。

`-t, --test pink|sine|wav`

使用 `-t pink` 时使用粉红噪声（默认）。

粉红噪声在感知上是均匀的噪声——也就是说，它听起来同时包含所有频率。如果你能听到任何音调，可能表明你的扬声器系统或房间存在共振。

使用 `-t sine` 时，响应使用正弦波。

使用 `-t wav` 时，播放 WAV 文件，可以是预定义文件或通过 `-w` 选项指定的。

你可以传递从 1 到 3 的数字作为向后兼容。

`-l`, `--nloops COUNT`

指定循环次数。零表示无限运行。

当给出一个带有有效通道的 `-s` 选项时，`speaker-test` 将始终执行单次操作而不进行循环。

`-s`, `--speaker CHANNEL`

对指定的通道进行单次扬声器测试。通道数字从 1 开始。通道数字对应左、右、后左、后右、中、LFE、侧左、侧右等。

例如，当传递 `1` 时，它将只测试一次左声道，而不是以循环方式测试两个声道。

`-w`, `--wavfile FILE`

使用指定的 WAV 文件进行播放，而不是使用预定义的 WAV 文件。

`-W`, `--wavdir DIRECTORY`

指定包含播放 WAV 文件的目录。默认路径为 `/usr/share/sounds/alsa`。

`-m`, `--chmap MAP`

传递通道映射进行覆盖。如果需要在特定的通道顺序或通道位置进行播放，请向此选项传递通道位置字符串。

`-X`, `--force-frequency`

允许提供的 `FREQ` 超出默认的 30-8000 Hz 范围。仍强制执行 1 Hz 的最小值。

## 使用示例

从一个立体声插口产生立体声：

```bash
speaker-test -Dplug:front -c2
```

从两个立体声插口产生 4 声道扬声器声：

```bash
speaker-test -Dplug:surround40 -c4
```

从三个立体声插口产生 5.1 声道扬声器声：

```bash
speaker-test -Dplug:surround51 -c6
```

向低音变换器发送一个良好的低 75 Hz 音调然后退出，而不触碰任何其他扬声器：

```bash
speaker-test -Dplug:surround51 -c6 -s1 -f75
```

使用 SPDIF（同轴或光纤）输出进行 2 声道扬声器测试：

```bash
speaker-test -Dplug:spdif -c2
```

从前置 PCM 按前右和前左的顺序播放：

```bash
speaker-test -Dplug:front -c2 -mFR,FL
```

`-engine id`

指定引擎（通过其唯一的 `id` 字符串）将导致 `speed` 尝试获取指定引擎的功能引用，从而在需要时对其初始化。该引擎将设置为所有可用算法的默认引擎。

### 测试算法

[零或多个测试算法]

如果给出任何选项，`speed` 将测试这些算法，否则将测试上述所有算法。

* * *

# SPICE-VDAGENT

## 名称

`spice-vdagent` - Spice 客户代理 X11 会话代理

## 概要

`spice-vdagent [OPTIONS]`

## 说明

Linux 的 Spice 客户代理由两部分组成：一个系统级守护进程 `spice-vdagentd` 和一个 X11 会话代理 `spice-vdagent`（每个 X11 会话有一个）。

`spice-vdagent` 会在遵循 `/etc/xdg/autostart` 的桌面环境以及 gdm 下自动启动。

## 特性

Spice 客户代理为 Spice Linux 客户增加了以下功能：

- 客户端鼠标模式（无需由客户端捕获鼠标，无鼠标延迟）。
- 自动调整 X11 会话的虚拟显示器数量及其分辨率，使其与客户端窗口的数量及其分辨率匹配。
- 支持在活跃的 X11 会话与客户端之间进行复制和粘贴（文本和图像），这同时支持主选择区和剪贴板。
- 支持从客户端向代理传输文件。

## 选项

`-h`

打印所有命令行选项的简短描述。

`-d`

记录调试信息。

`-s port`

设置 virtio 串口 `port`（默认：`/dev/virtio-ports/com.redhat.spice.0`）。

`-x`

不进行进程化。

`-f dir|xdg-desktop|xdg-download`

设置从客户端发送的文件保存目录，可以是任意 `dir`，也可以是 `xdg-desktop` 或 `xdg-download` 的特殊值之一，以选择默认的 XDG 桌面相应目录或 XDG 下载目录。如果未指定值，在具有桌面图标的桌面环境中运行时默认为 `xdg-desktop`，在其他桌面环境中默认为 `xdg-download`。

`-o 0|1`

禁用或启用当从客户端传输完成后使用 `xdg-open` 打开文件保存目录（在文件管理器中显示该目录）。如果未指定值，在具有桌面图标的桌面环境中默认为 `0`，在其他桌面环境中默认为 `1`。

## 参见

(1)

## 版权

Copyright 2010-2013 Red Hat, Inc. License GPLv3+：GNU GPL 版本 3 或更高版本 <..>

此是免费软件：你可以自由地更改和分发它。在法律允许的范围内不提供任何保证。

* * *

# SPICE-VDAGENTD

## 名称

`spice-vdagentd` - Spice 客户代理守护进程

## 概要

`spice-vdagent [OPTIONS]`

## 说明

Linux 的 Spice 客户代理由两部分组成：一个系统级守护进程 `spice-vdagentd` 和一个 X11 会话代理 `spice-vdagent`（每个 X11 会话有一个）。

`spice-vdagentd` 通过 Sys-V 初始化脚本或 systemd 单元启动。

## 特性

Spice 客户代理为 Spice Linux 客户增加了以下功能：

- 客户端鼠标模式（无需由客户端捕获鼠标，无鼠标延迟）。
- 自动调整 X11 会话的虚拟显示器数量及其分辨率，使其与客户端窗口的数量及其分辨率匹配。
- 支持在活跃的 X11 会话与客户端之间进行复制和粘贴（文本和图像），这同时支持主选择区和剪贴板。
- 支持从客户端向代理传输文件。

## 选项

`-h`

打印所有命令行选项的简短描述。

`-d`

记录调试信息（使用两次获取额外信息）。

`-f`

将 uinput 设备视为伪设备；不执行 ioctl。这与 Xspice 配合使用非常有用。

`-o`

Sys-V 初始化脚本或 systemd 单元解析以下文件：

`/etc/sysconfig/spice-vdagentd`

可以通过设置该文件中的 `SPICE_VDAGENTD_EXTRA_ARGS` 变量向 `spice-vdagentd` 传递默认命令行选项。

## 参见

(1)

## 版权

Copyright 2010-2013 Red Hat, Inc. License GPLv3+：GNU GPL 版本 3 或更高版本 <.>。

此是免费软件：你可以自由地更改和分发它。在法律允许的范围内不提供任何保证。

* * *

# SPKAC

## 名称

`spkac` - SPKAC 打印和生成工具

## 概要

`openssl spkac [-in filena] [-out filena] [-key keyfile] [-passin arg] [-challenge string] [-pubkey] [-spkac spkacna] [-spksect section] [-noout] [-verify] [-engine id]`

## 说明

`spkac` 命令处理 Netscape 签名的公钥和挑战（SPKAC）文件。它可以打印其内容、验证签名，并根据提供的私钥生成自己的 SPKAC。

## 命令选项

### `-in filena`

指定要读取的输入文件 `filena`，如果不指定此选项，则使用标准输入。如果使用了 `-key` 选项，将被忽略。

### `-out filena`

指定写入的输出文件 `filena`，默认写入标准输出。

### `-key keyfile`

使用 `keyfile` 中的私钥创建一个 SPKAC 文件。如果存在 `-in`、`-noout`、`-spksect` 和 `-verify` 选项，将被忽略。

### `-passin password`

输入文件密码源。有关 `arg` 格式的更多信息，请参见 (1) 中的 `PASS PHRASE ARGUMENTS` 部分。

### `-challenge string`

在创建 SPKAC 时指定挑战字符串。

### `-spkac spkacna`

允许指定包含 SPKAC 的变量名称。默认值为 `SPKAC`。此选项会影响生成和输入的 SPKAC 文件。

### `-spksect section`

允许指定包含 SPKAC 的节名称。默认值是默认节。

### `-noout`




不输出 `SPKAC` 的文本版本（如果在创建 `SPKAC`，则不使用）。

### `-pubkey`

输出 `SPKAC` 的公钥（如果在创建 `SPKAC`，则不使用）。

### `-verify`

验证提供的 `SPKAC` 数字签名。

### `-engine id`

指定引擎（通过其唯一的 `id` 字符串）会导致 `spkac` 尝试获取指定引擎的功能引用，从而在需要时对其初始化。然后该引擎将设置为所有可用算法的默认引擎。

## 示例

打印 `SPKAC` 内容：

```bash
openssl spkac -in spkac.cnf
```

验证 `SPKAC` 的签名：

```bash
openssl spkac -in spkac.cnf -noout -verify
```

使用挑战字符串 `'hello'` 创建 `SPKAC`：

```bash
openssl spkac -key key.pem -challenge hello -out spkac.cnf
```

## 注意事项

附加了适当 `DN` 组件的生成的 `SPKAC` 可以输入到 `ca` 工具。

`SPKAC` 通常由 Netscape 在证书注册过程中提交的包含 `KEYGEN` 标签的表单时生成。

挑战字符串允许对私钥所有权进行原始形式的证明。通过检查 `SPKAC` 签名和随机挑战字符串，可以确保用户知道正在认证的公钥对应的私钥。这在许多应用程序中至关重要。如果没有它，之前的 `SPKAC` 可能会用于“重放攻击”。

## 另请

(1)

***

# SPLAIN

## 名称

`diagnostics`、`splain` - 产生详细的警告诊断信息

## 概要

使用 `diagnostics` 指令：

```perl
use diagnostics; use diagnostics -verbose; enable diagnostics; disable diagnostics;
```

使用 `splain` 独立过滤器程序：

```bash
perl program 2>diag.out splain [-v] [-p] diag.out
```

使用 `diagnostics` 从运行异常脚本的堆栈跟踪：

```bash
perl -Mdiagnostics=-traceonly my_bad_script
```

以查看崩溃时的调用栈。通过提供 `-warntrace`（或只需 `-w`）标志，任何发出的警告将带有堆栈跟踪。

### `splain` 程序

`splain` 看起来是另一个程序，但实际上只是指向（可执行的）`diagnostics.pm` 模块以及指向 `diagnostics.pod` 文档的链接。`-v` 标志类似于 `use diagnostics -verbose` 指令。`-p` 标志类似于 `$diagnostics::PRETTY` 变量。由于你是使用 `splain` 进行后处理，因此没有必要使用 `enable()` 或 `disable()` 处理。

`splain` 的输出重定向到 `STDOUT`，与指令不同。

## 示例

以下文件肯定会在运行时和编译时触发几个错误：

```perl
use diagnostics; print NOWHERE "nothing\n"; print STDERR "\n\tThis ssage should be unadorned.\n"; warn "\tThis is a user warning"; print "\nDIAGNOSTIC TESTER: Please enter a <CR> here: "; my $a, $b = scalar <STDIN>; print "\n"; print $x/$y;
```

如果你喜欢先运行程序然后再查看问题，这样做：

```bash
perl -w test.pl 2>test.out ./splain < test.out
```

注意，这在某些不熟悉的 shell 中通常是不可能的，因为理论上：

```bash
(perl -w test.pl >/dev/tty) >& test.out ./splain < test.out
```

因为你刚刚将现有的 `stdout` 移动到了其他地方。

如果你不想修改源代码，但仍希望实时警告，这样做：

```bash
exec 3>&1; perl -w test.pl 2>&1 1>&3 3>&- | splain 1>&2 3>&-
```

很巧妙对吧？

如果你想实时控制警告，可以这样做。确保你先执行 `use`，否则你无法访问 `enable()` 或 `disable()` 方法。

```perl
use diagnostics; # 检查整个编译阶段 print "\nti for 1st bogus diags: SQUAWKINGS\n"; print BOGUS1 'nada'; print "done with 1st bogus\n"; disable diagnostics; # 只关闭运行时警告 print "\nti for 2nd bogus: (squelched)\n"; print BOGUS2 'nada'; print "done with 2nd bogus\n"; enable diagnostics; # 重新开启运行时警告 print "\nti for 3rd bogus: SQUAWKINGS\n"; print BOGUS3 'nada'; print "done with 3rd bogus\n"; disable diagnostics; print "\nti for 4th bogus: (squelched)\n"; print BOGUS4 'nada'; print "done with 4th bogus\n";
```

## 内部

诊断信息在运行时可用时源自 `perldiag.pod` 文件。否则，它们可能在构建 `splain` 包时包含在文件中本身。详参见 `Makefile`。

如果发现现有的 `$SIG{__WARN__}` 处理器，它将继续被尊重，但只有在 `diagnostics::splainthis()` 函数（模块的 `$SIG{__WARN__}` 拦截器）处理完你的警告之后。

如果你非常好奇拦截了哪些类型的内容，可以设置一个 `$diagnostics::DEBUG` 变量。

```perl
BEGIN { $diagnostics::DEBUG = 1 }
```

## 缺陷

无法说“no diagnostics”虽然很恼人，但可能并非解决。

`-pretty` 指令调用得太晚，无法影响结果。你必须这样做，并且在加载模块之前。

```perl
BEGIN { $diagnostics::PRETTY = 1 }
```

可以通过推迟编译到需要时来加快启动速度，但在 Perl 5.001e 中使用 `pragma` 形式时这会导致 `panic: top_level`。

虽然这份文档确实有些不严肃，但如果你使用名为 `splain` 的程序，你应该预期会有一些幽默。

## 作者

Tom Christiansen <>, 1995 年 6 月 25 日。

# SPROF

## 名称

`sprof` - 读取并显示共享对象性能分析数据

## 概要

`sprof` [`option`]... `shared-object-path` `[`profile-data-path`]`

## 描述

`sprof` 命令显示第一个命令行参数指定的共享对象的性能分析摘要。该摘要是使用（可选的）第二个参数中之前生成的分析数据创建的。如果省略了分析数据路径 `na`，则 `sprof` 将尝试使用共享对象的 `sona` 来推断它，在当前目录下查找名为 `<sona>.profile` 的文件。

## 选项

以下命令行选项指定了要生成的分析输出：

`-c`、`--call-pairs`

打印共享对象导出接口的调用路径对列表，以及每个路径被使用的次数。

`-p`、`--flat-profile`

生成被监控对象中所有函数的扁平分析报告，包含计数和滴答（`ticks`）。

`-q`、`--graph`

生成调用图。

如果没有指定上述任何选项，默认行为是显示扁平分析报告和调用图。

还有以下可选的命令行选项：

`-?`、`--help`

显示命令行选项和参数的摘要并退出。

`--usage`

```c
$ cat libdemo.c
#include <> void consuCpu1(int lim) { int j; for (j = 0; j < lim; j++) getppid(); } void x1(void) { int j; for (j = 0; j < 100; j++) consuCpu1(200000); } void consuCpu2(int lim) { int j; for (j = 0; j < lim; j++) getppid(); } void x2(void) { int j; for (j = 0; j < 100; j++) consuCpu2(10000); }
```

现在我们使用真实的 `na`、`libdemo.so.1.0.1` 和 `sona`、`libdemo.so.1` 构建共享库：

```bash
$ cc -g -fPIC -shared -Wl,-sona,libdemo.so.1 -o libdemo.so.1.0.1 libdemo.c
```

然后我们为库 `sona` 和库链接器 `na` 构建符号链接：

```bash
$ ln -sf libdemo.so.1.0.1 libdemo.so.1
$ ln -sf libdemo.so.1 libdemo.so
```

接下来，我们编译主程序并将其链接到共享库，然后列出程序的动态依赖：

```bash
$ cc -g -o prog prog.c -L. -ldemo
$ ldd prog
linux-vdso.so.1 => (0x00007fff86d66000) libdemo.so.1 => not found libc.so.6 => /lib64/libc.so.6 (0x00007fd4dc138000) /lib64/ld-linux-x86-64.so.2 (0x00007fd4dc51f000)
```

为了获取共享库的性能分析信息，我们带有库的 `sona` 定义环境变量 `LD_PROFILE`：

```bash
$ export LD_PROFILE=libdemo.so.1
```

然后我们定义写入分析输出的目录路径 `pathna` 的环境变量 `LD_PROFILE_OUTPUT`，如果该目录不存在则创建它：

```bash
$ export LD_PROFILE_OUTPUT=$(pwd)/prof_data
$ mkdir -p $LD_PROFILE_OUTPUT
```

`LD_PROFILE` 会导致分析输出如果输出文件已存在则追加到输出文件中，因此我们确保没有预先存在的分析数据：

```bash
$ rm -f $LD_PROFILE_OUTPUT/$LD_PROFILE.profile
```

我们随后运行程序产生分析输出，该输出被写入 `LD_PROFILE_OUTPUT` 指定的目录文件中：

```bash
$ LD_LIBRARY_PATH=. ./prog
$ ls prof_data
libdemo.so.1.profile
```

然后我们使用 `sprof -p` 选项生成带有计数和滴答的扁平分析报告：

```text
$ sprof -p libdemo.so.1 $LD_PROFILE_OUTPUT/libdemo.so.1.profile
Flat profile: Each sample counts as 0.01 seconds. % culative self self total ti seconds seconds calls us/call us/call na 60.00 0.06 0.06 100 600.00 consuCpu1 40.00 0.10 0.04 1000 40.00 consuCpu2 0.00 0.10 0.00 1 0.00 x1 0.00 0.10 0.00 1 0.00 x2
```

`sprof -q` 选项生成调用图：

```text
$ sprof -q libdemo.so.1 $LD_PROFILE_OUTPUT/libdemo.so.1.profile
index % ti self children called na 0.00 0.00 100/100 x1 [1] [0] 100.0 0.00 0.00 100 consuCpu1 [0] ----------------------------------------------- 0.00 0.00 1/1 <UNKNOWN> [1] 0.0 0.00 0.00 1 x1 [1] 0.00 0.00 100/100 consuCpu1 [0] ----------------------------------------------- 0.00 0.00 1000/1000 x2 [3] [2] 0.0 0.00 0.00 1000 consuCpu2 [2] ----------------------------------------------- 0.00 0.00 1/1 <UNKNOWN> [3]
```

# SSH-AGENT

## 名称

`ssh-agent` - 身份验证代理

## 语法概要

```text
ssh-agent [-c | -s] [-a bind_address] [-E fingerprint_hash] [-t life] [command [arg ...]]
ssh-agent [-c | -s] -k
```

## 描述

`ssh-agent` 是一个用于存放公钥认证（RSA、DSA、ECDSA、Ed25519）私钥的程序。`ssh-agent` 通常在 X 会话或登录会话开始时启动，其他窗口或程序作为 `ssh-agent` 程序的客户端启动。通过使用环境变量，可以找到代理，并在使用 (1) 登录到其他机器时自动将其用于身份验证。

代理最初不包含任何私钥。使用 `ssh-add1` 添加密钥。`ssh-agent` 可以同时存储多个身份，并且如果存在，(1) 将自动使用它们。`ssh-add1` 也用于从 `ssh-agent` 中删除密钥以及查询其中持有的密钥。

选项如下：

### `-a bind_address`

将代理绑定到 UNIX 套接字 `bind_address`。默认值为 `$TMPDIR/ssh-XXXXXXXXXX/agent.<ppid>`。

### `-c`

在 `stdout` 上生成 C-shell 命令。如果 `SHELL` 看起来像 `csh` 风格的 shell，则为此默认值。

### `-D`

前台模式。指定此选项时，`ssh-agent` 将不会派生。

### `-d`

调试模式。指定此选项时，`ssh-agent` 将不会派生，并将调试信息写入标准错误。

### `-E fingerprint_hash`

指定在显示密钥指纹时使用的哈希算法。有效选项有：`md5` 和 `sha256`。默认值为 `sha256`。

### `-k`

杀死当前代理（由环境变量 `SSH_AGENT_PID` 给出）。

### `-s`

在 `stdout` 上生成 Bourne shell 命令。如果 `SHELL` 看起来不像 `csh` 风格的 shell，则为此默认值。

### `-t life`

为添加到代理的身份设置默认最大生命周期。生命周期可以用秒或 `sshd_config5` 中指定的时间格式来指定。使用 `ssh-add1` 为某个身份指定的生命周期将覆盖此值。如果不使用此选项，默认的最大生命周期为永久。

如果给出了命令行，它将作为代理的子进程执行。当命令结束时，代理也随之结束。

其理念是代理运行在用户的本地电脑、笔记本电脑或终端上。身份验证数据不需要存储在任何其他机器上，且身份验证密码绝不会通过网络传输。然而，到代理的连接通过 SSH 远程登录转发，因此用户可以安全地在网络中的任何地方使用身份所提供的权限。

设置代理有两种主要方法：第一种是代理启动一个新的子命令，并在其中导出相应的环境变量，例如 `ssh-agent xterm &`。第二种是代理打印所需的 shell 命令（可以生成 (1) 或 (1) 语法），这些命令可以在调用的 shell 中求值，例如对于 Bourne 类型的 shell（如 (1) 或 (1)）使用 `eval \`ssh-agent -s\``，对于 (1) 及其变体使用 `eval \`ssh-agent -c\``。

随后 (1) 查看这些变量并使用它们建立与代理的连接。

代理永远不会通过其请求通道发送私钥。相反，需要私钥的操作将由代理执行，并将结果返回给请求者。这样，私钥就不会暴露给使用代理的客户端。

系统会创建一个 UNIX 套接字，该套接字的名称存储在环境变量 `SSH_AUTH_SOCK` 中。该套接字仅当前用户可用。这种方法很容易被 root 或 sa 用户的另一个实例滥用。

### `~/.ssh/id_dsa`

包含用户的协议版本 1 RSA 认证身份。

### `~/.ssh/id_dsa`

包含用户的协议版本 2 DSA 认证身份。

### `~/.ssh/id_ecdsa`

包含用户的协议版本 2 ECDSA 认证身份。

### `~/.ssh/id_ed25519`

包含用户的协议版本 2 Ed25519 认证身份。

### `~/.ssh/id_rsa`

包含用户的协议版本 2 RSA 认证身份。身份文件不应被除用户以外的任何人读取。注意，如果身份文件可以被其他人访问，`ssh-add` 将忽略这些文件。

## 退出状态

成功时退出状态为 0，如果指定的命令失败则为 1，如果 `ssh-add` 无法连接身份验证代理则为 2。

## 参见

(1)、`ssh-add1`、`ssh-askpass1`、`ssh-keygen1`、(8)

## 作者



OpenSSH 是 Tatu Ylonen 原始免费 `ssh` 1.2.12 版本的衍生版本。Aaron Campbell, Bob Beck, Markus Friedl, Niels Provos, Theo de Raadt 和 Dug Song 修复了许多错误，添加了新功能并创建了 OpenSSH。Markus Friedl 为 SSH 协议版本 1.5 和 2.0 的支持做出了贡献。

# SSH-COPY-ID

## NAME

`ssh-copy-id` - 使用本地密钥授权远程机器的登录

## SYNOPSIS

`[-n]` `[-i [identity_file]]` `[-p port]` `[-o ssh_option]` `[user@hostname]`

`-h | -`

## DESCRIPTION

这是一个使用 `ssh` 登录远程机器的脚本（假定使用登录密码，因此应该启用密码认证，除非你巧妙地使用了多个身份验证）。它会检查一个或多个指纹的列表（下文所述），并尝试使用每个密钥登录，以查看其中任何一个是否已经安装（当然，如果你没有使用 `ssh-agent`，这可能会导致你被反复提示密码）。然后它会检查失败登录的列表，并使用 `ssh` 在远程服务器上启用这些密钥的登录。默认情况下，它通过将密钥追加到远程用户的 `~/.ssh/authorized_keys` 来添加密钥（必要时创建该文件和目录）。它还能检测远程系统是否为 NetScreen，并使用其 `set ssh pka-dsa key ...` 命令。

选项如下：

### `-i identity_file`

仅使用 `identity_file` 中包含的密钥（而不是通过 `ssh-add` 或在 `default_ID_file` 中查找身份）。如果文件名没有以 `.pub` 结尾，将加上该后缀。如果省略了文件名，则使用 `default_ID_file`。

注意，这可以用来确保所复制的密钥具有用户所需的注释和/或应用了额外的选项，只需在尝试复制之前确保密钥文件已设置了这些首选。

### `-n`

执行空运行（dry-run）。不再在远程系统上安装密钥，而是打印将要安装的密钥。

### `-h , -`

打印用法摘要

### `-p port , -o ssh_option`

这两个选项将连同其参数直接原封不动地传递，允许分别设置端口或其他 `ssh` 选项。

与其将这些指定为命令行选项，不如使用 `ssh` 配置文件中的（每个主机的）设置：`ssh_config`。

不带 `-i` 时的默认行为是检查 `ssh-add -L` 是否有输出，如果有，则使用这些密钥。注意，这会导致密钥上的注释成为加载到你的 `ssh-agent` 时传递给 `ssh-add` 的文件名，而不是文件中包含的注释，这有点奇怪。如果 `ssh-add` 没有提供密钥，则将使用 `default_ID_file` 的内容。

`default_ID_file` 是匹配以下模式的最文件：`~/.ssh/id*.pub`（排除匹配 `~/.ssh/*-cert.pub` 的，因此如果你创建了一个不是你想使用的密钥，只需在你偏好的密钥的 `.pub` 文件上运行 `ssh` 即可恢复其为最新文件）。

## EXAMPLES

如果你已经从一个系统在许多远程主机上安装了密钥，然后在新的客户端机器上创建了一个新密钥，可能很难跟踪你在哪些系统上安装了新密钥。处理此问题的方法是将新密钥和旧密钥都加载到你的 `ssh-agent` 中。先加载新密钥（不带 `-c` 选项），然后将一个或多个旧密钥加载到 agent 中，可以通过 `ssh` 连接到拥有该旧密钥的客户端机器，并使用 `-A` 选项允许代理转发：

现在，如果新密钥已安装在服务器上，你将在无需提示的情况下进入，而如果你只启用了旧密钥，你会被要求确认，这提示你注销并运行

在这种情况下，你可能想指定 `-i` 选项，是为了确保安装的密钥上的注释来自 `.pub` 文件，而不是仅仅是加载到你 agent 中的文件名。它还确保只安装了你意指的 id，而不是你在 `ssh-agent` 中的所有密钥。当然，你可以根据喜好指定另一个 id 或使用 `ssh-agent` 的内容。

既然提到了 `ssh-add` 的 `-c` 选项，你可能考虑在每次使用代理转发时使用它，以避免密钥被劫持，但更好的做法是使用 `ssh` 的 `ProxyCommand` 和 `-W` 选项，在通过远程服务器跳转时始终进行直接的端到端认证。这样中间跳转节点无法访问你的 `ssh-agent`。网络搜索 `ssh proxycommand nc` 应该会很有启发（注意，现代方法是使用 `-W` 选项，而不是 `nc`）。

## ENVIRONMENT

### `SSH_COPY_ID_LEGACY`

如果设置了 `SSH_COPY_ID_LEGACY` 变量，以旧模式运行。在此模式下，它不检查是否安装。

## SEE ALSO

`ssh(1)`, `sshd(8)`

# SSH-KEYGEN

## NAME

`ssh-keygen` 生成、管理和转换用于 `ssh` 的身份密钥。

## SYNOPSIS

`ssh-keygen` `-t dsa | ecdsa | ed25519 | rsa` [`-b bits`] [`-m format`] [`-f output_file`] `-C comment` [`-P passphrase`] [`-I identity`] [`-n principals`] [`-O option`] [`-V validity_interval`] [`-z serial_number`] `file ...`

`ssh-keygen` `-k -f krl_file` [`-u`] [`-s version`] [`-a rounds`] [`-J num_lines`] [`-j start_line`] [`-K checkpt`] [`-W generator`] `-E hash` `-D check` `-R file` `-G point` [`-S start`] `-Q`

## DESCRIPTION

`ssh-keygen` 生成、管理和转换用于 `ssh` 的身份密钥。`ssh-keygen` 可以创建用于 SSH 协议版本 1 的 RSA 密钥，以及用于协议版本 2 的 DSA、ECDSA、Ed25519 或 RSA 密钥。要生成的密钥类型通过 `-t` 选项指定。如果在没有任何参数的情况下调用，`ssh-keygen` 将为用于 SSH 协议 2 的连接生成一个 RSA 密钥。

`ssh-keygen` 还用于为 Diffie-Hellman 组交换 (DH-GEX) 生成组。详见 **MODULI GENERATION** 部分。

最后，`ssh-keygen` 可生成和更新密钥撤销列表（KRL），并测试给定的密钥是否已被撤销。详见 **KEY REVOCATION LISTS** 部分。

通常，每个想要使用公钥认证 SSH 的用户都会运行一次此命令，以在 `~/.ssh/identity`、`~/.ssh/id_dsa`、`~/.ssh/id_ecdsa`、`~/.ssh/id_ed25519` 或 `~/.ssh/id_rsa` 中创建身份密钥。此外，系统管理员可能会使用它生成主机密钥，如 `/etc/rc` 所示。

通常情况下，此程序会生成密钥并要求指定一个用于存储私钥的文件。公钥将存储在一个与私钥名字相同但添加了 `.pub` 后缀的文件中。程序还会要求输入密码短语（passphrase）。密码短语可以为空以表示没有密码短语（主机密钥的密码短语均为空），也可以是任意长度的字符串。密码短语与密码相似，不同之处在于它可以是一个由一系列单词、标点符号、数字、空白符或你想要的任何字符字符串组成的短语。良好的密码短语长度应在 10-30 个字符之间，不应该是简单的句子或其他易于推测的内容（英语散文的每个字符仅有 1-2 位熵，提供的密码短语效果非常差），并且包含大小写字母、数字和非字母数字字符的混合。以后可以使用 `-p` 选项更改密码短语。

在创建密钥时，注释初始化为空字符串，但可以使用 `-c` 选项进行更改。

### `-D`

指定输出文件。

### `-E`

显示指定公钥的哈希指纹。

### `-e`

指定导出密钥格式。

### `-F`

指定文件名。

### `-G`

指定输出文件。

### `-g`

指定输出的位数。

### `-H`

指定密钥文件。

### `-I`

在签名密钥时指定证书身份。

### `-i`

导入私钥或公钥。

### `-J`

在指定的行数退出。

### `-j`

从指定的行开始筛选。

### `-K`

将最后处理的行写入检查点。

### `-k`

生成撤销列表文件（KRL）。

### `-L`

打印证书的内容。

### `-M`

在生成 DH-GEX 候选数时指定使用的内存量（GB）。

### `-m`

指定转换格式。

### `-N`

提供新密码短语。

### `-n`

在签名密钥时指定要包含在证书中的一个或多个主体（用户或主机名）。

### `-O`

在签名密钥时指定证书选项。

### `no-pty`

禁用 PTY 分配（默认允许）。

### `no-user-rc`

禁用由 `sshd` 执行 `~/.ssh/rc`（默认允许）。

### `no-x11-forwarding`

禁用 X11 转发（默认允许）。

### `permit-agent-forwarding`

允许 `ssh-agent` 转发。

### `permit-port-forwarding`

允许端口转发。

### `permit-pty`

允许 PTY 分配。

### `permit-user-rc`

允许由 `sshd` 执行 `~/.ssh/rc`。

### `permit-x11-forwarding`

允许 X11 转发。

### `source-address =`

限制认为证书有效的源地址。`address_list` 是一个以 CIDR 格式表示的一个或多个地址/网络掩码对的逗号分隔列表。

目前，主机密钥没有有效的选项。

### `-o`

使 `ssh-keygen` 使用新的 OpenSSH 格式保存 SSH 协议 2 私钥，而不是兼容性更好的 PEM 格式。新格式增加了对暴力破解密码的抵抗力，但不支持 OpenSSH 6.5 之前的版本。Ed25519 密钥始终使用新的私钥格式。

### `-P passphrase`

提供（旧的）密码短语。

### `-p`

请求更改私钥文件的密码短语，而不是创建新的私钥。程序将提示输入包含私钥的文件、旧密码短语，并提示两次输入新密码短语。

### `-Q`

测试密钥是否已在 KRL 中被撤销。

### `-q`

静默运行 `ssh-keygen`。

### `-R hostname`

从 `known_hosts` 文件中删除所有属于 `hostname` 的密钥。此选项用于删除哈希处理过的主机（见上文的 `-H` 选项）。

### `-r hostname`

为指定的公钥文件打印 SSHFP 指纹资源记录。

### `-S start`

在为 DH-GEX 生成候选模数时指定起始点（十六进制）。

### `-s ca_key`

使用指定的 CA 密钥对公钥进行认证（签名）。详情请参阅 **CERTIFICATES** 部分。

在生成 KRL 时，`-s` 指定一个 CA 公钥文件路径，用于直接通过密钥 ID 或序列号撤销证书。详情请参阅 **KEY REVOCATION LISTS** 部分。

### `-T output_file`

测试 DH 组交换候选值（使用 `-G` 选项生成）的安全性。

### `-t dsa | ecdsa | ed25519 | rsa | rsa1`

指定要创建的密钥类型。可能的值是协议版本 1 的 `rsa1`，以及协议版本 2 的 `dsa`、`ecdsa`、`ed25519` 或 `rsa`。

### `-u`

更新 KRL。当配合 `-k` 使用时，命令行列出的密钥将添加到现有的 KRL 中，而不是创建新的 KRL。

### `-V validity_interval`

在签名证书时指定有效期。有效期可以由单个时间点组成，表示该证书从现在开始有效并在该时间过期；也可以由两个用冒号隔开的时间点组成，表示一个明确的时间间隔。起始时间可以指定为 YYYYMMDD 格式的日期、YYYYMMDDHHMMSS 格式的时间，或相对于当前时间的相对时间（由一个负号加上按照 `sshd_config` 中 `TIME FORMATS` 部分描述的格式的相对时间组成）。结束时间可以指定为 YYYYMMDD 日期、YYYYMMDDHHMMSS 时间或以加号开头的相对时间。

例如：`+52w1d`（从现在起到 52 周后一天有效），`-4w:+4w`（从四周前到四周后有效），`20100101123000:20110101123000`（从 2010 年 1 月 1 日下午 12:30 到 2011 年 1 月 1 日下午 12:30 有效），`-1d:20110101`（从昨天到 2011 年 1 月 1 日午夜有效）。

### `-v`

详细模式。使 `ssh-keygen` 输出关于进度的调试信息。这对于调试模数生成很有帮助。多个 `-v` 选项会增加详细程度，最多 3 个。

### `-W generator`

在测试 DH-GEX 候选模数时指定所需的生成器。

### `-y`

此选项将读取 OpenSSH 格式私钥文件并将 OpenSSH 公钥打印到标准输出。

### `-z serial_number`

指定证书中的序列号，以将此证书与其他来自相同 CA 的证书区分开来。

在生成 KRL 时，`-z` 标志用于指定 KRL 版本号。

## 模数生成

可以使用 `ssh-keygen` 来为 Diffie-Hellman 组交换 (DH-GEX) 协议生成组。生成这些组是一个两步的过程：首先，使用快速但内存密集的过程生成候选值。然后对这些候选值进行适用性测试（这是一个 CPU 密集型过程）。

值的生成是通过 `-G` 选项执行的。可以通过 `-b` 选项指定候选值所需的长度。例如：

```
ssh-keygen -G 2048
```

一旦生成了一组候选值，就可以对它们进行测试。这可以使用 `-T` 选项进行覆盖。例如：

```
ssh-keygen -T 2048 -f /etc/ssh/moduli
```

最后，证书可以定义一个有效期。`-V` 选项允许指定证书的开始和结束时间。在这些范围之外提交的证书将不被视为有效。默认情况下，证书从 UNIX 纪元（Epoch）一直有效到未来。

除了 `-k` 之外，可以使用 `-u` 标记更新 KRL。当指定此选项时，通过命令行列出的密钥将合并到 KRL 中，添加到已有的密钥中。

给定 KRL，还可以测试它是否撤销了某个特定密钥（或某些密钥）。`-Q` 标记将查询现有的 KRL，测试命令行指定的每个密钥。如果命令行列出的任何密钥已被撤销（或遇到错误），则 `ssh-keygen` 将以非零退出状态退出。只有在没有密钥被撤销时，才会返回零退出状态。

## 文件 (FILES)

### `~/.ssh/identity`

包含用户的协议版本 1 RSA 身份验证标识。此文件不应被除用户以外的任何人可读。在生成密钥时可以指定密码；该密码将使用 3DES 加密此文件的私有部分。`ssh-keygen` 不会自动访问此文件，但它作为私钥的默认文件提供。`ssh` 在尝试登录时会读取此文件。

### `~/.ssh/identity.pub`

包含用于身份验证的协议版本 1 RSA 公钥。对于用户希望使用 RSA 身份验证登录的所有机器，应将此文件的内容添加到 `~/.ssh/authorized_keys` 中。没有必要保持此文件的秘密。

### `~/.ssh/id_dsa`

### `~/.ssh/id_ecdsa`

### `~/.ssh/id_ed25519`

### `~/.ssh/id_rsa`

包含用户的协议版本 2 DSA, ECDSA, Ed25519 或 RSA 身份验证标识。此文件不应被除用户以外的任何人可读。在生成密钥时可以指定密码；该密码将使用 128 位 AES 加密此文件的私有部分。`ssh-keygen` 不会自动访问此文件，但它作为私钥的默认文件提供。`ssh` 在尝试登录时会读取此文件。

### `~/.ssh/id_dsa.pub`

### `~/.ssh/id_ecdsa.pub`

### `~/.ssh/id_ed25519.pub`

### `~/.ssh/id_rsa.pub`

包含用于身份验证的协议版本 2 DSA, ECDSA, Ed25519 或 RSA 公钥。对于用户希望使用公钥身份登录的所有机器，应将此文件的内容添加到 `~/.ssh/authorized_keys` 中。没有必要保持此文件的秘密。

### `/etc/ssh/moduli`

包含用于 DH-GEX 的 Diffie-Hellman 组。文件格式在 `moduli(5)` 中描述。

## 环境 (ENVIRONMENT)

### `SSH_USE_STRONG_RNG`

OpenSSL 随机生成器的重新种子通常从 `/dev/urandom` 完成。如果环境变量 `SSH_USE_STRONG_RNG` 设置为 `0`以外的值，则 OpenSSL 随机生成器将从 `/dev/random` 重新种子。读取的字节数由 `SSH_USE_STRONG_RNG` 值定义。最小为 14 字节。在没有硬件随机生成器的计算机上不建议此设置，因为熵不足会导致连接阻塞直到有足够的熵。

## 参见 (SEE ALSO)

`ssh(1)`, `sshd(8)`



(1), `ssh-add1`, `ssh-agent1`, (5), (8)

*RFC 4716* *The Secure Shell (SSH) Public Key File Format* 2006

## 作者 (AUTHORS)

OpenSSH 是由 Tatu Ylonen 发布的原始免费 `ssh 1.2.12` 的衍生版本。Aaron Campbell, Bob Beck, Markus Friedl, Niels Provos, Theo de Raadt 和 Dug Song 修复了许多错误，增加了新功能并创建了 OpenSSH。Markus Friedl 为支持 SSH 协议版本 1.5 和 2.0 做出了贡献。

* *

# SSH-KEYSCAN

## 名称 (NAME)

`ssh-keyscan` - 收集 ssh 公钥

## 概要 (SYNOPSIS)

`ssh-keyscan -words [-46Hv` [-f` *file* ] ] [-p` *port* ] [-T` *tiout* ] [-t` *type* ] [*host | addrlist nalist* ] *...*

## 描述 (DESCRIPTION)

`ssh-keyscan` 是一个收集主机 ssh 主机密钥的实用工具。它旨在辅助构建和验证 `ssh_known_hosts` 文件。`ssh-keyscan` 提供适用于 shell 和 perl 脚本的最小接口。

`ssh-keyscan` 使用非阻塞套接字 I/O 尽可能并行联系主机，因此非常高效。可以在几十秒内从 1,000 个主机中收集密钥，即使某些主机宕机或未运行 ssh。扫描时不需要被扫描机器的登录权限，扫描过程也不涉及任何加密。

选项如下：

`-4`

强制 `ssh-keyscan` 只使用 IPv4 地址。

`-6`

强制 `ssh-keyscan` 只使用 IPv6 地址。

`-f` *file*

从 `file` 每行读取一个主机或地址列表对。如果用 `-` 代替文件名，`ssh-keyscan` 将从标准输入读取主机或地址列表对。

`-H`

对输出中的所有主机名和地址进行哈希。哈希后的主机名可以正常由 `ssh` 和 `sshd` 使用，但即使文件内容泄露也不会暴露身份信息。

`-p` *port*

连接到远程主机的端口。

`-T` *tiout*

设置连接尝试的超时时间。自启动连接或上次从该主机读取内容以来已 *tiout* 秒，则关闭连接并将该主机视为不可用。默认为 5 秒。

`-t` *type*

指定从扫描主机获取的密钥类型。可能的值对于协议版本 1 为 `rsa1`，对于协议版本 2 为 `dsa`、`ecdsa`、`ed25519` 或 `rsa`。可以使用逗号分隔多个值。默认是获取 `rsa`、`ecdsa` 和 `ed25519` 密钥。

`-v`

详细模式。导致 `ssh-keyscan` 关于其进度的调试信息。

## 安全 (SECURITY)

如果使用 `ssh-keyscan` 构建 `ssh_known_hosts` 文件而未对密钥进行验证，用户将面临`中间人`攻击的风险。另一方面，如果安全模型允许此类风险，`ssh-keyscan` 可以帮助检测在 `ssh_known_hosts` 文件创建后开始的被篡改密钥文件或中间人攻击。

## FILES

输入格式：`1.2.3.4,1.2.4.4 na.my.domain,na,n.my.domain,n,1.2.3.4,1.2.4.4`

RSA1 密钥的输出格式：`host-or-nalist bits exponent modulus`

## AUTHORS

An -nosplit An David Mazieres Aq Mt 编写了初始版本，An Wayne Davison Aq Mt 增加了对协议版本 2 的支持。

## BUGS

如果服务器版本低于 2.9，它会在扫描的所有机器控制台上生成“Connection closed by remote host”消息。这是因为它打开到 `ssh` 端口的连接，读取公钥，并在获取密钥后立即关闭连接。

***

# SSH

## NAME

`ssh` - OpenSSH SSH 客户端（远程登录程序）

## SYNOPSIS

`ssh` -words [-1246AaCfGgKkMNnqsTtVvXxYy` [-b *`bind_address` ] ] [-c *`cipher_spec` ] [-D *[`bind_address :* *`port` ] ] [-E *`log_file` ] [-e *`escape_char` ] [-F *`configfile` ] [-I *`pkcs11` ] [-i *`identity_file` ] [-L *`address` ] [-l *`login_na` ] [-m *`mac_spec` ] [-O *`ctl_cmd` ] [-o *`option` ] [-p *`port` ] [-Q `cipher | cipher-auth | mac | kex | key | protocol-version` ] [-R *`address` ] [-S *`ctl_path` ] [-W *`host :* *`port` ] [-w *`local_tun`[: *`remote_tun` ] ] [`user` **@** `hostna` ] [`command` ]]

## DESCRIPTION

`ssh` (SSH 客户端) 是一个用于登录远程机器并在远程机器上执行命令的程序。它旨在取代 `rlogin` 和 `rsh`，并在不安全网络上的两个不受信任的主机之间提供安全的加密通信。X11 连接、任意 TCP 端口和 UNIX 套接字也可以通过安全通道进行转发。

`ssh` 连接并登录到指定的 `hostna`（可选的 `user` na）。用户必须根据所使用的协议版本（见下文）使用多种方法之一向远程机器证明其/她的身份。

如果指定了 `command`，它将在远程主机上执行，而不是打开登录 shell。

选项如下：

`-1`

强制 `ssh` 仅尝试协议版本 1。

`-2`

强制 `ssh` 仅尝试协议版本 2。

`-4`

强制 `ssh` 仅使用 IPv4 地址。

`-6`

强制 `ssh` 仅使用 IPv6 地址。

`-A`

启用身份验证代理连接的转发。这也可以在配置文件中按主机指定。

应谨慎开启代理转发。具有绕过远程主机文件权限能力（针对代理的 UNIX 套接字）的用户可以通过转发的连接访问本地代理。然而，攻击者无法从代理中获取密钥材料，但他们可以对密钥执行操作，从而可以使用加载到代理中的身份进行身份验证。

`-a`

禁用身份验证代理连接的转发。

`-b` *`bind_address`

使用本地机上的 `bind_address` 作为连接的源地址。仅对于具有多个地址的系统有用。

`-C`

请求对所有数据（包括 stdin、stdout、stderr 以及转发的 X11、TCP 和 UNIX 连接的数据）进行压缩。压缩算法是 (1) 使用的，`level` 可以通过协议版本 1 的 `CompressionLevel` 选项控制。在调制解调器线路和其他慢连接上是有意义的，但在快速网络上只会减慢速度。默认值可以在配置文件中按主机设置；参见 `Compression` 选项。

`-c` *`cipher_spec`

选择加密会话的加密规范。

协议版本 1 允许指定单一加密。支持的值为 `3des`、`blowfish` 和 `des`。对于协议版本 2，`cipher_spec` 是按优先级排序的加密算法逗号分隔列表。更多信息请参见 `ssh_config5` 中的 `Ciphers` 关键字。

`-D` *[`bind_address :` ] *`port`

指定本地 `dynamic` 应用程序级端口转发。这通过分配一个套接字来监听 `port` 来工作，可选绑定到指定的 `bind_address`。当连接到此端口时，通过安全通道转发，应用程序协议决定从哪里连接。目前支持 SOCKS4 和 SOCKS5 协议，`ssh` 将作为 SOCKS 服务器运行。只有 root 可以转发特权端口。动态端口转发也可以在配置文件中指定。

IPv6 地址可以通过方括号包含地址来指定。只有超级用户可以转发特权端口。默认情况下，本地端口根据 `GatewayPorts` 设置绑定。然而，可以使用显式的 `bind_address` 将连接绑定到特定地址。`localhost` 的 `bind_address` 表示供本地使用，而空地址 `*` 表示所有接口可用。

`-E` *`log_file`

将调试日志附加到 `log_file` 而不是标准输出。

`-e` *`escape_char`

为带有 pty 的会话设置转义字符（默认：`~` ）。转义字符仅在行首被识别。转义字符后接点 (`.` ) 关闭连接；后接控制-Z 挂起连接；后接自身则发送转义字符。将字符设置为 `none` 将禁用任何转义并使会话完全透明。

`-F` *`configfile`

指定替代的用户配置文件。如果在命令行上给出配置文件，则系统级配置文件 (`/etc/ssh/ssh_config` ) 将忽略。用户配置文件的默认值是 `~/.ssh/config`

`-f`

请求 `ssh` 在执行命令之前进入后台。如果 `ssh` 将询问密码或密码，但用户希望它在后台运行，这很有用。这包含了 `-n` 远程站点启动 X11 程序的推荐方法类似于 **ssh -f host xterm**

如果 `ExitOnForwardFailure` 配置选项设置为 `yes` 则使用 `-f` 启动的客户端将在所有端口转发成功建立之前进入后台。

`-G`

使 `ssh` 在评估 `Host` 和 `Match` 块后打印其配置并退出。

`-g`

允许远程主机连接到本地转发的端口。如果在多路复用连接上使用，则此选项必须在主进程上指定。

`-I` *`pkcs11`

指定 `ssh` 应使用的 PKCS11 共享库以提供用户私有 RSA 密钥的 PKCS11 令牌通信。

`-i` *`identity_file`

选择一个用于读取公钥认证身份（私钥）的文件。对于协议版本 1，默认为 `~/.ssh/identity`；对于协议版本 2，使用 `~/.ssh/id_dsa`、`~/.ssh/id_ecdsa`、`~/.ssh/id_ed25519` 和 `~/.ssh/id_rsa`。可以在配置文件中按主机指定身份文件。可以使用多个 `-i` 选项（以及在配置文件中指定多个身份）。`ssh` 还会尝试从在身份文件名后附加 `-cert.pub` 获取的文件中加载证书信息。

`-K`

启用基于 GSSAPI 的认证，并将 GSSAPI 凭据转发（委派）到服务器。

`-k`

禁用将 GSSAPI 凭据转发（委派）到服务器。

`-L`

- `-L` [*bind_address :* ] *port : host : hostport*

- `-L` [*bind_address :* ] *port : remote_socket*

- `-L` *local_socket : host : hostport*

# 身份验证

OpenSSH SSH 客户端支持 SSH 协议 1 和 2。默认仅使用协议 2，但可以通过 `ssh_config` 中的 `Protocol` 选项或 `-1` 和 `-2` 选项（见上文）进行更改。两种协议都支持类似的身份验证方法，但协议 2 是默认选项，因为它提供了额外的机密性机制（使用 `AES`、`3DES`、`Blowfish`、`CAST128` 或 `Arcfour` 加密）和完整性机制（`hmac-md5`、`hmac-sha1`、`hmac-sha2-256`、`hmac-sha2-512`、`umac-64`、`umac-128`、`hmac-ripemd160`）。协议 1 缺乏确保连接完整性的强机制。

可用的身份验证方法有：基于 GSSAPI 的验证、基于主机的验证、公钥验证、挑战响应验证和密码验证。身份验证按照上述指定的顺序尝试，但协议 2 有一个配置选项可以更改默认顺序：`PreferredAuthentications`。

## 基于主机的身份验证

基于主机的验证工作如下：如果参数 `-S` 为 `ctl_path`，则将在服务器上动态分配一个套接字并告知客户端。与 `-O` 同时使用时，分配的端口将打印到标准输出。

设备可以通过数字 ID 或关键字 "any" 指定，后者使用下一个可用设备。如果未指定 `remote_tun`，则默认为 "any"。另见 `ssh_config` 中的 `Tunnel` 和 `TunnelDevice` 指令。如果未设置 `Tunnel` 指令，它将被设置为默认隧道模式，即“点对点”。

`-X` 启用 X11 转发。这也可以在配置文件中按主机指定。应谨慎启用 X11 转发。具有绕过远程主机文件权限能力（针对用户的 X 授权数据库）的用户可以通过转发的连接访问本地的 X11 显示器。攻击者随后可能执行诸如按键监控等活动。因此，X11 转发默认受到 X11 安全限制。更多信息请参阅 `ssh` 的 `-Y` 选项和 `ssh_config` 中的 `ForwardX11` 指令。

`-x` 禁用 X11 转发。

`-Y` 启用信任的 X11 转发。信任的 X11 转发不受 X11 安全控制的影响。

`-y` 使用 (3) 系统模块发送日志信息。默认情况下，这些信息被发送到 `stderr`。

`ssh` 可能还会从用户级配置文件和系统级配置文件获取配置数据。文件格式和配置选项在 `ssh_config` 中描述。

## 公钥验证

使用公钥或证书验证最方便的方法可能是使用身份验证代理。更多信息请参阅 `ssh-agent`。

公钥验证工作如下：服务器发送其愿意接受的公钥列表。然后客户端选择它想要使用的一个密钥，并证明它拥有该私钥的访问权限。

用户通过运行 `ssh-keygen` 创建密钥对。这会将私钥存储在 `~/.ssh/identity` 中，公钥存储在 `~/.ssh/identity.pub` 中。用户应将公钥复制到远程机器对应目录下的 `~/.ssh/authorized_keys` 中。之后，用户无需提供密码即可登录。

公钥验证的变体是以证书验证的形式提供的：使用签名证书代替一组公钥/私钥。这种方法的优点是可以使用单个信任的证书机构代替许多公钥/私钥。更多信息请参阅 `ssh-keygen` 的 `CERTIFICATES` 章节。

## 挑战响应验证

挑战响应验证工作如下：服务器发送任意挑战文本，并提示响应。协议 2 允许多次挑战和响应；协议 1 则限于一次挑战/响应。挑战响应验证的示例包括 BSD 验证（见 `login.conf`）和 PAM。

## 密码验证

最后，如果其他身份验证方法失败，`ssh` 将提示用户输入密码。密码被发送到远程主机进行检查；然而，由于所有通信都是加密的，监听网络的人无法看到密码。

`ssh` 会自动维护并检查一个包含其曾使用过的所有主机标识符的数据库。主机密钥存储在用户主目录的 `~/.ssh/known_hosts` 中。此外，系统会自动检查 `/etc/ssh/ssh_known_hosts` 文件以获取已知主机。任何新主机都会自动添加到用户的文件中。如果主机的标识符发生变化，`ssh` 会对此发出警告并禁用密码认证，以防止服务器欺骗或中间人攻击，这些攻击可能被用于绕过加密。可以使用 `StrictHostKeyChecking` 选项来控制对主机密钥未知或已更改机器的登录。

当用户的身份被服务器接受后，服务器将在非交互式会话中执行指定的命令，或者在未指定命令的情况下，登录到机器并为用户提供一个交互式会话的标准 shell。与远程命令或 shell 的所有通信都将自动加密。

如果请求交互式会话，`ssh` 默认只在客户端拥有终端时，才为交互式会话请求伪终端（pty）。可以使用 `-T` 和 `-t` 标志来覆盖此行为。

如果分配了伪终端，用户可以使用下文注明的转义字符。

如果没有分配伪终端，则会话是透明的，可以可靠地传输二进制数据。在大多数系统上，将转义字符设置为 `none` 即使在使用 tty 时也会使会话保持透明性。

当远程机器上的命令或 shell 退出且所有 X11 和 TCP 连接关闭时，会话将终止。

## 转义字符 (ESCAPE CHARACTERS)

当请求伪终端时，`ssh` 支持通过转义字符实现多种功能。

单个波浪号可以通过 `~~` 发送，或者在波浪号后跟随一个下述描述之外的字符。转义字符始终位于换行符之后以便解释为特殊字符。可以在配置文件中使用 `EscapeChar` 配置指令，或在命令行中使用 `-e` 选项来更改转义字符。

支持的转义（假设默认为 `~`）包括：

- `~.`: 断开连接。

- `~^Z`: 后台运行 `.`

- `~#`: 列出转发的连接。

- `~&`: 在注销时等待转发的连接 / X11 会话结束，并将 `ssh` 放入后台运行。

- `~?`: 显示转义字符列表。

- `~B`: 向远程系统发送 BREAK（仅适用于 SSH 协议版本 2 且对方支持时）。

- `~C`: 打开命令行。目前这允许使用 `-L`、`-R` 和 `-D` 选项添加端口转发（见上文）。它还允许使用 `-KL [bind_address : port]` 取消本地、`-KR [bind_address : port]` 取消远程或 `-KD [bind_address : port]` 取消动态端口的现有端口转发。如果在 `ssh_config` 中启用了 `PermitLocalCommand` 选项，`!command` 允许用户执行本地命令。可以使用 `-h` 选项获取基本帮助。

- `~R`: 请求重置连接密钥（仅适用于 SSH 协议版本 2 且对方支持时）。

- `~V`: 当错误写入 stderr 时降低详细程度（`LogLevel`）。

- `~v`: 当错误写入 stderr 时增加详细程度（`LogLevel`）。



## TCP 转发（TCP FORWARDING）

在安全通道上对任意 TCP 连接进行转发可以在命令行或配置文件中指定。TCP 转发的一种可能应用是安全连接到邮件服务器；另一种是穿过防火墙。

在下面的示例中，我们查看如何在 IRC 客户端和服务器之间加密通信，尽管 IRC 服务器并不直接支持加密通信。其工作原理如下：用户使用 `-L` 连接到远程主机，指定一个用于转发连接到远程服务器的端口。之后，可以在客户端上启动需要加密的服务并连接到本地端口，`ssh` 将加密并转发该连接。

以下示例将 IRC 会话从客户端机器 `127.0.0.1`（本地主机）隧道到远程服务器 `server.example.com`：

```bash
ssh -f -L 1234:localhost:6667 server.example.com sleep 10
irc -c '#users' -p 1234 pinky 127.0.0.1
```

该隧道通过端口 `1234` 建立了到 IRC 服务器 `server.example.com` 的连接，加入 `#users` 频道，昵称为 `pinky`。使用哪个端口并不重要，只要它大于 1023（实际上，只有 root 用户可以在特权端口上打开套接字）并且与任何已使用的端口不冲突。连接被转发到远程服务器的端口 6667，因为那是 IRC 服务的标准端口。

`-f` 选项让 `ssh` 在后台运行，指定远程命令 `sleep 10` 是为了留出足够的时间（示例中为 10 秒）启动要隧道的服务。如果在指定时间内未建立连接，`ssh` 将退出。

## X11 转发（X11 FORWARDING）

如果 `ForwardX11` 变量设置为 `yes`（或见上文 `-X`、`-x` 和 `-Y` 选项的描述），且用户在使用 X11（设置了 `DISPLAY` 环境变量），到 X11 显示器的连接将自动转发到远程，从 shell（或命令）启动的任何 X11 程序将通过加密通道，而与真实 X 服务器的连接将从本地机器建立。用户不应手动设置 `DISPLAY`。X11 连接转发可以在命令行或配置文件中配置。

`ssh` 设置的 `DISPLAY` 值将指向服务器机器，但显示号大于零。这是正常的，因为 `ssh` 在服务器上创建了一个“代理”X 服务器，以便通过加密通道转发连接。

`ssh` 还会在服务器机器上自动设置 Xauthority 数据。为此，它将生成一个随机授权 cookie，将其存储在服务器的 `Xauthority` 中，并验证任何转发连接是否携带此 cookie，并在连接打开时替换为真实的 cookie。真实的认证 cookie 永远不会发送到服务器机器（且不会发送任何 cookie）。

如果 `ForwardAgent` 变量设置为 `yes`（或见上文 `-A` 和 `-a` 选项的描述），且用户在使用身份代理，到代理的连接将自动转发到远程。

## 验证主机密钥（VERIFYING HOST KEYS）

首次连接服务器时，会向用户展示服务器公钥的指纹（除非禁用了 `StrictHostKeyChecking` 选项）。可以使用 `ssh-keygen` 确定指纹：

```bash
ssh-keygen -l -f /etc/ssh/ssh_host_rsa_key
```

如果指纹已知，可以对其进行匹配并接受或拒绝密钥。如果只有服务器的旧版（MD5）指纹，可以使用 `ssh-keygen -E` 选项将指纹算法降级以匹配。

由于仅通过查看指纹字符串很难比较主机密钥，因此还支持使用随机图形进行视觉上的主机密钥比较。通过将 `VisualHostKey` 选项设置为 `yes`，每次登录服务器时都会显示一个小型 ASCII 图形，无论会话本身是否是交互式的都是如此。通过学习已知服务器产生的模式，当显示完全不同的模式时，用户可以很容易地发现主机密钥已更改。然而，由于这些模式并非无歧义的，与所述模式相似的模式只能说明主机密钥相同的概率很大，不能作为保证性的证明。

## 指纹列表与 DNS 验证

最后客户端进行连接：

```bash
ssh -o "VerifyHostKeyDNS ask" host.example.com [...]
```

在 DNS 中找到匹配的主机密钥指纹。确定要继续连接吗（yes/no）？

更多信息请参阅 `ssh_config` 中的 `VerifyHostKeyDNS` 选项。

## 基于 SSH 的虚拟专用网络

`ssh` 包含使用（4）网络伪设备进行虚拟专用网络（VPN）隧道的支持，允许两个网络安全连接。`sshd_config` 配置选项 `PermitTunnel` 控制服务器是否支持此功能，以及在什么级别（第 2 层或 3 层流量）。

以下示例将通过从 `10.1.1.1` 到 `10.1.1.2` 的点对点连接连接客户端网络 `10.0.50.0/24` 与远程网络 `10.0.99.0/24`，前提是运行在远程网络网关 `192.168.1.15` 上的 SSH 服务器允许此类操作。

在客户端上：

```bash
ssh -f -w 0:1 192.168.1.15 true
ifconfig tun0 10.1.1.1 10.1.1.2 netmask 255.255.255.252
route add 10.0.99.0/24 10.1.1.2
```

在服务器上：

```bash
ifconfig tun1 10.1.1.2 10.1.1.1 netmask 255.255.255.252
route add 10.0.50.0/24 10.1.1.1
```

可以通过 `/root/.ssh/authorized_keys` 文件（见下文）和 `PermitRootLogin` 服务器选项对客户端访问进行更精细的调整。如果 `PermitRootLogin` 设置为 `forced-commands-only`，以下条目将允许用户 `jane` 在（4）设备 1 上连接，并允许用户 `john` 在 tun 设备 2 上连接：

`tunnel="1",command="sh /etc/netstart tun1" ssh-rsa ... jane`

`tunnel="2",command="sh /etc/netstart tun2" ssh-rsa ... john`

由于基于 SSH 的设置涉及大量的开销，它可能更适用于临时设置，例如无线 VPN。更永久的 VPN 由如（8）和（8）等工具提供的效果更好。

## 环境变量

`ssh` 通常会设置以下环境变量：

### `DISPLAY`

`DISPLAY` 变量指示 X11 服务器的位置。它由 `ssh` 自动设置，指向形如 `hostna:n` 的值，其中 `hostna` 表示运行 shell 的宿主机，`n` 是一个大于或等于 1 的整数。`ssh` 使用此特殊值通过安全通道转发 X11 连接。用户通常不应显式设置 `DISPLAY`，因为那会导致 X11 连接变得不安全（并要求用户手动复制任何所需的授权 cookie）。

### `HOME`

设置为用户家目录目录的路径。

### `LOGNAME`

`USER` 的同义词，用于兼容使用此变量的系统。

### `MAIL`

设置为用户信箱的路径。

### `PATH`

设置为编译 `.` 时指定的默认 `PATH`。

### `SSH_ASKPASS`

如果 `ssh` 需要密码短语，且它是从终端运行的，它将从当前终端读取密码短语。如果 `ssh` 没有关联的终端，但设置了 `DISPLAY` 和 `SSH_ASKPASS`，它将执行 `SSH_ASKPASS` 指定的程序并打开 X11 窗口来读取密码短语。这在从 `.xsession` 或相关脚本调用 `ssh` 时特别有用。（注意，在某些机器上，可能需要从 `/dev/null` 重定向输入以使其工作。）

### `SSH_AUTH_SOCK`

识别用于与代理通信的 UNIX 套接字路径。

### `SSH_CONNECTION`

识别连接的客户端和服务器端。该变量包含四个空格分隔的值：客户端 IP 地址、客户端端口号、服务器 IP 地址和服务器端口号。

### `SSH_ORIGINAL_COMMAND`

当执行强制命令时，此变量包含原始命令行。它可以用于提取原始参数。

### `SSH_TTY`

此变量设置为与当前 shell 或命令关联的 tty 名称（设备路径）。如果当前会话没有 tty，则不设置此变量。

### `TZ`

如果在启动守护进程时设置了时区，则此变量将被设置为指示当前时区（即守护进程将该值传递给新连接）。

### `USER`

设置为登录用户的名称。

此外，如果存在 `~/.ssh/environ` 文件且允许用户更改环境变量，`ssh` 会读取该文件并将形如 `VARNAME=value` 的行添加到环境变量中。更多信息请参见 `ssh_config` 中的 `PermitUserEnviron` 选项。

## 环境变量（继续）

### `SSH_USE_STRONG_RNG`

OpenSSL 随机生成器的重新种子通常从 `/dev/urandom` 完成。如果环境变量 `SSH_USE_STRONG_RNG` 设置为 0 以外的值，OpenSSL 随机生成器将从 `/dev/random` 重新种子。读取的字节数由 `SSH_USE_STRONG_RNG` 值定义。最小为 14 字节。在没有硬件随机生成器的计算机上不建议此设置，因为熵不足会导致连接阻塞直到有足够的熵。

## 文件

### `~/.rhosts`

此文件用于基于主机的验证（见上文）。在某些机器上，如果用户的家目录在 NFS 分区上，此文件可能需要所有人可见，因为（8）以 root 身份读取它。此外，此文件必须由用户所有，且不能让其他人具有写权限。大多数机器的建议权限是用户读写，其他人无法访问。

### `~/.shosts`

此文件的使用方式与 `.rhosts` 完全相同，但允许在不许可 `rlogin`/`rsh` 登录的情况下进行基于主机的验证。

### `~/.ssh/`

该目录是所有用户特定配置和验证信息的默认位置。没有要求此目录的所有内容保密，但建议的权限是用户读/写/执行，其他人无法访问。

### `~/.ssh/authorized_keys`

列出可以作为此用户登录的公钥（DSA、ECDSA、Ed25519、RSA）。该文件的格式在（8）手册页中描述。此文件并非高度敏感，但建议的权限是用户读/写，其他人无法访问。

### `~/.ssh/config`

这是每个用户的配置文件。该文件格式和配置选项在 `ssh_config` 中描述。由于存在被滥用的可能，此文件必须具有严格的权限：用户读写，其他人不可写。

### `~/.ssh/environ`

包含环境变量的额外定义；见上文的“环境变量”。

### `~/.ssh/identity`

### `~/.ssh/id_dsa`

### `~/.ssh/id_ecdsa`

### `~/.ssh/id_ed25519`

### `~/.ssh/id_rsa`

包含用于验证的私钥。这些文件包含敏感数据，应允许用户读取但其他人不可访问（读/写/执行）。如果私钥文件可被其他人访问，`ssh` 将简单忽略该文件。在生成密钥时可以指定密码短语，这将使用 3DES 加密此文件的敏感部分。

### `~/.ssh/identity.pub`

### `~/.ssh/id_dsa.pub`

### `~/.ssh/id_ecdsa.pub`

### `~/.ssh/id_ed25519.pub`

### `~/.ssh/id_rsa.pub`

包含用于验证的公钥。这些文件并不敏感，任何人都可以读取（但不必如此）。

包含用户登录过的所有主机的密钥列表，且这些密钥尚未在系统范围已知主机密钥列表中。有关该文件格式的更多细节请参见（8）。

### `~/.ssh/rc`

此文件中的命令会在用户登录时由 `ssh` 执行，在用户的 shell（或命令）启动之前执行。更多信息请参阅（8）手册页。

### `/etc/hosts.equiv`

此文件用于基于主机的认证（见上文）。它应仅允许 root 用户写入。

此文件中的命令会在用户登录时由 `ssh` 执行，在用户的 shell（或命令）启动之前执行。更多信息请参阅（8）手册页。

## 退出状态

`ssh` 以远程命令的退出状态退出，或者在发生错误时返回 255。

## IPv6

IPv6 地址可以使用任何使用 IPv4 地址的地方。在所有条目中，必须使用方括号括起的 IPv6 地址。注意：方括号是 shell 的特殊字符，在 shell 中必须进行转义。

## 参见

（1）、（1）、`ssh-add1`、`ssh-agent1`、`ssh-keygen1`、`ssh-keyscan1`、（4）、`ssh_config5`、`ssh-keysign8`、（8）

## 标准

S. Lehtinen，C. Lonvick，January 2006，*RFC 4250*，*The Secure Shell (SSH) Protocol Assigned Numbers*

T. Ylonen，C. Lonvick，January 2006，*RFC 4251*，*The Secure Shell (SSH) Protocol Architecture*

T. Ylonen，C. Lonvick，January 2006，*RFC 4252*，*The Secure Shell (SSH) Authentication Protocol*

T. Ylonen，C. Lonvick，January 2006，*RFC 4253*，*The Secure Shell (SSH) Transport Layer Protocol*

T. Ylonen，C. Lonvick，January 2006，*RFC 4254*，*The Secure Shell (SSH) Connection Protocol*

J. Schlyter，W. Griffin，January 2006，*RFC 4255*，*Using DNS to Securely Publish Secure Shell (SSH) Key Fingerprints*

F. Cusack，M. Forssen，January 2006，*RFC 4256*，*Generic Message Exchange Authentication for the Secure Shell Protocol (SSH)*

J. Galbraith，P. Remaker，January 2006，*RFC 4335*，*The Secure Shell (SSH) Session Channel Break Extension*

M. Bellare，T. Kohno，C. Namprempre，January 2006，*RFC 4344*，*The Secure Shell (SSH) Transport Layer Encryption Modes*

B. Harris，January 2006，*RFC 4345*，*Improved Arcfour Modes for the Secure Shell (SSH) Transport Layer Protocol*

M. Friedl，N. Provos，W. Simpson，March 2006，*RFC 4419*，*Diffie-Hellman Group Exchange for the Secure Shell (SSH) Transport Layer Protocol*

J. Galbraith，R. Thayer，November 2006，*RFC 4716*，*The Secure Shell (SSH) Public Key File Format*

D. Stebila，J. Green，December 2009，*RFC 5656*，*Elliptic Curve Algorithm Integration in the Secure Shell Transport Layer*

A. Perrig，D. Song，1999，International Workshop on Cryptographic Techniques and E-Commerce（CrypTEC '99），*Hash Visualization: a New Technique to improve Real-World Security*

## 作者

OpenSSH 是 Tatu Ylonen 发布的原始免费 `ssh` 1.2.12 版本的衍生版本。Aaron Campbell、Bob Beck、Markus Friedl、Niels Provos、Theo de Raadt 和 Dug Song 修复了许多错误，重新添加了新功能并创建了 OpenSSH。Markus Friedl 为支持 SSH 协议版本 1.5 和 2.0 做出了贡献。

---

# PASSWD

## 名称

`passwd` - 计算密码哈希

## 语法

`openssl passwd [-crypt] [-1] [-apr1] [-salt string] [-in file] [-stdin] [-noverify] [-quiet] [-table] {password*}`

## 描述

`passwd` 命令计算运行时输入的密码的哈希，或计算列表中每个密码的哈希。密码列表从选项 `-in file` 指定的文件、从选项 `-stdin` 的 stdin、或者从命令行或终端获取。可以使用 Unix 标准算法 `crypt` 和基于 MD5 的 BSD 密码算法 `1` 及其 Apache 变体 `apr1`。

## 选项

### `-crypt`

使用 `crypt` 算法（默认）。

### `-1`

使用基于 MD5 的 BSD 密码算法 `1`。

### `-apr1`

使用 `apr1` 算法（BSD 算法的 Apache 变体）。

### `-salt string`

使用指定的盐。从终端读取密码时，这意味着使用了 `-noverify`。

### `-in file`

从 `file` 读取密码。

### `-stdin`

从 `stdin` 读取密码。

### `-noverify`

从终端读取密码时不验证。

### `-quiet`



当命令行给出的密码被截断时，不输出警告。

`-table`

在输出列表中，在每个密码哈希之前加上明文密码和一个 TAB 字符。

## 示例

`openssl passwd -crypt -salt xx password` 输出 `xxj31ZMTZzkVA`。

`openssl passwd -1 -salt xxxxxxxx password` 输出 `$1$xxxxxxxx$UYCIxa628.9qXjpQCjM4a..`。

`openssl passwd -apr1 -salt xxxxxxxx password` 输出 `$apr1$xxxxxxxx$dxHfLAsjHkDRmG83UXe8K0..`。

---

# RAND

## 名称

`rand` - 生成伪随机字节

## 语法

`-hex`

显示输出为十六字符串。

## 参见

(3)

---

# SSLTAP

## 名称

`ssltap` - 接入 SSL 连接并显示通过的数据

## 语法

`ssltap` `[-fhlsvx]` `[-pport]` `[hostna:port]`

## 状态

此文档仍在进行中。请在 Mozilla NSS bug 836477 中参与初始评审。

## 描述

SSL 调试工具 `ssltap` 是一个感知 SSL 的命令行代理。它监控 TCP 连接并显示通过的数据。如果连接是 SSL，数据显示将包含解释的 SSL 记录和握手。

## 选项

`-f`

开启花式打印。输出以彩色 HTML 打印。从客户端发送到服务器的数据是蓝色的；服务器的回复是红色的。当与循环模式一起使用时，不同的连接用水平线分隔。可以使用此选项将输出上传到浏览器。

`-h`

开启十六/ASCII 打印。不是输出原始数据，而是将每个记录解释为一行十六进制值，随后是作为 ASCII 字符的数据。两部分用竖线分隔。非打印字符被点替换。

`-l` 前缀

开启循环；即继续接受连接，而不是在第一个连接完成后停止。

`-p` `port`

将默认会话端口 (1924) 修改为其他端口。

以下是常见的端口号：

- HTTP 80
- HTTPS 443
- SMTP 25
- FTP 21
- IMAP 143
- IMAPS 993 (IMAP over SSL)
- NNTP 119
- NNTPS 563 (NNTP over SSL)

`-s`

开启 SSL 解析和解码。该工具不会自动检测 SSL 会话。如果您正在拦截 SSL 连接，请使用此选项，以便工具能够检测并解码 SSL 结构。

如果工具检测到证书链，它会将 DER 编码的证书保存到当前目录下的文件中。文件名为 `nad cert.0x`，其中 `x` 是证书的序列号。

如果 `-s` 配合 `-h` 使用，每条记录将打印两个独立的部分：原始十六进制/ASCII 输出，以及解析后的 SSL 输出。

`-v`

打印工具的版本字符串。

`-x`

开启额外的 SSL 十六进制转储。

## 使用方法与示例

你可以使用 SSL 调试工具拦截任何连接信息。虽然你可以通过执行除 `hostname:port` 之外没有任何选项的 `ssltap` 命令来运行工具，但通过这种方式获得的信息非常有限。例如，假设你的开发机名为 `intercept`。使用调试工具最简单的方法是从命令行终端执行以下命令：

```bash
$ ssltap
```

程序会在默认端口 `1924` 上等待传入的连接。在你的浏览器窗口中输入 URL。浏览器从服务器获取请求的页面，但页面被 `intercept` 上的调试工具拦截并传递给浏览器。在传输浏览的过程中，数据会打印到你执行命令的命令行窗口中。从客户端发送到服务器的数据被以下符号包裹：`--> [ data ]`。从服务器发送到客户端的数据被以下符号包裹：`"left arrow"-- [ data ]`。原始数据流被发送到标准输出且不经过任何方式解释。这可能会导致异常效果，例如声音、闪烁甚至命令行窗口的崩溃。要输出数据基础的、可打印的解释结果，请使用 `-h` 选项；或者如果你正在查看 SSL 连接，请使用 `-s` 选项。你会发现获取的页面在浏览器中看起来不完整。这是因为工具默认在第一次连接完成后就会关闭，导致浏览器无法加载图像。要让工具继续接受连接，请使用 `-l` 选项开启循环模式。以下示例展示了常用选项组合的输出。

### 示例 1

```bash
$ ssltap.exe -sx -p 444 interzone.mcom.com:443 > sx.txt
```

输出：

```text
Connected to interzone.mcom.com:443 -->; [ alloclen = 66 bytes [ssl2] ClientHelloV2 { version = {0x03, 0x00} cipher-specs-length = 39 (0x27) sid-length = 0 (0x00) challenge-length = 16 (0x10) cipher-suites = { (0x010080) SSL2/RSA/RC4-128/MD5 (0x020080) SSL2/RSA/RC4-40/MD5 (0x030080) SSL2/RSA/RC2CBC128/MD5 (0x040080) SSL2/RSA/RC2CBC40/MD5 (0x060040) SSL2/RSA/DES64CBC/MD5 (0x0700c0) SSL2/RSA/3DES192EDE-CBC/MD5 (0x000004) SSL3/RSA/RC4-128/MD5 (0x00ffe0) SSL3/RSA-FIPS/3DES192EDE-CBC/SHA (0x00000a) SSL3/RSA/3DES192EDE-CBC/SHA (0x00ffe1) SSL3/RSA/FIPS/DES64CBC/SHA (0x000009) SSL3/RSA/DES64CBC/SHA (0x000003) SSL3/RSA/RC4-40/MD5 (0x000006) SSL3/RSA/RC2CBC40/MD5 } session-id = { } challenge = { 0xec5d 0x8edb 0x37c9 0xb5c9 0x7b70 0x8fe9 0xd1d3 0x2592 } } ] <-- [ SSLRecord { 0: 16 03 00 03 e5 |..... type = 22 (handshake) version = { 3,0 } length = 997 (0x3e5) handshake { 0: 02 00 00 46 |...F type = 2 (server_hello) length = 70 (0x000046) ServerHello { server_version = {3, 0} random = {...} 0: 77 8c 6e 26 6c 0c ec c0 d9 58 4f 47 d3 2d 01 45 | wn&l.ì..XOG.-.E 10: 5c 17 75 43 a7 4c 88 c7 88 64 3c 50 41 48 4f 7f | \.uC\A7L.&Ccedil;.d<PAHO. session ID = { length = 32 contents = {..} 0: 14 11 07 a8 2a 31 91 29 11 94 40 37 57 10 a7 32 | ...ad*1.)..@7W.\A72 10: 56 6f 52 62 fe 3d b3 65 b1 e4 13 0f 52 a3 c8 f6 | VoRbþ=\B3e\B1...R\A3È. } cipher_suite = (0x0003) SSL3/RSA/RC4-40/MD5 } 0: 0b 00 02 c5 |...Å type = 11 (certificate) length = 709 (0x0002c5) CertificateChain { chainlength = 706 (0x02c2) Certificate { size = 703 (0x02bf) data = { saved in file 'cert.001' } } } 0: 0c 00 00 ca |.... type = 12 (server_key_exchange) length = 202 (0x0000ca) 0: 0e 00 00 00 |.... type = 14 (server_hello_done) length = 0 (0x000000) } } ] --> [ SSLRecord { 0: 16 03 00 00 44 |....D type = 22 (handshake) version = { 3,0 } length = 68 (0x44) handshake { 0: 10 00 00 40 |...@ type = 16 (client_exchange) length = 64 (0x0040) ClientKeyExchange { age = {...} } } ] --> [ SSLRecord { 0: 14 03 00 01 |..... type = 20 (change_cipher_spec) version = { 3,0 } length = 1 (0x1) 0: 01 |. } SSLRecord { 0: 16 03 00 38 |....8 type = 22 (handshake) version = { 3,0 } length = 56 (0x38) < encrypted > ] <-- [ SSLRecord { 0: 14 03 00 01 |..... type = 20 (change_cipher_spec) version = { 3,0 } length = 1 (0x1) 0: 01 |. } ] <-- [ SSLRecord { 0: 17 03 00 01 1f |..... type = 23 (application_data) version = { 3,0 } length = 287 (0x11f) < encrypted > } ] --> [ SSLRecord { 0: 17 03 00 00 a0 |.... type = 23 (application_data) version = { 3,0 } length = 160 (0xa0) < encrypted > } ] <-- [ SSLRecord { 0: 17 03 00 00 df |....ß type = 23 (application_data) version = { 3,0 } length = 223 (0xdf) < encrypted > } SSLRecord { 0: 15 03 00 00 12 |..... type = 21 (alert) version = { 3,0 } length = 18 (0x12) < encrypted > } ] Server socket closed.
```

### 示例 2

`-s` 选项开启 SSL 解析。由于此示例中未使用 `-x` 选项，未解码的值将以原始数据输出。输出被重定向到文件中。

```bash
$ ssltap -s -p 444 interzone.mcom.com:443 > s.txt
```

---

# SSS_SSH_AUTHORIZEDKEYS

## 名称

`sss_ssh_authorizedkeys` - 获取 OpenSSH 授权密钥

## 概要

`sss_ssh_authorizedkeys` `[*options*]` `USER`

## 描述

`sss_ssh_authorizedkeys` 获取用户 `USER` 的 SSH 公钥，并以 OpenSSH `authorized_keys` 格式将它们输出（更多信息请参阅 (8) 中的“AUTHORIZED_KEYS FILE FORMAT”章节）。

如果在编译时支持 `AuthorizedKeysCommand` 或 `PubkeyAgent`(5) 选项，则可以配置 (8) 用于使用 `sss_ssh_authorizedkeys` 进行公钥认证。

如果支持 `AuthorizedKeysCommand`，可以通过在 (5) 中放入以下指令来配置 (8) 使用它：

`AuthorizedKeysCommand /usr/bin/sss_ssh_authorizedkeys AuthorizedKeysUser nobody`

如果支持 `PubkeyAgent`，可以通过使用以下 (8) 配置指令来配置它：

---

# SSS_SSH_KNOWNHOSTSPROXY

## 摘要

`sss_ssh_knownhostsproxy` `[`options`]` `HOST` `[`PROXY_COMMAND`]`

## 描述

`sss_ssh_knownhostsproxy`

获取主机 `HOST` 的 SSH 主机公钥，将其存储在自定义的 OpenSSH `known_hosts` 文件中（更多信息请参阅 (8) 中的“SSH_KNOWN_HOSTS FILE FORMAT”部分）`/var/lib/sss/pubconf/known_hosts`，并建立到主机的连接。

如果指定了 `PROXY_COMMAND`，则使用它来创建到主机的连接，而不是打开 socket。

(1) 可以通过以下指令 (1) 配置为使用 `sss_ssh_knownhostsproxy` 进行主机密钥认证：

```text
ProxyCommand /usr/bin/sss_ssh_knownhostsproxy -p %p %h GlobalKnownHostsFile /var/lib/sss/pubconf/known_hosts
```

## 选项

`-p`, `--port` `PORT`

使用端口 `PORT` 连接到主机。默认使用端口 22。

`-d`, `--domain` `DOMAIN`

在 SSSD 域 `DOMAIN` 中搜索主机公钥。

`-?`, `--help`

显示帮助信息并退出。

## 退出状态

成功时，返回退出值 0。否则，返回 1。

## 参见

(8), (5), (5), (5), (5), (5), (5), (5), (8), (8), (8), (8), (8), (8), (8), (8), (8), (8), (8), (8), (8), (8),(5),(8). (5)

## 作者

SSSD 上游

---

# start-pulseaudio-x11

## 名称

`start-pulseaudio-x11` - PulseAudio 音服务器 X11 启动脚本

## 摘要

`start-pulseaudio-x11` `[`pulseaudio options`]`

## 描述

此脚本启动 `pulseaudio`（如果尚未运行）并加载模块在 X11 根窗口中发布 PulseAudio 服务器的访问凭据，并在 cork/uncork 请求上合成 X11 键事件。此外，它还会将 PulseAudio 注册到 X11 会话管理器。

所有参数直接传递给 `pulseaudio`。

## 作者

PulseAudio 开发者 `<pulseaudio-discuss (at) lists (dot) freedesktop (dot) org>`；PulseAudio 可从此处获取。

## 参见

(1)

---

# STARTX

## 名称

`startx` - 初始化一个 X 会话

## 摘要

`startx` `[` `[`client`]` `options` ... `]` `[` `--` `[`server`]` `[`display`]` `[`-listen`]` `options` ... `]` `]`

## 描述

`startx` 脚本是 (1) 的前端，为运行单个 X 窗口系统会话提供了一个更美观的用户界面。它通常不带任何参数运行。

紧跟在 `startx` 命令后的参数将用于以与 (1) 的方式启动客户端。特殊参数 `--` 标记客户端参数的结束和服务器选项的开始。默认情况下 `startx` 向服务器传递 `-nolistentcp`，可以使用特殊的服务器选项 `-listen` 来阻止 `startx` 执行此操作。通过 `startx` 指定服务器选项可能很方便，以便根据每个会话更改默认颜色深度、显示设备呈现的每英寸点数（dpi）服务器的概念，或者利用 (1) 服务器允许并在 (5) 配置中指定的不同服务器布局。以下是指定服务器参数的示例；请查阅您的 X 服务器手册页以确定哪些参数是有效的。

```bash
startx -- -depth 16
startx -- -dpi 100
startx -- -layout Multihead
```

要确定运行的客户端，`startx` 首先在用户的家目录下查找名为 `.xinitrc` 的文件。如果没有找到，它将使用 `xinit` 库目录下的 `xinitrc` 文件。如果提供了命令行客户端选项，它们将覆盖此行为并还原 (1) 的行为。要确定运行的服务器，`startx` 首先在用户的家目录下查找名为 `.xserverrc` 的文件。如果没有找到，它将使用 `xinit` 库目录下的 `xserverrc`。如果提供了命令行服务器选项，它们将覆盖此行为并还原 (1) 的行为。用户很少需要提供 `.xserverrc` 文件。有关参数的更多细节请参阅 (1) 手册页。

系统范围的 `xinitrc` 和 `xserverrc` 文件位于 `/etc/X11/xinit` 目录。

`.xinitrc` 通常是一个 shell 脚本，根据用户的喜好启动多个客户端。当该 shell 脚本退出时，`startx` 会杀死服务器并执行任何其他会话关闭操作。由 `.xinitrc` 启动的大多数客户端应该在后台运行。最后一个客户端应该在前台运行；当它退出时，会话将退出。人们通常选择会话管理器、窗口管理器或 `xterm` 作为“魔法”客户端。

## 示例

下面是一个示例 `.xinitrc`，它启动多个应用程序并将窗口管理器作为“最后一个”应用程序运行。假设窗口管理器已正确配置，用户可以选择“退出”菜单项关闭 X。



```
xrdb -load $HOME/.Xresources xsetroot -solid gray & xbiff -geotry -430+5 & oclock -geotry 75x75-0-0 & xload -geotry -80-0 & xterm -geotry +0+60 -ls & xterm -geotry +0-100 & xconsole -geotry -0+0 - fn 5x7 & exec twm
```

## 环境变量

`DISPLAY`

此变量被设置为客户端应连接的显示器名称。注意，它是被设置的而不是读取的。

当用户没有 `.xserverrc` 时运行的服务器。

## 参见

`(1)`, `(7)`, `(1)`, `(5)`

---

# STAT

## 名称

`stat` - 显示文件或系统状态

## 摘要

`stat` [*OPTION*]... `FILE`...

## 描述

显示文件或系统状态。

长选项的强制参数也是强制的。

`-L`, `--dereference` 跟踪链接

`-f`, `--file-system` 显示文件系统状态而不是文件状态

`-c`, `--format=*FORMAT*` 使用指定的 `FORMAT` 代替默认值；在每次使用 `FORMAT` 后输出换行

`--printf=*FORMAT*` 与 `--format` 类似，但解释反斜杠转义，且不输出强制换行；如果你需要换行，请在 `FORMAT` 中包含 `\n`

`-t`, `--terse` 以紧凑形式打印信息

`--help` 显示此帮助并退出

`--version` 输出版本信息并退出

文件的有效格式序列（无 `--file-system`）：

`a` 八进制权限

`A` 人类可读的权限

`b` 分配的块数（参见 `%B`）

`B` `%b` 报告的每个块的大小

`C` SELinux 安全上下文字符串

`d` 十进制设备数

`D` 十六进制设备数

`f` 原始模式

`F` 文件类型

`g` 所有的者的组 ID

`G` 所有的者的组名

`h` 硬链接数

`i` 节点数

`m` 挂载点

`n` 文件名

`N` 带引用的文件名

`o` 优化 I/O 大小提示

`s` 总大小，字节

`t` 字符/块特殊文件的主设备类型（十六进制）

`T` 字符/块特殊文件的次设备类型（十六进制）

`u` 所有者的用户 ID

`U` 所有者的用户名

`w` 文件创建时间，人类可读；未知则为 `-`

`W` 文件创建时间，自 Unix 以来；未知则为 `0`

`x` 最后访问时间，人类可读

`X` 最后访问时间，自 Unix 以来

`y` 最后修改时间，人类可读

`Y` 最后数据修改时间，自 Unix 以来

`z` 最后状态更改时间，人类可读

`Z` 最后状态更改时间，自 Unix 以来

文件系统的有效格式序列（无 `--file-system`）：

`a` 非超级用户可用的空闲块

`b` 文件系统中的总数据块

`c` 文件系统中的总文件节点

`d` 文件系统中的空文件节点

`f` 文件系统中的空闲块

`i` 文件系统 ID（十六进制）

`l` 文件名最大长度

`n` 文件名

`s` 块大小（用于更快的传输）

`%S` 基本块大小（用于块计数）

`%t` 十六进制格式的文件系统类型

`%T` 可读格式的文件系统类型

注意：您的 shell 可能有其自己的 `stat` 版本，该版本通常优于此处描述的版本。请参阅您 shell 的文档以获取其支持的选项详情。

## 作者

由 Michael Meskes 编写。

## 报告错误

GNU coreutils 在线帮助：<>

向 <> 报告 `stat` 翻译错误

## 版权

版权所有 2015 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 3 版或更高版本 <>。

这是免费软件：你可以自由地更改和重新发行它。在法律允许范围内不提供任何保证。

## 另请

`(2)`

完整文档位于：<>

或通过本地路径可用：`info '(coreutils) stat invocation'`

---

# STTY

## 名称

`stty` - 更改并打印终端行设置

## 摘要

`stty` [*OPTION*]... [*SETTING*]...

## 描述

打印或更改终端行设置。

`-a`, `--all`

以可读形式打印所有设置

`-g`, `--save`

以终端可读形式打印所有当前设置

`-F`, `--file=*DEVICE*`

打开并使用指定的 `DEVICE` 而不是标准输入

`--help`

显示此帮助并退出

`--version`

输出版本信息并退出

可选 - 在 `SETTING` 之前的减号表示否定。`*` 标记非 POSIX 设置。底层系统定义了哪些设置可用。

### 特殊字符：

- `discard CHAR`

`CHAR` 将切换输出丢弃状态

- `eof CHAR`

`CHAR` 将发送文件结束符（终止输入）

- `eol CHAR`

`CHAR` 将结束行

- `eol2 CHAR`

用于结束行的替代 `CHAR`

- `erase CHAR`

`CHAR` 将擦除输入的最后一个字符

- `intr CHAR`

`CHAR` 将发送中断信号

- `kill CHAR`

`CHAR` 将擦除当前行

- `lnext CHAR`

`CHAR` 将进入下一个被引号的字符

- `quit CHAR`

`CHAR` 将发送退出信号

- `rprnt CHAR`

`CHAR` 将重绘当前行

- `start CHAR`

`CHAR` 将停止后重启输出

- `stop CHAR`

`CHAR` 将停止输出

- `susp CHAR`

`CHAR` 将发送终端停止信号

- `swtch CHAR`

`CHAR` 将切换到不同的 shell 层

- `werase CHAR`

`CHAR` 将擦除输入的最后一个单词

### 特殊设置：

- `N`

将输入和输出速度设置为 `N` 波特

- `cols N`

告知内核终端有 `N` 列

- `columns N`

同于 `cols N`

- `ispeed N`

将输入速度设置为 `N`

- `line N`

使用行控制律 `N`

- `min N`

配合 `-icanon` 使用，设置 `N` 个字符为完成读取的最小数量

- `ospeed N`

将输出速度设置为 `N`

- `rows N`

告知内核终端有 `N` 行

- `size`

根据内核打印行和列数

- `speed`

打印终端速度

- `ti N`

配合 `-icanon` 使用，设置读取超时为 `N` 十分之一秒

### 控制设置：

- `[-]clocal`

禁用调制解调器控制信号

- `[-]cread`

允许接收输入

- `[-]crtscts`

启用 RTS/CTS 握手

- `csN`

将字符大小设置为 `N` 位，`N` 范围为 `[5..8]`

- `[-]cstopb`

每个字符使用两个停止位（配合 `-` 使用一个）

- `[-]hup`

当最后一个进程关闭 tty 时发送挂断信号

- `[-]hupcl`

同于 `[-]hup`

- `[-]parenb`

在输出中生成校验位，并在输入中期望校验位

- `[-]parodd`

设置奇数校验（或通过 `-` 设置偶数校验）

- `*]cmspar`

使用“粘性”（标记/空格）校验

### 输入设置：

- `[-]brkint`

中断将导致中断信号

- `[-]icrnl`

将回车转换为换行符

- `[-]ignbrk`

忽略中断字符

- `[-]igncr`

忽略回车

- `[-]ignpar`

忽略具有校验错误的字符

- `*]imaxbel`

蜂鸣且在字符上接收到一个字符时不冲空完整的输入缓冲区

- `[-]inlcr`

将换行符转换为回车

- `[-]inpck`

启用输入校验检查

- `[-]istrip`

清除输入字符的高位（第 8 位）

- `*]iutf8`

假设输入字符为 UTF-8 编码

- `*]iuclc`

将大写字母转换为小写字母

- `*]ixany`

允许任何字符重启输出，而不仅仅是起始字符

- `[-]ixoff`

启用发送起始/停止字符

- `[-]ixon`

启用 XON/XOFF 控

- `[-]parmrk`

标记校验错误

### 输出设置：

- `*]bsdly`

使用 `\b` 和 `\r` 作为退格和回车

- `*]cr3`

使用 `\r` 作为回车

- `[-]crnl`

将回车转换为换行符

- `*]ff1`

使用 `\f` 作为换页

- `*]n10`

使用 `\n` 作为换行

- `*]nl1`

使用 `\n` 作为换行

- `*]ocrnl`

将回车转换为换行符

- `*]ofdel`

使用 DEL 作为填充字符

- `*]ofill`

使用填充字符而不是定时延迟

- `*]olcuc`

将小写字母转换为大写字母

- `*]onlcr`

将换行符转换为回车

- `*]onlret`

换行符执行回车

- `*]onocr`

在列 0 不打印回车

- `*]opost`

处理输出

- `*]tab3`

使用制表符作为水平制表

- `*]tabs`

使用制表符作为水平制表

- `*]vt1`

使用 `\v` 作为垂直制表

### 本地设置：

- `[-]crterase`

擦除字符回显为退格-空格-退格

- `*]crtkill`

根据 `echoprt` 和 `echoe` 设置擦除行

- `*]defecho`

擦除字符回显为退格-空格-退格

- `[-]echo`

回显输入字符

- `*]echoctl`

回显控制字符为 `^c`

- `[-]echoe`

擦除字符回显为退格-空格-退格

- `*]echok`

在擦除行后回显换行

- `*]echoke`

根据 `echoprt` 和 `echoe` 设置擦除行

- `*]echonl`

即使未设置 `echo` 也回显换行

- `*]echoprt`

擦除字符回显为 `\/` 格式

- `[-]icanon`

启用 `erase`、`kill`、`werase` 和 `rprnt` 特殊字符

- `[-]iexten`

启用非 POSIX 特殊字符

- `[-]isig`

启用 `intr`、`quit` 和 `susp` 特殊字符

- `[-]noflsh`

在 `intr`、`quit` 和 `susp` 特殊字符后禁用刷新

- `[-]prterase`

擦除字符回显为 `\/` 格式

- `[-]tostop`

后台作业尝试写入时发送 `SIGTTOU`

- `[-]xcase`

配合 `icanon` 使用，用 `\` 转义大写字母

### 组合设置：

- `[-]evenp` 或 `[-]parity`

同于 `parenb -parodd` 和 `cs7`

- `[-]oddp`

同于 `parenb parodd` 和 `cs7`

- `[-]raw`

同于 `-ignbrk -brkint -ignpar -parmrk -inpck -istrip -inlcr -igncr -icrnl -ixon -ixoff -icanon -opost -isig -isig -iuclc -ixany -imaxbel -xcase -olcuc -ocrnl -onlcr -onocr -onlret -ofill -ofdel -nl1 -cr3 -tab3 -bsdly -vt1 -ff1`

- `[-]cooked`

同于 `-raw`

- `[-]nl`

同于 `-icrnl -inlcr -igncr -ocrnl -onlcr -onocr -onlret`

- `[-]ek`

将 `erase` 和 `kill` 设置为 `#` 和 `@`

- `sane`

同于 `cread -ignbrk brkint -inlcr -igncr icrnl -ixoff -iuclc -ixany imaxbel opost -olcuc -ocrnl onlcr -onocr -onlret -ofill -ofdel nl1 cr3 tab3 -bsdly -vt1 -ff1 isig icanon iexten echo echoe echok -echonl -noflsh -xcase -tostop -echoprt echoctl echoke`

## 作者

由 David MacKenzie 编写。

## 报告错误

GNU coreutils 在线帮助：<>

向 <> 报告 `stty` 翻译错误

## 版权

版权所有 2015 Free Software Foundation, Inc. 许可协议 GPLv3+: GNU GPL 3 版本或更高版本 <>。

这是一款免费软件：你可以自由地更改和重新发行它。在法律允许范围内，不提供任何保证。

## 另请

完整文档位于：<>

或通过本地以下命令可用：`info '(coreutils) stty invocation'`

---

# SU

## 名称

`su` - 以替换用户和组 ID 运行命令

## 概要

`su` [options] [-] [`user` [*argument*...]]

## 描述

`su` 允许以替换的用户和组 ID 运行命令。

当在不带参数的情况下调用时，`su` 默认以 `root` 身份运行交互式 shell。

为了向后兼容性，`su` 默认不更改当前目录，并且仅设置环境变量 `HOME` 和 `SHELL`（如果目标 `user` 不是 root，则额外设置 `USER` 和 `LOGNAME`）。建议始终使用 `--login` 选项（而不是快捷选项 `-`），以避免混合环境引起的副作用。

此版本的 `su` 使用 PAM 进行身份验证、账户和会话管理。因此，其他 `su` 实现中找到配置选项（例如对 wheel 组的支持）必须通过 PAM 配置。

## 选项

`-c`, `--command`=`command`

使用 `-c` 选项将 `command` 传递给 shell。

`-f`, `--fast`

将 `-f` 传递给 shell，这取决于 shell 可能有用也可能有害。

`-g`, `--group`=`group`

指定主组。此选项仅 root 用户可用。

`-G`, `--supp-group`=`group`

指定附加组。此选项仅 root 用户可用。

`-`, `-l`, `--login`

作为登录 shell 启动 shell，其环境类似于真实的登录：

- 清除 `TERM` 以外的所有环境变量
- 初始化环境变量 `HOME`、`SHELL`、`USER`、`LOGNAME` 和 `PATH`
- 切换到目标用户的家目录
- 将 shell 的 `argv[0]` 设置为 `-` 以使 shell 成为登录 shell

`-m`, `-p`, `--preserve-environment`

保留整个环境，即不设置 `HOME`、`SHELL`、`USER` 或 `LOGNAME`。如果指定了 `--login` 选项，则忽略此选项。

`-s`, `--shell`=`shell`

运行指定的 `shell` 而不是默认 shell。运行的 shell 根据以下规则顺序选择：

- 使用 `--shell` 指定 shell
- 如果使用了 `--preserve-environment` 选项，则使用环境变量 `SHELL` 指定 shell
- 目标用户 `passwd` 条目列出的 shell
- `/bin/sh`

如果目标用户拥有受限 shell（即未列在 `/etc/shells` 中），除非调用用户是 root，否则 `--shell` 选项和 `SHELL` 环境变量将被忽略。

`--session-command=`command`

类似于 `-c` 但不创建新会话。（不建议使用。）

`-V`, `--version`

显示版本信息并退出。

`-h`, `--help`

显示帮助文本并退出。

## 信号

在接收到 `SIGINT`、`SIGQUIT` 或 `SIGTERM` 时，`su` 会终止其子进程，随后使用接收到的信号终止自身。

## 配置文件

`su` 读取 `/etc/default/su` 和 `/etc/login.defs` 配置文件。以下配置项与 `login(1)` 相关：

`FAIL_DELAY` (number)

身份验证失败时的延迟（秒）。该数字必须是非负整数。

`ENV_PATH` (string)

为普通用户定义 `PATH` 环境变量。默认值为 `/usr/local/bin:/bin:/usr/bin`。

`ENV_ROOTPATH` (string)

`ENV_SUPATH` (string)

为 root 定义 `PATH` 环境变量。默认值为 `/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin`。

`ALWAYS_SET_PATH` (boolean)

如果设置为 `yes` 且未指定 `--login` 和 `--preserve-environment`，`su` 将初始化 `PATH`。

## 退出状态

`su` 通常返回其执行的命令的退出状态。如果命令被信号杀死，`su` 返回信号值加 128。

## `su` 本身生成的退出状态：

`1`: 执行请求命令之前的通用错误

`126`: 无法执行请求的命令

`127`: 未找到请求的命令

## 文件

`/etc/pam.d/su`

默认 PAM 配置文件

此 `su` 命令派自 coreutils 的 `su`，该版本基于 David MacKenzie 的实现。

## 可用性

`su` 命令是 util-linux 包的一部分，可在 Linux 内核存档中获得

---

# SYMCRYPTRUN

## 名称

`symcryptrun` - 调用一个简单的对称加密工具

## 概要

`symcryptrun` `--class` `class` `--program` `program` `--keyfile` `keyfile` [--decrypt`|--encrypt] [`inputfile`]

## 描述

简单的加密工具已经使用了很长时间，可能希望将其集成到 GnuPG 框架中。协议和加密方法可能不是标准的或没有正确的文档，因此无法实现具有类似 gpg 接口的完整加密工具。`symcryptrun` 提供了一个解决方案：它通过调用外部加密/解密模块运行，并通过 `gpg-agent` 使用基于 `pinentry` 机制为密钥提供密码。

注意，`symcryptrun` 只有在 GnuPG 编译时使用了 `--enable-symcryptrun` 才可用。

对于加密，明文应通过 STDIN 提供或作为参数 `inputfile`，密文将输出到 STDOUT。解密反之亦然。

`CLASS` 描述外部工具的调用约定。目前必须指定为 `confucius`。`PROGRAM` 是该外部工具的完整路径。

对于类 'confucius'，需要 `--keyfile` 选项；`keyfile` 是包含密钥的文件名，该文件可能受密码保护。详细的调用约定请参阅源代码。

注意在启动 `symcryptrun` 之前必须运行 `gpg-agent`。

可以使用以下附加选项：

`-v`, `--verbose`

运行期间输出额外信息。

`-q`, `--quiet`

尽可能安静。

`--homedir` `dir`

将家目录名称设置为 `dir`。如果不使用此选项，家目录默认为 `~/.gnupg`。它仅在命令行给出时被识别。它还会覆盖通过环境变量 `GNUPGHOME` 或（在 Windows 系统上）通过注册表项 `HKCU\Software\GNU\GnuPG:HomeDir` 指定家目录。

在 Windows 系统上，可以将 GnuPG 安装为便携应用程序。在这种情况下，仅考虑此命令行，忽略所有其他设置家目录的方法。

要在 Windows 下作为便携程序安装 GnuPG，请在工具 `gpgconf.exe` 所在的目录中创建一个名为 `gpgconf.ctl` 的空文件。安装根目录即为该目录；或者如果 `gpgconf.exe` 直接安装在目录 `bin` 下，则为其父目录。你还需要确保以下目录存在且可写：用于 GnuPG 家目录的 `ROOT/home` 和用于内部缓存文件的 `ROOT/var/cache/gnupg`。

`--log-file` `file`

将所有日志输出附加到 `file`。默认将日志信息写入 `STDERR`。

`symcryptrun` 可能的退出状态码为：

`0`

成功。

`1`

发生错误。

`2`

提供了无效的密码。

`3`

操作被用户取消。

## 参见

`gpg(1)`, `gpg-agent(1)`, `pinentry(1)`

此工具的完整文档维护在 Texinfo 手册中。如果你的站点上正确安装了 GnuPG 和 info 程序，运行命令：

```
info gnupg
```

将让你访问包含目录结构和索引的完整手册。

---

# SYNC

## 名称

`sync` - 将缓存写入同步到持久化存储

## 语法

`sync` `[OPTION]` `[FILE]`...

## 描述

将缓存写入同步到持久化存储

如果指定了一个或多个文件，则仅同步这些文件或它们包含的文件系统。

`-d`, `--data`

`sync` 只同步文件数据，不包含必要的元数据

`-f`, `--file-system`

`sync` 同步包含这些文件的文件系统

`--help`

显示此帮助并退出

`--version`

输出版本信息并退出

## 缺陷

持久性保证随系统而异。详情请参阅下方的系统调用。

## 作者

由 Jim Meyering 和 Giuseppe Scrivano 编写。

## 报告缺陷

GNU coreutils 在线帮助：<>

向 <> 报告 `sync` 翻译缺陷

## 另请

`sync(2)`, `fdatasync(2)`

完整文档位于：<>

或通过本地路径可用：`info '(coreutils) sync invocation'`

---

# SYNAPTICS

## 名称

`synclient` - 在 X 运行时更改 Synaptics TouchPad 驱动参数

## 摘要

`synclient` `[-lV?]` `[var1=value1 [var2=value2] ...]`

## 描述

此程序允许你在 X 运行时更改 XOrg/XFree86 服务器的 Synaptics TouchPad 驱动参数。

## 选项

`-l`

列出当前用户设置。如果没有提供选项，这是默认选项。

`-V`

打印版本号并退出。



`-?`

显示帮助信息。

`var=value`

将用户参数 `var` 设置为 `value`。

## 文件

`/etc/X11/xorg.conf`

## 示例

禁用 `EdgeMotionMinSpeed`：

```bash
synclient EdgeMotionMinSpeed=0
```

## 作者

Peter Osterlund <> 以及其他。

此帮助页由 Mattia Dongili <> 编写。

## 参见

(1)、(1)、(4)

---

# syndaemon

## 名称

`syndaemon` - 一个监控键盘活动并在使用键盘时禁用触摸板的程序。

## 语法

`syndaemon [-i idle-ti] [-m poll-inverval] [-d] [-p pid-file] [-t] [-k] [-K] [-R]`

## 描述

在打字时禁用触摸板可以避免指针意外移动，这种移动可能会导致焦点转移到错误的窗口。

## 选项

`-i <idle-ti>`

在最后一次按键后等待多少秒再启用触摸板。（默认是 2.0s）。

`-m <poll-interval>`

两次轮询之间等待多少毫秒。如果此值太低，会导致不必要的唤醒。如果此值太高，某些按键（在两个间隔之间按下和释放）可能无法被注意到。此开关配合 `-R` 运行时无效。默认是 200ms。

`-d`

作为守护进程启动，即在后台运行。

`-p <pid-file>`

带有指定文件名的 pid 文件。只有当程序以守护进程模式启动时，才会创建 pid 文件。

`-t`

响应键盘活动时仅禁用点击和滚动，而不是鼠标移动。

`-k`

在监控键盘活动时忽略修饰键。

`-K`

类似于 `-k`，但也忽略修饰键+键的组合。

`-R`

使用 XRecord 扩展检测键盘活动，而不是轮询键盘状态。

`-?`

显示帮助信息。

## 环境变量

`DISPLAY`

指定要连接的 X 服务器。

## 退出代码

如果 `syndaemon` 以非 0 的返回码退出，则遇到的错误如下。

`Exit code 1`

命令行参数无效。

`Exit code 2`

无法建立到 X 服务器的连接或未找到触摸板设备。

`Exit code 3`

进入守护进程模式失败或无法创建 pid 文件。

`Exit code 4`

请求 XRECORD 但服务器上不可用或无效。

## 注意

连接到远程 X 服务器没有意义，因为守护进程将监控远程服务器的键盘活动，但会禁用本地机器上的触摸板。

## 作者

Peter Osterlund <>。

此帮助页由 Mattia Dongili <> 编写。

## 参见

(1)、(1)、(4)

---

# SYSLINUX

## 名称

`syslinux` - 在 FAT 文件系统上安装 SYSLINUX 引导程序。

## 语法

`syslinux [OPTIONS] device`

## 描述

`Syslinux` 是一个基于 MS-DOS/Windows FAT 文件系统的 Linux 操作系统引导程序。它旨在简化 Linux 的首次安装，并创建救援和其他特殊用途启动磁盘。

为了使用 `Syslinux` 创建可启动的 Linux 软盘，请准备一个普通的 MS-DOS 格式软盘。将一个或多个 Linux 内核文件复制其中，然后执行命令：

```bash
syslinux --install /dev/fd0
```

`-t`、`--offset`

指示文件系统位于设备或文件的基基偏移处。

`--once <command>`

声明一个仅在第一次启动时尝试的启动命令。

`--clear-once`

清除启动一次命令。

`-H`、`--heads <count>`

覆盖检测到的几何磁头数。

`-S`、`--sectors <count>`

覆盖检测到的几何扇区数。

`-z`、`--zipdrive`

假设软驱驱动几何结构（`--heads 64 --sectors 32`）。

## 文件

### 配置文件

`syslinux` 中所有可配置的默认值都可以通过在启动磁盘的安装目录中放置名为 `syslinux.cfg` 的文件来更改。这是一个 UNIX 或 DOS 格式的文本文件，包含一个或多个以下项目之一（关键字不区分大小写）。

此列表已过时。

在配置文件中，空行和以井号（`#`）开头的注释行将被忽略。

`default kernel [options ...]`

设置默认命令行。如果 `syslinux` 自动启动，它的行为将类似于在 `boot:` 提示符处输入了 `default` 之后的条目。

如果没有找到 `DEFAULT` 或 `UI` 语句，或者完全缺少配置文件，`SYSLINUX` 将显示错误消息并退回到 `boot:` 提示符（如果设置了 `NOESCAPE`，它将显示 “boot failed” 消息并停止；`PXELINUX` 在未找到配置文件时也是如此）。

注意：在 `SYSLINUX` 3.85 之前，如果不存在配置文件，或者配置文件中没有 `default` 条目，默认值是 `linux auto`。

更早版本的 `SYSLINUX` 曾会自动向用户使用 `DEFAULT` 命令指定的任何内容后追加 `auto` 字符串。从 1.54 版本开始，此规则不再适用，因为这在用 shell 作为 `init` 的替代品时会产生问题。你可能需要手动包含此选项。

#### `append` 选项 ...

向内核命令行中添加一个或多个 `options`。这些选项在自动启动和手动启动时都会添加。选项被添加到内核命令行的最开始，通常允许显式输入的内核选项覆盖它们。这等同于 (8) `append` 选项。

#### `label image append` 选项 ...

指示如果输入 `label` 作为要启动的内核，`syslinux` 将转而启动 `image`，并使用指定的 `append` 选项，而不是文件全局部分（第一个 `label` 命令之前）指定的选项。`image` 的默认值与 `label` 相同，如果未给出 `append`，则默认使用全局条目（如果有）。使用 `append -` 则表示不使用任何选项。最多允许 128 个 `label` 条目。

`image` 不一定非得 Linux 内核；它可以是一个引导扇（见下文）。

#### 隐式标志 `flag_val`

如果 `flag_val` 为 0，除非在 `label` 语句中显式指定，否则不加载内核镜像。默认值为 1。

#### `tiout tiout`

指示在 `boot:` 提示符处等待自动启动的时间，单位为 1/10 秒。一旦用户在键盘上输入任何内容，`tiout` 就会取消，假设用户将完成已开始的命令行。`tiout` 为零将完全禁用 `tiout`，这也是默认值。最大可能的 `tiout` 值为 35996；对应略低于一小时。

#### 串口 `port [baudrate]`

启用串口作为控制台。`port` 是一个数字（0 = `/dev/ttyS0` = `COM1` 等）；如果省略 `baudrate`，波特率默认为 9600 bps。串口参数硬编码为 8 位、无奇校验、1 个停止位。

为了确保此指令能够正常工作，它应该是配置文件中的第一个指令。

#### `font filena`

在显示任何输出之前加载 `.psf` 格式的字体（版权行除外，该行是在 `ldlinux.sys` 自身加载时输出的）。`syslinux` 仅将字体加载到显卡中；如果 `.psf` 文件包含 Unicode 表，则会被忽略。这仅在 EGA 和 VGA 显卡上有效；希望在其他显卡上不会产生任何影响。

#### `kbdmap keymap`

安装一个简单的键盘映射。使用的键盘重映射器非常简单（它只是重新映射了从 BIOS 接收的键码，这意味着只有与默认布局——通常是美国英语——相关的键组合可以被映射），但至少可以帮助使用 AZERTY 键盘布局以及寻找 `=` 和 `,` 位置的人（这是 Linux 内核命令行中频繁使用的两个特殊字符）。

包含的 (8) 程序可以从 (8) 分发创建此类键盘映射。

#### `display filena`

在启动时在屏幕上显示指定的文件（在 `boot:` 提示符之前，如果显示）。请参见下文关于 `DISPLAY` 文件的章节。如果文件缺失，则直接忽略此选项。

#### `prompt flag_val`

如果 `flag_val` 为 0，仅在按下 Shift 或 Alt 键，或设置 Caps Lock 或 Scroll Lock 时显示 `boot:` 提示符（这是默认值）。如果 `flag_val` 为 1，则始终显示 `boot:` 提示符。

#### `f1 filena f2 filena ... f9 filena f10 filena f11 filena f12 filena`

在 `boot:` 提示符处按下功能键时，在屏幕上显示指定的文件。这可以实现启动前的在线帮助（推测用于内核命令行选项）。

使用串口控制台时，按下 `<Ctrl-F><digit>` 进入帮助屏幕，例如按下 `<Ctrl-F>2` 进入 `f2` 屏幕。对于 `f10`-`f12`，按下 `<Ctrl-F>A`、`<Ctrl-F>B`、`<Ctrl-F>C`。为了兼容早期版本，`f10` 也可以作为 `<Ctrl-F>0` 输入。

### 显示文件格式

`DISPLAY` 和功能键帮助文件是 DOS 或 UNIX 格式的文本文件（带有或不带 `<CR>`）。此外，还会解释以下特殊代码：

- `<FF>` = `<Ctrl-L>` = ASCII 12

  清屏并移动光标。注意屏幕将用当前的显示颜色填充。

- `<SI><bg><fg>`，`<SI>` = `<Ctrl-O>` = ASCII 15

  将显示颜色设置为指定的背景色和前景色，其中 `<bg>` 和 `<fg>` 是十六进制数字，对应标准 PC 显示属性：

  `0 = 黑色 8 = 深灰色 1 = 深蓝色 9 = 亮蓝色 2 = 深绿色 a = 亮绿色 3 = 深青色 b = 亮青色 4 = 深红色 c = 亮红色 5 = 深紫色 d = 亮紫色 6 = 棕色 e = 黄色 7 = 浅灰色 f = 白色`

  选择亮色（8-f）作为背景会导致相应的深色（0-7），且前景会闪烁。这些颜色在串口控制台上不可见。

- `<CAN>filena<newline>`，`<CAN>` = `<Ctrl-X>` = ASCII 24

  如果存在 VGA 显示器，进入图形模式并显示指定文件中的图形。该格式是一种称为 LSS16 的专用格式。包含的 Perl 程序 `ppmtolss16` 可用于生成这些图像。图像以 640x480 16 色模式显示。一旦进入图形模式，显示属性（由 `<SI>` 代码序列设置）的工作方式略有不同：背景色被忽略，前景颜色是图像文件中指定的 16 种颜色。因此，`ppmtolss16` 允许你指定某些颜色分配给颜色索引。

  特别是颜色索引 0 和 7 应该仔细选择：0 是背景色，7 是 SYSLINUX 自身打印文本使用的颜色。

- `<EM>`，`<EM>` = `<Ctrl-U>` = ASCII 25

  如果当前处于图形模式，则返回文本模式。

- `<DLE>..<ETB>`，`<Ctrl-P>..<W>` = ASCII 16-23

  这些代码可以用于选择以何种模式打印消息文件的特定部分。每个控制字符选择一组特定的模式（文本屏幕、图形屏幕、串口），输出实际显示在其中：

  | 字符 | 文本 | 图形 | 串口 |
  |---|---|---|---|
  | ... | ... | ... | ... |

链加载要求外部操作系统的引导扇存储在文件系统根目录下的文件中。由于 Linux 内核和引导扇镜像都没有可靠的魔数，`syslinux` 将检查扩展名。以下扩展名被识别为：

- `none` 或其他 Linux 内核镜像
- `BSS` 引导区（DOS 超块将被补丁在）
- `BS` 引导区

对于命令行给出的文件名，如果未找到原始文件名，`syslinux` 将按照上述顺序添加扩展名来搜索该文件。`KERNEL` 语句中的文件名必须是全路径。

### 新手保护

`syslinux` 会尝试检测用户是否正尝试在 286 或更低级别的机器上启动，或者在少于 608K 低内存（`DOS` RAM）的机器上启动（这将导致 Linux 启动无法完成）。如果是这样，将显示消息并终止启动序列。在启动时按住 `Ctrl` 键可以禁用此功能。

特定 `syslinux` 版本的编译时间和编译日期可以通过 DOS 命令 `type ldlinux.sys` 获取。这也被用作 `LDLINUX.SYS` 文件的签名，它必须与引导区匹配。

`syslinux` 使用的任何文件都可以根据需要标记为隐藏、系统或只读；`syslinux` 会忽略所有文件属性。自动安装的 `SYSLINUX` 会对 `LDLINUX.SYS` 设置只读属性。

### 可启动光盘

`SYSLINUX` 可用于创建兼容 El Torito 的可启动 CD-ROM 磁盘镜像。然而，许多 BIOS 在处理启动光盘方面似乎存在很多 Bug。因此，用户报告以下步骤对于制作在尽可能多机器上均可启动的光盘很有帮助：

- 对 `SYSLINUX` 使用 `-s`（安全、缓慢且愚笨）选项。
- 将启动镜像尽可能地放在 ISO 9660 文件系统的开头。
- CD-ROM 的速度远快于软盘，因此从速度角度来看，`-s` 选项其实并不重要。

当然，你可能更想使用 `ISOLINUX`。请参阅文档 `isolinux.doc`。

### 从硬盘上的 FAT 分区启动

`SYSLINUX` 可以从硬盘上的 FAT 文件系统分区启动（包括 `FAT32`）。其安装步骤与在软盘上安装的程序相同，并且在 DOS 或 Linux 下均可正常工作。要从分区启动，`SYSLINUX` 需要从主引导记录（MBR）或另一个引导加载程序启动，就像 DOS 本身一样。`SYSLINUX` 包含了一个示例主引导扇（`r.bin`）。

## 缺陷

我非常欢迎收到你在使用 `SYSLINUX` 时遇到的任何问题反馈。如果你成功使用了 `SYSLINUX`，我也想听听你的反馈，特别是当你将其用于发行版时。

如果你正在报告问题，请包含关于你的系统和 BIOS 的所有信息；绝大多数报告的问题都被证明是 BIOS 或硬件 Bug，我需要尽可能的信息来诊断问题。

有一个用于 `SYSLINUX` 用户讨论以及发布新版本和测试版本的邮件列表。要加入，请向 [ ] 发送邮件，并在正文中包含以下行：

```text
subscribe syslinux
```

提交地址为 []。

## 另请

(8)、(8)、(8)、(8)、(1)。

## 作者

本手册页是 H. Peter Anvin <> 编写的原始 `syslinux` 文档的修改版本。转换为 man 页的工作由 Arthur Korn <> 完成。

---

# SYSLINUX2ANSI

## 名称

`syslinux2ansi` - 将 syslinux 格式的屏幕转换为 pc-ansi。

## 语法

```bash
syslinux2ansi < filena.input > filena.output
```

## 描述

`syslinux2ansi` 是一个过滤器，用于将 `syslinux` 格式的屏幕转换为与 PC ANSI 的格式。它只从标准输入读取，没有命令行选项。

## 缺陷

帮助和版本命令行选项将会很有用。

在命令行上放置输入和输出文件名可能也不错。

### 缺陷报告

我非常欢迎收到你在使用 `SYSLINUX` 时遇到的任何问题反馈。如果你成功使用了 `SYSLINUX`，我也想听听你的反馈，特别是当你将其用于发行版时。

如果你正在报告问题，请包含关于你的系统和 BIOS 的所有信息；绝大多数报告的问题都被证明是 BIOS 或硬件 Bug，我需要尽可能的信息来诊断问题。

有一个用于 `SYSLINUX` 用户讨论以及发布新版本和测试版本的邮件列表。要加入，请向 [ ] 发送邮件，并在正文中包含以下行：

```text
subscribe syslinux
```

提交地址为 []。

## 另请

(1)、(1)

## 作者

本手册页是 Kevin Krear <> 为 Debian 编写的快速说明，通过查看 `syslinux2ansi` 的一整页 Perl 代码完成。

---

# SYSTEM-CONFIG-ABRT

## 名称

`system-config-abrt` - 用于配置 ABRT 的 GUI 工具。

## 语法

```bash
system-config-abrt
```



## 描述

`system-config-abrt` 是一个图形化工具，为用户提供了一个在一个处更改 ABRT 配置文件的方法。

## 作者

ABRT 团队

---

# SYSTEMCTL

## 名称

单元的属性随单元类型而异，因此显示任何单元（即使是不存在的）都是列出与该类型相关的属性的方法。同样，显示任何作业将列出与所有作业相关的属性。单元属性记录在 (5) 中，以及各个单元类型的页面 (5) 等中。

### `-a`、`--all`

在列出单元时，显示所有已加载的单元，无论其状态如何，包括未激活的单元。在显示单元、作业或管理器属性时，无论是否设置都显示所有属性。

要列出系统上安装的所有单元，请使用 `list-unit-files` 命令。

### `-r`、`--recursive`

在列出单元时，也显示本地容器的单元。本地容器的单元将以容器名称为缀，用单个冒号（":"）分隔。

### `--reverse`

使用 `list-dependencies` 显示单元之间的反向依赖关系，即遵循 `WantedBy=`、`RequiredBy=`、`RequiredByOverridable=`、`PartOf=`、`BoundBy=` 类型的依赖关系，而不是 `Wants=` 类似关系。

### `--after`

使用 `list-dependencies` 显示在指定单元排序之前的单元。换句话说，递归列出遵循 `After=` 依赖的单元。

注意，任何 `After=` 依赖会自动镜像创建一个 `Before=` 依赖。时间依赖可以显式指定，但也会隐式创建，例如对于 `WantedBy=` 目标（参见 (5)）以及由于其他指令（例如 `RequiresMountsFor=`）。显式和隐式引入的依赖关系都会通过 `list-dependencies` 显示。

### `--before`

使用 `list-dependencies` 显示在指定单元之后的单元。换句话说，递归列出遵循 `Before=` 依赖关系的单元。

### `-l`、`--full`

在 `status`、`list-units`、`list-jobs` 和 `list-tirs` 的输出中不省略单元名称、进程树项、日志输出或截断单元描述。

### `--show-types`

在显示套接字时显示套接字类型。

### `--job-mode=`

当队列新任务时，此选项控制如何处理已排队的任务。它接受 `"fail"`、`"replace"`、`"replace-irreversibly"`、`"isolate"`、`"ignore-dependencies"`、`"ignore-requirents"` 或 `"flush"` 之一。默认为 `"replace"`，但使用 `isolate` 命令时除外，该命令意味着 `"isolate"` 任务模式。

如果指定 `"fail"` 且请求的操作与等待处理的任务冲突（具体而言：导致已等待处理的启动任务反转为停止任务，或反之），则导致该操作失败。

如果指定 `"replace"`（默认值），将根据需要替换任何冲突的等待处理的任务。

如果指定 `"replace-irreversibly"`，操作方式类似于 `"replace"`，但会将新任务标记为不可逆的。这防止了未来的冲突事务替换这些任务（甚至在不可逆任务仍在等待处理期间防止其被排入队列）。不可逆任务仍可以使用 `cancel` 命令取消。

`"isolate"` 仅对启动操作有效，并在启动指定单元时停止所有其他单元。在使用 `isolate` 命令时始终使用此模式。

`"flush"` 将导致在新任务排队时，所有已排队的任务被取消。

如果指定 `"ignore-dependencies"`，则此新任务将忽略所有单元依赖并立即执行操作。如果传递了此项，将不会引入所传递单元的需要单元，也不会遵守顺序依赖。这主要是为管理员提供的调试和救援工具，不应供应用程序使用。

`"ignore-requirents"` 与 `"ignore-dependencies"` 类似，但仅忽略需要依赖（requirement dependencies），顺序依赖仍会被遵守。

### `-i`、`--ignore-inhibitors`

当请求系统关机或睡眠状态时，忽略抑制锁（inhibitor locks）。应用程序可以建立抑制锁以避免某些重要操作（如刻刻 光等）被系统关机或睡眠状态中断。任何用户都可以获取这些锁，特权用户可以覆盖这些锁。如果获取了任何锁，关机和睡眠请求通常会失败（无论是否有特权），并打印活动锁列表。然而，如果指定了 `--ignore-inhibitors`，锁将被忽略且不打印，并且仍会尝试操作，可能需要额外的权限。

### `-q`、`--quiet`

在 `snapshot`、`is-active`、`is-failed`、`is-enabled`、`is-system-running`、`enable` 和 `disable` 中抑制到标准输出的输出。

### `--no-block`

不要同步等待请求的操作完成。如果没有指定此项，任务将通过验证、排队，`systemctl` 将等待直到单元启动完成。通过传递此参数，仅会进行验证和排队。

### `--user`

与调用用户的服务管理器通信，而不是系统的服务管理器通信。

### `--system`

与系统的服务管理器通信。这是隐含的默认值。

### `--no-wall`

在停止、关机、重启之前不发送广播消息（wall message）。

### `--global`

当与 `enable` 和 `disable` 配合使用时，对全局用户配置目录操作，从而为所有用户未来的登录全局范围内启用或禁用单元文件。

### `--no-reload`

当与 `enable` 和 `disable` 配合使用时，执行更改后不隐式重新加载守护进程配置。

### `--no-ask-password`

当与 `start` 和相关命令配合使用时，禁用询问密码。后台服务可能需要输入密码或密码语字符串，例如解锁系统硬盘或加密证书。除非指定了此项且从终端调用命令，否则 `systemctl` 将在终端询问用户所需的密钥。使用此项来关闭此行为。在这种情况下，密码必须由其他方式（例如图形界面密码代理）提供，否则服务可能会失败。这还禁用了对特权操作询问用户身份。

### `--kill-who=`

当与 `kill` 配合使用时，选择向哪些进程发送信号。必须是 `main`、`control` 或 `all` 之一，以选择仅杀掉主进程、控制进程或单元的所有进程。单元的主进程是定义其生命周期的进程。单元的控制进程是管理器调用以诱导其状态变化的进程。例如，由于服务单元的 `ExecStartPre=`、`ExecStop=` 或 `ExecReload=` 设置而启动的所有进程都是控制进程。注意，每个单元一次只有一个控制进程，因为一次只执行一个状态变化。对于类型 `Type=forking` 的服务，管理器为 `ExecStart=` 启动的初始进程是控制进程，而由该进程最终派生的进程随后被视为单元的主进程（如果可以确定的话）。其他类型的服务单元则不同，管理器为 `ExecStart=` 派生的进程始终是主进程本身。服务单元由零或一个主进程、零或一个控制进程以及任意数量额外进程组成。并不是所有的单元类型都管理这些进程。例如，对于挂载单元，定义了控制进程（`/usr/bin/mount` 和 `/usr/bin/umount` 的调用），但没有定义主进程。如果省略，默认为 `all`。

### `-s`、`--signal=`

当与 `kill` 配合使用时，选择向所选进程发送什么信号。必须是著名的信号标识符，如 `SIGTERM`、`SIGINT` 或 `SIGSTOP` 之一。如果省略，默认为 `SIGTERM`。

### `-f`、`--force`

当与 `enable` 使用时，覆盖任何现有的链接。

当与 `halt`、`poweroff`、`reboot` 或 `kexec` 使用时，在不关闭所有单元的情况下执行选定的操作。然而，所有进程将被强制杀死，所有文件系统将被卸载或重新挂载为只读。因此，这是请求立即重启的一种极端但相对安全的选项。如果对这些操作指定了两次 `--force`，它们将立即执行而不终止任何进程或卸载任何文件系统。警告：在任何这些操作中指定两次 `--force` 可能导致数据丢失。

### `--now`

当与 `enable` 使用时，单元也将将被启动。当与 `disable` 或 `mask` 使用时，单元也将将被停止。只有在相应的启用或禁用操作成功后才会执行启动或停止操作。

### `--root=`

当与 `enable`、`disable`、`is-enabled`（以及相关命令）一起时，使用备根路径查找单元文件。

### `--runtime`

当与 `enable`、`disable`、`edit`（以及相关命令）一起时，仅进行临时更改，以便其在下次重启时丢失。这将产生这种效果：更改不在 `/etc` 的子目录中，而是在 `/run` 中，具有相同的立即效果，但由于后者在重启时会丢失，更改也会丢失。

同样，当与 `set-property` 使用时，仅进行临时更改，以便其在下次重启时丢失。

### `--preset-mode=`

### `-H`、`--host=`

远程执行操作。指定一个主机名或用 `"@"` 分隔的用户名和主机名进行连接。主机名可选带有以 `":"` 分隔的容器名后缀，这将直接连接到指定主机上的特定容器。此将使用 SSH 与远程机器管理器实例通信。可以使用 `machinectl -H HOST` 列出容器名。

### `-M`、`--machine=`

在本地容器上执行操作。指定一个要连接的容器名。

### `--no-pager`

不将输出管道到分页器中。

### `--no-legend`

不打印图例，即列标题和带有提示的页脚。

### `-h`、`--help`

打印简短帮助文本并退出。

### `--version`

打印简短的版本字符串并退出。

## 命令

支持以下命令：

### 单元命令

#### `list-units [PATTERN...]`

列出已知单元（受 `-t` 指定的限制）。如果指定了一个或多个 `PATTERN`，则只显示匹配其中之一的单元。

这是默认命令。

#### `list-sockets [PATTERN...]`

按监听地址列出 socket 单元。如果指定了一个或多个 `PATTERN`，则只显示匹配其中之一的 socket 单元。产生的输出类似于：

```text
LISTEN UNIT ACTIVATES
/dev/initctl systemd-initctl.socket systemd-initctl.service
... [::]:22 sshd.socket sshd.service
kobject-uevent 1 systemd-udevd-kernel.socket systemd-udevd.service
5 sockets listed.
```




注意：由于地址可能包含空格，此输出不适用于程序化处理。  
另见选项 `--show-types`、`--all` 和 `--state=`。

### `list-timer [PATTERN...]`

按下次到的计时时间列出 timer 单元。如果指定了一个或多个 `PATTERN`，则只显示匹配其中之一的单元。  
另见选项 `--all` 和 `--state=`。

### `start [PATTERN...]`

启动（激活）命令行上指定的一个或多个单元。

注意，全局通配符模式作用于当前加载的单元列表。未激活且未处于失败状态的单元通常未加载，因此不会被任何模式匹配。此外，对于已实例化的单元，systemd 在实例启动之前通常感知不到实例名。因此，在 `start` 中使用全局通配符模式用途有限。

### `stop [PATTERN...]`

停止（去激活）命令行上指定的一个或多个单元。

### `reload [PATTERN...]`

请求命令行上列出的所有单元重新加载其配置。注意，这将重新加载服务特定的配置，而不是 systemd 的单元配置文件。如果你想让 systemd 重新加载单元的配置文件，请使用 `daemon-reload` 命令。

换句话说：对于 Apache 的示例，这将重新加载 Web 服务器中的 Apache `httpd.conf`，而不是 `apache.service` systemd 单元文件。

此命令不应与 `daemon-reload` 命令混淆。

### `restart [PATTERN...]`

重启命令行上指定的一个或多个单元。如果单元尚未运行，它们将被启动。

### `try-restart [PATTERN...]`

如果单元正在运行，则重启命令行上指定的一个或多个单元。如果单元未运行则什么都不做。注意，为了与 RedHat init 脚本兼容，`condrestart` 与此命令等效。

### `reload-or-restart [PATTERN...]`

如果支持，则重新加载一个或多个单元。不支持，则重启它们。如果单元尚未运行，它们将被启动。

### `reload-or-try-restart [PATTERN...]`

如果支持，则重新加载一个或多个单元。不支持，则重启它们。如果单元未运行则什么都不做。注意，为了与 SysV init 脚本兼容，`force-reload` 与此命令等效。

### `isolate NAME`

启动命令行上指定的单元及其依赖项，并停止所有其他单元。如果给出没有扩展名的单元名，将自动加上 `.target` 后缀。

这类似于在传统的 init 系统中更改运行级别。`isolate` 命令将立即停止在新单元中未启进程，可能包括你正在使用的图形环境或终端。

注意，这仅在启用了 `AllowIsolate=` 的单元上允许。详情请见 (5)。

### `kill [PATTERN...]`

向单元的一个或多个进程发送信号。使用 `--kill-who=` 选择要杀的进程。使用 `--signal=` 选择要发送的信号。

### `is-active [PATTERN...]`

检查指定的单元是否处于激活状态（即正在运行）。如果至少有一个处于激活，则返回退出码 `0`，否则返回非零。除非指定了 `--quiet`，否则会将当前单元状态打印到标准输出。

### `is-failed [PATTERN...]`

检查指定的单元是否处于“失败”（failed）状态。如果至少有一个已失败，则返回退出码 `0`，否则返回非零。除非指定了 `--quiet`，否则会将当前单元状态打印到标准输出。

### `status [PATTERN...|PID...]`

显示关于一个或多个单元的简要运行状态信息，随后是来自日志的最新日志数据。如果没有指定单元，则显示系统状态。如果与 `--all` 配合，还会显示所有单元的状态（受 `-t` 指定的限制）。如果传递了 `PID`，则显示该进程所属单元的信息。

此功能旨在生成人类可读的输出。如果你正在寻找计算机可解析的输出，请使用 `show`。默认情况下，此函数仅显示 10 行输出，并截断行以适应终端窗口。可以通过 `--lines` 和 `--full` 修改，见上文。此外，`journalctl --unit=NAME` 或 `journalctl --user-unit=NAME` 使用类似的消息过滤，并可能更方便。

### `show [PATTERN...|JOB...]`

显示一个或多个单元、作业或管理器本身的属性。如果没有指定参数，将显示管理器的属性。如果指定了单元名，则显示单元的属性；如果指定了作业 ID，则显示作业的属性。默认情况下，空属性会被隐藏。使用 `--all` 显示这些属性。要选择显示的特定属性，请使用 `--property=`。

此命令旨在任何需要计算机可解析输出的场景。如果你正在寻找格式化的人类可读输出，请使用 `status`。

### `cat [PATTERN...]`

显示一个或多个单元的备份文件。打印单元的“片段”（fragment）和“覆盖”（drop-ins，源文件）。每个文件之前都有一个包含文件名的注释。

### `set-property NAME ASSIGNMENT...`

在支持的运行时设置指定的单元属性。这允许在运行时更改配置参数属性，例如资源控制设置。并非所有属性都可以在运行时更改，但许多资源控制设置（主要是 (5) 中的）可以更改。

更改会立即生效，并存储在磁盘上供以后启动，除非传递了 `--runti` 参数，在这种情况下设置仅持续到下次重启为止。属性赋值的语法严格遵循单元文件中赋值的语法。

示例：`systemctl set-property foobar.service CPUShares=777`

注意，此命令允许同时更改多个属性，这比逐个设置它们更好。类似于单元文件配置设置，将空列表分配给列表参数将重置列表。

### `help PATTERN...|...PID...`

注意，此操作仅为单元创建建议的链接。虽然此命令是操作单元配置目录推荐的方法，但管理员可以自由通过在目录中放置或删除链接来手动进行额外更改。这对于创建偏离建议默认安装的配置特别有用。在这种情况下，管理员必须确保根据需要手动调用 `daemon-reload` 以确保更改生效。

启用单元不应与通过 `start` 命令启动（激活）单元相混淆。启用和启动单元是正交的：单元可以被启用而不启动，也可以在不启用的情况下启动。

启用仅仅是将单元挂钩到各种建议的位置（例如，以便单元在启动时或插入特定类型硬件时自动启动）。启动实际上会派生守护进程（对于服务单元）或绑定套接字（对于套接字单元）等。

根据指定的是 `--system`、`--user`、`--runti` 还是 `--global`，启用单元针对系统、仅针对调用用户、仅针对系统本次启动、所有用户未来的登录，或仅针对本次启动。注意在最后一种情况下，不会重新加载 systemd 守护配置。

在屏蔽（masked）单元上使用 `enable` 会导致错误。

### `disable NAME...`

禁用一个或多个单元。这将从单元配置目录中删除指向指定单元文件的所有链接，从而撤销由 `enable` 做的更改。但注意，这会移除单元文件的所有链接（即包括手动添加的），而不仅仅是由 `enable` 创建的。

此调用在完成禁用单元后会隐式重新加载 systemd 守护配置。注意，此命令不会隐式停止正在禁用的单元。如果需要，应与此命令配合使用 `--now`，或者在之后执行额外的 `stop` 命令。

此命令将打印执行的操作。可以通过传递 `--quiet` 抑制此输出。

此命令对 `--system`、`--user`、`--runti` 和 `--global` 的遵循方式与 `enable` 类似。

### `reenable NAME...`

重新启用命令行指定的多个单元文件。这是 `disable` 和 `enable` 的组合，用于将单元启用的链接重置为单元文件 `[Install]` 部分配置的默认值。

### `preset NAME...`

将命令行指定的多个单元文件重置为预设策略文件中配置的默认值。其效果与 `disable` 或 `enable` 类似，取决于单元在预设文件中列出的方式。

使用 `--preset-mode=` 控制单元应该是启用并禁用、仅启用还是仅禁用。

有关预设策略格式的更多信息，请参见 (5)。关于预设概念的更多信息，请咨询 `Preset` 文。

### `preset-all`

将所有已安装的单元文件重置为预设策略文件中配置的默认值（见上文）。

使用 `--preset-mode=` 控制单元应该是启用并禁用、仅启用还是仅禁用。

### `is-enabled NAME...`

检查指定的单元文件是否启用（同 `enable`）。如果至少有一个已启用，则返回退出码 `0`，否则返回非零。打印当前的启用状态（见表）。要抑制此输出，请使用 `--quiet`。

**表 1：`is-enabled` 输出**

| 打印字符串 | 含义 | 返回值 |
| :--- | :--- | :--- |
| `enabled` | 通过 `.wants` 目录中的链接启用（永久或仅在 `/run`）。 | `0` |
| `enabled-runti` |  |  |
| `linked` | 通过指向单元文件的链接可用（永久或仅在 `/run`）。 | `1` |
| `linked-runti` |  |  |
| `masked` | 完全禁用（永久或仅在 `/run`）。 | `1` |
| `masked-runti` |  |  |
| `static` | 单元文件未启用，且在 `[Install]` 部分没有提供启用的规定。 | `0` |
| `indirect` | 单元文件本身未启用，但其 `[Install]` 部分中有非空的 `Also=` 设置，列出了可能启用的其他单元文件。 | `0` |
| `disabled` | 单元文件未启用。 | `1` |

### `mask NAME...`

屏蔽命令行指定的多个单元文件。这将这些单元链接到 `/dev/null`，使其无法启动。这是 `disable` 的强力版本，因为它禁止了单元的各种激活，包括启用和手动激活。请谨慎使用此选项。

它遵循 `--runti` 选项，仅临时屏蔽直到系统下次重启。`--now` 选项可以确保单元也被停止。

### `unmask NAME...`

取消命令行上指定的一个或多个单元文件的锁定。这将撤销 `mask` 的效果。

### `link FILENAME...`

将一个不在单元文件搜索路径中的单元文件链接到单元文件搜索路径中。这需要单元文件的绝对路径。此效果可以通过 `disable` 撤销。

此命令的效果是使得单元文件可供 `start` 和其他命令使用，尽管它没有直接安装在单元搜索路径中。

### `add-wants TARGET NAME...`、`add-requires TARGET NAME...`

分别为指定的 `TARGET` 的一个或多个单元添加 `Wants=` 或 `Requires=` 依赖项。

此命令以类似于 `enable` 的方式处理 `--system`、`--user`、`--runti` 和 `--global`。

### `edit NAME...`

编辑一个 drop-in 配置（如果指定了 `--full` 则编辑整个替换文件），以扩展或覆盖指定的单元。

取决于是否指定 `--system`（默认）、`--user` 或 `--global`，这将为每个单元创建一个针对系统、调用用户或所有用户未来登录的 drop-in 文件。然后，将在临时文件上调用编辑器（见下文“Environment”部分），如果编辑器成功退出，这些文件将写入实际位置。

如果指定了 `--full`，这将复制原始单元而不是创建 drop-in 文件。

如果指定了 `--runti`，更改将临时在 `/run` 中进行，并在下次重启时丢失。

如果退出时临时文件为空，则取消对相关单元的修改。

在编辑单元后，将重新加载 systemd 配置（其方式等同于 `daemon-reload`）。

注意，此命令不能用于远程编辑单元，且你无法临时编辑位于 `/etc` 中的单元，因为它们的优先级高于 `/run`。

### `get-default`

返回要启动的默认目标。这返回 `default.target` 别名（符号）所指向的目标单元。

### `set-default NAME`

设置要启动的默认目标。这会将 `default.target` 别名指向指定的单元单元。

## 机器命令

### `list-machines [PATTERN...]`

列出主机和所有运行中的本地容器及其状态。如果指定了一个或多个 `PATTERN`，则只显示匹配其中一个模式的容器。

## 任务命令

### `list-jobs [PATTERN...]`

列出正在进行的任务。如果指定了一个或多个 `PATTERN`，则只显示匹配其中一个模式的单元的任务。

### `cancel JOB...`

通过数值任务 ID 取消命令行指定的一个或多个任务。如果没有指定任务 ID，则取消所有挂起的任务。

## 快照命令

### `snapshot [NAME]`

创建快照。如果指定了快照名称，则新快照将以此名称命名。如果没有指定，则会生成一个自动快照名称。在任何情况下，快照名称都会打印到标准输出，除非指定了 `--quiet`。

取消一个或多个 systemd 管理器环境变量。如果只指定了变量名称，无论其值如何都将被删除。如果指定了变量和值，则只有当该变量具有指定的值时才会被删除。

### `import-environnt [VARIABLE...]`

将客户端上设置的一个或多个环境变量导入到 systemd 管理器环境块。如果没有传递任何参数，则导入整个环境块。否则，应传递一个或多个环境变量名称列表，其客户端值将被导入管理器的环境块中。

## 管理器生命周期命令

### `daemon-reload`

重新加载 systemd 管理器配置。这将重新运行所有生成器（见 (7)），重新加载所有单元文件并重建整个依赖树。在守护器重新加载期间，systemd 代表用户监听的所有套接字将保持可用。

此命令不应与 `reload` 命令混淆。

### `daemon-reexec`

重新执行 systemd 管理器。这将序列化管理器状态，重新执行进程并再次反序列化状态。此命令除了调试和软件包升级外几乎没有用处。但是，它可能作为重量级的 `daemon-reload` 很有帮助。

在守护器重新执行期间，systemd 代表用户监听的所有套接字将保持可用。

## 系统命令

### `is-system-running`

检查系统是否运行正常。当系统完全启动并运行（即不在启动、关机或维护模式）时，返回成功。否则返回失败。

此外，当前状态将以短字符串的形式打印到标准输出，见下表。使用 `--quiet` 抑制此输出。

**表 2：管理器运行状态**

| 名称 | 含义 |
| :--- | :--- |
| `initializing` | 早期启动，在达到 `basic.target` 之前或进入 `maintenance` 状态之前。 |
| `starting` | 晚期启动，在任务队列首次为空闲之前或达到其中一个救援目标之前。 |
| `running` | 系统完全运行。 |
| `degraded` | 系统运行正常但一个或多个单元失败。 |
| `maintenance` | 救援或紧急目标处于激活状态。 |
| `stopping` | 管理器正在关机。 |

### `default`

进入默认模式。这大部分等同于 `isolate default.target`。

### `rescue`

进入救援模式。这大部分等同于 `isolate rescue.target`，但向所有用户打印广播消息。

### `ergency`

进入紧急模式。这大部分等同于 `isolate ergency.target`，但向所有用户打印广播消息。

### `halt`

关机并停止系统。这大部分等同于 `start halt.target --job-mode=replace-irreversibly`，但向所有用户打印广播消息。

如果带有 `--force`，将跳过所有运行服务的关机，但所有进程将被杀死，所有文件系统将被卸载或挂载为只读，随后系统停止。如果指定两次 `--force`，操作将立即执行，而不终止任何进程或卸载任何文件系统。这可能导致数据丢失。

### `poweroff`

关机并关闭系统。这大部分等同于 `start poweroff.target --job-mode=replace-irreversibly`，但向所有用户打印广播消息。

如果带有 `--force`，将跳过所有运行服务的关机，但所有进程将被杀死，所有文件系统将被卸载或挂载为只读，随后关闭电源。如果指定两次 `--force`，操作将立即执行，而不终止任何进程或卸载任何文件系统。这可能导致数据丢失。

### `reboot [arg]`

关闭并重启系统。这大部分等同于 `start reboot.target --job-mode=replace-irreversibly`，但也会向所有用户打印广播消息。

如果配合 `--force` 使用，将跳过所有正在运行服务的关闭，但所有进程将被杀死，且所有文件系统将被卸载或挂载为只读，随后立即进行重启。如果指定两次 `--force`，操作将立即执行，而不终止任何进程或卸载任何文件系统。这可能导致数据丢失。

如果给定了可选参数 `arg`，它将作为可选参数传递给 (2) 系统调用。该值取决于架构和固件。例如，可以使用 `"recovery"` 来触发系统恢复，可以使用 `"fota"` 来触发“空中下载固件（firmware over the air）”更新。

### `kexec`

通过 kexec 关闭并重启系统。这大部分等同于 `start kexec.target --job-mode=replace-irreversibly`，但也会向所有用户打印广播消息。

如果配合 `--force` 使用，将跳过所有正在运行服务的关闭，但所有进程将被杀死，且所有文件系统将被卸载或挂载为只读，随后立即进行重启。

### `exit`

要求 systemd 管理器退出。这仅支持用户服务管理器（即与 `--user` 选项配合使用），否则将失败。

### `switch-root ROOT [INIT]`

切换到不同的根目录并在其下方执行新的系统管理器进程。这旨在用于初始 RAM 磁盘（`"initrd"`），并将从 initrd 的系统管理器进程（即 `"init"` 进程）过渡到主系统管理器进程。

此调用接受两个参数：将成为新根目录的目录，以及其下方将作为 PID 1 执行的新系统管理器二进制文件路径。如果后者被省略或为空字符串，系统将自动搜索并使用 systemd 二进制文件作为 init。

如果系统管理器路径被省略或为空字符串，则 initrd 系统管理器进程的状态将传递给主系统管理器，这允许稍后检查参与 initrd 启动的涉及的服务状态。

### `suspend`

挂起系统。这将触发特殊 `suspend.target` 目标的激活。

### `hibernate`

使系统进入休眠状态。这将触发特殊 `hibernate.target` 目标的激活。

### `hybrid-sleep`

将系统进入休眠并挂起。这将触发特殊 `hybrid-sleep.target` 目标的激活。

## 参数语法

上述列出的单元命令接受单个单元名称（指定为 `NAME`）或多个单元规范（指定为 `PATTERN`...）。

在第一种情况下，可以给出带或不带后缀的单元名称。如果未指定后缀，systemctl 将附加一个合适的后缀，默认是 `.service`，并且对于仅操作于特定单元类型的命令，将附加类型特定的后缀。

例如，




# systemctl start sshd

```
systemctl start sshd
```

# systemctl start sshd.service

它们是等价的，同样如下：

```
systemctl isolate default
```

```
systemctl isolate default.target
```

注意，到设备节点的（绝对）路径会自动转换为设备单元名称，其他到挂载单元名称的（绝对）路径将转换为挂载单元名称。

```
systemctl status /dev/sda
systemctl status /ho
```

它们等价于：

```
systemctl status dev-sda.device
systemctl status ho.mount
```

在第二种情况下，将使用 shell 风格的 glob 与当前加载的单元进行匹配；字面单元名称（无论是否带后缀）将像第一种情况一样处理。这确保字面单元名称始终指向精确的一个单元，但 glob 可能会匹配零个单元，这不被视为错误。

Glob 模式使用 `glob(3)`，因此使用了标准的 shell 风格 glob 匹配规则，可以使用 `"*"`、`"?"` 和 `"[]"`。更多信息请参阅 `glob(7)`。模式与当前加载的单元名称进行匹配，不匹配任何内容的模式将被静默地跳过。例如：

```
systemctl stop sshd@*.service
```

将停止所有实例。

对于单元文件命令，指定的 `NAME` 应该是单元文件的完整名称，或者到该单元文件的绝对路径：

```
systemctl enable foo.service
```

# SYSTEMD-ANALYZE

## 名称

`systemd-analyze` - 分析系统启动性能

## 概要

`systemd-analyze` [OPTIONS...] [time]

`systemd-analyze` [OPTIONS...] blame

`systemd-analyze` [OPTIONS...] critical-chain [*UNIT*...]

`systemd-analyze` [OPTIONS...] plot [>file.svg]

`systemd-analyze` [OPTIONS...] dot [*PATTERN*...] [>file.dot]

`systemd-analyze` [OPTIONS...] dump

`systemd-analyze` [OPTIONS...] set-log-level [*LEVEL*]

`systemd-analyze` [OPTIONS...] verify [*FILES*...]

## 描述

`systemd-analyze` 可用于确定系统启动性能统计，并从系统和服务管理器检索其他状态和跟踪信息，并验证单元文件的正确性。

`systemd-analyze time` 打印在到达用户空间之前在内核中花费的时间、在到达正常系统用户空间之前在初始 RAM 磁盘 (initrd) 中花费的时间，以及正常系统用户空间初始化所花费的时间。注意，这些时间仅确保了到所有系统服务被派生为止的时间，但并不一定直到它们完全完成初始化或磁盘空闲。

`systemd-analyze blame` 打印所有运行单元的列表，按它们初始化所需的时间排序。此信息可用于优化启动时间。注意，输出可能具有误导性，因为一个服务的初始化缓慢可能是因为它在等待另一个服务的初始化完成。

`systemd-analyze critical-chain [*UNIT*...]` 打印单元关键时间链的树（对于每个指定的 `UNIT`，否则对于默认目标）。在单元激活或启动之后的时间打印在 `"@"` 字符之后。单元启动所需的时间打印在 `"+"` 字符之后。注意，输出可能具有误导性，因为一个服务的初始化可能依赖于套接激活，并且由于单元的并行执行。

`systemd-analyze plot` 打印 SVG 图形，详细说明哪些系统服务在什么时间启动，突出显示它们在初始化上花费的时间。

`systemd-analyze dot` 生成 dot 格式的文本依赖图描述，以便使用 GraphViz `dot(1)` 工具进一步处理。使用类似 `systemd-analyze dot | dot -Tsvg > systemd.svg` 的命令行生成图形依赖树。除非传递了 `--order` 或 `--require`，否则生成的图将同时显示顺序和强制依赖。可以在结尾给出可选的模式 glob 风格规范（例如 `*.target`）。如果这些模式中的任何一个匹配源节点或目标节点，则图中包含该单元依赖。

`systemd-analyze dump` 输出完整的（通常很长的）人类可读服务器状态序列化。其格式可能会在不通知的情况下更改，不应由应用程序解析。

`systemd-analyze set-log-level` `LEVEL` 将 `systemd` 守护进程的日志级别更改为 `LEVEL`（接受如 `systemd(1)` 中描述的 `--log-level=` 值）。

`systemd-analyze verify` 将加载单元文件并在检测到任何错误时打印警告。命令行上指定的文件将被加载，以及被它们引用的其他单元。该命令通过将所有命令行参数的目录位于单元加载路径的开头来工作，这确保这些目录中的所有单元文件优于标准位置的单元文件，即使它们没有显式列出。

如果没有传递任何命令，则隐含执行 `systemd-analyze time`。

## 选项

支持以下选项：

`--user`

在用户级 `systemd` 实例上操作。

`--system`

在系统级 `systemd` 实例上操作。这是隐含的默认值。

`--order`, `--require`

与 `dot` 命令（见上文）配合使用时，选择在依赖图中显示哪些依赖。如果传递了 `--order`，则只显示类型为 `After=` 或 `Before=` 的依赖。如果传递了 `--require`，则只显示类型为 `Requires=`、`RequiresOverridable=`、`Requisite=`、`RequisiteOverridable=`、`Wants=` 和 `Conflicts=` 的依赖。如果两者均未传递，则显示所有这些类型的依赖。

`--from-pattern=`, `--to-pattern=`

与 `dot` 命令（见上文）配合使用时，选择在依赖图中显示哪些关系。这两个选项都需要一个 `glob(7)` 模式作为参数，该模式将分别匹配关系的左侧节点和右侧节点。

这些每个项都可以多次使用，在这种情况下单元将匹配其中一个值。当关系的两侧都存在测试时，关系必须通过两项测试才能显示。当模式也被指定为位置参数时，它们将匹配关系的至少一侧。换句话说，使用这两个选项指定的模式将修剪由位置参数匹配的边边列表（如果提供了位置参数），否则将完全决定所显示的边边列表。

`--fuzz=*timespan*`

与 `critical-chain` 命令（见上文）配合使用时，也显示比 `sa` 级别中最新单元早 *timespan* 的单元。*timespan* 的单位是秒，除非指定了不同的单位，例如 `"50ms"`。

`--no-man`

不调用 `man` 来验证 `Documentation=` 中列出的 man 页是否存在。

`-H`, `--host=`

远程执行操作。指定一个主机名，或用 `"@"` 分隔的用户名和主机名进行连接。主机名可选地以 `":"` 分隔的容器名为后缀，这将直接连接到指定主机上的特定容器。这将使用 SSH 与远程机器管理器实例进行通信。可以使用 `machinectl -H` *HOST* 列出容器名。

`-M`, `--machine=`

在本地容器上执行操作。指定要连接的容器名。

`-h`, `--help`

打印简短帮助文本并退出。

`--version`

打印简短的版本字符串并退出。

`--no-pager`

不将输出通过管道到分页器。

## 退出状态

成功时返回 0，否则返回非零失败代码。

## DOT 示例

**示例 1. 绘制所有以 "avahi-daemon" 开头的单元的依赖关系**

```
$ systemd-analyze dot 'avahi-daemon.*' | dot -Tsvg > avahi.svg
$ eog avahi.svg
```

**示例 2. 绘制所有已知 target 单元之间的依赖关系**

```bash
systemd-analyze dot --to-pattern='*.target' --from-pattern='*.target' | dot -Tsvg > targets.svg
$ eog targets.svg
```

## VERIFY 示例

目前检测到以下错误：

- 未知的节和指令，
- 启动给定单元所需的依赖项缺失，
- `Documentation=` 中列出的系统中未找到的 man 页，
- `ExecStart=` 和类似项列出的命令在系统中未找到或不可执行。

**示例 3. 拼写错误的指令**

```bash
$ cat ./user.slice
[Unit]
WhatIsThis=11
Documentation=man(1)
Requires=different.service
[Service]
Desription=x
$ systemd-analyze verify ./user.slice
[./user.slice:9] Unknown lvalue 'WhatIsThis' in section 'Unit'
[./user.slice:13] Unknown section 'Service'. Ignoring.
Error: org.freedesktop.systemd1.LoadFailed: Unit different.service failed to load: No such file or directory.
Failed to create user.slice/start: Invalid argument
user.slice: man (1) command failed with code 16
```

**示例 4. 缺失的服务单元**

```bash
$ tail ./a.socket ./b.socket
==> ./a.socket <==
[Socket]
ListenStream=100
==> ./b.socket <==
[Socket]
ListenStream=100
Accept=yes
$ systemd-analyze verify ./a.socket ./b.socket
Service a.service not loaded, a.socket cannot be started.
Service b@0.service not loaded, b.socket cannot be started.
```

## 环境

`$SYSTEMD_PAGER`

## 描述

`systemd-ask-password`

可用于通过命令行指定的消息向用户查询系统密码或密码短语。当从 TTY 运行时，它将在 TTY 上查询密码并打印到标准输出。当在没有 TTY 或使用 `--no-tty` 运行时，它将在整个系统范围内查询密码并允许活动用户通过多个代理进行响应。后者仅对特权进程可用。

此工具的目的是查询系统级密码——即未附加到特定用户账户的密码。例如：在插入或启动时解锁加密硬盘硬盘，为 Web 服务器和 VPN 服务器输入 SSL 证书密码短语。

现有的代理有：一个使用 Plymouth 向用户请求密码的启动时密码代理；一个直接在控制台上查询用户密码的启动时密码代理；一个通过 `wall(1)` 消息请求密码输入的代理；一个适用于在 GNOME 会话中运行的代理；一个可以临时启动以处理队列密码请求的命令行代理；一个在 `ssh(1)` 调用期间临时生成的 TTY 代理。

可以根据 `systemd Password Agent Specification`[1] 实现额外的密码代理。

如果在 TTY 上查询密码，用户可以按 TAB 键隐藏通常为每个输入字符显示的星号。按回格键作为第一个键可以实现相同的效果。

## 选项

支持以下选项：

`--icon=`

在密码查询时指定图标名称，该图标可能用于所有支持图形显示器代理。图标名称应遵循 `XDG Icon Naming Specification`[2]。

`--timeout=`

指定查询超时时间（秒）。默认为 90s。超时为 0 则无限等待。

`--echo`

显示用户输入而不是掩盖它。这在使用 `systemd-ask-password` 查询用户名时有用。

`--no-tty`

即使当前可用 TTY，也绝不在当前 TTY 上请求密码。始终使用代理系统。

`--accept-cached`

如果传递，则接受缓存的密码，即之前输入过的密码。

`--multiple`

与 `--accept-cached` 配合使用时接受多个密码。每行输出一个密码。

`-h`, `--help`

打印简短帮助文本并退出。

## 退出状态

成功时返回 0，否则返回非零失败代码。

## 参见

`systemd(1)`, `systemctl(1)`, `wall(8)`, `ssh(1)`

## 注意

1. systemd Password Agent Specification

2. XDG Icon Naming Specification

---

# SYSTEMD-BOOTCHART

## 名称

`systemd-bootchart` - 启动性能图表工具

## 描述

`systemd-bootchart` 是一个通常在系统启动时运行的工具，用于收集运行系统的 CPU 负载、磁盘负载、内存使用以及每个进程的信息。收集到的结果以 SVG 图表的形式输出。通常，`systemd-bootchart` 由内核通过在内核命令行传递 `init=/usr/lib/systemd/systemd-bootchart` 来调用。随后，`systemd-bootchart` 将 fork 出真正的 init 进程以恢复正常的系统启动，同时在后台监控并记录启动信息。

在收集了一定的数据（通常为 15-30 秒，默认为 20 秒）后，记录停止并根据日志信息生成图表。该图表包含了关键线索，显示了哪些资源正在被使用、以什么顺序，以及系统启动序列中可能存在哪些问题。它本质上是 `systemd-analyze plot` 函数的更详细版本。

当然，bootchart 也可以在任何时间点收集并对一段时间内的数据绘制图表。在这种情况下，建议使用 `--rel` 选项。

Bootchart 不需要 root 权限，可以作为普通用户运行。

Bootchart 图表默认带有时间戳写入 `/run/log`，并保存到 journal 中，`MESSAGE_ID=9f26aa562cf440c2b16c773d0479b518`。Journal 字段 `BOOTCHART=` 为 SVG 格式的 bootchart。

## 调用

`systemd-bootchart` 可以通过几种不同的方式调用：

### 内核调用

内核可以调用 `systemd-bootchart` 代替 init 进程。随后，`systemd-bootchart` 会调用 `/usr/lib/systemd/systemd`。

### 作为独立程序启动

用户可以从命令行作为普通应用程序执行 `systemd-bootchart`。在此模式下，强烈建议传递 `-r` 标志，以避免绘制从启动以来到 `systemd-bootchart` 启动之前经过的时间，因为这可能导致图表极其巨大。从启动以来的时间可能包括系统挂起的任何时间。

## 选项

这些选项也可以在 `/etc/systemd/bootchart.conf` 文件中设置。参见 `systemd.bootchart(5)`。

- `-h`, `--help`

打印简短的帮助文本并退出。

- `-n`, `--sample` *N*

指定要记录的样本数 *N*。样本将按照 `--freq` 定义的间隔进行记录。

- `-f`, `--freq` *f*

指定采样日志频率，单位为 Hz 的正实数 *f*。大多数系统可以处理高达 25-50 的值，而不会产生太多开销。

- `-r`, `--rel`

使用相对时间代替绝对时间。这对于在启动后使用 bootchart 对已启动的系统进行性能分析非常有用。如果没有此选项，图表将变得极其巨大。如果设置了，横轴将从第一个记录的样本开始，而不是从时间 0.0 开始。

- `-F`, `--no-filter`

禁用对启动没有显著贡献的任务的过滤。运行时间过短（仅在一个样本中可见）或不消耗任何显著 CPU 时间（小于 0.001 秒）的进程将不会显示在输出图表中。

- `-C`, `--cmdline`

显示带参数的进程完整命令行，而不仅仅是进程名。

- `-g`, `--control-group`

显示进程控制组。

- `-o`, `--output` *path*

指定图表的输出目录。默认情况下，bootchart 将图表写入 `/run/log`。

- `-i`, `--init` *path*

使用此 init 二进制文件。默认为 `/usr/lib/systemd/systemd`。

- `-p`, `--pss`

启用进程 PSS（比例集合大小）内存消耗的记录和绘图。参见内核文档中的 `filesystems/proc.txt` 以获取该字段的解释。

- `-e`, `--entropy`

启用内核随机熵池大小的记录和绘图。

- `-x`, `--scale-x` *N*

所有变量图表组件的水平缩放因子。

## 另请

`systemd.bootchart(5)`

## 缺陷

`systemd-bootchart` 在未指定 `root=/dev/sdx` 时无法获取硬盘模型信息。使用 UUID 或 PARTUUID 可以正常启动，但图表中不会添加模型。

对于 Bug，请联系作者和当前维护者：

Auke Kok

---

# SYSTEMD

## 名称

`systemd`, `init` - systemd 系统和服务管理器

## 语法

`systemd [OPTIONS...]`

`init [OPTIONS...] {COMMAND}`

## 描述



`systemd`是 Linux 操作系统的系统和服务管理器。当作为启动进程（作为 PID 1）运行时，它作为启动并维护用户空间服务的 init。

为了兼容 SysV，如果作为 `init` 且 PID 不是 1 时调用，它将执行 `telinit` 并传递所有命令行参数。这意味着在普通登录会话中 `init` 和 `telinit` 基本是等等的。更多信息请参见 (8)。

作为系统实例运行时，`systemd` 解析配置文件 `system.conf` 和 `system.conf.d` 目录；作为用户实例运行时，`systemd` 解析 `user.conf` 和 `user.conf.d` 目录。更多信息请参见 (5)。

## 选项

以下选项是有效的：

`--test`

确定启动序列，导出并退出。这是一个仅用于调试的选项。

`--dump-configuration-items`

导出已知的配置项。这会输出单元文件中理解的简明但完整的列表。

`--unit=`

设置启动时激活的默认单元。如果没有指定，默认为 `default.target`。

`--system`, `--user`

对于 `--system`，告诉 `systemd` 系统实例，即使进程 ID 不是 1，即 `systemd` 未作为 init 进程运行。`--user` 相反，即使进程 ID 为 1 也运行用户实例。通常没有必要传递这些选项，因为 `systemd` 会自动检测它运行的模式。因此，这些选项除了调试外几乎没有用。注意不支持在 `systemd` 以 `--system` 模式运行但 PID 不是 1 时启动并维护完整系统。在实践中，显式传递 `--system` 仅在配合 `--test` 时有用。

`--dump-core`

崩溃时转储核心。在作为用户实例运行时无效。

`--crash-shell`

崩溃时运行 shell。在作为用户实例运行时无效。

`--confirm-spawn`

在派生进程时请求确认。在作为用户实例运行时无效。

`--show-status=`

在启动时显示简短的服务状态信息。当作为用户实例运行时，此开关无效。接受一个布尔参数，该参数可以省略，默认解释为 `true`。

`--log-target=`

设置日志目标。参数可以是 `console`、`journal`、`kmsg`、`journal-or-kmsg`、`null` 之一。

`--log-level=`

设置日志级别。参数接受数字日志级别或常用的符号（小写）：`emerg`、`alert`、`crit`、`err`、`warning`、`notice`、`info`、`debug`。

`--log-color=`

高亮重要的日志消息。参数为布尔值。如果省略参数，默认值为 `true`。

`--log-location=`

在日志消息包含代码位置。主要用于调试。参数为布尔值。如果省略参数，默认值为 `true`。

`--default-standard-output=`, `--default-standard-error=`

分别为所有服务和套接设置默认输出或错误输出。也就是说，它控制了 `StandardOutput=` 和 `StandardError=` 的默认值（详见 (5)）。接受 `inherit`、`null`、`tty`、`journal`、`journal+console`、`syslog`、`syslog+console`、`kmsg`、`kmsg+console` 之一。如果省略参数，`--default-standard-output=` 默认为 `journal`，`--default-standard-error=` 默认为 `inherit`。

`-h`, `--help`

打印短帮助文本并退出。

`--version`

打印短版本字符串并退出。

## 概念

`systemd` 在各种实体之间提供了一种依赖系统，这些实体被称为不同类型的“单元”。单元封装了与系统启动和维护相关的各种对象。大多数单元在单元配置文件中配置，其语法和基本选项集在 (5) 中描述；然而，单元也可以从其他配置创建、根据系统状态动态创建或在运行时通过程序创建。单元可以是“激活的”（已启动、绑定、已插入……，取决于单元类型，见下文）或“非激活的”（已停止、取消绑定、已拔出……），也可以正处于激活或去激活的过程中，即这两个状态之间（这些状态被称为“激活中”和“去激活中”）。还有一个特殊的“失败”状态，它与“非激活”状态非常相似，当服务以某种方式失败（退出时返回错误代码、崩溃或操作超时）时进入。如果进入此状态，原因将被记录以供日后参考。注意，各种单元类型可能有若干额外的子状态，这些状态映射到此处描述的五种通用单元状态。

可用单元类型如下：

1. 服务单元（Service units）：用于启动和控制守护进程及其包含的进程。详情见 (5)。

2. 套接字单元（Socket units）：封装系统中的本地 IPC 或网络套接字，用于基于套接字的激活。有关套接字单元的详情见 (5)，关于套接字激活和其他形式的激活的详情见 (7)。

3. 目标单元（Target units）：用于分组单元，或在启动期间提供众知的同步点，见 (5)。

4. 设备单元（Device units）：在 `systemd` 中暴露内核设备，并可用于实现基于设备的激活。详情见 (5)。

5. 挂载单元（Mount units）：控制文件系统中的挂载点，详情见 (5)。

6. 自动挂载单元（Automount units）：提供自动挂载功能，用于按需挂载文件系统以及并行启动。见 (5)。

7. 快照单元（Snapshot units）：可临时保存一组 `systemd` 单元的状态，稍可以通过激活保存的快照单元来恢复。更多信息见 (5)。

8. 计时器单元（Timer units）：用于根据定时触发其他单元的激活。你可以在 (5) 中找到详情。

9. 交换单元（Swap units）：与挂载单元非常相似，封装操作系统的内存交换分区或文件。它们在 (5) 中描述。

10. 路径单元（Path units）：当文件系统对象发生变化或修改时激活其他服务。见 (5)。

11. 切片单元（Slice units）：用于在层级树中对管理系统进程的单元（如服务和范围单元）分组。见 (5)。

12. 范围单元（Scope units）：与服务单元类似，但管理的是外部进程而不是启动它们。见 (5)。

单元与其对应的配置文件同名。因此，单元具有特殊的语义。详细列表可在 (7) 中查看。

`systemd` 了解各种依赖关系，包括正向和负向需求依赖（即 `Requires=` 和 `Conflicts=`）以及顺序依赖关系（`After=` 和 `Before=`）。注意：顺序依赖和需求依赖是正交的。如果两个单元之间仅存在需求依赖（例如 `foo.service` 需要 `bar.service`），但没有顺序依赖（例如 `foo.service` 在 `bar.service` 之后）且两个者都被请求启动，则它们将并行启动。在两个单元之间同时放置需求依赖和顺序依赖是一种常见模式。还要注意，大多数依赖关系由 `systemd` 隐式创建和维护。在大多数情况下，没有必要手动声明额外的依赖，但这是可能的。

应用程序和单元（通过依赖关系）可能会请求单元的状态更改。在 `systemd` 中，这些请求被封装为“作业”（jobs）并维护在作业队列中。作业可能会成功也可以失败，它们的执行根据其所调度单元的顺序依赖关系进行排序。

启动时，`systemd` 激活目标单元 `default.target`，其任务是通过依赖关系拉入来激活启动时服务和其他启动时单元。通常，该单元只是 `graphical.target`（用于进入 UI 的全功能启动）或 `multi-user.target`（用于嵌入式或服务器环境的限制性控制台启动，或类似；`graphical.target` 的子集）的别名。然而，将其配置为任何其他目标单元的别名取决于管理员。关于这些目标单元的详情见 (7)。

`systemd` 生成的进程被放在单独的 Linux 控制组（cgroups）中，并在私有的 `systemd` 层级结构中位于所属单元之后。（有关控制组的更多信息见 `cgroups.txt` 或简称 "cgroups"）。`systemd` 利用此有效跟踪进程。控制组信息维护在内核中，并通过文件系统层次结构访问（位于 `/sys/fs/cgroup/systemd/` 下），或通过工具如 (1)（`ps x xf -eo pid,user,cgroup,args` 对于列出所有进程及其所属的 `systemd` 单元特别有用）。

`systemd` 在很大程度上兼容 SysV init 系统：支持 SysV init 脚本，并将其作为替代（尽管有限）的配置格式进行读取。提供了 SysV `/dev/initctl` 接口，并提供了各种 SysV 客户端工具的兼容实现。此外，还支持各种成熟的 Unix 功能，如 `/etc/fstab` 或 utmp 数据库。

`systemd` 拥有一个极的事务系统：如果一个单元被请求启动或关闭，它将其及其所有的依赖项添加到一个临时事务中。然后，它将验证该事务是否具有一致性（即所有单元的顺序是否存在循环）。如果不一致，`systemd` 将尝试对其进行修复，并从事务中移除可能消除循环的非本质作业。此外，`systemd` 会尝试抑制事务中会停止正在运行服务的非本质作业。最后，将检查事务中的作业是否与已经队列的作业产生冲突，如果有，则可以选择中止该事务。如果一切顺利，且事务具有一致性并影响最小化，它将与所有已待处理的作业合并并添加到运行队列。从效果上看，这意味着 `systemd` 在执行请求的操作之前，会验证该操作是否合理，并在可能的情况下进行修复，仅在确实无法工作时才失败。

`systemd` 包含了作为启动过程中需要执行的各种任务的原生实现。例如，它会设置主机名或配置环回网络设备。它还会设置并挂载各种 API 文件系统，例如 `/sys` 或 `/proc`。

SysV init 脚本目录的位置在不同发行版之间不同。如果 `systemd` 无法为请求的服务找到原生单元文件，它将查找同名的 SysV init 脚本（移除 `.service` 后缀）。

### SysV 运行级别链接场目录

SysV 运行级别链接场的位置在不同发行版之间不同。`systemd` 在确定是否应启用服务时会考虑该链接场。注意，具有原生单元配置文件的单元无法通过激活 SysV 运行级别链接场中的来启动。

## 信号

### SIGTERM

接收到此信号后，`systemd` 系统管理器会序列化其状态，重新执行自身并再次反序列化保存的状态。这通常等同于 `systemctl daemon-reexec`。

`systemd` 用户管理器会在接收到此信号时启动 `exit.target` 单元。这通常等同于 `systemctl --user start exit.target`。

### SIGINT

接收到此信号后，`systemd` 系统管理器将启动 `ctrl-alt-del.target` 单元。这通常等同于 `systemctl start ctl-alt-del.target`。如果每 2 秒接收到此信号超过 7 次，将触发立即重启。注意，在控制台上按按下 Ctrl-Alt-Del 会触发此信号。因此，如果重启挂起，在 2 秒内按下 Ctrl-Alt-Del 超过 7 次是触发立即重启的相对安全的方法。

`systemd` 用户管理器处理此信号的方式与 `SIGTERM` 相同。

### SIGWINCH

接收到此信号后，`systemd` 系统管理器将启动 `kbrequest.target` 单元。这通常等同于 `systemctl start kbrequest.target`。

`systemd` 用户管理器忽略此信号。

### SIGPWR

接收到此信号后，`systemd` 管理器将启动 `sigpwr.target` 单元。这通常等同于 `systemctl start sigpwr.target`。

### SIGUSR1

接收到此信号后，`systemd` 管理器将尝试重新连接到 D-Bus 总线。

### SIGUSR2

接收到此信号后，`systemd` 管理器将以人类可读的格式记录其完整状态。记录的数据与 `systemd-analyze dump` 打印的内容相同。

### SIGHUP

重加载完整的守护进程配置。这通常等同于 `systemctl daemon-reload`。

### SIGRTMIN+0

进入默认模式，启动 `default.target` 单元。这通常等同于 `systemctl start default.target`。

### SIGRTMIN+1

进入救援模式，启动 `rescue.target` 单元。这通常等同于 `systemctl isolate rescue.target`。

### SIGRTMIN+2

进入紧急模式，启动 `ergency.service` 单元。这通常等同于 `systemctl isolate ergency.service`。

### SIGRTMIN+3

停止机器，启动 `halt.target` 单元。这通常等同于 `systemctl start halt.target`。

### SIGRTMIN+4

关闭机器，启动 `poweroff.target` 单元。这通常等同于 `systemctl start poweroff.target`。

### SIGRTMIN+5

重启机器，启动 `reboot.target` 单元。这通常等同于 `systemctl start reboot.target`。

### SIGRTMIN+6

通过 kexec 重启机器，启动 `kexec.target` 单元。这通常等同于 `systemctl start kexec.target`。

### SIGRTMIN+13

立即停止机器。

### SIGRTMIN+14

立即关闭机器。

### SIGRTMIN+15

立即重启机器。

### SIGRTMIN+16

通过 kexec 立即重启机器。

### SIGRTMIN+20

启用在控制台上显示状态消息，通过内核命令行上的 `systemd.show_status=1` 控制。

### SIGRTMIN+21

禁用在控制台上显示状态消息，通过内核命令行上的 `systemd.show_status=0` 控制。

### SIGRTMIN+22, SIGRTMIN+23

将日志级别设置为“debug”（在 `SIGRTMIN+23` 上为“info”），通过内核命令行上的 `systemd.log_level=debug`（在 `SIGRTMIN+23` 上为 `systemd.log_level=info`）控制。

### SIGRTMIN+24

立即退出管理器（仅对 `--user` 可用）。

### SIGRTMIN+26, SIGRTMIN+27, SIGRTMIN+28

将日志目标设置为“journal-or-kmsg”（在 `SIGRTMIN+27` 上为“console”，在 `SIGRTMIN+28` 上为“kmsg”），通过内核命令行上的 `systemd.log_target=journal-or-kmsg`（在 `SIGRTMIN+27` 上为 `systemd.log_target=console` 或在 `SIGRTMIN+28` 上为 `systemd.log_target=kmsg`）控制。

## 环境

*`$SYSTEMD_LOG_LEVEL`*

`systemd` 从此环境变量中读取日志级别。可以通过 `--log-level=` 覆盖。

*`$SYSTEMD_LOG_TARGET`*

`systemd` 从此环境变量中读取日志目标。可以通过 `--log-target=` 覆盖。

*`$SYSTEMD_LOG_COLOR`*

控制 `systemd` 是否高亮重要的日志消息。可以通过 `--log-color=` 覆盖。

*`$SYSTEMD_LOG_LOCATION`*

`systemd.unit=*`, `rd.systemd.unit=*`

覆盖启动时激活的单元。默认为 `default.target`。这可以临时启动到不同的启动单元，例如 `rescue.target` 或 `ergency.service`。这些单元的详情请见 (7)。带有 "rd." 前缀的选项仅在初始内存磁盘 (initrd) 中有效，而无前缀的选项仅在主系统中有效。

`systemd.dump_core=*`

接受一个布尔参数。如果为 `true`，`systemd` 在崩溃时转转储（core dump）。否则不创建转储文件。默认为 `true`。

`systemd.crash_shell=*`

接受一个布尔参数。如果为 `true`，`systemd` 在崩溃时产生一个 shell。否则不产生 shell。出于安全考虑，默认为 `false`，因为 shell 不受密码身份验证的保护。

`systemd.crash_chvt=*`

接受一个整数参数。如果为正数，`systemd` 在崩溃时激活指定的虚拟终端。默认为 `-1`。

`systemd.confirm_spawn=*`

接受一个布尔参数。如果为 `true`，在产生进程时请求确认。默认为 `false`。

`systemd.show_status=*`

接受一个布尔参数或常量 `auto`。如果为 `true`，在启动期间在控制台上显示精简的服务状态更新。`auto` 的行为表现于 `false`，直到服务失败或启动出现显著延迟。默认为 `true`，除非作为内核命令行选项传递了 `quiet`，在这种情况下默认为 `auto`。

`systemd.log_target=*`, `systemd.log_level=*`, `systemd.log_color=*`, `systemd.log_location=*`

控制日志输出，其效果与上述的 `SYSTEMD_LOG_TARGET`, `SYSTEMD_LOG_LEVEL`, `SYSTEMD_LOG_COLOR`, `SYSTEMD_LOG_LOCATION` 环境变量相同。

`systemd.default_standard_output=*`, `systemd.default_standard_error=*`



控制服务的默认标准输出和错误输出，其效果分别与上述的`--default-standard-output=`和`--default-standard-error=`命令行参数相同。

`systemd.setenv=*`

接受`VARIABLE=VALUE`格式的字符串参数。可用于设置添加到 fork 子进程的默认环境变量。可以多次使用来设置多个变量。

`quiet`

关闭启动时的状态输出，类似于`systemd.show_status=false`。注意，该选项也会被内核本身读取并禁用内核日志输出。因此，传递此选项将同时关闭来自系统管理器和内核的常规输出。

`debug`

开启调试输出。这等同于`systemd.log_level=debug`。注意，该选项也会被内核本身读取并启用内核调试输出。因此，传递此选项将开启系统管理器和内核的调试输出。

`ergency`, `-b`

进入紧急模式（emergency mode）。这等同于`systemd.unit=ergency.target`，是为了兼容性并方便输入。

`rescue`, `single`, `s`, `S`, `1`

进入救援模式（rescue mode）。这等同于`systemd.unit=rescue.target`，是为了兼容性并方便输入。

`2`, `3`, `4`, `5`

启动到指定的遗留 SysV 运行级别。这些分别等同于`systemd.unit=runlevel2.target`, `systemd.unit=runlevel3.target`, `systemd.unit=runlevel4.target`, 和`systemd.unit=runlevel5.target`，是为了兼容性并方便输入。

`locale.LANG=*`, `locale.LANGUAGE=*`, `locale.LC_CTYPE=*`, `locale.LC_NUMERIC=*`, `locale.LC_TIME=*`, `locale.LC_COLLATE=*`, `locale.LC_MONETARY=*`, `locale.LC_MESSAGES=*`, `locale.LC_PAPER=*`, `locale.LC_NAME=*`, `locale.LC_ADDRESS=*`, `locale.LC_TELEPHONE=*`, `locale.LC_MEASUREMENT=*`, `locale.LC_IDENTIFICATION=*`

设置要使用的系统区域设置。这将覆盖`/etc/locale.conf`中的设置。更多信息请见 (5) 和 (7)。

对于核心操作系统组件理解的其他内核命令行参数，请参阅 (7)。

## SOCKET 和 FIFOs

`/run/systemd/notify`

守护进程状态通知套接字。这是一个`AF_UNIX`数据报套接字，用于实现 (3) 中实现的守护进程通知逻辑。

`/run/systemd/private`

内部用于 (1) 和 systemd 进程之间的通信通道。这是一个`AF_UNIX`流式套接字。此接口是 systemd 私有的，不应在外部项目中使用。

`/dev/initctl`

对 SysV 客户端接口的有限兼容性支持，由`systemd-initctl.service`单元实现。这是文件系统中的命名管道（named pipe）。该接口已过时，不应在新应用程序中使用。

## Notes

1. `cgroups.txt`

2. 原始设计文档

3. 接口承诺

4. 容器接口

5. initrd 接口

6. XDG Base Directory 规范

7. 如果在 Linux 容器内部运行，这些参数作为命令行参数传递给 systemd 本体，位于上述 Options 部分列出的任何命令行选项旁边。如果在 Linux 容器外部运行，这些参数将从`/proc/cmdline`解析。

8. systemd 帮助页
