
### Audit

运行以下命令：

```bash
# ssh -T -C user=root -C host="$(hostname)" -C addr="$(grep $(hostname) /etc/hosts | awk '{print $1}')" | grep permituserenvironment
```

验证输出匹配：

```
permituserenvironment no
```

运行以下命令：

```bash
# grep -Ei '^\s*PermitUserEnvironment\s+yes' /etc/ssh/sshd_config
```

没有任何输出。

### Remediation

编辑 `/etc/ssh/sshd_config` 文件，将参数设置如下：

```
PermitUserEnvironment no
```

### Default Value

`PermitUserEnvironment no`

### References

1. `SSHD_CONFIG(5)`

## 5.2.11 确保 SSH IgnoreRosts 已启用（自动化）

### 配置适用性

* Level 1 - 服务器
* Level 1 - 工作站

### 描述

`IgnoreRosts` 参数指定在 `RhostsRSAAuthentication` 或 `HostbasedAuthentication` 身份验证中不使用 `.rhosts` 和 `.hosts` 文件。

### 原理

设置此参数将强制用户在使用 SSH 进行身份验证时输入密码。

### Audit

运行以下命令：

```bash
# sshd -T -C user=root -C host="$(hostname)" -C addr="$(grep -p \$(grep \$(hostname) /etc/hosts) | awk '{print $1}')" | grep ignorerosts
```

验证输出是否匹配：

```
ignorerosts yes
```

运行以下命令：

```bash
# grep -Ei '^\s*ignorerosts\sno\b' /etc/ssh/sshd_config
```

不应返回任何内容。

### Remediation

编辑 `/etc/ssh/sshd_config` 文件，将参数设置如下：

```
IgnoreRosts yes
```

### Default Value

`IgnoreRosts yes`

### References

1. `SSHD_CONFIG(5)`

### CIS 控制

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 4.1 建立并维护安全配置流程 | 为企业资产（终端设备，包括便携式和移动设备、非计算/IoT 设备和服务器）以及软件（操作系统和应用程序）建立并维护安全配置流程。每年审查更新文档，或发生可能影响此保护措施的重大企业变更时进行更新。 | | | |
| v7 | 9.2 确保仅运行批准的端口、协议和服务 | 确保每个系统仅运行在经过验证的业务需求的系统上监听的网络端口、协议和服务。 | | | |

### MITRE ATT&CK 映射

| 技术 / 子技术 | 战术 | 缓解措施 |
|---|---|---|
| T1078, T1078.001, T1078.003 | TA0001 | M1027 |

## 5.2.12 确保 SSH X11 转发已禁用（自动化）

### 配置适用性

* Level 1 - 工作站
* Level 2 - 服务器

### 描述

`X11Forwarding` 参数提供了通过连接到远程图形连接隧道 X11 流量的能力。

### 原理

除非有直接使用 X11 应用程序的需求，否则禁用 X11 转发。存在极小风险，即通过开启 X11 转发登录 SSH 的用户其远程 X11 服务器可能会被 X11 服务器上的其他用户攻击。请注意，即使禁用了 X11 转发，用户也可以安装自己的转发。

### Audit

运行以下命令：

```bash
# sshd -T -C user=root -C host="$(hostname)" -C addr="$(grep $(hostname) /etc/hosts | awk '{print $1}')" | grep -i x11forwarding
```

验证输出是否匹配：

```
x11forwarding no
```

运行以下命令：

```bash
# grep -Ei '^\s*x11forwarding\s+yes' /etc/ssh/sshd_config
```

未返回任何内容。

### Remediation

编辑 `/etc/ssh/sshd_config` 文件，将参数设置如下：

```
X11Forwarding no
```

### CIS 控制

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 4.8 在企业资产和软件上卸载或禁用不必要的服务 | 卸载或禁用企业资产和软件上必要的服务，例如未使用的文件共享服务、Web应用程序模块或服务功能。 | | | |
| v7 | 9.2 确保仅运行批准的端口、协议和服务 | 确保每个系统仅运行在经过验证的业务需求的系统上监听的网络端口、协议和服务。 | | | |

### MITRE ATT&CK 映射

| 技术 / 子技术 | 战术 | 缓解措施 |
|---|---|---|
| T1210, T1210.000 | TA0008 | M1042 |

## 5.2.13 确保使用强加密（自动化）

### 配置适用性

* Level 1 - 服务器
* Level 1 - 工作站

### 描述

此变量限制了 SSH 在通信期间可以使用的加密算法。

### 注意

* 某些组织对加密算法有更严格的要求。
* 确保使用的加密算法符合站点策略。
* 目前符合 FIPS 140-2 的“强”加密算法：
    * `aes256-ctr`
    * `aes192-ctr`
    * `aes128-ctr`
* OpenSSH 8.2 支持的加密算法：

```
3des-cbc
aes128-cbc
aes192-cbc
aes256-cbc
aes128-ctr
aes192-ctr
aes256-ctr
aes128-gcm@openssh.com
aes256-gcm@openssh.com
chacha20-poly1305@openssh.com
```

### 原理

SSH 中使用的弱加密算法无法提供机密性或完整性，数据可能被破解。

* SSH 中使用的 Triple DES 加密具有约十亿次的碰撞，这使得远程攻击者更容易对加密会话进行“Sweet32”攻击。
* SSH 协议中的错误处理：当客户端和服务器使用 CBC 块链式加密模式时，远程攻击者更容易通过未知向量恢复某些密文明文。

### Audit

运行以下命令：

```bash
# sshd -T -C user=root -C host="$(hostname)" -C addr="$(grep $(hostname) /etc/hosts | awk '{print $1}') | grep ciphers
```

验证输出不包含以下内容：

* `3des-cbc`
* `aes128-cbc`
* `aes192-cbc`
* `aes256-cbc`

### Remediation

编辑 `/etc/ssh/sshd_config` 文件，添加/修改 `Ciphers` 行，包含以逗号分隔的加密算法列表。

示例：

```
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com,aes256-ctr,aes192-ctr,aes128-ctr
```

### Default Value

`Ciphers chacha20-poly1305@openssh.com,aes128-ctr,aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com`

### References

1. `https://nvd.nist.gov/vuln/detail/CVE-2016-2183`
2. `https://www.openssh.com/txt/cbc`
3. `https://nvd.nist.gov/vuln/detail/CVE-2008-5161`
4. `https://www.openssh.com/txt/cbc`
5. `SSH_CONFIG(5)`

### CIS 控制

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 3.10 加密传输数据 | 加密传输中的数据。示例实现包括：传输层安全 (TLS) 和 Open Secure Shell (OpenSSH)。 | | ● | |
| v7 | 14.4 加密传输的所有敏感信息 | 加密传输的所有敏感信息。 | | ● | ● |

### MITRE ATT&CK 映射

| 技术 / 子技术 | 战术 | 缓解措施 |
|---|---|---|
| T1040, T1040.000, T1557 | TA0006 | M1041 |

## 5.2.14 确保仅使用强 MAC 算法（自动化）

### 配置适用性

* Level 1 - 服务器
* Level 1 - 工作站

### 描述

此变量限制了 SSH 在通信期间可以使用 MAC 算法类型。

### 注意

* 某些组织对批准的 MAC 有更严格的要求。
* 确保使用的 MAC 符合站点策略。
* 目前通过 FIPS 140-2 批准的“强”MAC 是：
    * `hmac-sha2-256`
    * `hmac-sha2-512`
* 支持的 MAC 如下：

```
hmac-md5
hmac-md5-96
hmac-sha1
hmac-sha1-96
hmac-sha2-256
hmac-sha2-512
umac-648@openssh.com
umac-128@openssh.com
hmac-md5-etm@openssh.com
hmac-md5-96-etm@openssh.com
hmac-sha1-etm@openssh.com
hmac-sha1-96-etm@openssh.com
hmac-sha2-256-etm@openssh.com
hmac-sha2-512-etm@openssh.com
umac-648-etm@openssh.com
umac-128-etm@openssh.com
```

### 原理

MD5 和 96 位 MAC 算法被认为是弱算法，已被证明会增加 SSH 级攻击的可利用性。弱算法继续被关注，可以使用扩展计算能力利用的弱点。破解算法的攻击者可以利用中间人（MITM）位置来解密 SSH 隧道并捕获凭据和信息。

### Audit

运行以下命令：

```bash
# ssh -T -C user=root -C host="$(hostname)" -C addr="$(grep $(hostname) /etc/hosts | awk '{print $1}')" | grep -i "MACS"
```

验证输出不包含列出的弱 MAC 算法：

* `hmac-md5`
* `hmac-md5-96`
* `hmac-ripemd160`
* `hmac-sha1`
* `hmac-sha1-96`
* `hmac-64@openssh.com`
* `hmac-128@openssh.com`
* `hmac-md5-etm@openssh.com`
* `hmac-md5-96-etm@openssh.com`
* `hmac-ripemd160-etm@openssh.com`
* `hmac-sha1-etm@openssh.com`
* `hmac-sha1-96-etm@openssh.com`
* `hmac-64-etm@openssh.com`
* `hmac-128-etm@openssh.com`

### CIS Controls

| Controls Version | Control | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 3.10 加密传输敏感数据<br>加密传输中的敏感数据。示例实现包括：传输层安全 (TLS) 和开放安全外壳 (OpenSSH)。 | | ● | ● |
| v7 | 14.4 加密传输所有敏感信息<br>加密传输中的所有敏感信息。 | | ● | ● |
| v7 | 16.5 加密用户名和身份凭据传输<br>确保所有账户用户名和身份凭据都通过加密通道跨网络传输。 | | ● | ● |

### MITRE ATT&CK Mappings

| Techniques / Sub-techniques | Tactics | Mitigations |
|---|---|---|
| T1040, T1040.000, T1557, T1557.000 | TA0006 | M1041 |

## 5.2.15 确保仅使用强密钥交换算法（自动化）

### Profile Applicability

* Level 1 - 服务器
* Level 1 - 工作站

### Description

密钥交换是密码学中的一种方法，通过双方之间交换加密密钥，允许使用加密算法。如果发送者和接收者希望交换加密消息，双方都必须具备加密待发送消息和解密接收消息的能力。

### Notes

* `Kex` 算法在列表中越靠前出现，优先级越高
* 某些组织对已批准的密钥交换算法可能有更严格的要求
* 确保使用的密钥交换算法符合站点策略
* 目前受 FIPS 140-2 批准的密钥交换算法有：
    * `ecdh-sha2-nistp256`
    * `ecdh-sha2-nistp384`
    * `ecdh-sha2-nistp521`
    * `diffie-hellman-group-exchange-sha256`
    * `diffie-hellman-group16-sha512`
    * `diffie-hellman-group18-sha512`
    * `diffie-hellman-group14-sha256`
* OpenSSH 8.2 支持的密钥交换算法为：

```
curve25519-sha256
curve25519-sha256@libssh.org
diffie-hellman-group1-sha
diffie-hellman-group4-sha
diffie-hellman-group14-sha256
diffie-hellman-group16-sha512
diffie-hellman-group18-sha512
diffie-hellman-group-exchange-sha
diffie-hellman-group-exchange-sha256
ecdh-sha2-nistp256
ecdh-sha2-nistp384
ecdh-sha2-nistp521
sntrup459176i6x25519-sha512@tinyssh.org
```

### Rationale

应该移除被认为较弱的密钥方法。密钥交换方法可能因为使用的位太少，或者哈希算法被认为太弱。弱算法可能会导致连接遭受中间人攻击。

### Audit

运行以下命令并验证输出结果不包含列出的任何弱密钥交换算法。

Weak Key Exchange Algorithms:

* `diffie-hellman-group1-sha`
* `diffie-hellman-group4-sha`
* `diffie-hellman-group-exchange-sha`

```bash
# ssh -T -C user@root -C "$(hostname)" -C addr="$(grep \$ $(hostname)" /etc/hosts | awk '{print $1}'" | grep keyalgorithms
```

### Remediation

编辑 `/etc/ssh/ssh_config` 文件，添加或修改 `KexAlgorithms` 行，使其包含由逗号分隔的站点批准密钥交换算法列表。

Example:

```
KexAlgorithms curve25519-sha256,curve25519-sha256@libssh.org,diffie-hellman-group4-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp256,diffie-hellman-group-exchange-sha256
```

### Default Value

`KexAlgorithms curve25519-sha256,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,diffie-hellman-group14-sha256`

### CIS Controls

| Controls Version | Control | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 3.10 加密传输敏感数据<br>加密传输中的敏感数据。示例实现包括：传输层安全 (TLS) 和开放安全外壳 (OpenSSH)。 | | ● | ● |
| v7 | 14.4 加密传输所有敏感信息<br>加密传输中的所有敏感信息。 | | ● | ● |
| v7 | 16.5 加密用户名和身份凭据传输<br>确保所有账户用户名和身份凭据都通过加密通道跨网络传输。 | | ● | ● |

### MITRE ATT&CK Mappings

| Techniques / Sub-techniques | Tactics | Mitigations |
|---|---|---|
| T1040, T1040.000, T1557, T1557.000 | TA0006 | M1041 |
