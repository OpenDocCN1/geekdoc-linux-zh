
```bash
$student@workstation ~]$ ansible --version
ansible 2.8.0
config file = /etc/ansible/ansible.cfg
configured module search path = ['/home/student/.ansible/plugins/modules','/usr/share/ansible/plugins/modules']
ansible python module location = /usr/lib/python3.6/site-packages/ansible
executable location = /usr/bin/ansible
python version = 3.6.8 (default, Apr 3 2019, 17:26:03) [GCC 8.2.1
20180905 (Red Hat 8.2.1-3)]
```

- 2. 在工作站的 `student` 用户目录 `/home/student` 下创建一个名为 `deploy-review` 的新目录。进入该目录。

```bash
$student@workstation ~]$ mkdir ~/deploy-review
$student@workstation ~]$ cd ~/deploy-review
```

- 3. 在 `deploy-review` 目录下创建一个 `ansible.cfg` 文件，用于设置以下默认值：
  - 以 `devops` 用户连接被管理主机。
  - 使用 `inventory` 子目录包含清单文件。
  - 默认禁用权限提升。如果通过命令行启用权限提升，配置默认设置让 Ansible 使用 `sudo` 切换到 `root` 账户。账户不应提示 `devops` 登录或 `sudo` 密码。
被管理主机已配置 `devops` 用户，该用户可以使用 SSH 密钥登录，并无需密码即可 `sudo` 命令运行任何命令。

### 3.1
使用文本编辑器创建 `/home/student/deploy-review/ansible.cfg` 文件。创建一个 `[defaults]` 段。添加 `remote_user` 指令，让 Ansible 在连接被管理主机时使用 `devops` 用户。添加 `inventory` 目录，配置 Ansible 使用 `/home/student/deploy-review/inventory` 目录作为清单文件的默认位置。

```
[defaults]
remote_user = devops
inventory = inventory
```

### 3.2
在 `/home/student/deploy-review/ansible.cfg` 文件中，创建 `[privilege_escalation]` 段并添加以下条目以禁用权限提升。将特权提升方法设置为使用 `sudo` 配合 `root` 账户，且不需要密码认证。

```
[privilege_escalation]
become = False
become_method = sudo
become_user = root
become_ask_pass = False
```

### 3.3
完成后的 `ansible.cfg` 文件内容如下：

```
[defaults]
remote_user = devops
inventory = inventory
```

```
[privilege_escalation]
become = False
become_method = sudo
become_user = root
become_ask_pass = False
```

保存你的工作并退出编辑器。

- 4. 创建 `/home/student/deploy-review/inventory` 目录。
下载 `http://materials.example.com/labs/deploy-review/inventory` 文件并将其保存为名为 `/home/student/deploy-review/inventory/inventory` 的静态清单文件。

### 4.1
创建 `/home/student/deploy-review/deploy-review/inventory` 目录。（注：此处路径可能有误，已按原文保留）

```
[student@workstation deploy-review]$ mkdir inventory
```

### 4.2
将 `http://materials.example.com/labs/deploy-review/inventory` 文件下载到 `/home/student/deploy-review/inventory` 目录。

```
[student@workstation deploy-review]$ wget -O inventory/inventory \
> http://materials.example.com/labs/deploy-review/inventory
```

### 4.3
检查 `/home/student/deploy-review/inventory/inventory` 文件的内容。

```
[student@workstation deploy-review]$ cat inventory/inventory
[internetweb]
serverb.lab.example.com
```

```
[intranetweb]
servera.lab.example.com
serverc.lab.example.com
serverd.lab.example.com
```

- 5. 执行 `id` 命令作为一个即性命令（ad hoc command），针对 `all` 主机组，以验证 `devops` 是远程用户且默认禁用了权限提升。

```
[@workstation deploy-review]$ ansible all -m command -a 'id'
server.lab.com | CHANGED | rc=>
uid=1001(devops) gid=1001(devops) groups=1001(devops) context=unconfined:
unconfined_r:unconfined:t:s0:s0.c023
nserver.lab.com | CHANGED | rc=>
uid=1001(devops) gid=1001(devops) groups=1001(devops) context=unconfined:
unconfined_r:unconfined:t:s0:s0.c023
nserver.lab.com | CHANGED | rc=>
uid=1001(devops) gid=1001(devops) groups=1001(devops) context=unconfined:
unconfined_r:unconfined:t:s0:s0.c023
```

你的结果返回顺序可能有所不同。

- 6. 执行一个即性命令，针对 `all` 主机组，使用 `copy` 模块修改 `/etc/motd` 文件的内容。
使用 `copy` 模块的 `content` 选项确保 `/etc/motd` 文件包含字符串 `This server is managed by Ansible.\n` 作为一个单行。（配合 `content` 选项使用的 `\n` 会导致模块在字符串末尾添加换行）。
你必须从命令行请求权限提升，以便根据当前的 `ansible.cfg` 默认设置执行此操作。
