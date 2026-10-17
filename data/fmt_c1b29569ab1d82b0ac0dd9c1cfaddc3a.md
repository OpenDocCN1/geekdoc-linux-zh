
`var: file_contents`

## 设置 SSH 用户密钥

为了使用 SSH 从控制主机的用户账户连接到托管主机上的用户账户，你可能希望将本地用户的公钥复制到远程用户的 `~/.ssh/authorized_keys` 文件。如果目标 `authorized_keys` 文件只需要包含一个单一密钥，你可以使用 `copy` 模块将其拷贝过去。然而，如果你想在远程用户的 `authorized_keys` 文件中管理多个密钥，那么使用 `authorized_key` 模块会更好。从本质上，这个模块非常易用。

在列表 13-6 的示例中，你可以看到如何使用 `authorized_key` 模块为用户 `ansible` 拷贝 `authorized_key` 密钥。输入源使用了 `/home/ansible/.ssh/id_rsa.pub` 文件。使用查找插件来引用应该使用的文件内容。

### 列表 13-6 使用 authorized_key 模块

```yaml
---
- name: authorized_key simple demo
  hosts: ansible2
  tasks:
    - name: copy authorized key for ansible user
      authorized_key:
        user: ansible
        state: present
        key: "{{ lookup('file','/home/ansible/.ssh/id_rsa.pub') }}"
```

如果你理解列表 13-6 的工作原理，那么很容易增强该代码，使其对多个用户执行相同的操作。列表 13-7 显示了两个变量包含文件的内容，这些文件被应用于列表 13-8 的剧本中。

### 列表 13-7 列表 13-8 中变量文件

```bash
[ansible@control rhce8-book]$ cat vars/users
users:
  - username: linda
    groups: sales
  - username: lori
    groups: sales
  - username: lisa
    groups: account
  - username: lucy
    groups: account

[ansible@control rhce8-book]$ cat vars/groups
usergroups:
  - groupname: sales
  - groupname: account
```

### 列表 13-8 使用查找插件使用 authorized_key 模块

```yaml
---
- name: configure users with SSH keys
  hosts: ansible2
  vars_files:
```

列表 13-8 中最有趣的新部分是 `authorized_key` 模块，它被设置为对 `item.username` 进行操作，并对 `users` 变量使用循环。这种结构使得剧本能够应用于每个用户。注意，需要拷贝的 `id_rsa.pub` 文件预计存在 `files` 目录，该目录位于当前项目目录下。

将用户公钥拷贝到项目目录是解决一个难以处理的重要问题的方案：`authorized_key` 模块无法从隐藏目录读取文件。如果能使用 `key: "{{ lookup('file', '/home/' + item.username + '.ssh/id_rsa.pub') }}"` 就太好了，但这行不通。因此，为了让它运行，你需要应用一种变通方法。你在练习 13-2 的示例剧本中应用了这种变通方法。在开始练习之前，让我们先看看你在这个练习中具体要做什么。

在第一个任务中（见列表 13-9），你创建了一个本地用户并包含一个 SSH 密钥。因为 SSH 密钥应该包含其所应用的用户和主机名称，因此你需要使用 `generate_ssh_key` 参数以及 `ssh_key_comment` 参数向公钥中写入正确的注释。如果没有这些内容，密钥将具有通用内容且不被视为有效密钥。

### 列表 13-9 创建带有 SSH 密钥的用户

以这种方式创建 SSH 密钥后，你将无法直接从用户家目录获取密钥。为了解决这个问题，你在项目目录中创建一个与用户同名的目录，并使用 `shell` 模块从那里拷贝用户公钥。你可以在列表 13-9 中看到执行此操作的示例代码。

### 列表 13-10 将用户公钥拷贝到可以拷贝的位置

```yaml
- name: create directory to store the file
  file:
    path: "{{ item }}"
    state: directory
  loop:
    - "{{ user_home }}/.ssh"

- name: copy the User Public Key to Location It Can Be Copied
  shell: "cat {{ item }}/id_rsa.pub"
  loop:
    - "{{ user_home }}/.ssh"

- name: verify that file exists
  command: ls -l {{ item }}
  loop:
    - "{{ user_home }}/.ssh"
```

接下来，在第二个任务中，你创建用户并使用 `authorized_key` 模块从本地获取密钥，然后将其拷贝到远程用户家目录下的 `authorized_keys` 文件。

## 练习 13-2 使用密钥管理用户

1. 使用编辑器创建 `exercise132.yaml` 并编写第一个剧本，它在本地创建用户：

```yaml
---
- name: prepare localhost
  hosts: localhost
```

2. 注意使用了 `{{ username }}` 变量。运行剧本时，你需要通过 `-e username=sharon` 传递用户名。

3. 以下任务用于确保目录是可用的：

```yaml
- name: create directory to store the file
  file:
    path: "{{ item }}"
    state: directory
  loop:
    - "{{ user_home }}/.ssh"

- name: copy the user ssh key to temporary
  shell: "cat {{ item }}/id_rsa.pub > /tmp/rsa.pub"
  loop:
    - "{{ user_home }}/.ssh"

- name: verify that file exists
  command: ls -l {{ item }}
  loop:
    - "{{ user_home }}/.ssh"
```

4. 在此之后，用户公钥已创建，你可以编写第二个剧本。该第二个剧本使用 `user` 模块创建用户，并使用 `authorized_key` 模块从本地获取密钥，将其拷贝到远程用户家目录下的 `authorized_keys` 文件。

5. 此时，使用命令 `ansible-playbook exercise132.yaml -e username=radha` 为用户 `radha` 创建相应的 SSH 密钥。

6. 为了验证执行结果，在控制主机上使用 `sudo su - radha`，然后输入 `ssh` 命令。你应该不需要密码即可登录。

## 管理加密密码

在 Ansible 管理用户时，你可能还想设置用户密码。挑战在于，你不能直接将密码作为用户模块 `password` 参数的值，因为用户模块期望你使用加密字符串。

### 理解加密密码

当用户创建密码时，密码会被加密的。加密密码的哈希值存储在 `/etc/shadow` 文件中，该文件经过严格保护，只有 root 权限可以访问。字符串看起来像这样：`$$237687687$9809erhb8oywy48oih290u09`。这个字符串包含三个元素，用 `$` 符号分隔：

- 使用的哈希算法
- 加密密码时使用的随机盐
- 用户密码的加密哈希值

当用户设置密码时，使用随机盐是为了防止具有相同密码的用户在 `/etc/shadow` 中具有相同的条目。盐和未加密密码结合并加密，生成存储在的加密哈希值。

根据此字符串，用户输入的密码将与 `/etc/shadow` 中的密码字段进行比对，如果匹配，则该用户通过身份验证。

### 生成加密密码

在使用 Ansible 的 `user` 模块创建用户时，有一个 `password` 选项。该选项无法生成加密密码。它期望一个加密密码字符串作为输入。这意味着必须使用外部工具来生成加密字符串。该加密字符串必须存储在变量中以创建密码。由于该变量本质上是用户密码，因此该变量应安全地存储在（例如）Ansible Vault 安全的文件中。

要生成加密变量，你可以选择在创建用户账户之前创建该变量。或者，你可以在 playbook 中运行创建变量的命令，使用 `register` 将结果写入变量，然后使用该变量创建加密用户。如果你想预先生成变量，可以使用以下 `ansible` 命令：

```
ansible localhost -m debug -a "msg={{ 'password' | password_hash('sha512','myrandomomsalt') }}"
```

此命令生成了如列表 13-11 所示的加密字符串，该字符串随后可以在 playbook 中使用。此类 playbook 的示例如列表 13-12 所示。

#### 列表 13-11 生成加密密码字符串

```
[ansible@control ~]$ ansible localhost -m debug -a "msg={'password': password_hash('sha512','myrandomomsalt') }}"
localhost SUCCESS => (
"$6MyrandomomsaltSMcEB.xAVUe0/6XqZe8n/7k9VV/Gxndy9nIMLyQAi
PnyhoBctToMbWX2vA4f.Uv9PnPrAYUUc76ajlWAX6U10")
```

#### 列表 13-12 创建加密用户密码的示例 Playbook

这里使用的方法有效但并不优雅。首先，你需要预先手动生成加密密码。此外，加密密码字符串在 playbook 中是以可见方式使用的。通过查看加密密码和盐（salt），有可能获取原始密码，这就是为什么在安全环境中，密码不应该在 playbook 中可见。

在练习 13-3 中，你创建了一个提示用户密码并使用 `debug` 模块的 playbook，该模块在 playbook 内部配合列表 13-11 结合 `register` 使用，使得密码不再以明文形式可见。但在查看练习 13-3 之前，让我们先看另一种同样有效的替代方法。

> **考试技巧**
> 在创建用户账户时使用加密密码的过程记录在 Ansible 文档的“常见问题”中。由于考试时可以查阅文档，请确保你知道在哪里可以找到这些信息！搜索项目“我如何为 `user` 模块生成加密密码？”

### 使用替代方法

正如多次提到的，在 Ansible 中，对于同一个优雅的问题，通常有不同的解决方案。有时，除了最优雅的解决方案外，还有一种“快速且粗暴”的解决方案，这对于设置用户加密密码同样适用。与其使用上一节“生成加密密码”中描述的解决方案，不如你可以使用 Linux 命令 `echo password | passwd --stdin` 来设置用户密码。列表 13-13 显示了如何操作。请注意，此示例侧重于如何操作，而不是安全性。如果你想让 playbook 更安全，将密码存储在 Ansible Vault 中会更好。

#### 列表 13-13 设置用户密码：替代方案

```yaml
---
- name: create user with encrypted password
  hosts: ansible3
  vars:
    password: mypassword
    user: anna
  tasks:
    - name: configure user {{ user }}
      user:
        name: "{{ user }}"
        groups: wheel
        append: yes
        state: present
    - name: set a password for {{ user }}
      shell: 'echo {{ password }} | passwd --stdin {{ user }}'
```

### 练习 13-3 使用加密密码创建用户

1. 使用你的编辑器创建文件 `exercise133.yaml`。
2. 按照如下内容编写 play 头：

```yaml
---
- name: create user with encrypted password
  hosts: ansible3
  vars_prompt:
    - name: password
      prompt: which password do you want to use
  vars:
    user: sharon
  tasks:
```

3. 添加第一个使用 `debug` 模块的任务来生成加密密码字符串并使用 `register` 将字符串存储在变量 `mypass` 中：

```yaml
- debug:
    msg: "{{ password }}|password_hash('sha512','myrandomsalt') }}"
  register: mypass
```

4. 添加一个 `debug` 模块来分析注册变量的精确格式：

```yaml
- debug:
    var: mypass
```

5. 使用 `ansible-playbook exercise133.yaml` 首次运行 playbook，这样你就可以看到必须使用的变量精确名称。这段代码显示 `mypass.msg` 变量包含了加密密码字符串（参见列表 13-14）。

#### 列表 13-14 查找变量

```
TASK [debug] *************************************************
ok SUCCESS => {
    "msg": "$6MyrandomomsaltSMcEB.xAVUe0/6XqZe8n/7k9VV/Gxndy9nIMLyQAiPnyhoBctToMbWX2vA4f.Uv9PnPrAYUUc76ajlWAX6U10",
    "changed": false
}
```

6. 根据输出，现在可以使用该变量。添加以下任务：

```yaml
- name: configure user
  user:
    name: "{{ user }}"
    password: "{{ mypass.msg }}"
```

7. 使用 `ansible-playbook exercise133.yaml` 首次运行 playbook，以便你看到必须使用的变量的精确名称。

```
TASK [debug] *************************************************
ok SUCCESS => {
    "msg": "$6MyrandomomsaltSMcEB.xAVUe0/6XqZe8n/7k9VV/Gxndy9nIMLyQAiPnyhoBctToMbWX2vA4f.Uv9PnPrAYUUc76ajlWAX6U10",
    "changed": false
}
```

# 管理用户

## 高级场景

## 练习

现在是处理一个高级场景了。在练习中，你将创建几个用户。这些用户需要在本地主机和托管主机上创建，运行 playbook 后，本地创建的任何用户都通过 SSH 密钥登录远程主机而无需输入密码。请确保设置满足以下要求：

- `sharon`、`blair`、`ashley` 和 `ahmed`。
- 用户 `sharon` 和 `blair` 属于 `admins` 组；`ashley` 和 `ahmed` 属于 `students` 组。
- 在托管主机上，`admins` 组的成员应具有运行任何命令的 `sudo` 权限。
- 所有用户必须配置默认密码 “password”。

1. 这次你将使用不同的方法并先设置 playbook 的框架。这可以减少遗漏任何内容的概率。为此，使用你的编辑器创建一个名为 `exercise134.yaml` 的文件，并根据以下示例定义你打算用于每个任务的 play 头和模块：

```yaml
---
- name: create users on localhost
  hosts: localhost
  tasks:
    - name: create groups
      groups:
    - name: create users
      users:

- name: create users on managed hosts
  hosts: ansible4
  tasks:
    - name: create groups
      groups:
    - name: create users
      users:
    - name: copy authorized keys
      authorized_key:
    - name: modify sudo configuration
      template:
```

2. 现在既然你已经定义了全局结构，就可以开始填充细节。从第一个 play 开始，它应该从创建用户账户开始。首先，关注基础设置：

```yaml
---
- name: create users on localhost
  hosts: localhost
  vars:
    users:
```
