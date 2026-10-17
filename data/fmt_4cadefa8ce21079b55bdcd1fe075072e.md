
### 4. 角色文档包含每个角色变量的描述，包括该变量的默认值。确定需要覆盖的角色变量以满足时间同步的要求。

将角色变量值放置在名为 `timesync.yml` 的文件中。由于这些值适用于清单中的所有主机，请将 `timesync.yml` 文件放置在 `group_vars/all` 子目录下。

#### 4.1. 查看 `rhel-system-timesync` 角色的 `README.md` 中的 Role Variables 章节。

```bash
[student@workstation role-system]$ cat \
> /share/doc/rhel-system-roles/timesync/README.md
> ...output omitted.
Role Variables
```

```yaml
...output omitted.
## List of NTP servers:
timesync_ntp_servers:
  hostname: foo.example.com  # 服务器的主机或地址
  minpoll: 4                  # 最小轮间隔 (默认 6)
  maxpoll: 8                  # 最大轮间隔 (默认 10)
  burst: yes                   # 启用快速启动的标记
  synchronization:           # (默认 no)
    pool: no                  # 表示主机名解析出的每个
      address               # 都是独立 NTP 服务器的标记
  ...output omitted...
 (default no)
# 应为 NTP 安装并配置的软件包包名。
```

#### 4.2. 创建 `group_vars/all` 子目录

```bash
[student@workstation role-system]$ mkdir -pv group_vars/all
mkdir: created directory group_vars
mkdir: created directory group_vars/all
```

#### 4.3. 使用文本编辑器创建一个新文件 `group_vars/all/timesync.yml`。添加变量定义以满足时间同步需求。该文件现在包含：

```yaml
## rhel-system-roles.timesync variables for all hosts
timesync_ntp_provider: chrony
timesync_ntp_servers:
  hostname: classroom.example.com
  iburst: yes
```

### 5. 在 `configure_time.yml` 中添加一个任务来为每个主机设置时区。确保该任务使用 `timezone` 模块并在 `Rhel-system-roles.timesync` 角色之后执行。由于主机不属于同一个时区，请使用变量 `host_timezone` 作为时区名称。

#### 5.1. 查看 `timezone` 模块文档中的 Examples 章节。

#### 5.2. 在 `configure_time.yml` playbook 的 play 的 `post_tasks` 部分添加一个任务。参考文档中的示例编写该任务，但使用 `host_timezone` 变量作为时区名称。

`ansible-doc timezone` 中的文档建议，如果模块更改了时区，应重启 Cron 服务，以确保 Cron 任务在正确的时间运行。为任务添加一个 `notify` 关键字，其关联的值为 `restart crond`。play 的 `post_tasks` 部分应如下：

```yaml
post_tasks:
  name: Set timezone
  timezone:
    name: "{{ host_timezone }}"
  notify: restart crond
```

#### 5.3. 将 `restart crond` 处理器添加到 `Time Synchronization` play 中。现在完整的 playbook 包含：

```yaml
---
- name: Time Synchronization
  hosts: database_servers
roles:
  - rhel-system-roles.timesync
post_tasks:
  name: Set timezone
  timezone:
    name: "{{ host_timezone }}"
  notify: restart crond
handlers:
  name: restart crond
  service:
    name: crond
    state: restarted
```

### 6. 为每个数据中心创建一个名为 `timezone.yml` 的文件，其中包含适用于 `host_timezone` 变量的适当值。使用 `timedatectl list-timezones` 命令查找每个数据中心有效的时区字符串。

#### 6.1. 为 `na_datacenter` 和 `european_datacenter` 主机组创建 `group_vars` 子目录。

```bash
$[workstation role-system]$ mkdir -pv \
> group_vars/{na_datacenter,europe_datacenter}
mkdir: created directory 'group_vars/na_datacenter'
mkdir: created directory 'group_vars/europe_datacenter'
```

#### 6.2. 使用 `timedatectl list-timezones` 命令确定美国和欧洲数据中心的时区：

```bash
$[workstation role-system]$ timedatectl list-timezones | grep
America/Chicago
$[workstation role-system]$ timedatectl list-timezones | grep
Helsinki
Europe/Helsinki
```

#### 6.3. 为两个数据中心创建 `timezone.yml`：

```bash
$[workstation role-system]$ echo "host_timezone: America/
Chicago" > \
> group_vars/na_datacenter/timezone.yml
$[workstation role-system]$ echo "host_timezone: Europe/
Helsinki" > \
> group_vars/europe_datacenter/timezone.yml
```

### 7. 运行 playbook。
