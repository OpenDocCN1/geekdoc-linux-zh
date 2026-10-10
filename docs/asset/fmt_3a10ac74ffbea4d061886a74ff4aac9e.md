
```
$ sprof -p libdemo.so.1 $LD_PROFILE_OUTPUT/libdemo.so.1.profile
Flat
profile: Each sample counts as 0.01 seconds.
% cumulative       self       self    total
               time      time      time     calls  us/call  us/call
   na      60.00   0.06   0.06       100  600.00 consuCpu1
   40.00   0.10   0.04      1000   40.00 consuCpu2
   0.00   0.10   0.00         1    0.00 x1
   0.00   0.10   0.00         1    0.00 x2
```

` sprof -q` 选项生成调用图：

```
$ sprof -q libdemo.so.1 $LD_PROFILE_OUTPUT/libdemo.so.1.profile
  index % time     self  children    called     name
  0.00 0.00         100/100 x1 [1] [0]
  100.0 0.00       100 consuCpu1 [0]
------------------------
  0.00 0.00         1/1 <UNKNOWN> [1]
  0.00 0.00       100/100 consuCpu1 [0]
------------------------
  0.00 0.00      1000/1000 x2 [3] [2]
  0.00 0.00      1000 consuCpu2 [2]
------------------------
  0.00 0.00         1/1 <UNKNOWN> [3]
  0.00 0.00      1000/1000 consuCpu2 [2]
------------------------
```

在上方和下方，“`<UNKNOWN>`”字符串表示位于受配置文件监控对象之外的标识符（在本示例中，这些是 `main()` 的实例）。

` sprof -c` 选项生成调用对及其出现次数的列表：

```
$ sprof -c libdemo.so.1 $LD_PROFILE_OUTPUT/libdemo.so.1.profile
<UNKNOWN> x1 1
x1 consuCpu1 100
<UNKNOWN> x2 1
x2 consuCpu2 1000
```

### 参见

(1), (1), (8)

### 结语

本页是 Linux *man-pages* 项目版本 4.00 的一部分。有关该项目的说明、报告错误的信息以及本页的最新版本，请参阅

### SSH-ADD

### 名称

`ssh-add` - 将私钥身份添加到认证代理

### 概要

`ssh-add` `[-cDdkLlXx]` `[-E` *fingerprint_hash*` ]` `[-t` *life*`]` [`*file*`...]`  

`ssh-add` `-s` *pkcs11*  

`ssh-add` `-e` *pkcs11*

### 描述

`ssh-add` 将私钥身份添加到认证代理 `ssh-agent(1)`。在没有参数运行时，它会添加文件 `~/.ssh/id_rsa` `~/.ssh/id_dsa` `~/.ssh/id_ecdsa` `~/.ssh/id_ed25519` 和 `~/.ssh/identity`。加载私钥后，`ssh-add` 将尝试从文件加载相应的证书信息：该文件名是通过在私钥文件名称后追加 `-cert.pub` 获得的。可以在命令行上提供替代的文件名。

如果任何文件需要密码短语，`ssh-add` 会向用户询问密码短语。密码短语从用户的 tty 读取。如果提供了多个身份文件，`ssh-add` 会重试最后一次使用的密码短语。

认证代理必须正在运行，并且环境变量 `SSH_AUTH_SOCK` 必须包含其套接字名称，`ssh-add` 才能正常工作。

选项如下：

- `-c`

  - 指示添加的身份在用于认证之前应经过确认。确认由 `ssh-askpass(1)` 执行。成功的确认由 `ssh-askpass(1)` 的零退出状态表示，而不是请求者输入文本。

- `-D`

  - 从代理中删除所有身份。

- `-d`

  - 不添加身份，而是从代理中删除身份。如果未运行 `ssh-add` 参数，默认身份及其相应证书的密钥将被删除。否则，参数列表将被解释为公钥文件路径列表，以指定要从代理中删除的密钥和证书。如果在指定路径未找到公钥，`ssh-add` 将追加 `.pub` 并重试。

- `-E` *fingerprint_hash*

  - 指定显示密钥指纹时使用的哈希算法。有效选项为："md5" 和 "sha256"。默认为 "sha256"。

- `-e` *pkcs11*

  - 移除由 PKCS#11 共享库 *pkcs11* 提供的密钥。

- `-k`

  - 在将密钥加载到代理或从代理中删除密钥时，仅处理普通私钥并跳过证书。

- `-L`

  - 列出当前由代理表示的所有身份的公钥参数。

- `-l`

  - 列出当前由代理表示的所有身份的指纹。

- `-s` *pkcs11*

  - 添加由 PKCS#11 共享库 *pkcs11* 提供的密钥。

- `-t` *life*

  - 向代理添加身份时设置最大生存时间。生存时间可以指定为

### 环境变量

`DISPLAY` 和 `SSH_ASKPASS`

如果 `ssh-add` 需要密码短语，且它是在终端中运行的，则它会从当前终端读取密码短语。如果 `ssh-add` 没有关联的终端，但设置了 `DISPLAY` 和 `SSH_ASKPASS`，它将执行 `SSH_ASKPASS` 指定的程序（默认为“ssh-askpass”），并打开一个 X11 窗口来读取密码短语。在从 .xsession 或相关脚本中调用 `ssh-add` 时，这特别有用。（注意：在某些机器上，可能需要将输入重定向自 /dev/null 才能使此功能正常工作。）

`SSH_AUTH_SOCK`

标识用于与代理通信的 UNIX 套接字的路径。

`SSH_USE_STRONG_RNG`

OpenSSL 随机生成器的重新填充通常来自 `/dev/urandom`。

如果 `SSH_USE_STRNG` 环境变量的值设置为非 `0`，OpenSSL 随机生成器将使用 `/dev/random` 进行重新填充。读取的字节数由 `SSH_USE_STRONG_RNG` 的值定义，最少为 14 字节。对于没有硬件随机生成器的计算机，不建议使用此设置，因为熵不足会导致连接被阻塞，直到有足够的熵可用。

### 文件

- `~/ssh/identity`

  - 包含用户协议版本 1 的 RSA 认证身份。

- `~/ssh/id_dsa`

  - 包含用户协议版本 2 的 DSA 认证身份。

- `~/ssh/id_ecdsa`

  - 包含用户协议版本 2 的 ECDSA 认证身份。

- `~/ssh/id_ed25519`

  - 包含用户协议版本 2 的 Ed25519 认证身份。

- `~/ssh/id_rsa`

  - 包含用户协议版本 2 的 RSA 认证身份。

身份文件不应被除用户以外的任何人读取。请注意，如果身份文件可被他人访问，ssh-add 将忽略这些文件。

### 退出状态

成功时退出状态为 0，如果指定命令失败则为 1，如果 `ssh-add` 无法联系认证代理则为 2。

### 参见

`ssh(1)`, `ssh-agent(1)`, `ssh-askpass(1)`, `ssh-keygen(1)`, `sshd_config(5)`

### 作者

OpenSSH 是 Tatu Ylonen 最初免费发布的 ssh 1.2.12 版本的衍生产品。Aaron Campbell、Bob Beck、Markus Friedl、Niels Provos、Theo de Raadt 和 Dug Song 修复了许多漏洞，重新添加了较新的功能，并创建了 OpenSSH。Markus Friedl 为 SSH 协议版本 1.5 和 2.0 提供了支持。

### SSH-AGENT

### 名称

`ssh-agent` - 认证代理

### 语法

```
ssh-agent [ -c | s ] [ -a bind_address ] [ -E fingerprint_hash ] [ -t life ] [ command [arg ... ] ]
ssh-agent [ -c | s ] -k
```
