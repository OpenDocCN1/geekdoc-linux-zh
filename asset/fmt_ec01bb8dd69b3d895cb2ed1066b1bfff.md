
虽然 Firefox 浏览器可以在未执行 `update-ca-trust` 的情况下使用新添加的证书，但建议在 CA 变更后运行 `update-ca-trust`。请注意，诸如 Firefox、Epiphany 或 Chromium 等浏览器会缓存文件，您可能需要清除浏览器缓存或重启浏览器以加载当前的系统证书配置。

### 4.14.3. 管理受信任的系统证书

要列出、提取、添加、删除或更改信任锚点，请使用 `trust` 命令。要查看此命令的内置帮助，请输入不带任何参数的该命令，或者使用 `--help` 指令：

```bash
$ trust
usage: trust command <args>...

Common trust commands are:
    list        List trust or certificates
    extract     Extract certificates and trust
    extract-compat Extract trust compatibility bundles
    anchor      Add, remove, change trust anchors
    dump        Dump trust objects in internal format

See 'trust <command> --help' for more information
```

要列出所有系统信任锚点和证书，请使用 `trust list` 命令：

```bash
$ trust list
pkcs11:id=%d2%87b4%e3%df%37%2793%55%f6%56%ea%81%e5%36%cc%8c%1e%3f%bd;type=cert
        type: certificate
        label: ACCVRAIZ1
        trust: anchor
        category: authority

pkcs11:id=%a6%b3%e1%2b%2b%49%b6%d77%3%aa%94%f5%01%e7%73%65%4c%ac%50;type=cert
        type: certificate
        label: ACEDICOM Root
        trust: anchor
        category: authority
...
[Output has been truncated]
```

`trust` 命令的所有子命令都提供详细的内置帮助，例如：

```bash
$ trust list --help
usage: trust list --filter=<what>

  --filter=<what>      filter of what to export
                       ca-anchors     certificate anchors
                       blacklist      blacklisted certificates
                       trust-policy   anchors and blacklist (default)
                       certificates   all certificates
                       pkcs11:object=xx a PKCS#11 URI
  --purpose=<usage>    limit to certificates usable for the purpose
                       server-auth    for authenticating servers
                       client-auth    for authenticating clients
                       email          for email protection
                       code-signing   for authenticating signed code
                       1.2.3.4.5...   an arbitrary object id
  -V, --verbose        show verbose debug output
  -q, --quiet         suppress command output
```

要将信任锚点存储到系统范围的信任存储中，请使用 `trust anchor` 子命令并指定证书的*路径*，例如：

```bash
# trust anchor path.to/certificate.crt
```

要删除证书，请使用证书的*路径*或证书的 ID：

```bash
# trust anchor --remove path.to/certificate.crt
# trust anchor --remove "pkcs11:id=%AABB%CC%DD%EE;type=cert"
```

### 4.14.4. 其他资源

如需更多信息，请参见以下 man 页：

- `update-ca-trust(8)`
- `trust(1)`

## 4.15. 使用 MACsec

媒体访问控制安全（MACsec，IEEE 802.1AE）使用 GCM-AES-128 算法对局域网中的所有流量进行加密和认证。MACsec 不仅可以保护 IP，还可以保护地址解析协议（ARP）、邻居发现（ND）或 DHCP。虽然 `Ipsec` 在网络层（第 3 层）运行，SSL - TLS 在传输层（第 4 层）运行，但 MACsec 在数据链路层（第 2 层）运行。将 MACsec 与其他网络层的安全协议结合使用，可以利用这些标准提供的不同安全特性。

有关 MACsec 网络架构、用例场景和配置示例的更多信息，请参阅*MACsec：加密网络流量的另一种解决方案*文章。

关于如何使用 `wpa_supplicant` 和 `NetworkManager` 配置 MACsec 的示例，请参见*Red Hat Enterprise Linux 7 网络指南*。

## 4.16. 使用 SCRUB 安全删除数据

`scrub` 实用程序在特殊文件或磁盘设备上设置模式，以使检索数据变得更加困难。使用 `scrub` 比在磁盘上写入随机数据更快。此过程提供高可用性、可靠性和数据保护。

要开始使用 `scrub` 命令，请安装 `scrub` 包：

```bash
~]# yum install scrub
```

`scrub` 实用程序在以下基本模式之一中运行：

### 字符或块设备

对应于整个磁盘的*特殊文件*被擦除，其上的所有数据都会被销毁。这是最有效的方法。

```bash
scrub [OPTIONS] special file
```

### 文件

常规文件被擦除，并且仅销毁文件中的数据。

```bash
scrub [OPTIONS] file
```

### 目录

使用 `-X` 选项时，会创建一个目录并填充文件，直到文件系统已满。然后，像文件模式那样擦除这些文件。

```bash
scrub -X [OPTIONS] directory
```

### 示例 4.7. 擦除原始设备

要使用默认的 National Nucluar Security Administration (NNSA) 模式擦除原始设备 `/dev/sdf1`，请输入以下命令：

```bash
~]# scrub /dev/sdf1
scrub: using NNSA NAP-14.1-C patterns
scrub: please verify that device size below is correct!
scrub: scrubbing /dev/sdf1 1995650048 bytes (~1GB)
scrub: random |...................................................|
scrub: random |...................................................|
scrub: 0x00   |...................................................|
scrub: verify  |...................................................|
```

### 示例 4.8. 擦除文件

1. 创建一个*1MB*文件：

```bash
~]$ base64 /dev/urandom | head -c $[ 1024*1024 ] > file.txt
```

2. 显示文件大小：
