
```yaml
include_role:
  name: rhel-system-roles.sshd
vars:
  sshd:
    # 仅从特定子网允许 root 登录和密码登录
    PermitRootLogin: no
    PasswordAuthentication: no
    Match:
      - Condition: "Address 192.0.2.0/24"
        PermitRootLogin: yes
        PasswordAuthentication: yes
```

该剧本（playbook）将受控节点配置为 SSH 服务器，配置如下：

- 禁用了密码登录和 root 用户登录
- 仅从子网 `192.0.2.0/24` 启用密码登录和 root 用户登录

你可以根据喜好修改变量。有关更多信息，请参阅 SSHD 服务器系统角色变量。

### 可选：验证剧本语法

```bash
ansible-playbook --syntax-check path/custom-playbook.yml
```

### 在你的清单文件上运行剧本

```bash
ansible-playbook -i inventory_file path/custom-playbook.yml
...
PLAY RECAP
****************************************************

localhost : ok=12 changed=2 unreachable=0 failed=0
skipped=10 rescued=0 ignored=0
```

#### 验证

1. 登录到 SSH 服务器：

```bash
$ ssh user1@10.1.1.1
```

其中：

- `user1` 是 SSH 服务器上的一个用户。
- `10.1.1.1` 是 SSH 服务器的 IP 地址。

2. 检查 SSH 服务器上 `sshd_config` 文件的内容：

```bash
# vim /etc/ssh/sshd_config
# Ansible managed
HostKey /etc/ssh/ssh_host_rsa_key
```

```bash
HostKey /etc/ssh/ssh_host_ecdsa_key
HostKey /etc/ssh/ssh_host_ed25519_key
AcceptEnv LC_CTYPE LC_NUMERIC LC_TIME LC_COLLATE LC_MONETARY LC_MESSAGES
AcceptEnv LC_PAPER LC_NAME LC_ADDRESS LC_TELEPHONE LC_MEASUREMENT
AcceptEnv LC_IDENTIFICATION LC_ALL_LANGUAGE
AcceptEnv XMODIFIERS
AuthorizedKeysFile .ssh/authorized_keys
ChallengeResponseAuthentication no
GSSAPICAuthentication yes
GSSAPICleanupCredentials no
PasswordAuthentication no
PermitRootLogin no
Subsystem sftp /usr/lib/exec/openssl/sftp-server
SyslogFacility AUTHPRIV
UsePAM yes
X11Forwarding yes
Match Address 192.0.2.0/24
PasswordAuthentication yes
PermitRootLogin yes
```

3. 检查你是否可以从 `192.0.2.0/24` 子网以 root 身份连接服务器：

a. 确定你的 IP 地址：

```bash
$ hostname -l
192.0.2.1
```

如果 IP 地址在 `192.0.2.1 - 192.0.2.254` 范围内，你就可以连接到服务器。

b. 以 root 身份连接到服务器：

```bash
$ ssh root@10.1.1.1
```

额外资源

- `/usr/share/doc/rhel-system-roles/sshd/README.md` 文件。
- `ansible-playbook(1)` 手页。

## 8.3 SSH 系统角色变量

在 SSH 系统角色中，你可以根据自己的喜好和限制为客户端 SSH 配置文件定义参数。

如果你不配置这些变量，系统角色将生成一个与 RHEL 默认设置匹配的全局 `ssh_config` 文件。

在所有情况下，布尔值在 ssh 配置中会正确渲染为 `yes` 或 `no`。你可以使用列表定义多行配置项。例如：

```yaml
LocalForward:
- 22 localhost:2222
- 403 localhost:4003
```

渲染为：

```text
LocalForward 22 localhost:2222
LocalForward 403 localhost:4003
```

> 注意
> 配置选项对大小写敏感。

### SSH 系统角色的变量

#### `ssh_user`

你可以定义一个已有的用户名，系统角色将为该用户修改用户特定的配置。用户特定配置保存在指定用户的 `~/.ssh/config` 中。默认值为 `null`，这会修改所有用户的全局配置。

#### `ssh_skip_defaults`

默认值为 `auto`。如果设置为 `auto`，系统角色将写入系统级配置文件 `/etc/ssh/ssh_config` 并保留其中定义的 RHEL 默认值。通过创建插入式（drop-in）配置文件（例如通过定义 `drop_in_name` 变量），将自动禁用 `ssh_skip_defaults` 变量。

#### `ssh_drop_in_name`

定义插入式配置文件的名称，该文件放置在系统级插入式目录下。该名称用于模板 `/etc/ssh/ssh_config/(drop_in_name).conf`，以引用要修改的配置文件。如果系统不支持插入式目录，则默认值为 `null`。如果系统支持插入式目录，则默认值为 `00-able`。

> 警告
> 如果系统不支持插入式目录，设置此选项将导致剧本执行失败。

建议的格式为 `NN-name`，其中 `NN` 是用于配置文件排序的两位数字，`name` 是名称。

#### `ssh_user`

你可以定义一个已有的用户名，系统角色将为该用户修改用户特定的配置。用户特定配置保存在指定用户的 `~/.ssh/config` 中。默认值为 `null`，这会修改所有用户的全局配置。

#### `ssh_skip_defaults`

默认值为 `auto`。如果设置为 `auto`，系统角色将写入系统级配置文件 `/etc/ssh/ssh_config` 并保留其中定义的 RHEL 默认值。通过创建插入式（drop-in）配置文件（例如通过定义 `drop_in_name` 变量），将自动禁用 `ssh_skip_defaults` 变量。

#### `ssh_drop_in_name`

定义插入式配置文件的名称，该文件放置在系统级插入式目录下。该名称用于模板 `/etc/ssh/ssh_config/(drop_in_name).conf`，以引用要修改的配置文件。如果系统不支持插入式目录，则默认值为 `null`。如果系统支持插入式目录，则默认值为 `00-able`。

> 警告
> 如果系统不支持插入式目录，设置此选项将导致剧本执行失败。

建议的格式为 `NN-name`，其中 `NN` 是用于配置文件排序的两位数字，`name` 是名称。

#### `ssh_user`

你可以定义一个已有的用户名，系统角色将为该用户修改用户特定的配置。用户特定配置保存在指定用户的 `~/.ssh/config` 中。默认值为 `null`，这会修改所有用户的全局配置。

#### `ssh_skip_defaults`

默认值为 `auto`。如果设置为 `auto`，系统角色将写入系统级配置文件 `/etc/ssh/ssh_config` 并保留其中定义的 RHEL 默认值。通过创建插入式（drop-in）配置文件（例如通过定义 `drop_in_name` 变量），将自动禁用 `ssh_skip_defaults` 变量。

#### `ssh_drop_in_name`

定义插入式配置文件的名称，该文件放置在系统级插入式目录下。该名称用于模板 `/etc/ssh/ssh_config/(drop_in_name).conf`，以引用要修改的配置文件。如果系统不支持插入式目录，则默认值为 `null`。如果系统支持插入式目录，则默认值为 `00-able`。

> 警告
> 如果系统不支持插入式目录，设置此选项将导致剧本执行失败。

建议的格式为 `NN-name`，其中 `NN` 是用于配置文件排序的两位数字，`name` 是名称。

#### `ssh_user`

你可以定义一个已有的用户名，系统角色将为该用户修改用户特定的配置。用户特定配置保存在指定用户的 `~/.ssh/config` 中。默认值为 `null`，这会修改所有用户的全局配置。
