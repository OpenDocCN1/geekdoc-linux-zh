
## 针对用户

这些目录的所有者必须是作为 TCFS 目录使用它们的用户。如果 `/work` 的属主是 root，那么 root 将执行以下命令：

```bash
# mkdir /work/mary
# chown mary.mary /work/mary
```

以为用户 mary 提供一个工作目录。

现在，root 用户必须按照示例 15-14 所示将 mary 添加到 TCFS 用户数据库中。每个使用 TCFS 资源的用户都必须以这种方式添加，并且只有 root 可以执行 `/usr/local/sbin/tcfsadduser` 命令。

### 示例 15-14 将用户添加到 TCFS 用户数据库

```bash
# /usr/local/sbin/tcfsadduser
Username to add to TCFS database: mary
Ok
#
```

移除用户的过程与此类似，如示例 15-15 所示。这也是一个仅限 root 执行的命令。

### 示例 15-15 移除 TCFS 用户

```bash
# /usr/local/sbin/tcfsrmuser
Username to remove from TCFS database: bill
Ok
#
```

用户数据库维护在文件 `/etc/tcfspwdb` 中，该文件还保存着用户的加密密钥。

## 客户端侧

一旦设置了适当的属性，你就可以挂载该资源。在此示例中，我们假设有一个本地挂载目录 `/mnt/safe`。如果要在本地访问该资源，则应使用以下命令：

```bash
# mount -t tcfs localhost:/work /mnt/safe
```

如果是远程资源，则如下示例所示：

```bash
[root@pluto]# mount -t tcfs underdog:/work /mnt/safe
```

资源现已可用，TCFS 用户可以开始使用它。

## TCFS 扩展属性

首先，我们需要设置适当的属性，以确保工作目录中文件的加密。当按照第 420 页步骤 7 的描述安装替换的 chattr 命令后，会有两个属性 `x` 和 `g` 被添加到 chattr 命令中。当 `x` 属性应用于文件时，表示该文件将被加密。如果将 `x` 属性应用于目录，则该目录中的所有文件和子目录都会被加密。`g` 属性用于指示该文件或目录对 TCFS 组可访问（加密和解密）。TCFS 组在第 429 页的 TCFS 组章节中有详细介绍。

用户 mary 可以通过使用 chattr 命令来设置其拥有的文件或目录的 `x` 属性，例如：

```bash
[mary@underdog]$ chattr +X /mnt/safe/mary
```

这将导致在 `/mnt/safe/mary` 被挂载为 TCFS 资源后，在该目录下创建的所有文件和子目录都会进行加密。请注意，该属性是在已挂载的目录上设置的，而不是在真实目录上设置。这允许 TCFS 识别哪些文件需要加密。

不幸的是，替换的 chattr(1) man 手册页没有描述 `x` 或 `g` 属性。

### 设置加密目录

为了让 Mary 能在 TCFS 资源中创建加密的文件和目录，她最初必须创建一个加密密钥，随后将该密钥推入内核模块。第一步如示例 15-16 所示。在密码提示处，mary 必须提供她的登录密码。

**示例 15-16 初始生成 TCFS 加密密钥**

```bash
[mary@topcat]$ /usr/local/bin/tcffgenkey
password: 
Please, press 10 random keys, so we can create a new key for you:
press 10 keys:************
Ok.
Key successfully generated.
[mary@topcat]$
```

现在 mary 已经拥有了一个密钥，她可以按照示例 15-17 所示将其推入内核模块。同样地，mary 必须在密码提示处提供她的登录密码。

**示例 15-17 推入密钥**

```bash
[mary@topcat]$ /usr/local/bin/tcffpushkey
password: 
Ok
[mary@topcat]$
```

现在，mary 在 `/mnt/safe/mary` 中创建的任何文件和目录都将在资源 `underdog:/work/mary` 上被加密。只有 mary 能够通过 `/mnt/safe/mary` 看到明文。以下示例说明了这种行为。

在示例 15-18 中，用户 mary 在 pluto 上的明文目录 `/mnt/safe/mary` 中创建一个名为 `secret` 的文件。

**示例 15-18 在 TCFS 目录中创建文件**

```bash
[mary@pluto]$ echo "Really secret stuff" > /mnt/safe/mary/secret
[mary@pluto]$ cat /mnt/safe/mary/secret
Really secret stuff
[mary@pluto]$
```

实际上，位于 underdog 的 `/work/mary` 下的文件及其内容是加密的，如示例 15-19 所示。

**示例 15-19 实际文件及其内容已被加密**

```bash
[mary@underdog]$ ls /work/mary
MwGldWrg4CsA=
[mary@underdog]$ cat /work/mary/MwGldWrg4CsA=
“,0$E6&@IO@]‘û(mary@topcat]$
```

即使是 root 用户也无法访问 Mary 的加密文件，如示例 15-20 所示。

**示例 15-20 只有用户 mary 可以访问该文件**

```bash
[root@pluto]$ cd /mnt/safe/mary
[root@pluto]$ ls
ls: .: Permission denied
[root@pluto]$
```

## 顺便提一下...

这里提供的步骤很容易被 root 用于敏感目录，例如 `/var/log`。虽然这可能很有吸引力，但每当系统启动并运行时，`/var/log` 都需要被挂载为 TCFS。这意味着每次重启时都必须提供 root 密码，同时也意味着如果 root 权限被攻陷，则不会提供保护。然而，这将完全消除除 root 以外用户对日志文件的检查。

## TCFS 组

与描述 TCFS 用户的方式非常相似，可以使用 `/usr/local/sbin/tcfsaddgrp` 命令创建 TCFS 组，并使用 `/usr/local/sbin/tcfsmgrp` 命令移除它们。TCFS 组名必须与 `/etc/group` 中的名称匹配。TCFS 组可以配置任意数量的用户，也可以设置要求最少一定数量的用户将其密钥推入内核模块后，才允许访问组文件和目录。

## TCFS 密钥管理

TCFS 的密钥管理至多只是简陋的。用户 mary 可以使用 `tcfsviewkey -k` 命令查看她的密钥，如示例 15-21 所示。她必须提供密码才能查看密钥。

**示例 15-21 查看用户的密钥**

```bash
[mary@topcat]$ ./usr/local/bin/tcfviewkey -k
password:
TCFS key: 08aaxA#VeWDAwmDozxFQBA=
[mary@topcat]$
```

她还可以确定她的密钥是否已推入内核。**示例 15-22** 显示了密钥在内核中的情况，表明 Mary 之前执行过 `tcfsputkey`。

**示例 15-22 验证密钥在内核中**

```bash
[mary@topcat]$ ./usr/local/bin/tcfviewkey -c
TCFS counter: 1
[mary@topcat]$
```

不幸的是，密钥本身不容易被更改。`tcfsgenkey` 的源代码中有迹象表明即将推出 `-c` 标志，这将允许通过该命令更改密钥。然而，截至本文撰写时，更改密钥的唯一方法是使用 `tcfsrmuser` 命令移除用户，然后使用 `tcfsadduser` 命令重新添加该用户。这些命令必须由 root 执行。完成后，用户可以使用 `tcfsgenkey` 生成新密钥。使用这些步骤，用户可以生成多个密钥。用户必须记录通过 `tcfsviewkey` 生成的 TCFS 密钥，如**示例 15-21**所示。随后可以使用 `tcfsputkey -k` 将每个密钥推入内核，如**示例 15-23**所示。用于加密文件的密钥必须以此方式推入内核，以便对该文件进行解密。

**示例 15-23 将特定密钥推入内核**

```bash
[mary@topcat]$ ./usr/local/bin/tcfsputkey -k 08aaxA#VeWDAwmDozxFQBA=
password:
Ok
[mary@topcat]$
```

关于 TCFS 密钥生成和使用的根本问题在于，密钥与用户的密码绑定。因此，如果用户的密码被攻陷，那么当前密钥（且仅当前密钥）也会随之被攻陷。如果使用过其他密钥，则必须知道这些密钥才能解密用它们加密的任何文件。这意味着，虽然使用多个密钥更安全，但需要手动密钥管理或自定义软件。

## TCFS 的漏洞

与 CFS 类似，有时明文会存储在 RAM 或文件系统缓存中。与 CFS 不同的是，这种情况仅在内核空间中发生，且持续时间较短。在这方面，TCFS 比 CFS 更安全。

