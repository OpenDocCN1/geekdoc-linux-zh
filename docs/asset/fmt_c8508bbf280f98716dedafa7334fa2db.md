
```bash
#!/usr/bin/bash
{
  output=""
  skgid="ssh keys" # 指定拥有 openSSH 密钥的组
  awk -F ' ' '$1 ~ "$skgid" {print $3}' /etc/group
  awk -F'|' <<< "$(find /etc/ssh -name "*ssh_host*" -type f -exec stat -l -c "%a %U %g" +)" | while read -r file mode owner group; do
    [ -z "$skgid" ] && cga="$mask" || cga="root"
    [ "$mode" != "0177" ] || mask="0177"
    maxperm=$(printf "%o" "$(0177 & mask)")
    if [ $((mode & mask)) -gt 0 ]; then
      echo "File: $file is mode $mode changing to mode: $maxperm"
      [ -n "$skgid" ] ; then
        chmod u-x,g-rw "$file"
      else
        chmod u-x,g-rw "$file"
      fi
    fi
    if [ "$owner" != "root" ]; then
      echo "File: $file is owned by $owner changing owner to "root""
      chown root "$file"
    fi
    if [ "$group" = "root" ] && [ "$group" != "root" ]; then
      chgrp "$cga" "$file"
    fi
  done
  if [ -z "$output" ]; then
    echo -e "\n- Audit Result:\nPASS"
  else
    echo -e "\n- Audit Result:\nFAILED"
  fi
fi
}
```

# CIS 控制项：

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | **3.3 配置访问控制列表** 根据用户的知情需要配置数据访问控制列表。将数据访问控制列表（也称为访问权限）应用于本地和远程文件系统、数据库和应用程序。 | | | |
| v7 | **14.6 通过访问控制列表保护信息** 通过特定的文件系统、网络共享、声明、应用程序或数据库访问控制列表来保护存储在系统上的所有信息。这些控制将实施以下原则：只有授权的个人根据其职责范围内访问信息的需要才能访问信息。 | | | |

# MITRE ATT&CK 映射：

| 技术 / 子技术 | 战术 | 缓解措施 |
|---|---|---|
| T1552, T1552.004 | TA0003, TA0006 | M1022 |

# 5.2.3 确保 SSH 公钥主机密钥文件的权限已配置（自动化）

**策略适用性：**

+ Level 1 - 服务器
- Level 1 - 工作站

**描述：**

SSH 公钥是 SSH 公钥认证中使用的两个文件之一。在这种认证方法中，公钥是用于验证使用相应私钥生成的数字签名的密钥。只有与私钥对应的公钥才能成功通过验证。

**原理：**

如果公主机密钥文件被未经授权的用户修改，SSH 服务可能会受到破坏。

# 审计：

对所有返回的文件运行以下权限命令以检查组或其他用户：访问权限未授予写入或执行权限

```bash
# find /etc/ssh -xdev -type f -name 'ssh_host_*_key.pub' -exec stat {} \;
```

示例输出：

```
File: /etc/ssh/ssh_host_rsa_key.pub
Size: 382 Blocks: 8 IO Block: 4096 regular file
Device: ca01h/5713d Inode: 8631758 Links: 1
Access: (0644/rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)
Access: 2018-10-22 18:24:56.89750616 +0000
Modify: 2018-10-22 18:24:56.94750616 +0000
Change: 2018-10-22 18:24:56.91750616 +0000
File: /etc/ssh/ssh_host_ed25519_key.pub
Size: 82 Blocks: 8 IO Block: 4096 regular file
Device: ca01h/5713d Inode: 8631763 Links: 1
Access: (0644/rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)
Access: 2018-10-22 18:24:56.94750616 +0000
Modify: 2018-10-22 18:24:56.94750616 +0000
Change: 2018-10-22 18:24:56.91750616 +0000
```

# 修复：

运行以下命令为 SSH 主机公钥文件设置权限和所有权

```bash
# find /etc/ssh -xdev -type f -name 'ssh_host_*_key.pub' -exec chmod u-x,go-wx {} \;
# find /etc/ssh -xdev -type f -name 'ssh_host_*_key.pub' -exec chown root:root {} \;
```

# 默认值：

Access: (0644/rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)

# CIS 控制：

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 3.3 配置数据访问控制列表 | 根据用户的知情需求配置数据控制列表。将数据访问控制列表（也称为访问权限）应用于本地和远程文件系统、数据库和应用程序。 | ● | ● | ● |
| v7 | 5.1 建立安全配置 | 为所有授权的操作系统和软件维护文档化的、标准的安全配置标准。 | ● | ● | ● |

# MITRE ATT&CK 映射：

| 技术 / 子技术 | 战术 | 缓解措施 |
|---|---|---|
| T1557, T1557.000 | TA0003, TA0006 | M1022 |

# 5.2.4 限制 SSH 访问（自动化）

**配置适用性：**

- 级别 1 - 服务器
- 级别 1 - 工作站

**描述：**

有多种选项可以限制哪些用户和组可以通过 SSH 访问系统。建议至少利用以下选项之一：

- `AllowUsers`:
  - `AllowUsers` 变量允许系统管理员允许特定用户 ssh 进系统的选项。该列表由空格分隔的用户名组成。此变量不识别数字用户 ID。如果系统管理员想通过仅允许用户从特定主机登录来进一步限制用户访问，可以使用 `user@host` 的形式指定条目。
- `AllowGroups`:
  - `AllowGroups` 变量允许系统管理员允许特定用户组 ssh 进入系统的选项。该列表由空格分隔的组名组成。此变量不识别数字组 ID。
- `DenyUsers`:
  - `DenyUsers` 变量允许系统管理员拒绝特定用户 ssh 进入系统的选项。该列表由空格分隔的用户名组成。此变量不识别数字用户 ID。如果系统管理员想通过专门拒绝用户从特定主机的访问来进一步限制用户访问，可以使用 `user@host` 的形式指定条目。
- `DenyGroups`:
  - `DenyGroups` 变量允许系统管理员拒绝特定用户组 ssh 进入系统的选项。该列表由空格分隔的组名组成。此变量不识别数字组 ID。

**理由：**

限制哪些用户可以通过 SSH 远程访问系统将有助于确保只有授权的用户访问系统。

# 审计：

运行以下命令并验证输出：

```bash
# sshd -T -C user=root -C host="$(hostname)" -C addr="$(grep $(hostname) /etc/hosts | awk '{print $1}')" | grep '^(allow|deny) (users|groups)'
```

验证两个命令的输出至少匹配其中一个：

- `allow-users <userlist>`
- `allow-groups <grouplist>`
- `deny-users <userlist>`
- `deny-groups <grouplist>`

# 修复：

编辑 `/etc/ssh/sshd_config` 文件以设置以下参数：

- `AllowUsers <userlist>`
- OR
- `AllowGroups <grouplist>`
- OR
- `DenyUsers <userlist>`
- OR
- `DenyGroups <grouplist>`

# CIS Controls:

| Controls Version | Control | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 4.1 建立并维护安全配置流程：为企业资产（终端用户设备，包括便携式和移动设备、非计算/IoT 设备以及服务器）和软件（操作系统和应用程序）建立并维护安全配置流程。每年审查并更新文档，或在发生可能影响此保护措施的重大企业变更时更新。 | ● | ● | ● |
| v7 | 5.1 建立安全配置：为所有授权的操作系统和软件维护记录的标准的安全配置标准。 | ● | ● | ● |

# MITRE ATT&CK 映射:

| Techniques / Sub-techniques | Tactics | Mitigations |
|---|---|---|
| T1021, T1021.004 | TA0001 | M1035 |

## 5.2.7 确保禁用 SSH root 登录（自动化）

**Profile Applicability:**

- Level 1 - 服务器
- Level 1 - 工作站

**Description:**

`PermitRootLogin` 参数指定了 `root` 用户是否可以使用 SSH 登录。默认值是 `prohibit-password`。

**Rationale:**

禁止通过 SSH 允许 `root` 登录需要系统管理员使用其个人账户进行身份验证，然后提升到 `root` 权限。这限制了不可否认性的风险，并在发生安全事件时提供清晰的审计追踪。

**Audit:**

运行以下命令：

```bash
# sshd -T -C user=root -C host="$(hostname)" -C addr="$(grep $(hostname) /etc/hosts | awk '{print $1}')" | grep permitrootlogin
```

验证输出匹配：

```
permitrootlogin no
```

运行以下命令：

```bash
# grep -Ei '\s*PermitRootLogin\s+no' /etc/ssh/sshd_config
```

验证输出匹配：

```
PermitRootLogin no
```

**Remediation:**

编辑 `/etc/ssh/sshd_config` 文件，将参数设置如下：

```
PermitRootLogin no
```

**Default Value:**

`PermitRootLogin without-password`

**References:**

- 1. `SSHD_CONFIG(5)`

# CIS Controls:

| Controls Version | Control | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 5.4 限制管理员权限至专用管理员账户：将企业资产上的管理员权限限制在专用管理员账户中。通用计算活动（如互联网浏览、电子邮件和生产力套件的使用）应通过用户的主要非特权账户进行。 | ● | ● | ● |
| v7 | 4.3 确保使用专用管理账户：确保所有具有管理账户访问权限的用户都使用专用或次要账户执行提升活动。此账户应仅用于管理活动，而不应用于互联网浏览、电子邮件或类似活动。 | ● | ● | ● |

# MITRE ATT&CK 映射:

| Techniques / Sub-techniques | Tactics | Mitigations |
|---|---|---|
| T1021 | TA0008 | M1042 |

## 5.2.8 确保禁用 SSH HostbasedAuthentication（自动化）

**Profile Applicability:**

- Level 1 - 服务器
- Level 1 - 工作站

**Description:**

`HostbasedAuthentication` 参数指定了是否允许通过使用 `.shosts` 或 `/etc/hosts.equiv` 的受信任主机，结合成功的公钥客户端主机认证进行身份验证。

**Rationale:**

即使在 `/etc/pam.conf` 中禁用了支持，`.hosts` 文件也将无效，但在 SSH 中禁用使用 `.hosts` 文件的功能可以提供额外的保护。

**Audit:**

运行以下命令：

```bash
# sshd -T -C user=root -C host="$(hostname)" -C addr="$(grep $(hostname) /etc/hosts | awk '{print $1}')" | grep hostbasedauthentication
```

验证输出匹配：

```
hostbasedauthentication no
```

运行以下命令：

```bash
# grep -Ei '^HostbasedAuthentication\s+yes' /etc/ssh/sshd_config
```

没有任何输出。

**Remediation:**

编辑 `/etc/ssh/sshd_config` 文件，将参数设置如下：

```
HostbasedAuthentication no
```

**Default Value:**

`HostbasedAuthentication no`

**References:**

- 1. `SSHD_CONFIG(5)`

| Controls Version | Control | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 4.1 建立并维护安全配置流程：为企业资产（终端用户设备，包括便携式和移动设备、非计算/IoT 设备以及服务器）和软件（操作系统和应用程序）建立并维护安全配置流程。每年审查并更新文档，或在发生可能影响此保护措施的重大企业变更时更新。 | | | |
| v7 | 16.3 确保多因素认证：确保无论是在线管理还是由第三方提供，所有用户账户都使用多因素认证。 | | | |

# MITRE ATT&CK 映射:

| Techniques / Sub-techniques | Tactics | Mitigations |
|---|---|---|
| T1021, T1021.004 | TA0001 | M1035 |

## 5.2.9 确保禁用 SSH PermitPasswords（自动化）

**Profile Applicability:**

- Level 1 - 服务器
- Level 1 - 工作站

**Description:**

`PermitPasswords` 参数指定 SSH 是否允许空密码。

**Rationale:**

禁止空密码可以减少未经授权访问的概率。

**Audit:**

运行以下命令：

```bash
# sshd -T -C user=root -C host="$(hostname)" -C addr="$(grep $(hostname) /etc/hosts | awk '{print $1}')" | grep permitpass
```

验证输出匹配：

```
permitpass no
```

运行以下命令：

```bash
# grep -Ei '^PermitPasswords\s+yes' /etc/ssh/sshd_config
```

没有任何输出。

**Remediation:**

编辑 `/etc/ssh/sshd_config` 文件，将参数设置如下：

```
PermitPasswords no
```

**Default Value:**

`PermitPasswords no`

**References:**

- 1. `SSHD_CONFIG(5)`

# CIS Controls:

| Controls Version | Control | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 4.1 建立并维护安全配置流程：为企业资产（终端用户设备，包括便携式和移动设备、非计算/IoT 设备以及服务器）和软件（操作系统和应用程序）建立并维护安全配置流程。每年审查并更新文档，或在发生可能影响此保护措施的重大企业变更时更新。 | | | |
| v7 | 16.3 确保多因素认证：确保无论是在线管理还是由第三方提供，所有用户账户都使用多因素认证。 | | | |

## 5.2.10 确保禁用 SSH PermitUserEnvironment（自动化）

**Profile Applicability:**

- Level 1 - 服务器
- Level 1 - 工作站

**Description:**

`PermitUserEnvironment` 允许用户向 SSH 守护进程提供环境变量选项。

**Rationale:**

允许用户通过 SSH 设置环境变量可能允许用户绕过安全控制（例如设置一个包含木马程序的执行路径）。
