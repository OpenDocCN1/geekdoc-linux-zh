
### 1.2. 创建 `repo_playbook.yml` playbook，该将在 `webservers` 主机组的受托管主机上运行。添加一个使用 `yum_repository` 模块的任务，以确保受托管主机内部 yum 仓库的配置。确保：
* 仓库配置存储在文件 `/etc/yum.repos.d/example.repo` 中
* 仓库 ID 为 `example-internal`
* base URL 为 `http://materials.example.com/yum/repository`
* 仓库配置为检查 RPM GPG 签名
* 仓库描述为 Example Inc. Internal YUM repo

## 第 10 章 | 自动化 Linux 管理任务

该 playbook 包含以下内容：

```yaml
- name: Repository Configuration
  hosts: webservers
  tasks:
    - name: Ensure Example Repo exists
      yum_repository:
        name: example-internal
        description: Example Inc. Internal Yum repo
        file: example
        baseurl: http://materials.example.com/yum/repository/
        gpgcheck: yes
```

### 1.3. 在 play 中添加一个任务，使用 `rpm-key` 模块以确保远程主机上存在仓库密钥。仓库密钥可以通过 `http://materials.example.com/repository/RPM-GPG-KEY-example` 获取。该任务显示为：

```yaml
- name: Ensure Repo Key is Installed
  rpm_key:
    key: http://materials.example.com/repository/RPM-GPG-KEY-example
    state: present
```

### 1.4. 在 play 中添加一个任务，使用 `yum_repository` 模块安装该仓库中的 `example-mold` 软件包。该任务显示为：

```yaml
- name: Install example-mold
  yum_repository:
    name: example-mold
    state: present
```

### 1.5. 执行 playbook：

```
[student@workstation -~$ ansible-playbook repo_playbook.yml
```

```
PLAY (Repository Configuration)
************************************************

TASK (Gathering Facts)
************************************************
ok: [webservers]

TASK (Ensure Repo exists)
************************************************
changed: [webservers]

TASK (Ensure Repo Key is Installed)
************************************************
changed: [webservers]

TASK (Install example-mold)
************************************************
changed: [webservers]

PLAY RECAP
************************************************
webservers      : ok=4 changed=3 unreachable=0
failed=0

46 RH294-RHEL.8.0-en-1-20190531
```

## 自动化管理任务

### 2. 在 `webservers` 主机组上创建并执行一个 playbook，创建 `webadmin` 用户组，并向该组添加两个用户 `ops1` 和 `ops2`。

#### 2.1. 作为工作站用户，切换到 `/home/student/system-review` 工作目录。

```
[student@workstation -~$ mkdir vars

[student@workstation system-review~$ cd vars
```

#### 2.2. 创建 `users_playbook.yml` playbook，将在 `webservers` 主机组的受托管主机上运行。添加一个使用 `group` 模块的任务以确保受托管主机上 `webadmin` 组的配置。

```yaml
name: Create webadmin group

hosts: webservers

tasks:

  - name: Ensure webadmin group

    group:

      name: webadmin

      state: present
```

#### 2.3. 在 play 中添加一个任务，使用 `user` 模块将 `ops1` 和 `ops2` 添加到组。该任务显示为：

```yaml
- name: Add ops1 and ops2

  user:

    name: "{{ item }}"

    group: webadmin

    state: present

  loop:

    - ops1

    - ops2
```

#### 2.4. 执行 playbook：

```
[student@workstation system-review/vars~$ ansible-playbook users_playbook.yml
```

```
PLAY (Create webadmin group)
************************************************

TASK (Gathering Facts)
************************************************
ok: [webservers]

TASK (Ensure webadmin group)
************************************************
changed: [webservers]

TASK (Add ops1 and ops2)
************************************************
changed: [webservers] => (item=ops1)
changed: [webservers] => (item=ops2)
************************************************

PLAY RECAP
************************************************
webservers      : ok=3 changed=3 unreachable=0
failed=0
```

#### 2.5. 创建 `users_vars.yml` 文件。

```
[student@workstation system-review/vars~$ vi users_vars.yml
```

```yaml
users:

  - ops1

  - ops2
```

#### 2.6. 更新 `users_playbook.yml` 以使用变量和循环。

```yaml
name: Create users

hosts: webservers

vars_files:

  - users_vars.yml

tasks:

  - name: Add users

    user:

      name: "{{ item }}"

      group: webadmin

      state: present

    loop: "{{ users }}"
```

#### 2.7. 执行更新后的 playbook：

```
[student@workstation system-review/vars~$ ansible-playbook users_playbook.yml
```
