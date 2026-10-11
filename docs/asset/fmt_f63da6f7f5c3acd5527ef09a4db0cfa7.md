
从系统中解析的 `roles` 列表

- `--roles-path`

  包含 `roles` 的路径。默认是 `roles_path` (`ansible.cfg`) 或 `/etc/ansible/roles`

### import:

将 `role` 导入 `ansible galaxy`

- `--branch <REFERENCE>`

  分支名称。默认为仓库的分支（通常为 `master`）。

- `--no-wait`

  不等待导入。

- `--role-name <ROLE_NAME>`

  你应该拥有的 `role` 名称，如果与仓库名不同

- `--status`

  检查给定 `github_user/github.repo` 的最新请求状态。

### setup:

从 `github` 或通过 `galaxy galaxy` 设置集成

- `--list`

  列出你所有的集成。

- `--remove <REMOVE_ID>`

  删除匹配提供的 `id` 值。使用 `--list` 查看。

### search:

- `--author <AUTHOR>`

  `galaxy` 上的 `github` 用户名

- `--galaxy-tags <TAGS>`

  用于过滤的标签列表

- `--platforms <PLATMS>`

  用于过滤的平台列表

- `--roles-path`

  包含 `roles` 的路径。默认是 `roles_path` (`ansible.cfg`) 或 `/etc/ansible/roles`

### Common Options:

- `-author <AUTHOR>`
- `-galaxy-tags <TAGS>`
- `-platforms <PLATMS>`
- `-version`
- `-c`
- `-h`
- `-p`
- `-s`
- `-v`

## `ansible-doc [-F][-s] [options] [<plugin>]`

显示 Ansible 库中安装的模块信息；插件及其描述，指定配置、文件、执行文件位置和包含 `roles` 的目录的有用详情。默认是 `roles_path` (`ansible.cfg`) 或 `/etc/ansible/roles`。

## Ad Hoc Commands

`ansible <host-pattern> -m <module-name> -a <arguments>` 运行命令，你必须指定。`shell` 模块是默认，但如果你有其他想使用的模块。

检查磁盘空间：`ansible all -m shell -a "cat /root | head"`

检查 `uptime`：`ansible all -m user -a 'cat=/etc/passwd' --become` 它将根据 `ansible.cfg` 进行验证。

作为 `root` 身份执行命令：`ansible all -m shell -a 'cat/passwd' --become`

创建用户组：`ansible all -m group -a 'name=devops'`

创建用户：`ansible all -m user -a 'name=doe' --become`

更改文件所有权：`ansible all -m file -a 'path=/tmp/my_directory owner=devops'`

带权限创建目录：`ansible all -m file -a 'path=/tmp/my_directory mode=0755' --become`

复制文件：`ansible all -m copy -a 'src=ansible.cfg dest=/home/ansible/.ansible.cfg'`

在主机上启动（或重启）：`ansible all -m service -a 'name=httpd state=started enabled'`

检查状态：`ansible all -m service -a 'name=httpd state=status'`

重启服务：`ansible all -m service -a 'name=httpd state=restarted'`

使用 `systemd` 模块启动/重启/加载：`ansible all -m systemd -a 'name=nginx state=reloaded' -i=prod-hosts`

获取文件清单：`ansible all -m file -a 'path=/etc/ansible/hosts'`

收集事实：`ansible all -m setup -a 'name=system'`

检查开放端口：`ansible all -m shell -a 'netstat -antlp | grep listen'`

获取日志信息：`ansible all -m shell -a 'tail /var/log/syslog'`

追加行：`ansible all -m shell -a 'echo "hello" >> /home/user'`

在 RHEL 系统上安装：`ansible all -m yum -a 'name=vim'`

在 Debian 系统上安装：`ansible all -m apt -a 'name=vim --update-cache'`

运行 `cron` 任务：`ansible all -m cron -a 'name=daily-cron-all-servers schedule=0 0 * * * job=/path/to/hour-cron-script'`

通过指定 15 分钟的 `cron`，对于那些每日或每周的任务也是特殊时间超时

- 使用列表项获取特定实体：`ansible all -m setup -a 'systemd' --limit=112.168.0.17` 限制匹配到此节点的一个 IP - 所有插件都可以使用 `"*44"` 通配符，你可以使用 `--limit="ansible:112.168.0.17"` 排除，使用 `--limit="ansible:!112.168.0.17"` 包含

- `B` 选项方法对于可能在后台运行一段时间的临时命令最有帮助，让你可以在终端中继续工作而不会超时。

- `setup` 模块访问 `_facts` 变量，可以对其进行过滤。使用过滤工具查找信息非常有用：

`ansible appsevers -m ansible_hosts -a 'filter=ansible_distribution,ansible_distribution_version,ansible_memfree_mb,ansible_mem_total_mb,ansible_processor_cores,ansible_architecture=2"/dev/null`

## Ansible 目录结构

`production`

`staging`

`group_vars/`

`group1.yml`

`group2.yml`

`host_vars/`

`hostname1.yml`

`hostname2.yml`

# 生产服务器的清单文件

# 测试环境的清单文件

# 我们为特定组分配变量

`library`

`module_utils/`

`filter_plugins/`

`site.yml`

`webservers.yml`

`dbserver.yml`

# 如果有任何自定义模块，放在这里（可选）

# 如果有支持模块的自定义 `module_utils`，放在这里（可选）

# 如果有任何自定义过滤器插件，放在这里（可选）

# 我们为特定系统分配变量

`roles/`

`common/`

`tasks/`

`main.yml`

`handlers/`

`main.yml`

`templates/`

`tp.conf.j2`

`files/`

`bar.txt`

`foo.sh`

`vars/`

`main.yml`

`defaults/`

`main.yml`

`meta/`

`library/`

`module_utils/`

`lookup_plugins/`

# 主剧本 (master playbook)

# Web服务器层的 playbook

# 数据库服务器层的 playbook

# 此层级结构代表一个“角色 (role)”

# <- 如果需要，tasks 可以包含更小的文件

# <- handlers 文件

# <- 用于模板资源的 files 文件夹

# <- templates 以 .j2 结尾

# <- 用于 copy 资源的文件

# <- 用于 script 资源的脚本文件

# <- 与此角色关联的变量

# <- 该角色的默认且低优先的变量

# <- 角色也可以包含自定义模块

# <- 其他类型的插件，例如本例中的 lookup

# 我们使用了与上面 "common" 相同的的结构，用于 Web 服务器层

# *

### 备选布局：

将每个清单及其对应的 `group_vars/host_vars` 放在单独的目录中。如果这些在不同环境之间没有太多共同点，则这种方法非常有用。

`inventories/`

`production/`

`group_vars/`

`group1.yml`

`group2.yml`

`host_vars/`

`hostname1.yml`

`hostname2.yml`

# 生产服务器的清单文件

# 我们为特定组分配变量
