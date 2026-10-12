

/var/spool/cron L
/var/spool/mqueue L
/var/spool/mail L
!/var/lock
!/var/tripwire

# GENE: /sbin 包含单用户模式下至关重要的二进制文件
/sbin R

# 其他关键目录
/usr/etc R

# 非标准目录
=/proc E
=/tmp

由于此类配置文件的语法在 tw.config 手册页中已有详细说明，此处不再讨论文件语法。

在创建数据库文件之前，请务必确定当前系统上的文件未被不法分子篡改。创建该数据库的理想时机是您的新系统尚未连接到互联网或任何其他网络时。在确定文件未被动过后，将目录切换到 /usr/local/bin/tw 并按如下方式运行 Tripwire：

```
./tripwire -initialize
```

创建数据库后，请迅速将其移至只读介质（如 CD-ROM，如果可能）。您也可以打印整个数据库内容，以便在必要时手动核对信息。创建数据库后，您还需要保护 Tripwire 文件。

## 保护 Tripwire 本身

不法分子可能会修改 Tripwire 二进制文件或配置文件以掩盖其行踪。因此，请运行 siggen 实用程序为这些文件创建一组签名。要为 tripwire 二进制文件生成签名，请从 `/usr/local/bin/tw` 目录运行以下命令：

```
./siggen tripwire
```

您将在屏幕上看到类似如下内容：

```
sig0: nullsig : 0
sig1: md5 : 0f17OytJSfosJXBXCXbZxuo
sig2: snefru : 2U0lmpiKyb5tKDJ0206G
sig3: crc32 : 08arMS
sig4: crc16 : 000dFd
sig5: md4 : 2DDym8m3JGRyRy.W5uwPzX4
sig6: md2 : 3NTKpom:A5ynvixpGLmK.O
sig7: sha : 4AGzq5nq16DM7D6pRartMk49wGX
sig8: haval : 07MQyp6T4EERZw1mypzLkw
sig9: nullsig : 0
```

您可以通过重定向将签名保存在文件中。同时打印签名，别忘了为 siggen 实用程序本身也生成签名。如果您怀疑 Tripwire 未按预期工作，请在这些文件上各运行一次 siggen 实用程序并比对签名。如果有任何不匹配，请勿信任这些文件 —— 用新副本替换它们，并调查差异产生的原因。

## 运行 Tripwire 检测完整性问题

您可以通过两种方式运行 Tripwire：

- **交互模式** —— 每当 Tripwire 遇到已添加、删除或更改的文件或目录时，它会询问您是否更新数据库。
- **作为 cron 作业** —— 通过创建一个小脚本，如 **清单 15-7** 所示。

### 清单 15-7：tripwire.sh 文件

```
#!/bin/sh
/usr/local/bin/tw/tripwire -q | /bin/mail -s "Security report by Tripwire" your@email
```

`-q` 允许 tripwire 安静运行并通过邮件将报告发送到 your@email 地址。您可以将此类脚本放入 `/etc/cron.daily` 目录，使其每日运行。您的文件如有任何更改，将每日报告给您。

## 更新 Tripwire 数据库

要更新整个 Tripwire 数据库，请运行

```bash
./tripwire -update
```

或者，如果您想添加一个新目录及其下的所有文件和子目录，请运行

```bash
./tripwire -update /some/dir
```

更新现有的已修改目录或其文件时，也使用此命令。如果您只想添加或更新单个文件，请使用以下语法：

```bash
./tripwire -update newfile
```

## 在速度与更高安全级别之间权衡

Tripwire 采用多种签名算法，例如空签名、来自 RSA Data Security, Inc. 的消息摘要算法 (MD5)、来自施乐的安全哈希函数 Snefru、循环冗余校验 (CRC-32)、CRC-16、MD4、MD2、安全哈希算法 (SHA) 和 Haval。

在大型文件系统上对每个文件执行所有这些算法会消耗大量 CPU 资源并耗费很长时间。为了减轻系统负载或加快检查过程，您可以指示 Tripwire 忽略其中一种或多种算法。例如，

```bash
./tripwire -i 1
```

指示 Tripwire 忽略第一种算法 MD5。只要您知道算法对应的编号，就可以使用 `-i` 命令行选项忽略任意算法。编号到算法的映射如表 15-9 所示。

### 表 15-9：Tripwire 算法

| -i 选项 | 签名算法 |
|---|---|
| -i 0 | 空签名 |
| -i 1 | MD5 |
| -i 2 | Snefru |
| -i 3 | CRC-32 |
| -i 4 | CRC-16 |
| -i 5 | MD4 |
| -i 6 | MD2 |
| -i 7 | SHA |
| -i 8 | Haval |
| -i 9 | 空签名（保留供将来使用） |

要在不进行任何签名完整性检查的情况下查找新增或丢失的文件，请运行

```bash
./tripwire -i all
```

## 扮演反方辩手

许多经验丰富的管理员认为，仅采取预防措施并希望坏事永不发生，无异于自寻死路。他们认为，要获得真正的安全感，系统必须经受实际考验。换句话说，为什么不在不法分子发动攻击之前，自己先攻击自己的安全基础设施？通过扮演潜在攻击者，您可能在*不友好*的攻击者发现您之前，自行揭示潜在漏洞。幸运的是，如今您无需费太大力气就能扮演不法分子。现有工具可以帮助您轻松承担这一角色。本节讨论一些常用工具。

### 破解自己的密码

弱密码通常是各年龄段攻击者的易攻击目标。不法分子一旦非法获取您的 `/etc/passwd` 文件（如果您尚未使用影子密码），就会将其输入密码破解程序以揭示您的秘密 —— 弱密码。因此，在黑客破解之前先破解自己的密码，有助于消除弱密码。

### 密码如何被破解

理解加密学神秘细节的最佳方法是举个例子。如果您在系统上创建一个用户名为 bob、密码为 umbrella 的新用户，您将在 /etc/passwd 文件中看到类似如下的一行：

```
bob:XoAlxlaie wp8s:Red Hat Linux User:/home/bob:/bin/bash
```

该行可能不完全相同，但关键是您将得到一行包含 bob 加密密码的记录。加密密码是一个由 crypt() 函数创建的 13 字符字符串，如下所示：

```
加密密码 = crypt("umbrella", "Xo", salt)
```

salt 是从 `[a-zA-Z0-9./]` 集合中选取的两字符字符串。该字符串用于以 4,096 种不同方式之一影响加密算法。salt 值存储在加密密码的前两个字符中。例如，**XoAlxlaie wp8s** 中的 Xo 是 umbrella 的加密密码，使用的 salt 值为 Xo。没有已知方法能从加密版本中恢复原始密码，因为加密算法是单向的。然而，如果已知加密密码，则可以编写程序利用两字符的 salt 值，用该 salt 加密大量字典单词。如果密码恰好是字典中的单词（如本例），它将被加 salt 并找到匹配项。换句话说，当您知道 bob 密码的 salt 值为 Xo 时，可以使用该 salt 编写程序执行以下操作：

```
加密密码 = crypt(每个单词, "Xo")
```

当该程序选中单词 "umbrella" 时，加密密码将与 /etc/passwd 中存储的相同。糟糕，bob 的密码刚被破解！现在程序知道创建密码使用的是哪个单词。这是破解软件工作原理的简化解释。但请记住，现在的破解软件先进得多，随着计算机硬件越来越强大，破解密码变得更容易、更快。

